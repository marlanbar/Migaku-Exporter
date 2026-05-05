# Migaku → Anki Exporter

A Tampermonkey/Violentmonkey userscript that sends your Migaku memory cards **directly to Anki** via [AnkiConnect](https://ankiweb.net/shared/info/2055492159).

> Fork by [marlanbar](https://github.com/marlanbar/Migaku-Exporter) — AnkiConnect integration on top of the original exporter.

---

## Attribution

Originally created by **SirOlaf**: https://github.com/SirOlaf/migaku-anki-exporter/  
Forked by **wa-ra-ki**: https://github.com/wa-ra-ki/Migaku-Exporter  
Extended by **marlanbar**: https://github.com/marlanbar/Migaku-Exporter

---

## Features

- **Direct push to Anki** — cards go straight into your Anki collection, no file downloads.
- **Auto-connect** — polls AnkiConnect automatically and shows connection status.
- **Field mapping** — map each Anki note type field to the corresponding Migaku field.
- **Searchable deck list** — filter by language, search by name, select multiple.
- **Merge decks** — combine multiple Migaku decks into one Anki deck.
- **Media included** — images and audio uploaded automatically.
- **Duplicate detection** — existing cards are skipped.
- **Persistent button** — blue Anki icon always visible in the corner.

---

## Requirements

- [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/)
- [Anki](https://apps.ankiweb.net/) desktop with [AnkiConnect](https://ankiweb.net/shared/info/2055492159) add-on installed

---

## Installation

1. Install a userscript manager (Tampermonkey / Violentmonkey).
2. Copy the contents of `Javascript.js` into a new userscript.
3. Visit https://study.migaku.com/ — the blue Anki button appears in the bottom-right.

---

## How to use

1. **Open Anki** (with AnkiConnect running on port 8765).
2. Click the blue **Anki icon** on Migaku — it auto-connects and shows "Connected to Anki".
3. Select your **target deck** and **note type** from the dropdowns.
4. Click **Map Fields** to assign each Anki field to a Migaku source field (saved automatically).
5. Pick Migaku decks from the list.
6. Click **Send to Anki** — done.

If Anki isn't open, the status shows "Anki is not open" and the controls are disabled until you open it.

---

## Development

Single-file project — all logic in `Javascript.js`. See `AGENTS.md` for conventions.

```sh
node --check Javascript.js   # syntax check
```

---

## FAQ

**Q: Nothing happens when I click Send to Anki.**  
A: Make sure Anki is open and AnkiConnect is installed. The status indicator should say "Connected to Anki".

**Q: Will it add duplicate cards?**  
A: No — duplicates within the target deck are skipped automatically.

**Q: Are images and audio included?**  
A: Yes, always.

**Q: Can I merge multiple Migaku decks into one Anki deck?**  
A: Yes — enable the **Merge decks** toggle and select a single target deck.
