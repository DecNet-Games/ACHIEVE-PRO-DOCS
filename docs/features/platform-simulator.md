---
layout: default
title: In-Editor Platform Simulator
parent: Core Features
nav_order: 6
---

# In-Editor Platform Simulator
{: .no_toc }

Preview and test authentic Steam, PlayStation 5, Xbox, and Mobile notifications directly inside the Unity Editor with zero external SDKs.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🎮 The Zero-SDK Advantage

Traditionally, testing Steam overlays or Game Center banners requires:
- Installing heavy C++ native plugins.
- Running the Steam client locally with an `appid.txt`.
- Deploying to a physical iOS/Android device for every single test.

**ACHIEVE PRO's In-Editor Simulator eliminates this friction entirely.**

---

## 🖥️ Simulated Platform HUDs

In Play Mode, the simulator injects authentic overlays into your Game View:

| Platform | Position & Visual Style |
|:---|:---|
| **Steam Overlay** | Bottom-right dark glass card with Steam badge, achievement icon, and blue title. |
| **PlayStation 5 Trophy** | Top-right translucent toast with Bronze/Silver/Gold/Platinum trophy cues. |
| **Xbox Series X/S** | Bottom-center neon green HUD with Gamerscore `+G` badge. |
| **Apple Game Center** | Top-center frosted glass slide-down pill with Game Center bubbles. |
| **Google Play Games** | Top/Bottom green capsule pill with game controller badge and `+XP` rewards. |
| **Epic Online Services** | Bottom-right dark card with gold accent bar and EOS diamond badge. |

---

## 🎛️ Simulator Controls Window

Open `Tools > Achievement System Pro > In-Editor Platform Simulator` to:
- Switch simulated platform style on the fly.
- Adjust toast display duration and anchor offsets.
- Fire test unlocks across Common, Rare, Epic, and Legendary tiers.
- Audition procedurally synthesized platform chimes without imported audio assets.
