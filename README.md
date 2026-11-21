# AI Game Studio Skills

A set of reusable agent skills for building polished HTML5 mobile games with AI assistance.

These are the production rules used at **Dana Games** to ship [Paper Soccer](https://playgama.ai/play/d7nbp5h2yci4vs), a free browser football game made with Phaser 3, TypeScript and three.js. Characters are organic 3D models built on a CC0 human base, then restyled with original clothes, kits and animations. Online 1v1 uses the host platform's multiplayer bridge, with a local AI fallback if no opponent joins.

The skills are written for coding agents (Cursor, Claude Code, Codex, and similar). Drop a skill folder into your agent's skills directory, or paste the `SKILL.md` into the project brief.

## What's in this pack

| Skill | Use it for |
|---|---|
| [studio-game-process](studio-game-process/SKILL.md) | The full production cycle: design doc, art, code milestones, polish, performance, visibility tests, and the release zip |
| [mobile-game-dev-studio](mobile-game-dev-studio/SKILL.md) | Non-negotiable 3D quality, mobile UI, animation, and milestone verification |
| [quality-bar](quality-bar/SKILL.md) | The visual and gameplay bar to check before showing a build |
| [polish-and-qa](polish-and-qa/SKILL.md) | Game feel, procedural audio, and a pre-release bug pass |
| [organic-3d-pipeline](organic-3d-pipeline/SKILL.md) | How to turn a CC0 human base into web-ready character GLBs and batch skins |
| [publish-visibility-gate](publish-visibility-gate/SKILL.md) | An automated layout check that blocks the release zip if buttons are off-screen or too small |

## Recommended workflow

1. **Lock the design first.** Write a short game design document (loop, controls, win/loss, economy, screens). Do not start production art or feature code until the design and a visual concept are approved.
2. **Set a style contract.** Pick one commercial 3D look (for example a vibrant stylized sports style) and apply it only to visuals: silhouettes, materials, lighting and UI. Do not copy another game's mechanics, code or assets.
3. **Build characters the organic way.** Start from a high-quality CC0 human base. Sculpt original clothing as shells, paint kits in code, export a strict GLB contract, then generate many skins from a few meshes. Never assemble people from cubes, and never project a concept image onto the model as the final texture.
4. **Code in playable milestones.** Core rules and touch input, then the match loop and HUD, then shop/skins/progression, then animation and effects. Each milestone must be playable and verified before the next one starts.
5. **Polish like a shipped title.** Hit-stop, camera shake, particles, squash-and-stretch, instant button feedback, and procedural sound if you have no audio yet.
6. **Gate the release.** Measure 60 fps on a real phone when you can. Run an automated visibility test on several phone sizes, including inside a host iframe, and refuse to build the zip if any menu button is clipped, hidden, or too small to tap. Keep the zip under 5 MB for web portals.
7. **Be honest about online.** If the host sandbox blocks third-party backends, use the platform multiplayer API for live matches and keep a local AI fallback. Do not ship a "needs internet" error as the only online state.

## Play the example

Paper Soccer (free, no sign-up): https://playgama.ai/play/d7nbp5h2yci4vs

## Licence

MIT. Use, adapt and share these skills in your own studio or agent setup. Please keep the licence notice.

These documents describe a method. They are not the game source, and they do not include any private keys, account data or third-party reference images.
