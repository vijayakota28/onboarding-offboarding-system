# HR Dashboard & Reports Specification

## 1. Dashboard: "Onboarding & Offboarding Overview"

**Audience:** HR leadership, department managers
**Refresh:** Real-time / near real-time (Performance Analytics scheduled data collection)

### Widgets

| Widget | Type | Description |
|---|---|---|
| Requests This Month | Single Score | Count of onboarding + offboarding requests submitted |
| Open Requests by Status | Pie Chart | New / In Progress / Some Complete / Complete |
| Average Time to Complete | Single Score / Trend | Avg. days from request creation to full completion, split by onboarding vs. offboarding |
| SLA Compliance Rate | Gauge | % of tasks completed within SLA over last 30/90 days |
| Breached Tasks | List | Live list of tasks currently in SLA breach, grouped by assignment group |
| Requests by Department | Bar Chart | Volume of onboarding/offboarding requests per department |
| Task Completion by Team | Stacked Bar | IT vs. Facilities vs. Security completion rates |

## 2. Reports

### 2.1 SLA Compliance Report
- **Purpose:** Track how often each team meets SLA commitments
- **Fields:** Task, Assignment Group, SLA Duration, Actual Duration, Breached (Y/N)
- **Schedule:** Weekly email to HR + department managers

### 2.2 Offboarding Compliance/Audit Report
- **Purpose:** Provide an auditable record that all access was revoked on time for compliance (e.g. SOX, ISO 27001)
- **Fields:** Employee, Termination Type, Last Working Day, Access Revocation Task Completion Timestamp, SLA Met (Y/N)
- **Schedule:** Monthly, retained for audit purposes

### 2.3 Onboarding Readiness Report
- **Purpose:** Confirm new hires have working accounts/equipment/access by their start date
- **Fields:** Employee, Start Date, IT Task Status, Facilities Task Status, Security Task Status, Overall Ready (Y/N)
- **Schedule:** Daily, sent to HR the week before each new hire's start date

## 3. Access & Visibility

- Dashboard visibility restricted to `hr_manager` and `admin` roles via Performance Analytics dashboard permissions
- Individual department leads may get a filtered view scoped to their own team's tasks only
