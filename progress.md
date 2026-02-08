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

Updates (2026-02-06):
- Stabilized claw logic: unified cord scaling with ROOF_Y + CLAW_TOP_Y constants, removed dead RELEASING state, fixed credit/turn consumption, guarded close logic until GLB loaded, and corrected motor pitch to use movement magnitude.
- Added neon arcade environment: grid floor + gradient backdrop, fog, dust particles, neon base strips, cyan/magenta lights; moved/realigned chute into machine with emissive rim.
- Added lightweight grab realism with distance/weight chance and slip risk; test mode remains deterministic.
- Mobile-first UI polish: stacked HUD on small screens, resized joystick/drop, improved HUD opacity and z-index.
- Extended render_game_to_text with clawReady and slipRisk plus grabQuality.

Test runs:
- Playwright baseline (2 iterations): PASS (no console errors, claw returns to IDLE).
- Playwright grab realism smoke (custom actions, 1 iteration): PASS (grabQuality/slipRisk present; no errors).
- Note: One Playwright run timed out at 10s with 2 iterations; reran with 1 iteration successfully.
- Deterministic win test (`?test=1` + `B` + drop): PASS (prizeCount 1, tickets 10).

TODOs:
- Optionally add a short on-screen controls hint for first-time players.

Updates (2026-02-08):
- Replaced HUD with overhaul control panel UI, joystick visuals, and compact prize/ticket/turn displays; integrated coin tray + drag-to-slot in panel.
- Added spring-lag wiggle motion and rope/coil/drag-chain visuals; kept custom claw model and existing grab logic.
- Added new prize models (bethany, caleb, connie, maia) alongside existing prizes.
- Applied new floor/ceiling textures to the room and cabinet interior; updated skybox to match textures.
- Added cabinet shell visuals (pillars, glass panels, marquee box) and brightened interior lighting.

Test runs:
- Not run (manual verification recommended for UI + wiggle + rope visuals).

TODOs:
- Run Playwright smoke test and validate joystick/coin drag interactions.

Updates (2026-02-08, later):
- Simplified UI to only the overhaul joystick and drop button (removed other HUD elements).
- Swapped cabinet visuals to an overhaul-style shell (pillars, glass, marquee, rails, chute, retrieval box).
- Reduced prize model scale to roughly half of the previous size.

Test runs:
- Not run (manual verification recommended for cabinet visuals and UI changes).

Updates (2026-02-08, latest):
- Rebuilt cabinet and gantry visuals to match the overhaul layout (scaled to current machine bounds) while keeping the custom claw and gameplay logic.
- Updated rope/coil/drag-chain visuals and anchors to align with overhaul gantry proportions.
- Simplified the UI to only the overhaul joystick + drop button.

Test runs:
- Not run (manual verification recommended).
