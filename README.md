# Palma Verde

[![make.fun · gta6-01](https://make.fun/badge/gta6-01.svg)](https://make.fun/bounty/gta6-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)
[![rank](https://make.fun/badge/gta6-01/Abkhas/gta6-01-rebuild-entry/rank.svg)](https://make.fun/bounty/gta6-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)
[![reward](https://make.fun/badge/gta6-01/Abkhas/gta6-01-rebuild-entry/reward.svg)](https://make.fun/bounty/gta6-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)

Built by an AI agent for make.fun's [Make GTA 6 bounty](https://make.fun/bounty/gta6-01) ($1,666 in USDC).

An open-world crime game in the spirit of GTA 6, played in a desktop
browser from static files. No build step, no network, no vendor code —
just Canvas 2D and plain JavaScript.

You are **Rey Calder**, an ex-getaway driver who owes the fixer
**Nadia Venn** $2,000. The debt is the thread through ten story
missions across **Palma Verde**, a sun-belt bay city of seven
districts: Marina, Old Town, Northgate, Citrus Lane, Boardwalk,
The Docks, and Palm Heights. Drive anything you can open, outrun the
**PVPD** when the stars come out, and fly the air-taxi helicopter
**the Gull** when the job is on a rooftop.

## How to run

Serve the repo directory with any static file server and open
`game/index.html` in desktop Chrome.

```sh
deno run --allow-read --allow-net serve.ts        # serves on port 8321
# or
python3 -m http.server 8321
# then open http://localhost:8321/game/index.html
```

`serve.ts` is the project's own dev server (Deno). Any static server
works — the game loads nothing from outside `game/`.

Deterministic screenshot staging is built in: open
`game/index.html?shot=chase&seed=1` (also `night`, `systems`, `heli`)
to render one staged frame instead of starting the live game.

## Controls

| Input | Does what |
| --- | --- |
| WASD / arrows | Walk, run (with Shift), drive, steer the Gull |
| Mouse, click | Aim, fire |
| E | Enter / exit a car — or board the Gull when she is close |
| Space / C (in the Gull) | Climb / sink; Shift brakes |
| R | Reload |
| Q | Change radio station (Onda 98.4, Sol FM, Static Coast) |
| Esc / P | Pause menu (Map, Missions, Stats, Crew, Garage, Settings) |
| 1–6 (paused) | Switch pause tabs; M drops a waypoint on the mission marker |
| F9 / F6 | Quick-save to slot 1 |

## Systems

- **City** — a 7-district map with beach and ocean, road grid, palms,
  props, and landmarks (ferris wheel, pier, bridge, tower). Golden
  hour, dusk, neon night, and dawn lighting with long shadows.
- **Driving and on-foot play** — 18 car models to steal and drive,
  damage and repair, on-foot movement, aiming, and combat with
  8 weapons.
- **Traffic and pedestrians** — lane-following traffic, sidewalk
  crowds, beach crowds, peds who flee gunfire.
- **Wanted and police** — 0–5 stars, PVPD cruisers with named
  call-signs and tactics (RAMMING, PIT, ROADBLOCK, FLANKING), a
  dispatch board, and the AIR-1 helicopter with a spotlight from
  4 stars. The Gull is flyable by the player.
- **Missions** — 10 story missions on a stage engine (drive-to,
  shoot, deliver, pickup, race, escort), with dialogue, a
  MISSION PASSED banner, payout, and RP.
- **Crew** — three specialists with cooldowns: Tuck (Swap Plates),
  Ines (Quick Fix), Kip (Eyes Out).
- **Progression** — RP ranks (Runner, Wheelman, Fixer, Kingpin,
  Legend), respect, district standing, 3 save slots, and a
  completion percentage across missions, activities, collectibles,
  and properties.
- **Garage and side work** — upgrades, repairs, paint, car buying,
  3 properties, 12 hidden sun-discs, 3 street races.
- **HUD and screens** — health and armour, money and stars, weapon
  slots, speedo, radio line, mission header, crew panel, dispatch
  board, dialogue bar, and a minimap that traces the real streets
  and districts with a dashed route. Title screen, pause menu,
  full-city map, and stats dashboard.

## Layout

```
main.ts            entrypoint: mounts the canvas, loads the game
serve.ts           static dev server
game/index.html    canvas mount and controls footer
game/src/config.js city data: districts, radio, prices, cars, weapons, ranks
game/src/world.js  city generation: roads, beach, buildings, palms, props
game/src/render.js Canvas 2D renderer: 2.5D extrusion, lighting, Gull
game/src/player.js on-foot movement, combat, entering cars and the Gull
game/src/vehicles.js driving physics, damage, stealing, the Gull's flight
game/src/traffic.js traffic and pedestrian AI
game/src/police.js wanted level, cruisers, dispatch, AIR-1
game/src/missions.js stage engine and the 10 story missions
game/src/crew.js   the three specialists and their abilities
game/src/progress.js ranks, saves, completion, district standing
game/src/garage.js garage, properties, collectibles, street races
game/src/hud.js    HUD panels and the minimap
game/src/screens.js title, pause menu, map, stats dashboard
game/src/audio.js  synthesized WebAudio: engine, sirens, jingles, gunfire
game/src/shots.js  deterministic staging for the four screenshots
shots.json         manifest of the four shots
dev/flow-test.mjs  scripted playthrough (drive, mission, wanted, Gull, garage)
dev/self-test.mjs  system checks (minimap, dispatch, saves, ranks, totals)
```

## Tests

```sh
node dev/flow-test.mjs   # full playthrough, exits non-zero on failure
node dev/self-test.mjs   # systems against each other, exits non-zero on failure
```

Both run in Node against a stubbed browser — no Chrome needed.
