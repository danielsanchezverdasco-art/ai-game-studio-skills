---
name: studio-game-process
description: >-
  Use before starting, producing or reviewing an HTML5 mobile game (Phaser 3 +
  TypeScript + three.js, web portals and playables). Covers the approved cycle
  used on Paper Soccer: organic characters on a CC0 base, batch skins, pitch
  and 3D props, HUD, chests, menu and shop, online play, performance, a
  visibility gate, cover art, audit, icon and release zip, plus mistakes to avoid.
---

# Studio Game Process

Use this **before starting or when reviewing** an HTML5 game aimed at mobile browsers and playable portals (Phaser 3 + TypeScript + three.js). Ship the game in English. The steps are generic; Paper Soccer is the worked example.

## 1. Cycle order (do not skip a step)

1. Studio rules (style, language, size budget, security).
2. Gameplay study with real data (if you have no number yet, write "No data yet").
3. A closed, approved game design document before art production or screen builds.
4. Approved art (concept images are reference only).
5. Code in milestones, each one playable and verified.
6. Polish (centering, HUD, materials, facing, visual bugs).
7. Performance and the visibility test (section 12).
8. A PASS/FAIL audit with 3x screenshots and a side-by-side comparison.
9. Icon, home cover and store art (blocking).
10. Release zip under 5 MB, uploaded to the portal sandbox, then a play link for review.
11. Marketing only after the build is live the way the studio wants it.

One game at a time. Show each advance honestly and list what is still missing. Never call something "done" until you have seen it in the real build (including work that was only requested, not yet verified).

## 2. Humanoid characters (approved organic route)

**Forbidden:** building people from cubes, spheres or other primitives (it looks like a block toy). **Forbidden:** projecting the concept image onto the mesh as the final texture.

Fixed method: start from a high-quality CC0 human base (for example Quaternius Universal Base Characters, full-body hero meshes) and add original work on top: adult athletic proportions (about 5-6 heads tall), clothing as shells, jersey painted in code, hair, facial expressions, renamed bones and animation clips.

Export contract:

- Flat GLB for `GLTFLoader` (no Draco / meshopt / KTX2 in the runtime character slot; `KHR_mesh_quantization` is fine). JPEG textures around 1024 px at quality ~86.
- **Under 1.5 MB** per character.
- Character looks toward +Z, feet at the origin, height scaled to 1.0.
- Minimum clips: `idle`, `celebrate`. Morphs: `Blink`, `WinkL`, `Smile`, `Open`. The game should fall back to `idle` if a clip is missing.
- Contract bones: `root`, `hips`, `spine`, `chest`, `head`, `hair`, `shirt_hem`, `upper_arm.L/R`, `forearm.L/R`, `hand.L/R`, `thigh.L/R`, `shin.L/R`, `foot.L/R`, fingers and `ball`.
- Hide leftover idle props from the base mesh (for example a named `Ball` node) when the model loads.
- In a match, characters look at the play object (`lookTarget`); in menus, they look at the camera. Never stand with their back to the board.

If the CC0 base is not available, model from scratch in the same style. Do not fall back to primitives. Do not replace an approved GLB until the studio asks for it.

Palette and rarities live in a small data file. Typical build steps: assemble the dressed character in Blender, author football clips, export a compatible JPEG GLB, then render 3x portraits and preview frames.

## 3. Few bases, many skins

Few character meshes (Paper Soccer uses 3) and **about 10 skins per category** (kits, balls, trails, pitches), generated in batches from parameters. Rarities common / rare / epic / legendary need a clear frame (grey to blue to violet to gold with an aura).

- A JSON manifest listing characters, default kit, rarity, colours, pattern and path.
- One texture per character and kit, because each base has its own UVs.
- Clothing material named `Kit`. At runtime: `TextureLoader`, `flipY = false`, `SRGBColorSpace`, assign to `material.map`.
- Character and kit are chosen separately (locker tabs). The opponent must not clone your kit.
- **Skins are never shown with a lock icon only.** Show a gold price, and if the player is short on gold, offer a rewarded video. Gold must be useful for something.
- No real-world crests, logos or team names.
- Pitch cosmetics change the look, never the legal measurements.

