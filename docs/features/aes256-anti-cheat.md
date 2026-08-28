---
layout: default
title: AES-256 Anti-Cheat Persistence
parent: Core Features
nav_order: 8
---

# AES-256 Anti-Cheat Persistence
{: .no_toc }

Bank-grade AES-256 encryption, PBKDF2 salt derivation, atomic disk replacement, and multi-slot save profiles.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🔒 Security Architecture

Standard `PlayerPrefs` and raw `.json` files are vulnerable to Cheat Engine, hex editors, and root browser inspections. ACHIEVE PRO employs multiple security safeguards:

1. **AES-256-CBC Encryption**: Standard symmetric block cipher encrypting all serialized achievement buffers.
2. **PBKDF2 Key Derivation**: Custom salt and pepper hashes generating cryptographically robust 256-bit encryption keys.
3. **HMAC-SHA256 Checksums**: Save files contain a cryptographic hash of their inner content. If a player modifies any value with a hex editor, the checksum mismatch is detected and logged.
4. **Atomic Temp Writes (`.tmp`)**: Data is written to a temporary file before replacing the target save file, preventing corruption during power cuts or sudden game crashes.

---

## 💾 Multi-Slot Profile API

Support multiple player character slots with a single line of code:

```csharp
using DecnetGames.AchievementSystemPro;

// Switch active save slot (e.g. for character profiles)
AchievementManager.SwitchSlot("character_warrior_slot");

// List all saved profile slots on this device
List<SaveSlotInfo> slots = AchievementManager.ListAllSlots();
foreach (var slot in slots)
{
    Debug.Log($"Profile '{slot.slotName}': {slot.unlockedCount} Achievements, {slot.earnedGamerscore}G");
}
```
