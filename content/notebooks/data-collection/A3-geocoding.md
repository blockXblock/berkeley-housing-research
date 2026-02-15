---
title: "A3: Geocoding Pipeline"
---

# A3: Geocoding Pipeline

**Workflow:** Data Collection  
**Level:** Intermediate  
**Time:** 30 minutes

## 📋 Overview

Converts Berkeley addresses to latitude/longitude coordinates using Alameda County's comprehensive address database.

## 🎯 What You'll Learn

- Geocoding strategies and services
- Using lookup tables vs APIs
- Achieving 100% geocoding success
- Validating coordinate quality
- Handling coordinate systems (EPSG:4326)

## 🔑 Methodology

### Why Lookup Table over API?

**Traditional geocoding services:**
- ❌ Cost money (Google, Mapbox)
- ❌ Rate limits
- ❌ Can be inaccurate for new construction
- ❌ Require internet connection

**Alameda County lookup:**
- ✅ Free
- ✅ No rate limits
- ✅ 563,000 addresses
- ✅ Works offline
- ✅ County-maintained accuracy

### Geocoding Process
```python
# 1. Load lookup table (563k addresses)
lookup = pd.read_csv('alameda_lookup_complete.csv')

# 2. Standardize addresses for matching
df['address_clean'] = df['address'].apply(normalize_address)

# 3. Merge on standardized address
df = df.merge(lookup[['address', 'latitude', 'longitude']], 
              on='address_clean', how='left')

# 4. Validate coordinates
assert df['latitude'].notna().all()  # 100% success!
```

## 📊 Success Metrics

- **Total addresses:** 84 housing projects
- **Geocoded:** 84 (100%)
- **Within Berkeley bounds:** 84 (100%)
- **Average accuracy:** Parcel-level (<10m)

## 🗺️ Coordinate Validation

### Berkeley Bounding Box
```python
BERKELEY_BOUNDS = {
    'lat_min': 37.845,
    'lat_max': 37.915,
    'lon_min': -122.325,
    'lon_max': -122.235
}
```

All coordinates verified within city limits.

## 📊 Outputs

- `housing_projects_geocoded.csv` - All addresses with coordinates
- Quality report with validation statistics
- Map preview showing point distribution
- Failed geocoding report (if any)

## 🚀 Running This Notebook

**Locally:**
```bash
jupyter notebook workflows/A_data_collection/A3_geocoding_pipeline.ipynb
```

**Required Inputs:**
- Standardized addresses from A2
- `alameda_lookup_complete.csv` (563k addresses)

## 📚 Related Notebooks

**Previous:** [A2: Address Standardization](A2-address-standardization.md)  
**Next:** [B1: Lifecycle Tracking](../timeline-tracking/B1-lifecycle.md)  
**Uses output in:** All analysis notebooks

## 💡 Best Practice

**For other cities:**
- Check if county provides address/parcel databases
- Use official sources over commercial APIs
- Validate all coordinates within expected bounds
- Document any manual geocoding needed

## 🔗 Data Source

**Alameda County Address Database:**
- Public dataset
- Updated regularly
- Includes parcels, buildings, addresses
- Available at: data.acgov.org

---

[← Back to Notebooks](/notebooks) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A3_geocoding_pipeline.ipynb)
