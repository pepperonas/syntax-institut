# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file HTML presentation about APIs for Syntax Institut. No build system required.

## Development

Open `index.html` directly in a browser. For live reload during development, use any local server:
```bash
python3 -m http.server 8000
# or
npx serve .
```

## Architecture

**index.html** - Complete self-contained presentation with:
- Embedded CSS (~1600 lines) with responsive breakpoints at 1024px, 768px, 480px
- Embedded JavaScript for slide navigation, quiz logic, and API animation
- 20 slides about APIs (definition, REST, HTTP methods, examples, quiz)

**Key CSS sections:**
- Base styles and typography
- Responsive media queries (tablet, mobile landscape, mobile portrait, high DPI, landscape orientation)
- Progress bar and navigation buttons (`.slide-progress`)
- API animation keyframes (`.api-animation`)
- Quiz interactivity (`.quiz-*` classes)

**JavaScript components:**
- `showSlide(n)` / `navigatePrev()` / `navigateNext()` - Slide navigation
- `startAnimation()` / `replayAnimation()` - API data flow animation
- `checkQuiz()` / `resetQuiz()` - Quiz validation

## Deployment

Hosted via GitHub Pages at: https://pepperonas.github.io/syntax-institut/

Push to `main` branch triggers automatic deployment.

## Contact

Martin Pfeffer - martin.pfeffer@celox.io
