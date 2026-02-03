Original prompt: Build and iterate a playable web game in this workspace, validating changes with a Playwright loop.

Notes:
- Added deterministic update/render hooks and `window.render_game_to_text` to support automated testing.
- Added fullscreen toggle (key: f) and resize handling.
- Refactored animation loop into update/render for deterministic stepping.
- Fixed claw overshoot by clamping movement steps in MOVING_CORNER/RETURNING and enforcing bounds each frame.
- Added keyboard controls (WASD/Arrow keys + Space) for deterministic movement and drop.
- Added test mode (`?test=1`) with `B` hotkey to place a prize under the claw for deterministic win tests.
- Updated catalog toggle to rely on computed style and reported `catalogVisible` in text state.
- Prizes now removed via parent to keep render state consistent.

Test runs:
- Drop click + wait (360 frames): claw returned to bounds and mode IDLE; turns decremented.
- Fullflow drop click + wait (720 frames): completed without position overshoot.
- Keyboard move-only action: claw moved to x/z ~1.55/1.5 in render state.
- Keyboard move + drop + wait (480 frames): claw returned to origin; turns decremented.
- Win test (`?test=1` + `B` + drop): prizeCount incremented to 1 and tickets to 10.
- Insert coin click: credits 1 and turns 6 confirmed.
- Catalog toggle click: `catalogVisible: true` confirmed and UI visible in screenshot.

TODOs:
- If you want deterministic catalog purchase tests, add action payloads to click catalog items with sufficient tickets.
- Re-run Playwright after any new feature changes.
