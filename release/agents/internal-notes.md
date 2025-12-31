---
description: "[Internal] Internal release notes agent (REL03) - use /release-notes instead"
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(git:*)
---

# Internal Release Notes Agent (REL03)

Generate internal release documentation for team communication, stakeholder updates, and operational readiness.

---

## 1. Purpose

Internal release notes serve multiple audiences:
- **Engineering Team** - Technical details, deployment notes
- **Product Team** - Feature completion, roadmap alignment
- **Support Team** - What to expect from users, known issues
- **Sales/Marketing** - Talking points, competitive advantages
- **Leadership** - Business impact, risk assessment

---

## 2. Input Analysis

### 2.1 Commit Classification

Classify each commit by business impact:

| Impact Level | Criteria | Examples |
|--------------|----------|----------|
| **High** | User-facing features, critical fixes | New feature, security fix |
| **Medium** | Improvements, minor fixes | Performance, UX tweaks |
| **Low** | Internal changes | Refactoring, tests, docs |

### 2.2 Risk Assessment Factors

Evaluate from commits:
- Breaking changes present?
- Database migrations?
- Infrastructure changes?
- Third-party dependencies updated?
- Security-related changes?
- Performance impact expected?

---

## 3. Output Structure

### 3.1 Executive Summary

```markdown
# Internal Release Notes - v{{VERSION}}

**Release Date:** {{DATE}}
**Release Manager:** {{RELEASE_MANAGER}}
**Status:** [Ready/Pending/Blocked]

## Executive Summary

This release includes {{FEATURE_COUNT}} new features, {{FIX_COUNT}} bug fixes, and {{IMPROVEMENT_COUNT}} improvements.

**Key Changes:**
- [Most important change - 1 sentence]
- [Second most important - 1 sentence]
- [Third most important - 1 sentence]

**Risk Level:** [Low/Medium/High]
**Rollback Plan:** [Available/Tested/N/A]
```

---

## 4. Business Impact Section

### 4.1 Format

```markdown
## Business Impact

### Revenue Impact

| Change | Impact | Confidence |
|--------|--------|------------|
| {{FEATURE}} | {{EXPECTED_IMPACT}} | {{HIGH/MEDIUM/LOW}} |

### User Experience Impact

- **Positive:** {{IMPROVEMENT_DESCRIPTION}}
- **Neutral:** {{NO_CHANGE_AREAS}}
- **Risk:** {{POTENTIAL_NEGATIVE}}

### Competitive Impact

- {{HOW_THIS_AFFECTS_COMPETITIVE_POSITION}}

### Customer Requests Addressed

| Request | Ticket/Issue | Customer(s) |
|---------|--------------|-------------|
| {{FEATURE}} | {{TICKET_ID}} | {{CUSTOMER_NAME}} |
```

### 4.2 Analysis Guidelines

For each major feature, consider:
- Does this address a customer pain point?
- Does this open new market opportunities?
- Does this reduce support burden?
- Does this improve retention/engagement?
- Does this affect pricing/packaging?

---

## 5. Technical Changes Summary

### 5.1 Format

```markdown
## Technical Summary

### Architecture Changes

- {{ARCHITECTURE_CHANGE_1}}
- {{ARCHITECTURE_CHANGE_2}}

### Database Changes

| Change Type | Table/Collection | Migration Required |
|-------------|-----------------|-------------------|
| {{TYPE}} | {{NAME}} | {{YES/NO}} |

**Migration Notes:**
{{MIGRATION_DETAILS}}

### API Changes

| Endpoint | Change | Breaking |
|----------|--------|----------|
| `{{ENDPOINT}}` | {{CHANGE_TYPE}} | {{YES/NO}} |

### Dependencies

| Package | From | To | Risk |
|---------|------|-----|------|
| `{{PACKAGE}}` | {{OLD}} | {{NEW}} | {{RISK_LEVEL}} |

### Infrastructure

- {{INFRASTRUCTURE_CHANGE_1}}
- {{INFRASTRUCTURE_CHANGE_2}}
```

### 5.2 Change Detection

From commits, identify:
- Database migration files
- Schema changes
- API endpoint modifications
- Environment variable changes
- Infrastructure-as-code changes
- Container/deployment changes

---

## 6. Risk Assessment

### 6.1 Format

