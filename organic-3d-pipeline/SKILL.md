---
name: organic-3d-pipeline
description: >-
  Turn an approved concept into a web-ready animated character GLB: CC0 human
  base, original clothing shells, code-painted kits, a strict export contract,
  batch skins, and 3x portraits. Use when building or retargeting 3D characters
  for HTML5 games.
---

# Organic 3D Character Pipeline

This is the character method used for Paper Soccer. The goal is an adult, athletic, organic player that holds up next to commercial mobile sports games — not a block figure and not a scanned photo.

## What not to do

- Do not build a person from cubes, spheres or capsules.
- Do not project the concept image onto the mesh as the final texture.
- Do not use image-to-3D output as the shipping model without retopo, original materials and a proper rig.
- Do not use tools whose licence excludes the EU if the studio is in the EU.
- Do not put API tokens in scripts, chats or the repo. Keep them in the environment.

## Preferred route: CC0 base plus original clothing

1. **Start from a high-quality CC0 human base**, for example Quaternius Universal Base Characters (full-body hero meshes). Credit the source.
2. **Normalise the bind pose:** height 1.0, feet at the origin, facing +Z. Adjust proportions toward an adult athletic look (about 5-6 heads tall), with slightly larger hands and a readable neck.
3. **Build clothes as shells**, not as painted skin. Derive shirt, shorts, socks and boots from weight regions, shrink-wrap or Laplace-smooth them with a minimum distance to the body so fabric sits on top, and give hems real thickness. Delete skin that is fully covered.
4. **Paint the kit in code** on a dedicated atlas (light, baked AO, wear, fabric weave, numbers and patterns). One texture per character and kit, because UVs differ per body. The clothing material is named `Kit` so the game can swap it at runtime.
5. **Author face and hair:** separate materials for skin, eyes and lashes (lashes must not inherit hair colour). Add morphs `Blink`, `WinkL`, `Smile` and `Open`. If there is a beard, it must follow jaw weights and morphs.
6. **Rig to the studio bone contract** (see studio-game-process): `root`, `hips`, `spine`, `chest`, `head`, `hair`, `shirt_hem`, arm / leg chains, fingers and `ball`. Add secondary bones for hair and shirt hem.
7. **Animate with IK plus FK.** Minimum clips: `idle` and `celebrate`. Hide leftover props from the source base (for example a `Ball` node) when the model loads in game.
8. **Export a compatible GLB** for `GLTFLoader`: JPEG albedo around 1024 px, optional mesh quantization, no Draco / meshopt / KTX2 in the character runtime slot if the loader is not set up for them. Keep each character under 1.5 MB.
9. **Render 3x portraits** in the same lighting as the game, then downsample with a high-quality filter for menu, HUD, profile and rival views.
10. **Batch skins from parameters.** Few meshes, many kits. A manifest lists rarity, colours, pattern and path. Do not replace an approved GLB until the studio asks.

## Alternate route, if you must start from a concept image

Use this only to get a base form, then throw the projected texture away.

1. Concept in an A or T pose, **arms clearly separated from the torso**, plain background, front and three-quarter views. If the hands are glued to the hips, the generator will fuse them and you cannot raise the arms later without tearing.
2. Matt the background (no floor shadow, no white fringe).
3. Image-to-3D with an allowed open model. Local CPU options are slower and rougher; hosted GPUs need a personal token kept in the environment, never printed.
4. In Blender: voxel remesh, new UVs, **delete the generated UV and projected albedo**, then paint original materials. Dilate UV islands when baking so seams have no halos.
5. Continue from step 5 of the preferred route (face, rig, clips, export, portraits).

Inspect the result at 2x on all sides. Photo-scan look, blur, stretch or a white halo is a fail. Quality beats likeness: a sharp original is better than a faithful but muddy copy.

## Props, not just people

Chests, coins, gems, trophies, logos and buttons follow the same bar: real volume, bevels, readable materials, three-point light, Cycles at 3x or higher, clean alpha. In Blender 4+, RGBA `ShaderNodeMix` uses factor `inputs[0]`, A/B `inputs[6]` and `inputs[7]`, output `outputs[2]`. Soft icons usually mean a 1x render or a canvas without device pixel ratio. Prefer a sharper texture format for faces and icons; highly compressed GPU textures show blocks at 2x.

## Credits

List every CC0 or third-party 3D source in `CREDITS.md`. Do not include third-party reference photographs or their file names in a public repository.
