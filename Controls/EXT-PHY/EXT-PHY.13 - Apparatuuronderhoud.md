---
id: "EXT-PHY.13"
type: control
category: "EXT-PHY4"
category_name: "Infrastructure"
control_name: "Apparatuuronderhoud"
priority: 4
priority_label: "High"
baseline: true
control_type: "Physical"
iso27001: "A.7.13"
nis2: "-"
bio2: "-"
security_requirement:
  - "SR-11"
status: draft
created: 2026-01-29
modified: 2026-01-29
tags:
  - control
  - extended
  - ext-phy
---

# EXT-PHY.13 - Apparatuuronderhoud

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-PHY.13 |
| **Categorie** | EXT-PHY4 - Infrastructure |
| **Prioriteit** | 4 (High) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Physical |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.7.13 |
| [[Frameworks/NIS2|NIS2]] | - |
| [[Frameworks/BIO2|BIO2]] | - |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-11|SR-11]]

## Beschrijving

Onderhoud apparatuur correct met beveiligingstoezicht.

## Implementatie Richtlijnen

### Stappen

1. Sluit onderhoudscontracten
2. Definieer onderhoudsschema
3. Begeleid externe technici
4. Registreer onderhoud
5. Verifieer werkzaamheden

### Best Practices

- Preventief onderhoud
- Onderhoudsvensters
- Begeleiding externen
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

- Zie andere controls in categorie [[Controls/EXT-PHY|EXT-PHY]]
