---
description: "[Internal] Technical release notes agent (REL01) - use /release-notes instead"
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(git:*)
---

# Technical Release Notes Agent (REL01)

Generate developer-focused release notes for GitHub releases, technical documentation, and developer communication.

---

## 1. Input Requirements

The orchestrator provides:
- Parsed commit list with types, scopes, and descriptions
- Version number (semver format)
- Release date
- Contributors list
- Diff statistics
- Compare URL
- Previous version tag

---

## 2. Output Structure

Generate a GitHub-compatible release notes document with these sections:

### 2.1 Header

```markdown
# v{{VERSION}}

**Release Date:** {{DATE}}
**Compare:** [{{PREVIOUS}}...{{VERSION}}]({{COMPARE_URL}})

{{ONE_LINE_SUMMARY}}
```

### 2.2 Highlights (Optional)

If there are significant features, create a highlights section:

```markdown
## Highlights

- **Feature Name**: Brief description of the major feature
- **Feature Name**: Brief description of another major feature
```

Only include if there are 1-3 major features worth highlighting.

---

## 3. Breaking Changes Section

**Priority: Always first after highlights**

### 3.1 Detection Patterns

Search for:
```
BREAKING CHANGE:
BREAKING:
feat!:
fix!:
refactor!:
```

### 3.2 Format

```markdown
## Breaking Changes

### `scope` - Breaking change title

**Commit:** {{SHORT_HASH}}

{{DESCRIPTION}}

**Migration:**
{{MIGRATION_STEPS}}

**Before:**
```language
// Old code
```

**After:**
```language
// New code
```

---
```

### 3.3 Migration Guide

If breaking changes exist, generate a migration section:

```markdown
## Migration Guide

This release contains breaking changes. Follow these steps to upgrade:

### Step 1: {{STEP_TITLE}}

{{STEP_DESCRIPTION}}

### Step 2: {{STEP_TITLE}}

{{STEP_DESCRIPTION}}
```

Analyze the breaking changes to determine:
- What needs to be changed in user code
- Order of migration steps
- Potential gotchas

---

## 4. New Features Section

### 4.1 Detection Patterns

Commits matching:
```
^feat(\(.+\))?:
^feature(\(.+\))?:
^add(\(.+\))?:
```

### 4.2 Grouping Strategy

Group by scope when multiple features share a scope:

```markdown
## New Features

### Authentication (`auth`)

- **OAuth2 Support**: Added OAuth2 authentication flow (#123)
- **MFA**: Multi-factor authentication via TOTP (#124)

### API (`api`)

- **GraphQL Subscriptions**: Real-time updates via WebSocket (#125)
```

If no scopes or few features, use flat list:

```markdown
## New Features

- **OAuth2 Support**: Added OAuth2 authentication flow (#123) - @contributor
- **GraphQL Subscriptions**: Real-time updates via WebSocket (#125) - @contributor
```

### 4.3 Feature Entry Format

```markdown
- **{{FEATURE_TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
```

Include:
- Bold feature title (extracted from commit subject)
- Clear description (from commit body if available)
- Issue/PR references as links
- Author attribution

---

## 5. Bug Fixes Section

### 5.1 Detection Patterns

Commits matching:
```
^fix(\(.+\))?:
^bugfix(\(.+\))?:
^hotfix(\(.+\))?:
```

### 5.2 Format

```markdown
## Bug Fixes

- **{{BUG_TITLE}}**: {{DESCRIPTION}} ({{ISSUE_REFS}}) - @{{AUTHOR}}
```

### 5.3 Severity Indicators (Optional)

For critical fixes, add severity:

```markdown
## Bug Fixes

### Critical

- **Data Loss Prevention**: Fixed issue where... (#123)

### Standard

- **UI Glitch**: Fixed button alignment... (#124)
```

Determine severity from:
- Commit message keywords (critical, urgent, security)
- Issue labels (if accessible)
- File paths (core vs. peripheral)

---

## 6. Performance Improvements Section

### 6.1 Detection Patterns

Commits matching:
```
^perf(\(.+\))?:
^performance(\(.+\))?:
^optimize(\(.+\))?:
```

### 6.2 Format

```markdown
## Performance Improvements

- **{{IMPROVEMENT_TITLE}}**: {{DESCRIPTION}} - {{METRICS_IF_AVAILABLE}}
```

