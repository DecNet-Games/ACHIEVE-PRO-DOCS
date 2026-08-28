---
layout: default
title: Getting Started
nav_order: 3
parent: Docs
---

# Getting Started
{: .no_toc }

Understand the core architecture, operational flow, and mental model of ACHIEVE PRO.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🏛️ Core Architecture Overview

ACHIEVE PRO is designed around a clean, decoupled **Facade & Event-Driven Architecture**:

```
 ┌────────────────────────────────────────────────────────┐
 │            Your Gameplay Scripts / Triggers            │
 └────────────────────────────────────────────────────────┘
                             │  (Calls static facade methods)
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │               AchievementManager (Facade)              │
 └────────────────────────────────────────────────────────┘
           │                         │
           ▼                         ▼
 ┌───────────────────┐     ┌───────────────────┐
 │ AchievementTracker│     │    StatManager    │
 └───────────────────┘     └───────────────────┘
           │ (Domain Engine)         │ (Rule Engine)
           ▼                         ▼
 ┌───────────────────┐     ┌───────────────────┐
 │AchievementEvents  │     │AchievementDatabase│
 │   (C# Event Bus)  │     │(ScriptableObjects)│
 └───────────────────┘     └───────────────────┘
           │
           ├─────────────────────────┬─────────────────────────┐
           ▼                         ▼                         ▼
 ┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
 │PopupController    │     │AchievementPersist.│     │IPlatformAdapter   │
 │(Spring Physics UI)│     │(AES-256 Storage)  │     │(Steam, GPG, EOS)  │
 └───────────────────┘     └───────────────────┘     └───────────────────┘
```

---

## 🧱 The 4 Core Architectural Components

### 1. `AchievementManager` (Static Facade)
The primary entry point for your game. Provides high-level, zero-allocation static methods:
- `AchievementManager.Unlock("boss_dragon")`
- `AchievementManager.AddProgress("gold_hoarder", 50f)`
- `AchievementManager.SetStat("enemies_slain", 100f)`
- `AchievementManager.GetLoginStreak()`

### 2. `AchievementTracker` (Domain Engine)
Encapsulates all progression logic, including:
- Checking if prerequisites in quest trees are satisfied.
- Calculating fractional progress and milestone tier promotions (Bronze ➔ Silver ➔ Gold).
- Enforcing cooldowns and repeating cycle resets.
- Dispatching reward payloads (XP, In-Game Currency, Custom Items).

### 3. `StatManager` (Rule Evaluator)
Maintains decoupled gameplay statistics (e.g. `kills`, `score`, `accuracy_pct`). Automatically evaluates single-stat and multi-condition `CompositeRule` achievements whenever any tracked statistic changes.

### 4. `AchievementPersistence` (AES-256 Storage)
Saves profile data atomically to disk with AES-256 encryption, PBKDF2 salt derivation, and HMAC-SHA256 anti-tamper checksums. Supports multiple save slots (`AchievementManager.SwitchSlot("slot_2")`).

---

## ⚡ Your First Unlock in 30 Seconds

### Step 1: Initialize Scene with 1-Click Wizard
Open the Scene Wizard via `Tools > Achievement System Pro > 1-Click Scene Wizard`, pick your preferred toast anchor (e.g. **Top Right**), and click **"Generate Setup in Active Scene"**.

### Step 2: Trigger from Code
In any gameplay C# script, trigger an unlock with a single line:

```csharp
using DecnetGames.AchievementSystemPro;
using UnityEngine;

public class PlayerCombat : MonoBehaviour
{
    public void OnBossDefeated()
    {
        // Unlock an achievement by ID
        AchievementManager.Unlock("defeat_first_boss");
    }
}
```

When called, the engine will:
1. Validate dependencies in the quest tree.
2. Persist the unlock to encrypted disk storage.
3. Fire `AchievementEvents.OnAchievementUnlocked`.
4. Trigger the `PopupController` to spawn a 2nd-order damped spring physics toast with procedural audio.
5. Notify the active platform bridge (Steam, Game Center, Google Play, or Editor Simulator).
