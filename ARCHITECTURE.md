# System Architecture

## 1. High-Level Architecture

```
                    ┌─────────────────────┐
                    │   Employee / HR      │
                    │   (Requester)        │
                    └──────────┬───────────┘
                               │ submits
                               ▼
                    ┌─────────────────────┐
                    │  Service Catalog     │
                    │  - New Hire Onboard  │
                    │  - Offboarding       │
                    └──────────┬───────────┘
                               │ creates
                               ▼
                    ┌─────────────────────┐
                    │  Request / RITM      │
                    └──────────┬───────────┘
                               │ triggers
                               ▼
                    ┌─────────────────────┐
                    │  Flow Designer Flow  │
                    │  (Orchestration)     │
                    └──────────┬───────────┘
                               │ spawns
             ┌─────────────────┼─────────────────┐
             ▼                 ▼                 ▼
     ┌───────────────┐ ┌───────────────┐ ┌───────────────┐
     │   IT Task      │ │ Facilities    │ │  Security     │
     │  (accounts,    │ │ Task (desk,   │ │  Task (badge, │
     │   hardware)    │ │  seating)     │ │   access)     │
     └───────┬────────┘ └───────┬───────┘ └───────┬───────┘
             │                  │                  │
             └────────── SLA-monitored ─────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  HR Dashboard &      │
                    │  Reports             │
                    └─────────────────────┘
```

## 2. Core Components

### 2.1 Service Catalog Layer
- **Catalog Items:** "New Hire Onboarding" and "Employee Offboarding" record producers/catalog items
- **Variables:** Employee name, department, role, manager, start/end date, location, equipment needs, access level
- **Variable Sets:** Reusable across both catalog items where applicable (e.g. employee lookup)

### 2.2 Process/Orchestration Layer
- **Flow Designer:** A parent flow triggered on RITM creation
- **Subflows:** Separate subflows per department (IT, Facilities, Security) so each team's task logic is isolated and reusable
- **Actions:** Task creation, assignment group lookup, notification actions, SLA attachment

### 2.3 Task & Assignment Layer
- Child tasks (`sc_task`) created per department, linked to the parent RITM
- Assignment group determined by department + task type (e.g. `IT Support`, `Facilities`, `Corporate Security`)
- **Access Controls (ACLs)** restrict who can view/update sensitive tasks (e.g. only Security role can close access-revocation tasks)

### 2.4 SLA Layer
- **SLA Definitions** attached to each task type with start/pause/stop conditions
- Escalation notifications sent to assignment group manager when a task approaches breach
- Breach events logged for reporting

### 2.5 Reporting/Dashboard Layer
- **Performance Analytics / Reporting** module aggregates:
  - Open vs. closed onboarding/offboarding requests
  - Average time-to-complete per department
  - SLA compliance rate
  - Overdue/breached tasks
- Dashboard shared with HR leadership with role-based visibility

## 3. Data Model (Simplified)

| Table | Purpose |
|---|---|
| `sc_cat_item` | Catalog item definitions (Onboarding, Offboarding) |
| `sc_request` / `sc_req_item` | Parent request and requested item records |
| `sc_task` | Department-specific child tasks (IT, Facilities, Security) |
| `contract_sla` / `task_sla` | SLA definitions and instances per task |
| `sys_user_group` | Assignment groups (IT Support, Facilities, Security) |
| `sys_security_acl` | Access control rules per table/field |
| `pa_dashboards` / reports | HR dashboard and report definitions |

## 4. Security Model

- Role-based ACLs on `sc_task` restrict field-level edits (e.g. only assigned group can update `state`)
- Sensitive offboarding fields (e.g. access revocation confirmation) restricted to the Security role
- HR dashboard visibility restricted to HR and management roles via Performance Analytics permissions

## 5. Notifications

| Event | Recipient | Channel |
|---|---|---|
| New request submitted | Requester + assigned teams | Email |
| Task assigned | Assignment group | Email / Notification |
| SLA at risk (e.g. 80% elapsed) | Assignee + manager | Email |
| SLA breached | Assignee's manager + HR | Email |
| All tasks complete | Requester + HR | Email |
