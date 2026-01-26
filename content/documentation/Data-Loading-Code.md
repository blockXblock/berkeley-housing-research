# Data Loading Code Snippets

**Tags:** #code #data-loading #examples

---

## 📊 Loading from Different Sources

### 1. CSV Files
```python
import pandas as pd

# Basic CSV load
df = pd.read_csv('housing_projects.csv')

# With encoding specification
df = pd.read_csv('permits.csv', encoding='utf-8')

# With specific dtypes
df = pd.read_csv('permits.csv', dtype={
    'net_units': int,
    'year': int,
    'latitude': float,
    'longitude': float
})

# Skip bad lines
df = pd.read_csv('permits.csv', on_bad_lines='skip')

# Parse dates
df = pd.read_csv('permits.csv', parse_dates=['permit_date'])
```

---

### 2. Excel Files (.xlsx, .xls)
```python
import pandas as pd

# Read first sheet
df = pd.read_excel('building_permits.xlsx')

# Read specific sheet
df = pd.read_excel('building_permits.xlsx', sheet_name='Permits 2024')

# Read all sheets
excel_file = pd.ExcelFile('building_permits.xlsx')
print(f"Available sheets: {excel_file.sheet_names}")

sheets = {}
for sheet_name in excel_file.sheet_names:
    sheets[sheet_name] = pd.read_excel(excel_file, sheet_name=sheet_name)

# Combine multiple sheets
all_data = pd.concat(sheets.values(), ignore_index=True)

# Skip header rows
df = pd.read_excel('permits.xlsx', skiprows=3)

# Specify columns
df = pd.read_excel('permits.xlsx', usecols=['Address', 'Units', 'Year'])
```

---

### 3. Google Sheets
```python
import pandas as pd
import gspread
from oauth2client.service_account import ServiceAccountCredentials

# Method 1: Using gspread (requires API credentials)
scope = ['https://spreadsheets.google.com/feeds',
         'https://www.googleapis.com/auth/drive']

credentials = ServiceAccountCredentials.from_json_keyfile_name(
    'credentials.json', scope)
client = gspread.authorize(credentials)

# Open sheet
sheet = client.open('Berkeley Building Permits').sheet1
data = sheet.get_all_records()
df = pd.DataFrame(data)

# Method 2: Public sheet via URL
sheet_url = 'https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/export?format=csv'
df = pd.read_csv(sheet_url)

# Method 3: Using sheet ID
sheet_id = 'YOUR_SHEET_ID'
gid = '0'  # Sheet tab ID
url = f'https://docs.google.com/spreadsheets/d/{sheet_id}/export?format=csv&gid={gid}'
df = pd.read_csv(url)
```

---

### 4. PDF Files (Table Extraction)
```python
import pandas as pd
import tabula
import pdfplumber

# Method 1: Using tabula-py (Java-based)
# pip install tabula-py

# Extract all tables from PDF
tables = tabula.read_pdf('building_permits.pdf', pages='all')

# Extract from specific page
tables = tabula.read_pdf('building_permits.pdf', pages=1)

# Extract with specific area (coordinates)
tables = tabula.read_pdf(
    'building_permits.pdf',
    area=[50, 0, 800, 600],  # [top, left, bottom, right]
    pages=1
)

# Combine all tables
df = pd.concat(tables, ignore_index=True)

# Method 2: Using pdfplumber (Python-based, more flexible)
# pip install pdfplumber

with pdfplumber.open('building_permits.pdf') as pdf:
    tables = []
    
    for page in pdf.pages:
        # Extract tables from page
        page_tables = page.extract_tables()
        
        for table in page_tables:
            # Convert to DataFrame
            if table:
                df_page = pd.DataFrame(table[1:], columns=table[0])
                tables.append(df_page)
    
    # Combine all tables
    df = pd.concat(tables, ignore_index=True)

# Method 3: Extract text and parse manually
with pdfplumber.open('building_permits.pdf') as pdf:
    text = ''
    for page in pdf.pages:
        text += page.extract_text()
    
    # Parse text (custom logic needed)
    lines = text.split('\n')
    # Process lines...
```

---

### 5. PDF Files (Text Extraction with Patterns)
```python
import re
import pdfplumber
import pandas as pd

def extract_permits_from_pdf(pdf_path):
    """
    Extract building permit data from PDF using regex patterns
    """
    
    permits = []
    
    with pdfplumber.open(pdf_path) as pdf:
        for page in pdf.pages:
            text = page.extract_text()
            
            # Example pattern: "Address: 123 Main St, Units: 50"
            pattern = r'Address:\s*([^,]+),\s*Units:\s*(\d+)'
            
            for match in re.finditer(pattern, text):
                address = match.group(1).strip()
                units = int(match.group(2))
                
                permits.append({
                    'address': address,
                    'net_units': units
                })
    
    return pd.DataFrame(permits)

# Usage
df = extract_permits_from_pdf('building_permits.pdf')
print(f"Extracted {len(df)} permits from PDF")
```

---

