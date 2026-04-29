# Initial MVP — Refined Spec

## Goal
Eine Single-Page-App, die aktuelle Fussball-News aus mehreren oeffentlichen RSS-Feeds aggregiert,
durchsuchbar und filterbar macht. Keine API-Keys, lauffaehig auf GitHub Pages.

## App Type
Standalone PulseOS App (Vanilla HTML/CSS/JS, alles in einer index.html).

## Graph Ports (manifest.json)
- inputs:
  - `data` — Optional eingehende Daten (z.B. Suchbegriff aus anderem App-Node)
- outputs:
  - `state` — Aktueller Zustand (gewaehlte Quellen, Suchbegriff)
  - `selected-article` — Ausgewaehlter Artikel als Objekt {title, link, source, pubDate}

## Data Files
- `state.json` — { sources: string[], query: string, lastFetch: ISO, cache: Article[] }

## User Stories
1. Als Nutzer sehe ich beim Oeffnen der App sofort die neuesten Fussball-News in einer Liste.
2. Als Nutzer kann ich nach Stichworten in den News suchen (z.B. "Bayern", "Champions League").
3. Als Nutzer kann ich Quellen ein-/ausschalten (BBC, Sky, Guardian, ESPN, kicker).
4. Als Nutzer kann ich auf einen Artikel klicken und die Originalquelle in neuem Tab oeffnen.
5. Als Nutzer kann ich die Liste manuell neu laden.
6. Als Nutzer sehe ich Veroeffentlichungsdatum und Quelle bei jedem Artikel.

## Acceptance Criteria
- [ ] App laedt RSS-Feeds via rss2json.com Public API (kein Key noetig).
- [ ] Mindestens 4 Quellen verfuegbar: BBC, Sky Sports, Guardian, ESPN.
- [ ] Artikel-Liste zeigt: Titel, Beschreibung (gekuerzt), Quelle, Datum.
- [ ] Suche filtert clientseitig in Echtzeit (debounced).
- [ ] Quellen-Toggles speichern Auswahl in state.json + localStorage Fallback.
- [ ] Bei Klick auf Artikel oeffnet sich Original-URL in neuem Tab.
- [ ] Loading-State sichtbar waehrend Fetch.
- [ ] Error-State mit Retry-Button bei fehlgeschlagenem Fetch.
- [ ] Empty-State wenn nach Suche keine Treffer.
- [ ] App funktioniert offline mit gecachten Artikeln (cache aus state).
- [ ] Backup Export/Import-Buttons im Footer.
- [ ] CSS-Variablen statt hardcoded Farben.
- [ ] PulseOS SDK Integration: onInput('data') als Suchbegriff, emit('selected-article').
- [ ] Responsive Layout (Mobile + Desktop).

## Edge Cases
- RSS-Proxy down → zeige Error mit Retry, lade aus Cache wenn vorhanden.
- Keine Quelle aktiv → Hinweis "Bitte mindestens eine Quelle auswaehlen".
- Suchbegriff matcht nichts → Empty-State mit Link "Filter zuruecksetzen".
- Doppelte Artikel aus verschiedenen Quellen → dedup nach Title-Hash.
- Artikel ohne Bild → Layout bleibt stabil.

## Out of Scope
- Eigene Kommentare/Bookmarks (kann spaeter kommen).
- Push-Notifications.
- Live-Ticker / WebSocket.
- Bezahlte APIs.

## Stack Constraints (aus techstack.md)
- Vanilla ES6+ JS, alles in index.html.
- Keine npm-Dependencies, keine Build-Tools.
- CSS-Variablen: --bg, --text, --teal, --border, --bg-card, --text-dim.
- Standalone-Faehigkeit: localStorage-Fallback + Backup Export/Import.
