---
id: "EXT-MinIO"
type: extended-benchmark
name: "Extended Benchmark - MinIO"
component: "[[Components/MinIO]]"
version: "1.0"
status: Active
last_review: 2026-01-28
sources:
  - "MinIO Security Documentation"
  - "AWS S3 Security Best Practices"
  - "CIS Controls v8"
created: 2026-01-28
modified: 2026-01-28
tags:
  - benchmark
  - extended
  - minio
  - storage
---

# Extended Benchmark: MinIO

## 1. Overzicht

| Veld | Waarde |
|------|--------|
| **Component** | MinIO |
| **Type** | Object Storage (S3-compatible) |
| **Benchmark Versie** | 1.0 |
| **Laatste Review** | 2026-01-28 |
| **Gebaseerd op** | MinIO Security Docs, AWS S3 Best Practices |

### 1.1 Scope

Deze extended benchmark is van toepassing op:
- MinIO Server (standalone en distributed)
- MinIO Console
- S3 API endpoints
- Bucket policies en IAM

### 1.2 Bronnen

| Bron | URL |
|------|-----|
| MinIO Security | https://min.io/docs/minio/linux/operations/security.html |
| MinIO Hardening | https://min.io/docs/minio/linux/operations/checklists/security.html |
| AWS S3 Security | https://docs.aws.amazon.com/s3/security |

---

## 2. Recommendations

### 2.1 Encryption

#### EXT-MINIO-1: Enable Server-Side Encryption (SSE-S3)

**Beschrijving:**  
Alle objecten moeten worden versleuteld bij opslag met minimaal AES-256.

**Rationale:**  
Beschermt data tegen ongeautoriseerde toegang bij fysieke toegang tot storage.

**CIS Control Mapping:** [[Controls/CIS/CIS-3.11 - Encrypt Sensitive Data at Rest|CIS-3.11]]

**Audit:**
```bash
# Check SSE auto-encryption setting
mc admin config get myminio api | grep auto_encryption
# Expected: auto_encryption: on
```

**Remediation:**
```bash
# Enable auto-encryption
mc admin config set myminio api auto_encryption=on

# Restart MinIO
mc admin service restart myminio
```

**Evidence:** Screenshot van mc admin config output

---

#### EXT-MINIO-2: Enable TLS for All Connections

**Beschrijving:**  
Alle verbindingen naar MinIO moeten via TLS 1.2+ verlopen.

**Rationale:**  
Beschermt data in transit tegen afluisteren en man-in-the-middle aanvallen.

**CIS Control Mapping:** [[Controls/CIS/CIS-3.10 - Encrypt Sensitive Data in Transit|CIS-3.10]]

**Audit:**
```bash
# Check TLS configuration
curl -v https://minio.example.com:9000 2>&1 | grep -i "SSL connection"
# Expected: SSL connection using TLSv1.3

# Check certificate validity
openssl s_client -connect minio.example.com:9000 -servername minio.example.com
```

**Remediation:**
```bash
# Configure TLS certificates
export MINIO_CERTS_DIR=/path/to/certs

# Place certificates
# - public.crt (certificate)
# - private.key (private key)
# - CAs/ (CA certificates)

# Restart MinIO
systemctl restart minio
```

**Evidence:** TLS scan rapport (bijv. testssl.sh output)

---

#### EXT-MINIO-3: Configure Key Management Service (KMS)

**Beschrijving:**  
Encryptiesleutels moeten worden beheerd door een externe KMS (bijv. OpenBAO/Vault).

**Rationale:**  
Scheiding van data en sleutels, centrale key management, key rotation.

**CIS Control Mapping:** [[Controls/CIS/CIS-3.11 - Encrypt Sensitive Data at Rest|CIS-3.11]]

**Audit:**
```bash
# Check KMS configuration
mc admin config get myminio kms_kes

# Expected output shows KMS endpoint
```

**Remediation:**
```bash
# Configure KES (Key Encryption Service) with Vault backend
mc admin config set myminio kms_kes \
    endpoint=https://kes.example.com:7373 \
    key_name=minio-key-1 \
    enclave_name=default
```

**Evidence:** KMS configuratie export

---

### 2.2 Access Control

#### EXT-MINIO-4: Disable Root User for Regular Operations

**Beschrijving:**  
De root gebruiker (MINIO_ROOT_USER) mag alleen worden gebruikt voor initiële setup en emergency access.

**Rationale:**  
Beperkt blast radius van credential compromise.

