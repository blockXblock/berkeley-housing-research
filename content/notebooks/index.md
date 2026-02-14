---
title: Jupyter Notebooks
---

# Computational Notebooks

Interactive Jupyter notebooks for Berkeley housing analysis.

## 🚀 Quick Start

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/blockXblock/berkeley-housing-analysis/main)

Click above to launch all notebooks in your browser (no installation required!)

---

## 📊 Workflow Notebooks

### A. Data Collection & Processing

1. **[A1: Data Sources Setup](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A1_data_sources_setup.ipynb)**
   - Connect to Berkeley Open Data
   - API configuration
   - Dataset discovery

2. **[A2: Address Standardization](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A2_address_standardization.ipynb)**
   - Clean address data
   - Standardize formats
   - Handle variations

3. **[A3: Geocoding Pipeline](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/A_data_collection/A3_geocoding_pipeline.ipynb)**
   - Convert addresses to coordinates
   - 100% geocoding success
   - Alameda County lookup integration

### B. Timeline Tracking

4. **[B1: Lifecycle Tracking](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B1_lifecycle_tracking.ipynb)**
   - Track project from proposal to completion
   - Identify bottlenecks
   - Timeline visualization

5. **[B2: Status Classification](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B2_status_classification.ipynb)**
   - Categorize project status
   - Standardize status codes
   - Progress tracking

6. **[B3: Progress Indicators](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B3_progress_indicators.ipynb)**
   - Calculate progress metrics
   - Identify stalled projects
   - Predict completion dates

### C. Analysis

7. **[C1: Pipeline Analysis](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C1_pipeline_analysis.ipynb)**
   - Analyze housing pipeline
   - Development trends
   - Geographic patterns

8. **[C2: Timeline Analysis](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C2_timeline_analysis.ipynb)**
   - Review process timelines
   - Approval durations
   - Seasonal patterns

9. **[C3: Proposal vs Reality](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/C_analysis/C3_proposal_vs_reality.ipynb)**
   - Compare proposed vs built units
   - Analyze changes during review
   - Outcome assessment

### D. Reporting & Monitoring

10. **[D1: Monthly Report Generator](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D1_monthly_report_generator.ipynb)**
    - Generate automated reports
    - Track monthly progress
    - Export visualizations

11. **[D2: Dashboard Data Export](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D2_dashboard_data_export.ipynb)**
    - Prepare data for dashboards
    - Create summary statistics
    - Export for visualization tools

12. **[D3: Alerts & Monitoring](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/D_reporting/D3_alerts_monitoring.ipynb)**
    - Monitor for anomalies
    - Identify stalled projects
    - Generate alerts

---

## 🎓 Complete Analysis

**[MASTER_ANALYSIS.ipynb](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/notebooks/MASTER_ANALYSIS.ipynb)**

Comprehensive analysis combining all workflows. Best for:
- Understanding the complete pipeline
- Reproducing all results
- Learning the full methodology

---

## 💻 Running Locally
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

## 📚 Learning Path

**Beginners:** Start with A1 → A2 → A3  
**Intermediate:** Add B1 → C1  
**Advanced:** Explore full workflow A→B→C→D  
**Researchers:** Use MASTER_ANALYSIS.ipynb

---

## 🔗 Resources

- [Live Database](https://berkeley-housing.fly.dev/)
- [Documentation](/documentation)
- [GitHub Repository](https://github.com/blockXblock/berkeley-housing-analysis)
