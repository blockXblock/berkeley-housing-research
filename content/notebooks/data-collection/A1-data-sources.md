---
title: "A1: Data Sources Setup"
---

# A1: Data Sources Setup

**Workflow:** Data Collection  
**Level:** Beginner  
**Time:** 30 minutes

## 📋 Overview

Sets up connections to Berkeley Open Data Portal and configures API access for downloading permit data.

## 🎯 What You'll Learn

- How to connect to Socrata Open Data APIs
- Berkeley's dataset structure and IDs
- Handling API authentication
- Understanding API rate limits and blocks
- Manual download workarounds

## 🔑 Key Concepts

### API Access Challenge
Berkeley's Open Data Portal blocks most API requests with 403 errors due to Web Application Firewall (WAF) protection. This notebook demonstrates:
- ✅ How APIs *should* work
- ❌ Why Berkeley blocks access
- 💡 Manual download workarounds

### Dataset IDs
```python
DATASETS = {
    'building_permits': 'ydr8-5enu',
    'zoning_permits': 'vkhm-tsvp',
    'business_licenses': 'rwnf-bu3w',
    'planning_records': 'rk4r-58ys'
}
```

## 📊 Outputs

- API client configuration
- Understanding of data availability
- Manual download instructions
- CSV files ready for processing

## 🚀 Running This Notebook

**In Colab:**
```
https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb
```

**Locally:**
```bash
jupyter notebook workflows/A_data_collection/A1_data_sources_setup.ipynb
```

## 📚 Related Notebooks

**Next:** [A2: Address Standardization](A2-address-standardization.md)  
**Uses:** Manual CSV downloads from Berkeley Open Data

## 💡 Real-World Lesson

This notebook teaches a critical data science skill: **working around API limitations**. Many cities block programmatic access, requiring manual workflows.

---

[← Back to Notebooks](Project-Tool-1%20-%20Net%20Present%20Value.md) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)
