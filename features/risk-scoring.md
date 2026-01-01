---
title: Risk Scoring Dashboard
description: Monitor patient risk levels and predictive analytics
---

# Risk Scoring Dashboard

The Risk Scoring feature provides predictive analytics to identify patients at elevated risk, enabling proactive intervention before conditions worsen.

## Overview

The dashboard aggregates multiple health factors into a composite risk score for each patient, categorizing them by risk level and tracking trends over time.

## Risk Levels

| Level | Score Range | Color | Description |
|-------|-------------|-------|-------------|
| Low | 0-25 | Green | Stable, routine monitoring |
| Moderate | 26-50 | Yellow | Increased attention needed |
| High | 51-75 | Orange | Active intervention recommended |
| Critical | 76-100 | Red | Immediate action required |

## Dashboard Components

### Statistics Cards
Seven key metrics displayed:
- Total patients monitored
- Count by risk level (Low, Moderate, High, Critical)
- Patients improving (positive trend)
- Patients declining (negative trend)

### Risk Distribution Chart
Visual bar chart showing patient distribution across risk levels with:
- Clickable bars to filter by level
- Percentage tooltips on hover
- Color-coded by severity

### Risk Overview Gauge
Circular progress indicator showing:
- Average risk score across all patients
- Active alert count
- Alerts triggered today

### Patient Risk Table
Sortable table displaying:
- Patient name with avatar
- Risk score with progress bar
- Risk level badge
- Trend indicator with percentage change
- Action buttons

## Predictive Alerts Panel

Real-time alerts predicting potential issues:
- **Alert Types**: Deterioration, missed medication, vital signs
- **Severity**: Info, Warning, Urgent
- **Confidence Score**: Algorithm certainty percentage
- **Time to Threshold**: Estimated time until critical

### Alert Actions
- View patient profile
- Acknowledge alert
- Dismiss alert

## Risk Factors

Each patient's score is calculated from multiple factors:

### Factor Categories
- **Vital Signs**: Blood pressure, heart rate, temperature
- **Lab Results**: Blood work, diagnostic tests
- **Compliance**: Medication adherence, appointment attendance
- **Symptoms**: Reported symptoms, pain levels
- **History**: Previous conditions, hospitalizations

### Factor Details
Click the chart icon on any patient to view:
- Individual factor scores
- Current vs. normal range values
- Factor weights in overall score
- Trend direction per factor

## Filtering & Sorting

### Search
Find patients by name.

### Risk Level Filter
- All Levels
- Critical only
- High only
- Moderate only
- Low only

### Sort Options
- Score (descending/ascending)
- Name (A-Z)
- Declining patients first

## Quick Actions

- **Review Critical Patients**: One-click filter to critical level
- **Configure Thresholds**: Access risk scoring settings

## Configuration

Access settings to customize:
- Risk level thresholds
- Factor weights
- Alert triggers
- Notification preferences

## Integration

- **Alerts**: High-risk patients generate priority alerts
- **Patient Dashboard**: Risk score displayed on patient profile
- **Care Team**: Risk levels inform care prioritization
