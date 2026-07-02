# SLA Definitions & Escalation Matrix

## 1. Onboarding SLAs

| Task | Assignment Group | SLA Duration | Start Condition | Stop Condition |
|---|---|---|---|---|
| Create user account & licenses | IT Support | 2 business days before start date | Task created | Task state = Closed Complete |
| Provision hardware (laptop, monitor) | IT Support | 3 business days before start date | Task created | Task state = Closed Complete |
| Assign desk/workspace | Facilities | 2 business days before start date | Task created | Task state = Closed Complete |
| Issue building access badge | Security | 1 business day before start date | Task created | Task state = Closed Complete |

## 2. Offboarding SLAs

| Task | Assignment Group | SLA Duration | Notes |
|---|---|---|---|
| Disable user account | IT Support | Same business day (involuntary) / 1 day (voluntary) | Highest priority for involuntary terminations |
| Revoke software licenses | IT Support | 1 business day | |
| Retrieve/wipe hardware | IT Support | 3 business days | |
| Revoke building access | Security | Same business day (involuntary) / 1 day (voluntary) | ACL-restricted to Security role |
| Collect keys/badges | Facilities | 2 business days | |

## 3. Escalation Rules

| Elapsed % of SLA | Action |
|---|---|
| 50% | Reminder notification to assignee |
| 80% | Warning notification to assignee + their manager |
| 100% (Breach) | Escalation to assignment group manager, logged as SLA breach, flagged on HR dashboard |

## 4. Business Rules Notes

- SLA schedules should respect the assignment group's **business hours/holiday schedule**
- Involuntary offboarding SLAs should ideally use a **24/7 schedule** rather than standard business hours, given the security sensitivity
- SLA breach records feed directly into the compliance report described in `DASHBOARD_REPORTS.md`
