# ChipWorks — Claude Prompt Pack

**Game:** ChipWorks — a resource-management manufacturing game mixed with a clicker/idle game.
**Theme:** Electronics factory. **Look:** bright, friendly tycoon (light background, white rounded cards, blue/green/orange accents, emoji icons, no external images).
**Platform:** One single-file web game (`chipworks.html`) — vanilla HTML/CSS/JavaScript only, no libraries, no build tools, saves in localStorage, works on desktop and mobile.
**Scope:** Medium — two production chains, 5 raw materials, 6 components, 8 finished products.
**Selling:** Auto-sell at base price PLUS timed bonus orders that pay 2–3x.
**Pacing:** Hybrid — active clicking early, idle automation later.
**Storage:** Unlimited. Machines only stop when starved of inputs (bottlenecks), never because storage is full.

## How to use this pack

1. Paste **Prompt 1 (Master + Sprint 0)** into Claude first. Save the file it returns as `chipworks.html` and playtest it.
2. For each next sprint, start a fresh message, paste that sprint's prompt, and paste your current `chipworks.html` where indicated.
3. Playtest against the sprint's test checklist before moving on. Do not skip sprints and do not let Claude build ahead.

---

## PROMPT 1 — MASTER + SPRINT 0 (paste this first)

```
You are an expert browser-game developer. You will build a complete game for me
called "ChipWorks" across several sprints. This first message gives you the full
design so you understand where the game is going, but you must build ONLY
Sprint 0 in this reply. Do not build features from later sprints early, do not
ask me clarifying questions — the spec below is your source of truth, and where
numbers conflict, the PACING TARGETS win.

== THE GAME ==
ChipWorks is a resource-management manufacturing game mixed with a clicker/idle
game, set in an electronics factory. The player clicks to gather raw materials,
processes them into components, assembles components into electronics, and sells
them for money. Money buys machines that automate each stage. The core fun is
BOTTLENECKS: every machine consumes inputs and produces outputs continuously,
so if one stage is too slow, downstream machines sit idle ("Starved") and
upstream inventory piles up. The player fixes bottlenecks by buying more
machines and upgrades.

== TECH RULES (every sprint) ==
- Deliver ONE complete, self-contained HTML file named chipworks.html: CSS in
  <style> in the head, JavaScript in <script> at the end of <body>.
- Vanilla HTML/CSS/JS only. No libraries, no CDN, no external fonts, images,
  or assets. Use emoji as icons.
- State lives in a single `state` object. All game data (resources, machines,
  recipes, upgrades) lives in data-driven CONFIG tables at the top of the
  script so later sprints can extend tables instead of rewriting logic.
- Game loop: tick every 100 ms using real elapsed time (dt), so production is
  frame-rate independent and offline calculation is possible later.
- Inventories are fractional internally; display floored whole numbers. Money
  can be fractional internally; display with the formatter.
- Number formatter: 1,234 below 10,000; then 12.3K, 4.56M, 7.89B, 1.23T
  (3 significant figures).
- Save to localStorage under key "chipworks_save_v1" every 5 seconds and on
  page hide/unload. Include a save `version` field and a migrate() stub so
  future sprints never wipe an existing save.
- No placeholder buttons, no TODO features: every visible control must work.
- Responsive layout: 3 columns on desktop (Resources | Factory | Shop/Info),
  single stacked column on mobile. No horizontal scrolling on a 390px screen.
- Bright, friendly tycoon look: light #f4f7fb background, white cards with
  16px rounded corners and soft shadows, blue #2563eb primary, green #16a34a
  for positive/production, orange #f97316 for money/warnings, red only for
  "Starved" status. Font: system-ui. Big, tappable buttons (min 44px tall).

== FULL DESIGN (context for later sprints — do NOT build yet) ==
Raw materials: Silicon, Copper, Plastic (start) + Glass, Lithium (Sprint 3).
Raw materials sell for $1 each.
Components and recipes (rate-based, continuous production):
- Copper Wire: 1 Copper -> 1 Wire
- Microchip: 2 Silicon -> 1 Chip
- Casing: 2 Plastic -> 1 Casing
- Circuit Board: 1 Microchip + 2 Copper Wire -> 1 Board
- Screen: 2 Glass -> 1 Screen (Sprint 3)
- Battery: 2 Lithium -> 1 Battery (Sprint 3)
Finished products (auto-sell at base price; bonus Orders pay 2-3x, Sprint 3):
- LED Lamp: 1 Wire + 1 Casing — $18
- Calculator: 1 Board + 1 Casing — $50
- USB Charger: 1 Board + 1 Wire + 1 Casing — $90
- Bluetooth Speaker: 1 Board + 2 Wire + 1 Casing — $170
- Smartphone: 1 Board + 1 Screen + 1 Battery + 1 Casing — $500
- Tablet: 1 Board + 2 Screens + 1 Battery + 1 Casing — $800
- Drone: 2 Boards + 1 Screen + 2 Batteries + 2 Casings — $1,800
- Gaming Console: 3 Boards + 1 Screen + 1 Battery + 2 Casings — $2,600
Machines (base cost, +15% cost per owned, Sprint 1-3): one gatherer per raw
material, one processor per component, one assembly line per product.
Selling: finished products auto-sell at base price as they are produced;
timed bonus Orders (Sprint 3) divert an accepted product type into a
stockpile until the player delivers it for 2.5x base value.
Progression (Sprint 4): 12 achievements, offline earnings (50% efficiency,
8-hour cap, "Welcome Back" summary), and an IPO prestige: reset money,
inventory, machines and upgrades for Startup Shares; each Share gives
+5% production speed and +5% sell prices, permanently.
Storage is UNLIMITED. The only reason a machine stops is missing inputs.

== PACING TARGETS (for the finished game; balance toward these) ==
- First finished product within ~2 minutes of active play.
- First machine affordable within ~5 minutes.
- Second production chain (Glass/Lithium) unlocked around 45-60 minutes.
- IPO prestige first available after a few hours of play.
- A new player should always have a next purchase visible within reach.

== SPRINT ROADMAP (context only) ==
Sprint 0: core clicker skeleton (this sprint).
Sprint 1: first production chain — processors, Circuit Boards, LED Lamps and
  Calculators, manual crafting + machines, auto-sell, bottleneck status.
Sprint 2: automation & upgrades — auto-gatherers, click/machine/price
  upgrades, bulk buy x1/x10, per-second net rates per resource.
Sprint 3: second chain (Glass/Screens, Lithium/Batteries), remaining 6
  products, bonus Orders system.
Sprint 4: achievements, offline earnings, IPO prestige.
Sprint 5: tutorial, polish, animations, save export/import, balance pass.

== BUILD SPRINT 0 NOW ==
Goal: a playable clicker skeleton that proves clicking, inventory, money,
selling, and saving — nothing more.
Features:
1. Sticky header: game title "ChipWorks", Money, and Lifetime Earnings.
2. Three large click buttons: Gather Silicon, Gather Copper, Gather Plastic.
   Each click adds +1 of that resource, with a floating "+1" animation and a
   small squash/scale animation on the button.
3. Inventory panel listing Silicon, Copper, Plastic with current counts
   (icons: Silicon, Copper, Plastic — pick fitting emoji and use them
   consistently in all sprints).
4. Sell buttons per raw material: "Sell 1" and "Sell All" at $1 each. Selling
   updates Money and Lifetime Earnings. Buttons disable when count is 0.
5. A stats line: total clicks, total items sold.
6. localStorage save/load as per TECH RULES; on load, restore everything.
   Include a "Reset Save" button behind a confirm() dialog.
7. Game loop running (even though nothing is automated yet) so the dt-based
   tick architecture is in place for Sprint 1.
Acceptance criteria:
- Clicking 10 times and reloading the page restores counts and money exactly.
- Sell All on 0 items changes nothing and the button is disabled.
- No console errors. Layout works at desktop width and 390px mobile width.

== HOW TO REPLY ==
1. One short paragraph: what Sprint 0 includes and what it deliberately
   does not include yet.
2. The COMPLETE chipworks.html file in a single code block — the whole file,
   never a diff or snippet.
3. A changelog for this sprint.
4. A test checklist: the exact clicks/steps I should perform to verify
   Sprint 0, matching the acceptance criteria above.
5. Then STOP. Do not start Sprint 1 and do not include Sprint 1 code.
```

