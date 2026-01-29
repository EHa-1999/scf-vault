---
id: "DASH-Compliance"
type: dashboard
name: "Compliance Dashboard"
created: 2026-01-28
modified: 2026-01-28
tags:
  - dashboard
  - compliance
---

# Compliance Dashboard

## Overall Compliance Score

| Framework | Controls | Compliant | Partial | Gap | Score |
|-----------|----------|-----------|---------|-----|-------|
| **CIS Controls v8** | 153 | 110 | 25 | 18 | 82% |
| **Extended Privacy** | 27 | 16 | 6 | 5 | 70% |
| **Totaal** | 180 | 126 | 31 | 23 | 80% |

## ISO 27001:2022 Compliance

### Per Annex Categorie

| Annex | Naam | Controls | Score |
|-------|------|----------|-------|
| A.5 | Organisational Controls | 37 | 75% |
| A.6 | People Controls | 8 | 80% |
| A.7 | Physical Controls | 14 | 70% |
| A.8 | Technological Controls | 34 | 85% |

### ISO Controls Status

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  name as "Naam",
  iso27001 as "ISO Annex"
FROM "Controls/CIS"
WHERE iso27001 != null AND iso27001 != ""
SORT iso27001 ASC
LIMIT 15
```

## NIS2 Directive Compliance

| Artikel | Onderwerp | Score | Status |
|---------|-----------|-------|--------|
| Art. 21(2)(a) | Risicoanalyse en beleid | 85% | 🟢 |
| Art. 21(2)(b) | Incidentafhandeling | 70% | 🟡 |
| Art. 21(2)(c) | Bedrijfscontinuïteit | 80% | 🟢 |
| Art. 21(2)(d) | Ketenbeveiliging | 60% | 🟡 |
| Art. 21(2)(e) | Netwerkbeveiliging | 90% | 🟢 |
| Art. 21(2)(f) | Kwetsbaarheidsbeheer | 65% | 🟡 |
| Art. 21(2)(g) | Beveiligingsassessment | 85% | 🟢 |
| Art. 21(2)(h) | Cryptografie | 95% | 🟢 |
| Art. 21(2)(i) | Personeelsbeveiliging | 70% | 🟡 |
| Art. 21(2)(j) | Toegangsbeheer & MFA | 75% | 🟡 |

## BIO2 Compliance

### Per Domein

| Domein | Onderwerp | Score |
|--------|-----------|-------|
| 5 | Informatiebeveiligingsbeleid | 90% |
| 6 | Organisatie van IB | 85% |
| 7 | Personeelsbeveiliging | 75% |
| 8 | Beheer van bedrijfsmiddelen | 80% |
| 9 | Toegangsbeveiliging | 80% |
| 10 | Cryptografie | 95% |
| 11 | Fysieke beveiliging | 70% |
| 12 | Beveiliging bedrijfsvoering | 85% |
| 13 | Communicatiebeveiliging | 85% |
| 14 | Acquisitie en ontwikkeling | 75% |
| 15 | Leveranciersrelaties | 60% |
| 16 | Incidentbeheer | 70% |
| 17 | Bedrijfscontinuïteit | 80% |
| 18 | Naleving | 85% |

## AVG/GDPR - Privacy Controls

### Extended Privacy Controls Status

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  name as "Naam",
  status as "Status"
FROM "Controls/EXT-P"
SORT id ASC
```

### Privacy Domeinen

| Domein | Controls | Score |
|--------|----------|-------|
| Governance (P1) | 3 | 80% |
| DPIA (P2) | 2 | 75% |
| Dataminimalisatie (P3) | 2 | 70% |
| Doelbinding (P4) | 2 | 85% |
| Toegangsbeperking (P5) | 3 | 80% |
| Anonimisering (P6) | 1 | 60% |
| Transparantie (P7) | 2 | 75% |
| Rechten Betrokkenen (P8) | 5 | 65% |
| Grondslagen (P9) | 2 | 80% |
| Privacy by Design (P10) | 2 | 70% |
| Datalekken (P11) | 2 | 90% |
| Awareness (P12) | 1 | 75% |

