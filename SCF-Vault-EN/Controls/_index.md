---
type: index
name: "Controls"
icon: "📋"
created: 2026-01-28
---

# 📋 Security Controls

> 180 controls die samen de security baseline vormen — van asset management tot pentesting.

---

## Navigatie

| ← Terug | Omhoog | Gerelateerd |
|---------|--------|-------------|
| [[README\|🏠 Home]] | — | [[Frameworks/_index\|🏛️ Frameworks]] · [[Implementations/_index\|⚙️ Implementations]] |

---

## Wat vind je hier?

Deze map bevat alle **security controls** van het LISA framework, verdeeld over twee categorieën:

| Categorie | Aantal | Baseline | Beschrijving |
|-----------|--------|----------|--------------|
| [[Controls/CIS/_index\|CIS Controls v8]] | 153 | 93 | Center for Internet Security best practices |
| [[Controls/EXT-P/_index\|Privacy Controls]] | 27 | 27 | Extended privacy controls voor AVG compliance |
| **Totaal** | **180** | **120** | |

---

## Quick Stats

### Per Prioriteit

```dataview
TABLE WITHOUT ID
  priority_label as "Prioriteit",
  length(rows) as "Aantal",
  length(filter(rows, (r) => r.baseline = true)) as "Baseline"
FROM "Controls"
WHERE type = "control"
GROUP BY priority_label
SORT priority DESC
```

### Baseline vs Optioneel

```dataview
TABLE WITHOUT ID
  choice(baseline, "🔒 Baseline", "📘 Optioneel") as "Type",
  length(rows) as "Aantal"
FROM "Controls"
WHERE type = "control"
GROUP BY baseline
```

---

## CIS Controls per Categorie

```dataview
TABLE WITHOUT ID
  category as "Cat",
  category_name as "Domein",
  length(rows) as "Controls",
  length(filter(rows, (r) => r.baseline = true)) as "Baseline"
FROM "Controls/CIS"
WHERE type = "control"
GROUP BY category, category_name
SORT category ASC
```

→ [[Controls/CIS/_index|Bekijk alle CIS Controls]]

---

## Privacy Controls per Domein

```dataview
TABLE WITHOUT ID
  category as "Cat",
  category_name as "Domein",
  length(rows) as "Controls"
FROM "Controls/EXT-P"
WHERE type = "control"
GROUP BY category, category_name
SORT category ASC
```

→ [[Controls/EXT-P/_index|Bekijk alle Privacy Controls]]

---

## Zoeken in Controls

### Op Security Requirement

```dataview
TABLE WITHOUT ID
  security_requirement as "SR",
  length(rows) as "Controls"
FROM "Controls"
WHERE type = "control"
FLATTEN security_requirement
GROUP BY security_requirement
SORT security_requirement ASC
```

### Hoogste Prioriteit Baseline

```dataview
TABLE WITHOUT ID
  link(file.link, id) as "Control",
  control_name as "Naam",
  category_name as "Domein"
FROM "Controls"
WHERE baseline = true AND priority >= 4
SORT priority DESC
LIMIT 10
```

---

## Hoe controls gebruiken?

1. **Zoek** de relevante control via categorie of security requirement
2. **Bekijk** de control details (prioriteit, frameworks, baseline status)
3. **Maak** een Implementation document dat de control koppelt aan een component
4. **Documenteer** evidence en Definition of Done

→ [[Documentatie/System Onboarding Guide|System Onboarding Guide]]  
→ [[Documentatie/CIS Benchmark Mapping Guide|CIS Benchmark Mapping]]

---

## Gerelateerde Secties

- [[Frameworks/_index|🏛️ Frameworks]] — Waar controls vandaan komen
- [[Implementations/_index|⚙️ Implementations]] — Hoe controls worden toegepast
- [[Dashboards/Baseline Dashboard|🔒 Baseline Dashboard]] — Comply or Explain monitoring
