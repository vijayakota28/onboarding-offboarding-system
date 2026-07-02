# Automated Employee Onboarding & Offboarding System

> A ServiceNow-based solution that replaces manual HR/IT onboarding and offboarding workflows with catalog-driven requests, automated task orchestration, and SLA monitoring.

[![ServiceNow](https://img.shields.io/badge/Platform-ServiceNow-62D84E)](#)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)](#)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## Demo & Links

- **Live Demo:** _Add your demo link here (e.g. ServiceNow PDI instance URL or video walkthrough)_
- **GitHub Repository:** _Add your GitHub repo link here_
- **Video Walkthrough:** _Optional — add a Loom/YouTube link here_

## Overview

Employee onboarding and offboarding traditionally involve manual coordination across HR, IT, Facilities, and Security — often through emails and spreadsheets. This leads to delays, missed steps, and compliance risks.

This project automates the entire lifecycle in **ServiceNow** by:

- Replacing manual requests with a **Service Catalog** item for onboarding/offboarding
- Automatically generating and assigning **tasks** to IT, Facilities, and Security teams
- Enforcing **SLAs** to ensure timely completion at every stage
- Giving HR **real-time dashboards and reports** for visibility, efficiency, and compliance

## Problem Statement

| Manual Process | Pain Point |
|---|---|
| Email/spreadsheet-based requests | No single source of truth, easy to lose track |
| Manual task handoff between teams | Delays, unclear ownership |
| No SLA enforcement | Late account provisioning, badge issuance, etc. |
| No reporting | HR has no visibility into process health or bottlenecks |

## Solution Summary

A single **Service Catalog Request** ("New Hire Onboarding" / "Employee Offboarding") triggers a **Flow Designer** flow that:

1. Creates a parent Request/RITM record
2. Auto-generates child tasks for IT, Facilities, and Security based on employee role/department
3. Assigns tasks using **Access Controls (ACLs)** and assignment rules
4. Attaches **SLA definitions** to each task to track and escalate overdue work
5. Updates a live **HR Dashboard** with request status, SLA breaches, and completion metrics

See [`ARCHITECTURE.md`](ARCHITECTURE.md) for the full technical design and [`WORKFLOWS.md`](WORKFLOWS.md) for detailed onboarding/offboarding process flows.

## Key Features

- 🗂️ **Service Catalog** items for onboarding and offboarding requests
- 🔄 **Flow Designer** orchestration — no manual task creation
- 👥 Automatic task routing to **IT / Facilities / Security**
- ⏱️ **SLA definitions** with escalation and breach notifications
- 🔐 Role-based **Access Controls (ACLs)** for sensitive tasks (e.g. access revocation)
- 📊 **HR Dashboards & Reports** for real-time status and compliance tracking
- 📝 Full audit trail for compliance reviews

## Skills Demonstrated

- ServiceNow Certified System Administrator (CSA) fundamentals
- Service Catalog design (Catalog Items, Variables, Record Producers)
- Flow Designer (Flows, Subflows, Actions)
- Service-Level Agreements (SLA Definitions, Workflows, Breach/Notification triggers)
- Access Controls (ACLs) and role-based security
- Performance Analytics / Dashboards
- Process analysis and problem solving

## Project Structure

```
onboarding-offboarding-system/
├── README.md                 # This file
├── ARCHITECTURE.md           # System architecture & data model
├── WORKFLOWS.md              # Onboarding & offboarding process flows
├── docs/
│   ├── CATALOG_ITEMS.md      # Service Catalog item specs
│   ├── SLA_DEFINITIONS.md    # SLA rules and escalation matrix
│   └── DASHBOARD_REPORTS.md  # HR dashboard & report specs
├── screenshots/               # Add screenshots of your ServiceNow build here
└── LICENSE
```

## Getting Started (ServiceNow Developer Instance)

1. Spin up a free [ServiceNow Personal Developer Instance (PDI)](https://developer.servicenow.com/)
2. Import the Service Catalog items described in [`docs/CATALOG_ITEMS.md`](docs/CATALOG_ITEMS.md)
3. Build the Flow Designer flows described in [`WORKFLOWS.md`](WORKFLOWS.md)
4. Configure SLA definitions per [`docs/SLA_DEFINITIONS.md`](docs/SLA_DEFINITIONS.md)
5. Set up the HR dashboard per [`docs/DASHBOARD_REPORTS.md`](docs/DASHBOARD_REPORTS.md)
6. Test end-to-end by submitting a "New Hire Onboarding" catalog request

## Roadmap

- [ ] Add Integration Hub spoke for Active Directory account provisioning
- [ ] Add mobile-friendly approval experience
- [ ] Add Virtual Agent chatbot for status checks
- [ ] Add Predictive Intelligence for SLA breach risk scoring

## Author

_Add your name / contact / LinkedIn here_

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
