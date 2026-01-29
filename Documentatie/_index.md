---
type: index
name: "Documentatie"
icon: "📚"
created: 2026-01-28
---

# 📚 Documentatie

> Handleidingen, procedures en referentiedocumenten — alles wat je moet weten.

---

## Navigatie

| ← Terug | Omhoog |
|---------|--------|
| [[README\|🏠 Home]] | — |

---

## Start Hier

Nieuw met het framework? Begin met deze documenten:

| Document | Beschrijving | Tijdsinvestering |
|----------|--------------|------------------|
| [[Documentatie/SCF Architectuur\|SCF Architectuur]] | Hoe het framework in elkaar zit | 15 min |
| [[Documentatie/Handleiding\|Handleiding]] | Dagelijks gebruik van de vault | 10 min |
| [[Frameworks/LISA/1-LISA-Introductie\|LISA Introductie]] | Het framework filosofie | 20 min |

---

## Procedures

### System Onboarding

Hoe neem je een nieuw systeem op in het framework?

→ [[Documentatie/System Onboarding Guide|System Onboarding Guide]]

Stappen:
1. System registratie en classificatie
2. System Component Breakdown (SCB)
3. Control mapping en gap analyse
4. Implementation planning
5. Documentatie en sign-off

---

### CIS Benchmark Mapping

Hoe gebruik je CIS Benchmarks en wanneer maak je een Extended Benchmark?

→ [[Documentatie/CIS Benchmark Mapping Guide|CIS Benchmark Mapping Guide]]

---

## System Component Breakdowns (SCB)

Gedetailleerde technische documentatie per systeem:

| System | Document | Status |
|--------|----------|--------|
| XENA | [[Documentatie/SCB/SCB-XENA\|SCB-XENA]] | ✅ Compleet |
| ZGW | SCB-ZGW | 📋 Gepland |

---

## Extended Benchmarks

Custom security benchmarks voor technologieën zonder officiële CIS Benchmark:

| Technologie | Document |
|-------------|----------|
| MinIO | [[Documentatie/Benchmarks/EXT-MinIO\|EXT-MinIO]] |
| Apache NiFi | 📋 Gepland |
| KeyCloak | 📋 Gepland |
| OpenBAO | 📋 Gepland |

---

## Framework Documentatie

Uitgebreide documentatie over het LISA framework zelf:

```dataview
TABLE WITHOUT ID
  link(file.link, file.name) as "Document"
FROM "Frameworks/LISA"
SORT file.name ASC
```

---

## Alle Documenten

```dataview
TABLE WITHOUT ID
  link(file.link, file.name) as "Document",
  type as "Type"
FROM "Documentatie"
WHERE file.name != "_index"
SORT file.name ASC
```

---

## Gerelateerde Secties

- [[Templates/_index|📝 Templates]] — Herbruikbare templates
- [[Planning/_index|📅 Planning]] — Roadmaps en kalenders
