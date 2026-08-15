# Quadrant Chess

A single-page, dependency-free chess app supporting **classic 2‑player chess** and a **4‑player, cross‑shaped board variant** — play locally with friends, against the bot, or in 2v2 teams. Pure HTML/CSS/JavaScript, no build step, no external libraries.

**[Live demo](#)** — enable GitHub Pages on this repo (see below) and paste your link here.

![mode](https://img.shields.io/badge/players-2%20or%204-c99a4a) ![stack](https://img.shields.io/badge/stack-HTML%2FCSS%2FJS-6f4d34)

## Features

- **Main menu** with three modes:
  - **2 Player** — standard 8×8 chess.
  - **4 Player — Free For All** — every player for themselves, on the classic cross‑shaped 14×14 four‑player board (Red / Blue / Yellow / Green).
  - **4 Player — Teams (2 vs 2)** — Red & Yellow vs Blue & Green.
- **Per‑seat Human/Bot toggle** in the setup screen — so "vs Bot" works in *every* mode (1 human vs 1 bot, 2 humans vs 2 bots, any humans/bots mix in 4‑player, etc.).
- Full move legality: pieces can't move into/leave their king in check.
- **Check, checkmate, and (in 2‑player) stalemate** detection.
- **Castling** (king‑side & queen‑side) and **en passant**, standard chess rules.
- **Pawn promotion** with a piece‑choice popup (Queen / Rook / Bishop / Knight).
- 4‑player **elimination**: a checkmated player's pieces are removed and turns skip them; in Teams mode a side is defeated once both partners are checkmated.
- Turn tracker, captured/remaining-material panel, last‑move and in‑check highlighting.
- Responsive layout — playable on desktop and mobile.
- A simple **bot**: shallow minimax (with alpha‑beta pruning) for 2‑player, and a fast capture/check‑aware heuristic bot for 4‑player.

## How to play

1. Open `index.html` in any modern browser (or visit the GitHub Pages link above) — no server or build step required.
2. Pick a mode from the main menu.
3. On the setup screen, set each color's seat to **Human** or **Bot**, then **Start Game**.
4. Click a piece to see its legal moves highlighted, then click a highlighted square to move.
5. Use **← Menu** any time to leave the game, or **Rematch** from the game‑over dialog to replay the same setup.

## Project structure

```
.
├── index.html        # Menu, setup, and game screens (markup only)
├── style.css          # All styling / theming
├── js/
│   ├── engine.js      # Core rules engine — board, legal moves, check/checkmate, castling, en passant, promotion
│   ├── ai.js           # Bot move selection (minimax for 2P, heuristic for 4P)
│   └── ui.js            # Menu flow, board rendering, click handling, game loop
└── README.md
```

The engine (`js/engine.js`) is written once and generically drives **both** the 2‑player 8×8 board and the 4‑player 14×14 cross board — same piece‑movement code, same check/checkmate logic — configured by board shape and an active player list, so the rules stay consistent across modes.

## The 4‑player board

The board is the standard 14×14 "plus/cross" layout used by popular 4‑player chess variants: a shared 8×8 center with four 8×3 arms, one per player, each holding that player's back rank and pawn row. Turn order is clockwise: **Red → Blue → Yellow → Green**. In Teams mode, partners sit opposite each other (Red+Yellow vs Blue+Green) and cannot capture or block-check each other.

## Known simplifications

This project implements the rules that matter for a genuinely playable game, with a few intentional simplifications versus official/tournament rule sets:

- **No draw by threefold repetition or 50‑move rule.**
- **4‑player stalemate** (a player with no legal moves who isn't in check) simply has their turn skipped, rather than ending the game.
- **Castling is only available in 2‑player mode** — the 4‑player variant's castling rules are non‑standard across implementations, so it's omitted for clarity.
- **Checkmated players are fully eliminated** (their remaining pieces are removed from the board) rather than being "frozen in place," which is the simplest and most common approach among online 4‑player chess implementations.
- Pawn promotion always defaults to auto‑Queen for the bot; humans get a piece‑choice popup.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your default branch and the `/ (root)` folder.
4. Save — your game will be live at `https://buvanesh2406.github.io/4-player-chess/` within a minute or two.

## License

MIT — do whatever you like with it.
