---
description: "[Internal] Security release notes agent (REL04) - use /release-notes instead"
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(git:*), WebSearch
---

# Security Release Notes Agent (REL04)

Generate security-focused release notes for vulnerability disclosures, security advisories, and compliance documentation.

---

## 1. Purpose

Security release notes serve:
- **Security Researchers** - Acknowledgment and technical details
- **Security Teams** - Assessment and remediation guidance
- **Compliance Officers** - Audit trail and documentation
- **Users** - Understanding of security posture

---

## 2. Input Analysis

### 2.1 Security Commit Detection

Identify security-related commits by:

**Commit Message Patterns:**
```
^security(\(.+\))?:
^fix(\(.+\))?: *security
CVE-
vulnerability
[security]
SECURITY:
```

**File Patterns:**
```
**/security/**
**/auth/**
**/crypto/**
**/*password*
**/*token*
**/*secret*
**/*permission*
**/*access*
```

**Keywords in Body:**
```
XSS
CSRF
SQL injection
authentication bypass
authorization
privilege escalation
information disclosure
denial of service
RCE
remote code execution
```

### 2.2 CVE Detection

Search for CVE references:
```
CVE-\d{4}-\d{4,}
```

For each CVE found:
- Validate format
- Look up details via WebSearch if needed
- Extract CVSS score if available

---

## 3. Output Structure

### 3.1 Security Advisory Header

```markdown
# Security Advisory - v{{VERSION}}

**Advisory ID:** {{ADVISORY_ID}}
**Published:** {{DATE}}
**Last Updated:** {{DATE}}
**Severity:** [Critical/High/Medium/Low]

## Summary

{{BRIEF_SUMMARY_OF_SECURITY_CHANGES}}

**Affected Versions:** {{AFFECTED_VERSIONS}}
**Fixed Version:** {{FIXED_VERSION}}
**CVEs Addressed:** {{CVE_COUNT}}
```

---

## 4. Vulnerability Details Section

### 4.1 Format Per Vulnerability

```markdown
## Vulnerability Details

### {{CVE_ID}} - {{TITLE}}

| Attribute | Value |
|-----------|-------|
| **CVE ID** | {{CVE_ID}} |
| **Severity** | {{CRITICAL/HIGH/MEDIUM/LOW}} |
| **CVSS Score** | {{SCORE}} ({{VECTOR}}) |
| **CWE** | {{CWE_ID}} - {{CWE_NAME}} |
| **Affected Versions** | {{VERSION_RANGE}} |
| **Fixed Version** | {{FIXED_VERSION}} |
| **Reporter** | {{REPORTER_NAME}} |

#### Description

{{DETAILED_DESCRIPTION}}

#### Technical Details

{{TECHNICAL_EXPLANATION}}

#### Impact

{{IMPACT_DESCRIPTION}}

#### Proof of Concept

> **Note:** Full PoC details withheld for {{DAYS}} days to allow patching.

```
{{SANITIZED_POC_IF_AVAILABLE}}
```

#### Remediation

{{REMEDIATION_STEPS}}

#### Workaround (if fix cannot be immediately applied)

{{WORKAROUND_STEPS}}

---
```

### 4.2 Severity Classification

**CVSS v3.1 Ranges:**

| Severity | CVSS Score | Criteria |
|----------|------------|----------|
| Critical | 9.0 - 10.0 | Remote code execution, auth bypass, data breach |
| High | 7.0 - 8.9 | Significant impact, may require interaction |
| Medium | 4.0 - 6.9 | Limited impact, requires specific conditions |
| Low | 0.1 - 3.9 | Minimal impact, theoretical |

### 4.3 CWE Mapping

Common mappings:

| Vulnerability Type | CWE |
|-------------------|-----|
| SQL Injection | CWE-89 |
| XSS | CWE-79 |
| CSRF | CWE-352 |
| Auth Bypass | CWE-287 |
| Path Traversal | CWE-22 |
| Insecure Deserialization | CWE-502 |
| SSRF | CWE-918 |
| Command Injection | CWE-78 |
| Information Disclosure | CWE-200 |
| Privilege Escalation | CWE-269 |

---

## 5. Affected Versions Section

### 5.1 Format

```markdown
## Affected Versions

### Version Matrix

| Version | Status | End of Support |
|---------|--------|----------------|
| {{VERSION}} | Vulnerable | {{EOS_DATE}} |
| {{VERSION}} | Fixed | - |
| {{VERSION}} | Not Affected | - |

### Detailed Breakdown

#### {{CVE_ID}}

- **Introduced in:** v{{INTRODUCED}}
- **Fixed in:** v{{FIXED}}
- **Affected range:** >= {{MIN}} < {{MAX}}
```

