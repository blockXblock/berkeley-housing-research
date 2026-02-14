---
title: Jupyter Notebooks
---

# Computational Notebooks

Interactive Jupyter notebooks for Berkeley housing analysis.

## 🚀 Launch Options - Choose Your Platform

### ⚡ Google Colab (Recommended - Fast!)
- **Launch time:** 2-5 seconds
- **Best for:** Quick exploration, students with Google accounts
- **Click the blue Colab badge** next to any notebook below

### 🐳 Binder (Containerized Environment)
- **Launch time:** 1-2 minutes (builds complete environment)
- **Best for:** Reproducible environments, offline-capable
- **Click orange Binder badge** below to launch all notebooks

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/blockXblock/berkeley-housing-analysis/main)

*Note: Binder may occasionally hit rate limits. If it fails, use Colab or try again in 10 minutes.*

---

## 📊 Workflow Notebooks

### A. Data Collection & Processing

#### **[A1: Data Sources Setup](data-collection/A1-data-sources)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)

**What you'll learn:**
- Connect to Berkeley Open Data Portal
- Handle API authentication and rate limits
- Work around API blocks with manual downloads
- Real-world data access challenges

**Level:** Beginner | **Time:** 30 minutes

---

#### **[A2: Address Standardization](data-collection/A2-address-standardization)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A2_address_standardization.ipynb)

**What you'll learn:**
- Clean messy address data
- Handle variations and abbreviations
- Prepare addresses for geocoding
- Data quality validation

**Level:** Intermediate | **Time:** 45 minutes

---

#### **[A3: Geocoding Pipeline](data-collection/A3-geocoding)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A3_geocoding_pipeline.ipynb)

**What you'll learn:**
- Convert addresses to coordinates (100% success!)
- Use Alameda County lookup (563k addresses)
- Validate coordinate quality
- Why lookup tables beat APIs

**Level:** Intermediate | **Time:** 30 minutes

---

### B. Timeline Tracking

#### **[B1: Lifecycle Tracking](timeline-tracking/B1-lifecycle)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B1_lifecycle_tracking.ipynb)

**What you'll learn:**
- Track projects from proposal to completion
- Calculate timeline durations
- Identify process bottlenecks
- Visualize project lifecycles

**Level:** Intermediate | **Time:** 45 minutes

---

#### **[B2: Status Classification](timeline-tracking/B2-status)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B2_status_classification.ipynb)

**What you'll learn:**
- Standardize messy status categories
- Handle ambiguous classifications
- Build robust mapping schemes
- Data quality control

**Level:** Beginner | **Time:** 30 minutes

---

#### **[B3: Progress Indicators](timeline-tracking/B3-progress)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B3_progress_indicators.ipynb)

**What you'll learn:**
- Calculate project completion percentages
- Identify stalled projects
- Predict completion dates
- Create progress dashboards

**Level:** Advanced | **Time:** 60 minutes

---

### C. Analysis

#### **C1: Pipeline Analysis**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C1_pipeline_analysis.ipynb)

Analyze Berkeley's housing development pipeline, trends, and geographic patterns.

**Level:** Intermediate | **Time:** 45 minutes

---

#### **C2: Timeline Analysis**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C2_timeline_analysis.ipynb)

Review approval timelines, process durations, and seasonal patterns.

**Level:** Intermediate | **Time:** 45 minutes

---

#### **C3: Proposal vs Reality**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C3_proposal_vs_reality.ipynb)

Compare proposed vs built units, analyze changes during review process.

**Level:** Advanced | **Time:** 60 minutes

---

### D. Reporting & Monitoring

#### **D1: Monthly Report Generator**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D1_monthly_report_generator.ipynb)

Generate automated monthly reports with visualizations and statistics.

**Level:** Intermediate | **Time:** 45 minutes

---

#### **D2: Dashboard Data Export**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D2_dashboard_data_export.ipynb)

Prepare data for dashboards and visualization tools.

**Level:** Beginner | **Time:** 30 minutes

---

#### **D3: Alerts & Monitoring**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D3_alerts_monitoring.ipynb)

Monitor for anomalies, identify stalled projects, generate alerts.

**Level:** Advanced | **Time:** 60 minutes

---

## 🎓 Complete Analysis

### **[MASTER_ANALYSIS.ipynb](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/notebooks/MASTER_ANALYSIS.ipynb)**
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/blockXblock/berkeley-housing-analysis/blob/main/notebooks/MASTER_ANALYSIS.ipynb)

**Comprehensive analysis combining all workflows.**

Best for understanding the complete pipeline, reproducing all results, and learning the full methodology.

**Level:** Advanced | **Time:** 2+ hours

---

## 💻 Running Locally

Prefer to run on your own computer?
```bash
# Clone repository
git clone https://github.com/blockXblock/berkeley-housing-analysis.git
cd berkeley-housing-analysis

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

---

## 📚 Suggested Learning Paths

### 🟢 Beginners
Start here if you're new to data science or Python:
1. A1: Data Sources Setup
2. A2: Address Standardization
3. A3: Geocoding Pipeline
4. B2: Status Classification

### 🟡 Intermediate
Familiar with Python and pandas:
1. Complete A series (A1→A2→A3)
2. Add B1: Lifecycle Tracking
3. Try C1: Pipeline Analysis
4. Explore D1: Report Generator

### 🔴 Advanced
Experienced data scientists:
1. Start with MASTER_ANALYSIS.ipynb
2. Deep dive into C3: Proposal vs Reality
3. Explore B3: Progress Indicators
4. Build custom analyses using D series

### 🎓 Researchers & Students
Academic or research use:
1. Read all documentation first
2. Run complete A→B→C→D workflow
3. Review MASTER_ANALYSIS
4. Adapt for your city/region

---

## 🗂️ Dataset Information

**84 housing projects | 6,363 total units | 100% geocoded**

- Building permits (2015-2025)
- Zoning and planning data
- Timeline and status information
- Geographic coordinates

[Explore Live Database →](https://berkeley-housing.fly.dev/)

---

## 🔗 Additional Resources

- [Documentation](/documentation) - Detailed guides and tutorials
- [Research](/research) - API requirements and Clariti analysis
- [GitHub Repository](https://github.com/blockXblock/berkeley-housing-analysis) - Full source code
- [Live Database](https://berkeley-housing.fly.dev/) - Query housing data

---

## ❓ Need Help?

- **Issues with notebooks?** [Open an issue on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/issues)
- **Questions about methodology?** See [Documentation](/documentation)
- **Want to adapt for your city?** Check the [README](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/README.md)

---

*Last updated: January 2026*
