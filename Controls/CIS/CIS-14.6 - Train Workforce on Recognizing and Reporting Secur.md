---
id: "CIS-14.6"
type: control
category: "CIS 14"
category_name: "Security Awareness and Skills Training"
control_name: "Train Workforce on Recognizing and Reporting Security Incidents"
priority: 4
priority_label: "High"
baseline: true
control_type: "Foundational"
iso27001: "A.6.8"
nis2: "Art.21(2)(h)"
bio2: "5.25"
core_requirement: "SR-8: Incident Response"
security_requirement:
  - "SR-1"
status: draft
created: 2026-01-27
modified: 2026-01-27
tags:
  - control
  - cis-14
  - priority-4
---

# CIS-14.6 - Train Workforce on Recognizing and Reporting Security Incidents

## Overzicht

| Eigenschap | Waarde |
|------------|--------|
| **Categorie** | Security Awareness and Skills Training |
| **Prioriteit** | 4 - High |
| **Type** | Foundational |
| **Extended Baseline** | Ja |

## Framework Mappings

| Framework | Referentie |
|-----------|------------|
| [[Frameworks/ISO-27001-2022|ISO 27001:2022]] | A.6.8 |
| [[Frameworks/NIS2|NIS2]] | Art.21(2)(h) |
| [[Frameworks/BIO2|BIO2]] | 5.25 |
| **Core Requirement** | SR-8: Incident Response |


## Security Requirements

Dit control valt onder de volgende Security Requirements:

- [[Frameworks/Security-Requirements/SR-1 - Security Governance Framework|SR-1 - Security Governance Framework]]

## Beschrijving

Train workforce members on recognizing and reporting security incidents.

## Doel

Deze control draagt bij aan het mitigeren van risico's gerelateerd aan security awareness and skills training.

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
