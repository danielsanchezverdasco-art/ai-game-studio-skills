---
name: mobile-game-dev-studio
description: >-
  Professional mobile game development workflow enforcing true 3D depth and
  volume (never flat 2D cutouts), project-exclusive assets, flawless mobile
  buttons and a crystal-clear HUD, smooth animation with no cut-and-paste
  snapping, optional visual design prototypes before full production, strict
  scale alignment, and real verification checkpoints at every step. Use when
  building or refining mobile games, designing touch controls, creating
  skins/economy/progression, animating 3D characters, or auditing a build.
---

# Mobile Game Dev Studio

## Summary

Guide mobile game creation from concept to a polished, bug-free, commercial-grade 3D mobile build. Use a strict multi-stage pipeline with real verification gates. Enforce true 3D depth, lighting and volumetric models (never flat boards or sticker cutouts), assets built for this project, reliable touch buttons, crisp HUD information, continuous animation, and clean state resets.

## When to Use

- Building a true 3D mobile game with professional visual quality and no sloppy shortcuts
- Previewing 3 distinct 3D visual design prototypes on the same playable core before full production
- Delivering a complete playable game with custom 3D characters, fluid animation, currency, shop/skins and polished UI
- Designing touch controls, HUDs, safe areas, economies, shops, skins or progression
- Auditing builds, code or asset packages for flat visuals, reused assets, broken buttons or logic bugs

## Core Non-Negotiable Rules

1. **True 3D volume and lighting — never flat or "painted on".** Every world, board, stadium, character, prop and interactive element must be real 3D geometry with thickness, bevels, elevation and perspective. Use a real 3D or isometric camera, key / fill / rim lights, contact shadows, and rich PBR or stylized materials. Never fake 3D with a flat plane and drawn lines or sprite stickers.

2. **Project-exclusive visuals — never search or reuse external images.** Build environments, props, characters, effects, icons and badges for this project using procedural 3D, clean vector primitives and custom materials. Forbidden: scraping the web for images, importing stock PNG/JPG sprites, pasting raster cutouts, or leaving files from unrelated projects. CC0 3D bases used as a starting mesh (then fully restyled) are allowed when the organic-character pipeline says so. Photos and 2D cutouts are not.

3. **Flawless mobile buttons and crystal-clear information.** Buttons must look sculpted, sit in thumb reach and safe areas, have generous hitboxes, and give immediate press feedback. The HUD shows only clear, accurate, live information (score, turn, currency, win/loss) with high-contrast type and no truncation, overflow or overlap on any phone size.

4. **Fluid continuous animation — zero cut-and-paste snapping.** No instant teleporting, frozen poses or disconnected frame jumps. Movement, impacts, character actions and UI transitions use cubic or spring interpolation, velocity curves, anticipation, squash-and-stretch and follow-through.

5. **No half-baked shortcuts.** Never ship unfinished stubs, unhooked skins, misaligned hitboxes or broken rematches. Every feature promised in a milestone must work cleanly.

## Steps

### 1. Lock scope, 3D architecture, mobile ergonomics and the style contract

- **Mobile first:** orientation, thumb zones, tap/drag/swipe targets with a live preview, safe-area framing, and a 60 fps target. Do not rely on hover or tiny desktop controls.
- **Design-only style contract:** pick one commercial 3D look (vibrant stylized sports, toy-like tycoon, bold card-battler framing, and similar) and apply it only to silhouettes, materials, lighting, animation character and UI. Never force an unrelated gameplay genre, and never mix conflicting styles.
- **Unified scale:** one world unit, a shared ground plane (`Y = 0`), and consistent pivots so visuals, colliders and UI line up across resolutions and skin swaps.
- **Clean architecture:** keep gameplay simulation separate from rendering, animation, input and audio, with explicit state machines and teardown.

### 2. Execute in ordered milestones

- **Optional stage 0 — three interactive 3D design prototypes.** Same rules and scale, three distinct looks. Hold back economy and shop until one look is chosen.
- **Milestone 1 — core 3D gameplay and rules.** The mechanic, deterministic rules, win/loss/edge states, and clean touch input.
- **Milestone 2 — match loop, HUD and clean reset.** Turns, sculpted buttons, clear HUD, rematch, and a 100% clean state reset.
- **Milestone 3 — economy, shop and 3D skins.** Currency, saves, a 3D locker preview, and project-exclusive skins wired to live state.
- **Milestone 4 — animation, VFX and final polish.** Continuous interpolation, anticipation, easing, squash-and-stretch, follow-through, and camera/lighting feedback.

### 3. Enforce fluid motion

- Replace snaps with interpolation, anticipation and follow-through.
- Give characters and key props continuous states: idle breathing, anticipation, action, impact squash, celebration, defeat, recovery.
- Animate button presses, banners, rewards and modals without locking input behind slow motion.

### 4. Run real verification gates after every milestone

- **3D and asset audit:** real geometry and lighting; assets built for this project; declared features actually wired.
- **Buttons and HUD audit:** large, spaced, responsive, inside safe areas; numbers and labels accurate and unclipped.
- **Logic and edge cases:** valid and invalid inputs, boundaries, win/loss, and 5+ consecutive restarts with no stale state, while keeping earned currency and equipped items.
- **Scale and animation:** visuals, colliders and logic stay aligned across skins; animation stays smooth under rapid taps.
- When a check fails, classify the cause and fix only the affected module. Report PASS/FAIL and fix failures before the next milestone.

## Gotchas

- A flat board with top-down lines is not 3D. Build real meshes with height, bevels, shadows and lighting.
- Imported PNG cutouts clash and look cheap. Build 3D or vector work for this game.
- Tiny buttons near the notch, overlapping text, or dead buttons after a rematch ruin mobile play.
- A style name is not a gameplay genre. "Tycoon style" means how it looks, not that you must build a business sim.
- Forgetting teardown on restart or skin swap leaves ghost trails, live timers and soft-locks.

## Quality addendum (mandatory)

1. **No reused assets, no searched or cut-out images, no crude placeholders.** Use the strongest tool for each job: procedural 3D and shaders for precise geometry; sculpted or image-to-3D plus retopo for hero characters. Primitive block-outs are a fail for people.

2. **Real depth and one coherent style.** Volume, bevels, material contrast, directional and rim lighting, soft grounded shadows.

3. **Characters and hero assets must not look "code-made".** Pick whatever reaches top-game quality: image-to-3D plus Blender retopo/rig/texture, high-craft modelling, painted textures, or code only if it is indistinguishable from a shipped title.

4. **No edge halos.** Image-to-3D textures need zero white or background fringes. Matte the concept (for example rembg / BiRefNet), then dilate UV islands when baking so seams bleed into the part colour. Inspect at 2x on all sides; any fringe is a fail.

5. **Reference, never cut-out.** Concept art is a visual reference only. Never crop it or project it as the model texture. If you use image-to-3D for a base form, rebuild clean topology and author original materials in Blender. The result must look designed, not scanned. Blur, stretch, photo projection or fringe is a fail.

6. **Quality over likeness.** A sharp character built for this game beats a faithful but blurry scanned copy. Deviate from the concept whenever needed to reach the quality bar.
