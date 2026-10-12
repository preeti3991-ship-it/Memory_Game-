# Product Requirements Document: Dark Theme

## Summary

Add an optional dark theme to the Memory Game in `memory-game.html`. Players
must be able to switch between the existing light theme and a new dark theme
without changing how the game is played or affecting scores, board selection,
or other existing features.

## Background

The game is a self-contained HTML, CSS, and JavaScript application. Its visual
colors are primarily defined by CSS custom properties, and its best scores are
stored in browser `localStorage`. The current interface uses a light page
background, white panels and card faces, blue card backs and controls, and dark
text.

## Problem

Players who prefer a darker interface or play in low-light environments have
no way to change the game's bright default appearance.

## Goals

- Give players a clear, accessible way to switch between light and dark themes.
- Preserve the current light theme as the default for existing and first-time
  players.
- Remember the player's selected theme across reloads in the same browser.
- Keep all game behavior and existing saved scores intact.
- Ensure the complete interface remains readable and usable in either theme.

## Non-goals

- Redesigning the game or changing its layout, rules, scoring, animations, or
  supported board sizes.
- Adding a backend, external library, build step, or account-based preferences.
- Automatically following the operating system's theme preference. The
  initial theme remains light unless the player explicitly selects dark.
- Changing the existing best-score storage format or removing saved scores.

## Users and user stories

- As a player, I want to turn on a dark theme so the game is more comfortable
  to play in low-light environments.
- As a player, I want to return to the light theme whenever I prefer.
- As a returning player, I want my theme choice to remain selected after I
  reload or reopen the game in the same browser.
- As a keyboard or assistive-technology user, I want the theme control to be
  discoverable, operable, and clearly labeled.

## User experience

- Add a labeled theme control to the existing game controls area, near the
  board-size controls. Use a native button or another semantic control.
- The control must communicate the available action and current theme to
  assistive technology. Its visible label should remain understandable in both
  themes.
- Selecting the control changes the theme immediately without resetting the
  board, timer, move count, rating, matched cards, or best scores.
- The selected theme remains active when the player changes board size, wins
  a game, or starts another game.
- On first visit, show the current light appearance.

## Functional requirements

1. **Theme switching:** Players can switch from light to dark and back using
   the theme control.
2. **Theme persistence:** Save the selection using a new, dedicated
   `localStorage` key. Do not reuse or overwrite `memoryGameScores`.
3. **Startup:** Apply a previously saved valid theme before presenting the
   interactive page, where practical, to avoid briefly showing the wrong
   theme. If no valid theme is saved, use light.
4. **Scope:** Apply the selected theme consistently to the page background,
   text, statistics panel, board-size controls, game cards, best-score panel,
   completion dialog, and focus/hover/active states.
5. **Game state:** Theme changes must not call game initialization or alter
   any current game state.
6. **Compatibility:** Keep the game usable when opened directly as a local
   HTML file and when served by the documented local HTTP server. Do not add
   external assets or dependencies.
7. **Storage resilience:** A missing or unrecognized saved theme must fall
   back to light. If browser storage is unavailable, the game must still load
   and the in-page theme switch must still work for the current page session.

## Visual and accessibility requirements

- Implement theme colors using the existing CSS custom-property approach so
  the two palettes remain easy to maintain.
- Preserve the familiar blue accent while choosing dark-surface, text, border,
  and focus colors with sufficient contrast.
- Keep card faces and backs distinguishable in both themes; matched and
  flipped states must remain visually apparent.
- Keep keyboard focus visibly indicated on the theme control, board-size
  controls, and cards. Do not rely on color alone to communicate state.
- Ensure the theme control works with keyboard input and has an accessible
  name and exposed state (for example, a button with an appropriate pressed
  state).
- Maintain responsive behavior and the existing card-flip animation.

## Acceptance criteria

- [ ] A player can switch between light and dark themes and immediately see
  the whole game interface update.
- [ ] A fresh browser session with no theme preference opens in the existing
  light appearance.
- [ ] After choosing dark, reloading the page restores dark; choosing light
  and reloading restores light.
- [ ] Theme preference uses a separate storage key and leaves existing
  `memoryGameScores` data unchanged.
- [ ] Switching theme during a game preserves the current board, timer,
  moves, rating, and matched/unmatched card states.
- [ ] Changing board size, completing a game, and choosing Play Again do not
  reset the chosen theme.
- [ ] All game controls, panels, cards, and the completion dialog remain
  legible and usable in both themes at desktop and narrow/mobile widths.
- [ ] The theme control is usable with keyboard alone and has a visible focus
  indicator and meaningful accessible name/state.
- [ ] Invalid or unavailable theme storage does not prevent the game from
  loading or playing.
- [ ] The game still works with no external dependencies, both as a directly
  opened HTML file and via the README's local-server instructions.

## Validation plan

1. Open `memory-game.html` with no saved theme and confirm the original light
   appearance and existing game behavior.
2. Switch to dark and inspect the complete interface, including both board
   sizes, hover/focus states, matched cards, and the win dialog.
3. Reload in each theme and confirm the selection persists.
4. Start a game, switch themes mid-game, and verify the board and all displayed
   game statistics remain unchanged.
5. Change board size and use Play Again; verify the theme remains selected.
6. Confirm existing best scores remain visible and unchanged after theme
   switching and reload.
7. Navigate the theme control, board-size controls, and cards using only the
   keyboard.
8. Test at desktop and mobile viewport widths and check the browser console
   for errors.
9. If practical, test with theme storage missing, invalid, or unavailable and
   confirm the game still loads.

## Implementation constraints

- Keep the change focused on `memory-game.html`; no dependencies or build
  configuration are needed.
- Keep the existing light palette visually unchanged.
- Do not clear, migrate, or rewrite best-score data as part of theme selection.
- Report any browser-storage errors using the project's existing error
  handling conventions; do not let a preference-storage failure block play.

## Release readiness

The feature is ready for player testing when all acceptance criteria pass and
the existing game can still be played from start to finish in both themes.
