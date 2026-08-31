---
layout: default
title: Troubleshooting
nav_order: 90
parent: Docs
---

# Troubleshooting Guide
{: .no_toc }

Common issues and their solutions when working with ACHIEVE PRO.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🛑 UI Not Rendering
**Issue:** Achievement popups are not showing up on screen when an achievement is unlocked.

**Solutions:**
1. **Missing Canvas Rig:** Ensure you have the `AchievementCanvas` prefab in your scene. You can easily add it via `Tools > Achievement System Pro > Scene Wizard > Setup UI Rig`.
2. **Event System Missing:** Check if your scene has an `EventSystem` GameObject.
3. **Z-Ordering / Sorting Layer:** The canvas might be rendering behind other UI elements. Increase the `Sort Order` on the `Canvas` component of your `AchievementCanvas`.

## 💾 Progress Not Saving Between Sessions
**Issue:** Achievements unlock during play, but reset when restarting the game.

**Solutions:**
1. **Save Manager Initialization:** Ensure `AchievementManager.Instance.Save()` is being called, or enable **Auto-Save on Unlock** in the Studio Hub settings.
2. **Corrupted Save File:** Navigate to your persistent data path (usually `%APPDATA%\LocalLow\YourCompany\YourGame` on Windows) and delete `achievements_data.dat` to clear potentially corrupted data.
3. **AES Key Mismatch:** If you recently regenerated your AES-256 encryption keys, old save files will fail to load and will be discarded.

## 🎧 No Sound Playing on Unlock
**Issue:** The visual popup appears, but no sound plays.

**Solutions:**
1. **AudioListener Missing:** Ensure there is an `AudioListener` component on your Main Camera.
2. **Audio Source on Canvas:** The `AchievementPopupController` requires an `AudioSource` component to play SFX.
3. **Muted via Code:** Check if you've accidentally called `AchievementManager.Instance.SetAudioMuted(true)`.

## ⚠️ Compilation Errors After Import
**Issue:** Missing reference exceptions or namespace errors.

**Solutions:**
1. **Assembly Definitions:** If your project uses `.asmdef` files, you must add a reference to `AchievementSystemPro.Runtime` in your project's assembly definition file.
2. **Unity Version:** Ensure you are running Unity 2021.3 LTS or newer.

## 📈 Stats Not Tracking
**Issue:** `StatManager.AddProgress("enemies_killed", 1)` is not triggering the associated achievement.

**Solutions:**
1. **Stat ID Mismatch:** Double check that the Stat ID in your script matches EXACTLY with the ID in the Studio Hub.
2. **Prerequisites:** Check if the achievement has unmet prerequisites blocking its unlock.
