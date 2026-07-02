# Service Catalog Item Specifications

## 1. "New Hire Onboarding"

**Type:** Catalog Item (Record Producer, target table: `sc_request`)
**Category:** HR / IT Services

### Variables

| Variable Name | Type | Mandatory | Notes |
|---|---|---|---|
| employee_name | Single Line Text | Yes | Full legal name |
| employee_email | Single Line Text | No | Personal email for pre-boarding comms |
| start_date | Date | Yes | Must be a future date |
| department | Reference (Department) | Yes | Drives task routing |
| job_title | Single Line Text | Yes | |
| manager | Reference (sys_user) | Yes | Auto-notified on completion |
| location | Choice (Office/Remote/Hybrid) | Yes | Drives Facilities/Security task creation |
| equipment_needed | Multi-Select Checkbox | No | Laptop, Monitor, Headset, Phone |
| access_level | Choice (Standard/Elevated/Admin) | Yes | Drives Security/IT ACL requirements |

### Workflow Trigger
On submission, creates `sc_request` + `sc_req_item`, which triggers the **Onboarding Flow** (see `WORKFLOWS.md`).

---

## 2. "Employee Offboarding"

**Type:** Catalog Item (Record Producer, target table: `sc_request`)
**Category:** HR / IT Services

### Variables

| Variable Name | Type | Mandatory | Notes |
|---|---|---|---|
| employee_name | Reference (sys_user) | Yes | Existing employee record |
| last_working_day | Date | Yes | |
| department | Reference (Department) | Yes (auto-filled from user record) | |
| manager | Reference (sys_user) | Yes (auto-filled) | |
| termination_type | Choice (Voluntary/Involuntary/Retirement) | Yes | Drives SLA urgency |
| asset_return_required | True/False | Yes | Triggers Facilities/IT asset recovery task |
| notes | Multi Line Text | No | Any special handling instructions |

### Workflow Trigger
On submission, creates `sc_request` + `sc_req_item`, which triggers the **Offboarding Flow** (see `WORKFLOWS.md`). If `termination_type = Involuntary`, the flow applies expedited SLAs.

---

## 3. Suggested Catalog UI Policies

- Hide `equipment_needed` if `location = Remote` is false for hardware not applicable
- Make `notes` mandatory if `termination_type = Involuntary`
- Show a warning message if `start_date` (onboarding) is less than 3 business days away, since SLAs may not be met