---

## PROMPT 2 — SPRINT 1: FIRST PRODUCTION CHAIN

```
Here is my current chipworks.html from Sprint 0:

[PASTE YOUR CURRENT chipworks.html HERE]

Implement Sprint 1 of ChipWorks. Keep every Sprint 0 feature working, keep the
save key "chipworks_save_v1" and migrate the save (add new fields with defaults;
never wipe an existing save). Follow all TECH RULES from the master prompt.
Build ONLY this sprint.

SPRINT 1 — FIRST PRODUCTION CHAIN
Production model: continuous and rate-based. Each owned machine produces at its
base rate (units/second), consuming inputs proportionally. Each tick, process
machines in this fixed order: processors (Wire, Chip, Casing) -> Board
Assembler -> assembly lines (Lamp, Calculator). A machine's actual rate is
limited by available inputs: actualRate = min(baseRate, availableInput /
inputPerUnit). Consume and produce fractionally using dt. A machine with
0 owned never runs.

Add these processors (recipe, base rate per machine, base cost, cost x1.15 per
owned). The player can also CRAFT any of these manually with a "Craft 1" button
(enabled when inputs are available) — manual crafting is instant and free:
- Wire Drawer: 1 Copper -> 1 Copper Wire, 0.5/s, $40
- Chip Fabricator: 2 Silicon -> 1 Microchip, 0.2/s, $75
- Casing Molder: 2 Plastic -> 1 Casing, 0.4/s, $50
- Board Assembler: 1 Microchip + 2 Copper Wire -> 1 Circuit Board, 0.15/s, $200
Add these assembly lines (same machine rules; output auto-sells instantly at
base price and adds to Money and Lifetime Earnings; also track lifetime count
produced per product):
- Lamp Line: 1 Wire + 1 Casing -> LED Lamp, 0.2/s, $120, sells for $18
- Calculator Line: 1 Board + 1 Casing -> Calculator, 0.15/s, $300, sells for $50

UI requirements:
- Inventory panel now also lists Copper Wire, Microchips, Casings, Circuit
  Boards (with icons) plus lifetime counts for LED Lamps and Calculators sold.
- Factory panel: one card per machine showing icon + name, owned count, recipe
  (inputs -> output), base rate, current status pill, and a Buy button with
  current cost (disabled when unaffordable).
- Status pill logic: "No machine" (gray, 0 owned), "Running" (green, producing
  at >95% of max rate), "Starved" (red, owned but producing below 95% because
  an input is missing — the pill tooltip/text names the missing input),
  "Idle" (yellow, owned but inputs are available downstream-blocked — only if
  applicable; if never applicable, omit it).
- Manual craft buttons live on the relevant inventory rows or machine cards —
  choose one consistent place and label them "Craft 1".

Acceptance criteria:
- With no machines, a player can hand-craft Wire + Casing and produce and sell
  a first LED Lamp within ~2 minutes of clicking.
- Buying a Wire Drawer makes Copper decrease and Wire increase continuously;
  removing Copper (sell it all) flips the card to "Starved" naming Copper.
- Auto-sell money ticks up while a Lamp Line runs with inputs available.
- Reloading mid-production restores money, inventories, and machine counts.
Reply format: short summary, the COMPLETE updated file in one code block,
changelog, sprint-specific test checklist, then STOP. Do not build Sprint 2.
```

