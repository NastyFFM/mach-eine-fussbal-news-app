# Plan — Initial MVP

## Strategy
RSS-Feeds via rss2json.com (kein Key) parallel laden, mergen, dedup, anzeigen.
Suche/Filter clientseitig. State (Quellen-Auswahl, letzter Cache) via PulseOS API + localStorage.

## Quellen (RSS Feeds)
| Source | URL | Notiz |
|---|---|---|
| BBC Sport | https://feeds.bbci.co.uk/sport/football/rss.xml | global, englisch |
| Sky Sports | https://www.skysports.com/rss/12040 | Premier League Fokus |
| Guardian | https://www.theguardian.com/football/rss | global |
| ESPN Soccer | https://www.espn.com/espn/rss/soccer/news | US/Global |
| Goal.com DE | https://www.goal.com/de/feeds/news?fmt=rss | deutsch |

Alle Feeds via `https://api.rss2json.com/v1/api.json?rss_url=<encoded>` — oeffentlich, kein Key.

## Schritte

### 1. manifest.json updaten
- icon: "F", color: "#16a34a" (gruen, fussball-rasen)
- outputs: state, selected-article
- dataFiles: ["state"]
- Stack-Check: ✅ Pflichtfelder vorhanden

### 2. index.html aufbauen
**Layout:**
- Header: Titel + Refresh-Button
- Suchleiste (debounced)
- Quellen-Chips (Toggle pro Source)
- Artikel-Liste (Cards mit Bild, Titel, Beschreibung, Source, Datum)
- States: Loading-Skeleton, Empty, Error+Retry
- Footer: Export/Import Backup-Buttons

**JS-Module (alles in einer <script>-Section):**
- `SOURCES` const-Array mit {id, name, url, color}
- `state = { sources: Set, query: '', cache: [], lastFetch }` 
- `saveData()` / `loadData()` mit PulseOS-API + localStorage Fallback
- `fetchAllFeeds()` → Promise.all mit rss2json fuer aktive Sources
- `renderArticles()` → filtert nach query + sortiert nach pubDate
- `dedupArticles(arr)` → nach normalisiertem Titel
- `escapeHtml(s)` fuer XSS-Schutz
- `debounce(fn, ms)` fuer Suche
- `downloadBackup()` / `uploadBackup()`
- PulseOS SDK: `onInput('data')` → setQuery, `emit('selected-article')` bei Klick

**CSS:**
- CSS-Variablen mit Fallbacks: var(--bg, #0d1117), etc.
- Responsive: Grid auto-fill min 320px
- Mobile: Single column unter 600px

### 3. data/state.json initialisieren
Default: `{ "sources": ["bbc","sky","guardian","espn","goal-de"], "query": "", "cache": [], "lastFetch": null }`

### 4. project_tracker.md updaten
- Initial MVP → [~] implemented

### 5. Commit
`feat(mach-eine-fussbal-news-app): initial MVP`

## Stack Compliance Check
- ✅ Vanilla JS, alles in index.html
- ✅ Kein npm, keine Frameworks
- ✅ CSS-Variablen
- ✅ PulseOS SDK
- ✅ Standalone (localStorage Fallback + Backup)
- ✅ Korrekter Ordner (Standalone, neben PulseOS)