### 6. Combining Multiple Files
```python
from pathlib import Path
import pandas as pd

# Load all CSVs from directory
data_dir = Path('permit_data')
csv_files = data_dir.glob('*.csv')

dfs = []
for csv_file in csv_files:
    print(f"Loading: {csv_file.name}")
    df = pd.read_csv(csv_file)
    df['source_file'] = csv_file.name
    dfs.append(df)

# Combine
df_combined = pd.concat(dfs, ignore_index=True)
print(f"Total rows: {len(df_combined)}")
```

---

### 7. API Data Retrieval (Socrata)
```python
import requests
import pandas as pd
import time

def download_socrata_data(domain, dataset_id, app_token=None, limit=None):
    """
    Download data from Socrata open data portal
    
    Args:
        domain: e.g., "data.cityofberkeley.info"
        dataset_id: e.g., "ydr8-5enu"
        app_token: Optional API token
        limit: Max rows to retrieve
    """
    
    base_url = f"https://{domain}/resource/{dataset_id}.json"
    
    headers = {}
    if app_token:
        headers['X-App-Token'] = app_token
    
    all_data = []
    offset = 0
    page_size = 1000
    
    while True:
        params = {
            '$limit': page_size,
            '$offset': offset
        }
        
        response = requests.get(base_url, headers=headers, params=params, timeout=30)
        
        if response.status_code != 200:
            print(f"Error {response.status_code}: {response.text}")
            break
        
        data = response.json()
        
        if not data:
            break
        
        all_data.extend(data)
        print(f"Downloaded {len(all_data)} rows...")
        
        if limit and len(all_data) >= limit:
            all_data = all_data[:limit]
            break
        
        if len(data) < page_size:
            break
        
        offset += page_size
        time.sleep(0.5)  # Be nice to API
    
    return pd.DataFrame(all_data)

# Usage
df = download_socrata_data(
    domain='data.cityofberkeley.info',
    dataset_id='ydr8-5enu',
    app_token='YOUR_TOKEN',
    limit=5000
)
```

---

### 8. Accela API (Permit Systems)
```python
import requests
import pandas as pd

def download_from_accela(base_url, api_key, module='Building', record_type='Permit'):
    """
    Download permits from Accela-based system
    
    Many cities use Accela for permit tracking
    """
    
    headers = {
        'x-accela-appid': api_key,
        'Content-Type': 'application/json'
    }
    
    params = {
        'module': module,
        'type': record_type,
        'limit': 1000,
        'offset': 0
    }
    
    all_records = []
    
    while True:
        response = requests.get(
            f"{base_url}/v4/records",
            headers=headers,
            params=params
        )
        
        if response.status_code != 200:
            print(f"Error: {response.status_code}")
            break
        
        data = response.json()
        records = data.get('result', [])
        
        if not records:
            break
        
        all_records.extend(records)
        print(f"Downloaded {len(all_records)} records...")
        
        params['offset'] += params['limit']
        time.sleep(1)
    
    return pd.DataFrame(all_records)
```

---

### 9. Handling Common Issues
```python
import pandas as pd
import chardet

# Detect encoding
with open('building_permits.csv', 'rb') as f:
    result = chardet.detect(f.read())
    encoding = result['encoding']

print(f"Detected encoding: {encoding}")
df = pd.read_csv('building_permits.csv', encoding=encoding)

# Handle different date formats
df = pd.read_csv('permits.csv', parse_dates=['permit_date'])

# If date parsing fails, convert manually
df['permit_date'] = pd.to_datetime(df['permit_date'], format='%m/%d/%Y', errors='coerce')

# Handle missing values
df = pd.read_csv('permits.csv', na_values=['N/A', 'NA', '', 'None', 'null'])

# Handle thousands separator
df = pd.read_csv('permits.csv', thousands=',')

# Handle different delimiters
df = pd.read_csv('permits.txt', sep='\t')  # Tab-separated
df = pd.read_csv('permits.txt', sep='|')   # Pipe-separated
```

---

### 10. Validate Loaded Data
```python
def validate_permit_data(df):
    """Validate loaded permit data"""
    
    print("🔍 VALIDATING DATA")
    print("="*70)
    
    # Check required columns
    required = ['address', 'net_units', 'year']
    missing = set(required) - set(df.columns)
    
    if missing:
        print(f"❌ Missing columns: {missing}")
        return False
    else:
        print(f"✅ All required columns present")
    
    # Check row count
    print(f"   Rows: {len(df):,}")
    
    # Check for nulls
    null_counts = df[required].isnull().sum()
    if null_counts.any():
        print(f"⚠️  Null values found:")
        for col in null_counts[null_counts > 0].index:
            print(f"   {col}: {null_counts[col]} nulls")
    else:
        print(f"✅ No null values in required columns")
    
    # Check data types
    if pd.api.types.is_numeric_dtype(df['net_units']):
        print(f"✅ net_units is numeric")
    else:
        print(f"⚠️  net_units is not numeric: {df['net_units'].dtype}")
    
    # Check value ranges
    if (df['net_units'] <= 0).any():
        print(f"⚠️  Found {(df['net_units'] <= 0).sum()} rows with units <= 0")
    
    print("="*70)
    return True

# Usage
df = pd.read_csv('building_permits.csv')
validate_permit_data(df)
```

---

**Last Updated:** 2026-01-09
