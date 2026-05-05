# Migaku → Anki Exporter

A Tampermonkey/Violentmonkey userscript that exports decks from Migaku (https://study.migaku.com) to Anki `.apkg` files, or sends cards **directly to Anki** via AnkiConnect.

> **This is a fork by [marlanbar](https://github.com/marlanbar/Migaku-Exporter)** adding AnkiConnect integration on top of the original work.

---

## ⚠️ Attribution

Originally created by **SirOlaf**: https://github.com/SirOlaf/migaku-anki-exporter/  
Forked and extended by **wa-ra-ki**: https://github.com/wa-ra-ki/Migaku-Exporter  
Further extended by **marlanbar**: https://github.com/marlanbar/Migaku-Exporter

---

## Features

- 🔗 **Persistent FAB button** — blue Anki icon always visible on every page. Click to open the exporter.
- 🔎 **Searchable deck list** — filter by language, search by name.
- 📦 **Export as `.apkg`** — one file per deck, or merge multiple decks into one.
- 🃏 **Direct push to Anki** — send cards straight to a running Anki desktop app via AnkiConnect (no file download needed).
- 📝 **Field mapping** — map Migaku fields to your Anki note type fields.
- 📑 **Wordlist export** — export known/learning/ignored words as CSV inside a `.zip`.
- 💾 **Media cache** — images and audio are cached locally to avoid redundant downloads.
- 🎓 **Interactive tutorial** — onboarding for new users.

---

## Installation

1. Install [Tampermonkey](https://www.tampermonkey.net/) (Chrome/Edge) or [Violentmonkey](https://violentmonkey.github.io/) (Firefox/Chromium).
2. Copy the contents of `Javascript.js` into a new userscript in your manager.
3. Visit `https://study.migaku.com/` and wait for the page to fully load.

---

## How to use

### Export as .apkg

1. Click the blue **Anki icon** button (bottom-right corner, visible on all pages).
2. Pick decks from the searchable list (filter by language if needed).
3. Optionally enable **Merge decks** to combine everything into one file.
4. Click **Export selected decks** — the `.apkg` file downloads automatically.
5. Optionally click **Export wordlists** to download known/learning words as CSVs.

### Send directly to Anki (AnkiConnect)

Requires the [AnkiConnect](https://ankiweb.net/shared/info/2055492159) add-on installed in Anki.

1. Open Anki and make sure AnkiConnect is running (default port 8765).
2. Open the exporter and enable **Send to Anki directly**.
3. Click **Connect to Anki** — decks and note types will populate automatically.
4. Select your **target deck** and **note type**.
5. Click **Map Fields** to map each Anki field to the corresponding Migaku field. The mapping is saved automatically.
6. Select your Migaku decks and click **Export selected decks** — cards go straight to Anki. Duplicates are skipped automatically.

---

## Development / Contributing

- Uses `sql.js` (v1.13) to parse Migaku's compressed SQLite deck blobs from IndexedDB.
- Media fetched from Migaku's sync worker using a Firebase bearer token.
- AnkiConnect requests use `GM_xmlhttpRequest` (with `fetch` fallback) to bypass CORS.
- Single-file project — all logic lives in `Javascript.js`. See `AGENTS.md` for conventions.

---

## FAQ

**Q: Where's the Export button?**  
A: Click the blue Anki icon in the bottom-right corner — it's visible on every page.

**Q: Can I merge multiple decks into one file?**  
A: Yes — enable the **Merge decks** toggle before exporting.

**Q: Are images and audio included?**  
A: Yes, always — images and audio are included automatically.

**Q: Where are my exports saved?**  
A: In your browser's default downloads folder (`.apkg`), or directly in Anki when using AnkiConnect.

**Q: Can I customise which Anki fields get which Migaku data?**  
A: Yes — click **Field Mapping** to open the mapping editor.

**Q: Will it add duplicate cards?**  
A: No — when using AnkiConnect, duplicates within the target deck are automatically skipped.