---

## PROMPT 3 — SPRINT 2: AUTOMATION & UPGRADES

```
Here is my current chipworks.html from Sprint 1:

[PASTE YOUR CURRENT chipworks.html HERE]

Implement Sprint 2 of ChipWorks. Keep all previous features working, keep save
key "chipworks_save_v1" with migration (new fields get defaults). Follow all
TECH RULES from the master prompt. Build ONLY this sprint.

SPRINT 2 — AUTOMATION & UPGRADES
1. Auto-gatherers (machines, cost x1.15 per owned, each produces 0.5 of its raw
   material per second, no inputs):
   - Silicon Harvester $30, Copper Harvester $30, Plastic Extruder $30.
   They appear in the Factory panel in a "Gathering" group above processors.
2. Net rates: every inventory row shows its net rate per second
   (+x.x/s in green, -x.x/s in red, 0.0/s gray), calculated from all gatherers,
   processors, board assembler and assembly lines at their CURRENT actual
   (input-limited) rates.
3. Bulk buy: a x1 / x10 toggle above the Factory panel. In x10 mode, machine
   Buy buttons buy up to 10 at once, show the total cost of the bulk purchase
   (geometric series at x1.15 growth), and buy fewer if money runs out only
   when "buy max affordable up to 10" is the clear behavior — implement
   buy-exactly-N-or-nothing if N are affordable, otherwise disable.
4. Upgrades shop (new panel; each is a one-time purchase unless levels are
   stated; purchased upgrades show as owned and disappear or gray out):
   - Reinforced Click (5 levels): click power x2 per level (1 -> 2 -> 4 ->
     8 -> 16 -> 32 per click). Costs: $100, $400, $1,600, $6,400, $25,600.
     Applies to the three Gather click buttons.
   - Gatherer Efficiency (3 levels): +50% gatherer output per level.
     Costs: $500, $2,500, $12,500.
   - Machine Speed (3 levels): +25% production rate for all processors, the
     Board Assembler and assembly lines per level. Costs: $750, $3,750,
     $18,750.
   - Marketing (2 levels): +20% sell prices (raw materials AND products) per
     level. Costs: $1,000, $5,000.
   All multipliers must stack multiplicatively and be applied in the rate and
   price calculations in one central place, not scattered through the code.
5. Header now also shows Money per second (net $/s from auto-sell at current
   actual rates; raw-material selling by hand does not count).

Acceptance criteria:
- A Harvester visibly raises Silicon with no clicking; net rate matches the
  displayed gatherer rate after upgrades.
- Reinforced Click Level 1 makes one click add exactly +2.
- x10 buy shows the correct geometric total and deducts it exactly once.
- Marketing raises the LED Lamp auto-sell price from $18 to $21.60 at level 1.
- Old Sprint 1 saves load with 0 upgrades and 0 gatherers, nothing lost.
Reply format: short summary, COMPLETE updated file in one code block,
changelog, test checklist, then STOP. Do not build Sprint 3.
```

