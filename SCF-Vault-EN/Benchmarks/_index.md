---
type: index
name: "Benchmarks"
icon: "📏"
created: 2026-01-30
modified: 2026-01-30
---

# 📏 Benchmarks

> Hardening guides that bridge the gap between abstract controls and concrete configurations.

---

## Navigation

| ← Back | Up | Related |
|--------|-----|---------|
| [[README\|🏠 Home]] | — | [[Controls/_index\|📋 Controls]] |

---

## What is a Benchmark?

A **Benchmark** is a detailed hardening guide for a specific technology. It translates abstract security controls into concrete configuration settings.

```
CIS Control                    Benchmark                      Component
(WHAT to do)                   (HOW to do it)                 (WHERE)
────────────                   ──────────────                 ────────
CIS-3.11: Encrypt       ───▶   PostgreSQL Benchmark 4.2  ───▶  PostgreSQL
data at rest                   "Ensure TDE is enabled"        on XENA
```

### Benchmark Types

| Type | Source | Authority | Example |
|------|--------|-----------|---------|
| **CIS Benchmark** | [CIS Downloads](https://www.cisecurity.org/cis-benchmarks) | Industry standard | CIS PostgreSQL 16 Benchmark |
| **EXT Benchmark** | Self-developed | Organization standard | EXT-MinIO, EXT-KeyCloak |

---

## CIS Benchmarks

Official benchmarks from the Center for Internet Security, converted to Obsidian format.

→ [[Benchmarks/CIS/_index\|📘 CIS Benchmarks]]

```dataview
TABLE WITHOUT ID
  link(file.link, name) as "Benchmark",
  technology as "Technology",
  benchmark_version as "Version",
  cis_release_date as "Release Date"
FROM "Benchmarks/CIS"
WHERE type = "benchmark"
SORT technology ASC
```

### Available CIS Benchmarks by Category

| Category | Technologies |
|----------|--------------|
| **Databases** | PostgreSQL, MySQL, MariaDB, MongoDB, Oracle, SQL Server, Redis |
| **Operating Systems** | Ubuntu, Debian, RHEL, CentOS, Windows Server, macOS |
| **Containers** | Docker, Kubernetes, OpenShift |
| **Web Servers** | Apache HTTP, NGINX, IIS |
| **Cloud** | AWS, Azure, GCP (per service) |

> **Download:** https://www.cisecurity.org/cis-benchmarks (free account required)

---

## Extended Benchmarks (EXT)

Self-developed benchmarks for technologies without an official CIS Benchmark.

→ [[Benchmarks/EXT/_index\|📙 Extended Benchmarks]]

```dataview
TABLE WITHOUT ID
  link(file.link, name) as "Benchmark",
  technology as "Technology",
  benchmark_version as "Version",
  last_review as "Last Review"
FROM "Benchmarks/EXT"
WHERE type = "benchmark"
SORT technology ASC
```

### When to Create an EXT Benchmark?

Develop an Extended Benchmark when:
- No CIS Benchmark is available
- The technology is organization-specific
- Additional requirements apply beyond CIS

---

## Benchmark → Component Mapping

Which benchmark applies to which component?

```dataview
TABLE WITHOUT ID
  link(file.link, file.name) as "Component",
  benchmark as "Benchmark",
  benchmark_version as "Version"
FROM "Components"
WHERE benchmark != null
SORT file.name ASC
```

---

## Versioning

Benchmarks follow semantic versioning and are updated when:

| Trigger | Action |
|---------|--------|
| **CIS release** | Import new CIS Benchmark version |
| **Technology upgrade** | Verify if benchmark still applies |
| **Annual review** | Evaluate EXT Benchmarks |
| **Incident/CVE** | Supplement benchmark if needed |

### Version Conventions

| Type | Format | Example |
|------|--------|---------|
| CIS Benchmark | `CIS-{Tech}-{TechVer}-v{BenchVer}` | `CIS-PostgreSQL-16-v1.0.0` |
| EXT Benchmark | `EXT-{Tech}-v{Ver}` | `EXT-MinIO-v1.0` |

---

## Adding a New Benchmark

### Importing a CIS Benchmark

1. Download PDF from [CIS WorkBench](https://workbench.cisecurity.org/)
2. Copy [[Benchmarks/Templates/CIS Benchmark Template\|CIS Benchmark Template]]
3. Convert recommendations to Markdown
4. Fill in CIS Control mappings
5. Link to Component(s)

### Developing an EXT Benchmark

1. Copy [[Benchmarks/Templates/EXT Benchmark Template\|EXT Benchmark Template]]
2. Gather sources (vendor docs, OWASP, STIGs)
3. Define recommendations with audit/remediation
4. Map to CIS Controls
5. Review by Security Officer

---

## Templates

| Template | Use |
|----------|-----|
| [[Benchmarks/Templates/CIS Benchmark Template\|CIS Benchmark Template]] | For converted CIS Benchmarks |
| [[Benchmarks/Templates/EXT Benchmark Template\|EXT Benchmark Template]] | For self-developed benchmarks |

---

## Statistics

```dataview
TABLE WITHOUT ID
  "CIS Benchmarks" as "Type",
  length(filter(rows, (r) => r.benchmark_type = "CIS")) as "Count"
FROM "Benchmarks"
WHERE type = "benchmark"
GROUP BY true
```

---

## Related Sections

- [[Controls/_index\|📋 Controls]] — The controls that benchmarks implement
- [[Components/_index\|🔧 Components]] — The technologies benchmarks apply to
- [[Implementations/_index\|⚙️ Implementations]] — Control implementations per component
- [[Documentatie/CIS Benchmark Mapping Guide\|📚 CIS Benchmark Mapping Guide]] — How to use benchmarks
