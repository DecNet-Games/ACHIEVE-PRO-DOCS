---
layout: default
title: Spoiler & Secret Protection
parent: Core Features
nav_order: 4
---

# Spoiler & Secret Protection Engine
{: .no_toc }

Protect story twists and secret easter eggs with 7 distinct masking modes, Unicode redaction, and interactive player unmasking.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🕵️ The 7 Dynamic Secret Modes (`SecretBehavior`)

| Mode | Title Display | Description Display | Icon Display |
|:---|:---|:---|:---|
| **`HiddenUntilUnlocked`** | `??? Secret Achievement` | `Keep playing to discover this secret.` | Mystery Icon |
| **`ShowTitleOnly`** | Real Title | `??? Secret details masked until unlocked.` | Mystery / Lock Icon |
| **`ShowSpoiler`** | Real Title | `[SPOILER] {Real Description}` | Real Icon |
| **`CompletelyHidden`** | Omitted from gallery entirely until unlocked | Omitted | Omitted |
| **`RedactedText`** | Real Title | Black bar Unicode: `████ ██████ ████` | Mystery Icon |
| **`PartialHint`** | Real Title | Custom `secretHint` teaser text | Mystery Icon |
| **`BlurOverlay`** | Real Title | Marked for UI shader blur effect | Mystery Icon |

---

## 🖤 Unicode Black-Bar Redaction (`RedactedText`)

When `RedactedText` is selected, `SpoilerProtectionEngine.RedactText(desc)` dynamically replaces alphanumeric characters with solid black bars `█` while preserving punctuation, spacing, and word lengths for authentic redacted document styling!

---

## 👁️ Interactive Player Click-to-Reveal

If `allowPlayerReveal = true` on the `AchievementSO`:
- `AchievementGalleryItemUI` renders an **"👁️ Reveal Spoiler"** button.
- Clicking the button unmasks the description locally and remembers the player's reveal preference across sessions.

```csharp
// Reveal secret programmatically
AchievementManager.RevealSecret("secret_lore_shrine");
```
