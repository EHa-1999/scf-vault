---
id: "CIS-12.8"
type: control
category: "CIS 12"
category_name: "Network Infrastructure Management"
control_name: "Establish and Maintain Dedicated Computing Resources"
priority: 2
priority_label: "Low"
baseline: false
control_type: "Organizational"
iso27001: "A.8.31"
nis2: "Art.21(2)(b)"
bio2: "8.1"
core_requirement: "SR-7: Network Security"
security_requirement:
  - "SR-7"
status: draft
created: 2026-01-27
modified: 2026-01-27
tags:
  - control
  - cis-12
  - priority-2
---

# CIS-12.8 - Establish and Maintain Dedicated Computing Resources

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **Categorie** | Network Infrastructure Management |
| **Prioriteit** | 2 - Low |
| **Type** | Organizational |
| **Extended Baseline** | Nee |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.8.31 |
| [[Frameworks/NIS2|NIS2]] | Art.21(2)(b) |
| [[Frameworks/BIO2|BIO2]] | 8.1 |
| **Core Requirement** | SR-7: Network Security |


## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-7 - Network Security & Segmentation|SR-7 - Network Security & Segmentation]]

## Beschrijving

Establish and maintain dedicated computing resources for all administrative work.

## Doel

Deze control draagt bij aan het mitigeren van risico's gerelateerd aan network infrastructure management.

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