## 4. Board or pitch

Start from **real proportions** (association football: 105 x 68, goal 7.32, penalty areas 40.32 x 16.5 and 18.32 x 5.5, centre circle 9.15, penalty spot 11). Fit an even grid into a 390 x 844 portrait frame. Paper Soccer sizes: Small 6x10, Medium 8x12, Expert 10x16.

- Play area around 80-85% of the height; slim HUD; decoration only on the border; respect safe areas.
- Touch targets at least 44 px. Ring valid moves on your turn and announce the turn ("YOUR TURN").
- Painted surface (mowing stripes, speckle, wear). Never a flat neon plane.
- Keep measurements in pure rules code with tests.

## 5. 3D props (chests, coins, gems, trophies, logo, buttons)

Commercial toy-like realism: volume, bevels, recognisable materials, varnish only where it belongs, three-point lighting. Render in Cycles at 3x or higher, with a clean alpha. Offer 2-3 3D logo variants.

Known material bug: in Blender 4+, an RGBA `ShaderNodeMix` uses `inputs[0]` (factor), `inputs[6]` / `inputs[7]` (A/B) and `outputs[2]`, not the old `MixRGB` sockets. Soft trophies usually mean a 1x render or a canvas without device pixel ratio. Skin: do not overload `Coat` or drop roughness too far.

## 6. CC0 repositories first

Search first for a CC0 or commercially free 3D asset (Kenney, Quaternius, KayKit, Poly Pizza, Sketchfab CC0, OpenGameArt, Polyhaven, ambientCG, and similar). **Only downloadable 3D models (GLB / glTF / FBX / OBJ), never photos or 2D cut-outs.** Use the asset only if it meets the quality bar and does not look childish; otherwise build in the same style. Credit everything in `CREDITS.md`. No paid packs, and no paid GPU APIs without an explicit yes. Some image-to-3D licences exclude the EU — do not use those for a European studio. Example: the Paper Soccer stadium started from a CC0 football stadium and was improved in code.

## 7. Meta systems

- **Chests** with published loot tables (gold, gems, power-ups, cosmetics), visible odds, duplicates converted to gold, and pity (Paper Soccer: epic by 8, legendary by 20). A different opening animation per chest type.
- **Limited power-ups** with per-turn and per-match caps, including online. Feedback lives off the board. The AI uses the same budget.
- **A complete shop** (gold, gems, chests, skins) with the host's rewarded video API.
- **A clean profile:** 4 key stats plus "MORE STATS"; achievements, equipped skin and banner; display-name change **once** (profanity filter, server-validated). Friend lists need a persistent backend.
- **Animated profile banners** that also appear on the in-match nameplate (including the opponent). Start with a few high-quality ones and add more in updates.
- **Daily missions** (for example 3 per day, gold reward, midnight reset) and achievements with icons.
- **Locker** with a 3D turntable, rarity glow and a spring reveal. No pay-to-win.

## 8. Main menu, HUD and boards

- Approved menu structure: top bar (profile, gold, gems) · logo · **a symmetric row: Daily missions | PLAY (opens ONLINE) | Cup (leaderboard and leagues)** · league subtitle in a capsule ("ONLINE · Bronze League · 0 cups") · chest slots · **a fixed bottom bar: SHOP / LOCKER / BATTLE / LEAGUE / CAREER**. Nothing sits under the bottom bar.
- A back button on every screen (plus Esc / hardware back).
- Slim scoreboard with quality portraits and a ring timer.
- Centering audit on every screen at 390 x 844. In Phaser, a touch rectangle starts at (0, 0).
- Pitch-side boards show only the studio brand, driven by JSON.
- Local fonts, no CDN. `renderer.setPixelRatio(Math.min(devicePixelRatio, 3))`.

## 9. Online

