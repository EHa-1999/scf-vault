---
id: "DASH-Implementation"
type: dashboard
name: "Implementation Dashboard"
created: 2026-01-29
modified: 2026-01-29
tags:
  - dashboard
  - implementation
  - tracking
---

# 🚀 Implementation Dashboard

> Overview of implementation status for all security controls.

---

## Navigation

| ← Back | Up | Related |
|--------|-----|---------|
| [[Dashboards/_index\|📊 Dashboards]] | [[README\|🏠 Home]] | [[Dashboards/Compliance Dashboard\|✅ Compliance]] |

---

## Implementation vs Compliance

| Aspect | Implementation | Compliance |
|--------|----------------|------------|
| **Question** | Is it installed/configured? | Does it meet the standard? |
| **When** | During project | After validation |
| **Who** | Implementation team | Auditor / Assessor |
| **Evidence** | Configuration docs | Audit report |
| **Score** | % complete | % compliant |

> ⚠️ **Note**: A control can be 100% implemented but still not compliant (e.g., MFA installed but not activated by all users).

---

## Status Definitions

| Status | Meaning | Next Step |
|--------|---------|-----------|
| 🔴 `planned` | Not yet started | Start implementation |
| 🟡 `in_progress` | Currently being configured | Complete |
| 🟢 `completed` | Installed/configured | Validation |
| ✅ `validated` | Technically verified | Compliance assessment |

---

## Overall Status

### By Status

```dataview
TABLE WITHOUT ID
  impl_status as "Status",
  length(rows) as "Count",
  round(length(rows) / 180 * 100, 0) + "%" as "Percentage"
FROM "Controls"
WHERE type = "control"
GROUP BY impl_status
SORT impl_status ASC
```

### By Control Category

```dataview
TABLE WITHOUT ID
  category as "Category",
  length(filter(rows, (r) => r.impl_status = "validated")) as "✅",
  length(filter(rows, (r) => r.impl_status = "completed")) as "🟢",
  length(filter(rows, (r) => r.impl_status = "in_progress")) as "🟡",
  length(filter(rows, (r) => r.impl_status = "planned")) as "🔴",
  length(rows) as "Total"
FROM "Controls"
WHERE type = "control"
GROUP BY category
SORT category ASC
```

---

## CIS Controls Implementation

### CIS 1-6: Foundation Controls

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(impl_status = "validated", "✅", choice(impl_status = "completed", "🟢", choice(impl_status = "in_progress", "🟡", "🔴"))) as "Status",
  impl_percentage + "%" as "%",
  impl_owner as "Owner"
FROM "Controls/CIS"
WHERE type = "control" AND (category = "CIS 1" OR category = "CIS 2" OR category = "CIS 3" OR category = "CIS 4" OR category = "CIS 5" OR category = "CIS 6")
SORT id ASC
```

### CIS 7-12: Operational Controls

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(impl_status = "validated", "✅", choice(impl_status = "completed", "🟢", choice(impl_status = "in_progress", "🟡", "🔴"))) as "Status",
  impl_percentage + "%" as "%",
  impl_owner as "Owner"
FROM "Controls/CIS"
WHERE type = "control" AND (category = "CIS 7" OR category = "CIS 8" OR category = "CIS 9" OR category = "CIS 10" OR category = "CIS 11" OR category = "CIS 12")
SORT id ASC
```

### CIS 13-18: Advanced Controls

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(impl_status = "validated", "✅", choice(impl_status = "completed", "🟢", choice(impl_status = "in_progress", "🟡", "🔴"))) as "Status",
  impl_percentage + "%" as "%",
  impl_owner as "Owner"
FROM "Controls/CIS"
WHERE type = "control" AND (category = "CIS 13" OR category = "CIS 14" OR category = "CIS 15" OR category = "CIS 16" OR category = "CIS 17" OR category = "CIS 18")
SORT id ASC
```

---

## Extended Controls Implementation

### EXT-P: Privacy Controls

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(impl_status = "validated", "✅", choice(impl_status = "completed", "🟢", choice(impl_status = "in_progress", "🟡", "🔴"))) as "Status",
  impl_percentage + "%" as "%"
FROM "Controls/EXT-P"
WHERE type = "control"
SORT id ASC
```

### Other Extended Controls

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(impl_status = "validated", "✅", choice(impl_status = "completed", "🟢", choice(impl_status = "in_progress", "🟡", "🔴"))) as "Status",
  impl_percentage + "%" as "%"
FROM "Controls"
WHERE type = "control" AND (contains(file.path, "EXT-O") OR contains(file.path, "EXT-HR") OR contains(file.path, "EXT-PHY") OR contains(file.path, "EXT-SUP") OR contains(file.path, "EXT-BC") OR contains(file.path, "EXT-COM") OR contains(file.path, "EXT-T"))
SORT id ASC
```

---

## By System

```dataview
TABLE WITHOUT ID
  impl_system as "System",
  length(filter(rows, (r) => r.impl_status = "validated")) as "✅",
  length(filter(rows, (r) => r.impl_status = "completed")) as "🟢",
  length(filter(rows, (r) => r.impl_status = "in_progress")) as "🟡",
  length(rows) as "Total"
FROM "Controls"
WHERE type = "control" AND impl_system != "" AND impl_system != null
GROUP BY impl_system
SORT impl_system ASC
```

---

## Implementation Backlog

### Not Started (Planned, Priority 5)

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  category as "Category",
  impl_owner as "Owner"
FROM "Controls"
WHERE type = "control" AND impl_status = "planned" AND priority = 5
SORT category ASC, id ASC
LIMIT 20
```

### In Progress

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  impl_percentage + "%" as "Progress",
  impl_owner as "Owner",
  impl_date as "Expected"
FROM "Controls"
WHERE type = "control" AND impl_status = "in_progress"
SORT impl_percentage DESC
```

### Completed, Awaiting Validation

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  impl_date as "Completed",
  impl_owner as "Owner"
FROM "Controls"
WHERE type = "control" AND impl_status = "completed" AND impl_validated = false
SORT impl_date ASC
```

---

## Validation Checklist

Before a control moves from `completed` to `validated`:

- [ ] **Technical verification**: Is the configuration correctly applied?
- [ ] **Functional test**: Does the control work as intended?
- [ ] **Documentation**: Is the implementation documented?
- [ ] **Evidence**: Is evidence collected (screenshots, logs, configs)?
- [ ] **Owner approval**: Has the owner validated?

---

## Workflow

![[Assets/diagrams/Implementation-Workflow.svg]]

---

## Related Documents

- [[Dashboards/Compliance Dashboard|Compliance Dashboard]]
- [[Dashboards/Implementation Tracker|Implementation Tracker]]
- [[Planning/Implementatieplan 2026|Implementation Plan 2026]]
- [[Documentatie/System Onboarding Guide|System Onboarding Guide]]
