# Working with Difficult Data Sources

**Tags:** #workarounds #education

## Common Obstacles

### 1. API Access Blocked (403 Forbidden)

**Berkeley's case:**
```python
response = requests.get('https://data.cityofberkeley.info/resource/ydr8-5enu.json')
print(response.status_code)  # 403 Forbidden
```

**Workaround: Manual Download**
```markdown
1. Visit dataset page
2. Click "Export" → "CSV"
3. Save to project directory
4. Document process in README
```

### 2. No API Available

**Solution: Web Scraping (Ethical)**
```python
import requests
from bs4 import BeautifulSoup

headers = {'User-Agent': 'Research Project (contact@example.com)'}
response = requests.get(url, headers=headers)
# Parse HTML...
time.sleep(2)  # Be polite
```

### 3. Freedom of Information Request

**Template:**
```
Subject: Public Records Request - Building Permit Data

I am requesting access to building permit records for 
educational research purposes...
```

## For Students

**Key lesson:** Real civic data work requires:
- Technical skills (APIs, scraping)
- Problem-solving (workarounds)
- Communication (working with officials)
- Persistence (trying multiple approaches)

**Last Updated:** 2026-01-09
