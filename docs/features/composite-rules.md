---
layout: default
title: Multi-Condition Composite Rules
parent: Core Features
nav_order: 3
---

# Multi-Condition Composite Rule Engine
{: .no_toc }

Evaluate complex multi-stat achievements combining `AND`, `OR`, `NOT`, and `N_OF_M` logic without writing custom evaluation loops.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🧠 Why Composite Rules?

Many AAA achievements require multiple game statistics to be satisfied simultaneously:
- *Example*: Slay **100 Bosses** `AND` complete run in **under 120 seconds** `AND` take **zero damage**.

Instead of writing bespoke monitoring coroutines, define a `CompositeRule` directly inside the achievement!

---

## ⚙️ Supported Logical & Comparison Operators

### Logical Operators (`LogicalOperator`)
- **`AND`** — All conditions must evaluate to true.
- **`OR`** — At least one condition must evaluate to true.
- **`NOT`** — None of the conditions can evaluate to true.
- **`N_OF_M`** — Exactly $N$ out of $M$ conditions must evaluate to true.

### Comparison Operators (`ComparisonOperator`)
- `GreaterThan` ($>$)
- `GreaterThanOrEqual` ($\ge$)
- `LessThan` ($<$)
- `LessThanOrEqual` ($\le$)
- `Equal` ($==$)
- `NotEqual` (!=)
- `BetweenInclusive` ($A \le x \le B$)

---

## 💻 Code Example: Updating Game Stats

The game simply feeds raw stats into `StatManager`. The engine automatically computes fractional progress and triggers the unlock when the rule is satisfied:

```csharp
using DecnetGames.AchievementSystemPro;

// Update individual stats anywhere in gameplay
AchievementManager.SetStat("bosses_slain", 100f);
AchievementManager.SetStat("clear_time_seconds", 95f);
AchievementManager.SetStat("damage_taken", 0f);

// StatManager automatically checks all composite rules and triggers unlock!
```
