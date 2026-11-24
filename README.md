# Save Charminar – VR Bubble Smash (WebXR)

A giant UFO hovers over Charminar and fires bubble aliens onto it. Smash **70** to win.
If **100** are alive on the monument, the UFO abducts Charminar.

You are tiny: Charminar, the UFO and the aliens are **10× bigger than you**, and you stand about 32 m away.

## Folder layout
```
index.html
models/
  charminar.glb | charminar.gltf | charminar.fbx   <- your model (tried in this order)
  ufo.glb       | ufo.gltf       | ufo.fbx         <- your model
```
Missing models are replaced by simple placeholders, and any load error is printed in a red box at the bottom of the page.

## Host on GitHub Pages
1. Upload everything (keep `models/`). 2. Settings → Pages → `main` / root.
3. Open `https://<user>.github.io/<repo>/` in the Meta Quest Browser and tap **ENTER VR**.

## Controls
**Quest 3 (controllers or hand tracking)**
- **Right hand = shotgun.** Trigger (or pinch) fires 12 pellets with a short pump delay. A red laser shows your aim.
- **Left hand = spin Charminar.** Hold grip (or pinch) and sweep your hand sideways, like turning a turntable. The thumbstick also spins it.
- The floating panel (score, START, EXIT, MUSIC) hovers in front of where you look and follows your head turn. Shoot or poke a button to use it.
- **EXIT** (press twice to confirm) returns to the menu and leaves VR.

**Phone:** tap *Enable motion sensor*, look around with the gyro, use ◀ ▶ (or swipe) to walk around Charminar, tap aliens. **✕ Exit** is at the top right.
**Desktop:** drag to orbit, click aliens and buttons.

## Music
A quiet procedural background track starts after your first tap/click (browsers require this). Toggle with the MUSIC button.
Loudness: `MUSIC_VOL` in `index.html` (default 0.06).

## Tweaking (`CFG` at the top of `index.html`)
- `worldScale` (10): how many times bigger the world is than the player.
- `playerDistance` (32): metres from Charminar.
- `charminarRot` / `ufoRot`: fix models that load lying down or facing the wrong way.
- `gunHand`: `'right'` or `'left'`.
- `winAt`, `loseAt`, `bubbleR`: balance.

## Performance tips for Quest
Keep Charminar under ~100k triangles, textures ≤ 2048 px, ideally a single `.glb` under ~15 MB.
