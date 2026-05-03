# Final Year Project

A first-person 3D puzzle game built in **Unreal Engine 5**. Players bend space, flip gravity, and warp object scale to navigate a dream world.

---

## Story

A patient has spent five years lying in a hospital bed, trapped in a dream realm. As the player, you must solve puzzles across five levels before reclaiming control of your life.

---

## Core Mechanics

### Portal System
Fire a portal gun to place two linked portals on compatible surfaces. Stepping through one instantly transports you to the other, preserving momentum, velocity, and gravity.

- Per-frame scene capture renders each portal's view as a dynamic texture on the opposite portal.
- Teleportation fires only when the player crosses the portal plane, preventing double-teleports.
- The **display plane** offset from the **logic plane** eliminates single-frame view glitches at crossing.
- Distance-based culling turns off scene captures for far portals to save performance.

### Gravity Flip
Look at any surface and flip gravity to walk on it. The entire movement and camera system reorients to your new "down."

- An orthogonal basis `{forward, right, up}` tracks movement independent of world axes.
- A **flip rotator** (change-of-basis) is composed with the **logic rotator** (player input) via quaternion multiplication, keeping pitch/yaw/roll constraints valid on any surface.
- Gram-Schmidt orthogonalization rebuilds the basis on each gravity change.

### Forced Perspective Scaling
Pick up a scalable object and walk around, its physical size changes relative to the surrounding environment.

- The object is rescaled so that its apparent size from the player's viewpoint stays constant as its real-world distance changes.
- A line trace detects nearby surfaces, and the final placement distance is calculated to ensure the scaled object never clips into surrounding geometry.

---

## Levels

| # | Level | Theme |
|---|-------|-----------------|
| 1 | **The Building** | Complexity — a sprawling metropolis with non-Euclidean geometry |
| 2 | **The Station** | Isolation — a cold, silent sci-fi space station in the void |
| 3 | **The Street** | Lost — an urban street with a shifting sense of direction |
| 4 | **The Bedroom** | Nostalgia — a surreal, oversized childhood bedroom |
| 5 | **The Hospital** | Determination — escape the chase of your own shadow |

---

## Inspirations

| Game | Influence |
|------|-----------|
| [Portal (2007)](https://store.steampowered.com/app/400/Portal/) | Portal-based spatial traversal |
| [Superliminal (2019)](https://store.steampowered.com/app/1049410/Superliminal/) | Forced perspective scaling |
| [Metro Gravity (2025)](https://store.steampowered.com/app/2986450/Metro_Gravity/) | Gravity reorientation |
