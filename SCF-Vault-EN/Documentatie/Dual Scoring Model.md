---
id: "DOC-Dual-Scoring"
type: documentation
name: "Dual Scoring Model"
created: 2026-01-29
modified: 2026-01-29
tags:
  - documentation
  - scoring
  - implementation
  - compliance
---

# Dual Scoring Model

> Two scores, two questions, one complete picture.

---

## Navigation

| ← Back | Up | Related |
|--------|-----|---------|
| [[Documentatie/_index\|📚 Documentation]] | [[README\|🏠 Home]] | [[Dashboards/Implementation Dashboard\|🚀 Implementation]] |

---

## Why Two Scores?

The SCF-Vault framework distinguishes between **implementation** and **compliance** because these answer two fundamentally different questions:

| Question | Score | Who | When |
|----------|-------|-----|------|
| "Is the control installed?" | **Implementation** | Project team | During implementation |
| "Does it meet the standard?" | **Compliance** | Auditor / Assessor | After validation |

### The Problem with One Score

A single score can be misleading:

- **MFA is 100% installed** in KeyCloak...
- ...but **only 94% of users** have activated it
- Is the control "compliant"? No, not fully.

With two scores:
- `impl_percentage: 100%` → technically fully configured
- `compliance_score: 94%` → not all users comply

---

## The Two Scores

### 🚀 Implementation Score

**Question:** "Is the technical configuration complete?"

| Field | Type | Values |
|-------|------|--------|
| `impl_status` | enum | `planned` → `in_progress` → `completed` → `validated` |
| `impl_percentage` | number | 0-100 |
| `impl_validated` | boolean | false / true |
| `impl_date` | date | Validation date |
| `impl_owner` | string | Responsible party |
| `impl_system` | string | Implementing system |

**Focus:** Project progress, technical realization

### ✅ Compliance Score

**Question:** "Does the implementation meet the standard?"

| Field | Type | Values |
|-------|------|--------|
| `compliance_status` | enum | `not_assessed` → `non_compliant` → `partial` → `compliant` |
| `compliance_score` | number | 0-100 (null if not assessed) |
| `compliance_assessed` | date | Date of last assessment |
| `compliance_assessor` | string | Who assessed |
| `compliance_evidence` | list | Links to evidence |

**Focus:** Audit readiness, standard compliance

---

## Workflow

![[Assets/diagrams/Implementation-Workflow.svg]]

### Phase 1: Implementation

```
PLANNED → IN_PROGRESS → COMPLETED → VALIDATED
```

1. **Planned** (`impl_status: "planned"`)
   - Control is on the roadmap
   - No work started yet
   - `impl_percentage: 0`

2. **In Progress** (`impl_status: "in_progress"`)
   - Actively configuring
   - `impl_percentage: 1-99`

3. **Completed** (`impl_status: "completed"`)
   - Technically finished
   - `impl_percentage: 100`
   - Awaiting validation

4. **Validated** (`impl_status: "validated"`)
   - Technically verified by owner
   - `impl_validated: true`
   - Ready for compliance assessment

### Phase 2: Compliance Assessment

![[Assets/diagrams/Compliance-Assessment-Workflow.svg]]

Only **after validation** can compliance be assessed:

| Assessment Type | Frequency | By Whom |
|-----------------|-----------|---------|
| Self-Assessment | Quarterly | Control owner |
| Internal Audit | Annually | CISO / Internal Audit |
| External Audit | Annually | External auditor |

### Compliance Status

| Status | Score Range | Meaning |
|--------|-------------|---------|
| 🟢 `compliant` | 80-100% | Meets the standard |
| 🟡 `partial` | 31-79% | Partially compliant |
| 🔴 `non_compliant` | 0-30% | Does not meet |
| ⬜ `not_assessed` | - | No assessment yet |

---

## YAML Frontmatter Example

