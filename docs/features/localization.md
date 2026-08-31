---
layout: default
title: Localization
parent: Features
nav_order: 10
---

# Localization (I18N)
{: .no_toc }

Translate your achievements to reach a global audience effortlessly.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🌍 Overview

ACHIEVE PRO includes a built-in localization framework that allows you to translate Achievement Titles and Descriptions into multiple languages, switching dynamically at runtime.

## 📝 Setting up Languages

1. Open the **Achievement Studio Hub**.
2. Navigate to the **Localization** tab.
3. Add your target languages (e.g., `English`, `Spanish`, `French`, `Japanese`).
4. Set the **Default Language** (fallback language).

## 🔤 Translating Content

In the Studio Hub, when you select an Achievement, you will see translation fields for each language you've defined. 

You can manually type translations, or use the **CSV Exporter** to send a spreadsheet to your localization team, and import it back once translated.

## 🔄 Switching Languages at Runtime

You can change the active language at runtime via code, and the UI will automatically update on the next popup.

```csharp
// Switch language to French
AchievementManager.Instance.SetLanguage("French");
```

## 🔌 Unity Localization Package Integration

If your project already uses Unity's official `Localization` package, ACHIEVE PRO can bridge to it.

1. Enable the `USE_UNITY_LOCALIZATION` scripting define symbol in your Project Settings.
2. Instead of typing direct translations in the Studio Hub, you can enter the **String Table Key**.
3. ACHIEVE PRO will automatically pull the translated string from your Unity String Tables before displaying the popup.
