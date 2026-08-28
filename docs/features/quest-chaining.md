---
layout: default
title: Quest & Dependency Chaining
parent: Core Features
nav_order: 1
---

# Quest & Dependency Chaining
{: .no_toc }

Construct sequential quest trees, RPG storylines, and branching skill progressions with zero manual state checking.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🔗 The Problem with Traditional Progression

In standard games, late-game achievements often accidentally unlock if prerequisites are not meticulously guarded:
- E.g. *A player kills a late-game boss in multiplayer before completing the tutorial.*
- In standard codebases, this requires hundreds of `if (hasCompletedQuest1 && hasCompletedQuest2)` boilerplate checks throughout combat and quest scripts.

---

## 🛡️ ACHIEVE PRO Prerequisite Guard

ACHIEVE PRO moves dependency logic directly into ScriptableObject metadata.

### Evaluation Modes (`DependencyRequirement`)

| Mode | Behavior | Use Case |
|:---|:---|:---|
| **`AllRequired`** | ALL configured prerequisites must be unlocked before this achievement can progress or unlock. | Linear story chapters (Chapter 3 requires Chapter 1 AND Chapter 2). |
| **`AnyRequired`** | Unlocks as soon as AT LEAST ONE prerequisite is completed. | Branching story paths (Join Mages Guild OR Fighters Guild). |
| **`MinimumCount`** | Requires at least $N$ out of $M$ prerequisites to be completed. | Tier 2 Talents (Requires any 3 Tier 1 Talents). |

---

## 🛠️ Configuring in the Studio Hub

1. Select your target achievement in the **Achievement Studio Hub**.
2. Scroll to **🔗 Dependency Chaining (Quest / Tech Trees)**.
3. Choose the **Dependency Logic** (`AllRequired`, `AnyRequired`, `MinimumCount`).
4. Click **"+ Add Prerequisite Achievement"** and drag your prerequisite `AchievementSO` assets into the list.

---

## 💻 C# Code API

```csharp
// Check if an achievement's prerequisites are currently met
bool canUnlock = AchievementManager.ArePrerequisitesMet("chapter_3_boss");

if (!canUnlock)
{
    // Retrieve list of IDs still locking this achievement
    List<string> missing = AchievementManager.GetUnmetPrerequisites("chapter_3_boss");
    Debug.Log($"Locked! Still requires: {string.Join(", ", missing)}");
}
```

When an achievement unlocks, the engine automatically checks if any dependent achievements had their prerequisites satisfied and fires:
```csharp
AchievementEvents.OnPrerequisitesSatisfied += (dependentAch) =>
{
    Debug.Log($"🔓 New Quest Unlocked in Tree: {dependentAch.title}");
};
```
