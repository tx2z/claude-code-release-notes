---
description: "[Internal] Technical release notes template - use /release-notes instead"
disable-model-invocation: true
---

# Technical Release Notes Template

Template for GitHub-style technical release notes.

---

## Template

```markdown
# v{{VERSION}}

**Release Date:** {{DATE}}
**Compare:** [{{PREVIOUS_VERSION}}...{{VERSION}}]({{COMPARE_URL}})

{{SUMMARY}}

---

{{#HIGHLIGHTS}}
## Highlights

{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}}
{{/ITEMS}}

---
{{/HIGHLIGHTS}}

{{#BREAKING_CHANGES}}
## Breaking Changes

{{#ITEMS}}
### `{{SCOPE}}` - {{TITLE}}

**Commit:** [`{{SHORT_HASH}}`]({{COMMIT_URL}})

{{DESCRIPTION}}

{{#MIGRATION}}
**Migration:**

{{STEPS}}

**Before:**
```{{LANGUAGE}}
{{BEFORE_CODE}}
```

**After:**
```{{LANGUAGE}}
{{AFTER_CODE}}
```
{{/MIGRATION}}

---
{{/ITEMS}}
{{/BREAKING_CHANGES}}

{{#MIGRATION_GUIDE}}
## Migration Guide

{{CONTENT}}

---
{{/MIGRATION_GUIDE}}

{{#FEATURES}}
## New Features

{{#GROUPED_BY_SCOPE}}
### {{SCOPE_NAME}} (`{{SCOPE}}`)

{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
{{/ITEMS}}

{{/GROUPED_BY_SCOPE}}

{{#UNGROUPED}}
{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
{{/ITEMS}}
{{/UNGROUPED}}

---
{{/FEATURES}}

{{#BUG_FIXES}}
## Bug Fixes

{{#CRITICAL}}
### Critical

{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
{{/ITEMS}}

{{/CRITICAL}}

{{#STANDARD}}
{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
{{/ITEMS}}
{{/STANDARD}}

---
{{/BUG_FIXES}}

{{#PERFORMANCE}}
## Performance Improvements

{{#ITEMS}}
- **{{TITLE}}**: {{DESCRIPTION}} {{#METRICS}}- {{METRICS}}{{/METRICS}}
{{/ITEMS}}

---
{{/PERFORMANCE}}

{{#DEPRECATIONS}}
## Deprecations

The following features are deprecated and will be removed in a future release:

| Feature | Deprecated In | Removal Version | Replacement |
|---------|---------------|-----------------|-------------|
{{#ITEMS}}
| `{{FEATURE}}` | {{DEPRECATED_VERSION}} | {{REMOVAL_VERSION}} | {{REPLACEMENT}} |
{{/ITEMS}}

{{#DETAILED}}
### `{{FEATURE}}` ({{SCOPE}})

**Deprecated in:** v{{VERSION}}
**Planned removal:** v{{REMOVAL_VERSION}}
**Replacement:** `{{REPLACEMENT}}`

{{MIGRATION_NOTES}}

{{/DETAILED}}

---
{{/DEPRECATIONS}}

{{#DEPENDENCIES}}
## Dependencies

{{#UPDATED}}
### Updated

| Package | From | To | Type |
|---------|------|-----|------|
{{#ITEMS}}
| `{{PACKAGE}}` | {{FROM_VERSION}} | {{TO_VERSION}} | {{DEP_TYPE}} |
{{/ITEMS}}
{{/UPDATED}}

{{#ADDED}}
### Added

{{#ITEMS}}
- `{{PACKAGE}}@{{VERSION}}` - {{DESCRIPTION}}
{{/ITEMS}}
{{/ADDED}}

{{#REMOVED}}
### Removed

{{#ITEMS}}
- `{{PACKAGE}}` - {{REASON}}
{{/ITEMS}}
{{/REMOVED}}

---
{{/DEPENDENCIES}}

{{#OTHER_CHANGES}}
## Other Changes

{{#DOCUMENTATION}}
### Documentation

{{#ITEMS}}
- {{DESCRIPTION}} ({{ISSUE_REFS}})
{{/ITEMS}}

{{/DOCUMENTATION}}

{{#TESTING}}
### Testing

{{#ITEMS}}
- {{DESCRIPTION}} ({{ISSUE_REFS}})
{{/ITEMS}}

{{/TESTING}}

{{#REFACTORING}}
### Refactoring

{{#ITEMS}}
- {{DESCRIPTION}} ({{ISSUE_REFS}})
{{/ITEMS}}

{{/REFACTORING}}

{{#BUILD_CI}}
### Build & CI

{{#ITEMS}}
- {{DESCRIPTION}} ({{ISSUE_REFS}})
{{/ITEMS}}

{{/BUILD_CI}}

{{#CHORE}}
### Maintenance

{{#ITEMS}}
- {{DESCRIPTION}} ({{ISSUE_REFS}})
{{/ITEMS}}

{{/CHORE}}

---
{{/OTHER_CHANGES}}

{{#COMMITS}}
## Commits

<details>
<summary>All commits in this release ({{COUNT}})</summary>

| Commit | Type | Scope | Description | Author |
|--------|------|-------|-------------|--------|
{{#ITEMS}}
| [`{{SHORT_HASH}}`]({{COMMIT_URL}}) | {{TYPE}} | {{SCOPE}} | {{SUBJECT}} | @{{AUTHOR}} |
{{/ITEMS}}

</details>

---
{{/COMMITS}}

{{#CONTRIBUTORS}}
## Contributors

Thanks to everyone who contributed to this release!

{{#AVATARS}}
<a href="https://github.com/{{USERNAME}}"><img src="https://github.com/{{USERNAME}}.png" width="50" height="50" alt="{{USERNAME}}"></a>
{{/AVATARS}}

{{#LIST}}
- @{{USERNAME}} ({{COMMIT_COUNT}} commits)
{{/LIST}}

{{#FIRST_TIME}}
### First-time Contributors

Welcome to our new contributors!

{{#ITEMS}}
- @{{USERNAME}} - {{FIRST_COMMIT_DESCRIPTION}}
{{/ITEMS}}
{{/FIRST_TIME}}

---
{{/CONTRIBUTORS}}

**Full Changelog:** [{{PREVIOUS_VERSION}}...{{VERSION}}]({{COMPARE_URL}})

{{#DOCS_URL}}
**Documentation:** [{{DOCS_TITLE}}]({{DOCS_URL}})
{{/DOCS_URL}}

{{#DOCKER_IMAGE}}
**Docker Image:** `{{DOCKER_IMAGE}}:{{VERSION}}`
{{/DOCKER_IMAGE}}

---

*Release notes generated with Claude Code Release Notes Generator*
```

