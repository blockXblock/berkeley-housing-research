---
title: "A1: Data Sources Setup"
---

# A1: Data Sources Setup

**Workflow:** Data Collection  
**Level:** Beginner  
**Time:** 30 minutes

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockxblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)

---

## 📋 Overview

Connects to Berkeley Open Data Portal and demonstrates both API access and manual download workflows for permit data.

**Updated:** Now includes execution timestamps and comprehensive error handling!

---

## 🎯 What You'll Learn

### Working with APIs
- Connect to Socrata Open Data APIs
- Handle API authentication with app tokens
- Understand rate limits and access restrictions
- Debug API errors (especially 403 Forbidden)

### Real-World Data Collection
- **Success case:** Business licenses API (works!)
- **Blocked case:** Zoning & building permits (403 errors)
- **Workarounds:** Manual CSV and Excel downloads
- **Documentation:** Why this happens and how to handle it

### Execution Tracking
- Add timestamps to cells
- Monitor execution duration
- Track which cells completed successfully
- Debug workflow timing issues

---

## 🔑 Key Concepts

### Berkeley's Web Application Firewall (WAF)

**The Challenge:**
Berkeley blocks most API requests with 403 Forbidden errors to prevent server overload.

**What Works:**
- ✅ **Business Licenses API** - Full programmatic access
- ❌ **Zoning Permits** - Blocked by WAF
- ❌ **Building Permits** - Blocked by WAF

**This is a feature, not a bug!** It teaches students:
1. How APIs should work (business licenses example)
2. Real barriers they'll encounter (WAF blocks)
3. Professional workarounds (manual downloads)
4. Complete documentation practices

---

## 📊 Data Sources Covered

### 1. Business Licenses (API)
```python
DATASETS = {
    'business_licenses': 'rwnf-bu3w',  # ✅ API works!
}

df_business = fetch_berkeley_data('business_licenses', limit=10000)
# Successfully fetches ~2,800 active licenses
```

### 2. Zoning Permits (Manual Excel)
**Source:** Accela Planning Portal  
**Format:** Excel (.xlsx)  
**Manual Steps:**
1. Visit: https://aca-prod.accela.com/BERKELEY/Cap/CapHome.aspx?module=Planning
2. Export "Active Zoning Projects"
3. Save as: `inputs/Active_Zoning_Projects.xlsx`

**Notebook handles:**
```python
df_zoning = pd.read_excel('inputs/Active_Zoning_Projects.xlsx')
# Loads 84+ housing projects
```

### 3. Building Permits (Manual CSV)
**Source:** Berkeley Open Data Portal  
**Format:** CSV  
**Manual Steps:**
1. Visit: https://data.cityofberkeley.info/d/ydr8-5enu
2. Click: Export → CSV
3. Save as: `inputs/building_permits_raw.csv`

**Notebook handles:**
```python
df_building = pd.read_csv('inputs/building_permits_raw.csv')
# Filters to housing-related permits
```

---

## 🛠️ New Features

### Execution Timestamps
Every major cell now includes:
```python
timer_start()
# Cell code here
timer_end()
```

**Shows:**
- 🕐 Start time
- 🕐 End time  
- ⏱️ Duration in seconds

**Why this matters:**
- Track which cells are slow
- Debug execution order
- Document when analysis was run
- Identify performance bottlenecks

### Better Error Messages
```python
try:
    df = fetch_data(...)
except Exception as e:
    print(f"❌ Error: {e}")
    if '403' in str(e):
        print("→ This dataset is blocked by WAF")
        print("→ Use manual download instead")
```

### Data Summary
Final cell shows:
```
📊 DATA COLLECTION SUMMARY
✅ Business Licenses  (API)    - 2,847 records
✅ Zoning Permits     (Excel)  - 84 records
✅ Building Permits   (CSV)    - 512 records
```

---

## 📊 Expected Outputs

After running all cells:

**If all manual files present:**
```
✅ Business licenses: ~2,800 records (API)
✅ Zoning permits: ~84 projects (Excel)
✅ Building permits: ~500 housing permits (CSV)
```

**If manual files missing:**
```
✅ Business licenses: ~2,800 records (API)
⚠️  Zoning permits: Download required
⚠️  Building permits: Download required
```

Clear instructions show exactly what to do next!

---

## 🚀 Running This Notebook

### In Google Colab
1. Click the blue Colab badge above
2. Notebook opens in browser (no installation!)
3. Run cells in order
4. Upload manual files if prompted

### Locally
```bash
# Clone repository
git clone https://github.com/blockXblock/berkeley-housing-analysis.git
cd berkeley-housing-analysis/workflows/A_data_collection

# Activate environment
conda activate jupyter_env

# Launch
jupyter notebook A1_data_sources_setup.ipynb
```

---

## 📚 Related Notebooks

**Next Steps:**
- [A2: Address Standardization](A2-address-standardization.md) - Clean the addresses
- [A3: Geocoding Pipeline](A3-geocoding.md) - Add coordinates

**Uses This Data:**
- All B-series notebooks (timeline tracking)
- All C-series notebooks (analysis)
- MASTER_ANALYSIS.ipynb

---

## 💡 Teaching Value

### For Students
This notebook demonstrates:
- ✅ Professional API usage
- ✅ Error handling strategies
- ✅ Real-world workarounds
- ✅ Documentation practices
- ✅ Execution monitoring

### For Instructors
Perfect for teaching:
- API basics (working example with business licenses)
- Real barriers (WAF blocks, 403 errors)
- Backup strategies (manual downloads)
- Code quality (timestamps, error messages)

---

## 🔗 Resources

- **Live Demo:** [Launch in Colab](https://colab.research.google.com/github/blockxblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)
- **Source Code:** [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)
- **Dataset:** [Berkeley Open Data](https://data.cityofberkeley.info/)
- **Documentation:** [Berkeley API Guide](/research/api-requirements)

---

## ⚠️ Common Issues

**"403 Forbidden" error:**
- Expected! Berkeley blocks these endpoints
- Use manual download instead
- See instructions in cell output

**"Module not found" error:**
- Run `!pip install sodapy` in Colab
- Or `conda install -c conda-forge sodapy` locally

**"File not found" error:**
- Manual download required
- Follow step-by-step instructions in cell output
- Check file is saved in `inputs/` directory

---

**Last Updated:** January 2026 - Added timestamps, improved error handling, manual download support
