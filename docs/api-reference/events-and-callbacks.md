---
layout: default
title: Global Event Bus Callbacks
parent: API Reference
nav_order: 2
---

# `AchievementEvents` Global Event Bus
{: .no_toc }

Listen to lifecycle progression events across UI, audio, analytics, and reward systems with zero GC allocations.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📡 Available Action Delegates

```csharp
namespace DecnetGames.AchievementSystemPro
{
    public static class AchievementEvents
    {
        // Fired when an achievement is fully unlocked
        public static Action<AchievementSO> OnAchievementUnlocked;

        // Fired when progress is updated (ach, currentProgress, maxProgress)
        public static Action<AchievementSO, float, float> OnProgressUpdated;

        // Fired when a milestone tier is unlocked (ach, tierIndex, tier)
        public static Action<AchievementSO, int, AchievementTier> OnTierUnlocked;

        // Fired when in-game rewards are granted (ach, rewardPayload)
        public static Action<AchievementSO, AchievementReward> OnRewardGranted;

        // Fired when quest prerequisites are satisfied
        public static Action<AchievementSO> OnPrerequisitesSatisfied;

        // Fired when a repeating achievement resets for a new cycle
        public static Action<AchievementSO, int> OnRepeatingAchievementReset;

        // Fired when player login streak changes (currentStreak, longestStreak)
        public static Action<int, int> OnLoginStreakUpdated;

        // Fired when a player reveals a secret in the UI
        public static Action<string> OnSecretRevealed;

        // Fired when all achievements in the database are unlocked (Platinum Trophy)
        public static Action OnAllAchievementsUnlocked;

        // Fired when save data is cleared or reset
        public static Action OnAchievementsReset;
    }
}
```

---

## 💡 Subscribing from Gameplay or UI Scripts

```csharp
using DecnetGames.AchievementSystemPro;
using UnityEngine;

public class GameAnalytics : MonoBehaviour
{
    private void OnEnable()
    {
        AchievementEvents.OnAchievementUnlocked += HandleUnlock;
        AchievementEvents.OnRewardGranted += HandleReward;
    }

    private void OnDisable()
    {
        AchievementEvents.OnAchievementUnlocked -= HandleUnlock;
        AchievementEvents.OnRewardGranted -= HandleReward;
    }

    private void HandleUnlock(AchievementSO ach)
    {
        Debug.Log($"Analytics Track: Unlocked '{ach.title}' (+{ach.pointsValue}G)");
    }

    private void HandleReward(AchievementSO ach, AchievementReward reward)
    {
        // Grant XP or Currency to Player Inventory
        if (reward.experienceReward > 0)
        {
            PlayerInventory.AddXP(reward.experienceReward);
        }
    }
}
```
