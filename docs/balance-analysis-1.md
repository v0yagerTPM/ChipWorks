# ChipWorks — Balance Analysis: The Circuit Board Bottleneck

_Ran 2026-11-14. Scenario: one of every assembly line, all running at full speed.
All figures computed from the game's actual rates, recipes, and costs._

## Component demand vs. supply (current numbers)

| Component | Demand /s | Output per machine /s | Machines needed |
|---|---|---|---|
| Circuit Board | 0.87 | 0.15 | **5.8 → buy 6** |
| Microchip | 0.87 | 0.20 | 4.3 → buy 5 |
| Copper Wire (total) | 2.33 | 0.50 | 4.7 → buy 5 |
| Casing | 1.02 | 0.40 | 2.5 → buy 3 |
| Screen | 0.37 | 0.25 | 1.5 → buy 2 |
| Battery | 0.35 | 0.25 | 1.4 → buy 2 |

Boards are a 2–4x outlier. Worse, 1.74 of the 2.33 wire/s (75%) is eaten by boards
themselves (2 Wire per board), so Wire is a hidden second bottleneck inside the first.

## The unlock ramp (why the player can never catch up)

Cumulative board demand as each board-using line unlocks (one of each):

| After unlocking | Board demand /s | Assemblers needed (current) | Assemblers needed (proposed) |
|---|---|---|---|
| Calculator | 0.15 | 1.0 | 0.5 |
| USB Charger | 0.30 | 2.0 | 1.0 |
| Bluetooth Speaker | 0.42 | 2.8 | 1.4 |
| Smartphone | 0.52 | 3.5 | 1.7 |
| Tablet | 0.60 | 4.0 | 2.0 |
| Drone | 0.72 | 4.8 | 2.4 |
| Gaming Console | 0.87 | 5.8 | 2.9 |

Early game: one Board Assembler makes 9 boards/min; one Calculator Line consumes
exactly 9/min. Zero slack — the second board product purchased immediately starves.

## Proposed overhaul — after numbers

Changes: Board Assembler 0.15 → 0.30/s and $200 → $160 · Board recipe 2 Wire → 1 Wire ·
Chip Fabricator 0.20 → 0.30/s · Gaming Console recipe 3 Boards → 2 Boards ·
new SMT Line upgrade (2 levels, +50% assembler speed each, $2,500 / $15,000).

| Component | Demand /s | Machines needed (proposed) |
|---|---|---|
| Circuit Board | 0.82 | 2.7 → buy 3 |
| Microchip | 0.82 | 2.7 → buy 3 |
| Copper Wire (total) | 1.41 | 2.8 → buy 3 |
| Casing | 1.02 | 2.5 → buy 3 |
| Screen | 0.37 | 1.5 → buy 2 |
| Battery | 0.35 | 1.4 → buy 2 |

Every component lands in a 1.4–2.8 machine band — no outlier. The next-tightest
chain becomes Plastic/Casings (2.04 plastic/s, ~5 extruders), which is a simple
single-input chain and cheap to expand, so it reads as a normal bottleneck, not a wall.

## Economy check

- Gross revenue ceiling (one of every line, fully fed): **$397/s — unchanged.**
- Cost to build the full supporting factory: $42,097 current vs $40,427 proposed (−4%).
- The overhaul does not make the game easier overall; it removes one spike and
  redistributes the same total machine investment across all chains evenly.
