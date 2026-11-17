# Save Charminar – VR Bubble Smash (WebXR)

A UFO hovers over Charminar and fires bubble aliens onto it. Smash **70** with your hands to win.
If **100** are alive on the monument, the UFO abducts Charminar.

## Folder layout
```
index.html
models/
  charminar.fbx   <- your model
  ufo.fbx         <- your model
```
If the FBX files are missing, simple placeholder models are used so you can still test.

## Put it on GitHub Pages
1. Create a repo and upload everything (keep the `models` folder).
2. Settings → Pages → Deploy from branch → `main` / root.
3. Open `https://<your-user>.github.io/<repo>/` in the **Meta Quest Browser**.
4. Tap **ENTER VR**. Poke the green **START** ball with your finger.

GitHub Pages is HTTPS, which WebXR requires.

## Quest 3 tips
- Enable hand tracking: Settings → Movement tracking → Hand tracking. Controllers also work (orange orbs pop bubbles).
- Keep each FBX under ~25 MB so it loads quickly (embed or place textures properly).

## Tweaking (top of `index.html`, `CFG`)
- `charminarRot` / `ufoRot`: fix models that load lying down or facing the wrong way, e.g. `[-90,0,0]` or `[0,180,0]`.
- `charminarHeight`: size in metres (default 1.6 so it is within arm's reach).
- `charminarPos`: distance in front of you.
- `winAt`, `loseAt`, `bubbleR`: game balance. Spawn rate is in `update()` under `case 'playing'`.
- Very heavy (high-poly) Charminar meshes may slow bubble placement – decimate the model if so.

## Desktop testing
Open the page in a normal browser: drag to orbit, click START, click bubbles.
Serve locally with `python3 -m http.server` (FBX can't load from `file://`).
