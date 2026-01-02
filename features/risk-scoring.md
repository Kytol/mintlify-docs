---
title: Risk Scoring Dashboard
description: Monitor patient risk levels and predictive analytics
---

# Risk Scoring Dashboard

The Risk Scoring feature provides predictive analytics to identify patients at elevated risk, enabling proactive intervention before conditions worsen.

## Overview

The dashboard aggregates multiple health factors into a composite risk score for each patient, categorizing them by risk level and tracking trends over time.

<Info>
Risk scores are calculated using AI-powered algorithms that analyze patient data patterns and clinical indicators.
</Info>

## Risk Levels

<CardGroup cols={4}>
  <Card title="Low (0-25)" icon="shield-check">
    Stable, routine monitoring
  </Card>
  <Card title="Moderate (26-50)" icon="shield">
    Increased attention needed
  </Card>
  <Card title="High (51-75)" icon="shield-exclamation">
    Active intervention recommended
  </Card>
  <Card title="Critical (76-100)" icon="shield-xmark">
    Immediate action required
  </Card>
</CardGroup>

| Level | Score Range | Color | Response |
|-------|-------------|-------|----------|
| Low | 0-25 | Green | Routine monitoring |
| Moderate | 26-50 | Yellow | Increased attention |
| High | 51-75 | Orange | Active intervention |
| Critical | 76-100 | Red | Immediate action |

## Dashboard Components

### Statistics Cards

<CardGroup cols={4}>
  <Card title="Total Monitored" icon="users">
    All patients in risk monitoring
  </Card>
  <Card title="Improving" icon="arrow-trend-up">
    Patients with positive trends
  </Card>
  <Card title="Declining" icon="arrow-trend-down">
    Patients with negative trends
  </Card>
  <Card title="Critical" icon="circle-exclamation">
    Patients requiring immediate attention
  </Card>
</CardGroup>

### Risk Distribution Chart

Visual bar chart showing patient distribution:
- Clickable bars to filter by level
- Percentage tooltips on hover
- Color-coded by severity

### Risk Overview Gauge

Circular progress indicator showing:
- Average risk score across all patients
- Active alert count
- Alerts triggered today

## Patient Risk Table

Sortable table displaying:

| Column | Description |
|--------|-------------|
| Patient | Name with avatar |
| Risk Score | Score with progress bar |
| Risk Level | Color-coded badge |
| Trend | Direction with percentage change |
| Actions | View, details, configure |

## Predictive Alerts Panel

<Warning>
Predictive alerts use AI to forecast potential issues. Always verify with clinical judgment.
</Warning>

Real-time alerts predicting potential issues:

<Tabs>
  <Tab title="Deterioration">
    Patient condition may worsen based on trend analysis.
  </Tab>
  <Tab title="Missed Medication">
    Predicted medication non-compliance.
  </Tab>
  <Tab title="Vital Signs">
    Abnormal vital sign patterns detected.
  </Tab>
</Tabs>

### Alert Information

| Field | Description |
|-------|-------------|
| Severity | Info, Warning, Urgent |
| Confidence | Algorithm certainty (%) |
| Time to Threshold | Estimated time until critical |

### Alert Actions

<Steps>
  <Step title="View Patient">
    Navigate to patient profile for full context
  </Step>
  <Step title="Acknowledge">
    Mark alert as seen by care team
  </Step>
  <Step title="Dismiss">
    Remove alert if not applicable
  </Step>
</Steps>

## Risk Factors

Each patient's score is calculated from multiple factors:

<AccordionGroup>
  <Accordion title="Vital Signs" icon="heart-pulse">
    Blood pressure, heart rate, temperature, respiratory rate, oxygen saturation.
  </Accordion>
  <Accordion title="Lab Results" icon="flask">
    Blood work, diagnostic tests, imaging results.
  </Accordion>
  <Accordion title="Compliance" icon="clipboard-check">
    Medication adherence, appointment attendance, questionnaire completion.
  </Accordion>
  <Accordion title="Symptoms" icon="stethoscope">
    Reported symptoms, pain levels, functional status.
  </Accordion>
  <Accordion title="History" icon="clock-rotate-left">
    Previous conditions, hospitalizations, family history.
  </Accordion>
</AccordionGroup>

### Factor Details View

Click the chart icon on any patient to view:
- Individual factor scores
- Current vs. normal range values
- Factor weights in overall score
- Trend direction per factor

## Filtering & Sorting

### Search
Find patients by name using the search bar.

### Risk Level Filter

| Filter | Description |
|--------|-------------|
| All Levels | Show all patients |
| Critical | Only critical risk |
| High | Only high risk |
| Moderate | Only moderate risk |
| Low | Only low risk |

### Sort Options
- Score (descending/ascending)
- Name (A-Z)
- Declining patients first

## Quick Actions

<CardGroup cols={2}>
  <Card title="Review Critical" icon="circle-exclamation">
    One-click filter to critical patients
  </Card>
  <Card title="Configure Thresholds" icon="sliders">
    Access risk scoring settings
  </Card>
</CardGroup>

## Configuration

Access settings to customize:

| Setting | Description |
|---------|-------------|
| Risk Thresholds | Score ranges for each level |
| Factor Weights | Importance of each factor |
| Alert Triggers | When to generate alerts |
| Notifications | Who receives alerts |

## Integration Points

<AccordionGroup>
  <Accordion title="Alerts" icon="bell">
    High-risk patients automatically generate priority alerts in the Alerts dashboard.
  </Accordion>
  <Accordion title="Patient Dashboard" icon="user">
    Risk score displayed prominently on patient profile.
  </Accordion>
  <Accordion title="Care Team" icon="users">
    Risk levels inform care prioritization and resource allocation.
  </Accordion>
  <Accordion title="Analytics" icon="chart-line">
    Risk trends included in analytics reporting.
  </Accordion>
</AccordionGroup>

## Best Practices

<Tip>
**Monitor Critical Daily** - Review critical patients at least once per day
</Tip>

<Tip>
**Investigate Declining** - Patients with declining trends need attention
</Tip>

<Tip>
**Verify Predictions** - Use clinical judgment alongside AI predictions
</Tip>

<Tip>
**Adjust Thresholds** - Tune thresholds based on your patient population
</Tip>

<Tip>
**Document Actions** - Record interventions for declining patients
</Tip>
