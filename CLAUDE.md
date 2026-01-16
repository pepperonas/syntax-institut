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
/web-grundlagen/apis/       → Interaktive API-Präsentation (20 Folien)
/frontend/                  → Kategorie-Übersicht (React, Vue, TypeScript)
/backend/                   → Kategorie-Übersicht (Node.js, Datenbanken, REST-API)
/backend/rest-api/          → REST-API Präsentation (10 Folien)
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
4. **Präsentationen** - Vollständige interaktive Slide-Decks:
   - `/web-grundlagen/apis/index.html` - API-Grundlagen (20 Folien)
   - `/backend/rest-api/index.html` - REST-API entwickeln (10 Folien)
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

## Präsentationen

### Einheitliches Design
Alle Präsentationen verwenden das gleiche Grundlayout:
- Embedded CSS/JS (keine externen Abhängigkeiten)
- Farbschema je nach Kategorie (Lila für Web-Grundlagen, Orange für Backend)
- Einheitliche Progress-Bar am unteren Bildschirmrand

### Progress-Bar Template
```css
.slide-progress {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    display: flex;
    align-items: center;
    padding: 10px 25px;
    background: rgba(10, 22, 40, 0.95);
    backdrop-filter: blur(10px);
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    gap: 15px;
}
```

### Navigation Features
- **Loop-Navigation**: Von erster Folie zurück zur letzten, von letzter vor zur ersten
- **Slide Persistence**: Position wird im localStorage gespeichert
- **Hash Navigation**: `#start` setzt auf Folie 1 zurück, `#quiz` springt zum Quiz
- **Keyboard Support**: Pfeiltasten und Leertaste für Navigation

### Neue Präsentation erstellen
1. Kopiere `/web-grundlagen/apis/index.html` als Template
2. Passe Farbschema an (z.B. `#6366f1` → `#f97316` für Backend)
3. Ändere localStorage-Key (z.B. `apis-currentSlide` → `rest-api-currentSlide`)
4. Aktualisiere Breadcrumbs für korrekten Pfad
5. Verlinke von vorheriger Präsentation ("Weiter lernen" Link)

### API-Präsentation (Web-Grundlagen)
Located at `/web-grundlagen/apis/index.html`:
- 20 Folien zu API-Grundlagen
- Slide navigation: `showSlide()`, `navigatePrev()`, `navigateNext()`
- Animation: `startAnimation()`, `replayAnimation()`
- Quiz: `checkQuiz()`, `resetQuiz()` (5 Fragen)
- Farbschema: Lila (`#6366f1`)

### REST-API Präsentation (Backend)
Located at `/backend/rest-api/index.html`:
- 10 Folien zu Express.js und CRUD
- Themen: Setup, Routen, GET/POST/PUT/DELETE, Status Codes, Best Practices
- Verlinkt von API-Präsentation ("Weiter lernen" Link)
- Farbschema: Orange (`#f97316`)

## Features

### Slide Persistence
Alle Präsentationen merken sich die aktuelle Folie:
- Position wird bei jedem Folienwechsel in `localStorage` gespeichert
- Nach Seiten-Refresh wird automatisch zur letzten Folie gesprungen
- `#start` Hash setzt Position zurück und löscht gespeicherten Stand

### Card Buttons
Kategorie-Karten können mehrere Buttons haben:
```html
<div class="card-buttons">
    <a href="apis/index.html#quiz" class="card-button">Zum Quiz</a>
    <a href="apis/index.html#start" class="card-button card-button-secondary">🔄</a>
</div>
```
- Primärer Button (grün): Volle Breite, z.B. "Zum Quiz"
- Sekundärer Button (lila): Kompakt daneben, z.B. Restart-Icon (🔄)

### Quiz System
- 5 Multiple-Choice Fragen pro Präsentation
- Ergebnisse werden in localStorage gespeichert
- Statistik-Seite zeigt Verlauf und Durchschnitt

### Achievements System
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
| `rest-api-currentSlide` | Aktuelle Folie der REST-API-Präsentation |
| `quizResults` | Array mit Quiz-Ergebnissen |
| `achievements` | Freigeschaltete Achievements |
| `userProfile` | Benutzerprofil-Daten |

## Präsentations-Verlinkung

Die Präsentationen sind miteinander verlinkt für einen Lernpfad:
```
APIs verstehen → REST API entwickeln → (weitere folgen)
```

Auf der letzten Folie jeder Präsentation gibt es einen "Weiter lernen" Link:
```html
<div class="link-item">
    <div class="link-icon">🚀</div>
    <div class="link-content">
        <h3>Weiter lernen: REST API entwickeln</h3>
        <a href="../../backend/rest-api/index.html" class="next-link">
            Zur REST API Präsentation →
        </a>
    </div>
</div>
```

## Deployment

GitHub Pages: https://pepperonas.github.io/syntax-institut/

Push to `main` triggers automatic deployment.

## Contact

Martin Pfeffer - martin.pfeffer@celox.io
