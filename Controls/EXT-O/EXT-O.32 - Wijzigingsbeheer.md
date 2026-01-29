---
id: "EXT-O.32"
type: control
category: "EXT-O4"
category_name: "Operational Security"
control_name: "Wijzigingsbeheer"
priority: 5
priority_label: "Critical"
baseline: true
control_type: "Organizational"
iso27001: "A.8.32"
nis2: "Art.21(3)"
bio2: "B8.2"
security_requirement:
  - "SR-10"
status: draft
created: 2026-01-29
modified: 2026-01-29
tags:
  - control
  - extended
  - ext-o
---

# EXT-O.32 - Wijzigingsbeheer

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-O.32 |
| **Categorie** | EXT-O4 - Operational Security |
| **Prioriteit** | 5 (Critical) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Organizational |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.8.32 |
| [[Frameworks/NIS2|NIS2]] | Art.21(3) |
| [[Frameworks/BIO2|BIO2]] | B8.2 |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-10|SR-10]]

## Beschrijving

Implementeer wijzigingsbeheer voor alle changes aan informatieverwerkende faciliteiten en systemen.

## Implementatie Richtlijnen

### Stappen

1. Definieer change procedure
2. Richt CAB in
3. Classificeer changes
4. Implementeer rollback
5. Monitor en rapporteer

### Best Practices

- ServiceNow Change Management
- Wekelijkse CAB
- Emergency change procedure
- CI/CD deployment

## Component Implementaties

```dataview
TABLE 
  component as "Component",
  system as "Systeem", 
  impl_status as "Status",
  next_review as "Review"
FROM "Implementations"
WHERE contains(string(control), this.id)
SORT system ASC
```

## Gerelateerde Risico's

```dataview
TABLE 
  risk_level as "Niveau",
  name as "Risico"
FROM "Risks"
WHERE contains(string(controls), this.id)
```

## Gerelateerde Controls

- Zie andere controls in categorie [[Controls/EXT-O|EXT-O]]
