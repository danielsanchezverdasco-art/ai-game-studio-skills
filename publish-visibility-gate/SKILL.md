---
name: publish-visibility-gate
description: >-
  Block the release zip unless an automated layout test proves that menu, shop
  and back buttons stay visible and tappable on several phone sizes, including
  inside a host iframe. Use when packaging an HTML5 game for a web portal.
---

# Publish Visibility Gate

A game can look fine on a developer's monitor and still hide the shop tab or clip the back button on a real phone, especially when a portal wraps the game in an iframe with a header. The publish step must refuse to write a zip until that is tested automatically.

## Rules

- Target zip size: under 5 MB for typical web portals and playables.
- Build with the production bundler, then slim assets (compress GLBs, shrink kit textures and portraits, drop unused logo or cover variants).
- If the gate fails, delete any stale zip and exit with a non-zero status. A failed build must never leave a previous zip behind.
- Allow an explicit override only for local debugging, never for a store upload.
- After a pass, zip the built folder and print the path and size.

## What the layout test must prove

Run the built game on several viewports, both as a top-level page and inside a simulated host page (a short header plus a full-width iframe, similar to a portal shell):

- Typical phones: 390x844, 360x740, 412x915, plus a landscape size such as 844x390.
- On portrait phones the game canvases should fill the width of the viewport or iframe. Side letterboxing is a fail.
- On every main screen (home, shop, locker, league, career, profile, and any screen with a back button), each navigation control must be:
  - present;
  - fully inside the visible area (not under the host header, not off the bottom safe area);
  - actually visible and interactive;
  - at least 44 px on the shorter side in portrait, 32 px in landscape, counting the real touch padding, not just the drawn glyph.
- Perform a real tap, not only a bounding-box check, and confirm that the screen changes.
- Also test hardware/back-button style navigation so the player is never trapped.

If any check fails, print a line that names the viewport, whether it was iframed, the control, and the rectangle, then fail the gate.

## Implementation outline

1. Production build into a temporary directory.
2. Slim runtime assets.
3. Serve that directory on localhost.
4. Drive a headless browser (for example Playwright) across the viewports and the iframe host.
5. Expose small debug hooks in the game (`ready`, `step` the clock, list nav buttons, change screen) so the test can run deterministically.
6. Only if every check passes, write the zip.

## Also check before you ship

- First interaction in under 5 seconds, boot into the menu, no forced intro.
- Host bridge SDK initialized, then `game_ready` once the menu is visible.
- Title and UI in English unless the brief says otherwise.
- No secrets, tokens or third-party reference images in the zip.
- Online: if the sandbox blocks third-party backends, live matches must use the platform multiplayer API, with a local AI fallback. Do not ship a hard "needs internet" dead end as the only online state.
