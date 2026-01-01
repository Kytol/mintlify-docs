---
title: Questionnaires
description: Create and manage patient data collection forms
---

# Questionnaires

Questionnaires are structured forms used to collect patient data at various points in their care journey. They can be embedded in carepath steps or used independently.

## Creating a Questionnaire

### Basic Information
1. Enter a descriptive title (required)
2. Add an optional description explaining the questionnaire's purpose
3. Configure recurrence settings if needed
4. Add an optional infographic image
5. Add questions using the question builder

### Using Templates
The platform includes ready-made templates for common use cases:
- Laser Eye Surgery - Pre-Operative Assessment
- Laser Eye Surgery - Post-Operative Care
- Prenatal Care - Initial Assessment
- Orthopedic Surgery - Recovery Assessment

Click "or use a template" to browse and select a template as your starting point.

## Question Types

The platform supports 9 question types, each designed for specific data collection needs:

### Text (String)
Free-form text input for descriptive responses.

**Use cases:**
- Describe current health concerns
- List allergies or medications
- Document symptoms or observations

**Example:** "Describe your current health concerns"

### Number
Numeric input for quantitative data.

**Use cases:**
- Hours of sleep per night
- Glasses of water daily
- Weeks pregnant

**Example:** "How many hours of sleep do you get per night?"

### Date
Date picker for selecting a specific date.

**Use cases:**
- Last doctor visit
- Symptom onset date
- Estimated due date

**Example:** "When was your last doctor visit?"

### Date & Time
Combined date and time picker.

**Use cases:**
- Last medication taken
- Next scheduled appointment
- Symptom occurrence time

**Example:** "When did you take your last medication?"

### Weight
Weight input with unit selection (kg or lbs).

**Response format:**
```json
{
  "value": 75.5,
  "unit": "kg"
}
```

**Use cases:**
- Current weight tracking
- Weight change monitoring
- Pre/post procedure weight

**Example:** "What is your current weight?"

### Pain Scale
Visual 0-10 pain scale selector.

**Scale interpretation:**
- 0: No pain
- 1-3: Mild pain
- 4-6: Moderate pain
- 7-9: Severe pain
- 10: Worst possible pain

**Use cases:**
- Current pain level
- Pain after medication
- Pain at specific body location

**Example:** "Rate your current pain level (0-10)"

### Blood Pressure
Dual input for systolic and diastolic readings.

**Response format:**
```json
{
  "systolic": 120,
  "diastolic": 80
}
```

**Use cases:**
- Daily BP monitoring
- Pre/post medication BP
- Vital signs tracking

**Example:** "What is your current blood pressure?"

### Image
Photo upload for visual documentation.

**Supported formats:** PNG, JPG, GIF (up to 5MB)

**Use cases:**
- Wound photos for healing progress
- Skin condition documentation
- Post-surgery site images

**Example:** "Upload a photo of the wound"

### Threshold
Numeric input with automatic alert triggering when values exceed configured limits.

**Configuration options:**
- Threshold value (numeric)
- Comparison operator
- Alert message for care team

**Example:** "Enter your blood glucose level" (alert if greater than 180)

## Threshold Configuration

Threshold questions are powerful tools for proactive patient monitoring.

### Comparison Operators

| Operator | Symbol | Description |
|----------|--------|-------------|
| Greater than | `>` | Alert when value exceeds threshold |
| Less than | `<` | Alert when value below threshold |
| Equal to | `=` | Alert when value matches exactly |
| Greater or equal | `>=` | Alert when value at or above threshold |
| Less or equal | `<=` | Alert when value at or below threshold |

### Setting Up a Threshold Question

1. Select "Threshold" as question type
2. Enter the question text
3. Choose the comparison operator
4. Set the threshold value
5. Write a clear alert message for the care team

### Alert Message Best Practices
- Be specific about what triggered the alert
- Include recommended actions
- Reference normal ranges when helpful

**Example alert message:** "Blood glucose level exceeds 180 mg/dL. Patient may need insulin adjustment. Contact physician if reading persists."

## Recurrence Settings

Configure questionnaires to repeat automatically for ongoing monitoring.

### Frequency Options
- **Daily**: Every day
- **Weekly**: Once per week
- **Biweekly**: Every two weeks
- **Monthly**: Once per month

### Configuration
- **Start Date**: When recurrence begins
- **End Date**: Optional end date for recurrence
- **Occurrences**: Specific number of times (leave empty for indefinite)

### Recurrence Summary
The form displays a human-readable summary:
> "Repeats weekly starting Jan 15, 2025 for 12 occurrences"

## Infographics

Add visual instructions to help patients understand the questionnaire.

### Adding an Infographic
1. Click the upload area or drag and drop an image
2. Or paste an image URL and click "Add"
3. Add a caption describing the image
4. Add alt text for accessibility

### Infographic Best Practices
- Use clear, simple visuals
- Include step-by-step instructions when applicable
- Ensure text in images is readable
- Keep file sizes reasonable (under 5MB)

## Question Management

### Adding Questions
1. Click "Add Question" button
2. Select question type from dropdown
3. Enter question text
4. Toggle "Required" if mandatory
5. Configure threshold settings (if applicable)
6. Click "Add Question"

### Editing Questions
1. Click the edit icon on any question
2. Modify question properties
3. Click "Save Changes"

### Reordering Questions
Drag and drop questions to change their order. Order numbers update automatically.

### Deleting Questions
Click the delete icon and confirm removal.

## Version History

Every change to a questionnaire is tracked:

### Change Types
- **created**: Initial questionnaire creation
- **updated**: General updates
- **question_added**: New question added
- **question_removed**: Question deleted
- **question_modified**: Question settings changed
- **reordered**: Question order changed

### Version Information
- Version number (auto-incremented)
- Change description
- User who made the change
- Timestamp
- Previous/new values (for rollback)

## Sample Questionnaires

### General Health Assessment
Basic intake questionnaire with:
- Health concerns (string)
- Allergies (string)
- Sleep hours (number)
- Water intake (number)

### Vital Signs Monitoring
Daily monitoring with:
- Current weight (weight)
- Pain level (pain)
- Blood pressure (bloodpressure)
- Pain after medication (pain)

### Wound Assessment
Visual documentation with:
- Wound location (string)
- Wound photo (image)
- Pain at site (pain)
- Infection concerns (string)

### Pre-Surgery Instructions
Checklist with infographic:
- Fasting confirmation (string)
- Medications taken (string)
- Questions/concerns (string)
- Last food/drink time (date)
- Preparation checklist (string)

## Integration Points

### Carepaths
Questionnaires are embedded as steps in carepath templates. Patients complete them as they progress through their care journey.

### Alerts
Threshold questions automatically generate alerts when triggered, appearing in the Alerts dashboard for care team review.

### Pending Approvals
Submitted questionnaire responses enter the approval queue for clinical review before processing.

### Patient Dashboard
View a patient's complete questionnaire history, responses, and any associated comments.

## Best Practices

1. **Choose appropriate types**: Match question types to the data you need
2. **Set thresholds wisely**: Configure alerts for clinically significant values
3. **Write clear questions**: Use simple, unambiguous language
4. **Mark required fields**: Only require truly essential questions
5. **Use recurrence**: Set up recurring questionnaires for ongoing monitoring
6. **Add infographics**: Visual aids improve patient compliance
7. **Version control**: Document significant changes for audit trails
