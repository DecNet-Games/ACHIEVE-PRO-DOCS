---
layout: default
title: UI Components
parent: Features
nav_order: 11
---

# UI Components & Galleries
{: .no_toc }

Drop-in UI prefabs for viewing your achievements in-game.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🖼️ The Gallery View

Players need a place to see what they've unlocked and what they are missing. ACHIEVE PRO includes a fully functional, scrollable **Gallery Prefab**.

### Setup
1. Drag the `AchievementGalleryView` prefab from `Assets/AchievementSystemPro/UI/Prefabs` into your scene's Canvas.
2. Hook it up to a button in your pause menu.
3. Call `GalleryController.Show()` to open it.

## 🎨 Customizing the Gallery

The Gallery is built using standard Unity UI (uGUI) and TextMeshPro. 

- **Layout:** Modifying the `GridLayoutGroup` allows you to change between list views and grid views.
- **Styling:** The gallery fully supports the **Theme Designer**. Changing your primary theme color in the Studio Hub will dynamically tint the Gallery's progress bars and headers.

## 📈 UI Progress Bars

We provide a standalone `StatProgressBar` component that you can drop anywhere in your UI.

1. Add the component to a UI Image (Filled).
2. Set the `Target Stat ID` in the inspector (e.g., `trees_chopped`).
3. The bar will automatically subscribe to stat changes and animate its fill amount using spring physics without any additional code.

## 🎮 Gamepad Navigation

The built-in UI components have explicit navigation mapping configured, meaning they work out-of-the-box with controllers (Xbox, PlayStation, Switch) using Unity's EventSystem. Ensure your `StandaloneInputModule` or `InputSystemUIInputModule` is active.