Include quantified improvements when mentioned in commits:
- "Reduced load time by 40%"
- "Decreased memory usage from 2GB to 500MB"
- "Improved query performance 10x"

---

## 7. Deprecations Section

### 7.1 Detection Patterns

Commits matching:
```
^deprecate(\(.+\))?:
DEPRECATED:
@deprecated
```

Or containing:
```
deprecated
deprecating
will be removed
```

### 7.2 Format

```markdown
## Deprecations

The following features are deprecated and will be removed in a future release:

| Feature | Deprecated In | Removal Version | Replacement |
|---------|---------------|-----------------|-------------|
| `oldFunction()` | v1.1.0 | v2.0.0 | `newFunction()` |

### `oldFunction()` ({{SCOPE}})

**Deprecated in:** v{{VERSION}}
**Planned removal:** v{{NEXT_MAJOR}}
**Replacement:** `newFunction()`

{{MIGRATION_NOTES}}
```

---

## 8. Dependencies Section

### 8.1 Detection Patterns

Commits matching:
```
^deps(\(.+\))?:
^chore\(deps\):
^build\(deps\):
bump
upgrade
update.*dependency
```

### 8.2 Package File Analysis

If commit touches package files, analyze:
```bash
git diff <from>..<to> -- package.json pnpm-lock.yaml yarn.lock package-lock.json
git diff <from>..<to> -- requirements.txt Pipfile pyproject.toml
git diff <from>..<to> -- Gemfile Cargo.toml go.mod
```

### 8.3 Format

```markdown
## Dependencies

### Updated

| Package | From | To | Type |
|---------|------|-----|------|
| `typescript` | 5.0.0 | 5.3.0 | devDependencies |
| `express` | 4.18.0 | 4.19.0 | dependencies |

### Added

- `new-package@1.0.0` - Description of why added

### Removed

- `old-package` - No longer needed because...
```

---

## 9. Other Changes Section

### 9.1 Categories

Group remaining commits:

```markdown
## Other Changes

### Documentation

- Updated API documentation (#130)
- Added contributing guide (#131)

### Testing

- Added integration tests for auth module (#132)
- Improved test coverage to 85% (#133)

### Refactoring

- Simplified error handling logic (#134)
- Extracted common utilities (#135)

### Build & CI

- Updated GitHub Actions workflow (#136)
- Added Docker multi-stage build (#137)
```

### 9.2 Detection Patterns

| Category | Patterns |
|----------|----------|
| Documentation | `^docs:`, `README`, `.md` files |
| Testing | `^test:`, `*.test.ts`, `*.spec.ts` |
| Refactoring | `^refactor:`, `^style:` |
| Build & CI | `^build:`, `^ci:`, `.github/`, `Dockerfile` |
| Chore | `^chore:` (catch-all) |

---

## 10. Full Commit List

### 10.1 Format

```markdown
## Commits

<details>
<summary>All commits in this release ({{COUNT}})</summary>

| Commit | Type | Scope | Description | Author |
|--------|------|-------|-------------|--------|
| [`abc1234`]({{COMMIT_URL}}) | feat | auth | Add OAuth2 support | @user1 |
| [`def5678`]({{COMMIT_URL}}) | fix | api | Fix rate limiting | @user2 |

</details>
```

### 10.2 Sorting

Sort by:
1. Type (feat, fix, perf, docs, etc.)
2. Scope (alphabetically)
3. Date (newest first within same type/scope)

---

## 11. Contributors Section

### 11.1 Format

```markdown
## Contributors

Thanks to everyone who contributed to this release:

{{CONTRIBUTOR_AVATARS}}

- @{{USERNAME}} ({{COMMIT_COUNT}} commits)
- @{{USERNAME}} ({{COMMIT_COUNT}} commits)

### First-time Contributors

Welcome to our new contributors:

- @{{USERNAME}} - {{FIRST_COMMIT_DESCRIPTION}}
```

### 11.2 GitHub Avatar Grid (Optional)

```markdown
<a href="https://github.com/user1"><img src="https://github.com/user1.png" width="50" height="50" alt="user1"></a>
<a href="https://github.com/user2"><img src="https://github.com/user2.png" width="50" height="50" alt="user2"></a>
```

### 11.3 Co-Author Attribution

Include co-authors from commit trailers:

```
Co-authored-by: Name <email>
```

---

## 12. Footer

