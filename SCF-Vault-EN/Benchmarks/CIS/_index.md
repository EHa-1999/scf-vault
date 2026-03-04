---
type: index
name: "CIS Benchmarks"
icon: "📘"
created: 2026-01-30
modified: 2026-01-30
---

# 📘 CIS Benchmarks

> Official hardening guides from the Center for Internet Security.

---

## Navigation

| ← Back | Up | Related |
|--------|-----|---------|
| [[Benchmarks/_index\|📏 Benchmarks]] | [[README\|🏠 Home]] | [[Benchmarks/EXT/_index\|📙 Extended]] |

---

## About CIS Benchmarks

CIS Benchmarks are consensus-based best practice configuration guides, developed by security experts worldwide. They provide:

- **Specific configuration settings** per technology
- **Audit procedures** — how to verify
- **Remediation steps** — how to implement
- **CIS Controls mapping** — which control is addressed

### Download

- **CIS Website:** https://www.cisecurity.org/cis-benchmarks
- **CIS WorkBench:** https://workbench.cisecurity.org/ (free account)

---

## Available CIS Benchmarks

```dataview
TABLE WITHOUT ID
  link(file.link, name) as "Benchmark",
  technology as "Technology",
  technology_version as "Tech Version",
  benchmark_version as "Benchmark Version",
  cis_release_date as "Release",
  recommendations_count as "# Recs"
FROM "Benchmarks/CIS"
WHERE type = "benchmark"
SORT technology ASC
```

---

## By Category

### Databases

| Benchmark | Component | Status |
|-----------|-----------|--------|
| [[Benchmarks/CIS/CIS-PostgreSQL-16-v1.0.0\|CIS PostgreSQL 16]] | [[Components/PostgreSQL]] | ✅ Active |
| CIS MySQL 8.0 | — | 📋 Planned |
| CIS MongoDB 7.0 | — | 📋 Planned |

### Web Servers

| Benchmark | Component | Status |
|-----------|-----------|--------|
| [[Benchmarks/CIS/CIS-NGINX-v2.1.0\|CIS NGINX]] | [[Components/NGINX]] | ✅ Active |
| CIS Apache HTTP 2.4 | — | 📋 Planned |

### Containers & Orchestration

| Benchmark | Component | Status |
|-----------|-----------|--------|
| CIS Docker | — | 📋 Planned |
| CIS Kubernetes 1.29 | — | 📋 Planned |

### Operating Systems

| Benchmark | Component | Status |
|-----------|-----------|--------|
| CIS Ubuntu 24.04 LTS | — | 📋 Planned |
| CIS RHEL 9 | — | 📋 Planned |

---

## Benchmark Conversion Process

### From PDF to Obsidian

```
1. Download PDF from CIS WorkBench
       ↓
2. Identify sections with recommendations
       ↓
3. Convert to Markdown using template
       ↓
4. Add audit/remediation code blocks
       ↓
5. Fill in CIS Control mappings
       ↓
6. Link to Component document
```

### What to Convert

Not everything from the PDF is needed. Focus on:

| Section | Convert? | Reason |
|---------|----------|--------|
| Overview | ✅ Yes | Context and scope |
| Recommendations | ✅ Yes | Core of the benchmark |
| Audit Procedures | ✅ Yes | Verification |
| Remediation | ✅ Yes | Implementation |
| CIS Controls Mapping | ✅ Yes | Traceability |
| Appendix - Glossary | ❌ No | Reference in PDF |
| Appendix - Change Log | ⚠️ Summarize | Highlights only |

---

## Version Management

### When to Update?

| Situation | Action |
|----------|-------|
| CIS publishes new version | Create new benchmark MD |
| Technology major upgrade | Check if current benchmark applies |
| CVE related to config | Check if benchmark recommendation exists |

### Multiple Versions

It's normal to have multiple versions:

```
Benchmarks/CIS/
├── CIS-PostgreSQL-15-v1.0.0.md  ← For legacy PostgreSQL 15
├── CIS-PostgreSQL-16-v1.0.0.md  ← For current PostgreSQL 16
└── CIS-PostgreSQL-17-v1.0.0.md  ← For upgrade to 17
```

---

## Template

→ [[Benchmarks/Templates/CIS Benchmark Template|CIS Benchmark Template]]

---

## Related

- [[Benchmarks/EXT/_index|📙 Extended Benchmarks]] — Self-developed benchmarks
- [[Documentatie/CIS Benchmark Mapping Guide|📚 Benchmark Mapping Guide]] — Practical usage
