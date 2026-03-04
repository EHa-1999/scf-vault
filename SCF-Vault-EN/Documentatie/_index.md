---
type: index
name: "Documentatie"
icon: "📚"
created: 2026-01-28
---

# 📚 Documentation

> Guides, procedures and reference documents — everything you need to know.

---

## Navigation

| ← Back | Up |
|--------|-----|
| [[README\|🏠 Home]] | — |

---

## Start Here

New to the framework? Start with these documents:

| Document | Description | Time |
|----------|-------------|------|
| [[Documentatie/SCF Architectuur\|SCF Architecture]] | How the framework is structured | 15 min |
| [[Documentatie/Dual Scoring Model\|Dual Scoring Model]] | Implementation vs. Compliance scores | 10 min |
| [[Documentatie/Handleiding\|User Guide]] | Daily use of the vault | 10 min |
| [[Frameworks/LISA/1-LISA-Introductie\|LISA Introduction]] | The framework philosophy | 20 min |

---

### Dual Scoring Model

The framework uses two separate scores for complete tracking:

→ [[Documentatie/Dual Scoring Model|Dual Scoring Model]]

| Score | Question | Dashboard |
|-------|----------|-----------|
| 🚀 **Implementation** | Is it installed? | [[Dashboards/Implementation Dashboard\|Implementation]] |
| ✅ **Compliance** | Does it meet the standard? | [[Dashboards/Compliance Dashboard\|Compliance]] |

---

## Procedures

### System Onboarding

How do you onboard a new system into the framework?

→ [[Documentatie/System Onboarding Guide|System Onboarding Guide]]

Steps:
1. System registration and classification
2. System Component Breakdown (SCB)
3. Control mapping and gap analysis
4. Implementation planning
5. Documentation and sign-off

---

### CIS Benchmark Mapping

How to use CIS Benchmarks and when to create an Extended Benchmark?

→ [[Documentatie/CIS Benchmark Mapping Guide|CIS Benchmark Mapping Guide]]

---

## System Component Breakdowns (SCB)

Detailed technical documentation per system:

| System | Document | Status |
|--------|----------|--------|
| XENA | [[Documentatie/SCB/SCB-XENA\|SCB-XENA]] | ✅ Complete |
| ZGW | SCB-ZGW | 📋 Planned |

---

## Extended Benchmarks

Custom security benchmarks for technologies without official CIS Benchmark:

| Technology | Document |
|------------|----------|
| MinIO | [[Documentatie/Benchmarks/EXT-MinIO\|EXT-MinIO]] |
| Apache NiFi | 📋 Planned |
| KeyCloak | 📋 Planned |
| OpenBAO | 📋 Planned |

---

## Framework Documentation

Extended documentation about the LISA framework itself:

```dataview
TABLE WITHOUT ID
  link(file.link, file.name) as "Document"
FROM "Frameworks/LISA"
SORT file.name ASC
```

---

## All Documents

```dataview
TABLE WITHOUT ID
  link(file.link, file.name) as "Document",
  type as "Type"
FROM "Documentatie"
WHERE file.name != "_index"
SORT file.name ASC
```

---

## Related Sections

- [[Templates/_index|📝 Templates]] — Reusable templates
- [[Planning/_index|📅 Planning]] — Roadmaps and calendars
