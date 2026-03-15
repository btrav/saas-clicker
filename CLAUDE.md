# SaaS Clicker — Project Context

## What This Is
A single-file browser clicker/idle game (`index.html`) with no dependencies. Players build a SaaS startup: acquire users, convert them to paying customers, manage churn, and either bootstrap to acquisition or take VC funding toward an IPO. Tone is cheeky and satirical.

## File Structure
Everything is in `/Users/Ben/Projects/saas-clicker/index.html` — HTML, CSS, and JS all in one file. No build step.

## Core Architecture

### State
- `G` — all live game state (cash, users, rates, purchased upgrades, etc.)
- `prestigeData` — cross-run bonuses (persists across prestige/IPO resets)
- `UPGRADES` array — all purchasable items; drives the upgrades panel
- `COMPANIES` array — pool of randomized company names/emoji/taglines (25 entries)
- `FUNDING_ROUNDS` array — VC round triggers and term sheets
- `RANDOM_EVENTS` array — MRR-milestone-triggered events

### Key Constants
- `TICK_MS = 100` — game runs at 10 ticks/sec
- `SECS_PER_MONTH = 60` — 1 real minute = 1 game month
- `SECS_PER_DAY = 2` — cash pays out daily (MRR/30 every 2 real seconds)

### Key G Fields
- `G.cash`, `G.totalUsers`, `G.payingUsers` (float, smoothed)
- `G.convRate`, `G.churnRate`, `G.clickPower`, `G.autoRate`, `G.burnRate`
- `G.arpu` — computed by `recalcARPU()` from plan distribution
- `G.mrr` — `Math.round(G.payingUsers) * G.arpu * prestigeData.revMult`
- `G.path` — `'bootstrap'` by default, switches to `'vc'` on first accepted funding
- `G.activeCountdowns` — array of `{ id, label, total, remaining, onComplete }`
- `G.activeEffects` — timed effects via `addEffect(id, label, duration, onStart, onEnd)`
- `G.nextEventMRR` — MRR threshold for next random event
- `G.infraWarned` — one-time flag for cloud infra warning at 9k users
- `G.lastPayingFloor` — tracks integer crossings for immediate cash on new paying user

### Cash Flow
- Cash accrues as daily payouts: every `SECS_PER_DAY`, add `(MRR - burnRate) / 30`
- When `Math.round(G.payingUsers)` crosses an integer up, immediate ARPU payment fires

### Paying Users
- Stored as float; displayed/used via `Math.round()` (not `Math.floor` — was a bug)
- Smooth upward conversion toward `totalUsers * convRate`; churn applied per tick
- Churn affects `totalUsers` too (at 1.5× rate of paying churn)

## Upgrade System
- `UPGRADES` array; types: `'auto'` (Acquisition), `'upgrade'` (Product & Growth), `'plan'`, `'team'`, `'finance'`
- `onBuy()` callback; `repeatable: true` upgrades use `delete G.purchased[id]` to re-enable
- `dignityCost` field — display-only label shown on card (e.g. `💔 costs 1 dignity`)
- Upgrade visibility: `isUpgradeVisible()` checks `unlockCash`, `unlockUsers`, `unlockPaying`, path flags
- Upgrades render every ~5s (`G.tick % 50 === 0`) plus on buy

## Infrastructure Wall
- Cloud Infrastructure (`cloud_basic`) must be purchased to grow past 10,000 users
- At 9,000 users: auto-growth and clicks throttle to 8%, one-time warning fires, card pulses orange/red (`infra-needed` CSS class)
- Hard cap enforced in `gameTick()`

## Funding Rounds (VC path)
All rounds now gated at meaningful scale. First two are intentionally low-ball:
- **Pre-Seed**: 12,000 users + 150 paying — $40k@15% or $75k@22%
- **Seed**: 28,000 users + $8k MRR — $250k@18% or $500k@25%
- **Series A**: 50,000 users + $80k MRR
- **Series B**: 50,000 users + $500k MRR
- **Series C**: 200,000 users + $2M MRR
- **IPO**: 500,000 users + $5M MRR
- `passFunding()` lets players pass any round and stay equity-free
- Path starts as `'bootstrap'`; only switches to `'vc'` when funding is accepted

## Random Events
- Trigger when `G.totalUsers >= 5000` AND `G.mrr >= G.nextEventMRR`
- After firing: `G.nextEventMRR = G.mrr * 8` (intentionally infrequent)

## Countdown Timer System
- `G.activeCountdowns` array, ticked in `gameTick()`
- Rendered as progress bars in "In Progress" block in left panel
- Used by: Product Hunt Launch (10s → user burst + 60s click spike via addEffect), Podcast Sponsorship (30s → user burst + 90s autoRate spike via addEffect)

## Prestige System
- VC path: 3 IPOs max → Hall of Fame; each adds revenue/click/conv multipliers
- Bootstrap path: acquisition exit → bswins prestige; adds conv bonus + starting cash

## Company Names (25 total)
Satirical tech company parodies. Current pool includes: Flack, Noshun, Zoombomb, Stripclub, Intercram, Mailchump, JirAAAA, Figmeh, GitHubris, Snowjob, ZenDesk Jockey, Webflop, Cluck-Up, Moanday, Asinine, AirBnTable, Workaday, Linearly, OpenlyAI, Perplexed, Calenduh, DocuSigh, Salesfarce, Confusence, Dropbucks.

## Mobile Layout
- Tab bar at bottom (3 tabs: Click, Upgrades, Dashboard)
- `viewport-fit=cover` + `env(safe-area-inset-bottom)` for iOS safe area
- Panels are `position: absolute` within `#main` with explicit `bottom` offset — critical for tab tap targets
- Panels have `background: var(--bg)` — required to prevent panel layering bleed-through
- Tab bar `z-index: 200`

## Things Explicitly Removed / Rejected
- Niche Focus upgrade (removed — `nicheFocusCap` state also gone)
- Upfront VC/Bootstrap path selection screen (removed — path emerges from funding decisions)
- Repeatable risky upgrades (Sketchy Mailing List, Contact Influencer, Podcast, etc. are all one-time now)
- Continuous cash accrual per tick (replaced with daily payout system)
- `Math.floor` on paying users display (was causing off-by-one; now `Math.round` everywhere)

## Tone & Style Notes
- Company names and descriptions are cheeky, self-aware, satirical of real SaaS companies
- Upgrade/event copy leans into startup clichés and founder pain points
- Keep it punchy — short descriptions, no corporate speak