- Use a backend project that belongs to this studio. Never mix credentials or deployment keys from other projects. Keep secrets in the environment, never in the repo or in chat.
- Authoritative matches, matchmaking with a bot fallback after about 12 seconds, a 15-second turn timer, 3 timeouts equal a loss, cups, leagues, seasons, a top 100, and abuse limits. Keep the client isolated (for example under `src/online`).
- Some host sandboxes only allow connections to their own domains. In that case, live 1v1 should go through the platform multiplayer API (rooms, join-or-create, host state sync, messaging). Friend lists and other persistent social data need a backend the host permits. If there is no connection, show a clear notice and let the player face a local bot.
- Wipe test data before release.

## 10. Review

- Screenshot the real build at 390 x 844 with DPR 3. Crop faces, icons, type and edges at 200%: they must stay sharp.
- Compare side by side with the approved references. If the build does not beat them on 3 concrete points, it FAILS.
- Look at every screenshot yourself before sharing it.
- Run unit tests (for example Vitest). No power-up or loot table is "done" without a test.

## 11. Close-out: home cover, icon, marketing and zip

- **Home cover:** only the background changes (logo, buttons and bars stay). Options must be **different in scene and composition**, not the same shot recoloured. Mix shots with and without characters. Do not repeat an object already used in the logo. Use real 3D with depth and light. Drop unused covers from the bundle.
- Icon: 3-4 3D icons that stay readable at 64 px, compared with top store icons; the studio picks one. Then banners, covers (typical portal sizes: 800x800, 1080x1920, 1920x1080), screenshots and short-form video stills.
- Zip under 5 MB, with the host bridge SDK (call `game_ready` after `initialize`, once the menu is visible). English title. First interaction under 5 seconds. 60 fps target. Boot into the menu, no forced intro.
- Upload only when the studio has clearly approved that exact build, then share the play link.

## 12. Performance and visibility test (blocking)

- Performance first: no `getImageData` per texture, adaptive 3D resolution (up to 2x), fewer render passes, shadows on demand, GLB preload with a loading screen. Confirm on a real phone when you can.
- The publish script must run an automatic layout test at 390x844, 360x740, 412x915 and 844x390, including a simulated host iframe, proving that menu, shop and back buttons are visible and tappable (real touch area). If it fails, **do not write the zip**.

## 13. Mistakes already made

| Mistake | How to avoid it |
|---|---|
| Invented or stale measurements | Use real proportions; invalidate them in the GDD; add tests. |
| Tiny board, decoration eating the screen | About 80% of the height for play; slim HUD. |
| Blocky or childish characters | Organic CC0 route plus adult athletic style. |
| Concept projected as the texture | Author original materials. |
| Character facing away from the board | +Z contract and `lookTarget`; check in-game. |
| Base `Ball` node visible in a match | Hide it on load. |
| Lashes the same colour as the hair | Separate materials for eyes and lashes. |
| Beard detaching when the mouth opens | Beard follows jaw weights and morphs. |
| Crossed arms intersecting, stiff fingers | IK plus finger curl; review both clips. |
| Washed-out materials, soft trophies | Correct `ShaderNodeMix` sockets; 3x render; DPR 3; never ETC1S on faces or icons. |
| Stick-figure or outdated portraits | 3x portraits from the approved GLB, used in menu, HUD, profile and rival views. |
| Block crowd, flat grass | Painted or instanced crowd; mowing stripes. |
| Off-centre UI | Audit 390x844, centre and four corners. |
| Rejected emblem or logo | Offer 2-3 3D options and wait for a choice. |
| The same opening for every chest | Distinct clips per type. |
| Hitching gameplay | Section 12, plus a test on a real phone. |
| Shop or buttons invisible on some phones | Scaling plus the visibility gate in the publish script. |
| Locked skins, unused gold | Gold price plus rewarded video. |
| Chaotic profile packed with numbers | 4 key figures plus "MORE STATS". |
| Many rejected covers (same scene, new colour, repeated logo object) | Completely different scenes, quality 3D, no repeated logo object. |
| Calling work "done" when it was only requested | Call it "requested" until you see it in the build. |
| Art before the GDD, late reviews, invented numbers | Follow the cycle, show honest progress, write "No data yet". |
| Tokens or passwords in the repo or in chat | Environment only; grep before every commit. |
