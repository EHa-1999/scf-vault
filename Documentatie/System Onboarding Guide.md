---
id: "DOC-Onboarding"
type: documentation
name: "System Onboarding Guide"
created: 2026-01-28
modified: 2026-01-28
tags:
  - documentation
  - onboarding
  - process
---

# System Onboarding Guide

## Overzicht

Deze handleiding beschrijft het proces om een nieuw systeem op te nemen in het LISA Security Control Framework. Het doel is om systematisch te bepalen welke security controls van toepassing zijn en hoe deze moeten worden geïmplementeerd.

## Onboarding Proces

![[Assets/diagrams/LISA-Onboarding-Process.svg]]

---

## Fase 1: Inventarisatie

### Stap 1.1: System Registratie

Maak een nieuw System document aan via het template:

1. Kopieer [[Templates/System Template|System Template]]
2. Vul de basis informatie in:
   - System ID en naam
   - Eigenaar (system owner)
   - Primaire functie
   - Gebruikersgroepen

### Stap 1.2: System Component Breakdown (SCB)

Voer een SCB-analyse uit om alle componenten te identificeren:

```
Systeem
├── Applicatie Laag
│   ├── Frontend (web UI, mobile app)
│   ├── Backend (API, services)
│   └── Business Logic
│
├── Data Laag
│   ├── Database(s)
│   ├── Object Storage
│   ├── Cache
│   └── Message Queue
│
├── Integratie Laag
│   ├── API Gateways
│   ├── ESB/Orchestratie
│   └── Externe koppelingen
│
├── Security Laag
│   ├── IAM/SSO
│   ├── Secret Management
│   └── WAF/Firewall
│
└── Infrastructuur Laag
    ├── Compute (VMs, containers)
    ├── Netwerk
    └── Storage
```

Documenteer elk component met:

| Aspect | Te documenteren |
|--------|-----------------|
| **Naam** | Unieke identifier |
| **Type** | Database, Storage, IAM, etc. |
| **Technologie** | PostgreSQL, MinIO, KeyCloak, etc. |
| **Versie** | Huidige productie versie |
| **Vendor** | Leverancier/community |
| **Hosting** | On-prem, cloud, SaaS |
| **Eigenaar** | Verantwoordelijk team |

→ Gebruik [[Templates/SCB Template|SCB Template]] voor gedetailleerde analyse

### Stap 1.3: BIV Classificatie

Bepaal per systeem de Beschikbaarheid, Integriteit en Vertrouwelijkheid classificatie:

| Niveau | Beschikbaarheid | Integriteit | Vertrouwelijkheid |
|--------|-----------------|-------------|-------------------|
| **Laag (I)** | Uitval < 1 week acceptabel | Fouten hebben beperkte impact | Openbare informatie |
| **Midden (II)** | Uitval < 1 dag acceptabel | Fouten hebben operationele impact | Interne informatie |
| **Hoog (III)** | Uitval < 4 uur acceptabel | Fouten hebben ernstige impact | Vertrouwelijke/persoons gegevens |

De BIV classificatie bepaalt:
- Welke Implementation Group (IG) minimaal vereist is
- De frequentie van assessments
- De diepgang van controls

| BIV | Minimale IG | Assessment Frequentie |
|-----|-------------|----------------------|
| I-I-I | IG1 | Jaarlijks |
| II-II-II | IG2 | Halfjaarlijks |
| III-III-III | IG3 | Per kwartaal |

---

## Fase 2: Control Mapping

### Stap 2.1: CIS Benchmark Check

Controleer of er een CIS Benchmark beschikbaar is voor de technologie:

**Beschikbare CIS Benchmarks (selectie):**

| Categorie | Benchmarks |
|-----------|------------|
| **Databases** | PostgreSQL, MySQL, MariaDB, MongoDB, Oracle, SQL Server |
| **Operating Systems** | Ubuntu, RHEL, Windows Server, CentOS |
| **Cloud** | AWS, Azure, GCP, Kubernetes |
| **Webservers** | Apache, NGINX, IIS |
| **Containers** | Docker, Kubernetes |
| **Applications** | Apache Tomcat, JBoss |

→ Download benchmarks van: https://www.cisecurity.org/cis-benchmarks

### Stap 2.2: Control Selectie Matrix

Voor elk component, bepaal welke CIS Controls van toepassing zijn:

| CIS Categorie | Van toepassing op |
|---------------|-------------------|
| **1. Asset Inventory** | Alle componenten |
| **2. Software Inventory** | Alle componenten |
| **3. Data Protection** | Componenten met data opslag/verwerking |
| **4. Secure Configuration** | Alle componenten |
| **5. Account Management** | Componenten met user accounts |
| **6. Access Control** | Componenten met authenticatie/autorisatie |
| **7. Vulnerability Mgmt** | Alle componenten met software |
| **8. Audit Logging** | Componenten met security-relevante events |
| **9. Email/Browser** | Email servers, webapplicaties |
| **10. Malware Defense** | Endpoints, servers |
| **11. Data Recovery** | Componenten met persistente data |
| **12. Network Infrastructure** | Netwerk componenten |
| **13. Network Monitoring** | Alle netwerkverbonden componenten |
| **14. Security Awareness** | N.v.t. (organisatie-breed) |
| **15. Service Provider Mgmt** | SaaS/externe componenten |
| **16. Application Security** | Custom applicaties |
| **17. Incident Response** | N.v.t. (organisatie-breed) |
| **18. Penetration Testing** | Alle externe interfaces |

### Stap 2.3: Component-Control Matrix

Maak een matrix per systeem:

| Component | CIS 3 | CIS 4 | CIS 5 | CIS 6 | CIS 8 | CIS 11 | ... |
|-----------|-------|-------|-------|-------|-------|--------|-----|
| PostgreSQL | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | |
| MinIO | ✓ | ✓ | | | ✓ | ✓ | |
| KeyCloak | | ✓ | ✓ | ✓ | ✓ | | |
| NiFi | | ✓ | | | ✓ | | |

### Stap 2.4: Extended Controls (indien geen benchmark)

Als er geen CIS Benchmark beschikbaar is:

1. **Gebruik generieke benchmark** als basis (bijv. CIS Controls zelf)
2. **Analyseer vendor documentatie** voor security best practices
3. **Definieer custom controls** gebaseerd op:
   - Vendor security hardening guides
   - OWASP guidelines (voor applicaties)
   - NIST 800-53 mappings
   - Eigen risk assessment

Documenteer extended controls in een nieuw bestand onder `Controls/EXT-{System}/`

---

## Fase 3: Implementation Planning

### Stap 3.1: Implementation Documents

Voor elke combinatie van Control + Component, maak een Implementation document:

**Naamconventie:** `IMPL-{System}-{Component}-{Control}.md`

Voorbeeld: `IMPL-XENA-PostgreSQL-3.11.md`

Gebruik [[Templates/Implementation Template|Implementation Template]] met:

| Veld | Beschrijving |
|------|--------------|
| `control` | Link naar Control document |
| `component` | Link naar Component document |
| `system` | Link naar System document |
| `impl_status` | Not Started / Planned / In Progress / Implemented / Verified |
| `definition_of_done` | Specifieke criteria voor dit component |
| `evidence` | Vereist bewijsmateriaal |

### Stap 3.2: Definition of Done (DoD)

Definieer concrete, meetbare criteria per implementation:

**Voorbeeld: CIS-3.11 (Encrypt Data at Rest) op PostgreSQL:**

```markdown
## Definition of Done

- [ ] TDE (Transparent Data Encryption) is ingeschakeld
- [ ] Encryptiesleutels worden beheerd in OpenBAO
- [ ] Key rotation is geconfigureerd (90 dagen)
- [ ] Backup bestanden zijn ook versleuteld
- [ ] Configuratie is gedocumenteerd
```

**Bronnen voor DoD:**
- CIS Benchmark (specifieke checks)
- Vendor hardening guide
- Interne security policies

### Stap 3.3: Prioritering

Prioriteer implementations op basis van:

| Factor | Gewicht | Criteria |
|--------|---------|----------|
| **BIV Impact** | 40% | Hoge BIV = hogere prioriteit |
| **Implementation Group** | 30% | IG1 > IG2 > IG3 |
| **Risk Level** | 20% | Gekoppelde risico's |
| **Effort** | 10% | Quick wins eerst |

---

## Fase 4: Registratie

### Stap 4.1: Documenten Aanmaken

Maak de volgende documenten in volgorde:

```
1. Systems/{System}.md           ← Eerst het systeem
2. Components/{Component}.md     ← Dan elk component  
3. Implementations/IMPL-*.md     ← Dan de implementations
4. Risks/RSK-*.md               ← Tot slot de risico's
```

### Stap 4.2: CMDB Integratie

Het SCF is geen vervanging voor een CMDB, maar complementeert deze:

| CMDB | SCF |
|------|-----|
| Technische configuratie | Security configuratie |
| Alle assets | Security-relevante assets |
| Operationele status | Compliance status |
| Change management | Implementation tracking |

**Aanbevolen koppeling:**
- CMDB CI-ID opnemen in Component frontmatter
- Link naar CMDB in Component document
- Sync via export script (optioneel)

### Stap 4.3: Review & Goedkeuring

Voordat het systeem "live" gaat in het SCF:

| Stap | Reviewer | Check |
|------|----------|-------|
| 1 | System Owner | Systeem en componenten correct |
| 2 | Security Officer | Controls mapping compleet |
| 3 | CISO | Risico assessment akkoord |

---

## Checklist Nieuwe Systemen

```markdown
## Onboarding Checklist: {Systeem Naam}

### Fase 1: Inventarisatie
- [ ] System document aangemaakt
- [ ] SCB analyse uitgevoerd
- [ ] Alle componenten geïdentificeerd
- [ ] Component documenten aangemaakt
- [ ] BIV classificatie bepaald

### Fase 2: Control Mapping
- [ ] CIS Benchmarks geïdentificeerd
- [ ] Control selectie matrix ingevuld
- [ ] Extended controls gedefinieerd (indien nodig)
- [ ] Component-Control matrix compleet

### Fase 3: Implementation Planning
- [ ] Implementation documenten aangemaakt
- [ ] DoD gedefinieerd per implementation
- [ ] Prioritering bepaald
- [ ] Planning opgenomen in roadmap

### Fase 4: Registratie
- [ ] Alle documenten in SCF-Vault
- [ ] CMDB links toegevoegd
- [ ] Review door System Owner
- [ ] Review door Security Officer
- [ ] Goedkeuring CISO

### Sign-off
| Rol | Naam | Datum |
|-----|------|-------|
| System Owner | | |
| Security Officer | | |
| CISO | | |
```

---

## Gerelateerde Documenten

- [[Templates/System Template|System Template]]
- [[Templates/Component Template|Component Template]]
- [[Templates/Implementation Template|Implementation Template]]
- [[Templates/SCB Template|SCB Template]]
- [[Documentatie/CIS Benchmark Mapping|CIS Benchmark Mapping Guide]]
- [[Frameworks/LISA/5-LISA-Implementatie|LISA Implementatie Laag]]
