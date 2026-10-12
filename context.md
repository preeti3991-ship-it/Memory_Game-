# Repository Context

## What this project does

This repository contains a small, responsive browser-based Memory game, also
known as Concentration. The player turns over cards and tries to find every
matching pair. It is implemented with plain HTML, CSS, and JavaScript, with no
external libraries or build step.

## What "Memory Game" means here

The name describes the game's central challenge: remember where symbols are
while revealing cards two at a time and matching identical pairs. The
repository's source and README do not define what the `GHCP` suffix in the
repository name stands for, so this document does not assign it an expansion.

## Features

- Choose a 4x4 board (8 pairs) or a 6x6 board (18 pairs).
- Flip emoji cards, count moves, and time each game.
- Earn a three-, two-, or one-star rating based on the number of moves.
- View the five saved scores, ordered by fewest moves.
- Use a mouse or keyboard (Tab to focus a card, then Enter or Space to flip it).
- Play on mobile and desktop layouts, with card controls labeled for assistive
  technologies.

Scores are saved in the browser's `localStorage` under `memoryGameScores`.
They remain on that browser and origin, rather than being sent to a server.
The five-score list includes both board sizes.

## Project structure

- `memory-game.html` contains the page markup, responsive styles, and all game
  logic, including card shuffling, timer, scoring, and local score storage.
- `README.md` gives a short feature overview and instructions for opening or
  serving the game.

## Run locally

Open `memory-game.html` directly in a modern browser, or start a local server
from the repository directory:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000/memory-game.html>.

## Technology and scope

This is a self-contained front-end project. It has no account system, backend,
network API, package dependencies, or build process. The game and saved scores
run entirely in the browser.
