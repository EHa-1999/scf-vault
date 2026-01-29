# SCF-Vault - Security Control Framework

Een Obsidian-gebaseerde knowledge base voor het beheren van security controls, compliance frameworks en implementaties volgens het **LISA** (Layered Information Security Architecture) model.

## Wat is LISA?

LISA is een gelaagd raamwerk voor informatiebeveiliging dat de kloof overbrugt tussen abstracte compliance-eisen en concrete technische implementaties. Net zoals GEMMA, NORA en PETRA referentiekaders bieden voor respectievelijk gemeenten, rijksoverheid en provincies, biedt LISA een referentiekader voor informatiebeveiliging.

→ [[Frameworks/LISA/1-LISA-Introductie|Lees de LISA documentatie]]

## De Zes Lagen

![[Assets/diagrams/LISA-Six-Layers.svg]]

---

## 🧭 Navigatie

Elke map heeft een **_index.md** pagina met overzicht en navigatie.

> [!tip] Interactieve Navigatie
> Open [[Vault-Navigation.canvas|🗺️ Vault Navigation Canvas]] voor een **klikbare kaart** van de vault!

![[Assets/diagrams/Vault-Navigation.svg]]

| Sectie | Beschrijving | Start hier |
|--------|--------------|------------|
| [[Frameworks/_index\|🏛️ Frameworks]] | Governance kaders (ISO, NIS2, BIO2) | [[Frameworks/LISA/1-LISA-Introductie\|LISA Intro]] |
| [[Controls/_index\|📋 Controls]] | 180 security controls | [[Controls/CIS/_index\|CIS Controls]] |
| [[Systems/_index\|🖥️ Systems]] | Applicaties onder scope | [[Systems/XENA\|XENA]] |
| [[Components/_index\|🔧 Components]] | Technische bouwstenen | [[Components/PostgreSQL\|PostgreSQL]] |
| [[Implementations/_index\|⚙️ Implementations]] | Control → Component | — |
| [[Dashboards/_index\|📊 Dashboards]] | Monitoring & KPI's | [[Dashboards/Main Dashboard\|Main Dashboard]] |
| [[Risks/_index\|⚠️ Risks]] | Risico register | — |
| [[Audits/_index\|🔍 Audits]] | Assurance & findings | — |
| [[Documentatie/_index\|📚 Documentatie]] | Handleidingen | [[Documentatie/System Onboarding Guide\|Onboarding]] |
| [[Templates/_index\|📝 Templates]] | Herbruikbare templates | — |
| [[Planning/_index\|📅 Planning]] | Roadmaps & kalenders | [[Planning/Implementatieplan 2026\|Plan 2026]] |

---

## Mappenstructuur

```
SCF-Vault/
├── Frameworks/                    # Governance frameworks
│   ├── LISA/                     # LISA framework documentatie
│   │   ├── 1-LISA-Introductie.md
│   │   ├── 2-LISA-Governance-Laag.md
│   │   ├── 3-LISA-Security-Requirements.md
│   │   ├── 4-LISA-Controls.md
│   │   ├── 5-LISA-Implementatie.md
│   │   ├── 6-LISA-Risicobeheer.md
│   │   └── 7-LISA-Audits.md
│   ├── Security-Requirements/    # SR-1 t/m SR-13
│   ├── NIST-CSF.md
│   ├── ISO-27001-2022.md
│   ├── NIS2.md
│   ├── BIO2.md
│   ├── AVG-GDPR.md
│   └── CIS-Controls-v8.md
├── Controls/                      # Tactische controls
│   ├── CIS/                      # 153 CIS Controls v8
│   └── EXT-P/                    # 27 Extended Privacy Controls
├── Systems/                       # Applicaties en platforms
├── Components/                    # Technische bouwstenen
├── Implementations/               # Control implementaties
├── Risks/                         # Risico register
├── Evidence/                      # Links naar bewijsmateriaal
├── Audits/                        # Audit documentatie
│   ├── {YYYY}/                   # Per jaar
│   │   └── IA-{ID}/              # Audit dossier
│   │       ├── _IA-{ID}.md       # Hoofdrapport
│   │       ├── Self-Assessments/ # Assessments in scope
│   │       ├── Bevindingen/      # Findings
│   │       └── Evidence/         # Lokale evidence
│   └── Scripts/                  # Templater scripts
├── Dashboards/                    # Overzichtspagina's
│   ├── Main Dashboard.md
│   ├── Executive Summary.md      # Management rapportage
│   ├── Compliance Dashboard.md   # Per-framework status
│   ├── Implementation Tracker.md
│   ├── Risk Dashboard.md
│   └── Audit Dashboard.md
├── Planning/                      # Roadmaps en kalenders
│   ├── Implementatieplan 2026.md # Gefaseerde uitrol
│   └── Compliance Kalender 2026.md
├── Scripts/                       # Export en automatisering
│   ├── export_to_jira.py         # Jira/Redmine CSV export
│   └── README.md
├── Documentatie/                  # Handleidingen en procedures
│   ├── System Onboarding Guide.md # Nieuwe systemen toevoegen
│   ├── CIS Benchmark Mapping Guide.md
│   ├── SCB/                      # System Component Breakdowns
│   │   ├── SCB-Template.md
│   │   └── SCB-XENA.md
│   └── Benchmarks/               # Extended Benchmarks
│       └── EXT-MinIO.md
├── Templates/                     # Templates voor nieuwe items
│   ├── System Template.md
│   ├── Component Template.md
│   ├── Implementation Template.md
│   ├── Risk Template.md
│   └── SCB Template.md
├── Assets/                        # SVG diagrammen
│   └── diagrams/
└── Documentatie/                  # Handleidingen
```

