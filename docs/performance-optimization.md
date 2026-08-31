---
layout: default
title: Performance Optimization
nav_order: 85
parent: Docs
---

# Performance Optimization
{: .no_toc }

ACHIEVE PRO is built to be blisteringly fast, but here are some tips to squeeze out every last drop of performance.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🚀 Zero Allocation Design

ACHIEVE PRO is designed with a zero-allocation runtime architecture. This means once the game is running, updating stats and unlocking achievements will not generate garbage for the Garbage Collector (GC), preventing micro-stutters.

## 💾 Save Operations

Saving to disk is the most expensive operation in any system.

### Batching Saves
By default, ACHIEVE PRO uses an **Auto-Save on Unlock** feature. If your game unlocks many achievements in rapid succession (e.g., tally screen at the end of a level), this can cause disk I/O bottlenecks.

**Optimization:** Disable Auto-Save in the Studio Hub and manually call `AchievementManager.Instance.Save()` during loading screens, level transitions, or application quit.

## 🖼️ UI Canvas Rendering

Unity's UI Canvas redraws itself whenever an element inside it changes.

### Isolate the Canvas
The `AchievementCanvas` provided in the Scene Wizard is isolated. **Do not** place your game's main HUD (health bars, minimaps) inside the `AchievementCanvas`. Keep them separate so that the achievement popups animating don't force your entire HUD to rebuild every frame.

### Disable Graphic Raycasters
If your achievement popups don't require mouse clicks (e.g., they just fade away), remove the `Graphic Raycaster` component from the `AchievementCanvas` to save CPU time during input processing.

## 🔍 Data Lookups

When querying achievements via code, use the string IDs. The system uses highly optimized `Dictionary<string, Achievement>` lookups under the hood, making `AchievementManager.GetAchievement("id")` an $O(1)$ operation.

Avoid iterating over the entire `AchievementManager.Instance.GetAllAchievements()` list every frame. Cache references if you need them continuously.
