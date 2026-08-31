---
layout: default
title: HTML Team Report
parent: Studio Editor Tools
nav_order: 6
---

# HTML Team Report
{: .no_toc }

Share your game's achievement database instantly with game designers, QA testers, and stakeholders without opening Unity.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 🌐 Overview

The **HTML Team Report** tool generates a beautifully formatted, standalone web page containing your entire achievement database. This is perfect for team communication, allowing non-developers to review achievement logic, descriptions, and point values.

## 🚀 Generating a Report

You can generate the HTML report directly from the Unity Editor:

### From the Studio Hub
1. Open the **Achievement Studio Hub** (`Tools > Achievement System Pro > Studio Hub`).
2. At the bottom of the window, click the **"🌐 Generate Team Ready HTML Report"** button.

### From the Top Menu
1. Navigate to **Tools > Achievement System Pro > Data > Generate Team HTML Report...**
2. Choose a save destination (e.g., your Desktop or a shared team folder).
3. The report will be saved as `Achievement_Team_Report.html`.
4. A prompt will appear asking if you'd like to open it immediately in your default web browser.

## 📊 Report Contents

The generated HTML file is fully self-contained (no external CSS/JS dependencies) and includes:

- **Achievement ID**: The internal string ID.
- **Title**: The display name of the achievement.
- **Hidden Status**: A visual tag indicating if the achievement is secret/hidden.
- **Description**: The full localized description text.
- **Category**: The grouping category.
- **Points/XP**: The reward value.
- **Type**: Standard, Incremental, etc.
- **State Details**: Current configuration state.

## 🤝 Use Cases

- **QA Testing**: Testers can keep the HTML file open on a second monitor to track which achievements they need to verify.
- **Game Design Review**: Lead designers can review the points distribution and descriptions for typos and balance.
- **Wiki Generation**: Easily copy the generated HTML table into Confluence, Notion, or your internal team wiki.
