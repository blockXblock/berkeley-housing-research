---
title: "B3: Progress Indicators"
---

# B3: Progress Indicators

**Workflow:** Timeline Tracking  
**Level:** Advanced  
**Time:** 60 minutes

## 📋 Overview

Calculates quantitative progress metrics for housing projects and identifies stalled or delayed developments.

## 🎯 What You'll Learn

- Calculating project completion percentages
- Inspection-based progress tracking
- Identifying stalled projects
- Predicting completion dates
- Creating progress dashboards

## 🔑 Progress Metrics

### Inspection-Based Progress
```python
INSPECTION_SEQUENCE = [
    'Foundation',          # 10%
    'Framing/Rough',      # 25%
    'MEP Rough',          # 40%
    'Insulation',         # 55%
    'Drywall',            # 70%
    'MEP Final',          # 85%
    'Final Inspection',   # 95%
    'Certificate of Occupancy'  # 100%
]
```

### Progress Calculation
```python
def calculate_progress_percent(inspections_completed):
    """
    Calculate project completion based on inspections
    
    Args:
        inspections_completed: List of completed inspections
        
    Returns:
        Percentage complete (0-100)
    """
    
    if 'Certificate of Occupancy' in inspections_completed:
        return 100
    
    # Find highest completed inspection
    sequence_index = 0
    for inspection in inspections_completed:
        if inspection in INSPECTION_SEQUENCE:
            idx = INSPECTION_SEQUENCE.index(inspection)
            sequence_index = max(sequence_index, idx)
    
    # Map to percentage
    progress_map = {
        0: 10, 1: 25, 2: 40, 3: 55,
        4: 70, 5: 85, 6: 95, 7: 100
    }
    
    return progress_map.get(sequence_index, 0)
```

## 📊 Stalled Project Detection

### Criteria for "Stalled"
```python
def identify_stalled_projects(df, threshold_days=180):
    """
    Flag projects with no activity for extended period
    """
    
    today = pd.Timestamp.now()
    
    df['days_since_last_activity'] = (
        today - df['last_inspection_date']
    ).dt.days
    
    df['is_stalled'] = (
        (df['days_since_last_activity'] > threshold_days) &
        (df['status'] != 'completed')
    )
    
    return df
```

### Stalled Project Analysis
**Berkeley findings:**
- 8 projects stalled (>180 days no activity)
- Average stall duration: 347 days
- Common causes: Appeals, permit modifications, financing

## 🎯 Completion Prediction

### Model Approach
```python
def predict_completion_date(project):
    """
    Predict completion based on progress and historical data
    """
    
    # Calculate average time per percentage point
    similar_projects = get_similar_projects(project)
    avg_days_per_percent = similar_projects['total_days'].mean() / 100
    
    # Calculate remaining percentage
    remaining_percent = 100 - project['progress_percent']
    
    # Predict remaining days
    predicted_days = remaining_percent * avg_days_per_percent
    
    # Add to last activity date
    predicted_completion = (
        project['last_activity_date'] + 
        pd.Timedelta(days=predicted_days)
    )
    
    return predicted_completion
```

## 📊 Dashboard Metrics

### Key Performance Indicators
- **Active projects:** Count and progress distribution
- **Average completion:** X% complete
- **On-track projects:** Meeting timeline expectations
- **At-risk projects:** Behind schedule or stalled
- **Predicted completions:** Next 6/12 months

## 📊 Outputs

- `project_progress.csv` - All projects with progress %
- `stalled_projects.csv` - Flagged delayed projects
- Progress distribution charts
- Completion prediction timeline
- Risk assessment dashboard

## 🚀 Running This Notebook

**Locally:**
```bash
jupyter notebook workflows/B_timeline_tracking/B3_progress_indicators.ipynb
```

**Required Inputs:**
- Classified projects from B2
- Inspection records
- Historical timeline data

## 📚 Related Notebooks

**Previous:** [B2: Status Classification](B2-status.md)  
**Next:** [C1: Pipeline Analysis](../analysis/C1-pipeline.md)  
**Feeds into:** [D3: Alerts & Monitoring](../reporting/D3-alerts.md)

## 💡 Urban Planning Value

**Why progress tracking matters:**
- City can prioritize inspection resources
- Developers can benchmark their progress
- Community sees real progress on housing
- Early warning for troubled projects

---

[← Back to Notebooks](/notebooks) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B3_progress_indicators.ipynb)
