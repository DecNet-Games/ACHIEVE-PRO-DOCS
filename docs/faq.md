---
layout: default
title: FAQ & Troubleshooting
nav_order: 9
parent: Docs
---

# Frequently Asked Questions & Troubleshooting
{: .no_toc }

Common developer questions, edge cases, and performance diagnostics for ACHIEVE PRO.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## ❓ Frequently Asked Questions

### Q: Does ACHIEVE PRO require TextMeshPro?
**A**: ACHIEVE PRO natively supports TextMeshPro (`TextMeshProUGUI`) for crystal-clear typography, but includes automatic fallbacks to Unity's standard `UnityEngine.UI.Text` if TMP is not imported.

### Q: Can I use ACHIEVE PRO on consoles (PS5, Xbox, Switch)?
**A**: Yes! The runtime engine uses standard C# without platform-restricted dependencies. The `IPlatformAchievementAdapter` interface allows 1-line bridging to Sony PlayStation NP Toolkit, Microsoft GDK, and Nintendo Switch NPNS.

### Q: Does toast animation stutter when the game is paused (`Time.timeScale = 0`)?
**A**: No. The mass-spring-damper physics engine is computed strictly with `Time.unscaledDeltaTime`, guaranteeing smooth 60fps animations even when gameplay is completely frozen.

### Q: Where is save data stored on the player's device?
**A**: Saves are encrypted with AES-256 and stored in `Application.persistentDataPath/AchievementSystemPro/achievements_{slotName}.dat`. On WebGL builds, it automatically falls back to encrypted Base64 `PlayerPrefs`.

### Q: How do I clear save data during testing?
**A**: In the Unity Editor, click `Tools > Achievement System Pro > Wipe Save File` or press the **"🧹 Wipe Local Save File"** button in the Achievement Studio Hub. In code, call `AchievementManager.ResetAll()`.

---

## 🛠️ Performance & Allocation Benchmarks

- **Runtime Memory Overhead**: Under 150 KB.
- **Garbage Collection (GC Alloc)**: 0 B per frame during idle, 0 B during standard progress increments.
- **Physics Integration Time**: Under 0.02ms per active toast on mobile hardware.
