# Database Creation Code

**Tags:** #code #sqlite

## Complete Script
```python
#!/usr/bin/env python3
import pandas as pd
import sqlite_utils

# Load CSV
df = pd.read_csv('housing_projects_final_complete.csv')
print(f"Loaded {len(df)} projects")

# Create database
db = sqlite_utils.Database('berkeley_housing.db')
db['projects'].insert_all(df.to_dict('records'), replace=True)

# Create indexes
db['projects'].create_index(['year'])
db['projects'].create_index(['net_units'])
db['projects'].create_index(['latitude', 'longitude'])

# Create map view
db.execute("""
CREATE VIEW IF NOT EXISTS map_view AS
SELECT 
    address_display as address,
    net_units, year, status, street,
    latitude, longitude,
    CASE 
        WHEN net_units >= 200 THEN '🔴 200+ units'
        WHEN net_units >= 100 THEN '🟠 100-199 units'
        WHEN net_units >= 50 THEN '🔵 50-99 units'
        WHEN net_units >= 20 THEN '🟢 20-49 units'
        ELSE '🔷 <20 units'
    END as size_category
FROM projects
WHERE latitude IS NOT NULL
""")

print("✅ Database created!")
```

## Validate Database
```python
import sqlite3

conn = sqlite3.connect('berkeley_housing.db')
cursor = conn.cursor()

# Check row counts
projects_count = cursor.execute("SELECT COUNT(*) FROM projects").fetchone()[0]
map_view_count = cursor.execute("SELECT COUNT(*) FROM map_view").fetchone()[0]

print(f"projects: {projects_count} rows")
print(f"map_view: {map_view_count} rows")
```

**Last Updated:** 2026-01-09
