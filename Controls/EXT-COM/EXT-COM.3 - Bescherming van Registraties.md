---
id: "EXT-COM.3"
type: control
category: "EXT-COM"
category_name: "Compliance"
control_name: "Bescherming van Registraties"
priority: 5
priority_label: "Critical"
baseline: true
control_type: "Organizational"
iso27001: "A.5.33"
nis2: "-"
bio2: "B13.3"
security_requirement:
  - "SR-4"
status: draft
created: 2026-01-29
modified: 2026-01-29
tags:
  - control
  - extended
  - ext-com
---

# EXT-COM.3 - Bescherming van Registraties

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-COM.3 |
| **Categorie** | EXT-COM - Compliance |
| **Prioriteit** | 5 (Critical) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Organizational |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.5.33 |
| [[Frameworks/NIS2|NIS2]] | - |
| [[Frameworks/BIO2|BIO2]] | B13.3 |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-4|SR-4]]

## Beschrijving

Bescherm records conform wettelijke vereisten (Archiefwet).

## Implementatie Richtlijnen

### Stappen

1. Stel archiefbeleid op
2. Pas selectielijst toe
3. Definieer bewaartermijnen
4. Implementeer vernietigingsprocedure
5. Audit trail

### Best Practices

- XENA DMS voor archiefbeheer
- Selectielijst gemeenten
- Automatische vernietigingsvoorstellen
- Volledige audit trail

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
