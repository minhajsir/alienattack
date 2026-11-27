# Save Charminar – VR Bubble Smash (WebXR)

A giant UFO hovers over Charminar and fires **red spiky aliens** onto it. Smash **70** to win.
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

## Blue cubes, chests and score
Every 14–22 seconds the UFO releases a smooth **blue cube** that hovers in front of Charminar for ~9 s. Shoot it to open a chest lying on the ground (the lid swings open 120°):
1. **Left chest – knowledge.** A glowing hologram of Charminar and a fact card appear (first fact: built in 1591 by Muhammad Quli Qutb Shah, “four minarets”, granite and lime mortar, moved from Golconda). Later opens show facts on Laad Bazaar, the City of Pearls, Bathukamma and Golconda. On phone/desktop the fact is also shown at the top of the screen (tap to dismiss).
2. **Right chest – Bathukamma treasure.** Flower-shaped Bathukamma blooms, pearls and lac bangles spill out and fly to you for bonus points.

Cubes alternate between the two chests. Blue cubes are *not* aliens: they never count toward the 100 limit.

**Score:** alien +10 · blue cube +50 · Bathukamma flower +30 · bangle +20 · pearl +10. (Winning still needs 70 aliens smashed.)
Edit the facts in the `FACTS` list in `index.html`.

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
