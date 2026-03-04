---
id: "CIS-{{Technology}}-{{TechVersion}}-v{{BenchmarkVersion}}"
type: benchmark
benchmark_type: "CIS"
name: "CIS {{Technology}} {{TechVersion}} Benchmark"
technology: "{{Technology}}"
technology_version: "{{TechVersion}}"
benchmark_version: "{{BenchmarkVersion}}"
cis_release_date: {{ReleaseDate}}
cis_download_url: "https://workbench.cisecurity.org/"
applies_to:
  - "[[Components/{{Component}}]]"
status: Active
recommendations_count: 0
created: {{date}}
modified: {{date}}
tags:
  - benchmark
  - cis
  - {{technology_tag}}
---

# CIS {{Technology}} {{TechVersion}} Benchmark v{{BenchmarkVersion}}

## Benchmark Information

| Field | Value |
|-------|-------|
| **Technology** | {{Technology}} {{TechVersion}} |
| **Benchmark Version** | v{{BenchmarkVersion}} |
| **CIS Release Date** | {{ReleaseDate}} |
| **Status** | Active |
| **Download** | [CIS WorkBench](https://workbench.cisecurity.org/) |

## Navigation

| ← Back | Up | Component |
|--------|-----|-----------|
| [[Benchmarks/CIS/_index\|📘 CIS Benchmarks]] | [[Benchmarks/_index\|📏 Benchmarks]] | [[Components/{{Component}}]] |

---

## Scope

### Applies To

- {{Technology}} version {{TechVersion}}.x
- Both standalone and clustered deployments
- On-premise and cloud deployments

### Does Not Apply To

- Versions older than {{TechVersion}}
- Managed/SaaS variants (see cloud-specific benchmarks)

---

## Profile Definitions

CIS Benchmarks define two profiles:

| Profile | Description | Our Choice |
|---------|-------------|------------|
| **Level 1** | Basic security, minimal impact on functionality | ✅ Required |
| **Level 2** | Extended security, possible impact on functionality | ⚠️ Where possible |

---

## Recommendations Overview

| Section | Topic | # Recs | Level 1 | Level 2 |
|---------|-------|--------|---------|---------|
| 1 | Installation and Patches | | | |
| 2 | Directory and File Permissions | | | |
| 3 | Logging and Auditing | | | |
| 4 | Encryption | | | |
| 5 | Authentication | | | |
| 6 | Authorization | | | |
| 7 | Network | | | |
| **Total** | | | | |

---

## 1. Installation and Patches

### 1.1 Ensure latest security patches are installed

| Property | Value |
|----------|-------|
| **Level** | 1 |
| **CIS Control** | [[Controls/CIS/CIS-7.3\|CIS-7.3]], [[Controls/CIS/CIS-7.4\|CIS-7.4]] |

**Description:**
Ensure the latest security patches are installed for {{Technology}}.

**Rationale:**
Unpatched software contains known vulnerabilities that can be exploited.

**Audit:**
```bash
# Check the current version
{{audit_command}}

# Compare with latest release
# See: {{vendor_release_url}}
```

**Remediation:**
```bash
# Update to latest version
{{remediation_command}}
```

**References:**
- {{vendor_patch_url}}

---

### 1.2 {{Next recommendation title}}

| Property | Value |
|----------|-------|
| **Level** | 1 |
| **CIS Control** | [[Controls/CIS/CIS-x.y\|CIS-x.y]] |

**Description:**
{{description}}

**Rationale:**
{{rationale}}

**Audit:**
```bash
{{audit_command}}
```

**Remediation:**
```bash
{{remediation_command}}
```

---

## 2. Directory and File Permissions

### 2.1 {{Recommendation title}}

*(Repeat format for each recommendation)*

---

## 3. Logging and Auditing

### 3.1 {{Recommendation title}}

---

## 4. Encryption

### 4.1 {{Recommendation title}}

---

## 5. Authentication

### 5.1 {{Recommendation title}}

---

## 6. Authorization

### 6.1 {{Recommendation title}}

---

## 7. Network

### 7.1 {{Recommendation title}}

---

## CIS Controls Mapping

### Mapping Overview

| CIS Control | Recommendations |
|-------------|-----------------|
| [[Controls/CIS/CIS-3.11\|CIS-3.11]] | 4.1, 4.2 |
| [[Controls/CIS/CIS-5.2\|CIS-5.2]] | 5.1, 5.2 |
| [[Controls/CIS/CIS-6.5\|CIS-6.5]] | 5.3 |
| [[Controls/CIS/CIS-7.3\|CIS-7.3]] | 1.1 |
| [[Controls/CIS/CIS-8.2\|CIS-8.2]] | 3.1, 3.2, 3.3 |

### Implementation Tracking

```dataview
TABLE WITHOUT ID
  link(file.link, control_id) as "Control",
  impl_status as "Status",
  impl_percentage + "%" as "Progress"
FROM "Implementations"
WHERE contains(benchmark, this.file.name)
SORT control_id ASC
```

---

## CIS Change History

| CIS Version | Date | Key Changes |
|-------------|------|-------------|
| v{{BenchmarkVersion}} | {{ReleaseDate}} | Initial version for {{Technology}} {{TechVersion}} |

---

## Related Documents

- [[Components/{{Component}}|{{Component}} Component]]
- [[Documentatie/CIS Benchmark Mapping Guide|CIS Benchmark Mapping Guide]]
- Original PDF: [CIS WorkBench](https://workbench.cisecurity.org/)

---

## Conversion Notes

> **Converted by:** {{converter}}  
> **Conversion date:** {{date}}  
> **Source PDF version:** v{{BenchmarkVersion}}

Sections not converted:
- Appendix A: Glossary (see original PDF)
- Appendix B: Change Log (summarized in Change History)
