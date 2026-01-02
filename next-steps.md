---
title: 'Next Steps'
description: 'Roadmap for code improvements and technical enhancements'
---

# Next Steps

This document outlines the planned technical improvements and enhancements for the Healthcare Platform. These items represent opportunities to improve code quality, maintainability, and test coverage.

## Code Optimization

### Performance Improvements
- Implement lazy loading for feature modules to reduce initial bundle size
- Add OnPush change detection strategy to components where applicable
- Optimize RxJS subscriptions with proper operators (shareReplay, distinctUntilChanged)
- Implement virtual scrolling for large data lists (patients, alerts, messages)
- Add memoization for expensive computed values

### Bundle Optimization
- Analyze bundle size with webpack-bundle-analyzer
- Tree-shake unused dependencies
- Implement code splitting for route-based chunks
- Optimize image assets and implement lazy loading for images

## Remove Dummy Data

### Current Mock Data Locations
- `src/app/mock-data/` - Contains mock data files for development
- Inline mock data in component files
- Hardcoded values in services

### Migration Plan
1. Identify all mock data usage across the application
2. Create environment-specific data loading strategies
3. Implement feature flags to toggle between mock and real data
4. Remove mock data files once API integration is complete
5. Add data validation to ensure API responses match expected schemas

## Database Connection

### Backend Integration
- Implement proper API service layer with HttpClient
- Add request/response interceptors for authentication and error handling
- Create data models matching backend schemas
- Implement proper error handling and retry logic

### Data Layer Architecture
```typescript
// Example service structure
@Injectable({ providedIn: 'root' })
export class PatientService {
  private readonly apiUrl = environment.apiUrl;
  
  constructor(private http: HttpClient) {}
  
  getPatients(): Observable<Patient[]> {
    return this.http.get<Patient[]>(`${this.apiUrl}/patients`).pipe(
      catchError(this.handleError)
    );
  }
}
```

### State Management
- Implement centralized state management (NgRx or similar)
- Add caching layer for frequently accessed data
- Implement optimistic updates for better UX

## DRY Methods for Repetitive Logic

### Identified Patterns for Refactoring

#### Form Handling
- Create reusable form builder utilities
- Implement generic form validation helpers
- Extract common form field components

#### Data Transformation
- Create shared utility functions for date formatting
- Implement generic sorting and filtering utilities
- Extract common data mapping functions

#### API Calls
- Create generic CRUD service base class
- Implement shared error handling utilities
- Extract common HTTP interceptor logic

### Example Refactoring
```typescript
// Before: Repeated in multiple components
formatDate(date: Date): string {
  return date.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'short', 
    day: 'numeric' 
  });
}

// After: Shared utility
// src/app/shared/utils/date.utils.ts
export const formatDisplayDate = (date: Date): string => 
  date.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'short', 
    day: 'numeric' 
  });
```

### Shared Components to Extract
- Loading spinners and skeleton loaders
- Empty state displays
- Error message components
- Confirmation dialogs
- Pagination controls

## Unit Tests Addition

### Testing Strategy
- Achieve minimum 80% code coverage
- Focus on business logic and services first
- Test component interactions and state changes

### Priority Areas
1. **Services** - All data services and utilities
2. **Guards** - Authentication and authorization guards
3. **Pipes** - Custom transformation pipes
4. **Components** - Complex components with business logic

### Testing Tools
- Jasmine for test framework
- Karma for test runner (already configured)
- Angular Testing Library for component tests

### Example Test Structure
```typescript
describe('PatientService', () => {
  let service: PatientService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [PatientService]
    });
    service = TestBed.inject(PatientService);
    httpMock = TestBed.inject(HttpTestingController);
  });

  it('should fetch patients', () => {
    const mockPatients = [{ id: 1, name: 'John Doe' }];
    
    service.getPatients().subscribe(patients => {
      expect(patients).toEqual(mockPatients);
    });

    const req = httpMock.expectOne('/api/patients');
    req.flush(mockPatients);
  });
});
```

