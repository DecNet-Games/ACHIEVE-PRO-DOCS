---
layout: default
title: Spring Physics & UI Themes
parent: Core Features
nav_order: 5
---

# 2nd-Order Spring Physics & UI Themes
{: .no_toc }

Liquid-smooth toast animations powered by damped harmonic oscillator numerical integration and 5 factory console/genre theme presets.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## ⚡ 2nd-Order Mass-Spring-Damper Physics

Standard Unity linear lerps look rigid and unnatural. ACHIEVE PRO computes real-time 2nd-order differential equations:

$$F = -k \cdot x - c \cdot v$$

- **Stiffness ($k$)**: Controls the responsiveness and snap frequency.
- **Damping ($c$)**: Controls how smoothly the bounce settles into rest.
- **Unscaled Time**: Driven by `Time.unscaledDeltaTime` so animations remain buttery-smooth during pause menus (`Time.timeScale = 0`).

---

## 🎨 5 Factory Console & Genre Theme Presets

ACHIEVE PRO ships with 5 production-ready `AchievementThemeSO` presets:

1. **Xbox Gamerscore Toast**:
   - Carbon dark plate with `#107C11` Xbox neon green accent line.
   - Distinct circular Gamerscore `+50G` badge.
2. **PS5 Trophy Banner**:
   - Translucent midnight backdrop with Platinum/Gold gradient trim.
   - Smooth curved top-right slide transition.
3. **Steam Deck Toast**:
   - Charcoal navy card with `#1A9FFF` Steam blue glow.
   - Compact bottom-right pill notification.
4. **Cyberpunk Hologram**:
   - Electric cyan `#00F0FF` and magenta `#FF003C` dual borders.
   - Holographic glitch shake tremor with high-frequency spring bounce.
5. **Fantasy Parchment RPG**:
   - Aged parchment `#F3E9D2` texture with burnished gold `#C59B27` bevels.
   - Antique sepia serif typography.
