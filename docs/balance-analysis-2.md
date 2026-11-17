# ChipWorks — Full Balance Analysis #2 (2026-11-17)

Computed from the post-overhaul config (Board Assembler 0.30/s @ $160, 1-Wire boards, Chip Fab 0.30/s, Console 2 boards), assuming each product line is fully supplied with the minimum machine counts and ×1.15 cost growth.

## Stage table (cumulative, fully supplied)

| Stage | Cum. income | Stage cost | Cum. factory cost | Payback of stage cost |
|---|---|---|---|---|
| LED Lamp | $3.6/s | $270 | $270 | 75s |
| Calculator | $11.1/s | $600 | $870 | 54s |
| USB Charger | $24.6/s | $772 | $1,642 | 31s |
| Bluetooth Speaker | $45.0/s | $1,602 | $3,244 | 36s |
| Smartphone | $95.0/s | $5,190 | $8,434 | 55s |
| Tablet | $159.0/s | $6,081 | $14,515 | 38s |
| Drone | $267.0/s | $10,814 | $25,329 | 41s |
| Gaming Console | $397.0/s | $15,098 | $40,427 | 38s |

On paper there is NO stall — paybacks stay 31–75s at every stage. The stall Trey feels is structural, from four interacting causes:

## The four stall causes

1. **Nobody plays "fully supplied."** The table assumes perfect supply at every moment. In real play, lines run starved at partial rates while the player saves for the next machine, so realized income is a fraction of the table — and every purchase decision is made from that reduced income. The gap between theoretical and realized income widens as chains deepen (a starved Drone line wastes a $9,000 purchase).
2. **Declining line ROI.** Revenue per second per dollar of line cost falls monotonically: Lamp .0300 → Calculator .0250 → Charger .0225 → Speaker .0170 → Smartphone .0167 → Tablet .0128 → Drone .0120 → Console .0087. The Console returns 3.4× less per dollar than the Lamp. Late lines feel bad because they ARE worse investments than upgrades (Marketing +20% on everything, Machine Speed +25% on everything).
3. **The Wing B toll.** The Smartphone stage costs $5,190, of which the line is $3,000 — the other ~$2,150 is the Wing B entry fee (Glass Harvester $400 + Lithium Extractor $600 + Screen Press $500 + Battery Line $650) that earns nothing until the phone line exists. It lands exactly at the point where cause #2 starts biting.
4. **The buyout grind (and the broken button).** Shares = floor(√(run earnings / 10,000)). Marginal cost per share grows linearly: share 2 costs +$30K more run earnings, share 3 +$50K, share 4 +$70K, share 5 +$90K. Five shares = $250K run earnings. At a realistic partially-supplied mid-run income of ~$50–95/s that's 45–80 minutes of pure accumulation per late share, for +5% each. Compounded by the reported bug — the Buyout button not working at all — prestige progression reads as a dead end, which is likely a large part of the perceived stall.

Upgrade cliffs reinforce the plateau: Machine Speed Lv3 $18,750, SMT Lv2 $15,000, Reinforced Click Lv5 $25,600 — each costs more than the Drone line, at ×4–5 cost growth per level.

## Proposed tuning package (awaiting Trey's approval)

- **Buyout curve:** shares = floor(√(run earnings / 5,000)) — thresholds: 1 share @ $5K, 2 @ $20K, 3 @ $45K, 4 @ $80K, 5 @ $125K, 10 @ $500K (was $1M).
- **Wing B toll cut:** Glass Harvester $400→$250, Lithium Extractor $600→$400, Screen Press $500→$350, Battery Line $650→$450. Smartphone stage cost drops ~$900.
- **Late-line prices:** Tablet $800→$900, Drone $1,800→$2,000, Console $2,600→$3,000. Revenue ceiling $397/s → ~$430/s.
- **Upgrade cliffs softened:** Machine Speed $750/$3,750/$18,750 → $750/$3,000/$12,000; SMT Lv2 $15,000→$10,000; Reinforced Click Lv5 $25,600→$16,000.
- **Machine cost growth:** ×1.15 → ×1.13 per owned (softens the incremental-buying tax across a long run; full-factory cost drops ~8–10%).
