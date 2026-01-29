---
type: index
name: "CIS Controls"
icon: "🛡️"
created: 2026-01-28
---

# 🛡️ CIS Controls v8

> 153 controls van het Center for Internet Security — de industriestandaard voor technische security.

---

## Navigatie

| ← Terug | Omhoog | Gerelateerd |
|---------|--------|-------------|
| [[Controls/_index\|📋 Controls]] | [[README\|🏠 Home]] | [[Controls/EXT-P/_index\|🔐 Privacy Controls]] |

---

## Overzicht

| Statistiek | Waarde |
|------------|--------|
| **Totaal Controls** | 153 |
| **Baseline (Comply or Explain)** | 93 |
| **Optioneel** | 60 |
| **Categorieën** | 18 |

---

## Per Categorie

Klik op een categorie om de controls te bekijken:

### Asset & Software Management
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 1\|CIS 1]] | Inventory and Control of Enterprise Assets | 5 | 1 |
| [[#CIS 2\|CIS 2]] | Inventory and Control of Software Assets | 7 | 2 |

### Data & Configuration
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 3\|CIS 3]] | Data Protection | 14 | 10 |
| [[#CIS 4\|CIS 4]] | Secure Configuration | 12 | 6 |

### Identity & Access
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 5\|CIS 5]] | Account Management | 6 | 6 |
| [[#CIS 6\|CIS 6]] | Access Control Management | 8 | 8 |

### Vulnerability & Logging
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 7\|CIS 7]] | Continuous Vulnerability Management | 7 | 5 |
| [[#CIS 8\|CIS 8]] | Audit Log Management | 12 | 6 |

### Defense & Recovery
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 9\|CIS 9]] | Email and Web Browser Protections | 7 | 4 |
| [[#CIS 10\|CIS 10]] | Malware Defenses | 7 | 4 |
| [[#CIS 11\|CIS 11]] | Data Recovery | 5 | 5 |

### Network & Monitoring
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 12\|CIS 12]] | Network Infrastructure Management | 8 | 6 |
| [[#CIS 13\|CIS 13]] | Network Monitoring and Defense | 11 | 5 |

### People & Process
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 14\|CIS 14]] | Security Awareness Training | 9 | 4 |
| [[#CIS 15\|CIS 15]] | Service Provider Management | 7 | 4 |

### Application & Incident
| Cat | Naam | Controls | Baseline |
|-----|------|----------|----------|
| [[#CIS 16\|CIS 16]] | Application Software Security | 14 | 9 |
| [[#CIS 17\|CIS 17]] | Incident Response | 9 | 9 |
| [[#CIS 18\|CIS 18]] | Penetration Testing | 5 | 3 |

---

## CIS 1
### Inventory and Control of Enterprise Assets

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 1"
SORT id ASC
```

---

## CIS 2
### Inventory and Control of Software Assets

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 2"
SORT id ASC
```

---

## CIS 3
### Data Protection

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 3"
SORT id ASC
```

---

## CIS 4
### Secure Configuration

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 4"
SORT id ASC
```

---

## CIS 5
### Account Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 5"
SORT id ASC
```

---

## CIS 6
### Access Control Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 6"
SORT id ASC
```

---

## CIS 7
### Continuous Vulnerability Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 7"
SORT id ASC
```

---

## CIS 8
### Audit Log Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 8"
SORT id ASC
```

---

## CIS 9
### Email and Web Browser Protections

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 9"
SORT id ASC
```

---

## CIS 10
### Malware Defenses

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 10"
SORT id ASC
```

---

## CIS 11
### Data Recovery

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 11"
SORT id ASC
```

---

## CIS 12
### Network Infrastructure Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 12"
SORT id ASC
```

---

## CIS 13
### Network Monitoring and Defense

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 13"
SORT id ASC
```

---

## CIS 14
### Security Awareness Training

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 14"
SORT id ASC
```

---

## CIS 15
### Service Provider Management

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 15"
SORT id ASC
```

---

## CIS 16
### Application Software Security

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 16"
SORT id ASC
```

---

## CIS 17
### Incident Response

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 17"
SORT id ASC
```

---

## CIS 18
### Penetration Testing

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "ID",
  control_name as "Control",
  choice(baseline, "🔒", "📘") as "BL",
  implementation_group as "IG"
FROM "Controls/CIS"
WHERE category = "CIS 18"
SORT id ASC
```

---

## Legenda

| Symbool | Betekenis |
|---------|-----------|
| 🔒 | Baseline (Comply or Explain) |
| 📘 | Optioneel |
| IG1 | Implementation Group 1 (Basic) |
| IG2 | Implementation Group 2 (Foundational) |
| IG3 | Implementation Group 3 (Organizational) |