---

## Variable Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `{{VERSION}}` | Release version | `1.2.0` |
| `{{DATE}}` | Release date (YYYY-MM-DD) | `2025-01-15` |
| `{{PREVIOUS_VERSION}}` | Previous release version | `1.1.0` |
| `{{COMPARE_URL}}` | URL to compare changes | GitHub compare URL |
| `{{SUMMARY}}` | One-line release summary | "Bug fix release..." |
| `{{SHORT_HASH}}` | Short commit hash | `abc1234` |
| `{{COMMIT_URL}}` | URL to commit | GitHub commit URL |
| `{{SCOPE}}` | Commit scope | `auth`, `api` |
| `{{TITLE}}` | Feature/fix title | "OAuth2 Support" |
| `{{DESCRIPTION}}` | Detailed description | Full description |
| `{{ISSUE_REFS}}` | Issue/PR references | `#123, #124` |
| `{{AUTHOR}}` | Commit author username | `developer` |
| `{{LANGUAGE}}` | Code language for snippets | `typescript` |
| `{{METRICS}}` | Performance metrics | "50% faster" |
| `{{PACKAGE}}` | Dependency package name | `express` |
| `{{FROM_VERSION}}` | Previous dep version | `4.18.0` |
| `{{TO_VERSION}}` | New dep version | `4.19.0` |
| `{{DEP_TYPE}}` | Dependency type | `dependencies` |
| `{{USERNAME}}` | GitHub username | `octocat` |
| `{{COMMIT_COUNT}}` | Number of commits | `5` |

---

## Conditional Sections

Sections wrapped in `{{#SECTION}}...{{/SECTION}}` are only rendered if content exists:

- `{{#HIGHLIGHTS}}` - Major features worth highlighting
- `{{#BREAKING_CHANGES}}` - Breaking changes present
- `{{#MIGRATION_GUIDE}}` - Migration steps needed
- `{{#FEATURES}}` - New features added
- `{{#BUG_FIXES}}` - Bug fixes included
- `{{#PERFORMANCE}}` - Performance improvements
- `{{#DEPRECATIONS}}` - Deprecation notices
- `{{#DEPENDENCIES}}` - Dependency changes
- `{{#OTHER_CHANGES}}` - Docs, tests, refactoring, etc.
- `{{#COMMITS}}` - Full commit list
- `{{#CONTRIBUTORS}}` - Contributor listing
