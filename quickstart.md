---
title: Quick Start
description: 'Get up and running with the Healthcare Platform in minutes'
---

## Prerequisites

Before you begin, ensure you have the following installed:

<CardGroup cols={2}>
  <Card title="Node.js" icon="node-js">
    Version 18.x or higher
  </Card>
  <Card title="npm" icon="npm">
    Version 9.x or higher
  </Card>
</CardGroup>

<Info>
You can verify your installations by running `node --version` and `npm --version` in your terminal.
</Info>

## Installation

<Steps>
  <Step title="Clone the Repository">
    ```bash
    git clone https://github.com/example/healthcare-platform.git
    cd healthcare-platform
    ```
  </Step>
  <Step title="Install Dependencies">
    ```bash
    npm install
    ```
  </Step>
  <Step title="Configure Environment">
    Create a `.env` file in the root directory:
    ```bash
    cp .env.example .env
    ```
    
    Update the environment variables:
    ```env
    API_URL=http://localhost:3000
    AUTH_DOMAIN=your-auth-domain
    AUTH_CLIENT_ID=your-client-id
    ```
  </Step>
  <Step title="Start Development Server">
    ```bash
    npm start
    ```
    
    The application will be available at `http://localhost:4200`
  </Step>
</Steps>

<Check>
**Success!** You should now see the login page at http://localhost:4200
</Check>

## Project Structure

```
healthcare-platform/
├── src/
│   ├── app/
│   │   ├── components/     # Shared UI components
│   │   ├── pages/          # Page components
│   │   ├── services/       # Angular services
│   │   ├── models/         # TypeScript interfaces
│   │   └── pipes/          # Custom pipes
│   ├── assets/             # Static assets
│   └── environments/       # Environment configs
├── docs/                   # Documentation
└── package.json
```

## Key Concepts

### Pages vs Components

<Tabs>
  <Tab title="Pages">
    Pages are routable components that represent full views in the application:
    
    | Page | Description |
    |------|-------------|
    | `DashboardComponent` | Main landing page |
    | `PatientsListComponent` | Patient directory |
    | `PatientDetailComponent` | Individual patient view |
    | `MessagesComponent` | Messaging interface |
    
    Pages are located in `src/app/pages/`
  </Tab>
  <Tab title="Components">
    Components are reusable UI elements used across pages:
    
    | Component | Description |
    |-----------|-------------|
    | `RiskBadgeComponent` | Risk level indicator |
    | `FilterBarComponent` | Search and filter controls |
    | `ChatThreadComponent` | Message thread display |
    | `ToastComponent` | Notification display |
    
    Components are located in `src/app/components/`
  </Tab>
</Tabs>

### Services

Services manage application state and API communication:

```typescript
// Example: PatientService
@Injectable({ providedIn: 'root' })
export class PatientService {
  private patients$ = new BehaviorSubject<Patient[]>([]);
  
  getPatients(): Observable<Patient[]> {
    return this.patients$.asObservable();
  }
  
  getPatientById(id: string): Patient | undefined {
    return this.patients$.value.find(p => p.id === id);
  }
}
```

### Routing

The application uses Angular Router with the following main routes:

| Route | Component | Description |
|-------|-----------|-------------|
| `/dashboard` | DashboardComponent | Main dashboard |
| `/patients` | PatientsListComponent | Patient list |
| `/patients/:id` | PatientDetailComponent | Patient detail |
| `/messages` | MessagesComponent | Messaging |
| `/alerts` | AlertsComponent | Alert management |
| `/risk-scoring` | RiskDashboardComponent | Risk analytics |
| `/care-team` | CareTeamDashboardComponent | Team collaboration |
| `/settings` | SettingsComponent | Organization settings |

## First Steps

<CardGroup cols={2}>
  <Card
    title="Explore the Dashboard"
    icon="gauge"
    href="/features/dashboard"
  >
    Start with the main dashboard to understand the application layout
  </Card>
  <Card
    title="View Patient Management"
    icon="users"
    href="/design-specs/patients-list"
  >
    Learn how patient data is organized and displayed
  </Card>
  <Card
    title="Understand Risk Scoring"
    icon="chart-line"
    href="/features/risk-scoring"
  >
    Explore the predictive analytics features
  </Card>
  <Card
    title="Review Components"
    icon="puzzle-piece"
    href="/design-specs/components"
  >
    Browse the shared component library
  </Card>
</CardGroup>

## Development Commands

```bash
# Start development server
npm start

# Run tests
npm test

# Build for production
npm run build

# Lint code
npm run lint

# Format code
npm run format
```

## Common Tasks

<AccordionGroup>
  <Accordion title="Adding a New Page" icon="file-plus">
    1. Create component in `src/app/pages/`
    2. Add route in `app.routes.ts`
    3. Add navigation link in sidebar
  </Accordion>
  <Accordion title="Creating a Service" icon="gear">
    1. Generate with `ng generate service services/my-service`
    2. Add to providers if not using `providedIn: 'root'`
    3. Inject in components as needed
  </Accordion>
  <Accordion title="Adding a Component" icon="puzzle-piece">
    1. Create in `src/app/components/`
    2. Export from component module
    3. Import in consuming components
  </Accordion>
  <Accordion title="Styling with Tailwind" icon="paintbrush">
    1. Use Tailwind utility classes directly
    2. Custom styles in `styles.scss`
    3. Theme colors defined in `tailwind.config.js`
  </Accordion>
</AccordionGroup>

## Troubleshooting

<Warning>
If you encounter issues, try these common solutions first.
</Warning>

| Issue | Solution |
|-------|----------|
| Port 4200 in use | Use `npm start -- --port 4201` |
| Dependencies fail | Delete `node_modules` and run `npm install` |
| Build errors | Check TypeScript version compatibility |
| Styles not loading | Verify Tailwind config and imports |

## Next Steps

<Check>
**Congratulations!** You've set up the Healthcare Platform locally.
</Check>

Continue exploring:

1. Review the [Features](/features/index) for detailed feature documentation
2. Check the [API Reference](/api/API_INTEGRATION_GUIDE) for backend integration
3. Understand the [Architecture](/architecture/BACKEND_ARCHITECTURE) for system design
4. Browse [Design Specifications](/design-specs) for UI/UX details
