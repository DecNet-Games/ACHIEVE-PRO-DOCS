---
layout: default
title: Best Practices
nav_order: 80
parent: Docs
---

# Best Practices
{: .no_toc }

Guidelines for maintaining a clean, performant, and scalable achievement system.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🏷️ Naming Conventions

Maintain a consistent naming convention for your Achievement and Stat IDs to prevent confusion as your database grows.

**Recommended Approach (Snake Case):**
- `boss_defeat_dragon`
- `collectible_coins_100`
- `streak_login_7days`

**Avoid:**
- `Achievement1`, `Ach2` (Not descriptive)
- `Beat The Game` (Spaces can cause issues in webhooks/APIs)

## 🏗️ Architecture

### Decouple Logic using Events
Avoid tight coupling between your gameplay code and the Achievement System. Instead of checking achievement progress directly inside player scripts, use C# events.

**Good:**
```csharp
// Player Health Script
public event Action OnPlayerDeath;

public void Die() {
    OnPlayerDeath?.Invoke();
}

// Achievement Observer Script
void OnEnable() {
    playerHealth.OnPlayerDeath += () => StatManager.AddProgress("deaths", 1);
}
```

## 🔒 Security

### Don't Trust the Client (For Server-Side Games)
If you are building a competitive multiplayer game, do not unlock achievements directly on the client. Validate the action on your server, and send an RPC back to the client to trigger the UI popup.

### Enable AES-256
Always keep the AES-256 Anti-Cheat enabled for single-player games to prevent players from easily modifying their local save files to unlock everything.

## 🎨 UI & UX

### Avoid Spam
Don't trigger 5 achievements at the exact same moment if possible. While ACHIEVE PRO handles queueing perfectly, it can overwhelm the player. Use **Quest Chaining** to space them out.

### Descriptive Text
Ensure your descriptions clearly state *how* to unlock the achievement. 
- **Poor:** "You did it!"
- **Good:** "Defeat the final boss without taking any damage."
