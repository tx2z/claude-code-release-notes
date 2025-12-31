---
description: "[Internal] CHANGELOG.md template - use /release-notes instead"
disable-model-invocation: true
---

# CHANGELOG Template

Template following [Keep a Changelog](https://keepachangelog.com/) format.

---

## Full Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

{{#UNRELEASED_ADDED}}
### Added
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_ADDED}}

{{#UNRELEASED_CHANGED}}
### Changed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_CHANGED}}

{{#UNRELEASED_DEPRECATED}}
### Deprecated
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_DEPRECATED}}

{{#UNRELEASED_REMOVED}}
### Removed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_REMOVED}}

{{#UNRELEASED_FIXED}}
### Fixed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_FIXED}}

{{#UNRELEASED_SECURITY}}
### Security
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/UNRELEASED_SECURITY}}

## [{{VERSION}}] - {{DATE}}

{{#ADDED}}
### Added
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/ADDED}}

{{#CHANGED}}
### Changed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/CHANGED}}

{{#DEPRECATED}}
### Deprecated
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/DEPRECATED}}

{{#REMOVED}}
### Removed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/REMOVED}}

{{#FIXED}}
### Fixed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/FIXED}}

{{#SECURITY}}
### Security
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/SECURITY}}

{{#PREVIOUS_VERSIONS}}
## [{{VERSION}}] - {{DATE}}

{{CONTENT}}

{{/PREVIOUS_VERSIONS}}

[Unreleased]: {{REPO_URL}}/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: {{REPO_URL}}/compare/v{{PREVIOUS_VERSION}}...v{{VERSION}}
{{#OLDER_LINKS}}
[{{VERSION}}]: {{REPO_URL}}/compare/v{{PREVIOUS}}...v{{VERSION}}
{{/OLDER_LINKS}}
[{{OLDEST_VERSION}}]: {{REPO_URL}}/releases/tag/v{{OLDEST_VERSION}}
```

---

## Version Section Template

```markdown
## [{{VERSION}}] - {{DATE}}

{{#ADDED}}
### Added
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/ADDED}}

{{#CHANGED}}
### Changed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/CHANGED}}

{{#DEPRECATED}}
### Deprecated
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/DEPRECATED}}

{{#REMOVED}}
### Removed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/REMOVED}}

{{#FIXED}}
### Fixed
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/FIXED}}

{{#SECURITY}}
### Security
{{#ITEMS}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ITEMS}}
{{/SECURITY}}
```

---

## Entry Template

### Standard Entry

```markdown
- {{DESCRIPTION}} ({{REFERENCES}})
```

Examples:
```markdown
- Add dark mode support for all themes (#234)
- Fix memory leak in image processor (#235)
- Update authentication to use OAuth2 (#236)
```

### Breaking Change Entry

```markdown
- **BREAKING:** {{DESCRIPTION}} ({{REFERENCES}})
```

Examples:
```markdown
- **BREAKING:** Rename configuration file from `.apprc` to `app.config.js` (#237)
- **BREAKING:** Remove deprecated `legacyAuth()` method (#238)
```

### Security Entry with CVE

```markdown
- {{DESCRIPTION}} ({{CVE_ID}})
```

Examples:
```markdown
- Fix XSS vulnerability in comment rendering (CVE-2025-1234)
- Update lodash to patch prototype pollution (CVE-2025-5678)
```

### Entry with Author

```markdown
- {{DESCRIPTION}} ({{REFERENCES}}) - @{{AUTHOR}}
```

Examples:
```markdown
- Add Spanish language support (#239) - @contributor
```

---

## Compare Links Template

### GitHub

```markdown
[Unreleased]: https://github.com/{{OWNER}}/{{REPO}}/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: https://github.com/{{OWNER}}/{{REPO}}/compare/v{{PREVIOUS}}...v{{VERSION}}
```

### GitLab

```markdown
[Unreleased]: https://gitlab.com/{{OWNER}}/{{REPO}}/-/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: https://gitlab.com/{{OWNER}}/{{REPO}}/-/compare/v{{PREVIOUS}}...v{{VERSION}}
```

### Bitbucket

```markdown
[Unreleased]: https://bitbucket.org/{{OWNER}}/{{REPO}}/branches/compare/HEAD..v{{VERSION}}
[{{VERSION}}]: https://bitbucket.org/{{OWNER}}/{{REPO}}/branches/compare/v{{VERSION}}..v{{PREVIOUS}}
```

---

## Variable Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `{{VERSION}}` | Release version (semver) | `2.1.0` |
| `{{DATE}}` | Release date (YYYY-MM-DD) | `2025-01-15` |
| `{{PREVIOUS_VERSION}}` | Previous version | `2.0.0` |
| `{{DESCRIPTION}}` | Change description | `Add dark mode support` |
| `{{REFERENCES}}` | Issue/PR references | `#123`, `#123, #124` |
| `{{CVE_ID}}` | CVE identifier | `CVE-2025-1234` |
| `{{AUTHOR}}` | Contributor username | `@developer` |
| `{{REPO_URL}}` | Repository base URL | `https://github.com/org/repo` |
| `{{OWNER}}` | Repository owner | `organization` |
| `{{REPO}}` | Repository name | `project` |

---

## Category Guidelines

### Added

New features that users can use.

**Include:**
- New functionality
- New API endpoints
- New configuration options
- New integrations

**Commit types:** `feat`, `add`, `feature`

### Changed

Changes to existing functionality.

**Include:**
- Modified behavior
- Updated dependencies
- Performance improvements
- Refactored APIs

**Commit types:** `change`, `update`, `refactor`, `improve`, `perf`

### Deprecated

Features that will be removed in future versions.

**Include:**
- Deprecated functions
- Deprecated APIs
- Deprecated configuration

**Commit types:** `deprecate`

### Removed

Features that have been removed.

**Include:**
- Deleted functionality
- Removed deprecated features
- Dropped support

**Commit types:** `remove`, `delete`

### Fixed

Bug fixes.

**Include:**
- Bug fixes
- Corrections
- Error handling improvements

**Commit types:** `fix`, `bugfix`, `hotfix`

### Security

Security fixes and improvements.

**Include:**
- Vulnerability patches
- Security enhancements
- CVE fixes

**Commit types:** `security`

---

## Formatting Rules

### Description Writing

1. **Start with a verb** - Add, Fix, Update, Remove, etc.
2. **Use present tense** - "Add feature" not "Added feature"
3. **Be specific** - Describe what changed, not how
4. **Keep it brief** - One line, under 80 characters ideally
5. **Capitalize first letter** - "Add feature" not "add feature"
6. **No trailing period** - "Add feature" not "Add feature."

### Reference Formatting

- Single issue: `(#123)`
- Multiple issues: `(#123, #124)`
- CVE: `(CVE-2025-1234)`
- External link: `([link text](url))`

### Breaking Change Formatting

- Always prefix with `**BREAKING:**`
- Place in the appropriate category (usually Changed or Removed)
- Consider adding migration notes

---

## Example Changelog

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Work in progress feature X

## [2.1.0] - 2025-01-15

### Added
- Add dark mode support for all themes (#234)
- Add export to CSV functionality (#235)
- Add keyboard shortcuts for common actions (#236)

### Changed
- Improve search performance by 50% (#237)
- Update dashboard layout for mobile (#238)

### Fixed
- Fix memory leak when processing large files (#239)
- Fix login button not responding on Safari (#240)
- Fix timezone display in scheduled reports (#241)

### Security
- Update dependencies to patch CVE-2025-1234

## [2.0.0] - 2025-01-01

### Added
- Add new plugin architecture (#200)
- Add GraphQL API (#201)

### Changed
- **BREAKING:** Rename config file to `app.config.js` (#202)
- **BREAKING:** Update minimum Node.js to v18 (#203)

### Removed
- **BREAKING:** Remove legacy v1 API endpoints (#204)
- Remove deprecated `oldMethod()` function (#205)

## [1.5.0] - 2024-12-01

### Added
- Initial public release

[Unreleased]: https://github.com/org/repo/compare/v2.1.0...HEAD
[2.1.0]: https://github.com/org/repo/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/org/repo/compare/v1.5.0...v2.0.0
[1.5.0]: https://github.com/org/repo/releases/tag/v1.5.0
```

---

## Empty Version Template

For releases with no user-facing changes:

```markdown
## [{{VERSION}}] - {{DATE}}

No user-facing changes in this release. Internal improvements only.
```

Or with details:

```markdown
## [{{VERSION}}] - {{DATE}}

### Changed
- Internal refactoring and maintenance
- Updated development dependencies
```

---

## Initial Changelog Template

For new projects:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - {{DATE}}

### Added
- Initial release
- {{INITIAL_FEATURES}}

[Unreleased]: {{REPO_URL}}/compare/v0.1.0...HEAD
[0.1.0]: {{REPO_URL}}/releases/tag/v0.1.0
```
