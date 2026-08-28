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
| `Q` / `E` | Your two signature moves, each on its own cooldown |
| `F` | **AWAKEN** — plays your striker's awakening cutscene and upgrades both moves |
| `M` | Mute / unmute |
| `Enter` | Advance menus |

## Movesets and awakening

Every striker starts with a **base moveset** of two abilities on `Q` and `E`, each with its
own cooldown. Fill the **awakening gauge** and press `F`: a cutscene plays, and for the rest
of the match that pair is replaced by a stronger **awakened moveset**.

Gauge gains: tackle won **+14**, ball stolen **+12**, shot **+6→14** (scales with charge),
move used **+7**, pass **+5**, dash **+2**, dribbling above jogging speed **+3.2/sec** —
roughly 20–30 seconds of committed play.

| Striker | Base `Q` / `E` | ★ Awakening | Awakened `Q` / `E` |
| --- | --- | --- | --- |
| **Isagi** | Spatial Scan / Direct Shot | **Meta Vision** | Blind Spot / Meta Direct Shot |
| **Bachira** | Monster Feint / Rhythm Dribble | **Monster Unleashed** | Duet / Phase Dance |
| **Chigiri** | Afterburn / Cutback | **Absolute Speed** | Crimson Burst / Blaze Cross |
| **Nagi** | Zero Trap / Lazy Volley | **Genius Awakened** | Trap Master / Cannon Volley |
| **Rin** | Flat Drive / Predator Press | **Predator** | Ultra Long Shot / Snake Bite |
| **Barou** | Shoulder Charge / Hold Up | **King's Pride** | King's Charge / Crowned Strike |

Awakened shots are *ego shots*: they cut the keeper's dive reach to 45%, so they beat him far
more often than a normal strike. Moves that need the ball say so and do nothing without it;
everything else works off the ball — that is the whole point of Blind Spot and Zero Trap.

### The awakening cutscenes

Each awakening lands a hit-stop, clears the HUD, and plays its own motif before the character
cut-in:

- **Isagi — Blind Spot.** The camera climbs into a tactical overhead read. Every marker
  projects the cone of what they can actually see; the gap none of them covers is ringed in
  gold, with the run into it drawn as a dashed path. Then the camera slams back down behind him.
- **Bachira — Duet.** His monster rises out of the dark behind him, eyes and grin lit.
- **Chigiri — No Brakes.** The pitch tears into speed lines and scarlet shockwaves.
- **Nagi — Zero Friction.** The world greys out and freezes into drifting motes.
- **Rin — Tunnel Vision.** Everything but the goal mouth collapses into black.
- **Barou — The Crown.** A crown drops over him as gold rings blow out across the turf.

## Solo training

**SOLO TRAINING** on the select screen drops you onto an empty pitch — no teammates, no
opponents, no clock — with the awakening gauge refilling instantly, so you can run every
move and every awakening back to back.

| Key | Action |
| --- | --- |
| `1`…`6` | Swap striker on the spot (Isagi → Barou, in roster order) |
| `Q` / `E` | Fire the current moveset |
| `F` | Awaken — the gauge refills in about half a second |
| `X` | Drop back to the base moveset |
| `R` | Put the ball back at your feet |
| `G` | Toggle the opposition keeper |
| `T` | Cycle defenders: off → standing targets → chasing |
| `C` | Toggle cutscenes (off = instant restart after a goal) |
| `Esc` | Back to the select screen |

Standing targets don't fight back — they take a hit, get up and walk back to their mark,
which is what you want for Barou's charge and Bachira's phase. Switch them to *chasing*
when you want real pressure. Goals still count and still play their cutscene; the ball
just comes straight back to you afterwards.

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