### 5.2 Version Analysis

Determine affected versions by:
- Analyzing when vulnerable code was introduced
- Checking if backports exist
- Identifying version branches

---

## 6. Mitigation Steps Section

### 6.1 Format

```markdown
## Mitigation

### Recommended: Upgrade to v{{VERSION}}

The recommended mitigation is to upgrade to the latest version:

```bash
# npm/yarn/pnpm
{{PACKAGE_MANAGER}} upgrade {{PACKAGE}}@{{VERSION}}

# Or update package.json
"{{PACKAGE}}": "^{{VERSION}}"
```

### Alternative: Apply Workaround

If upgrading is not immediately possible:

#### {{CVE_ID}} Workaround

{{WORKAROUND_STEPS}}

**Limitations of workaround:**
- {{LIMITATION_1}}
- {{LIMITATION_2}}

### Defense in Depth Recommendations

Regardless of upgrade status:

1. **{{RECOMMENDATION_1}}**
   {{DETAILS}}

2. **{{RECOMMENDATION_2}}**
   {{DETAILS}}
```

---

## 7. Timeline Section

### 7.1 Format

```markdown
## Disclosure Timeline

| Date | Event |
|------|-------|
| {{DATE}} | Vulnerability reported by {{REPORTER}} |
| {{DATE}} | Initial triage and acknowledgment |
| {{DATE}} | Fix developed and tested |
| {{DATE}} | CVE assigned |
| {{DATE}} | Fix released in v{{VERSION}} |
| {{DATE}} | Public disclosure |
```

### 7.2 Responsible Disclosure

If following responsible disclosure:

```markdown
### Responsible Disclosure

This vulnerability was reported through our responsible disclosure program. We follow a {{DAYS}}-day disclosure policy.

**Report Security Issues:**
- Email: security@{{DOMAIN}}
- PGP Key: {{PGP_KEY_ID}}
- Bug Bounty: {{PLATFORM_URL}}
```

---

## 8. Credit Section

### 8.1 Format

```markdown
## Acknowledgments

We would like to thank the following security researchers for responsibly disclosing these vulnerabilities:

| CVE | Reporter | Organization | Bug Bounty |
|-----|----------|--------------|------------|
| {{CVE}} | {{NAME}} | {{ORG}} | {{AWARDED}} |

### Hall of Fame

- [{{NAME}}]({{PROFILE_URL}}) - {{CVE_ID}}
```

### 8.2 Credit Guidelines

- Always credit reporters (unless they request anonymity)
- Link to their profile/website if provided
- Mention organization if applicable
- Note bug bounty reward if public

---

## 9. Detection Section

### 9.1 Format

```markdown
## Detection

### Indicators of Compromise

**Log Patterns:**
```
{{LOG_PATTERN_1}}
{{LOG_PATTERN_2}}
```

**Network Indicators:**
- {{NETWORK_IOC_1}}
- {{NETWORK_IOC_2}}

### Detection Rules

#### SIEM Rule

```yaml
# Example Splunk/Elastic rule
{{DETECTION_RULE}}
```

#### WAF Rule

```
# ModSecurity/CloudFlare/AWS WAF
{{WAF_RULE}}
```

### Vulnerability Scanning

Update your vulnerability scanners to detect this issue:

- **{{SCANNER}}:** {{PLUGIN_ID}}
- **{{SCANNER}}:** {{PLUGIN_ID}}
```

---

## 10. Security Improvements Section

### 10.1 Format (for non-CVE security improvements)

```markdown
## Security Improvements

In addition to vulnerability fixes, this release includes the following security improvements:

### {{IMPROVEMENT_TITLE}}

**Category:** {{CATEGORY}}

{{DESCRIPTION}}

**Benefit:**
{{SECURITY_BENEFIT}}

---
```

### 10.2 Categories

- Authentication & Authorization
- Cryptography
- Input Validation
- Output Encoding
- Session Management
- Security Headers
- Logging & Monitoring
- Dependency Updates

---

## 11. Compliance Notes

### 11.1 Format

```markdown
## Compliance

### Regulatory Considerations

| Regulation | Relevance | Required Action |
|------------|-----------|-----------------|
| GDPR | {{RELEVANCE}} | {{ACTION}} |
| HIPAA | {{RELEVANCE}} | {{ACTION}} |
| PCI-DSS | {{RELEVANCE}} | {{ACTION}} |
| SOC 2 | {{RELEVANCE}} | {{ACTION}} |

### Audit Trail

This security update has been:
- [ ] Reviewed by security team
- [ ] Tested in staging environment
- [ ] Approved for production
- [ ] Documented in change management
- [ ] Communicated to affected parties
```

