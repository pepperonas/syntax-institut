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
/frontend/                  → Kategorie-Übersicht
/backend/                   → Kategorie-Übersicht
/tools/                     → Kategorie-Übersicht
/assets/styles.css          → Gemeinsame Styles für alle Seiten
```

### Page Types
1. **Startseite** (`/index.html`) - Karten zu allen Kategorien
2. **Kategorie-Index** (`*/index.html`) - Karten zu Unterthemen
3. **Platzhalter** (`*/thema/index.html`) - "Inhalt folgt..." Template
4. **API-Präsentation** (`/web-grundlagen/apis/index.html`) - Vollständige Präsentation

### Shared Styles (`assets/styles.css`)
- Layout: `.page`, `.container`
- Navigation: `.logo`, `.breadcrumb`, `.breadcrumb-item`
- Cards: `.cards-grid`, `.card`, `.card-title`, `.card-description`
- Placeholder: `.placeholder-content`, `.placeholder-icon`, `.back-link`
- Colors: `breadcrumb-purple`, `breadcrumb-pink`, `breadcrumb-green`, `breadcrumb-orange`

### API Presentation (Standalone)
Located at `/web-grundlagen/apis/index.html` with embedded CSS/JS:
- Slide navigation: `showSlide()`, `navigatePrev()`, `navigateNext()`
- Animation: `startAnimation()`, `replayAnimation()`
- Quiz: `checkQuiz()`, `resetQuiz()`

## Breadcrumb Navigation

All pages use clickable breadcrumbs:
```html
<nav class="breadcrumb">
    <a href="../../index.html" class="breadcrumb-item breadcrumb-home">🏠</a>
    <a href="../index.html" class="breadcrumb-item breadcrumb-purple">Kategorie</a>
    <span class="breadcrumb-item breadcrumb-pink breadcrumb-current">Thema</span>
</nav>
```

## Deployment

GitHub Pages: https://pepperonas.github.io/syntax-institut/

Push to `main` triggers automatic deployment.

## Contact

Martin Pfeffer - martin.pfeffer@celox.io
