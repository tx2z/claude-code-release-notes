# Claude Code Release Notes Generator

A comprehensive multi-format release notes generation command for [Claude Code](https://claude.ai/claude-code) that analyzes Git commits and produces release notes for different audiences.

## Features

- **Technical Release Notes** - GitHub releases with conventional commit grouping
- **Marketing Release Notes** - App store descriptions with character limits
- **Internal Release Notes** - Team communication with business impact
- **Security Release Notes** - CVE disclosures and vulnerability documentation
- **Changelog Maintenance** - Keep a Changelog format automation

## Requirements

- [Claude Code CLI](https://claude.ai/claude-code) installed and configured
- A Git repository with commit history

## Installation

1. Clone or download this repository
2. Copy the folders to your project's `.claude/` directory:

```bash
# From your project root
cp -r path/to/claude-code-release-notes/commands .claude/
cp -r path/to/claude-code-release-notes/release .claude/
```

Your project structure should look like:
```
your-project/
├── .claude/
│   ├── commands/
│   │   └── release-notes.md
│   └── release/
│       ├── agents/
│       │   ├── technical-notes.md
│       │   ├── marketing-notes.md
│       │   ├── internal-notes.md
│       │   ├── security-notes.md
│       │   └── changelog.md
│       └── templates/
│           ├── technical-release.template.md
│           ├── marketing-release.template.md
│           ├── internal-release.template.md
│           └── CHANGELOG.template.md
├── src/
└── ...
```

3. (Optional) Add `release-notes/` to your `.gitignore`:

```bash
echo "release-notes/" >> .gitignore
```

## Optional: Optimize for Your Project

After installation, you can optimize the release notes generator for your specific project. This produces more relevant release notes by understanding your commit conventions and release workflow.

Run this prompt in Claude Code:

```
I just installed the release-notes command in .claude/. Please:

1. Analyze my repository to detect my commit conventions, versioning strategy, and release workflow
2. Read the command files in .claude/commands/release-notes.md and .claude/release/agents/
3. Optimize each release notes agent by:
   - Adjusting commit pattern detection to match my commit message format
   - Customizing the marketing template for my product type (SaaS, mobile app, library, etc.)
   - Configuring internal notes format based on my team communication style
   - Setting up changelog format to match my existing CHANGELOG.md if present
4. Keep the agent structure, output formats, and Git analysis logic unchanged

Show me what you'll change before applying.
```

## Usage

In Claude Code, run the release notes command:

```
/release-notes
```

### Command Arguments

| Argument | Description | Example |
|----------|-------------|---------|
| `--from=<ref>` | Starting point (tag, commit, branch) | `--from=v1.0.0` |
| `--to=<ref>` | Ending point (default: HEAD) | `--to=v1.1.0` |
| `--version=<semver>` | Version number for the release | `--version=1.1.0` |
| `--date=<date>` | Release date (default: today) | `--date=2025-01-15` |

### Generation Modes

| Command | Description |
|---------|-------------|
| `/release-notes` | Interactive mode - asks which format to generate |
| `/release-notes technical` | GitHub-style technical release notes |
| `/release-notes marketing` | App store release notes with character limits |
| `/release-notes internal` | Team/stakeholder communication format |
| `/release-notes security` | Security-focused release notes (CVEs, vulnerabilities) |
| `/release-notes full` | Generate all formats |

### Examples

```bash
# Generate technical notes for a specific version range
/release-notes technical --from=v1.0.0 --to=v1.1.0 --version=1.1.0

# Generate marketing notes for the latest release
/release-notes marketing --from=v1.0.0 --version=1.1.0

# Generate all formats
/release-notes full --from=v1.0.0 --version=1.1.0 --date=2025-01-15

# Interactive mode
/release-notes
```

## Output Formats

### Technical Release Notes

Perfect for GitHub releases, includes:
- Version number with semantic versioning
- Release date
- Breaking Changes section
- New Features (from `feat:` commits)
- Bug Fixes (from `fix:` commits)
- Performance Improvements (from `perf:` commits)
- Dependencies Updated
- Deprecations
- Migration Guide (if breaking changes exist)
- Full commit list with conventional commit grouping
- Contributors list
- Compare link to previous version

### Marketing Release Notes

Optimized for app stores and end-user communication:
- Catchy headline summarizing the release
- What's New section with user benefits
- Bug fixes in user-friendly language
- Performance improvements with tangible benefits
- Coming soon teaser

**Character Limits:**
- App Store (iOS): 4000 characters
- Play Store (Android): 500 characters
- Tweet-length summary: 280 characters

### Internal Release Notes

For team and stakeholder communication:
- Release summary
- Business impact assessment
- Technical changes summary
- Risk assessment
- Rollback plan
- Monitoring checklist
- Known issues
- Support team notes
- Sales enablement notes

### Security Release Notes

For security-focused releases:
- CVE references
- Vulnerability descriptions
- Severity ratings (CVSS)
- Affected versions
- Fixed versions
- Mitigation steps
- Credits to security reporters
- Timeline of disclosure

### Changelog (CHANGELOG.md)

Maintains a changelog following [Keep a Changelog](https://keepachangelog.com/):
- Unreleased section for ongoing work
- Version sections with release dates
- Category grouping:
  - Added (new features)
  - Changed (changes in existing functionality)
  - Deprecated (soon-to-be removed features)
  - Removed (now removed features)
  - Fixed (bug fixes)
  - Security (vulnerability fixes)
- Links to issues and PRs
- Compare URLs between versions

## Commit Analysis

The generator analyzes commits for:

| Pattern | Detection |
|---------|-----------|
| `feat:` / `feature:` | New features |
| `fix:` / `bugfix:` | Bug fixes |
| `perf:` | Performance improvements |
| `docs:` | Documentation changes |
| `style:` | Code style changes |
| `refactor:` | Code refactoring |
| `test:` | Test additions/changes |
| `chore:` | Maintenance tasks |
| `build:` | Build system changes |
| `ci:` | CI/CD changes |
| `BREAKING CHANGE:` | Breaking changes |
| `!` after type | Breaking changes (e.g., `feat!:`) |

### Scope Extraction

Commits with scopes like `feat(auth):` are grouped by their scope for better organization.

### Issue/PR References

Automatically detects:
- `#123` - Issue/PR number
- `Fixes #123` - Closing references
- `Closes #123` - Closing references
- `Resolves #123` - Closing references

## Agent Specifications

| Agent | ID | Purpose |
|-------|-----|---------|
| Technical Notes | REL01 | GitHub/developer-focused release notes |
| Marketing Notes | REL02 | App store/end-user release notes |
| Internal Notes | REL03 | Team/stakeholder communication |
| Security Notes | REL04 | CVE and vulnerability documentation |
| Changelog | REL05 | CHANGELOG.md maintenance |

## Customization

To adapt for your specific needs:

1. **Commit patterns** - Modify pattern recognition in agent files
2. **Output format** - Edit templates in `release/templates/`
3. **Character limits** - Adjust limits in marketing agent
4. **Categories** - Add/remove categories in changelog agent

## Output Location

Generated release notes are saved to:
- `release-notes/YYYY-MM-DD-<version>-technical.md`
- `release-notes/YYYY-MM-DD-<version>-marketing.md`
- `release-notes/YYYY-MM-DD-<version>-internal.md`
- `release-notes/YYYY-MM-DD-<version>-security.md`
- `CHANGELOG.md` (project root, updated in place)

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) file.

## Tips for Best Results

1. **Use Conventional Commits** - The generator works best with [conventional commit](https://www.conventionalcommits.org/) format
2. **Include Scopes** - Use scopes like `feat(api):` for better categorization
3. **Mark Breaking Changes** - Use `BREAKING CHANGE:` in commit body or `!` after type
4. **Reference Issues** - Include issue numbers for automatic linking
5. **Write Good Commit Messages** - First line should be a clear summary

## References

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
