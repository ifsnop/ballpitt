# ballpit

A physics-based mobile game where balls rain down driven by gravity — tilt your device to change where they fall and flick them out through the side gaps before the screen fills up.

---

## How to play

The machine spawns balls continuously. Your job is to get rid of them before they pile up and fill the screen.

- **Tilt your device** to change the direction of gravity. Balls always fall toward the physical bottom, and they always spawn from the opposite edge.
- **Flick balls** toward the side exit gaps to make them disappear.
- The gaps are on the two walls perpendicular to gravity — tilt enough and the exits move too.
- The machine spawns faster than you can relax. Keep tilting.

On desktop, gravity is fixed downward (g = 9.8 m/s²) and you can drag balls with the mouse.

---

## Controls

| Input | Action |
|---|---|
| Tilt device | Change gravity direction |
| Tap and drag | Grab and throw a ball |
| Release | Ball inherits your throw velocity |

---

## Features

- Live accelerometer input with low-pass filtering for smooth gravity
- Gravity-aware spawn system: balls always enter from the edge opposite to physical down
- 60° hysteresis on edge selection — the spawn and exit walls don't flicker at boundary angles
- WebGL sphere shader with refraction, specular highlights and glow halo
- 2D canvas overlay with motion trails and animated gap indicators
- Exit gap arrows point outward; spawn gap arrows point inward
- Balls and score survive orientation changes and window resizes
- Touch drag pauses the physics runner to prevent burst acceleration on release
- Runs on mobile browsers (iOS and Android) and desktop

---

## Tech stack

- [Matter.js](https://brm.io/matter-js/) — 2D rigid body physics
- WebGL — background grid and ball rendering (refraction shader)
- Canvas 2D — overlay, trails, gap indicators
- DeviceMotion API — accelerometer input
- Vanilla JS, no build step

---

## Running locally

No build step required. Just open the file in a browser:

```bash
git clone https://github.com/ifsnop/ballpit.git
cd ballpit
open ball_physics.html
```

For accelerometer input on mobile, serve over HTTPS — browsers require a secure context for `DeviceMotionEvent`. A quick option:

```bash
npx serve .
# then open the local HTTPS URL on your phone
```

On iOS 13+ the browser will prompt for motion sensor permission on first touch.

---

## Browser support

| Browser | Status |
|---|---|
| Chrome for Android | ✓ Full |
| Safari for iOS | ✓ Full (permission prompt on first touch) |
| Firefox for Android | ✓ Full |
| Chrome / Firefox desktop | ✓ Fixed gravity |
| Safari desktop | ✓ Fixed gravity |

---

## Configuration

All tuning constants live in the `CFG` object at the top of the file:

| Key | Default | Description |
|---|---|---|
| `RADIUS_MIN` | 16 | Smallest ball radius in px |
| `RADIUS_MAX` | 44 | Largest ball radius in px |
| `SPAWN_DELAY` | 140 ms | Interval between spawn bursts |
| `SPAWN_BURST` | 3 | Max balls spawned per burst |
| `MAX_BALLS` | 80 | Soft cap before spawning pauses |
| `EXIT_GAP_FRAC` | 0.425 | Exit gap size as fraction of wall length |
| `RESTITUTION` | 0.88 | Bounciness (0 = dead, 1 = perfectly elastic) |

---

## License

MIT
