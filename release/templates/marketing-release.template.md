---
description: "[Internal] Marketing release notes template - use /release-notes instead"
disable-model-invocation: true
---

# Marketing Release Notes Template

Templates for app store and end-user release notes with character limits.

---

## Full Version Template (App Store - 4000 chars)

```markdown
{{EMOJI}} {{HEADLINE}}

{{INTRODUCTION}}

WHAT'S NEW

{{#FEATURES}}
{{FEATURE_TITLE}}

{{FEATURE_DESCRIPTION}}

{{/FEATURES}}

{{#BUG_FIXES}}
BUG FIXES

{{#ITEMS}}
- {{FIX_DESCRIPTION}}
{{/ITEMS}}

{{/BUG_FIXES}}

{{#PERFORMANCE}}
FASTER & SMOOTHER

{{#ITEMS}}
- {{IMPROVEMENT_DESCRIPTION}}
{{/ITEMS}}

{{/PERFORMANCE}}

{{#COMING_SOON}}
COMING SOON

{{TEASER}}

{{/COMING_SOON}}

---

{{CLOSING}}
```

---

## Short Version Template (Play Store - 500 chars)

```markdown
{{HEADLINE}}

What's New:
{{#FEATURES}}
- {{FEATURE_ONE_LINER}}
{{/FEATURES}}

{{#BUG_FIXES}}
Bug Fixes:
{{#ITEMS}}
- {{FIX_ONE_LINER}}
{{/ITEMS}}

{{/BUG_FIXES}}

{{#PERFORMANCE}}
{{PERFORMANCE_ONE_LINER}}
{{/PERFORMANCE}}

{{#COMING_SOON}}
{{TEASER_SHORT}}
{{/COMING_SOON}}
```

---

## Tweet Version Template (280 chars)

```markdown
{{EMOJI}} {{TWEET_HEADLINE}} {{TWEET_FEATURES}} {{CALL_TO_ACTION}} {{LINK}}
```

---

## Variable Reference

### Headlines

| Variable | Description | Max Length | Example |
|----------|-------------|------------|---------|
| `{{EMOJI}}` | Opening emoji | 2 chars | "✨" |
| `{{HEADLINE}}` | Main headline | 60 chars | "Lightning-Fast Search is Here!" |
| `{{TWEET_HEADLINE}}` | Tweet-optimized headline | 40 chars | "Big update!" |

### Introduction

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{INTRODUCTION}}` | 1-2 sentence intro | 150 chars |

### Features

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{FEATURE_TITLE}}` | Feature name | 30 chars |
| `{{FEATURE_DESCRIPTION}}` | Feature benefit description | 200 chars |
| `{{FEATURE_ONE_LINER}}` | Single-line feature | 50 chars |
| `{{TWEET_FEATURES}}` | Features for tweet | 80 chars |

### Bug Fixes

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{FIX_DESCRIPTION}}` | User-friendly fix description | 100 chars |
| `{{FIX_ONE_LINER}}` | Single-line fix | 40 chars |

### Performance

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{IMPROVEMENT_DESCRIPTION}}` | Performance improvement | 80 chars |
| `{{PERFORMANCE_ONE_LINER}}` | Single-line performance note | 50 chars |

### Coming Soon

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{TEASER}}` | Teaser for next release | 100 chars |
| `{{TEASER_SHORT}}` | Short teaser | 40 chars |

### Closing

| Variable | Description | Max Length |
|----------|-------------|------------|
| `{{CLOSING}}` | Call to action / feedback | 100 chars |
| `{{CALL_TO_ACTION}}` | Tweet CTA | 20 chars |
| `{{LINK}}` | Short link | 23 chars |

---

## Character Count Guidelines

### App Store (iOS) - 4000 characters

**Recommended Distribution:**
- Headline: 60 chars
- Introduction: 150 chars
- Features (3-4): 800 chars total
- Bug Fixes (3-5): 400 chars total
- Performance (2-3): 250 chars total
- Coming Soon: 100 chars
- Closing: 100 chars
- Whitespace/formatting: ~200 chars

**Total target: 2000-3500 chars** (leave room for expansion)

### Play Store (Android) - 500 characters

**Recommended Distribution:**
- Headline: 50 chars
- Features (2-3): 150 chars
- Bug Fixes (1-2): 80 chars
- Performance (1): 50 chars
- Teaser: 40 chars
- Whitespace: ~30 chars

**Total target: 400-480 chars** (stay under limit)

### Tweet - 280 characters

**Recommended Distribution:**
- Emoji: 2 chars
- Headline: 40 chars
- Features: 80 chars
- CTA: 20 chars
- Link: 23 chars (t.co)
- Spaces: ~15 chars

**Total target: 180-260 chars** (leave room for link expansion)

---

## Emoji Guidelines

### By Category

| Category | Recommended Emojis |
|----------|-------------------|
| Major Release | ✨ 🎉 🚀 💫 |
| Speed/Performance | ⚡ 🚀 💨 ⏱️ |
| Bug Fix | 🐛 ✅ 🔧 |
| Security | 🔒 🛡️ 🔐 |
| UI/Design | 🎨 ✏️ 💅 |
| Dark Mode | 🌙 🌑 |
| Photos/Media | 📸 🖼️ 🎬 |
| Sync/Cloud | ☁️ 🔄 |

### Usage Rules

- One emoji at start of headline
- Optionally one emoji per major feature section
- No emoji in bug fix descriptions
- No emoji strings or excessive use

---

## Example: Full Version

```markdown
✨ Lightning-Fast Search is Here!

Finding your files just got 10x faster. This update brings features you've been asking for.

WHAT'S NEW

Smart Search

Type a few letters and watch the magic happen. Our new search learns what you're looking for and shows relevant results first. Finding that photo from last summer now takes seconds.

Dark Mode

Easy on your eyes, especially at night. Switch to Dark Mode in Settings or let it follow your system automatically.

Offline Access

No internet? No problem. Your recent files are now available offline, so you can keep working anywhere.

BUG FIXES

- Sign-in is now more reliable on slower connections
- Notifications appear properly on all devices
- Files sync correctly across your devices

FASTER & SMOOTHER

- The app opens 50% faster
- Scrolling is buttery smooth
- Battery usage reduced significantly

COMING SOON

Something exciting is in the works. Stay tuned! 👀

---

Love the app? Leave us a review - it helps others find us!
```

**Character count: ~1,100 / 4,000**

---

## Example: Short Version

```markdown
Lightning-fast search is here! Find anything in seconds.

What's New:
- Smart Search - results as you type
- Dark Mode - easy on your eyes
- Offline Access - work anywhere

Bug Fixes:
- Sign-in more reliable
- Notifications fixed

50% faster app launch!
```

**Character count: ~260 / 500**

---

## Example: Tweet Version

```markdown
✨ App 2.0: Smart Search + Dark Mode + Offline Access. Your most-requested features, delivered! Update now 🚀
```

**Character count: ~108 / 280**

---

## Localization Notes

When preparing for translation:

1. **Avoid idioms** - "hit the ground running" doesn't translate well
2. **Keep sentences simple** - Subject-verb-object structure
3. **No puns** - Rarely work in other languages
4. **Be explicit** - Don't rely on cultural context
5. **Account for expansion** - Some languages need 30% more space
