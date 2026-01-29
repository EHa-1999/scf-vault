---
id: "EXT-BC.2"
type: control
category: "EXT-BC"
category_name: "Business Continuity"
control_name: "Continuïteit Implementatie"
priority: 5
priority_label: "Critical"
baseline: true
control_type: "Technical"
iso27001: "A.8.14"
nis2: "Art.21(2)(c)"
bio2: "B12.2"
security_requirement:
  - "SR-9"
status: draft
created: 2026-01-29
modified: 2026-01-29
tags:
  - control
  - extended
  - ext-bc
---

# EXT-BC.2 - Continuïteit Implementatie

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **ID** | EXT-BC.2 |
| **Categorie** | EXT-BC - Business Continuity |
| **Prioriteit** | 5 (Critical) |
| **Baseline** | Ja - Comply or Explain |
| **Type** | Technical |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.8.14 |
| [[Frameworks/NIS2|NIS2]] | Art.21(2)(c) |
| [[Frameworks/BIO2|BIO2]] | B12.2 |

## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-9|SR-9]]

## Beschrijving

Implementeer redundantie en herstelmogelijkheden voor informatieverwerkende faciliteiten.

## Implementatie Richtlijnen

### Stappen

1. Ontwerp redundantie architectuur
2. Implementeer failover
3. Richt DR site in
4. Test failover
5. Documenteer procedures

### Best Practices

- Database replicatie
- Active-active clustering
- DR site 50+ km
- Automatische failover tier 1

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

- Zie andere controls in categorie [[Controls/EXT-BC|EXT-BC]]