**CIS Control Mapping:** [[Controls/CIS/CIS-5.4 - Restrict Administrator Privileges|CIS-5.4]]

**Audit:**
```bash
# Check for root user usage in audit logs
grep "MINIO_ROOT_USER" /var/log/minio/audit.log

# List all users - root should not be used for daily operations
mc admin user list myminio
```

**Remediation:**
1. Maak dedicated admin users aan:
```bash
mc admin user add myminio admin-user SecurePassword123!
mc admin policy attach myminio consoleAdmin --user admin-user
```

2. Documenteer root credentials in secure vault
3. Roteer root credentials na elke noodtoegang

**Evidence:** Lijst van users, audit log sample

---

#### EXT-MINIO-5: Implement Bucket Policies

**Beschrijving:**  
Elk bucket moet een expliciete access policy hebben; geen publieke toegang.

**Rationale:**  
Principle of least privilege, voorkomt data lekkage.

**CIS Control Mapping:** [[Controls/CIS/CIS-6.8 - Define and Maintain Role-Based Access Control|CIS-6.8]]

**Audit:**
```bash
# Check bucket policies for all buckets
for bucket in $(mc ls myminio | awk '{print $NF}'); do
    echo "=== $bucket ==="
    mc policy get myminio/$bucket
done

# Expected: No "public" or "download" policies
```

**Remediation:**
```bash
# Remove public access
mc anonymous remove myminio/mybucket

# Set private policy
mc policy set none myminio/mybucket

# Configure specific access via IAM policies
mc admin policy create myminio mybucket-readonly mybucket-readonly-policy.json
```

**Evidence:** Bucket policy export voor alle buckets

---

#### EXT-MINIO-6: Enable Multi-Factor Authentication for Console

**Beschrijving:**  
Toegang tot de MinIO Console moet worden beschermd met MFA.

**Rationale:**  
Extra beschermingslaag tegen credential compromise.

**CIS Control Mapping:** [[Controls/CIS/CIS-6.5 - Require MFA for Administrative Access|CIS-6.5]]

**Audit:**
1. Login op MinIO Console
2. Ga naar Identity → Users → {user}
3. Controleer of MFA is geconfigureerd

**Remediation:**
Via OIDC integratie met KeyCloak (aanbevolen):
```bash
mc admin config set myminio identity_openid \
    config_url="https://keycloak.example.com/realms/master/.well-known/openid-configuration" \
    client_id="minio" \
    client_secret="XXXXX" \
    scopes="openid,profile,email"
```

**Evidence:** OIDC configuratie, KeyCloak MFA policy

---

### 2.3 Logging & Monitoring

#### EXT-MINIO-7: Enable Audit Logging

**Beschrijving:**  
Alle API calls moeten worden gelogd met minimaal: timestamp, user, action, bucket, object, source IP.

**Rationale:**  
Forensische analyse, compliance, anomaly detection.

**CIS Control Mapping:** [[Controls/CIS/CIS-8.2 - Collect Audit Logs|CIS-8.2]]

**Audit:**
```bash
# Check audit log configuration
mc admin config get myminio audit_webhook

# Check audit logs are being generated
ls -la /var/log/minio/audit/
```

**Remediation:**
```bash
# Configure audit webhook (bijv. naar Elasticsearch)
mc admin config set myminio audit_webhook:elastic \
    endpoint=https://elasticsearch.example.com:9200/minio-audit/_doc \
    auth_token=Bearer:XXXXX

# Of lokale audit logging
mc admin config set myminio audit_kafka \
    enable=on \
    brokers=kafka.example.com:9092 \
    topic=minio-audit
```

**Evidence:** Sample audit log entries

---

#### EXT-MINIO-8: Configure Log Retention

**Beschrijving:**  
Audit logs moeten minimaal 1 jaar worden bewaard.

**Rationale:**  
Compliance vereisten, incident investigation timeline.

**CIS Control Mapping:** [[Controls/CIS/CIS-8.10 - Retain Audit Logs|CIS-8.10]]

**Audit:**
```bash
# Check oldest available audit logs
ls -la /var/log/minio/audit/ | head -10

# Or check Elasticsearch retention policy
curl -X GET "elasticsearch.example.com:9200/_ilm/policy/minio-audit"
```

