# Salary2045 — Portfolio Rebalancer

**A free browser-based tool that tells you where to deploy new cash in your investment portfolio to stay on target — without selling anything.**

🔗 **[Live Demo → gavrielp1.github.io/Salary2045-Rebalancer](https://gavrielp1.github.io/Salary2045-Rebalancer/)**

---

![Demo](demo.gif)

---

## How it works

Most rebalancing tools tell you to sell overweight positions and buy underweight ones. This tool doesn't. It takes a **buy-only** approach: you enter how much new cash you have to deploy, and the tool tells you exactly where to put it to move your portfolio closer to your target allocation — without triggering any sales or tax events.

---

## Sections

### 1. Target Allocation (Sleeves)

![Target Allocation](screenshot1.png)

Define your portfolio structure using sleeves. Each sleeve represents a category of investments with a target percentage of your total portfolio. The default structure is:

| Sleeve | Default Target |
|---|---|
| Core | 40% |
| Satellite | 38% |
| High Conviction | 10% |
| Hedge | 7% |
| Cash | 5% |

All percentages are fully adjustable. The tool warns you if they don't sum to 100%.

---

### 2. Cash

![Cash and API](screenshot2.png)

Two separate cash fields:

- **Available Cash to Deploy** — new money you're adding now. This is what gets allocated into positions.
- **Existing Cash Position** — cash already sitting in your brokerage account. This counts toward the Cash sleeve target and is factored into the current allocation before any buying.

The tool reserves enough of your new cash to keep the Cash sleeve at its target before deploying the rest into securities.

---

### 3. Live Prices (Optional)

Choose a data provider from the dropdown and paste your API key to refresh prices automatically. Supported providers:

| Provider | Notes |
|---|---|
| **Finnhub** | Recommended. 60 calls/min free tier, CORS-friendly |
| **Twelve Data** | 800 calls/day free tier, CORS-friendly |
| **Financial Modeling Prep** | Free tier, CORS-friendly |
| **Alpha Vantage** | Free tier, limited calls/day |
| **Tiingo** | Free tier, may be CORS-blocked in browser |
| **Polygon** | Free tier, may be CORS-blocked in browser |

If you leave the API key empty, you can enter prices manually. All providers are modular — if one stops working or changes its pricing, switch to another from the dropdown without touching any code.

> ⚠️ Never commit a real API key to a public repo. Leave the API key field empty before publishing.

---

### 4. Holdings

![Holdings and Results](screenshot3.png)

Enter your current positions: ticker, sleeve, number of shares, and price. The tool calculates the value of each position automatically.

- **+ Add Holding** — add a new row
- **Load Sample Portfolio** — loads a pre-built example portfolio to explore the tool
- **✕** — remove a holding

---

### 5. Rebalance Plan

The output section shows:

- **Portfolio Value** — total current value of all holdings + existing cash
- **After Deploy** — portfolio value after the new cash is added
- **Cash Allocated** — how much of the new cash gets deployed into positions
- **Cash Left** — amount reserved for the Cash sleeve target

**Visual bars** show each sleeve's current allocation vs. its target. The white marker on each bar is the target — if the bar falls short, that sleeve is underweight.

**The plan table** breaks down exactly how much to buy in each sleeve:

| Column | Meaning |
|---|---|
| Current % | Sleeve's share of the portfolio right now |
| Target % | Your defined goal |
| Gap | How far off the sleeve is (green = underweight = needs buying) |
| $ To Buy | How much of the new cash goes to this sleeve |

The Cash sleeve shows a **reserve** amount instead of a buy amount — this is the portion of new cash held back to reach the cash target.

---

## Allocation Logic

The tool prioritizes the most underweight sleeves first:

1. Calculates how much each sleeve needs to reach its target based on the total portfolio after deployment
2. If cash is enough to fill all gaps → fills every gap, then spreads the remainder by target weight
3. If cash is not enough → distributes proportionally to each sleeve's gap size (biggest gap gets the most)
4. Cash sleeve is always handled separately — its portion is reserved before the rest is deployed

**Nothing is ever sold. Existing positions are never reduced.**

---

## Tech Stack

Pure HTML + CSS + JavaScript. Single file, zero dependencies, zero backend. Works offline after the first load.

---

## API Key Safety

- Keys stay in your browser — never sent anywhere except directly to the chosen provider's API
- No key is hardcoded in the source
- The field is empty by default — safe to publish as-is
- If a provider changes its pricing model, switch to another from the dropdown without touching any code

---

## License

MIT — free to use, fork, and modify.
