---
id: "EXT-COM.4"
type: control
category: "EXT-COM"
category_name: "Compliance"
control_name: "Compliance Verificatie"
priority: 5
priority_label: "Critical"
baseline: true
control_type: "Organizational"
iso27001: "A.5.36"
nis2: "-"
bio2: "B13.3"
security_requirement:
  - "SR-9"
status: draft
created: 2026-01-29
modified: 2026-01-29
tags:
  - control
  - extended
  - ext-com
---

# EXT-COM.4 - Compliance Verificatie

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-COM.4 |
| **Categorie** | EXT-COM - Compliance |
| **Prioriteit** | 5 (Critical) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Organizational |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.5.36 |
| [[Frameworks/NIS2|NIS2]] | - |
| [[Frameworks/BIO2|BIO2]] | B13.3 |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-9|SR-9]]

## Beschrijving

Verifieer periodiek de naleving van alle security policies en standaarden.

## Implementatie Richtlijnen

### Stappen

1. Definieer verificatie framework
2. Plan audits
3. Registreer bevindingen
4. Stel verbeterplannen op
5. Volg verbeteringen

### Best Practices

- Maandelijkse checks
- Kwartaalse interne audits
- Jaarlijkse externe audit
- Verbeterregister

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

- Zie andere controls in categorie [[Controls/EXT-COM|EXT-COM]]
