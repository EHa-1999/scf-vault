---
id: "DASH-Compliance"
type: dashboard
name: "Compliance Dashboard"
created: 2026-01-29
modified: 2026-01-29
tags:
  - dashboard
  - compliance
  - audit
---

# ✅ Compliance Dashboard

> Compliance status based on assessments and audits — only for validated implementations.

---

## Navigation

| ← Back | Up | Related |
|--------|-----|---------|
| [[Dashboards/_index\|📊 Dashboards]] | [[README\|🏠 Home]] | [[Dashboards/Implementation Dashboard\|🚀 Implementation]] |

---

## Compliance vs Implementation

| Aspect | Implementation | Compliance |
|--------|----------------|------------|
| **Question** | Is it installed? | Does it meet the standard? |
| **When** | During project | After validation |
| **Who** | Implementation team | Auditor / Assessor |
| **Evidence** | Configuration docs | Audit report |
| **Score** | % complete | % compliant |

> ⚠️ **Note**: A control can be 100% implemented but still not compliant (e.g., MFA installed but not activated by all users).

---

## Compliance Statuses

| Status | Meaning | Score Range |
|--------|---------|-------------|
| ⬜ `not_assessed` | Not yet assessed | - |
| 🔴 `non_compliant` | Does not meet requirements | 0-30% |
| 🟡 `partial` | Partially compliant | 31-79% |
| 🟢 `compliant` | Fully compliant | 80-100% |

---

## Overall Compliance Status

### By Status (Validated Controls Only)

```dataview
TABLE WITHOUT ID
  compliance_status as "Status",
  length(rows) as "Count"
FROM "Controls"
WHERE type = "control" AND impl_status = "validated"
GROUP BY compliance_status
SORT compliance_status ASC
```

### Compliance Score by Category

```dataview
TABLE WITHOUT ID
  category as "Category",
  length(filter(rows, (r) => r.impl_status = "validated")) as "Validated",
  length(filter(rows, (r) => r.compliance_status = "compliant")) as "🟢",
  length(filter(rows, (r) => r.compliance_status = "partial")) as "🟡",
  length(filter(rows, (r) => r.compliance_status = "non_compliant")) as "🔴"
FROM "Controls"
WHERE type = "control"
GROUP BY category
SORT category ASC
```

---

## Framework Compliance

### NIS2 Directive Compliance

```dataview
TABLE WITHOUT ID
  nis2 as "Article",
  length(rows) as "Controls",
  length(filter(rows, (r) => r.compliance_status = "compliant")) as "🟢",
  length(filter(rows, (r) => r.compliance_status = "partial")) as "🟡",
  length(filter(rows, (r) => r.compliance_status = "non_compliant")) as "🔴"
FROM "Controls"
WHERE type = "control" AND nis2 != null AND nis2 != "" AND impl_status = "validated"
GROUP BY nis2
SORT nis2 ASC
```

### ISO 27001:2022 Compliance

```dataview
TABLE WITHOUT ID
  iso27001 as "Annex",
  length(rows) as "Controls",
  length(filter(rows, (r) => r.compliance_status = "compliant")) as "🟢",
  length(filter(rows, (r) => r.compliance_status = "partial")) as "🟡",
  length(filter(rows, (r) => r.compliance_status = "non_compliant")) as "🔴"
FROM "Controls"
WHERE type = "control" AND iso27001 != null AND iso27001 != "" AND impl_status = "validated"
GROUP BY iso27001
SORT iso27001 ASC
LIMIT 20
```

### BIO2 Compliance

```dataview
TABLE WITHOUT ID
  bio2 as "Measure",
  length(rows) as "Controls",
  length(filter(rows, (r) => r.compliance_status = "compliant")) as "🟢",
  length(filter(rows, (r) => r.compliance_status = "partial")) as "🟡",
  length(filter(rows, (r) => r.compliance_status = "non_compliant")) as "🔴"
FROM "Controls"
WHERE type = "control" AND bio2 != null AND bio2 != "" AND impl_status = "validated"
GROUP BY bio2
SORT bio2 ASC
LIMIT 20
```

---

## Compliance Details

### CIS Controls - Compliance Status

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(compliance_status = "compliant", "🟢", choice(compliance_status = "partial", "🟡", choice(compliance_status = "non_compliant", "🔴", "⬜"))) as "Status",
  compliance_score as "Score",
  compliance_assessed as "Assessed",
  compliance_assessor as "Assessor"
FROM "Controls/CIS"
WHERE type = "control" AND impl_status = "validated"
SORT compliance_status ASC, id ASC
```

### Extended Controls - Compliance Status

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  choice(compliance_status = "compliant", "🟢", choice(compliance_status = "partial", "🟡", choice(compliance_status = "non_compliant", "🔴", "⬜"))) as "Status",
  compliance_score as "Score",
  compliance_assessed as "Assessed"
FROM "Controls"
WHERE type = "control" AND impl_status = "validated" AND !contains(file.path, "CIS")
SORT id ASC
```

---

## Assessment Backlog

### Validated but Not Yet Assessed

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  category as "Category",
  priority as "Priority",
  impl_date as "Validated On"
FROM "Controls"
WHERE type = "control" AND impl_status = "validated" AND compliance_status = "not_assessed"
SORT priority DESC, impl_date ASC
```

### Partially Compliant - Action Required

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  compliance_score + "%" as "Score",
  compliance_assessed as "Assessed"
FROM "Controls"
WHERE type = "control" AND compliance_status = "partial"
SORT compliance_score ASC
```

### Non-Compliant - Critical Gaps

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  compliance_score + "%" as "Score",
  compliance_assessor as "Assessor"
FROM "Controls"
WHERE type = "control" AND compliance_status = "non_compliant"
SORT priority DESC
```

---

## Compliance Assessment Process

### Workflow

![[Assets/diagrams/Compliance-Assessment-Workflow.svg]]

### Assessment Types

| Type | Frequency | By Whom | Depth |
|------|-----------|---------|-------|
| **Self-Assessment** | Quarterly | Control owner | Basic check |
| **Internal Audit** | Annually | CISO / Internal Audit | Full |
| **External Audit** | Annually | External auditor | Certification |

---

## Evidence Overview

### Controls with Evidence

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  compliance_evidence as "Evidence"
FROM "Controls"
WHERE type = "control" AND compliance_evidence != null AND length(compliance_evidence) > 0
SORT id ASC
LIMIT 20
```

---

## Compliance Checklist

For each compliance assessment:

- [ ] **Control validated?** Implementation must have status "validated"
- [ ] **Effectiveness tested?** Does the control work in practice?
- [ ] **Completeness?** Does the implementation cover all aspects of the control?
- [ ] **Evidence collected?** Screenshots, logs, configurations, interviews
- [ ] **Deviations documented?** What's missing, why, action plan
- [ ] **Score determined?** 0-100% based on findings
- [ ] **Status set?** compliant / partial / non_compliant

---

## Recent Assessments

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Name",
  compliance_status as "Status",
  compliance_score + "%" as "Score",
  compliance_assessed as "Date",
  compliance_assessor as "Assessor"
FROM "Controls"
WHERE type = "control" AND compliance_assessed != null
SORT compliance_assessed DESC
LIMIT 15
```

---

## Related Documents

- [[Dashboards/Implementation Dashboard|Implementation Dashboard]]
- [[Dashboards/Audit Dashboard|Audit Dashboard]]
- [[Audits/_index|Audits Overview]]
- [[Dashboards/Executive Summary|Executive Summary]]
