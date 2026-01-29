---
id: "EXT-COM.2"
type: control
category: "EXT-COM"
category_name: "Compliance"
control_name: "Intellectuele Eigendomsrechten"
priority: 4
priority_label: "High"
baseline: true
control_type: "Organizational"
iso27001: "A.5.32"
nis2: "-"
bio2: "B13.2"
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

# EXT-COM.2 - Intellectuele Eigendomsrechten

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-COM.2 |
| **Categorie** | EXT-COM - Compliance |
| **Prioriteit** | 4 (High) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Organizational |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.5.32 |
| [[Frameworks/NIS2|NIS2]] | - |
| [[Frameworks/BIO2|BIO2]] | B13.2 |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-9|SR-9]]

## Beschrijving

Zorg voor naleving van intellectuele eigendomsrechten en softwarelicenties.

## Implementatie Richtlijnen

### Stappen

1. Implementeer SAM proces
2. Onderhoud licentieregister
3. Voer jaarlijkse audit uit
4. Gebruik alleen goedgekeurde software
5. Registreer in CMDB

### Best Practices

- SAM tool voor inventarisatie
- Jaarlijkse licentie audit
- Goedgekeurde software lijst
- CMDB registratie

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