---

## PROMPT 4 — SPRINT 3: SECOND CHAIN, ALL PRODUCTS & ORDERS

```
Here is my current chipworks.html from Sprint 2:

[PASTE YOUR CURRENT chipworks.html HERE]

Implement Sprint 3 of ChipWorks. Keep all previous features working, keep save
key "chipworks_save_v1" with migration. Follow all TECH RULES from the master
prompt. Build ONLY this sprint.

SPRINT 3A — SECOND CHAIN
New raw materials (click-to-gather buttons, sell for $1, gatherers, inventory
rows, net rates — mirror exactly how Silicon/Copper/Plastic work):
- Glass (click button + Glass Harvester $400, 0.5/s)
- Lithium (click button + Lithium Extractor $600, 0.5/s)
New processors (manual Craft 1 + machines, cost x1.15 per owned):
- Screen Press: 2 Glass -> 1 Screen, 0.25/s, $500
- Battery Line: 2 Lithium -> 1 Battery, 0.25/s, $650
New assembly lines (auto-sell prices as listed):
- Charger Line: 1 Board + 1 Wire + 1 Casing -> USB Charger, 0.15/s, $600, $90
- Speaker Line: 1 Board + 2 Wire + 1 Casing -> Bluetooth Speaker, 0.12/s,
  $1,200, $170
- Phone Line: 1 Board + 1 Screen + 1 Battery + 1 Casing -> Smartphone,
  0.1/s, $3,000, $500
- Tablet Line: 1 Board + 2 Screens + 1 Battery + 1 Casing -> Tablet,
  0.08/s, $5,000, $800
- Drone Line: 2 Boards + 1 Screen + 2 Batteries + 2 Casings -> Drone,
  0.06/s, $9,000, $1,800
- Console Line: 3 Boards + 1 Screen + 1 Battery + 2 Casings -> Gaming
  Console, 0.05/s, $15,000, $2,600
Gate: Glass/Lithium content is hidden until the player has earned $1,000
lifetime, then revealed with a "New materials discovered!" toast. This targets
the 45-60 minute unlock pacing when combined with earlier costs — do not make
the gate higher.

SPRINT 3B — BONUS ORDERS
- An Orders panel shows at most ONE offered order at a time. A new offer
  appears 15 seconds after the previous one is completed, failed, or expires,
  and only offers products the player has an assembly line for.
- An offer: product, quantity (roughly 60-120 seconds of that line's current
  max production, minimum 5, maximum 100), reward = 2.5x the product's base
  sell value of the full quantity (Marketing multipliers do NOT apply to
  order rewards), and a time limit of 3 minutes from acceptance.
- The player may Accept or Dismiss (dismiss = offer expires, no penalty).
  While an order is active, that product type is DIVERTED: assembly lines
  still produce it, but instead of auto-selling it goes into a visible
  product stockpile count on the order card. Other products auto-sell as
  normal. When the stockpile reaches the required quantity, a "Deliver"
  button enables; clicking it pays the reward, clears the stockpile excess
  back to auto-sell (excess units sell at base price immediately), and shows
  a success toast. If the timer runs out, the order fails with no penalty,
  stockpiled units auto-sell at base price, and a new offer is scheduled.
- Orders UI shows: product icon/name, progress (stockpiled / required),
  reward, and a live countdown. Persist an active order in the save
  (including its deadline as a timestamp; on load, if the deadline passed
  while away, treat it as failed under the rules above).

Acceptance criteria:
- Before $1,000 lifetime earnings, no Glass/Lithium UI exists anywhere.
- A Smartphone requires all four inputs; starving Batteries flips the Phone
  Line to "Starved" naming Batteries.
- Accepting an order stops auto-sell income for that product only, stockpile
  grows, Deliver pays exactly 2.5x base value, timeout sells stockpile at 1x.
- Reloading with an active order restores its progress and remaining time.
Reply format: short summary, COMPLETE updated file in one code block,
changelog, test checklist, then STOP. Do not build Sprint 4.
```