```yaml
---
id: "CIS-6.5"
control_name: "Require MFA for Administrative Access"
type: control

# ─────────────────────────────────────────────────────────────────────
# Implementation Tracking
# ─────────────────────────────────────────────────────────────────────
impl_status: "validated"
impl_percentage: 100
impl_validated: true
impl_date: 2026-01-15
impl_owner: "Security Team"
impl_system: "KeyCloak"

# ─────────────────────────────────────────────────────────────────────
# Compliance Tracking
# ─────────────────────────────────────────────────────────────────────
compliance_status: "partial"
compliance_score: 94
compliance_assessed: 2026-01-20
compliance_assessor: "J. Smith"
compliance_evidence:
  - "[[Audits/2026/SA-2026-Q1]]"
compliance_notes: "3 of 50 admin accounts without MFA activated"
---
```

---

## Practical Example: MFA Implementation

### Situation

The Security Team has implemented MFA in KeyCloak for all administrators.

### Implementation Perspective

| Aspect | Status |
|--------|--------|
| KeyCloak MFA module | ✅ Installed |
| Configuration | ✅ Correct |
| Documentation | ✅ Updated |
| Technical test | ✅ Passed |

**Conclusion:** `impl_status: "validated"`, `impl_percentage: 100`

### Compliance Perspective

| Aspect | Finding |
|--------|---------|
| Total admin accounts | 50 |
| MFA activated | 47 |
| MFA not activated | 3 |
| Compliance percentage | 94% |

**Conclusion:** `compliance_status: "partial"`, `compliance_score: 94`

### Action

The 3 accounts without MFA must be addressed:
1. Notify users
2. Set deadline
3. Escalate if needed
4. Re-assess after 30 days

---

## Dashboards

### Implementation Dashboard

→ [[Dashboards/Implementation Dashboard|🚀 Implementation Dashboard]]

Shows:
- Status per control (planned/in_progress/completed/validated)
- Progress per category
- Backlog and validation queue

### Compliance Dashboard

→ [[Dashboards/Compliance Dashboard|✅ Compliance Dashboard]]

Shows:
- Compliance status of validated controls
- Framework compliance (NIS2, ISO 27001, BIO2)
- Assessment backlog
- Action items for non-compliant controls

### Executive Summary

→ [[Dashboards/Executive Summary|📈 Executive Summary]]

Shows both scores in one overview for management.

---

## Dataview Queries

### All Validated but Not-Assessed Controls

```dataview
TABLE
  control_name as "Control",
  impl_date as "Validated on"
FROM "Controls"
WHERE impl_status = "validated" AND compliance_status = "not_assessed"
SORT impl_date ASC
```

### Controls with Compliance Gaps

```dataview
TABLE
  control_name as "Control",
  compliance_score + "%" as "Score",
  compliance_notes as "Notes"
FROM "Controls"
WHERE compliance_status = "partial" OR compliance_status = "non_compliant"
SORT compliance_score ASC
```

---

## Best Practices

### 1. Implementation First, Compliance Later

Assess compliance only **after** technical validation. A half-installed control cannot be compliant.

### 2. Collect Evidence

Gather evidence during assessment:
- Configuration screenshots
- Log files
- Test results
- Interview notes

### 3. Regular Re-assessment

Compliance is not a one-time activity:
- **Quarterly:** Self-assessments
- **Annually:** Internal audit
- **On changes:** Re-assessment

### 4. Action Plans for Gaps

For `partial` or `non_compliant`:
1. Document the gap in `compliance_notes`
2. Create an action plan
3. Schedule re-assessment
4. Track in [[Dashboards/Risk Dashboard|Risk Dashboard]]

---

## Related Documents

- [[Documentatie/System Onboarding Guide|System Onboarding Guide]]
- [[Frameworks/LISA/7-LISA-Audits|LISA Audits]]
- [[Dashboards/_index|Dashboards Overview]]
- [[Templates/Control Template|Control Template]]
