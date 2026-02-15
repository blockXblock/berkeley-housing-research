---
title: "B1: Lifecycle Tracking"
---

# B1: Lifecycle Tracking

**Workflow:** Timeline Tracking  
**Level:** Intermediate  
**Time:** 45 minutes

## 📋 Overview

Tracks housing projects from initial proposal through completion, calculating timeline durations and identifying bottlenecks.

## 🎯 What You'll Learn

- Project lifecycle stages in Berkeley's process
- Calculating time between milestones
- Identifying process bottlenecks
- Timeline visualization techniques
- Predicting project duration

## 🔑 Project Stages

### Complete Lifecycle
```
1. Proposed → Pre-application meeting
2. Application Submitted → Under review
3. Planning Commission → Approval/conditions
4. Building Permit → Issued
5. Construction → Inspections
6. Certificate of Occupancy → Completed
```

### Key Metrics
- **Proposal to Permit:** Average 18-24 months
- **Permit to CO:** Average 12-18 months
- **Total timeline:** 30-42 months typical

## 📊 Data Requirements

**Input columns needed:**
- `proposal_date`
- `application_date`
- `planning_approval_date`
- `permit_issue_date`
- `construction_start_date`
- `completion_date` or `certificate_of_occupancy_date`

## 🛠️ Analysis Functions

### Timeline Calculations
```python
def calculate_lifecycle_stages(df):
    """Calculate duration for each stage"""
    
    df['proposal_to_permit'] = (
        df['permit_issue_date'] - df['proposal_date']
    ).dt.days
    
    df['permit_to_completion'] = (
        df['completion_date'] - df['permit_issue_date']  
    ).dt.days
    
    return df
```

### Bottleneck Identification
```python
def identify_bottlenecks(df):
    """Find stages taking longest"""
    
    # Calculate percentiles
    p75 = df['proposal_to_permit'].quantile(0.75)
    
    # Flag slow projects
    df['slow_approval'] = df['proposal_to_permit'] > p75
    
    return df
```

## 📊 Visualizations Included

1. **Gantt Chart** - All projects with timeline bars
2. **Stage Duration Boxplots** - Compare stage lengths
3. **Cumulative Timeline** - How long projects take overall
4. **Bottleneck Heatmap** - Which stages delay most projects

## 🎯 Key Findings

**From Berkeley data (2020-2025):**
- Planning review: 12-18 months median
- Permit issuance: 3-6 months after approval
- Construction: 12-24 months depending on size
- Projects >100 units: +6-12 months typical

## 📊 Outputs

- `project_lifecycles.csv` - Full timeline data
- Duration statistics by project size
- Bottleneck analysis report
- Timeline visualizations (PNG/HTML)

## 🚀 Running This Notebook

**Locally:**
```bash
jupyter notebook workflows/B_timeline_tracking/B1_lifecycle_tracking.ipynb
```

**Required Inputs:**
- Geocoded permits from A3
- Date fields for all lifecycle stages

## 📚 Related Notebooks

**Previous:** [A3: Geocoding Pipeline](../data-collection/A3-geocoding.md)  
**Next:** [B2: Status Classification](B2-status.md)  
**See also:** [C2: Timeline Analysis](../analysis/C2-timeline.md)

## 💡 Urban Planning Insights

**Why this matters:**
- Helps city identify process inefficiencies
- Developers can plan realistic timelines
- Community understands approval process
- Policy makers see impact of changes

---

[← Back to Notebooks](/notebooks) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B1_lifecycle_tracking.ipynb)
