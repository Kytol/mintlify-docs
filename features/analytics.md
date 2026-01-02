---
title: Analytics Dashboard
description: Comprehensive insights and performance metrics
---

# Analytics Dashboard

The Analytics Dashboard provides data-driven insights into platform usage, patient outcomes, and operational metrics through interactive visualizations.

## Overview

Analytics aggregates data across patients, carepaths, alerts, and activities to help care teams understand trends and optimize workflows.

<Info>
All metrics update in real-time and can be filtered by time period for trend analysis.
</Info>

## Time Period Selection

<Tabs>
  <Tab title="Last 7 Days">
    Short-term view for immediate trends and daily operations.
  </Tab>
  <Tab title="Last 30 Days">
    Monthly view for operational planning and review.
  </Tab>
  <Tab title="Last 90 Days">
    Quarterly view for strategic analysis.
  </Tab>
  <Tab title="This Year">
    Annual view for year-over-year comparisons.
  </Tab>
</Tabs>

## KPI Cards

<CardGroup cols={4}>
  <Card title="Total Patients" icon="users">
    All patients in the system
  </Card>
  <Card title="Active Carepaths" icon="route">
    Patients on care journeys
  </Card>
  <Card title="Completion Rate" icon="chart-pie">
    Carepath completion percentage
  </Card>
  <Card title="Response Time" icon="clock">
    Average response metrics
  </Card>
</CardGroup>

### Card Features
- Large value display
- Trend arrow (up/down/stable)
- Percentage change vs. previous period
- Clickable for drill-down details

## Activity Trends Chart

Bar chart showing patient interactions over time:

| Element | Description |
|---------|-------------|
| Current Period | Cyan bars showing current data |
| Previous Period | Gray bars for comparison |
| Tooltips | Hover for exact values |
| Summary | Total, average, peak, and trend |

## Patient Status Distribution

Horizontal bar chart showing patients by status:

| Status | Description |
|--------|-------------|
| In Progress | Active care pathway |
| Awaiting Approval | Pending review |
| Completed | Finished care journey |
| On Hold | Temporarily paused |

Each bar shows count, percentage, and is clickable to filter.

## Alert Severity Breakdown

Donut chart displaying alerts by severity:

<CardGroup cols={4}>
  <Card title="Critical" icon="circle-exclamation">
    Immediate attention (Red)
  </Card>
  <Card title="High" icon="triangle-exclamation">
    Urgent review (Orange)
  </Card>
  <Card title="Medium" icon="circle-info">
    Monitor closely (Yellow)
  </Card>
  <Card title="Low" icon="circle">
    Informational (Blue)
  </Card>
</CardGroup>

## Top Carepaths

Ranked list of most-used carepaths:

| Rank | Display |
|------|---------|
| 1st | Gold badge |
| 2nd | Silver badge |
| 3rd | Bronze badge |
| 4th+ | Numeric badge |

Each entry shows:
- Carepath name
- Patient count
- Completion rate with progress bar

## Response Time Metrics

Track care team responsiveness:

| Metric | Description |
|--------|-------------|
| Current Value | Actual response time |
| Target | Expected response time |
| Progress Bar | Visual comparison |
| Status | Good/Warning/Critical indicator |

## Recent Activity Feed

Chronological list of platform events:
- Activity icon and type
- Description message
- Timestamp (relative)

## Data Management

<Steps>
  <Step title="Refresh Data">
    Click refresh button for latest data
  </Step>
  <Step title="Change Period">
    Select time period to update all charts
  </Step>
  <Step title="Export Report">
    Download analytics summary as PDF/CSV
  </Step>
</Steps>

## Best Practices

<Check>
**Weekly Review**: Check analytics weekly for trends
</Check>

<Check>
**Compare Periods**: Identify changes over time
</Check>

<Check>
**Monitor Completion**: Track carepath completion rates
</Check>

<Check>
**Track Response Times**: Ensure SLA compliance
</Check>

<Check>
**Use Filters**: Focus on specific timeframes for analysis
</Check>
