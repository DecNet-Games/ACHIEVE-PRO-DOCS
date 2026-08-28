---
layout: default
title: Daily / Weekly Streaks & Recurrence
parent: Core Features
nav_order: 2
---

# Daily / Weekly Streaks & Recurrence
{: .no_toc }

Drive long-term player retention with automated calendar resets, recurring bounties, and streak trackers.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📅 Recurrence Cadence Options

ACHIEVE PRO provides enterprise-grade UTC-synchronized calendar timing:

| Cadence Mode (`AchievementRecurrence`) | Reset Timing |
|:---|:---|
| **`Daily`** | Resets every day at **00:00:00 UTC** midnight. |
| **`Weekly`** | Resets every **Monday at 00:00:00 UTC** midnight. |
| **`CustomCooldown`** | Resets after $X$ configurable hours (e.g. 12 hours, 72 hours). |
| **`StreakBased`** | Requires daily completion to maintain active consecutive streak count. |

---

## 🔥 Player Login Streak Engine

The built-in `StreakManager` processes player check-ins with a customizable **grace period** (default: 36 hours) to prevent timezone drift penalties:

```csharp
// Call upon player login or main menu launch
var (currentStreak, longestStreak) = AchievementManager.ProcessDailyLogin(gracePeriodHours: 36);

Debug.Log($"🔥 Active Login Streak: {currentStreak} Days (Record: {longestStreak})");
```

### Formatted Countdown Timers
Display real-time countdown clocks in your HUD with zero manual string parsing:

```csharp
long remainingSeconds = AchievementManager.GetTimeUntilReset("daily_dungeon_bounty");

// Outputs: "14h 32m 05s"
string formattedTime = StreakManager.FormatRemainingTime(remainingSeconds);
```

---

## 🔄 Repeating Cycles & Milestones

For recurring achievements (e.g. *Daily Dungeon Clear*):
- Total completions are tracked independently (`AchievementManager.GetCompletionCount("daily_dungeon")`).
- Consecutive streaks are tracked independently (`AchievementManager.GetAchievementStreak("daily_dungeon")`).
- `maxRepeats` can limit how many times a recurring achievement grants rewards (or set `0` for infinite).
