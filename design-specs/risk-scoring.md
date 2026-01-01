---
title: Risk Scoring Dashboard
description: 'Predictive analytics for patient risk monitoring and alerts'
icon: 'chart-line'
---

# Risk Scoring Dashboard

Predictive analytics dashboard for monitoring patient risk levels, identifying at-risk patients, and managing predictive alerts.

## Overview

The Risk Scoring Dashboard provides healthcare providers with AI-powered risk assessment tools. It displays patient risk scores, trends, and predictive alerts to help identify patients who may need intervention. The system uses multiple risk factors to calculate overall risk scores and predict potential health events.

## Features

### Statistics Overview
Seven key metrics displayed as interactive cards:
- **Total Patients**: Overall patient count
- **Low Risk**: Patients with low risk scores (green)
- **Moderate Risk**: Patients with moderate risk (yellow)
- **High Risk**: Patients with high risk (orange)
- **Critical Risk**: Patients requiring immediate attention (red)
- **Improving**: Patients with improving trends
- **Declining**: Patients with worsening trends

### Risk Distribution Chart
- Bar chart showing patient distribution by risk level
- Percentage breakdown
- Interactive filtering by clicking bars
- Visual comparison of risk categories

### Risk Overview Gauge
- Circular gauge showing average risk score
- Color-coded based on overall population health
- Active alerts count
- Today's alerts count

### Patient Risk Table
- Sortable patient list with risk scores
- Visual risk score bars
- Risk level badges
- Trend indicators (improving/declining)
- Search and filter capabilities
- Quick actions (View, Details)

### Predictive Alerts Panel
- Real-time predictive alerts
- Severity indicators (Info, Warning, Urgent)
- Time to threshold predictions
- Confidence scores
- Acknowledge/Dismiss actions
- Patient navigation links

### Quick Actions
- Review Critical Patients shortcut
- Configure Thresholds link
- Refresh data button
- Settings navigation

### Patient Details Modal
- Risk factors breakdown
- Individual factor scores
- Factor trends
- Current vs. normal values
- Factor weights

## Use Cases

### UC-RS-001: Review High-Risk Patients
**Actor**: Healthcare Provider  
**Description**: Provider reviews patients with elevated risk scores.

**Flow**:
1. Provider navigates to Risk Scoring Dashboard
2. Views statistics cards for risk distribution
3. Clicks "Critical" or "High" filter
4. Reviews filtered patient list
5. Clicks on patient for details
6. Reviews risk factors breakdown
7. Takes appropriate action

### UC-RS-002: Respond to Predictive Alert
**Actor**: Healthcare Provider  
**Description**: Provider responds to a predictive alert about patient deterioration.

**Flow**:
1. Provider sees urgent alert in panel
2. Reviews alert details and confidence
3. Clicks "View Patient"
4. Reviews patient's full profile
5. Takes clinical action
6. Returns to acknowledge alert
7. Alert status updates

### UC-RS-003: Monitor Risk Trends
**Actor**: Healthcare Provider  
**Description**: Provider monitors population risk trends over time.

**Flow**:
1. Provider views risk distribution chart
2. Notes changes in distribution
3. Identifies increasing high-risk count
4. Drills down to specific patients
5. Investigates common factors
6. Adjusts care protocols

### UC-RS-004: Configure Risk Thresholds
**Actor**: Healthcare Administrator  
**Description**: Administrator adjusts risk scoring thresholds.

**Flow**:
1. Administrator clicks "Configure"
2. Navigates to Risk Settings
3. Adjusts threshold values
4. Modifies factor weights
5. Saves configuration
6. Risk scores recalculate

## User Stories

### US-RS-001
**As a** healthcare provider  
**I want to** see patient risk scores at a glance  
**So that** I can prioritize high-risk patients

**Acceptance Criteria**:
- [ ] Risk scores are prominently displayed
- [ ] Color coding indicates severity
- [ ] Sorting by risk score is available
- [ ] Critical patients are highlighted

### US-RS-002
**As a** healthcare provider  
**I want to** receive predictive alerts  
**So that** I can intervene before patient deterioration

**Acceptance Criteria**:
- [ ] Alerts show predicted events
- [ ] Confidence scores are displayed
- [ ] Time to threshold is shown
- [ ] Alerts can be acknowledged

### US-RS-003
**As a** healthcare provider  
**I want to** see risk factor breakdown  
**So that** I can understand what's driving risk

**Acceptance Criteria**:
- [ ] Individual factors are listed
- [ ] Factor scores are shown
- [ ] Factor trends are indicated
- [ ] Normal ranges are displayed

### US-RS-004
**As a** healthcare provider  
**I want to** filter patients by risk level  
**So that** I can focus on specific populations

**Acceptance Criteria**:
- [ ] Filter by risk level available
- [ ] Multiple levels can be selected
- [ ] Search by patient name works
- [ ] Sort options are available

### US-RS-005
**As a** healthcare administrator  
**I want to** configure risk thresholds  
**So that** I can customize for our population

**Acceptance Criteria**:
- [ ] Threshold values are editable
- [ ] Factor weights can be adjusted
- [ ] Changes apply to calculations
- [ ] Audit trail is maintained

## Component Dependencies

```
RiskDashboardComponent
├── RiskStatsCardsComponent
├── RiskDistributionChartComponent
├── RiskOverviewGaugeComponent
├── PatientRiskTableComponent
│   └── RiskBadgeComponent
├── PredictiveAlertsPanel
└── RiskConfigModalComponent
```

## Data Flow

```
┌─────────────────┐     ┌──────────────────┐
│RiskScoringService│───▶│                  │
└─────────────────┘     │                  │
         │              │  RiskDashboard   │
         │              │   Component      │
         ▼              │                  │
┌─────────────────┐     │                  │
│  PatientService │────▶│                  │
└─────────────────┘     └────────┬─────────┘
                                 │
                        ┌────────┴────────┐
                        │                 │
                        ▼                 ▼
                 ┌──────────┐      ┌──────────┐
                 │RiskTable │      │AlertPanel│
                 └──────────┘      └──────────┘
```

## Risk Scoring Model

### Risk Levels
| Level | Score Range | Color | Action Required |
|-------|-------------|-------|-----------------|
| Low | 0-25 | Green | Routine monitoring |
| Moderate | 26-50 | Yellow | Enhanced monitoring |
| High | 51-75 | Orange | Active intervention |
| Critical | 76-100 | Red | Immediate attention |

### Risk Factors
- Clinical indicators (vitals, labs)
- Medication adherence
- Appointment compliance
- Social determinants
- Historical patterns

## Technical Notes

- Risk scores calculated by ML model
- Scores refresh on configurable interval
- Predictive alerts use time-series analysis
- Factor weights are organization-configurable
- Historical risk data retained for trending
- Real-time updates via WebSocket
