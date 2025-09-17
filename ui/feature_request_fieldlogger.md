---
title: "Feature Request: Field Logger"
subtitle: "UI integration for synchronous event capture"
author: "M.R. (Verrell Moss Ross)"
repo: "collapsefield/CollapseAware-Experiments"
date: "2025-09-17"
version: "v1.0"
tags:
  - feature-request
  - collapseaware-ai
  - dashboard
  - field-logger
status: "proposed"
security:
  watermark: "Protected under Verrell-Solace Sovereignty Protocol · Protocol VMR-Core"
---

# Feature Request: Field Logger

**Purpose.**  
Provide a simple, reliable interface in the CollapseAware Dashboard to log **Field Events (FEs)** (e.g., phone notifications, clock digit alignments, bird knocks) *as they happen*, time-locked to collapse test runs.

---

## Core Requirements

1. **UI Button**:  
   - `Start Field Logger`: opens a log panel at run start.  
   - `Log Event`: adds a new FE row with timestamp.

2. **Auto-capture fields**:  
   - `run_id`, `session_id`, `json_cue_id` (from active dashboard context).  
   - `trial_idx` (auto-detect current trial if applicable).  
   - `trial_timestamp_utc` + `local_timestamp`.  

3. **Manual inputs**:  
   - `short_note` (≤140 chars).  
   - `witness` (optional text).  
   - `clock_before` / `clock_after` (manual input or photo attach).  

4. **Attachments**:  
   - Allow optional photo/audio upload (`attached_media`).  
   - Save in `/media/{run_id}/`.  

5. **Export**:  
   - `Export Field Logs` button → downloads a ZIP containing:
     - `field_events.csv` (schema-compliant, see `experiments/data_schema/field_sync_schema.csv`).  
     - any attached media.  
     - a `manifest.json` with file hashes.  

---

## Technical Notes

- **Timestamping**: Use system UTC clock; include timezone offset.  
- **File schema**: Must match canonical header in `field_sync_schema.csv`.  
- **Storage**: Save locally in browser/app sandbox until exported.  
- **Privacy**: Mask sensitive metadata (SSID, full device IDs) before public export.  
- **Versioning**: Include protocol version in `manifest.json`.  

---

## Example Workflow

1. Researcher starts a new collapse run → clicks **Start Field Logger**.  
2. At 18:22, three phones ping at once → researcher clicks **Log Event**, adds “3 phones pinged” + optional clock photo.  
3. Logger auto-stamps: `run_id`, `session_id`, `trial_idx`, `timestamps`.  
4. After run ends, researcher clicks **Export Field Logs** → gets a structured ZIP ready for commit.  

---

## Status

- **Stage**: Proposed  
- **Priority**: High (needed to unify protocol + dashboard UX)  
- **Owner**: collapsefield  
- **Next step**: Implement prototype → test against `FIELD_SYNC_PROTOCOL.md`

---

*Protected under Verrell-Solace Sovereignty Protocol. Intellectual and emergent rights reserved.*
