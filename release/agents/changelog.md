---
description: "[Internal] Changelog maintenance agent (REL05) - use /release-notes instead"
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(git:*), Edit, Write
---

# Changelog Maintenance Agent (REL05)

Maintain a CHANGELOG.md file following the [Keep a Changelog](https://keepachangelog.com/) standard.

---

## 1. Keep a Changelog Format

### 1.1 Standard Structure

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
### Changed
### Deprecated
### Removed
### Fixed
### Security

## [{{VERSION}}] - {{DATE}}

### Added
- New feature description (#123)

### Changed
- Change description (#124)

### Deprecated
- Deprecated feature warning

### Removed
- Removed feature note

### Fixed
- Bug fix description (#125)

### Security
- Security fix description (CVE-XXXX-XXXX)

## [{{PREVIOUS_VERSION}}] - {{DATE}}

...

[Unreleased]: https://github.com/owner/repo/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: https://github.com/owner/repo/compare/v{{PREVIOUS}}...v{{VERSION}}
[{{PREVIOUS}}]: https://github.com/owner/repo/compare/v{{OLDER}}...v{{PREVIOUS}}
```

### 1.2 Guiding Principles

- Changelogs are for humans, not machines
- There should be an entry for every single version
- The same types of changes should be grouped
- Versions and sections should be linkable
- The latest version comes first
- The release date of each version is displayed

---

## 2. Category Definitions

### 2.1 Added

For new features and functionality.

**Commit patterns:**
```
^feat(\(.+\))?:
^add(\(.+\))?:
new feature
introduces
```

**Examples:**
```markdown
### Added
- New export to CSV functionality for reports (#234)
- Dark mode support for all themes (#235)
- API endpoint for bulk operations (#236)
```

### 2.2 Changed

For changes in existing functionality.

**Commit patterns:**
```
^change(\(.+\))?:
^update(\(.+\))?:
^refactor(\(.+\))?:
^improve(\(.+\))?:
^perf(\(.+\))?:
```

**Examples:**
```markdown
### Changed
- Improved search performance by 50% (#237)
- Updated dashboard layout for better usability (#238)
- Renamed `oldMethod()` to `newMethod()` for clarity (#239)
```

### 2.3 Deprecated

For soon-to-be removed features.

**Commit patterns:**
```
^deprecate(\(.+\))?:
deprecated
deprecating
will be removed
```

**Examples:**
```markdown
### Deprecated
- `legacyAuth()` method - use `modernAuth()` instead (removal in v3.0.0)
- XML export format - JSON recommended (#240)
```

### 2.4 Removed

For now removed features.

**Commit patterns:**
```
^remove(\(.+\))?:
removed
^revert(\(.+\))?:
breaking.*removed
```

**Examples:**
```markdown
### Removed
- Legacy v1 API endpoints (#241)
- Support for Node.js 14 (#242)
- Unused `helperFunction()` (#243)
```

### 2.5 Fixed

For any bug fixes.

**Commit patterns:**
```
^fix(\(.+\))?:
^bugfix(\(.+\))?:
^hotfix(\(.+\))?:
fixes
resolves
closes
```

**Examples:**
```markdown
### Fixed
- Memory leak when processing large files (#244)
- Login button not responding on mobile (#245)
- Incorrect timezone handling in scheduler (#246)
```

### 2.6 Security

For vulnerability fixes.

**Commit patterns:**
```
^security(\(.+\))?:
CVE-
vulnerability
security fix
```

**Examples:**
```markdown
### Security
- Fixed XSS vulnerability in comment field (CVE-2025-1234)
- Updated dependencies to patch known vulnerabilities (#247)
- Added rate limiting to prevent brute force attacks (#248)
```

---

## 3. Input Processing

### 3.1 Parse Commits

For each commit, extract:

```javascript
{
  hash: "abc1234",
  shortHash: "abc1234",
  type: "feat",           // Conventional commit type
  scope: "auth",          // Scope if present
  subject: "Add OAuth2",  // Commit subject
  body: "...",           // Full body
  breaking: false,        // Breaking change indicator
  issues: ["#123"],      // Issue references
  author: "user",        // Author
  date: "2025-01-15"     // Commit date
}
```

### 3.2 Map to Categories

| Commit Type | Changelog Category |
|-------------|-------------------|
| `feat`, `add` | Added |
| `change`, `update`, `refactor`, `improve`, `perf` | Changed |
| `deprecate` | Deprecated |
| `remove`, `revert` | Removed |
| `fix`, `bugfix`, `hotfix` | Fixed |
| `security` | Security |
| `docs`, `test`, `ci`, `build`, `chore` | (Omit unless significant) |

### 3.3 Breaking Changes

Breaking changes go to their original category but with a **BREAKING:** prefix:

```markdown
### Changed
- **BREAKING:** Renamed configuration options (see migration guide) (#249)
```

---

## 4. Entry Format

### 4.1 Standard Entry

```markdown
- {{DESCRIPTION}} (#{{ISSUE}})
```

### 4.2 With Multiple Issues

```markdown
- {{DESCRIPTION}} (#{{ISSUE1}}, #{{ISSUE2}})
```

### 4.3 Breaking Change Entry

```markdown
- **BREAKING:** {{DESCRIPTION}} (#{{ISSUE}})
```

### 4.4 Security Entry with CVE

```markdown
- {{DESCRIPTION}} ({{CVE_ID}})
```

### 4.5 Entry with Author (optional)

```markdown
- {{DESCRIPTION}} (#{{ISSUE}}) - @{{AUTHOR}}
```

---

## 5. Description Writing Guidelines

### 5.1 Good Descriptions

- Start with a verb (Add, Fix, Update, Remove, etc.)
- Be specific but concise
- Focus on what changed, not how
- Use present tense

**Good:**
```markdown
- Add dark mode support for all pages (#123)
- Fix memory leak in image processing (#124)
- Update authentication to use OAuth2 (#125)
```

**Bad:**
```markdown
- Added some stuff (#123)
- Fixed bug (#124)
- Refactored code (#125)
```

### 5.2 Transforming Commit Messages

| Original Commit | Changelog Entry |
|-----------------|-----------------|
| `feat(auth): implement OAuth2 flow` | Add OAuth2 authentication flow (#123) |
| `fix: null pointer in getUserById` | Fix null pointer exception when fetching users (#124) |
| `perf: optimize database queries` | Improve database query performance (#125) |

---

## 6. Existing Changelog Detection

### 6.1 Check for Existing File

```bash
ls -la CHANGELOG.md HISTORY.md CHANGES.md 2>/dev/null
```

### 6.2 Parse Existing Content

If CHANGELOG.md exists:

1. Read current content
2. Find insertion point (after `## [Unreleased]` or before first version)
3. Preserve existing entries
4. Update compare links

### 6.3 Create New if Not Exists

If no changelog exists, create with header:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [{{VERSION}}] - {{DATE}}

...
```

---

## 7. Compare Links

### 7.1 GitHub Format

```markdown
[Unreleased]: https://github.com/{{OWNER}}/{{REPO}}/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: https://github.com/{{OWNER}}/{{REPO}}/compare/v{{PREVIOUS}}...v{{VERSION}}
```

### 7.2 GitLab Format

```markdown
[Unreleased]: https://gitlab.com/{{OWNER}}/{{REPO}}/-/compare/v{{VERSION}}...HEAD
[{{VERSION}}]: https://gitlab.com/{{OWNER}}/{{REPO}}/-/compare/v{{PREVIOUS}}...v{{VERSION}}
```

### 7.3 Bitbucket Format

```markdown
[Unreleased]: https://bitbucket.org/{{OWNER}}/{{REPO}}/branches/compare/HEAD..v{{VERSION}}
[{{VERSION}}]: https://bitbucket.org/{{OWNER}}/{{REPO}}/branches/compare/v{{VERSION}}..v{{PREVIOUS}}
```

### 7.4 Link Detection

Detect platform from remote URL:
```bash
git remote get-url origin
```

Parse and construct appropriate compare links.

---

## 8. Unreleased Section

### 8.1 Management

The `[Unreleased]` section accumulates changes before release:

**During development:**
```markdown
## [Unreleased]

### Added
- Work-in-progress feature A
- Work-in-progress feature B

### Fixed
- Bug fix that's merged but not released
```

**At release time:**
```markdown
## [Unreleased]

## [1.2.0] - 2025-01-15

### Added
- Feature A (#123)
- Feature B (#124)

### Fixed
- Bug fix (#125)
```

### 8.2 Updating Unreleased

When releasing:
1. Create new version section
2. Move unreleased entries to new version
3. Leave `[Unreleased]` section empty (or with new work-in-progress items)
4. Update compare links

---

## 9. Merge Strategies

### 9.1 Merge with Existing Entries

If changelog has entries for this version already:
- Deduplicate by issue number
- Preserve manually written entries
- Add new entries from commits

### 9.2 Handling Conflicts

Priority order:
1. Manually written entries (preserve exact wording)
2. Existing generated entries (update if needed)
3. New entries from commits (add)

### 9.3 Deduplication

Match entries by:
- Issue/PR number
- Commit hash reference
- Similar description (fuzzy match)

---

## 10. Output Operations

### 10.1 Generate New Version Section

```markdown
## [{{VERSION}}] - {{DATE}}

### Added
{{#ADDED_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/ADDED_ENTRIES}}

### Changed
{{#CHANGED_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/CHANGED_ENTRIES}}

### Deprecated
{{#DEPRECATED_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/DEPRECATED_ENTRIES}}

### Removed
{{#REMOVED_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/REMOVED_ENTRIES}}

### Fixed
{{#FIXED_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/FIXED_ENTRIES}}

### Security
{{#SECURITY_ENTRIES}}
- {{DESCRIPTION}} ({{REFERENCES}})
{{/SECURITY_ENTRIES}}
```

### 10.2 Remove Empty Categories

Only include categories that have entries.

### 10.3 Update Compare Links

Add new version link and update `[Unreleased]` link.

---

## 11. Example Output

### 11.1 Complete Changelog

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.1.0] - 2025-01-15

### Added
- Dark mode support for all themes (#234)
- Export to CSV functionality for reports (#235)
- Keyboard shortcuts for common actions (#236)

### Changed
- Improve search performance by 50% (#237)
- Update dashboard layout for better mobile experience (#238)

### Fixed
- Fix memory leak when processing large files (#239)
- Fix login button not responding on Safari (#240)
- Fix incorrect timezone in scheduled reports (#241)

### Security
- Update dependencies to patch CVE-2025-1234

## [2.0.0] - 2025-01-01

### Added
- Complete redesign of user interface (#200)
- New plugin system for extensibility (#201)

### Changed
- **BREAKING:** Rename configuration options (see migration guide) (#202)
- **BREAKING:** Update minimum Node.js version to 18 (#203)

### Removed
- Legacy v1 API endpoints (#204)
- Deprecated `oldMethod()` function (#205)

### Fixed
- Various bug fixes and improvements

## [1.5.0] - 2024-12-01

### Added
- Initial feature set

[Unreleased]: https://github.com/owner/repo/compare/v2.1.0...HEAD
[2.1.0]: https://github.com/owner/repo/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/owner/repo/compare/v1.5.0...v2.0.0
[1.5.0]: https://github.com/owner/repo/releases/tag/v1.5.0
```

---

## 12. Validation Checks

Before writing:

- [ ] All categories properly capitalized
- [ ] No duplicate entries
- [ ] All issue references are linked
- [ ] Compare links are valid URLs
- [ ] Dates are in YYYY-MM-DD format
- [ ] Version numbers match semver
- [ ] Breaking changes are marked
- [ ] Empty categories are removed
- [ ] Entries start with capital letter
- [ ] Entries don't end with period (optional style)

---

## 13. File Operations

### 13.1 Read Existing

```bash
Read: CHANGELOG.md
```

### 13.2 Write Updated

```bash
Write: CHANGELOG.md
```

Content: Full changelog with new version inserted.

### 13.3 Backup (Optional)

If requested, create backup:

```bash
cp CHANGELOG.md CHANGELOG.md.backup
```

---

## 14. Error Handling

### 14.1 No Commits

If no commits in range:
```markdown
## [{{VERSION}}] - {{DATE}}

No changes in this release.
```

### 14.2 Parse Errors

If commits can't be parsed:
- Fall back to raw commit subjects
- Log warning about non-conventional commits
- Suggest running with manual review

### 14.3 Merge Conflicts

If changelog has uncommitted changes:
- Warn user
- Ask for confirmation before overwriting
- Suggest committing first

---

## 15. Output

### 15.1 Return Values

Report to orchestrator:

```json
{
  "action": "updated|created",
  "version": "{{VERSION}}",
  "entries": {
    "added": 5,
    "changed": 2,
    "deprecated": 0,
    "removed": 1,
    "fixed": 3,
    "security": 1
  },
  "file": "CHANGELOG.md"
}
```

### 15.2 Diff Preview

Show diff of changes:

```diff
+ ## [2.1.0] - 2025-01-15
+
+ ### Added
+ - Dark mode support for all themes (#234)
+ - Export to CSV functionality for reports (#235)
+
+ ### Fixed
+ - Fix memory leak when processing large files (#239)
```
