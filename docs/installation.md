---
layout: default
title: Installation
nav_order: 2
parent: Docs
---

# Installation & Setup
{: .no_toc }

Complete setup guide for importing and configuring **ACHIEVE PRO** in your Unity project.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🛒 Commercial License Notice

> ### ⚠️ Commercial Asset Notice
> **ACHIEVE PRO** is a premium commercial tool distributed exclusively through the **[Unity Asset Store](https://assetstore.unity.com)**.
> This GitHub documentation repository is for technical reference and guides only — full source code and editor assets are acquired upon purchasing a license from the official Asset Store.

---

## 📦 System Requirements

| Specification | Requirement |
|:---|:---|
| **Unity Version** | Unity 2021.3 LTS, 2022.3 LTS, Unity 6 (6000.x) or newer |
| **Render Pipeline** | Universal Render Pipeline (URP), High Definition Render Pipeline (HDRP), or Built-in Render Pipeline |
| **Platforms** | Windows, macOS, Linux, iOS, Android, WebGL, PlayStation 4/5, Xbox One/Series X/S, Nintendo Switch |
| **Dependencies** | None required! Standard TextMeshPro (TMP) is supported natively with automatic Legacy UI fallbacks. |

---

## 📥 Importing via Unity Package Manager

Once purchased from the Unity Asset Store:

1. Open your Unity Project.
2. Navigate to **Window > Package Manager** in the top menu.
3. In the Package Manager dropdown (top-left), select **Packages: My Assets**.
4. Search for `ACHIEVE PRO` (or `Achievement System Pro`).
5. Click **Download**, then click **Import**.
6. In the Import Unity Package window, keep all assets checked and click **Import**.

```
Assets/
└── AchievementSystemPro/
    ├── Core/             # Engine runtime, persistence, and platform adapters
    ├── Editor/           # Studio Hub, Theme Designer, SFX Studio, and Inspectors
    ├── Models/           # ScriptableObjects and serialization models
    ├── UI/               # Spring physics toast controllers, themes, and galleries
    ├── Examples/         # 4 playable interactive demo environments
    └── Runtime/          # No-code 2D/3D physics and event triggers
```

---

## 🧩 Assembly Definitions (`.asmdef`)

ACHIEVE PRO is split cleanly into isolated assembly definitions to minimize compile times and prevent editor code from leaking into standalone builds:

- `AchievementSystemPro.Runtime.asmdef` — Runtime engine, models, triggers, and UI controllers.
- `AchievementSystemPro.Editor.asmdef` — All editor windows, property drawers, tests, and scene generators.

> ### 💡 Pro Tip: Custom Assembly Linking
> If your game uses custom `.asmdef` assemblies, simply add a reference to `AchievementSystemPro.Runtime` in your project's assembly definition file to access `AchievementManager`, `StatManager`, and `AchievementEvents`.

---

## 🔍 Verification & Health Audit

After importing the package, verify that everything is installed correctly:

1. Open the **Project Validator** via:
   `Tools > Achievement System Pro > Project Validator & Health Check`
2. Click **"Run Automated Diagnostic Audit"**.
3. The auditor will scan your database, verify save directories, check audio references, and confirm theme assignments with green status badges.

---

## 🧪 Running Automated Unit Tests

ACHIEVE PRO includes a built-in automated test suite benchmarked for zero runtime allocations:

1. Navigate to:
   `Tools > Achievement System Pro > Run Automated Test Suite`
2. A comprehensive 16-test suite will execute in under 50ms, confirming:
   - AES-256 roundtrip encryption and tamper checksums.
   - Quest prerequisite dependency resolution.
   - Daily/weekly streak calendar calculation.
   - Multi-stat composite rule evaluation.
   - 100-unlock high-throughput queue stability.
