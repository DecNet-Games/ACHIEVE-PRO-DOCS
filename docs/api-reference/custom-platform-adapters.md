---
layout: default
title: Custom Platform Adapters
parent: API Reference
nav_order: 3
---

# Creating Custom Platform Adapters
{: .no_toc }

Integrate proprietary multiplayer backends, custom consoles, or specialized leaderboard SDKs into ACHIEVE PRO.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🛠️ Implementing `IPlatformAchievementAdapter`

Create a new C# class implementing `IPlatformAchievementAdapter`:

```csharp
using DecnetGames.AchievementSystemPro;
using UnityEngine;

public class MyCustomServerAdapter : IPlatformAchievementAdapter
{
    public string PlatformName => "CustomBackend";
    public PlatformType PlatformType => PlatformType.Custom;
    public bool IsInitialized { get; private set; }

    public void Initialize()
    {
        // Connect to your proprietary backend
        IsInitialized = true;
    }

    public void UnlockAchievement(AchievementSO achievement)
    {
        // Dispatch network packet to your server
        Debug.Log($"[CustomServer] Forwarding unlock: {achievement.id}");
    }

    public void UpdateProgress(AchievementSO achievement, float currentProgress, float maxProgress)
    {
        // Dispatch fractional progress
    }

    public void ResetAchievements()
    {
        // Sandbox reset call
    }

    public void Shutdown()
    {
        IsInitialized = false;
    }
}
```

---

## 🔄 Registering at Runtime

Inject your custom adapter into `AchievementManager` on startup:

```csharp
void Start()
{
    AchievementManager.SetPlatformAdapter(new MyCustomServerAdapter());
}
```
