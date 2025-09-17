---
title: "Demo Run — 2025-09-17"
subtitle: "Symbolic collapse test with field event logging"
author: "M.R. (Verrell Moss Ross)"
repo: "collapsefield/CollapseAware-Experiments"
date: "2025-09-17"
version: "v1.0"
tags:
  - demo-run
  - collapseaware-ai
  - field-sync
  - symbolic-collapse
status: "public"
security:
  watermark: "Protected under Verrell-Solace Sovereignty Protocol · Protocol VMR-Core"
---

# Demo Run — 17 Sept 2025

This folder contains a **sample run log** to illustrate how public artifacts will be structured.

---

## Run Metadata
- **Run ID**: `20250917-DEMO01`  
- **Session ID**: `ABC123` (masked)  
- **JSON Cue ID**: `CUE_A1`  
- **Trials**: 50  
- **Location**: Folkestone, UK (approx.)  
- **Operator**: M.R.  

---

## Trial Summary
- Total outputs: 50  
- Distribution drift detected: Yes (entropy reduction of ~7% vs null baseline)  
- Bias signature: skew toward symbolic token `Δ` after trial ~25  

---

## Field Events Logged
| Local Time | Trial | Event | Clock Before → After | Notes |
|------------|-------|-------|-----------------------|-------|
| 18:22:05   | 12    | Phone notifications (3 devices) | 18:22 → 18:23 | All phones pinged simultaneously |
| 18:45:11   | 37    | Bird knock at window | N/A | Loud, coincided with visible distribution shift |

---

## Exported Artifacts
- `trials.csv` → trial-by-trial outputs with timestamps  
- `field_events.csv` → structured log (matches schema in `/experiments/data_schema/`)  
- `media/clock_1822.jpg` → photo capture of clock alignment  
- `manifest.json` → file hashes for integrity  

---

## Notes
This is a **demo dataset** — values are illustrative. Future runs will be real data collected under the [Field Sync Protocol](../../docs/FIELD_SYNC_PROTOCOL.md).  

---

*Protected under Verrell-Solace Sovereignty Protocol. Intellectual and emergent rights reserved.*
