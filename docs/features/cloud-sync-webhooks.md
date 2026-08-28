---
layout: default
title: Cloud Sync & REST Webhooks
parent: Core Features
nav_order: 7
---

# Cloud Sync & REST Webhooks
{: .no_toc }

Synchronize player progression across mobile and PC backends with HMAC-SHA256 signatures, conflict resolution, and offline queuing.
{: .fs-6 .text-grey-dk-000 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## ☁️ Supported Backend Architectures

ACHIEVE PRO connects seamlessly to any backend:
- **PlayFab** (Title Data / Player Statistics)
- **Firebase / Firestore**
- **Supabase / PostgreSQL**
- **Custom Node.js / Python / Go REST Webhooks**

---

## 🔒 HMAC-SHA256 Tamper Verification

All cloud payloads dispatched by `CloudSyncAdapter` include an `X-Achievement-Signature` header calculated via HMAC-SHA256 using your private server secret. This prevents packet interception and unauthorized score spoofing.

---

## 📶 `CloudOfflineQueue` Resilience

When players play offline (airplane mode, subway, network loss):
- Unlocks and progress steps are appended to a persistent local queue on disk.
- When network connectivity is restored, the queue automatically drains in chronological order without losing player progress.

---

## 🔀 Conflict Resolution Strategies (`CloudMergeStrategy`)

When syncing between multiple devices:

| Strategy | Behavior |
|:---|:---|
| **`HighestProgressAndLatestTimestamp`** | Takes the highest progress value per achievement and the most recent unlock timestamps (Union merge). |
| **`UnionUnlocks`** | Merges unlocked sets from both client and cloud; never revokes an earned achievement. |
| **`ServerWins`** | Overwrites local client state with the authoritative server payload. |
| **`ClientWins`** | Pushes local client state as authoritative to the server. |
