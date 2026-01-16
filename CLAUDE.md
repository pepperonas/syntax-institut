# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Webentwickler-Schulungsplattform für das Syntax Institut mit navigierbarer Verzeichnisstruktur und interaktiven Präsentationen.

## Development

Open `index.html` directly in a browser. For live reload:
```bash
python3 -m http.server 8000
# or
npx serve .
```

## Architecture

### Directory Structure
```
/                           → Startseite (Übersicht aller Kategorien)
/web-grundlagen/            → Kategorie-Übersicht
/web-grundlagen/apis/       → Interaktive API-Präsentation (einziger fertiger Inhalt)
/frontend/                  → Kategorie-Übersicht (React, Vue, TypeScript)
/backend/                   → Kategorie-Übersicht (Node.js, Datenbanken, REST-API)
/tools/                     → Kategorie-Übersicht (Git, Terminal, VS Code)
/statistiken/               → Quiz-Statistiken mit Charts
/achievements/              → Erfolge/Badges System (20 freischaltbare Achievements)
/einstellungen/             → Profil, Export/Import Funktionalität
/assets/styles.css          → Gemeinsame Styles für alle Seiten
/assets/images/             → Bilder (z.B. bean-coffee.jpg für Pause-Folie)
```

### Page Types
1. **Startseite** (`/index.html`) - Karten zu allen Kategorien
2. **Kategorie-Index** (`*/index.html`) - Karten zu Unterthemen mit Quiz- und Restart-Buttons
3. **Platzhalter** (`*/thema/index.html`) - "Inhalt folgt..." Template
4. **API-Präsentation** (`/web-grundlagen/apis/index.html`) - Vollständige interaktive Präsentation
5. **Statistiken** (`/statistiken/index.html`) - Quiz-Ergebnisse mit localStorage und Charts
6. **Achievements** (`/achievements/index.html`) - Gamification mit 20 Badges
7. **Einstellungen** (`/einstellungen/index.html`) - Benutzerprofil und Daten-Export/Import

### Shared Styles (`assets/styles.css`)
- Layout: `.page`, `.container`
- Navigation: `.logo`, `.breadcrumb`, `.breadcrumb-item`
- Cards: `.cards-grid`, `.card`, `.card-title`, `.card-description`
- Card Buttons: `.card-buttons`, `.card-button`, `.card-button-secondary`
- Placeholder: `.placeholder-content`, `.placeholder-icon`, `.back-link`
- Statistics: `.card-stats`
- Colors: `breadcrumb-purple`, `breadcrumb-pink`, `breadcrumb-green`, `breadcrumb-orange`

### API Presentation (Standalone)
Located at `/web-grundlagen/apis/index.html` with embedded CSS/JS:
- Slide navigation: `showSlide()`, `navigatePrev()`, `navigateNext()`
- Animation: `startAnimation()`, `replayAnimation()`
- Quiz: `checkQuiz()`, `resetQuiz()`
- **Slide Persistence**: Aktuelle Folie wird im localStorage gespeichert (`apis-currentSlide`)
- **Hash Navigation**: `#quiz` springt zum Quiz, `#start` setzt auf Folie 1 zurück

### Features

#### Slide Persistence
Die API-Präsentation merkt sich die aktuelle Folie:
- Position wird bei jedem Folienwechsel in `localStorage` gespeichert
- Nach Seiten-Refresh wird automatisch zur letzten Folie gesprungen
- `#start` Hash setzt Position zurück und löscht gespeicherten Stand

#### Card Buttons
Kategorie-Karten können mehrere Buttons haben:
```html
<div class="card-buttons">
    <a href="apis/index.html#quiz" class="card-button">Zum Quiz</a>
    <a href="apis/index.html#start" class="card-button card-button-secondary">🔄</a>
</div>
```
- Primärer Button (grün): Volle Breite, z.B. "Zum Quiz"
- Sekundärer Button (lila): Kompakt daneben, z.B. Restart-Icon

#### Quiz System
- 5 Multiple-Choice Fragen pro Präsentation
- Ergebnisse werden in localStorage gespeichert
- Statistik-Seite zeigt Verlauf und Durchschnitt

#### Achievements System
- 20 freischaltbare Badges
- Fortschrittsbasiert (Quiz-Ergebnisse, Lernzeit, etc.)
- Visuelle Darstellung mit Lock/Unlock Status

## Breadcrumb Navigation

All pages use clickable breadcrumbs:
```html
<nav class="breadcrumb">
    <a href="../../index.html" class="breadcrumb-item breadcrumb-home">🏠</a>
    <a href="../index.html" class="breadcrumb-item breadcrumb-purple">Kategorie</a>
    <span class="breadcrumb-item breadcrumb-pink breadcrumb-current">Thema</span>
</nav>
```

## localStorage Keys

| Key | Beschreibung |
|-----|--------------|
| `apis-currentSlide` | Aktuelle Folie der API-Präsentation |
| `quizResults` | Array mit Quiz-Ergebnissen |
| `achievements` | Freigeschaltete Achievements |
| `userProfile` | Benutzerprofil-Daten |

## Deployment

GitHub Pages: https://pepperonas.github.io/syntax-institut/

Push to `main` triggers automatic deployment.

## Contact

Martin Pfeffer - martin.pfeffer@celox.io
