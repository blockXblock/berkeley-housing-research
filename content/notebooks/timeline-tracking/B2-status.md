---
title: "B2: Status Classification"
---

# B2: Status Classification

**Workflow:** Timeline Tracking  
**Level:** Beginner  
**Time:** 30 minutes

## 📋 Overview

Standardizes inconsistent status descriptions from permit records into clean, analyzable categories.

## 🎯 What You'll Learn

- Handling messy categorical data
- Creating standardized classification schemes
- Dealing with ambiguous statuses
- Building status transition matrices
- Tracking project state changes

## 🔑 Status Categories

### Standard Status Types
```python
STATUS_MAPPING = {
    'proposed': ['Proposed', 'Pre-Application', 'SB330 Preliminary'],
    'in_review': ['In Review', 'Under Review', 'Incomplete'],
    'approved': ['Approved', 'Conditionally Approved'],
    'appealed': ['Appealed', 'Appeal Pending'],
    'permitted': ['Permit Issued', 'Building Permit Issued'],
    'under_construction': ['Under Construction', 'Active'],
    'completed': ['Completed', 'CO Issued', 'Final Inspection'],
    'stalled': ['Stalled', 'Inactive', 'Expired'],
    'denied': ['Denied', 'Rejected', 'Withdrawn']
}
```

## 📊 Classification Challenges

### Ambiguous Status Examples

**"Pending Applicant"**
- Could be: in_review OR stalled
- Solution: Check last activity date

**"Conditionally Approved"**
- Could be: approved OR in_review
- Solution: Check if conditions met

**"Active Construction"**
- Could be: under_construction OR completed
- Solution: Check for CO date

## 🛠️ Classification Function
```python
def classify_project_status(status_text, last_activity_date):
    """
    Classify project status from text description
    
    Args:
        status_text: Raw status string
        last_activity_date: Date of last activity
        
    Returns:
        Standardized status category
    """
    
    # Check for exact matches first
    for category, variations in STATUS_MAPPING.items():
        if any(var.lower() in status_text.lower() 
               for var in variations):
            return category
    
    # Check for stalled projects (no activity > 180 days)
    if (datetime.now() - last_activity_date).days > 180:
        return 'stalled'
    
    return 'unknown'  # For manual review
```

## 📊 Status Distribution

**Berkeley housing projects (n=84):**
- Completed: 45 (54%)
- Under Construction: 22 (26%)
- Permitted: 8 (10%)
- In Review: 6 (7%)
- Proposed: 3 (4%)

## 📊 Outputs

- `projects_classified.csv` - All projects with standard status
- Status distribution charts
- Projects flagged for manual review
- Status transition report

## 🔍 Quality Control

### Validation Checks
1. **No "Unknown" status** - All classified
2. **Logical progression** - States follow expected order
3. **Date consistency** - Status aligns with dates
4. **Manual review list** - Ambiguous cases flagged

## 🚀 Running This Notebook

**Locally:**
```bash
jupyter notebook workflows/B_timeline_tracking/B2_status_classification.ipynb
```

**Required Inputs:**
- Project data with status fields
- Last activity dates

## 📚 Related Notebooks

**Previous:** [B1: Lifecycle Tracking](B1-lifecycle.md)  
**Next:** [B3: Progress Indicators](B3-progress.md)  
**Uses in:** All analysis and reporting notebooks

## 💡 Data Science Lesson

**Status classification teaches:**
- Dealing with real-world messy data
- Creating robust mapping schemes
- Validating classifications
- Documenting edge cases

---

[← Back to Notebooks](Project-Tool-1%20-%20Net%20Present%20Value.md) | [View on GitHub](https://github.com/blockXblock/berkeley-housing-analysis/blob/main/workflows/B_timeline_tracking/B2_status_classification.ipynb)
