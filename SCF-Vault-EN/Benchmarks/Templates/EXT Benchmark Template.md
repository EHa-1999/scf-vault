---
id: "EXT-{{Technology}}-v{{Version}}"
type: benchmark
benchmark_type: "EXT"
name: "Extended Benchmark - {{Technology}}"
technology: "{{Technology}}"
technology_version: "{{TechVersion}}"
benchmark_version: "{{Version}}"
status: Active
last_review: {{date}}
next_review: {{next_review_date}}
owner: "Security Officer"
applies_to:
  - "[[Components/{{Component}}]]"
sources:
  - "{{Vendor}} Security Documentation"
  - "OWASP Guidelines"
  - "NIST 800-53"
recommendations_count: 0
created: {{date}}
modified: {{date}}
tags:
  - benchmark
  - extended
  - {{technology_tag}}
---

# Extended Benchmark: {{Technology}} v{{Version}}

## Benchmark Information

| Field | Value |
|-------|-------|
| **Technology** | {{Technology}} |
| **Technology Version** | {{TechVersion}}+ |
| **Benchmark Version** | v{{Version}} |
| **Status** | Active |
| **Owner** | Security Officer |
| **Last Review** | {{date}} |
| **Next Review** | {{next_review_date}} |

## Navigation

| ← Back | Up | Component |
|--------|-----|-----------|
| [[Benchmarks/EXT/_index\|📙 Extended Benchmarks]] | [[Benchmarks/_index\|📏 Benchmarks]] | [[Components/{{Component}}]] |

---

## 1. Overview

### 1.1 Scope

This Extended Benchmark applies to:
- {{Technology}} version {{TechVersion}} and higher
- Standalone and clustered deployments
- On-premise and container deployments

### 1.2 Why an Extended Benchmark?

No official CIS Benchmark is available for {{Technology}}. This benchmark is developed based on:

| Source | Usage |
|--------|-------|
| [{{Vendor}} Security Documentation]({{vendor_url}}) | Primary configuration reference |
| OWASP Guidelines | Web security best practices |
| NIST 800-53 | Control framework mapping |
| Known CVEs | Specific mitigations |

### 1.3 Profile Definitions

| Profile | Description | Our Choice |
|---------|-------------|------------|
| **Basic** | Minimal security configuration | ✅ Required |
| **Extended** | Additional hardening | ⚠️ Where possible |

---

## 2. Recommendations

### 2.1 Authentication

#### EXT-{{Tech}}-2.1.1: {{Recommendation title}}

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-6.5\|CIS-6.5]] |
| **Source** | {{Vendor}} Security Guide |

**Description:**
{{Description of what needs to be configured}}

**Rationale:**
{{Why this is important for security}}

**Audit:**
```bash
# Check the current configuration
{{audit_command_or_steps}}
```

**Expected result:**
```
{{expected_output}}
```

**Remediation:**
```bash
# Implement the configuration
{{remediation_steps}}
```

**References:**
- [{{Vendor}} Documentation]({{doc_url}})

---

#### EXT-{{Tech}}-2.1.2: {{Next recommendation}}

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-x.y\|CIS-x.y]] |
| **Source** | {{source}} |

*(Repeat format)*

---

### 2.2 Authorization

#### EXT-{{Tech}}-2.2.1: {{Recommendation title}}

---

### 2.3 Cryptography

#### EXT-{{Tech}}-2.3.1: Use TLS for all connections

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-3.10\|CIS-3.10]] |
| **Source** | {{Vendor}} Security Guide |

**Description:**
All communication to and from {{Technology}} must use TLS 1.2 or higher.

**Audit:**
```bash
{{audit_tls_command}}
```

**Remediation:**
```bash
{{enable_tls_steps}}
```

---

#### EXT-{{Tech}}-2.3.2: Encrypt data at rest

| Property | Value |
|----------|-------|
| **Profile** | Extended |
| **CIS Control** | [[Controls/CIS/CIS-3.11\|CIS-3.11]] |

---

### 2.4 Logging and Monitoring

#### EXT-{{Tech}}-2.4.1: Enable audit logging

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-8.2\|CIS-8.2]] |

---

### 2.5 Network

#### EXT-{{Tech}}-2.5.1: Restrict network access

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-4.4\|CIS-4.4]], [[Controls/CIS/CIS-12.2\|CIS-12.2]] |

---

### 2.6 Configuration Hardening

#### EXT-{{Tech}}-2.6.1: Remove default credentials

| Property | Value |
|----------|-------|
| **Profile** | Basic |
| **CIS Control** | [[Controls/CIS/CIS-4.7\|CIS-4.7]] |

---

## 3. CIS Controls Mapping

### Mapping Matrix

| CIS Control | Recommendations | Profile |
|-------------|-----------------|---------|
| [[Controls/CIS/CIS-3.10\|CIS-3.10]] | 2.3.1 | Basic |
| [[Controls/CIS/CIS-3.11\|CIS-3.11]] | 2.3.2 | Extended |
| [[Controls/CIS/CIS-4.4\|CIS-4.4]] | 2.5.1 | Basic |
| [[Controls/CIS/CIS-4.7\|CIS-4.7]] | 2.6.1 | Basic |
| [[Controls/CIS/CIS-6.5\|CIS-6.5]] | 2.1.1 | Basic |
| [[Controls/CIS/CIS-8.2\|CIS-8.2]] | 2.4.1 | Basic |

### Coverage

```dataview
TABLE WITHOUT ID
  length(filter(rows, (r) => r.profile = "Basic")) as "Basic Recs",
  length(filter(rows, (r) => r.profile = "Extended")) as "Extended Recs"
FROM "Benchmarks/EXT"
WHERE file.name = this.file.name
```

---

## 4. Implementation Tracking

### Related Implementations

```dataview
TABLE WITHOUT ID
  link(file.link, control_id) as "Control",
  control_name as "Name",
  impl_status as "Status"
FROM "Implementations"
WHERE contains(benchmark, this.file.name)
SORT control_id ASC
```

---

## 5. Known Vulnerabilities

### CVE Tracking

| CVE | Description | Mitigation | Recommendation |
|-----|-------------|------------|----------------|
| CVE-YYYY-XXXXX | {{description}} | {{mitigation}} | EXT-{{Tech}}-x.x.x |

> **Note:** Monitor [CVE Database](https://cve.mitre.org/) for new vulnerabilities.

---

## 6. Review History

| Version | Date | Reviewer | Changes |
|---------|------|----------|---------|
| v{{Version}} | {{date}} | {{reviewer}} | Initial version |

---

## 7. Sources

### Primary Sources

- [{{Vendor}} Security Documentation]({{vendor_security_url}})
- [{{Vendor}} Hardening Guide]({{vendor_hardening_url}})

### Additional Sources

- [OWASP {{relevant_project}}]({{owasp_url}})
- [NIST 800-53](https://nvd.nist.gov/800-53)
- [CIS Controls v8](https://www.cisecurity.org/controls)

---

## Related Documents

- [[Components/{{Component}}|{{Component}} Component]]
- [[Benchmarks/CIS/_index|CIS Benchmarks]] — Similar official benchmarks
- [[Documentatie/CIS Benchmark Mapping Guide|Benchmark Mapping Guide]]