## CIS Controls v8 - Per Categorie

| Cat | Naam | Controls | Impl. | Score |
|-----|------|----------|-------|-------|
| 1 | Asset Inventory | 5 | 4 | 80% |
| 2 | Software Inventory | 7 | 5 | 71% |
| 3 | Data Protection | 14 | 12 | 86% |
| 4 | Secure Configuration | 12 | 10 | 83% |
| 5 | Account Management | 6 | 5 | 83% |
| 6 | Access Control | 8 | 6 | 75% |
| 7 | Vulnerability Mgmt | 7 | 4 | 57% |
| 8 | Audit Logging | 12 | 11 | 92% |
| 9 | Email/Browser | 7 | 5 | 71% |
| 10 | Malware Defense | 7 | 6 | 86% |
| 11 | Data Recovery | 5 | 5 | 100% |
| 12 | Network Infrastructure | 8 | 7 | 88% |
| 13 | Network Monitoring | 11 | 9 | 82% |
| 14 | Security Awareness | 9 | 6 | 67% |
| 15 | Service Provider Mgmt | 7 | 4 | 57% |
| 16 | Application Security | 14 | 10 | 71% |
| 17 | Incident Response | 9 | 7 | 78% |
| 18 | Penetration Testing | 5 | 3 | 60% |

## Gap Analysis

### Hoogste Prioriteit Gaps (IG1)

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  name as "Naam",
  security_requirement as "SR"
FROM "Controls/CIS"
WHERE implementation_group = "IG1"
SORT priority DESC
LIMIT 10
```

### Controls per Security Requirement

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "SR",
  name as "Security Requirement"
FROM "Frameworks/Security-Requirements"
SORT id ASC
```

## Compliance Trend

| Maand | CIS | Privacy | ISO | NIS2 | BIO2 |
|-------|-----|---------|-----|------|------|
| Jan 2026 | 82% | 70% | 78% | 85% | 82% |
| Dec 2025 | 78% | 65% | 74% | 82% | 78% |
| Nov 2025 | 74% | 60% | 70% | 78% | 74% |
| Okt 2025 | 70% | 55% | 66% | 75% | 70% |

## Certificering & Assessment Status

| Item | Type | Target | Status | Gap |
|------|------|--------|--------|-----|
| ISO 27001 | Certificering | Q4 2026 | 78% (need 85%) | -7% |
| NIS2 | Compliance | Okt 2024 | 85% (need 80%) | ✅ |
| BIO Self-Assessment | Assessment | Q2 2026 | 82% (need 80%) | ✅ |
| DigiD Assessment | Assessment | Q3 2026 | TBD | - |

## Acties voor Compliance Verbetering

| Prio | Actie | Impact | Framework | Deadline |
|------|-------|--------|-----------|----------|
| 🔴 | MFA privileged users | +3% | CIS, NIS2 | Feb 2026 |
| 🔴 | Vulnerability scanning | +4% | CIS, ISO | Mrt 2026 |
| 🟡 | Vendor assessments | +5% | NIS2, BIO | Apr 2026 |
| 🟡 | Awareness training | +2% | CIS, ISO | Mei 2026 |
| 🟢 | Documentatie | +1% | Alle | Jun 2026 |

## Evidence Coverage

| Type | Aanwezig | Ontbreekt | % |
|------|----------|-----------|---|
| Configuratie | 45 | 8 | 85% |
| Test resultaten | 32 | 15 | 68% |
| Proces docs | 28 | 10 | 74% |
| Approvals | 22 | 12 | 65% |
| **Totaal** | **127** | **45** | **74%** |

## Gerelateerde Dashboards

- [[Dashboards/Main Dashboard|Main Dashboard]]
- [[Dashboards/Executive Summary|Executive Summary]]
- [[Dashboards/Audit Dashboard|Audit Dashboard]]
- [[Dashboards/Implementation Tracker|Implementation Tracker]]
