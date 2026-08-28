---
layout: default
title: CSV / Excel Batch Importer
parent: Studio Editor Tools
nav_order: 4
---

# CSV / Excel Batch Importer & Exporter
{: .no_toc }

Bulk edit, translate, and balance hundreds of achievements in Microsoft Excel, Google Sheets, or Apple Numbers with 2-way CSV synchronization.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📥 2-Way Spreadsheet Synchronization

- **Export**: Generates a clean, RFC-4180 compliant CSV file containing all project achievements with ID, Title, Description, Type, Target Value, Rarity, Gamerscore Points, and Category columns.
- **Import**: Parses the edited CSV, creates missing `AchievementSO` assets automatically, and updates existing achievements with zero manual inspector clicks.

---

## ⚙️ How to Use

1. Open `Tools > Achievement System Pro > Achievement Studio Hub`.
2. Navigate to the **💾 Data Management** tab (or menu: `Tools > Achievement System Pro > Export Achievements to CSV`).
3. Save the exported CSV file.
4. Edit in Google Sheets / Excel (add new rows or adjust point values).
5. Click **"📥 Import Achievements from CSV"** to batch-apply changes to your project.