## Robot Framework E2E Tests

### Setup Requirements
- Install Robot Framework: `pip install robotframework`
- Install SeleniumLibrary: `pip install robotframework-seleniumlibrary`
- Install Browser drivers (ChromeDriver, GeckoDriver)

### Test Structure
```
e2e/
├── resources/
│   ├── common.robot
│   ├── pages/
│   │   ├── login.robot
│   │   ├── dashboard.robot
│   │   └── patients.robot
│   └── keywords/
│       └── custom_keywords.robot
├── tests/
│   ├── login.robot
│   ├── dashboard.robot
│   ├── patients.robot
│   └── carepaths.robot
└── results/
```

### Example Test Case
```robot
*** Settings ***
Library    SeleniumLibrary
Resource   ../resources/common.robot
Resource   ../resources/pages/login.robot

*** Test Cases ***
User Can Login Successfully
    [Documentation]    Verify user can login with valid credentials
    [Tags]    smoke    login
    Open Browser To Login Page
    Input Username    ${VALID_USER}
    Input Password    ${VALID_PASSWORD}
    Click Login Button
    Dashboard Should Be Visible
    [Teardown]    Close Browser

User Cannot Login With Invalid Credentials
    [Documentation]    Verify error message for invalid login
    [Tags]    login    negative
    Open Browser To Login Page
    Input Username    invalid@example.com
    Input Password    wrongpassword
    Click Login Button
    Error Message Should Be Visible
    [Teardown]    Close Browser
```

### Critical User Flows to Test
1. Authentication flow (login, logout, session management)
2. Patient management (create, view, edit, search)
3. Carepath workflows (create, assign, progress tracking)
4. Questionnaire completion
5. Alert management
6. Messaging functionality
7. Organization switching

## Logic Split from Templates

### Current Issues
- Business logic embedded in component templates
- Complex expressions in template bindings
- Inline styles mixed with component logic

### Separation Strategy

#### Move Logic to Component Class
```typescript
// Before: Logic in template
// <div *ngIf="patient.riskScore > 7 && patient.status === 'active'">

// After: Logic in component
get isHighRiskActivePatient(): boolean {
  return this.patient.riskScore > 7 && this.patient.status === 'active';
}
// Template: <div *ngIf="isHighRiskActivePatient">
```

#### Extract Complex Calculations to Services
```typescript
// Move from component to dedicated service
@Injectable({ providedIn: 'root' })
export class RiskCalculationService {
  calculateOverallRisk(patient: Patient): RiskLevel {
    // Complex calculation logic
  }
}
```

#### Separate Styles
- Move inline styles to component SCSS files
- Create shared style mixins for common patterns
- Use CSS custom properties for theming

### File Structure Best Practice
```
component/
├── component.component.ts      # Logic only
├── component.component.html    # Template only
├── component.component.scss    # Styles only
├── component.component.spec.ts # Tests
└── component.model.ts          # Interfaces/types
```

## Implementation Priority

| Priority | Task | Effort | Impact |
|----------|------|--------|--------|
| 1 | Remove dummy data & API integration | High | High |
| 2 | DRY refactoring | Medium | High |
| 3 | Unit tests | High | High |
| 4 | Logic separation | Medium | Medium |
| 5 | Code optimization | Medium | Medium |
| 6 | E2E tests | High | Medium |

## Timeline Recommendations

### Phase 1 (Weeks 1-2)
- Set up API integration infrastructure
- Begin removing mock data
- Start DRY refactoring of utilities

### Phase 2 (Weeks 3-4)
- Complete API integration
- Add unit tests for services
- Extract shared components

### Phase 3 (Weeks 5-6)
- Component unit tests
- Logic separation from templates
- Performance optimization

### Phase 4 (Weeks 7-8)
- Robot Framework E2E setup
- Critical path E2E tests
- Final optimization and cleanup
