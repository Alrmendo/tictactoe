# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the app

Open `tictactoe.html` directly in a browser — no build step, no server needed.

```powershell
Start-Process "tictactoe.html"
```

## Architecture

The entire app lives in a single file (`tictactoe.html`) with inline CSS and JS — no frameworks, no dependencies, no bundler.

**Game state** (module-level JS variables):
- `board` — flat 9-element array of `''`, `'X'`, or `'O'`
- `current` — whose turn it is (`'X'` or `'O'`)
- `over` — boolean that locks the board after a win or draw
- `scores` — `{X, O, D}` object persisted across games in memory

**Rendering** is full re-render on every move: `render()` wipes `#board` innerHTML and rebuilds all 9 `.cell` divs from scratch. DOM state is never the source of truth — `board[]` is.

**Win detection** (`checkWin`) iterates the 8 hardcoded winning index triples (`WINS`) and returns the matching triple or `null`. Called once per move after writing to `board[]`.

**CSS colour palette:**
- Background: `#1a1a2e` / `#16213e` / `#0f3460`
- X accent: `#e94560`
- O accent: `#a8dadc`

## Git workflow

Changes are committed and pushed to `https://github.com/Alrmendo/tictactoe` after each meaningful change. Branch: `master`.
