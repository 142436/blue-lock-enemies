# BLUE LOCK RIVALS — EGO ARENA

A single-file browser football game inspired by *Blue Lock Rivals* (Roblox) and the
**Blue Lock** manga/anime. Everything — the pitch, the strikers, the cut-in cutscenes,
the crowd, and every sound effect — is generated at runtime in one HTML file.

**No build step, no dependencies, no assets.** Open `index.html` in a browser and play.

---

## Play

Open `index.html` directly, or serve the folder:

```bash
npx http-server . -p 8080     # then visit http://localhost:8080
```

Best with sound on. Works in any modern desktop browser; touch controls appear on phones/tablets.

## Controls

| Key | Action |
| --- | --- |
| `W` `A` `S` `D` / arrows | Move (`W` always attacks the far goal) |
| `Shift` or `Space` | Dash — burst of speed with afterimages, costs stamina |
| `J` (hold) | Charge and release a shot. **Hold `A`/`D` while releasing to pick a corner** |
| `J` / `L` (no ball) | Slide tackle — steals the ball and puts the carrier on the floor |
| `K` | Pass to the best-placed teammate |
| `E` | **EGO MOVE** — unleashes your striker's signature ability once the gauge is full |
| `M` | Mute / unmute |
| `Enter` | Advance menus |

Fill the **EGO gauge** by dribbling, tackling, passing and shooting. At 100% you enter
Flow: a cut-in fires, the world slows, and your signature move goes off.

## The roster

| Striker | Role | Ego move |
| --- | --- | --- |
| **Isagi** | Field manipulator | *Direct Shot* — time crawls and the ball is fired into the only gap he can see |
| **Bachira** | Monster dribbler | *Monster Dance* — phases straight through tackles, leaving afterimages |
| **Chigiri** | Absolute speedster | *Crimson Burst* — top speed in a single stride |
| **Nagi** | Genius trapper | *Zero Trap Volley* — kills the ball dead, then detonates it |
| **Rin** | Complete striker | *Ultra Long Shot* — a flat rocket from anywhere |
| **Barou** | The King | *King's Charge* — goes **through** defenders, not around them |

Three rival levels (Rookie / Elite / Monster) change opponent speed, aggression and how
well the keeper reads your shot. Matches are two minutes; the result screen ranks your
ego from D to S.

## Cutscenes

- **Match intro** — a camera sweep over the arena, then cut-ins for you and your rival, then a VS smash.
- **Goal** — slow-motion into the net, an orbiting hero shot of the scorer, their cut-in and quote, then the scoreline.
- **Ego move** — hit-stop, a full-screen cut-in with halftone and speed lines, and the pitch scorched under your feet.
- **Full time** — the camera pulls back over the stadium before the ranking lands.

## How it's built

Everything lives in `index.html` (~2,400 lines) with no libraries.

- **Pseudo-3D renderer** — a hand-rolled perspective camera (yaw / pitch / roll / zoom) over
  a 2D canvas, with Sutherland–Hodgman near-plane clipping so geometry that straddles the
  camera still draws, and painter's-algorithm depth sorting for players, ball and goals.
- **Character art** — every striker is a procedural cel-shaded vector bust (hair silhouettes,
  eye shapes and expressions per character), reused across the select cards, the cut-ins
  and the result screen. On the pitch they are drawn as animated billboard sprites with a
  run cycle, tackle lunges, keeper dives and knockdowns.
- **VFX** — additive particle system with cached glow sprites, ground shockwave rings, motion
  afterimages, ball fire trails, screen shake, chromatic aberration, radial blur, speed lines,
  letterboxing, net ripple simulation and kinetic typography.
- **Audio** — a small Web Audio synth: kicks, whistles, saves, posts, the goal horn, ego
  stingers and a filtered-noise crowd bed that swells as the ball nears a box.
- **Performance** — glow sprite caching, a half-resolution post-processing buffer, a tiled
  halftone pattern, bounded particle/afterimage pools and an adaptive quality pass that drops
  the screen-space effects if the frame budget slips.

## Notes

This is a non-commercial fan tribute. *Blue Lock* is created by Muneyuki Kaneshiro and
Yusuke Nomura; *Blue Lock Rivals* is a Roblox community game. No official assets are used —
all art, audio and code here are original and generated at runtime.