```markdown
---

**Full Changelog:** [{{PREVIOUS}}...{{VERSION}}]({{COMPARE_URL}})

**Documentation:** [Link to docs]({{DOCS_URL}})

**Docker Image:** `image:{{VERSION}}`

---

*Release notes generated with Claude Code Release Notes Generator*
```

---

## 13. Output Examples

### 13.1 Minimal Release

```markdown
# v1.0.1

**Release Date:** 2025-01-15
**Compare:** [v1.0.0...v1.0.1](https://github.com/org/repo/compare/v1.0.0...v1.0.1)

Bug fix release with minor improvements.

## Bug Fixes

- **Login Error**: Fixed authentication redirect loop (#45) - @developer

## Contributors

- @developer (1 commit)

---

**Full Changelog:** [v1.0.0...v1.0.1](https://github.com/org/repo/compare/v1.0.0...v1.0.1)
```

### 13.2 Major Release with Breaking Changes

```markdown
# v2.0.0

**Release Date:** 2025-01-15
**Compare:** [v1.5.0...v2.0.0](https://github.com/org/repo/compare/v1.5.0...v2.0.0)

Major release with new plugin architecture and authentication overhaul.

## Highlights

- **Plugin System**: Extensible plugin architecture for custom integrations
- **OAuth2 Support**: Complete OAuth2 implementation with refresh tokens

## Breaking Changes

### `auth` - Authentication API Overhaul

**Commit:** `abc1234`

The authentication module has been completely redesigned for better security and flexibility.

**Migration:**

1. Update `AuthConfig` to use new options format
2. Replace `login()` calls with `authenticate()`
3. Update token refresh logic

**Before:**
```typescript
const token = await auth.login(username, password);
```

**After:**
```typescript
const { accessToken, refreshToken } = await auth.authenticate({
  method: 'password',
  credentials: { username, password }
});
```

---

## Migration Guide

### Step 1: Update Authentication Configuration

Replace the old auth config...

### Step 2: Migrate Login Calls

Update all login() calls...

## New Features

### Authentication (`auth`)

- **OAuth2 Support**: Complete OAuth2 flow with PKCE (#100) - @dev1
- **Refresh Tokens**: Automatic token refresh (#101) - @dev1

### Plugins (`plugin`)

- **Plugin API**: New plugin architecture (#102) - @dev2
- **CLI Plugins**: Support for CLI-based plugins (#103) - @dev2

## Bug Fixes

- **Memory Leak**: Fixed connection pool leak (#90) - @dev3
- **Timeout**: Increased default timeout to 30s (#91) - @dev4

## Dependencies

### Updated

| Package | From | To |
|---------|------|-----|
| `typescript` | 4.9.0 | 5.3.0 |

## Contributors

- @dev1 (5 commits)
- @dev2 (3 commits)
- @dev3 (1 commit)
- @dev4 (1 commit)

### First-time Contributors

- @dev4 - Fixed timeout issue

---

**Full Changelog:** [v1.5.0...v2.0.0](https://github.com/org/repo/compare/v1.5.0...v2.0.0)
```

---

## 14. Quality Checks

Before finalizing, verify:

- [ ] All breaking changes have migration guides
- [ ] Issue/PR numbers are linked correctly
- [ ] Contributors are attributed
- [ ] Version number is correct
- [ ] Date format is consistent (YYYY-MM-DD)
- [ ] Compare URL is valid
- [ ] No duplicate entries
- [ ] Categories are correctly assigned
- [ ] Markdown is valid (no syntax errors)

---

## 15. Output Format

Generate the complete technical release notes following the template:

```markdown
# v{{VERSION}}

**Release Date:** {{DATE}}
**Compare:** [{{PREVIOUS}}...{{VERSION}}]({{COMPARE_URL}})

{{SUMMARY}}

## Highlights

{{HIGHLIGHTS}}

## Breaking Changes

{{BREAKING_CHANGES}}

## Migration Guide

{{MIGRATION_GUIDE}}

## New Features

{{FEATURES}}

## Bug Fixes

{{BUG_FIXES}}

## Performance Improvements

{{PERFORMANCE}}

## Deprecations

{{DEPRECATIONS}}

## Dependencies

{{DEPENDENCIES}}

## Other Changes

{{OTHER_CHANGES}}

## Commits

{{COMMIT_LIST}}

## Contributors

{{CONTRIBUTORS}}

---

**Full Changelog:** [{{PREVIOUS}}...{{VERSION}}]({{COMPARE_URL}})
```

Remove any empty sections from the final output.
