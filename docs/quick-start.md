---
layout: default
title: 5-Minute Quick Start
nav_order: 4
parent: Docs
---

# 5-Minute Quick Start Guide
{: .no_toc }

A complete walkthrough showing how to create, configure, trigger, and display achievements in 5 minutes.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Step 1: Create an Achievement ScriptableObject

1. Open the **Achievement Studio Hub** (`Tools > Achievement System Pro > Achievement Studio Hub` or press `Ctrl+Shift+A` / `Cmd+Shift+A`).
2. Click **"+ Create New Achievement"**.
3. Fill in the fields:
   - **ID**: `slay_10_goblins`
   - **Title**: `Goblin Exterminator`
   - **Description**: `Defeat 10 sneaky goblins in the dungeon.`
   - **Type**: `Progress`
   - **Target Value**: `10`
   - **Unit Suffix**: `goblins`
   - **Rarity**: `Uncommon`
   - **Points (+G)**: `25`
4. Assign an **Icon** (Sprite).
5. Click **"Save Achievement"**. The asset will be generated into `Assets/Resources/Achievements/` and automatically registered with the database.

---

## Step 2: Track Progress from Gameplay

Attach a script or invoke `AchievementManager.AddProgress` when gameplay events happen:

```csharp
using DecnetGames.AchievementSystemPro;
using UnityEngine;

public class GoblinEnemy : MonoBehaviour
{
    public void OnGoblinKilled()
    {
        // Add 1 step towards the target value of 10
        AchievementManager.AddProgress("slay_10_goblins", 1f);
    }
}
```

> ### 💡 Pro Tip: Incremental Progress Toasts
> If enabled in the theme settings, `PopupController` will display discrete progress toasts (e.g. `Goblin Exterminator: 5 / 10 (50%)`) at specified percentage milestones.

---

## Step 3: Configure Tiered Milestones (Bronze ➔ Platinum)

For multi-stage achievements (e.g. *Slay 10, 50, 100 Goblins*), switch the **Type** to `Tiered` in the Studio Hub:

```csharp
// Increment progress — the engine auto-detects and triggers milestone tiers!
AchievementManager.AddProgress("goblin_hunter_tiered", 1f);
```

When the player crosses threshold values:
- **Tier 1 (Bronze - 10 kills)**: Triggers Bronze toast + awards 10G.
- **Tier 2 (Silver - 50 kills)**: Triggers Silver toast + awards 25G.
- **Tier 3 (Gold - 100 kills)**: Triggers Gold toast + awards 50G + grants in-game reward item.

---

## Step 4: Add No-Code Physics Triggers

Don't want to write code? Add an **`AchievementTrigger`** component to any 2D or 3D GameObject with a Collider:

1. Select your trigger GameObject (e.g. a secret door or checkpoint volume).
2. Click **Add Component > AchievementTrigger**.
3. Select your Achievement from the dropdown.
4. Set **Trigger Mode**: `OnTriggerEnter3D`.
5. Set **Required Tag**: `Player`.
6. Done! When the player walks into the collider, the achievement automatically unlocks.

---

## Step 5: Test in Play Mode with Platform Simulator

1. Press **Play** in the Unity Editor.
2. Trigger the unlock in your game.
3. Open `Tools > Achievement System Pro > In-Editor Platform Simulator` to toggle between **Steam**, **PS5 Trophy**, **Xbox Gamerscore**, and **Apple Game Center** overlay visuals in real time!
