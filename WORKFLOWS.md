# Onboarding & Offboarding Workflows

## 1. Onboarding Workflow

### Trigger
HR or hiring manager submits the **"New Hire Onboarding"** Service Catalog item.

### Flow Steps

1. **Request Submitted**
   - Requester fills in: employee name, start date, department, role, manager, location, equipment needs
2. **Flow Designer Triggered on RITM Creation**
   - Parent flow validates required fields and looks up the employee's department
3. **Parallel Task Creation**
   - **IT Task:** Create user account, assign licenses (email, collaboration tools), provision laptop/hardware
   - **Facilities Task:** Assign desk/workspace, prepare access badge request, arrange parking (if applicable)
   - **Security Task:** Issue physical access badge, configure building/floor access levels
4. **SLA Attachment**
   - Each task gets an SLA (e.g. IT account provisioning: 2 business days before start date; badge issuance: 1 business day before start date)
5. **Progress Tracking**
   - Parent RITM state reflects aggregate child task status (In Progress → Some Complete → Complete)
6. **Completion**
   - When all child tasks close, requester and new hire's manager are notified
   - HR dashboard updates completion metrics

### Task Breakdown by Department

| Department | Sample Tasks |
|---|---|
| IT | Create AD/email account, assign software licenses, ship/configure laptop, set up VPN access |
| Facilities | Assign desk, order nameplate, arrange parking/locker |
| Security | Issue access badge, set building/floor permissions, add to visitor/employee system |

## 2. Offboarding Workflow

### Trigger
HR or manager submits the **"Employee Offboarding"** Service Catalog item (typically triggered by a termination or resignation date).

### Flow Steps

1. **Request Submitted**
   - Requester fills in: employee name, last working day, department, manager, reason (optional), asset return details
2. **Flow Designer Triggered on RITM Creation**
   - Parent flow determines urgency (e.g. involuntary termination may trigger immediate/same-day tasks)
3. **Parallel Task Creation**
   - **IT Task:** Disable/deactivate accounts, revoke software licenses, wipe/retrieve hardware, forward or archive email
   - **Facilities Task:** Collect keys/access cards, clear desk/workspace, cancel parking
   - **Security Task:** Revoke building/floor access, deactivate badge, update visitor/security systems
4. **SLA Attachment**
   - Time-critical tasks (e.g. access revocation for involuntary termination) get tighter SLAs, sometimes same-day
5. **Access Control Enforcement**
   - Only users with the Security role can confirm/close access-revocation tasks, enforced via ACLs
6. **Completion & Compliance Record**
   - All task closures logged for audit/compliance
   - HR dashboard reflects offboarding completion and any SLA breaches (a compliance risk indicator)

### Task Breakdown by Department

| Department | Sample Tasks |
|---|---|
| IT | Disable accounts, revoke licenses, retrieve/wipe hardware, archive mailbox |
| Facilities | Collect keys/badges, clear workspace, cancel parking/locker |
| Security | Revoke building access, deactivate badge, remove from access systems |

## 3. SLA & Escalation Logic (Both Workflows)

- SLA timer starts when the child task is created and assigned
- At 80% of SLA duration elapsed → warning notification to assignee and their manager
- At 100% (breach) → escalation notification to assignment group manager and logged for HR reporting
- Involuntary offboarding tasks may use a **shorter, non-standard SLA** (e.g. same business day) to mitigate security risk

## 4. Process Diagram (Text Form)

```
Onboarding:
  Submit Request → Validate → [IT Task | Facilities Task | Security Task] → SLA Monitoring → All Tasks Closed → Notify + Dashboard Update

Offboarding:
  Submit Request → Determine Urgency → [IT Task | Facilities Task | Security Task] → SLA Monitoring (tighter for involuntary) → Access Revocation Confirmed (ACL-restricted) → All Tasks Closed → Notify + Compliance Log
```