**Remediation:**
```bash
# Configure Elasticsearch ILM policy for 1 year retention
curl -X PUT "elasticsearch.example.com:9200/_ilm/policy/minio-audit" \
-H 'Content-Type: application/json' -d'
{
  "policy": {
    "phases": {
      "delete": {
        "min_age": "365d",
        "actions": { "delete": {} }
      }
    }
  }
}'
```

**Evidence:** Retention policy configuratie

---

### 2.4 Data Protection

#### EXT-MINIO-9: Enable Object Versioning

**Beschrijving:**  
Versioning moet zijn ingeschakeld voor buckets met belangrijke data.

**Rationale:**  
Bescherming tegen accidentele deletes, ransomware recovery.

**CIS Control Mapping:** [[Controls/CIS/CIS-11.3 - Protect Recovery Data|CIS-11.3]]

**Audit:**
```bash
# Check versioning status
mc version info myminio/mybucket
```

**Remediation:**
```bash
# Enable versioning
mc version enable myminio/mybucket
```

**Evidence:** Versioning status output voor alle kritieke buckets

---

#### EXT-MINIO-10: Configure Object Lock for Compliance

**Beschrijving:**  
Object Lock (WORM) moet worden ingeschakeld voor buckets met compliance vereisten.

**Rationale:**  
Onveranderbare opslag voor audit trails, wettelijke bewaarplicht.

**CIS Control Mapping:** [[Controls/CIS/CIS-11.3 - Protect Recovery Data|CIS-11.3]]

**Audit:**
```bash
# Check object lock configuration
mc retention info myminio/compliance-bucket
```

**Remediation:**
```bash
# Bucket moet worden aangemaakt met object-lock enabled
mc mb myminio/compliance-bucket --with-lock

# Set retention policy
mc retention set --default COMPLIANCE 7y myminio/compliance-bucket
```

**Evidence:** Object Lock configuratie, retention policy

---

### 2.5 Configuration Management

#### EXT-MINIO-11: Disable Unnecessary Features

**Beschrijving:**  
Niet-gebruikte features en endpoints moeten worden uitgeschakeld.

**Rationale:**  
Reduceert attack surface.

**CIS Control Mapping:** [[Controls/CIS/CIS-4.8 - Uninstall or Disable Unnecessary Services|CIS-4.8]]

**Audit:**
```bash
# Check enabled features
mc admin config get myminio | grep enable

# Check if browser (Console) access is needed
mc admin config get myminio api browser
```

**Remediation:**
```bash
# Disable browser if not needed
mc admin config set myminio api browser=off

# Disable anonymous access
mc admin config set myminio api requests_max=0
```

**Evidence:** Feature configuration export

---

## 3. Implementation Checklist

| # | Recommendation | IG | Status |
|---|----------------|-------|--------|
| 1 | SSE-S3 Encryption | IG1 | ☐ |
| 2 | TLS Connections | IG1 | ☐ |
| 3 | KMS Integration | IG2 | ☐ |
| 4 | Disable Root User | IG1 | ☐ |
| 5 | Bucket Policies | IG1 | ☐ |
| 6 | MFA for Console | IG1 | ☐ |
| 7 | Audit Logging | IG1 | ☐ |
| 8 | Log Retention | IG2 | ☐ |
| 9 | Object Versioning | IG2 | ☐ |
| 10 | Object Lock | IG3 | ☐ |
| 11 | Disable Unused Features | IG1 | ☐ |

---

## 4. CIS Control Mapping Summary

| CIS Control | Recommendations |
|-------------|-----------------|
| CIS-3.10 | EXT-MINIO-2 |
| CIS-3.11 | EXT-MINIO-1, EXT-MINIO-3 |
| CIS-4.8 | EXT-MINIO-11 |
| CIS-5.4 | EXT-MINIO-4 |
| CIS-6.5 | EXT-MINIO-6 |
| CIS-6.8 | EXT-MINIO-5 |
| CIS-8.2 | EXT-MINIO-7 |
| CIS-8.10 | EXT-MINIO-8 |
| CIS-11.3 | EXT-MINIO-9, EXT-MINIO-10 |

---

## 5. Wijzigingshistorie

| Versie | Datum | Auteur | Wijziging |
|--------|-------|--------|-----------|
| 1.0 | 2026-01-28 | Security Team | Initiële versie |

## Gerelateerde Documenten

- [[Components/MinIO|MinIO Component]]
- [[Documentatie/CIS Benchmark Mapping Guide|Benchmark Mapping Guide]]
- [[Documentatie/System Onboarding Guide|System Onboarding Guide]]