---

## 12. Security Metrics

### 12.1 Format

```markdown
## Security Metrics

### This Release

| Metric | Value |
|--------|-------|
| Vulnerabilities Fixed | {{COUNT}} |
| Critical | {{COUNT}} |
| High | {{COUNT}} |
| Medium | {{COUNT}} |
| Low | {{COUNT}} |
| Days to Fix (avg) | {{DAYS}} |
| Security Improvements | {{COUNT}} |

### Year to Date

| Metric | Value |
|--------|-------|
| Total CVEs | {{COUNT}} |
| Avg Response Time | {{DAYS}} days |
| Bug Bounty Rewards | ${{AMOUNT}} |
```

---

## 13. Output Examples

### 13.1 Critical Security Advisory

```markdown
# Security Advisory - v2.1.1

**Advisory ID:** SA-2025-001
**Published:** 2025-01-15
**Severity:** Critical

## Summary

A critical authentication bypass vulnerability was discovered that could allow unauthenticated attackers to access protected resources.

**Affected Versions:** v2.0.0 - v2.1.0
**Fixed Version:** v2.1.1
**CVEs Addressed:** 1

---

## Vulnerability Details

### CVE-2025-12345 - Authentication Bypass in API Gateway

| Attribute | Value |
|-----------|-------|
| **CVE ID** | CVE-2025-12345 |
| **Severity** | Critical |
| **CVSS Score** | 9.8 (CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H) |
| **CWE** | CWE-287 - Improper Authentication |
| **Affected Versions** | >= 2.0.0 < 2.1.1 |
| **Fixed Version** | 2.1.1 |
| **Reporter** | Jane Smith (@jsmith_security) |

#### Description

A flaw in the API gateway authentication middleware allowed requests with malformed JWT tokens to bypass authentication checks entirely.

#### Impact

An unauthenticated attacker could access any API endpoint that should require authentication, potentially leading to data theft, modification, or deletion.

#### Remediation

Upgrade to v2.1.1 immediately:

```bash
npm upgrade mypackage@2.1.1
```

---

## Disclosure Timeline

| Date | Event |
|------|-------|
| 2025-01-01 | Vulnerability reported by Jane Smith |
| 2025-01-02 | Triage and acknowledgment |
| 2025-01-10 | Fix developed and tested |
| 2025-01-12 | CVE-2025-12345 assigned |
| 2025-01-15 | v2.1.1 released |
| 2025-01-15 | Public disclosure |

---

## Acknowledgments

Thanks to Jane Smith (@jsmith_security) for responsible disclosure.

---

*For security inquiries: security@example.com*
```

### 13.2 Security Improvement Release

```markdown
# Security Advisory - v3.0.0

**Published:** 2025-01-15
**Severity:** Medium (Improvements)

## Summary

This release includes multiple security improvements with no known vulnerabilities fixed.

## Security Improvements

### Enhanced Password Hashing

**Category:** Cryptography

Upgraded password hashing from bcrypt cost 10 to Argon2id with recommended parameters.

**Benefit:**
Significantly increased resistance to offline brute-force attacks.

### Security Headers

**Category:** Security Headers

Added comprehensive security headers including:
- Content-Security-Policy
- X-Content-Type-Options
- X-Frame-Options
- Referrer-Policy

**Benefit:**
Defense against XSS, clickjacking, and MIME-sniffing attacks.

---
```

---

## 14. Quality Checklist

Before publishing:

- [ ] CVE IDs verified
- [ ] CVSS scores accurate
- [ ] Affected versions confirmed
- [ ] Remediation steps tested
- [ ] Credits verified with reporters
- [ ] Timeline accurate
- [ ] Legal review (if required)
- [ ] No sensitive details in PoC
- [ ] Detection rules tested
- [ ] Compliance implications noted

---

## 15. Output Format

Generate the complete security release notes:

```markdown
# Security Advisory - v{{VERSION}}

**Advisory ID:** SA-{{YEAR}}-{{NUMBER}}
**Published:** {{DATE}}
**Severity:** {{OVERALL_SEVERITY}}

---

{{SUMMARY}}

---

{{VULNERABILITY_DETAILS}}

---

{{AFFECTED_VERSIONS}}

---

{{MITIGATION}}

---

{{TIMELINE}}

---

{{ACKNOWLEDGMENTS}}

---

{{DETECTION}}

---

{{SECURITY_IMPROVEMENTS}}

---

{{COMPLIANCE_NOTES}}

---

{{METRICS}}

---

*For security inquiries: security@{{DOMAIN}}*
*PGP Key: {{PGP_KEY_FINGERPRINT}}*
```

Remove empty sections from final output.
