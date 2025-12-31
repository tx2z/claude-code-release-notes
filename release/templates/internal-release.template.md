---
description: "[Internal] Internal release notes template - use /release-notes instead"
disable-model-invocation: true
---

# Internal Release Notes Template

Template for team and stakeholder communication.

---

## Template

```markdown
# Internal Release Notes - v{{VERSION}}

**Release Date:** {{DATE}}
**Release Manager:** {{RELEASE_MANAGER}}
**Status:** {{STATUS}}

---

## Executive Summary

This release includes {{FEATURE_COUNT}} new features, {{FIX_COUNT}} bug fixes, and {{IMPROVEMENT_COUNT}} improvements.

**Key Changes:**
{{#KEY_CHANGES}}
- {{CHANGE}}
{{/KEY_CHANGES}}

**Risk Level:** {{RISK_LEVEL}}
**Rollback Plan:** {{ROLLBACK_STATUS}}

---

## Business Impact

### Revenue Impact

| Change | Expected Impact | Confidence |
|--------|-----------------|------------|
{{#REVENUE_IMPACTS}}
| {{CHANGE}} | {{IMPACT}} | {{CONFIDENCE}} |
{{/REVENUE_IMPACTS}}

### User Experience Impact

- **Positive:** {{POSITIVE_UX}}
- **Neutral:** {{NEUTRAL_UX}}
- **Risk:** {{RISK_UX}}

### Customer Requests Addressed

| Request | Ticket | Customer(s) |
|---------|--------|-------------|
{{#CUSTOMER_REQUESTS}}
| {{REQUEST}} | {{TICKET}} | {{CUSTOMERS}} |
{{/CUSTOMER_REQUESTS}}

---

## Technical Summary

### Architecture Changes

{{#ARCHITECTURE_CHANGES}}
- {{CHANGE}}
{{/ARCHITECTURE_CHANGES}}

### Database Changes

| Type | Table/Collection | Migration Required |
|------|------------------|-------------------|
{{#DB_CHANGES}}
| {{TYPE}} | {{TABLE}} | {{MIGRATION}} |
{{/DB_CHANGES}}

{{#MIGRATION_NOTES}}
**Migration Notes:**
{{MIGRATION_NOTES}}
{{/MIGRATION_NOTES}}

### API Changes

| Endpoint | Change | Breaking |
|----------|--------|----------|
{{#API_CHANGES}}
| `{{ENDPOINT}}` | {{CHANGE}} | {{BREAKING}} |
{{/API_CHANGES}}

### Dependencies

| Package | From | To | Risk |
|---------|------|-----|------|
{{#DEPENDENCIES}}
| `{{PACKAGE}}` | {{FROM}} | {{TO}} | {{RISK}} |
{{/DEPENDENCIES}}

---

## Risk Assessment

**Overall Risk Level:** {{OVERALL_RISK}}

### Risk Matrix

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
{{#RISKS}}
| {{RISK}} | {{LIKELIHOOD}} | {{IMPACT}} | {{MITIGATION}} |
{{/RISKS}}

### Breaking Changes

| Change | Affected Users | Communication |
|--------|---------------|---------------|
{{#BREAKING_CHANGES}}
| {{CHANGE}} | {{AFFECTED}} | {{COMMUNICATION}} |
{{/BREAKING_CHANGES}}

### Rollback Considerations

**Can this release be rolled back?** {{ROLLBACK_POSSIBLE}}

**Rollback blockers:**
{{#ROLLBACK_BLOCKERS}}
- {{BLOCKER}}
{{/ROLLBACK_BLOCKERS}}

---

## Rollback Plan

### Quick Rollback (< 5 minutes)

```bash
{{QUICK_ROLLBACK_COMMANDS}}
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
6. **Communicate** - Update status page

### Post-Rollback Actions

