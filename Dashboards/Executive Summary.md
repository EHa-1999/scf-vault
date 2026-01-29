---
id: "DASH-Executive"
type: dashboard
name: "Executive Summary"
created: 2026-01-28
modified: 2026-01-28
tags:
  - dashboard
  - executive
  - management
---

# Executive Summary - Security Posture

> **Rapportage Datum:** `= date(today)`  
> **Periode:** Q1 2026

## 🎯 Security Score Overzicht

| Indicator | Waarde | Status | Trend |
|-----------|--------|--------|-------|
| **Overall Compliance** | 82% | 🟢 Op schema | ↑ +5% |
| **Kritieke Bevindingen** | 0 | 🟢 Geen | = |
| **Hoge Bevindingen** | 1 | 🟡 Actie nodig | ↓ -1 |
| **Overdue Acties** | 0 | 🟢 Geen | ↓ -2 |

## 📊 Framework Compliance

| Framework | Score | Status | Target | Deadline |
|-----------|-------|--------|--------|----------|
| **CIS Controls v8** | 82% | 🟢 | 85% | Q2 2026 |
| **ISO 27001:2022** | 78% | 🟡 | 85% | Q4 2026 |
| **NIS2 Directive** | 85% | 🟢 | 80% | Compliant |
| **BIO2** | 82% | 🟢 | 80% | Doorlopend |
| **AVG/GDPR** | 75% | 🟡 | 85% | Doorlopend |

## 📈 Implementation Voortgang

### Per Systeem

```dataview
TABLE WITHOUT ID
  regexreplace(id, "IMPL-([A-Za-z-]+)-.*", "$1") as "Systeem",
  length(filter(rows, (r) => r.status = "Verified" OR r.status = "Implemented")) as "✅ Compleet",
  length(filter(rows, (r) => r.status = "Partial" OR r.status = "In Progress")) as "🔄 In Progress",
  length(rows) as "Totaal"
FROM "Implementations"
GROUP BY regexreplace(id, "IMPL-([A-Za-z-]+)-.*", "$1")
```

### Status Verdeling

```dataview
TABLE WITHOUT ID
  status as "Status",
  length(rows) as "Aantal"
FROM "Implementations"
GROUP BY status
SORT choice(status = "Verified", 1,
  choice(status = "Implemented", 2,
    choice(status = "Partial", 3, 4))) ASC
```

## ⚠️ Risico Overzicht

### Open Risico's

```dataview
TABLE WITHOUT ID
  classification as "Ernst",
  length(rows) as "Aantal"
FROM "Risks"
WHERE status != "Closed" AND status != "Mitigated"
GROUP BY classification
SORT choice(classification = "Critical", 1,
  choice(classification = "High", 2, 3)) ASC
```

### Top Risico's

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  name as "Risico",
  classification as "Ernst"
FROM "Risks"
WHERE status != "Closed" AND (classification = "Critical" OR classification = "High")
LIMIT 5
```

## 🔍 Audit Status

### Lopende Audits

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Audit",
  scope as "Scope",
  status as "Status"
FROM "Audits"
WHERE type = "internal-audit" AND status != "Completed"
```

### Bevindingen Overzicht

```dataview
TABLE WITHOUT ID
  classification as "Ernst",
  length(rows) as "Open"
FROM "Audits"
WHERE type = "finding" AND status != "Closed"
GROUP BY classification
SORT choice(classification = "Critical", 1,
  choice(classification = "High", 2, 3)) ASC
```

### Kritieke/Hoge Bevindingen

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  name as "Bevinding",
  owner as "Eigenaar",
  due_date as "Deadline"
FROM "Audits"
WHERE type = "finding" AND (classification = "Critical" OR classification = "High") AND status != "Closed"
SORT due_date ASC
```

## 📅 Komende Deadlines

| Datum | Item | Type | Status |
|-------|------|------|--------|
| Feb 2026 | MFA uitrol privileged users | Bevinding | 🟡 |
| Mrt 2026 | Q1 Self-Assessments afronden | Audit | 🔵 |
| Apr 2026 | Interne Audit XENA | Audit | 🔵 |
| Jun 2026 | Security Awareness hertraining | Training | 🔵 |

## 📋 Kwartaal Highlights

### ✅ Gerealiseerd (Q1 2026)

- Data-at-rest encryptie volledig operationeel
- Audit logging voor alle XENA componenten
- Self-assessment proces geïmplementeerd
- LISA framework documentatie compleet

### 🎯 Gepland (Q2 2026)

- MFA uitrol naar alle privileged users
- Vulnerability management proces formaliseren
- Leveranciers risk assessments uitvoeren
- ISO 27001 gap-assessment starten

### ⚠️ Aandachtspunten

1. **MFA Coverage** - 12 accounts nog zonder MFA
2. **Patch Management** - Proces moet worden geformaliseerd
3. **Awareness Training** - Herhaling nodig voor nieuwe medewerkers

## 📊 Trend (4 kwartalen)

| Metric | Q2 '25 | Q3 '25 | Q4 '25 | Q1 '26 |
|--------|--------|--------|--------|--------|
| Compliance Score | 58% | 68% | 75% | 82% |
| Open Bevindingen | 12 | 8 | 5 | 4 |
| Kritieke Risico's | 2 | 1 | 1 | 0 |

## 💡 Management Beslispunten

| # | Onderwerp | Gevraagd | Deadline |
|---|-----------|----------|----------|
| 1 | Budget MFA uitbreiding | Goedkeuring €15K | 15 Feb |
| 2 | Security FTE uitbreiding | Beslissing 0.5 FTE | 1 Mrt |
| 3 | Tooling selectie SIEM | Vendor keuze | 15 Mrt |

---

*Automatisch gegenereerd vanuit LISA Security Control Framework*

## Gerelateerde Dashboards

- [[Dashboards/Main Dashboard|Main Dashboard]]
- [[Dashboards/Compliance Dashboard|Compliance Dashboard]]
- [[Dashboards/Audit Dashboard|Audit Dashboard]]
- [[Frameworks/LISA/1-LISA-Introductie|LISA Framework]]