---

## PROMPT 5 — SPRINT 4: ACHIEVEMENTS, OFFLINE EARNINGS & IPO PRESTIGE

```
Here is my current chipworks.html from Sprint 3:

[PASTE YOUR CURRENT chipworks.html HERE]

Implement Sprint 4 of ChipWorks. Keep all previous features working, keep save
key "chipworks_save_v1" with migration. Follow all TECH RULES from the master
prompt. Build ONLY this sprint.

SPRINT 4A — ACHIEVEMENTS
Add an Achievements panel listing all 12 below. Each unlocks once, shows a
toast ("Achievement unlocked: ..."), and is stored in the save. Locked ones
show their condition; unlocked ones show a checkmark and unlock order/time is
not required. The 12:
1. First Click — gather 1 raw material by clicking.
2. First Sale — sell anything.
3. First Chip — produce 1 Microchip.
4. First Product — sell 1 finished product.
5. Assembly Online — own 5 machines total.
6. Small Factory — own 25 machines total.
7. Mass Production — own 100 machines total.
8. Four Figures — reach $1,000 lifetime earnings.
9. Six Figures — reach $100,000 lifetime earnings.
10. Order Up — complete 1 bonus Order.
11. Reliable Supplier — complete 10 bonus Orders.
12. High Tech — sell 1 Smartphone.

SPRINT 4B — OFFLINE EARNINGS
- On every save, also store: lastSeen timestamp, and a snapshot of the current
  net money-per-second rate and each raw material's net gather rate.
- On load, if the player was away at least 60 seconds: simulate offline
  progress at 50% efficiency for at most 8 hours. Add money = snapshot $/s x
  seconds away x 0.5. Add raw materials from gatherers only (processors do
  NOT run offline — state this rule in the modal). Cap each raw material's
  offline gain at what its gatherers alone would produce in that window x 0.5.
- Show a "Welcome Back!" modal summarizing time away, money earned, and raw
  materials gained, with a single Collect/Close button. No modal for <60s.

SPRINT 4C — IPO PRESTIGE
- New "IPO" section (in the Shop/Info column). Going public resets: Money to
  $0, all inventories to 0, all machines to 0, all upgrades to unpurchased,
  any active order cancelled without reward. It KEEPS: achievements, lifetime
  stats, total orders completed, and Startup Shares.
- Shares earned on IPO = floor( sqrt( lifetimeEarningsThisRun / 10,000 ) ),
  where lifetimeEarningsThisRun resets to 0 after each IPO. The IPO button
  shows shares that would be earned and is disabled below 1 share (i.e.
  below $10,000 earned this run). Require a confirm modal that lists exactly
  what resets and what is kept.
- Each Startup Share permanently grants +5% production speed and +5% sell
  prices, applied multiplicatively as (1 + 0.05 x shares) in the same central
  multiplier code from Sprint 2. Display total Shares and current bonus in
  the header or IPO section.

Acceptance criteria:
- Achievements unlock exactly once, survive reload, and toasts appear.
- Setting the system clock / save timestamp back 1 hour and reloading shows
  the Welcome Back modal with money close to $/s x 3600 x 0.5 (within 5%).
- IPO below $10,000 this run is disabled; at $40,000 this run it offers
  exactly 2 shares; after IPO, production and prices reflect the +10% bonus
  and achievements/shares persist while everything else reset.
Reply format: short summary, COMPLETE updated file in one code block,
changelog, test checklist, then STOP. Do not build Sprint 5.
```

