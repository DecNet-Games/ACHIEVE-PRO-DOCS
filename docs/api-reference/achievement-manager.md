---
layout: default
title: AchievementManager API
parent: API Reference
nav_order: 1
---

# `AchievementManager` Static API Reference
{: .no_toc }

The primary C# entry point for runtime progression calls in your game.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🔓 Core Unlocks & Progress

```csharp
// Unlocks an achievement immediately
public static bool Unlock(string id);

// Unlocks an achievement by ScriptableObject reference
public static bool Unlock(AchievementSO achievement);

// Adds incremental progress towards an achievement
public static bool AddProgress(string id, float amount);

// Sets absolute progress value
public static bool SetProgress(string id, float value);

// Checks if an achievement is unlocked
public static bool IsUnlocked(string id);

// Retrieves current progress value
public static float GetProgress(string id);

// Retrieves highest unlocked milestone tier index (0=Bronze, 1=Silver, etc.)
public static int GetUnlockedTierIndex(string id);
```

---

## 📊 Gameplay Statistics & Rule Engine

```csharp
// Increments a tracked gameplay statistic
public static void IncrementStat(string statKey, float amount = 1f);

// Sets an absolute statistic value
public static void SetStat(string statKey, float value);

// Gets current statistic value
public static float GetStat(string statKey);
```

---

## 🔥 Login Streaks & Recurrence

```csharp
// Processes daily login check-in and updates consecutive streak
public static (int currentStreak, int longestStreak) ProcessDailyLogin(int gracePeriodHours = 36);

// Gets active consecutive daily login streak count
public static int GetLoginStreak();

// Gets all-time record login streak
public static int GetLongestLoginStreak();

// Gets total completion cycle count for a repeating achievement
public static int GetCompletionCount(string id);

// Gets active streak for a repeating achievement
public static int GetAchievementStreak(string id);

// Gets seconds remaining until next scheduled reset
public static long GetTimeUntilReset(string id);
```

---

## 💾 Multi-Slot Profiles & Cloud Sync

```csharp
// Switches active save slot and loads profile data
public static void SwitchSlot(string slotName);

// Gets currently active slot name
public static string GetActiveSlotName();

// Lists all discovered save slots on disk
public static List<SaveSlotInfo> ListAllSlots();

// Exports active slot as Base64-encrypted payload string
public static string ExportActiveSlotPayload();

// Imports and merges Base64-encrypted cloud payload
public static bool ImportActiveSlotPayload(string base64Payload, CloudMergeStrategy strategy);
```