{{#POST_ROLLBACK}}
- {{ACTION}}
{{/POST_ROLLBACK}}

---

## Monitoring Checklist

### Pre-Deployment

{{#PRE_DEPLOY_CHECKS}}
- [ ] {{CHECK}}
{{/PRE_DEPLOY_CHECKS}}

### During Deployment

| Metric | Expected | Alert Threshold |
|--------|----------|-----------------|
{{#METRICS}}
| {{METRIC}} | {{EXPECTED}} | {{THRESHOLD}} |
{{/METRICS}}

### Post-Deployment (First 24 Hours)

{{#POST_DEPLOY_CHECKS}}
- [ ] {{CHECK}}
{{/POST_DEPLOY_CHECKS}}

### Key Dashboards

{{#DASHBOARDS}}
- [{{NAME}}]({{URL}})
{{/DASHBOARDS}}

---

## Known Issues

### Existing Issues

| Issue | Severity | Workaround | ETA |
|-------|----------|------------|-----|
{{#EXISTING_ISSUES}}
| {{ISSUE}} | {{SEVERITY}} | {{WORKAROUND}} | {{ETA}} |
{{/EXISTING_ISSUES}}

### New Known Issues

| Issue | Severity | Impact | Ticket |
|-------|----------|--------|--------|
{{#NEW_ISSUES}}
| {{ISSUE}} | {{SEVERITY}} | {{IMPACT}} | {{TICKET}} |
{{/NEW_ISSUES}}

---

## Support Team Notes

### What's Changing for Users

| Change | Impact | How to Explain |
|--------|--------|----------------|
{{#USER_CHANGES}}
| {{CHANGE}} | {{IMPACT}} | {{EXPLANATION}} |
{{/USER_CHANGES}}

### Common Questions Expected

{{#FAQ}}
**Q: {{QUESTION}}**
A: {{ANSWER}}

{{/FAQ}}

### Troubleshooting

{{#TROUBLESHOOTING}}
#### {{FEATURE}}

**Symptoms:** {{SYMPTOMS}}
**Cause:** {{CAUSE}}
**Solution:** {{SOLUTION}}

{{/TROUBLESHOOTING}}

### Escalation Criteria

{{#ESCALATION}}
- {{CRITERIA}}
{{/ESCALATION}}

---

## Sales Enablement

### New Talking Points

{{#TALKING_POINTS}}
#### {{FEATURE}}

**Elevator Pitch:** {{PITCH}}

**Key Benefits:**
{{#BENEFITS}}
- {{BENEFIT}}
{{/BENEFITS}}

**Target Customers:** {{TARGET}}

{{/TALKING_POINTS}}

### Pricing Impact

| Feature | Plan Availability | Upsell Opportunity |
|---------|------------------|-------------------|
{{#PRICING}}
| {{FEATURE}} | {{PLANS}} | {{UPSELL}} |
{{/PRICING}}

---

## Deployment Notes

### Prerequisites

{{#PREREQUISITES}}
- [ ] {{PREREQUISITE}}
{{/PREREQUISITES}}

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
{{#ENV_VARS}}
| `{{VAR}}` | {{REQUIRED}} | {{DEFAULT}} | {{DESCRIPTION}} |
{{/ENV_VARS}}

### Feature Flags

| Flag | Default | Description |
|------|---------|-------------|
{{#FEATURE_FLAGS}}
| `{{FLAG}}` | {{DEFAULT}} | {{DESCRIPTION}} |
{{/FEATURE_FLAGS}}

### Deployment Order

{{#DEPLOY_STEPS}}
1. {{STEP}}
{{/DEPLOY_STEPS}}

### Rollout Plan

| Phase | Traffic | Duration | Proceed If |
|-------|---------|----------|------------|
{{#ROLLOUT}}
| {{PHASE}} | {{TRAFFIC}} | {{DURATION}} | {{CRITERIA}} |
{{/ROLLOUT}}

---

## Communication Plan

### Internal

| Audience | Channel | Timing | Owner |
|----------|---------|--------|-------|
{{#INTERNAL_COMMS}}
| {{AUDIENCE}} | {{CHANNEL}} | {{TIMING}} | {{OWNER}} |
{{/INTERNAL_COMMS}}

### External

| Audience | Channel | Timing | Content |
|----------|---------|--------|---------|
{{#EXTERNAL_COMMS}}
| {{AUDIENCE}} | {{CHANNEL}} | {{TIMING}} | {{CONTENT}} |
{{/EXTERNAL_COMMS}}

---

## Appendix

### Full Commit List

| Hash | Author | Type | Description |
|------|--------|------|-------------|
{{#COMMITS}}
| {{HASH}} | {{AUTHOR}} | {{TYPE}} | {{DESCRIPTION}} |
{{/COMMITS}}

### Files Changed

**Total:** {{FILES_CHANGED}} files, +{{INSERTIONS}} -{{DELETIONS}}

| Directory | Files | Changes |
|-----------|-------|---------|
{{#FILE_CHANGES}}
| {{DIRECTORY}} | {{COUNT}} | +{{INS}} -{{DEL}} |
{{/FILE_CHANGES}}

---

*Generated: {{GENERATED_DATE}}*
*By: Claude Code Release Notes Generator*
```

---

## Variable Reference

### Header Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `{{VERSION}}` | Release version | `2.1.0` |
| `{{DATE}}` | Release date | `2025-01-15` |
| `{{RELEASE_MANAGER}}` | Person responsible | `@manager` |
| `{{STATUS}}` | Release status | `Ready`, `Pending`, `Blocked` |

### Summary Variables

| Variable | Description |
|----------|-------------|
| `{{FEATURE_COUNT}}` | Number of features |
| `{{FIX_COUNT}}` | Number of fixes |
| `{{IMPROVEMENT_COUNT}}` | Number of improvements |
| `{{RISK_LEVEL}}` | `Low`, `Medium`, `High`, `Critical` |
| `{{ROLLBACK_STATUS}}` | `Available`, `Tested`, `N/A` |

### Risk Variables

| Variable | Description |
|----------|-------------|
| `{{OVERALL_RISK}}` | Overall risk assessment |
| `{{ROLLBACK_POSSIBLE}}` | `Yes`, `Partial`, `No` |

### Deployment Variables

| Variable | Description |
|----------|-------------|
| `{{QUICK_ROLLBACK_COMMANDS}}` | Commands for quick rollback |
| `{{APP_ROLLBACK_COMMANDS}}` | Application rollback commands |
| `{{DB_ROLLBACK_COMMANDS}}` | Database rollback commands |

---

## Section Guidelines

### When to Include Sections

| Section | Include If... |
|---------|--------------|
| Business Impact | Major feature or customer-facing change |
| Architecture Changes | Significant technical changes |
| Database Changes | Any schema modifications |
| Risk Assessment | Always |
| Rollback Plan | Always (even if N/A) |
| Known Issues | Any exist |
| Support Notes | User-facing changes |
| Sales Enablement | New features for positioning |
| Deployment Notes | Non-standard deployment |

### Risk Level Guidelines

| Level | Criteria |
|-------|----------|
| **Low** | No breaking changes, tested thoroughly, easy rollback |
| **Medium** | Minor breaking changes, some risk, rollback available |
| **High** | Major changes, database migrations, limited rollback |
| **Critical** | High user impact, difficult rollback, security-related |