---

## PROMPT 6 — SPRINT 5: POLISH, TUTORIAL & BALANCE PASS

```
Here is my current chipworks.html from Sprint 4:

[PASTE YOUR CURRENT chipworks.html HERE]

Implement Sprint 5 (final) of ChipWorks. Keep all previous features working,
keep save key "chipworks_save_v1" with migration. Follow all TECH RULES from
the master prompt. This is a polish sprint: do not add new resources,
machines, products, or currencies.

SPRINT 5 — POLISH, TUTORIAL & BALANCE
1. Tutorial: on a brand-new save only, show a short 4-step guided hint bar
   (dismissible at any step, "Replay Tutorial" button in Settings):
   Step 1 "Click Gather to collect raw materials" -> Step 2 "Sell raw
   materials, or Craft a component" -> Step 3 "Buy your first machine to
   automate" -> Step 4 "Assemble products and watch for Starved machines —
   that is your bottleneck." Advance each step when the player performs the
   action. Never show it again after completion/dismissal (store the flag).
2. Animation & feedback: floating "+N" on clicks (already in Sprint 0 — extend
   to Craft buttons), a brief green flash on a machine card when its product
   sells in a noticeable batch is NOT required; instead: smooth number
   transitions are forbidden (numbers must stay exact), button press states,
   toast system unified for achievements/orders/unlocks, and a subtle pulse
   on the Money display when an Order reward is paid.
3. Settings section: Reset Save (double confirm), Export Save (shows the save
   JSON in a textarea with a Copy button), Import Save (paste JSON, validate
   it has the right key/version, load it, show an error toast on invalid
   data), Replay Tutorial.
4. Help section: a "How to Play" collapsible that explains the production
   chain with the full recipe list, what "Starved" means, how Orders divert
   products, offline rules, and IPO — generated from the CONFIG tables where
   practical so it cannot drift from the real numbers.
5. Balance pass: re-check every cost/rate/price against these targets and
   adjust CONFIG numbers ONLY (no logic changes), listing every number you
   changed and why: first product ~2 min, first machine ~5 min, second chain
   revealed at $1,000 lifetime (~45-60 min), first IPO (1+ share) realistically
   reachable in 2-4 hours of hybrid play, Gaming Console line is the most
   profitable per second when fully supplied.
6. Final QA sweep: fix any console errors, ensure no button is a placeholder,
   verify the layout at 390px and 1440px, verify a fresh save and a migrated
   Sprint 4 save both load, and verify keyboard focus is visible on buttons.

Reply format: short summary, the COMPLETE final chipworks.html in one code
block, changelog INCLUDING the balance-change table (old -> new, with
reason), a full-game test checklist (fresh-save playthrough steps from first
click to first IPO), and a short "Known limitations" list. This completes
the project — do not propose a Sprint 6.
```

---

## Design decisions locked (for your reference)

| Decision | Choice |
|---|---|
| Genre | Resource management + manufacturing + clicker/idle |
| Theme | Electronics factory |
| Name / look | ChipWorks — bright, friendly tycoon |
| Scope | Medium — 2 chains, 5 raw, 6 components, 8 products |
| Selling | Auto-sell + timed bonus Orders (2.5x) |
| Platform | Single-file HTML/CSS/JS, localStorage |
| Pacing | Hybrid — active early, idle later, offline capped at 8h |
| Storage | Unlimited — bottlenecks only |
| Prestige | IPO for Startup Shares (+5% speed & prices each) |
| Build model | 6 sprints, one prompt each, playtest between sprints |
