# Save Charminar – VR Bubble Smash (WebXR)

A giant UFO hovers over Charminar and fires bubble aliens onto it. Smash **70** to win.
If **100** are alive on the monument, the UFO abducts Charminar.

It is night: starry sky, moon, floodlit Charminar and lit windows. You are tiny: Charminar, the UFO and the aliens are **10× bigger than you**, and you stand 15 m back.

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
- A **title card** (story + controls + START) appears in front of you; it disappears when the game starts.
- The **score panel** is a single line in the lower part of your view and follows your gaze. START / PLAY AGAIN, MUSIC and EXIT are on it – shoot or poke them.
- **EXIT** (press twice to confirm) returns to the menu and leaves VR.

**Phone:** a title card shows first. Tap *Enable motion sensor* (bottom-left), then START. Look around with the gyro, use ◀ ▶ (or swipe) to walk around Charminar, tap aliens. A one-line bar near the bottom shows the score with PLAY AGAIN, 🔊 and ✕ Exit.
**Desktop:** drag to orbit, click aliens and buttons.

## Music
A quiet procedural background track starts after your first tap/click (browsers require this). Toggle with the MUSIC button.
Loudness: `MUSIC_VOL` in `index.html` (default 0.06).

## Tweaking (`CFG` at the top of `index.html`)
- `worldScale` (10): how many times bigger the world is than the player.
- `playerDistance` (15): metres from Charminar (10–15 works well; closer = steeper neck angle to see the UFO).
- `charminarRot` / `ufoRot`: fix models that load lying down or facing the wrong way.
- `gunHand`: `'right'` or `'left'`.
- `winAt`, `loseAt`, `bubbleR`: balance.

## Performance tips for Quest
Keep Charminar under ~100k triangles, textures ≤ 2048 px, ideally a single `.glb` under ~15 MB.

Night look: colours are set in the scenery block (`0x…` values), moon/star code is next to the sky, and the two warm floodlights on Charminar are the `PointLight(0xffd9a0, 220, …)` lines.