## Quick Start

1. Open deze vault in Obsidian
2. Installeer de Dataview plugin (Community Plugins → Browse → Dataview)
3. Start bij de [[Dashboards/Main Dashboard|Main Dashboard]]

## Inhoud

| Type | Aantal | Beschrijving |
|------|--------|--------------|
| Frameworks | 6 | NIST CSF, ISO 27001, NIS2, BIO2, AVG, CIS |
| Security Requirements | 13 | SR-1 t/m SR-13 |
| CIS Controls | 153 | CIS Controls v8 (93 baseline, 60 niet-baseline) |
| Privacy Controls (EXT-P) | 27 | Extended Privacy Controls (alle baseline) |
| Organizational (EXT-O) | 18 | ISO A.5 governance, beleid, classificatie |
| HR Security (EXT-HR) | 6 | ISO A.6 + BIO B3 personele beveiliging |
| Physical Security (EXT-PHY) | 12 | ISO A.7 + BIO B7 fysieke beveiliging |
| Supplier Mgmt (EXT-SUP) | 4 | BIO B11 + NIS2 supply chain security |
| Business Continuity (EXT-BC) | 4 | BIO B12 + NIS2 continuïteit |
| Compliance (EXT-COM) | 4 | BIO B13 wet- en regelgeving |
| Technical (EXT-T) | 3 | ISO A.8 resterende gaps |
| **Totaal Controls** | **231** | **168 baseline** |
| Systems | 3 | XENA, ZGW, E-mail Archief |
| Components | 8 | MinIO, PostgreSQL, KeyCloak, etc. |
| Dashboards | 7 | Main, Executive, Compliance, Impl, Risk, Audit, **Baseline** |
| Templates | 6 | Control, Implementation, Risk, System, Component, SCB |
| Templater Scripts | 3 | Nieuwe Audit, Self-Assessment, Bevinding |
| Export Scripts | 1 | Jira/Redmine CSV export |
| Planning Docs | 2 | Implementatieplan, Compliance Kalender |
| Onboarding Docs | 3 | Onboarding Guide, Benchmark Mapping, SCB-XENA |
| Extended Benchmarks | 1 | EXT-MinIO |
| SVG Diagrammen | 15 | ArchiMate-style LISA + XENA + Navigation |

## Baseline Security (Comply or Explain)

Het framework maakt onderscheid tussen **baseline** en **niet-baseline** controls:

- **Baseline controls** (`baseline: true`) zijn verplicht - "always on"
- Als een baseline control niet is geïmplementeerd, moet er een goedgekeurde **exception** zijn met compenserende maatregelen
- Zie [[Dashboards/Baseline Dashboard|Baseline Dashboard]] voor monitoring en exception management

| Type | Baseline | Niet-Baseline |
|------|----------|---------------|
| CIS Controls | 93 | 60 |
| Privacy Controls | 27 | 0 |
| **Totaal** | **120** | **60** |

## Belangrijke Links

- [[Frameworks/LISA/1-LISA-Introductie|LISA Introductie]] - Het framework begrijpen
- [[Dashboards/Main Dashboard|Main Dashboard]] - Centraal overzicht
- [[Dashboards/Baseline Dashboard|Baseline Dashboard]] - **Comply or Explain** monitoring
- [[Dashboards/Executive Summary|Executive Summary]] - Management rapportage
- [[Dashboards/Compliance Dashboard|Compliance Dashboard]] - Framework compliance
- [[Dashboards/Audit Dashboard|Audit Dashboard]] - Audits en bevindingen
- [[Planning/Implementatieplan 2026|Implementatieplan 2026]] - Roadmap
- [[Planning/Compliance Kalender 2026|Compliance Kalender]] - Deadlines
- [[Documentatie/System Onboarding Guide|System Onboarding Guide]] - Nieuwe systemen toevoegen
- [[Documentatie/CIS Benchmark Mapping Guide|CIS Benchmark Mapping]] - Benchmarks gebruiken
- [[Scripts/README|Export Scripts]] - Jira/Redmine export

## Versie

**SCF-Vault v3.1** - Extended Controls voor volledige ISO/NIS2/BIO compliance  
Laatste update: 2026-01-29

### Nieuwe Features v3.1

* **+51 Extended Controls** voor ISO 27001, NIS2 en BIO gaps
* **EXT-O**: 18 Organizational Controls (ISO A.5)
* **EXT-HR**: 6 HR Security Controls (ISO A.6, BIO B3)
* **EXT-PHY**: 12 Physical Security Controls (ISO A.7, BIO B7)
* **EXT-SUP**: 4 Supplier Management Controls (BIO B11, NIS2)
* **EXT-BC**: 4 Business Continuity Controls (BIO B12, NIS2)
* **EXT-COM**: 4 Compliance Controls (BIO B13)
* **EXT-T**: 3 Technical Controls (ISO A.8)
* Framework coverage: ISO 95%+, NIS2 100%, BIO 95%+

### Features v3.0
- **Index pagina's (_index.md)** voor elke map
- **Vault-Navigation.svg** interactief navigatiediagram
- Website-achtige navigatie door de hiërarchie
- Breadcrumb navigatie in elke index
- Dataview queries voor dynamische inhoud per sectie

### Features v2.9
- Baseline parameter op alle 180 controls (120 baseline)
- Baseline Dashboard voor comply-or-explain monitoring
- Exception Management workflow
