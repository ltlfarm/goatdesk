# GoatDesk

**Livestock health logging for farmOS — Android app, offline-first**

GoatDesk is a single-file Android app for logging goat (and small livestock) health data in the field and syncing it to a [farmOS](https://farmos.org) instance. It runs inside a WebView APK and is designed for outdoor use on older Android hardware — high contrast, large touch targets, no internet required to log.

GoatDesk is the **reference standard** for the FarmDesk suite. All other modules follow its UI patterns, auth approach, and sync model.

---

## Features

- Log weight, vitals, medication, procedures, hoof care, observations, births, and general activity
- Per-animal dose calculator — enter weight once, doses auto-calculate from saved formulas
- Multi-animal "herd mode" — step through your whole roster in one session
- Task scheduler — create pending tasks in farmOS, complete them with a PATCH (never duplicates)
- Animal profiles with photos, sex, age, type, and notes
- Full history with filters by animal, log type, and severity
- Syncs to farmOS JSON:API — new logs POST, edits and completions PATCH
- Offline-first: all data saved locally first, pushed only when you tap Sync
- Config sync — settings (formulas, logo) stored as a farmOS activity log so all devices stay in sync
- Export/import logs as JSON
- No hardcoded farm data — works with any farmOS instance

---

## Requirements

- farmOS 2.x with JSON:API enabled
- OAuth2 credentials with `farm_manager` scope
- Android 6+ (tested on Samsung Galaxy devices)

---

## Installation

Download the latest APK from [Releases](https://github.com/ltlfarm/goatdesk/releases) and sideload it onto your device.

> **Note:** If you previously had GoatDesk installed with a different signing key, uninstall the old version first. **Sync to farmOS before uninstalling** — local-only data will be lost.

---

## Setup

1. Open the app and tap **Settings → FarmOS Sync**
2. Enter your farmOS URL, username, and password
3. Tap **Fetch** to import your animals and existing logs
4. Start logging

---

## farmOS Integration Notes

- All write operations require `farm_manager` OAuth scope (`farm_worker` returns 0 logs for non-owners)
- Log timestamps are Unix integer strings as required by farmOS
- Task completion uses PATCH on the existing log — never creates a duplicate
- Photos are uploaded as binary POST to the log image endpoint
- Animal list is filtered by `animal_type` term (set type on your animals in farmOS to keep mixed farms clean)

---

## Repository

`github.com/ltlfarm/goatdesk`

APK builds automatically via GitHub Actions on every push to `main`.
