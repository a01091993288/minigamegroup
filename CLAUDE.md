# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Zero-dependency browser game collection — 6 standalone HTML files, no build step, no package manager. Open any file directly in a browser.

**Live URL:** https://a01091993288.github.io/minigamegroup/
**Repository:** https://github.com/a01091993288/minigamegroup

## Files

| File | Role |
|------|------|
| `index.html` | Game hub homepage — links to all 5 games |
| `minesweeper.html` | 지뢰찾기 (Minesweeper) |
| `snake.html` | 스네이크 (Snake) |
| `2048.html` | 2048 puzzle |
| `memory.html` | 메모리 카드 (Memory card matching) |
| `breakout.html` | 벽돌깨기 (Breakout) |

## Architecture

Each game is a **self-contained single HTML file**: `<style>` + markup + `<script>` with no external dependencies. Game state lives entirely in JS variables; persistent data (high scores, best times) uses `localStorage`.

Canvas-based games (`snake.html`, `breakout.html`) use `requestAnimationFrame` / `setTimeout` loops.
DOM-based games (`minesweeper.html`, `2048.html`, `memory.html`) manipulate the DOM directly.

### Design System (all files share these values)
```css
--dark:   #1a1a2e   /* page background */
--darker: #16213e   /* panel background */
--card:   #0f2040   /* card background */
--blue:   #0f3460   /* borders/cells */
/* Per-game accent colors */
minesweeper → #e94560 (red)
snake       → #81c784 (green)
2048        → #ffd54f (gold)
memory      → #4dd0e1 (cyan)
breakout    → #ce93d8 (purple)
```

Each game page has a fixed `← 홈` link in the top-left that returns to `index.html`.

## Git & Deploy Workflow

**Auto-commit rule:** Every file change must be committed and pushed immediately.

```bash
cd "C:\Users\User\바탕화면\minigamegroup"
git add <changed files>
git commit -m "메시지"
git push
```

GitHub Pages rebuilds automatically on every push to `master` (source: `/`, branch: `master`). No CI configuration needed.

## Adding a New Game

1. Create `<gamename>.html` following the single-file pattern (shared CSS variables, `← 홈` button, `localStorage` for scores).
2. Add a game card to `index.html` — assign the next unused accent color and update the card grid layout.
3. Commit and push both files together.
