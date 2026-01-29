---
id: "CIS-4.3"
type: control
category: "CIS 4"
category_name: "Secure Configuration of Enterprise Assets and Software"
control_name: "Configure Automatic Session Locking"
priority: 3
priority_label: "Medium"
baseline: false
control_type: "Foundational"
iso27001: "A.8.5"
nis2: "Art.21(2)(i)"
bio2: "5.35"
core_requirement: "SR-3: Access Control & IAM"
security_requirement:
  - "SR-11"
status: draft
created: 2026-01-27
modified: 2026-01-27
tags:
  - control
  - cis-4
  - priority-3
---

# CIS-4.3 - Configure Automatic Session Locking

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **Categorie** | Secure Configuration of Enterprise Assets and Software |
| **Prioriteit** | 3 - Medium |
| **Type** | Foundational |
| **Extended Baseline** | Nee |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.8.5 |
| [[Frameworks/NIS2|NIS2]] | Art.21(2)(i) |
| [[Frameworks/BIO2|BIO2]] | 5.35 |
| **Core Requirement** | SR-3: Access Control & IAM |


## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-11 - Physical & Environmental Security|SR-11 - Physical & Environmental Security]]

## Beschrijving

Configure automatic session locking on enterprise assets.

## Doel

Deze control draagt bij aan het mitigeren van risico's gerelateerd aan secure configuration of enterprise assets and software.

## Implementatie Richtlijnen

Algemene richtlijnen voor implementatie van deze control:

1. Inventariseer welke componenten binnen scope vallen
2. Bepaal de specifieke implementatie per component
3. Definieer Definition of Done criteria
4. Verzamel vereist bewijsmateriaal
5. Plan periodieke reviews

## Gerelateerde Controls

<!-- Links naar gerelateerde controls -->

## Component Implementaties

```dataview
TABLE 
  component as "Component",
  system as "Systeem", 
  impl_status as "Status",
  next_review as "Review"
FROM "Implementations"
WHERE contains(control, this.file.name)
SORT system ASC
```

## Risico's bij Ontbreken

```dataview
TABLE 
  risk_level as "Niveau",
  status as "Status"
FROM "Risks"
WHERE contains(controls, this.file.link)
SORT risk_level DESC
```

## Wijzigingshistorie

| Datum | Wijziging | Door |
|-------|-----------|------|
| 2026-01-27 | Initiële versie | @architect |