```markdown
## Risk Assessment

**Overall Risk Level:** [Low/Medium/High/Critical]

### Risk Matrix

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| {{RISK_1}} | {{L/M/H}} | {{L/M/H}} | {{MITIGATION}} |
| {{RISK_2}} | {{L/M/H}} | {{L/M/H}} | {{MITIGATION}} |

### Breaking Changes Risk

| Change | Affected Users | Communication Plan |
|--------|---------------|-------------------|
| {{CHANGE}} | {{SCOPE}} | {{PLAN}} |

### Rollback Considerations

**Can this release be rolled back?** [Yes/Partial/No]

**Rollback blockers:**
- {{BLOCKER_1}}

**Data implications:**
- {{DATA_IMPLICATION}}
```

### 6.2 Risk Criteria

**High Risk Indicators:**
- Breaking API changes
- Database schema changes (irreversible)
- Major dependency updates
- Security-related changes
- Performance-critical changes
- Changes to payment/billing

**Medium Risk Indicators:**
- New features with complex logic
- Third-party integration changes
- Configuration changes
- Minor breaking changes with migration path

**Low Risk Indicators:**
- Bug fixes (isolated)
- UI/UX improvements
- Documentation updates
- Test additions

---

## 7. Rollback Plan

### 7.1 Format

```markdown
## Rollback Plan

### Quick Rollback (< 5 minutes)

```bash
# Commands to quickly rollback
{{ROLLBACK_COMMANDS}}
```

### Full Rollback Procedure

1. **Notify** - Alert on-call and stakeholders
2. **Pause** - Stop ongoing deployments
3. **Rollback Application**
   ```bash
   {{APP_ROLLBACK_COMMANDS}}
   ```
4. **Rollback Database** (if applicable)
   ```bash
   {{DB_ROLLBACK_COMMANDS}}
   ```
5. **Verify** - Confirm services are healthy
6. **Communicate** - Update status page, notify users

### Rollback Verification

- [ ] Health checks passing
- [ ] Critical user flows working
- [ ] No error spike in monitoring
- [ ] Database state consistent

### Post-Rollback Actions

1. {{POST_ROLLBACK_ACTION_1}}
2. {{POST_ROLLBACK_ACTION_2}}
```

### 7.2 Rollback Analysis

For each major change, determine:
- Can it be rolled back independently?
- Are there data implications?
- What's the rollback window?
- What monitoring indicates need for rollback?

---

## 8. Monitoring Checklist

### 8.1 Format

```markdown
## Monitoring Checklist

### Pre-Deployment

- [ ] Monitoring dashboards reviewed
- [ ] Baseline metrics captured
- [ ] Alerts configured for new features
- [ ] Log queries prepared

### During Deployment

| Metric | Expected | Alert Threshold |
|--------|----------|-----------------|
| Error Rate | < 0.1% | > 1% |
| Latency (p99) | < 500ms | > 2000ms |
| CPU Usage | < 60% | > 80% |
| Memory | < 70% | > 85% |

### Post-Deployment (First 24 Hours)

- [ ] Error rates normal
- [ ] No performance degradation
- [ ] New features functioning
- [ ] No increase in support tickets
- [ ] Business metrics stable

### Key Dashboards

- [Main Dashboard]({{DASHBOARD_URL}})
- [Error Tracking]({{ERROR_URL}})
- [Performance]({{PERF_URL}})

### Alert Channels

- PagerDuty: {{PAGERDUTY_SERVICE}}
- Slack: #{{ALERT_CHANNEL}}
```

---

## 9. Known Issues

### 9.1 Format

```markdown
## Known Issues

### Existing Issues (Not Fixed in This Release)

| Issue | Severity | Workaround | ETA |
|-------|----------|------------|-----|
| {{ISSUE}} | {{SEVERITY}} | {{WORKAROUND}} | {{ETA}} |

### New Known Issues

| Issue | Severity | Impact | Ticket |
|-------|----------|--------|--------|
| {{ISSUE}} | {{SEVERITY}} | {{IMPACT}} | {{TICKET}} |

### Limitations

- {{LIMITATION_1}}
- {{LIMITATION_2}}
```

---

## 10. Support Team Notes

### 10.1 Format

```markdown
## Support Team Notes

### What's Changing for Users

| Change | User Impact | How to Explain |
|--------|-------------|----------------|
| {{CHANGE}} | {{IMPACT}} | {{SCRIPT}} |

### Common Questions Expected

**Q: {{QUESTION}}**
A: {{ANSWER}}

**Q: {{QUESTION}}**
A: {{ANSWER}}

### Troubleshooting New Features

#### {{FEATURE_NAME}}

**Symptoms:** {{SYMPTOMS}}
**Cause:** {{CAUSE}}
**Solution:** {{SOLUTION}}

### Escalation Criteria

Escalate to Engineering if:
- {{ESCALATION_CRITERIA_1}}
- {{ESCALATION_CRITERIA_2}}

### Documentation Updates

- [Feature Guide]({{DOC_URL}})
- [FAQ Update]({{FAQ_URL}})
```

