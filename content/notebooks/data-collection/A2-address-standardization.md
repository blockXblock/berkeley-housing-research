---
title: "A2: Address Standardization"
---

# A2: Address Standardization

**Workflow:** Data Collection  
**Level:** Intermediate  
**Time:** 45 minutes

## 📋 Overview

Cleans and standardizes messy address data from building permits to prepare for geocoding.

## 🎯 What You'll Learn

- Parse unstructured address strings
- Extract street numbers, names, and types
- Handle address variations and abbreviations
- Standardize formats for geocoding
- Detect and fix common address errors

## 🔑 Key Techniques

### Address Parsing
```python
# Before: "2190 shattuck avenue apt 3"
# After:  "2190 SHATTUCK AVE"

def standardize_address(address):
    # Remove apartment/unit numbers
    # Standardize street types (AVE, ST, BLVD)
    # Uppercase for consistency
    # Remove extra whitespace
```

### Common Challenges

**Variations:**
- "Shattuck Ave" vs "Shattuck Avenue"
- "2190" vs "2190-2192" (ranges)
- "MLK Jr Way" vs "Martin Luther King Jr Way"

**Solutions:**
- Comprehensive abbreviation dictionary
- Range detection and splitting
- Named street lookup table

## 📊 Data Quality Metrics

- **Input:** ~500 raw permit addresses
- **Standardized:** 100% of valid addresses
- **Geocoding-ready:** 98%+ match rate

## 🛠️ Functions Provided

### Core Functions
```python
parse_address(address)           # Extract components
standardize_address(address)     # Clean format
get_street_variations(street)    # Handle variations
normalize_for_lookup(address)    # Prepare for geocoding
```

## 📊 Outputs

- `addresses_standardized.csv` - Clean addresses
- Quality report with match statistics
- List of addresses needing manual review

## 🚀 Running This Notebook

**Locally:**
```bash
jupyter notebook workflows/A_data_collection/A2_address_standardization.ipynb
```

**Required Inputs:**
- Raw permit CSV from A1
- Street variations lookup table

## 📚 Related Notebooks

**Previous:** [A1: Data Sources Setup](A1-data-sources.md)  
**Next:** [A3: Geocoding Pipeline](A3-geocoding.md)

## 💡 Key Learning

Address standardization is **critical** for geocoding success. Berkeley achieved 100% geocoding by:
1. Thorough address cleaning
2. Comprehensive lookup table (563k addresses)
3. Manual review of edge cases

---

[← Back to Notebooks](Project-Tool-1%20-%20Net%20Present%20Value.md) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A2_address_standardization.ipynb)
