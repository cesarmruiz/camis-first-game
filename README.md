# Snake SPA — Project Overview

This repository contains a single-page, front-end-only recreation of the classic Snake game. Everything — markup, styles, logic, and persistence — lives inside [`snake-classic.html`](snake-classic.html), making the project easy to deploy to any static hosting provider.

## Repository structure

```
.
├── README.md             # Project documentation and onboarding guide
└── snake-classic.html    # Self-contained HTML document with CSS and JavaScript
```

## How the game is built

The HTML file structures the interface into a three-row layout (`header`, main panel, `footer`) using CSS Grid. The main gameplay surface is an HTML `<canvas>` element sized to 840×600 pixels, wrapped in a responsive container so it scales down on smaller viewports.

Key UI elements include:

- **Control buttons** (`Start / Pause`, `Reset`) wired to `onclick` handlers.
- **Select dropdowns** for speed, grid size, and wrap mode, each updating runtime configuration.
- **HUD elements** (`Score`, `Best`) updated after every tick.
- **Overlay panel** that displays pause and game-over messages.

## Core game loop

All JavaScript lives in an immediately-invoked function expression (IIFE) to avoid leaking globals. Important components are:

- **State variables** for snake segments, direction, growth counter, apple position, score, wrap mode, and timing information.
- **`reset()`** initializes the grid size, snake position, pending direction, growth amount, and HUD.
- **`tick()`** advances the snake: it applies the latest input direction, wraps or collides based on the current mode, handles apple consumption, score updates, and growth.
- **Rendering helpers** (`drawGrid`, `drawSnake`, `drawApple`, `drawCell`) redraw the entire frame every `requestAnimationFrame` cycle.
- **Input handlers** for keyboard (arrows/WASD) and touch swipe gestures, translating them into `pendingDir` updates.
- **Persistence** via `localStorage` under the key `snake_best_v1`, preserving the best score between sessions.

`requestAnimationFrame(frame)` drives the render loop. Inside `frame()`, the canvas is resized to fit the viewport, the scene is drawn, and a soft timer (`lastTick`) ensures the snake only advances according to the selected speed.

## Working with grid sizing

`resizeGrid()` recomputes how many rows fit vertically for the chosen column count while keeping square cells. The cell size is clamped so the snake always moves on an integer grid, and the dropdown lets players experiment with denser or sparser playfields.

## Extending the project

Ideas for newcomers looking to learn more:

1. **Break the code into modules.** Extract CSS into a standalone stylesheet and move JavaScript into ES modules to practice modern bundling.
2. **Enhance visuals.** Add sprite sheets, background animations, or particle effects by extending the drawing helpers.
3. **Introduce new mechanics.** Examples: power-ups, obstacles, or a timed mode that speeds up automatically.
4. **Add accessibility & UX improvements.** Provide focus styles for buttons, add ARIA live regions for status updates, or implement gamepad support.
5. **Persist full game state.** Use `localStorage` or IndexedDB to store recent runs or settings beyond the high score.

Each enhancement provides a pathway to learn more about Canvas rendering, JavaScript architecture, and front-end deployment workflows.