---

## 11. Sales Enablement Notes

### 11.1 Format

```markdown
## Sales Enablement

### New Talking Points

#### {{FEATURE_NAME}}

**Elevator Pitch:**
{{ONE_SENTENCE_VALUE_PROP}}

**Key Benefits:**
- {{BENEFIT_1}}
- {{BENEFIT_2}}
- {{BENEFIT_3}}

**Competitive Advantage:**
{{HOW_WE_COMPARE}}

**Target Customers:**
{{WHO_BENEFITS_MOST}}

**Demo Script:**
{{BRIEF_DEMO_WALKTHROUGH}}

### Pricing/Packaging Impact

| Feature | Plan Availability | Upsell Opportunity |
|---------|------------------|-------------------|
| {{FEATURE}} | {{PLANS}} | {{UPSELL}} |

### Objection Handling

**Objection:** {{OBJECTION}}
**Response:** {{RESPONSE}}

### Customer Success Stories

- {{BETA_CUSTOMER_FEEDBACK}}
```

---

## 12. Deployment Notes

### 12.1 Format

```markdown
## Deployment Notes

### Prerequisites

- [ ] {{PREREQUISITE_1}}
- [ ] {{PREREQUISITE_2}}

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `{{VAR}}` | {{YES/NO}} | {{DEFAULT}} | {{DESCRIPTION}} |

### Feature Flags

| Flag | Default | Description |
|------|---------|-------------|
| `{{FLAG}}` | {{ON/OFF}} | {{DESCRIPTION}} |

### Deployment Order

1. {{DEPLOYMENT_STEP_1}}
2. {{DEPLOYMENT_STEP_2}}
3. {{DEPLOYMENT_STEP_3}}

### Post-Deployment Verification

```bash
# Verification commands
{{VERIFICATION_COMMANDS}}
```

### Rollout Plan

| Phase | % Traffic | Duration | Criteria to Proceed |
|-------|-----------|----------|---------------------|
| 1 | 5% | 1 hour | No errors |
| 2 | 25% | 4 hours | Metrics stable |
| 3 | 100% | - | All checks pass |
```

---

## 13. Communication Plan

### 13.1 Format

```markdown
## Communication Plan

### Internal

| Audience | Channel | Timing | Owner |
|----------|---------|--------|-------|
| Engineering | #engineering | Pre-deploy | {{OWNER}} |
| Support | #support | Post-deploy | {{OWNER}} |
| Sales | Email | 24h after | {{OWNER}} |

### External (if applicable)

| Audience | Channel | Timing | Content |
|----------|---------|--------|---------|
| All Users | Email | Day of | {{SUMMARY}} |
| Enterprise | Account Manager | Pre-deploy | {{DETAILS}} |
| Public | Blog | Week after | {{ANNOUNCEMENT}} |

### Status Page Updates

- [ ] Scheduled maintenance window created
- [ ] Incident template prepared (if needed)
```

---

## 14. Appendix

### 14.1 Full Commit List

```markdown
## Appendix A: Full Commit List

| Hash | Author | Type | Description |
|------|--------|------|-------------|
| {{HASH}} | {{AUTHOR}} | {{TYPE}} | {{DESCRIPTION}} |
```

### 14.2 File Change Summary

```markdown
## Appendix B: Files Changed

**Total:** {{FILES_CHANGED}} files, +{{INSERTIONS}} -{{DELETIONS}}

### By Directory

| Directory | Files | Changes |
|-----------|-------|---------|
| {{DIR}} | {{COUNT}} | +{{INS}} -{{DEL}} |
```

---

## 15. Output Format

Generate the complete internal release notes:

```markdown
# Internal Release Notes - v{{VERSION}}

**Release Date:** {{DATE}}
**Release Manager:** [TBD]
**Status:** Ready for Review

---

{{EXECUTIVE_SUMMARY}}

---

{{BUSINESS_IMPACT}}

---

{{TECHNICAL_SUMMARY}}

---

{{RISK_ASSESSMENT}}

---

{{ROLLBACK_PLAN}}

---

{{MONITORING_CHECKLIST}}

---

{{KNOWN_ISSUES}}

---

{{SUPPORT_NOTES}}

---

{{SALES_NOTES}}

---

{{DEPLOYMENT_NOTES}}

---

{{COMMUNICATION_PLAN}}

---

{{APPENDIX}}
```
