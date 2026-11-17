# ChipWorks — Plant No. 9

A single-file idle / factory-management game for the browser. You are the new manager of **ChipWorks Plant No. 9**, an electronics plant that was shuttered two years ago. Corporate will sell it for scrap unless it ships again. Doss, the foreman who never left, shows you the ropes.

Grow the plant from hand-salvaged scrap to a full electronics factory: gather raw materials, process them into components, run assembly lines, fulfill contracts for named clients, and eventually **buy the plant from corporate**.

## Play it

No build step, no dependencies — it's one HTML file.

- **Just open it:** double-click `index.html`, or
- **Serve it:** `python3 -m http.server` in this folder, then visit `http://localhost:8000`

Progress saves automatically in your browser (`localStorage`, key `chipworks_save_v1`). Export/import/reset are in the Office view.

## The game

- **5 raw materials** — Silicon, Copper, Plastic, plus Glass and Lithium behind the Wing B reopening ($1,000 lifetime earnings)
- **6 components** — Copper Wire, Microchips, Casings, Circuit Boards, Screens, Batteries
- **8 products** — LED Lamp → Calculator → USB Charger → Bluetooth Speaker → Smartphone → Tablet → Drone → Gaming Console
- **Flow-board factory floor** — the production chain drawn as Raw → Components → Products, with live per-minute flow rates on every connection and status on every machine (`▶ RUNNING`, `⚠ STARVED: WIRE −6/min`, `⏸ HELD`, `○ IDLE`, `🔒 LOCKED`)
- **Line control** — every assembly line can be set to HOLD / NORMAL / EXPEDITE; scarce components are allocated to EXPEDITE lines first
- **Contracts** — three offers at a time (Easy 2× / Medium 2.5× / Hard 3.25×) from named clients; your delivery track record scales future offers, and accepting a contract auto-expedites its line
- **Upgrades** — Reinforced Click, Gatherer Efficiency, Machine Speed, Marketing, and the SMT Line for the Circuit Board bottleneck
- **Plant Log** — a 9-entry story log that fills in as the plant hits milestones
- **Buyout (prestige)** — earn Ownership Shares at `floor(√(run earnings ÷ 100,000))`; each share is +5% production speed and +5% sell prices, permanently
- **Offline earnings** at 50% efficiency, capped at 8 hours, reported as a Shift Report when you return

## Tech

Vanilla HTML / CSS / JavaScript in a single file (`index.html`, ~150 KB). No libraries, no build tooling. Fixed-timestep simulation, fractional inventories, `localStorage` saves with migration-by-defaults.

## Design docs

- [`docs/design-prompt-pack.md`](docs/design-prompt-pack.md) — the original game design and sprint plan
- [`docs/balance-analysis-1.md`](docs/balance-analysis-1.md) — first balance pass (the Circuit Board bottleneck)
- [`docs/balance-analysis-2.md`](docs/balance-analysis-2.md) — full progression analysis and the stall diagnosis

## Development

ChipWorks was designed and built iteratively with AI assistance (Muse), including playtest-driven reworks: phone app-shell layout, priority/pause line controls, an industrial reskin with a story layer, and a research-based UI overhaul (flow board inside a persistent frame, modeled on Melvor Idle / Factorio / shapez UI patterns).
