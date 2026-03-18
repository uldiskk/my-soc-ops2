---
description: "Use when: working on the Soc Ops social bingo game, setting up development, or customizing game content and styling."
---

# Soc Ops Workspace Instructions

**Soc Ops** is a React + TypeScript social bingo game for in-person mixers. Players find people matching randomized questions and tap squares to get 5-in-a-row for a win.

## ✓ Mandatory Development Checklist

Before committing, ensure all pass:
- [ ] **Lint**: `npm run lint` — ESLint checks (no unused vars, proper React hooks)
- [ ] **Build**: `npm run build` — TypeScript + Vite compile to `dist/`
- [ ] **Test**: `npm test` — vitest passes (bingoLogic requires 100% coverage)

## Quick Start

```bash
npm install        # Install dependencies
npm run dev        # Start dev server @ http://localhost:5173/ (auto-reload)
```

## Tech Stack

- **React 19** + **TypeScript 5.9** (strict mode)
- **Vite** (build & dev server)
- **Tailwind CSS v4** (CSS-first, `@import "tailwindcss"` in `src/index.css`)
- **Vitest** + **ESLint** for tests & quality
- **Node.js 22+** required

## Project Structure

| Folder | Purpose |
|--------|---------|
| `src/components/` | React UI (GameScreen, BingoBoard, BingoSquare, StartScreen, BingoModal) |
| `src/hooks/` | `useBingoGame` hook (centralized game state & actions) |
| `src/data/` | `questions.ts` (24-question pool + FREE_SPACE) |
| `src/utils/` | `bingoLogic.ts` (board gen, win detection) + tests |

## Game Customization

**Add questions**: Edit `src/data/questions.ts` (simple string array)

**Game flow**: `"start"` → StartScreen → `"playing"` → GameScreen (tap to mark) → `"bingo"` → Win detected → BingoModal → "Back" resets

**Board logic**: `generateBoard()` creates 5×5, shuffles 24 questions, FREE_SPACE at center (index 12). `checkWin()` detects 5-in-a-row (rows/cols/diagonals).

## Styling & Tailwind v4

- Use `@theme` CSS directive in `src/index.css` (NOT `tailwind.config.js`)
- Defaults: bg-white, text-gray-900, custom accent color
- See [tailwind-4.instructions.md](.github/instructions/tailwind-4.instructions.md) for v4 patterns

## Deployment

- **Build**: `npm run build` → `dist/`
- **CI/CD**: GitHub Actions auto-publishes to GitHub Pages on main branch push
- **URL**: `https://{github-username}.github.io/{repo-name}`
- **Setup**: Enable Pages in repo Settings → Deploy from a branch → GitHub Actions

## Common Tasks

| Goal | How |
|------|-----|
| Add questions | `src/data/questions.ts` |
| Change colors | `@theme` in `src/index.css` or Tailwind utilities in components |
| Add animations | Tailwind transitions or `@keyframes` in `src/index.css` |
| Debug game logic | Check `src/utils/bingoLogic.test.ts` + `npm run dev` |
| Modify UI | Edit `src/components/*.tsx` |

## References & Docs

- [README.md](../../README.md) — Quick start
- [.lab/GUIDE.md](../../.lab/GUIDE.md) — Workshop guide
- [Tailwind v4 docs](https://tailwindcss.com/docs)
- [React 19 docs](https://react.dev)

---

**TL;DR**: React bingo game, 24 custom questions, 5×5 board. Modify `src/data/` (questions), `src/components/` (UI), `src/utils/` (logic). Always lint → build → test before commit.
