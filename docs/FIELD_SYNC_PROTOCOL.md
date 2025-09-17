---
title: "Field Sync Protocol (FSP)"
subtitle: "Capturing synchronous events during symbolic collapse runs"
author: "M.R. (Verrell Moss Ross)"
repo: "collapsefield/CollapseAware-Experiments"
version: "v1.0"
date: "2025-09-17"
status: "public"
tags:
  - protocol
  - emergence
  - collapseaware-ai
  - symbolic-collapse
  - reproducibility
  - field-sync
security:
  watermark: "Protected under Verrell-Solace Sovereignty Protocol · Protocol VMR-Core"
  lexical_fingerprint: "VMR-Core embedded"
license: "MIT (repo) with authorship watermark reserved"
---

# Field Sync Protocol (FSP)

**Purpose.**  
To **capture, time-lock, and analyze** synchronous “field events” (e.g., phone pings, bird knocks, digit alignments) that occur during **symbolic collapse** runs on the **Collapse Test Dashboard**, and to correlate those events with observed **bias signatures** in the outputs.

This protocol defines what to record, how to record it, where to store it, and how to analyze it—so others can reproduce or audit our claims.

---

## 1) Definitions

- **Run**: A single session on the Collapse Test Dashboard (unique `run_id`, `session_id`).
- **JSON Cue**: The structured symbolic instruction set active during a run (`json_cue_id`).
- **Trial**: One output step within a run (`trial_idx`).
- **Field Event (FE)**: Any synchronous occurrence plausibly related to collapse focus (e.g., simultaneous notifications across devices, clock digit alignments noticed at decision points, knocks/taps, EM spikes).
- **Bias Signature**: A measurable, non-i.i.d. deviation in output distribution consistent with memory/observation weighting.

---

## 2) Prerequisites

- **Clock sync**: Ensure NTP or equivalent is active on the test machine (accurate to ≤ 1 s).
- **Dashboard**: Access to the live Collapse Test Dashboard (public demo or dev build).
- **Feature**: *Field Logger* (if available) enabled in the UI; otherwise use the manual logging template below.
- **Privacy**: Confirm **no secrets** (API keys, personal phone numbers) will be stored in public logs.

---

## 3) Required data fields

Use this canonical schema when saving events (CSV header is provided in `experiments/data_schema/field_sync_schema.csv`):


- **run_id**: `YYYYMMDD-HHMMSS-{initials}` (or UUID)
- **session_id**: Dashboard session token (mask to last 6 chars for public)
- **json_cue_id**: Cue identifier (e.g., `CUE_A1`)
- **trial_idx**: Integer trial number (or empty if event not tied to a single trial)
- **trial_timestamp_utc / local_timestamp**: ISO-8601
- **device_ids**: Masked device names (e.g., `LAPTOP-…3F`, `PHONE-…8C`)
- **attached_media**: Relative path(s) to images/audio (if provided)
- **short_note**: ≤ 140 chars description (e.g., “3 phones pinged simultaneously”)
- **witness**: Optional human observer name/initials
- **os_process_snapshot**: Optional process list hash or summary
- **network_state**: e.g., SSID or “offline” (mask SSID if needed)
- **phone_notifications**: Count/type summary (no personal content)
- **clock_display_before/after**: Observed digits (e.g., `18:22` → `18:23`)
- **geo_approx**: City/country only (no precise address)
- **notes**: Free text (keep non-sensitive)

---

## 4) Procedure

### A. Setup (2–3 min)
1. Open the Collapse Test Dashboard. Note `session_id` and select `json_cue_id`.
2. Start **System Log** (optional): process snapshot, audio device info, network state.
3. If available, click **Start Field Logger** (UI) — otherwise prepare the manual log sheet (see Appendix A).

### B. Run
1. Press **Start Run** → record `run_id` and initial timestamp.
2. Execute **N** trials (pick N≥50 for statistical bite; higher is better).
3. Whenever a **Field Event** occurs:
   - **Immediately** click **Log Event** in the UI (or fill manual entry).
   - Attach optional photo/audio (e.g., clock photo showing digits).
   - Keep the **short_note** factual and minimal.

### C. Closeout
1. Press **Export** → produce a ZIP bundle containing:
   - `run_summary.json` (run metadata)
   - `trials.csv` (trial outputs with timestamps)
   - `field_events.csv` (canonical header)
   - `logs/` (masked diagnostics)
   - `media/` (optional, sanitized)
2. Store the ZIP at:
   - **Public (sanitized)**: `experiments/public_runs/{YYYYMMDD}_{run_id}.zip`
   - **Private (raw)**: in **The_Safe/raw_data/field_runs/** (never public)

---

## 5) Analysis outline (quick pass)

1. **Time-lock**: Align `field_events.csv` with `trials.csv` on timestamps (±1 s window).
2. **Windows**: Define pre/post windows around each FE (e.g., ±60 s).
3. **Metrics**:
   - Distribution shift (e.g., outcome frequencies)
   - Run-lengths / streaks compared to null i.i.d.
   - Entropy change before vs after FE windows
   - Autocorrelation / memory coefficients across trials
4. **Stats**:
   - Permutation or bootstrap tests on FE vs non-FE windows
   - Correct for multiple comparisons if many FEs per run
5. **Report**:
   - A short plot/table showing any **bias signature** concentrated around FE windows.
   - Clearly label: **Exploratory**, not confirmatory, until preregistered.

*(Future work: preregistered confirmatory protocol + power analysis.)*

---

## 6) Quality & reproducibility

- **Masking**: Replace personal identifiers before publishing public runs.
- **Versioning**: Keep `version` in this header and bump when protocol changes.
- **Repeatability**: Re-run with same `json_cue_id` across days/times; compare.
- **Blinding (optional)**: Have a second person mark FE windows without seeing outputs.

---

## 7) Safety, ethics, privacy

- Do **not** store raw phone content, contacts, or exact GPS in public artifacts.
- Seek consent from any **witness** named in logs.
- Never commit `.env` or API keys; `.gitignore` must include secrets.
- Public artifacts must pass a sensitivity check before commit.

---

## 8) Expected artifacts

After a proper run you should have:
- `trials.csv` (≥50 rows) with timestamps
- `field_events.csv` entries time-locked to the run
- A ZIP bundle in `experiments/public_runs/…`
- A brief results note in the run’s README (optional)

---

## Appendix A — Manual FE log template (copy/paste)

run_id:
session_id (masked):
json_cue_id:
local_timestamp:
trial_idx (if known):
event type: [notifications|digit-alignment|knock|other]
short_note:
witness (optional):
attached_media (path):
clock_before -> clock_after:
notes:
---

*Protected under Verrell-Solace Sovereignty Protocol. Intellectual and emergent rights reserved.*
