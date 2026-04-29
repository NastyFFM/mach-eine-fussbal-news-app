# Project Tracker — mach eine fussbal news app

## Setup
- Type: Standalone App
- Folder: /Users/chris.pohl/Documents/GitHub/mach-eine-fussbal-news-app
- Created: 2026-04-29
- Template: frontend
- GitHub: https://github.com/NastyFFM/mach-eine-fussbal-news-app
- Live URL: https://nastyffm.github.io/mach-eine-fussbal-news-app/
- Deployed: 2026-04-29 via GitHub Pages

## Features

| Feature | Branch | Status | Refined | Plan | Progress | Review | Deployed |
|---------|--------|--------|---------|------|----------|--------|----------|
| Initial MVP | main | [x] deployed | [x] | [x] | [x] | [ ] | [x] |

## Description
zeige aktuelle fussballnews an und lass suchen finden und browsen

## MVP Scope
- 5 RSS-Quellen (BBC, Sky Sports, Guardian, ESPN, Goal DE) via rss2json.com
- Volltextsuche (debounced) ueber Titel + Beschreibung
- Quellen-Toggle Chips
- Artikel-Cards mit Bild, Titel, Snippet, Quelle, relativem Datum
- Klick → Original im neuen Tab + emit('selected-article') ueber PulseOS Graph
- localStorage Fallback fuer Standalone (GitHub Pages)
- Backup Export/Import als JSON
- Auto-Refresh wenn Cache > 10 Min alt
