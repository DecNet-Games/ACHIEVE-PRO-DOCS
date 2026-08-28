---
layout: default
title: Architecture
nav_order: 5
parent: Docs
---

# Architecture & Engine Design
{: .no_toc }

A technical deep-dive into ACHIEVE PRO's runtime engine, event bus, memory optimization, and security model.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🏛️ Layered Architectural Structure

ACHIEVE PRO adheres strictly to clean architecture principles, separating concerns across distinct layers:

```
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                       │
│  - PopupController (Queue & Layout)                         │
│  - PopupAnimator (2nd-Order Mass-Spring Physics)            │
│  - AchievementGalleryUI (Search, Filter, Spoilers)          │
│  - InEditorPlatformSimulator (Mock Steam/PS5/Xbox Overlays) │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      DOMAIN LAYER                           │
│  - AchievementManager (Static Facade)                       │
│  - AchievementTracker (State, Milestones, Dependencies)     │
│  - StatManager (Gameplay Stats & Composite Rules)           │
│  - StreakManager (UTC Daily/Weekly Resets & Cadence)        │
│  - SpoilerProtectionEngine (7-Mode Masking & Unmasking)     │
│  - RuleEngine (Non-allocating Boolean AST Evaluator)        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   INFRASTRUCTURE LAYER                      │
│  - AchievementPersistence (AES-256-CBC, PBKDF2, HMAC)       │
│  - CloudSyncAdapter (REST Webhooks & Cloud Storage)         │
│  - CloudOfflineQueue (Persistent Network Buffer)            │
│  - Platform Adapters (Steamworks, GameCenter, GPG, EOS)     │
└─────────────────────────────────────────────────────────────┘
```

---

## ⚡ Zero-Allocation Runtime Design

To ensure consistent 60+ FPS on mobile devices and consoles, ACHIEVE PRO is engineered for minimal garbage collection:
- **No Dynamic String Concatenation in Game Loops**: Formatted strings and UI text updates are cached or evaluated only when values actually change.
- **Cached Delegates & Event Invocations**: Event listeners avoid runtime lambda allocations.
- **Physics Oscillator In-Place Vector Math**: Damped harmonic oscillator computations use stack-allocated structs without instantiating animator objects.
- **Collection Pooling**: List and dictionary buffers are reused across batch operations.

---

## 🔒 Thread Safety & Coroutine Time-Scaling

In modern games, pausing gameplay by setting `Time.timeScale = 0` is common practice (e.g. inventory screens, pause menus, dialog cutscenes).

- All ACHIEVE PRO UI animations, spring physics integrators, and toast timeouts use `Time.unscaledDeltaTime`.
- Toasts slide in, hold, and dismiss smoothly even when the game is completely paused.
- The mass-spring-damper integrator clamps $\Delta t \le 0.033\text{s}$ to guarantee absolute mathematical stability during extreme frame rate hitches.

---

## 🌐 Cross-Platform Abstraction Model

ACHIEVE PRO abstracts platform SDK differences via the `IPlatformAchievementAdapter` interface:

```csharp
public interface IPlatformAchievementAdapter
{
    string PlatformName { get; }
    PlatformType PlatformType { get; }
    bool IsInitialized { get; }
    void Initialize();
    void UnlockAchievement(AchievementSO achievement);
    void UpdateProgress(AchievementSO achievement, float currentProgress, float maxProgress);
    void ResetAchievements();
    void Shutdown();
}
```

The `PlatformAdapterFactory` automatically resolves the proper adapter at compile time:
- **`STEAMWORKS_NET` / `FACEPUNCH_STEAMWORKS`** ➔ `SteamworksAdapter`
- **`UNITY_ANDROID`** ➔ `GooglePlayGamesAdapter`
- **`UNITY_IOS` / `UNITY_STANDALONE_OSX`** ➔ `GameCenterAdapter`
- **`EOS_SDK`** ➔ `EpicOnlineServicesAdapter`
- **Unity Editor** ➔ `InEditorPlatformSimulator`
