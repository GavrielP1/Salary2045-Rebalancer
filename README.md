# Salary2045 — Portfolio Rebalancer

A free, browser-based tool that tells you where to deploy new cash in your investment portfolio to stay on target — without selling anything. Buy-only, multi-currency, fee-aware.

🔗 **[Live Demo → gavrielp1.github.io/Salary2045-Rebalancer](https://gavrielp1.github.io/Salary2045-Rebalancer)**

---

![Demo](demo.gif)

<table>
  <tr>
    <td><img src="screenshot1-sleeves-cash.png" alt="Target allocation, cash input, base currency" width="100%"/><br/><sub><b>Set sleeves, cash, and base currency</b></sub></td>
    <td><img src="screenshot2-fees-fx.png" alt="Fees, optimization mode, FX rates" width="100%"/><br/><sub><b>Configure fees, mode, and FX rates</b></sub></td>
    <td><img src="screenshot3-holdings.png" alt="Holdings table with currencies and caps" width="100%"/><br/><sub><b>Enter holdings, currencies, and caps</b></sub></td>
  </tr>
  <tr>
    <td><img src="screenshot4-rebalance-plan.png" alt="Rebalance plan with summary cards and sleeve bars" width="100%"/><br/><sub><b>Read the rebalance plan</b></sub></td>
    <td><img src="screenshot5-ticker-breakdown.png" alt="Ticker breakdown and allocation logic notes" width="100%"/><br/><sub><b>Per-ticker breakdown and logic notes</b></sub></td>
    <td></td>
  </tr>
</table>

---

## What It Does

Most rebalancing tools tell you to sell overweight positions and buy underweight ones. This tool doesn't. It takes a **buy-only** approach: you enter how much new cash you have to deploy, and the tool tells you exactly where to put it to move your portfolio closer to your target allocation — without triggering any sales or tax events.

Over time, as you add money regularly (e.g. monthly salary savings), your portfolio gradually converges to your target without ever selling.

---

## How to Use It

1. **Set your target allocation** — define your sleeves and the % you want each to represent.
2. **Enter your cash** — how much new money you're adding, and how much cash already sits in your account.
3. **Enter your holdings** — ticker, sleeve, shares, price, currency, and optional cap.
4. **Read the plan** — the tool tells you exactly how many units and how many dollars to deploy into each position.

No account, no login, no server. Everything runs locally in your browser.

---

## Features

### Dynamic Sleeves

Sleeves are the categories you define for your portfolio. Each has a name, target %, and color. The default structure is:

| Sleeve | Default Target | Purpose |
|---|---|---|
| **Core** | 40% | Stable, diversified — index funds, dividend ETFs |
| **Satellite** | 40% | Individual stocks with long-term conviction |
| **High Conviction** | 10% | Higher-risk, higher-upside positions |
| **Hedge** | 7% | Defensive assets — gold, inverse ETFs |
| **Cash** | 3% | Liquidity buffer for fees, taxes, opportunities |

All percentages are adjustable. The tool warns you if they don't sum to 100%. You can add, rename, recolor, and delete any sleeve except Cash.

### Three-Tier Cash Priority

| Cash level | Condition | Action |
|---|---|---|
| **Critically low** | below 1% | Funded **first**, but only up to the 1% floor |
| **Normal** | 1% to target % | Funded **last** — only after all securities sleeves are covered |
| **Overfunded** | at or above target % | Gets **nothing** |

### Per-Ticker Max % Cap

Each holding has an optional **Max %** field. If a stock is already at or above its cap, it receives zero new allocation, and the money is redirected to uncapped siblings in the same sleeve.

### Transaction Fees

Optional fixed and/or percentage fees per trade:

```
Fee per trade = Fixed Fee + (Percentage Fee ÷ 100) × trade amount
```

Fees are paid through a cascade: cash reserve → existing cash → raid stock allocation. A strict no-debt constraint guarantees your cash never goes negative.

### Version A / Version B Optimization

| Mode | Behavior |
|---|---|
| **Version A** | Accuracy-first. All eligible tickers receive allocation regardless of fee impact. |
| **Version B** | Budget-first. Smallest trades are cut until total fees fit within your Max Fee Budget. |

### Whole-Unit Round-Up Tolerance

For brokers that don't allow fractional shares, the tool buys whole units only. When a remainder of ≥ 0.5 units exists, the tool can round up — but only within a tolerance you set. Rounded-up positions are marked with ▲ in the Units column.

### Multi-Currency Support

Hold securities in different currencies within a single portfolio:

- **Base currency** — all allocation math and summary values run in this currency.
- **Per-ticker currency** — set the native currency for each holding.
- **FX rates** — fetched automatically from [frankfurter.app](https://frankfurter.app) (free, no API key), editable manually.
- **Ticker Breakdown** shows buy amounts in **native** currency (what you execute at your broker).

If a rate is missing, allocation is blocked until you provide it.

### Live Price Refresh (Optional)

| Provider | Notes |
|---|---|
| **Finnhub** ✅ Recommended | Real-time US stocks, 60 calls/min free |
| **Twelve Data** | Real-time, 800 calls/day free |
| **Financial Modeling Prep** | EOD only, free |
| **Alpha Vantage** | 15-20 min delayed, 25 calls/day free |
| **Tiingo** | Free tier, may be CORS-blocked |
| **Polygon** | Free tier, may be CORS-blocked |

> ⚠️ Never commit a real API key to a public repo. Leave the field empty before publishing.

### Multiple Portfolios

Switch between up to 5 separate portfolios using the tabs at the top of the page. Each portfolio has its own sleeves, holdings, settings, and FX rates — all saved independently in localStorage.

- **Switch** — click any tab to load that portfolio (animated transition).
- **Rename** — double-click a tab to rename it.
- **Delete** — click ✕ next to the active tab (with confirmation).
- **Add** — click "+ New" to create a blank portfolio.

### Drag to Reorder

Both **sleeves** and **holdings** support smooth drag-and-drop reordering. Grab the ⠿ handle on any row and drag it to a new position. Other rows shift in real time to show where the item will land.

### Onboarding Tour

Click **? Take a Tour** to walk through a 10-step guided tour of every section of the tool. Each step highlights the relevant panel and explains what to do. You can skip, go back, or jump to done at any time.

### Share URL

Click **Share** in the Rebalance Plan panel to generate a URL that encodes your entire portfolio state as a base64 query parameter. Anyone with the link (and access to the hosted page) can open your exact configuration. Works from GitHub Pages — not from a local file.

### Export / Import

- **↓ Export JSON** — downloads a full backup of your current portfolio state.
- **↑ Import JSON** — restores from a previously exported file.
- **↓ Export CSV** — exports the Ticker Breakdown as a spreadsheet-ready CSV.
- **🖨 Print Plan** — opens a print-optimized view of the Rebalance Plan and Ticker Breakdown.

### Dark / Light Mode

Click ☀ in the top-right corner to toggle between dark and light mode. Your preference is applied immediately.

### Days Since Rebalance

A counter below the title shows how many days have passed since you last rebalanced. Click it to reset the counter to today.

### Auto-Save Indicator

A small dot in the bottom-left corner flashes green ("Saved") after every automatic save to localStorage.

### Mobile Responsive

The tool works on phones and tablets. Tables scroll horizontally. Stat cards stack into a 2-column grid. The portfolio switcher scrolls horizontally. All panels adapt to narrow viewports.

### Market Ticker Background

Animated rows of your ticker symbols scroll across the background in real time — green for gains, red for losses. The tickers shown are pulled directly from your Holdings table. If Holdings is empty, a default set of tickers is used.

### Persistence

All data saves automatically to your browser's **localStorage** after every change. No manual saving required.

---

## Reading the Results

### Summary Cards

| Card | Meaning |
|---|---|
| **Portfolio Value** | `totalNow` — current value of all holdings + existing cash, in base currency |
| **After Deploy** | `totalAfter = totalNow + newCash` — portfolio value once all trades execute |
| **Cash Allocated** | Total actually spent on securities |
| **Cash Left** | Unspent cash: rounding leftovers + cash reserve + overflow from capped tickers |
| **Total Fees** | Sum of all transaction fees (shown only when fees are configured) |

### Sleeve Plan Table

| Column | Meaning |
|---|---|
| Current % | Sleeve's share of the portfolio right now (`÷ totalNow`) |
| After % | Projected share after deployment (green = near target, red = over, gold = under) |
| Target % | Your defined goal |
| Gap | How far off the sleeve is (green positive = underweight = needs buying) |
| $ To Buy | Amount allocated to this sleeve, in base currency |

### Ticker Breakdown Table

| Column | Meaning |
|---|---|
| Current % | Position's current share of the total portfolio |
| Max % | Your cap (purple = under cap, red + ⚠ = at or above cap) |
| Units | Whole units to buy (blue = normal, purple ▲ = rounded up) |
| $ To Buy | Amount in **native** currency — execute this at your broker |

---

## Allocation Logic (Formula Reference)

**Core quantities**
```
totalNow   = existingCash + Σ (shares × nativePrice ÷ fxRate)
totalAfter = totalNow + newCash
```

**Sleeve targets** (always measured against `totalAfter`, never `totalNow`)
```
targetValue[s] = totalAfter × (target% ÷ 100)
need[s]        = max(0, targetValue[s] − currentValue[s])
```

**Cash floor**
```
cashFloor   = totalAfter × 0.01
cashReserve = max(0, cashFloor − existingCash)
```

**Ticker allocation**
```
allocBase[t]   = sleeveBudget ÷ numEligibleTickers
allocNative[t] = allocBase[t] × fxRate[currency]
units[t]       = floor(allocNative[t] ÷ nativePrice[t])   [whole-unit]
units[t]       = allocNative[t] ÷ nativePrice[t]          [fractionable]
finalBuy[t]    = units[t] × nativePrice[t] ÷ fxRate[t]    [in base currency]
```

**Conservation identity**
```
Cash Allocated + Cash Left = Available Cash to Deploy
```

---

## Common Scenarios

- **First investment** — set sleeve targets, add tickers with prices and 0 shares, enter your initial cash. The tool distributes proportionally by target weight.
- **Monthly salary deployment** — update prices, enter the month's new cash. The tool directs money to underweight sleeves. Over time the portfolio converges without selling.
- **Large Cash Left** — happens when every ticker in an underweight sleeve is already at its cap. Not a bug — raise a cap or add a ticker.
- **Fee limiting** — set a fixed fee, select Version B, set a budget. The tool cuts the smallest trades until fees fit.
- **Multi-currency** — set base currency, enter native currency per holding, refresh FX rates. Allocation runs in base; broker amounts show in native.
- **Multiple goals** — create separate portfolios for different accounts (e.g. one for your IRA, one for your taxable account).

---

## Privacy

- No server, no database, no analytics.
- All calculations run locally in your browser.
- Nothing leaves your machine except optional API price requests sent directly to your chosen provider.
- API keys are stored only in your browser session — never hardcoded, never logged.

---

## Tech Stack

Single HTML file — HTML, CSS, vanilla JavaScript. No frameworks, no build tools, no dependencies. Open directly in any modern browser.

---

## License

MIT — free to use, fork, and modify.

---

# Changelog

## v6 (Stage 3) — Multi-Currency + UI Overhaul

**Allocation engine:**
- Dynamic base currency — switch it and everything re-converts; sleeve targets stay fixed.
- Per-ticker currency field — holdings in different currencies coexist.
- `toBase` / `fromBase` conversion layer — all math flows through it.
- FX rates from frankfurter.app — auto-fetched, cached in localStorage, manually editable.
- Missing-rate gate — allocation is blocked until every active currency has a rate.
- Native-currency broker amounts in Ticker Breakdown.
- Cap-overflow recovery — undeployable sleeve budget returns to the pool instead of disappearing.
- `tickerBuy` now reflects whole-unit purchases, so sleeve totals reconcile to ticker buys.

**UI features added:**
- Multiple portfolios (up to 5) with animated tab switching.
- Drag-to-reorder sleeves and holdings with floating ghost preview.
- 10-step onboarding tour.
- Share URL (base64 encoded portfolio state).
- Dark / Light mode toggle.
- Market ticker background (your Holdings tickers scrolling in real time).
- Export CSV and Print Plan.
- Days since rebalance counter.
- Auto-save indicator.
- Mobile responsive layout.
- Search/filter holdings.
- Sortable Ticker Breakdown columns.
- Smooth portfolio switch transition.

## v5 (Stage 2) — Optimization Modes

- Version A / Version B selector.
- Global fee-budget cap (Version B).
- Smallest-trade cutting with within-sleeve redistribution.
- Upward-overshoot tolerance with shared `applyWholeUnitRoundingGate()` helper.

## v4 (Stage 1) — Fees & Fractional Shares

- Optional fixed and percentage transaction fees.
- Per-ticker fractional-shares checkbox.
- Fee payment cascade (cash reserve → existing cash → stock allocation).
- Strict no-debt constraint.

## v3 — Per-Ticker Max % Cap

- Max % column in Holdings.
- Ticker Breakdown table in results.
- Iterative overflow redistribution (up to 20 iterations).
- Within-sleeve discipline — overflow never crosses sleeve boundaries.

## v1–v2 — Foundation

- Buy-only allocation engine.
- Dynamic sleeve system (add, rename, recolor, delete).
- Three-tier cash priority.
- localStorage persistence.
- Export / Import JSON.
- Live price refresh with six API providers.

---

## Locked Architectural Invariants

These rules hold across every version:

- Target dollars are always measured against `totalAfter`, never `totalNow`.
- Recycled dollars from cut or capped trades stay within the same sleeve and never spill across sleeves.
- Version B's fee budget is a global cap on total fees combined, not per-trade.
- Per-ticker fractional flags default to whole-units.
- Guard comparisons run in **base** currency; unit counting runs in **native** currency.
- A single-currency portfolio produces identical results to the pre-multi-currency engine.
