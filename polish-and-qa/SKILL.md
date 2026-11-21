---
name: polish-and-qa
description: >-
  Use when designing, programming or reviewing any HTML5 game (Phaser, three.js,
  Canvas): write a design document before coding, enforce game feel, add
  procedural sound, and run a bug pass before delivery.
---

# Polish and QA for Web Games

## 1. Design document before code

Before writing code, draft a short GDD with:

- the concept in one sentence, and the audience;
- the main loop (what the player does every 5 seconds, every match, every session);
- exact touch controls and target sizes (88 px where possible, 44 px minimum);
- rules, win / loss / draw conditions, and edge cases;
- progression and economy (coins, shop, skins) if any;
- screens: home, play, pause, end with a fast restart, and shop.

Do not program features until the art direction and the GDD are approved.

## 2. Game feel (required on every important action)

- Impact pause (hit-stop) of 40 to 90 ms on hits, goals and bounces.
- A short camera shake proportional to the impact; never nauseating.
- Particles on impacts, combos and victories.
- Squash-and-stretch, anticipation and easing (cubic or spring). Nothing teleports.
- Immediate visual response on touch (highlight, scale, glow) in under 100 ms.
- Banner and modal transitions with a spring, without blocking input.

## 3. Procedural sound

- Synthesize effects with the Web Audio API (oscillators, noise and envelopes) when you do not yet have original audio: tap, move, bounce, goal, win, lose, purchase.
- Unlock audio after the first tap, provide a mute button that is saved, and keep volume balanced.

## 4. Debugging and error control before delivery

- Cover rules and collisions with automated tests for the edge cases.
- Restart the match 5 times in a row and swap skins: no ghost lines, no live timers left behind, no soft-locks.
- Memory: destroy tweens, timers, listeners, textures and objects on scene change; watch that memory does not grow.
- Measure fps on a phone (target 60) and confirm the console is clean.
- Always deliver complete code, never stubs such as "rest of the code here".
- End with a PASS/FAIL audit summary and list what was fixed.

## 5. Platform

- For web portals and playables, use Phaser 3 + TypeScript + Vite (and three.js when 3D is needed). Avoid a single giant HTML file and avoid heavy engines that blow the size budget.
- Before showing a build, also apply the studio quality bar skill.
