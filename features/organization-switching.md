# Organization Switching Feature

## Overview
Added the ability to switch between different care units, hospitals, and departments in the settings, with the selected organization name displayed in the sidebar.

## Implementation Details

### Key Features
1. **Organization Management**: Users can select from predefined organizations (hospitals, departments, care units)
2. **Settings Integration**: New organization section in settings with dropdown selector
3. **Sidebar Display**: Selected organization name and type shown in sidebar header
4. **Real-time Updates**: Changes reflect immediately in the sidebar when saved
5. **Persistent Storage**: Organization selection is saved to localStorage

### Technical Implementation

#### New Models (`settings.model.ts`)
- `Organization`: Represents a healthcare organization with id, name, type, address, phone
- `OrganizationSettings`: Manages selected organization and available options
- Default organizations include hospitals, departments, and care units

#### Enhanced Settings Service (`settings.service.ts`)
- `getOrganizationSettings()`: Retrieves current organization settings
- `saveOrganizationSettings()`: Saves organization preferences
- `getSelectedOrganization()`: Gets currently selected organization
- `setSelectedOrganization()`: Updates selected organization
- Observable `selectedOrganization$` for real-time updates

#### Updated Sidebar (`sidebar.component.ts`)
- Displays selected organization name and type below "Carepath Manager"
- Subscribes to organization changes for real-time updates
- Shows organization type label (Hospital/Department/Care Unit)

#### Enhanced Settings Component (`settings.component.ts`)
- New "Organization" section with dropdown selector
- Organization details display (type, address, phone)
- Save functionality with success/error notifications

### Available Organizations
1. **St. Mary's Hospital** (Hospital)
2. **Cardiology Department** (Department)  
3. **ICU Care Unit** (Care Unit)
4. **Emergency Department** (Department)
5. **Pediatric Care Unit** (Care Unit)

### Usage
1. Navigate to Settings page
2. Find the "Organization" section (third column)
3. Select desired organization from dropdown
4. View organization details below selector
5. Click "Save Organization" to apply changes
6. See updated organization name in sidebar immediately

### Benefits
- **Multi-facility Support**: Supports healthcare systems with multiple locations
- **Role-based Context**: Users can switch between different work contexts
- **Clear Identification**: Always shows current organizational context
- **Easy Switching**: Simple dropdown interface for quick changes
- **Data Persistence**: Remembers selection across sessions

## Files Modified
- `src/app/models/settings.model.ts` - Added organization models and defaults
- `src/app/services/settings.service.ts` - Added organization management methods
- `src/app/layout/sidebar/sidebar.component.ts` - Added organization display
- `src/app/pages/settings/settings.component.ts` - Added organization settings UI

## Testing
The feature can be tested by:
1. Opening the Settings page
2. Changing the organization selection
3. Saving the settings
4. Verifying the sidebar updates with the new organization name
5. Refreshing the page to confirm persistence
