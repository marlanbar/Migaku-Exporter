# Project Guidelines

## Overview

Tampermonkey userscript that exports Migaku memory cards to Anki — either as `.apkg` files or directly via AnkiConnect.

Single-file project: all logic lives in `Javascript.js`.

## Code Style

- Vanilla JS, no build step, no modules — everything in one IIFE
- Use `var` in older sections for consistency; `const`/`let` in newer code is fine
- No TypeScript, no JSX
- Keep functions concise; prefer the existing module pattern (`const ModuleName = { ... }`)

## Architecture

- `CONFIG` — constants, field names, presets
- `Utils`, `Storage` — helpers and localStorage persistence
- `AnkiConnect` — REST API calls to Anki desktop (port 8765)
- `MediaProcessor`, `MediaHandler` — image/audio fetching, caching, conversion
- `FirebaseAuth` — token retrieval for Migaku's media CDN
- `DatabaseOps` — SQLite queries on Migaku's IndexedDB blobs
- `FieldMapper` — maps Migaku fields to Anki note fields
- `AnkiBuilder` — constructs `.apkg` SQLite databases
- `ExportProcessor` — orchestrates export (both `.apkg` and AnkiConnect paths)
- `UI`, `MappingModal`, `TutorialManager` — DOM manipulation, modals, onboarding
- `robustMigakuLauncher` IIFE at bottom — entry point, FAB injection, recovery logic

## Build and Test

```sh
# Syntax check (no test suite exists)
node --check Javascript.js
```

No dependencies to install — external libs loaded via `@require` in the userscript header.

## Conventions

- Always bump `@version` in the userscript header when making changes
- Use `CONFIG.MIGAKU_FIELDS` as fallback when `FieldMapper.getFieldNames()` returns empty
- AnkiConnect calls go through `GM_xmlhttpRequest` (CORS bypass) with `fetch` fallback
- Persist user preferences in `localStorage` under keys defined in `CONFIG`
- Never remove the FAB button in `destroyUI()` — it lives outside route management
- Run `node --check Javascript.js` before committing
- Commit with `git -c commit.gpgsign=false commit` (no GPG key in this environment)
- Push to `origin` (git@github.com:marlanbar/Migaku-Exporter.git)
