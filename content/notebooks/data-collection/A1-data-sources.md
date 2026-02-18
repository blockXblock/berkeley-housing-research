---
title: "A1: Data Sources Setup"
---

# A1: Data Sources Setup

**Workflow:** Data Collection  
**Level:** Beginner  
**Time:** 30 minutes

## 📋 Overview

Sets up connections to Berkeley Open Data Portal and configures API access for downloading permit data.
### This set of notebooks complement and support the City of Berkeley Annual Progress Update, to be submitted in March, 2026, to CA HCD per legal requirement. With adequate data upload access, we can replace the City's APR.
#### These notebooks are designed to extend the 2019 and 2023 Terner Center "Making It Pencil" series by David Garcia. The Terner Center created an illustrative website examining a small set of alternative options available to developers, but failed to present their calculations, choosing to show project facts: ft^2, units, rents, parking requirements, but not how they calculated whether the project was likely to be built. We can extend the Terner Center's vision by building computational notebooks for every potential project in Berkeley, both in and out of Berkeley's Permit PIpeline.

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
