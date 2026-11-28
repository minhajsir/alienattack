# Save Charminar – VR Bubble Smash (WebXR)

A comic intro tells the story: aliens want to steal Charminar. Then a giant UFO hovers over it and fires **red spiky aliens** onto it. Smash **70** to win; if **100** are alive, the UFO abducts Charminar. Shoot the **blue cubes** to open heritage chests (facts, Bathukamma flowers, lac bangles, pearls) for bonus points.

It is night, you are tiny (Charminar, the UFO and the aliens are 10× your size) and you stand 15 m back.

## Folder structure (what to upload to GitHub)
```
your-repo/
├─ index.html              ← the whole game
├─ README.md
├─ images/                 ← the comic intro (6 panels)
│   ├─ story-1.jpg
│   ├─ story-2.jpg
│   ├─ story-3.jpg
│   ├─ story-4.jpg
│   ├─ story-5.jpg
│   └─ story-6.jpg
└─ models/                 ← your 3D models (all lowercase names)
    ├─ charminar.glb       (or charminar.gltf / charminar.fbx)
    ├─ ufo.glb             (or ufo.gltf / ufo.fbx)
    └─ chest.glb           (optional; or chest.gltf / chest.fbx)
```
- `index.html` must be in the **root** of the repo (not inside another folder).
- Names are **case-sensitive** on GitHub Pages: `images/story-1.jpg` ≠ `Images/Story-1.JPG`.
- A `.gltf` needs its `.bin` and texture files next to it (a single `.glb` is simpler).
- Missing models/images never crash the game: placeholders are used and a message shows at the top of the page.

### Upload steps
**Website (easiest):** create a repo → *Add file → Upload files* → drag in `index.html`, `README.md`, the `images` folder and the `models` folder (folders upload with their contents) → *Commit changes*. Files over 25 MB can't be uploaded this way; use git or shrink the model.

**Git:**
```
git init && git add . && git commit -m "Save Charminar VR"
git branch -M main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```
**Publish:** repo → *Settings → Pages → Deploy from a branch → main / (root) → Save*. After 1–2 minutes open `https://<user>.github.io/<repo>/` in the **Meta Quest Browser** and tap **ENTER VR**. After each update, hard-refresh (Ctrl+Shift+R).

## The comic intro
Six panels pop into a grid one by one (3 columns × 2 rows on laptops, 2 columns on phones, 6 across on very wide screens – force with `--cols:6` in the `#grid` CSS). Each panel has a yellow narration caption. **START** at the bottom begins the game and hides the comic. In VR the same comic appears as a wall in front of you with a START ball.

Edit the story in the `COMIC` list near the top of the script in `index.html`: file name and caption per panel, in the order they appear (currently images 5 → 3 → 2 → 1 → 4 → 6).

## Blue cubes, chests and score
Every 14–22 seconds the UFO releases a smooth **blue cube** that hovers in front of Charminar for ~9 s. Shoot it and the **next chest** (four chests lie on the ground facing you) swings its lid open 120°:
1. **Facts** – hologram + fact card (built in 1591 by Muhammad Quli Qutb Shah, “four minarets”, granite and lime mortar, moved from Golconda; later rounds: Laad Bazaar, City of Pearls, Bathukamma, Golconda).
2. **Bathukamma flowers** – 10 flowers fly to you.
3. **Lac bangles** – 12 bangles.
4. **Pearls** – 18 pearls. Then the cycle repeats.

Blue cubes are not aliens: they never count toward the 100 limit.
**Score:** alien +10 · blue cube +50 · flower +30 · bangle +20 · pearl +15. Winning still needs 70 aliens.
Edit `FACTS` and `SPILL` in `index.html` to change facts, counts and values.

## Using your own chest model
Put `chest.glb` (or `.gltf` / `.fbx`) in `models/`. It is scaled, its lid is found, and it is instanced for all four chests.
- Best: the lid is a **separate object named `Lid`** (names containing *lid*, *cap*, *cover*, *top* also work). Unnamed parts: the highest part is the lid.
- A chest made of **one mesh** is cut into base + lid at 55% of its height (`chestSplit` in `CFG`; 0 turns it off).
- Front must face **+Z**, upright. Fix with `chestRot` in `CFG` (e.g. `[0,180,0]`). Size: `chestWidth`.
- The status text at the top-left of the page says `Chest model loaded (x4)`; if your model can't be used, a red message says why (and the console lists `Chest model parts`).

## Controls
**Quest 3 (controllers or hand tracking)**
- **Right hand = shotgun.** Trigger (or pinch) fires 12 pellets; a red laser shows your aim.
- **Left hand = spin Charminar.** Hold grip (or pinch) and sweep sideways like a turntable. The thumbstick also spins it.
- The **score panel** is a single line in the lower part of your view and follows your gaze: START / PLAY AGAIN, MUSIC, EXIT (press EXIT twice). Shoot or poke the buttons.

**Phone:** the comic shows first. Tap *Enable motion sensor* (bottom-left), then START. Gyro look-around, ◀ ▶ (or swipe) to walk around Charminar, tap aliens. A one-line bar shows the score with PLAY AGAIN, 🔊 and ✕ Exit.
**Desktop:** drag to orbit, click aliens and buttons.

A quiet procedural music track starts after your first tap/click (`MUSIC_VOL` in `index.html`).

## Tweaking (`CFG` at the top of the script)
`worldScale` (10), `playerDistance` (15), `charminarRot` / `ufoRot` (fix lying-down or backwards models), `gunHand` (`'right'`/`'left'`), `winAt`, `loseAt`, `bubbleR`.

## Performance tips for Quest
Charminar under ~100k triangles, textures ≤ 2048 px, ideally a single `.glb` under ~15 MB.
