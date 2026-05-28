# Mock CAD Rates, FX, and Trading-Book Pricing

Hi guys! This is a student project I built to practice the kind of basic pricing or PnL or risk work that might sit around a rates/FX desk.

It is by NO means a real trading system!!! It uses fake trades and fake market data. I made it more like a small desk support tool (trade inputs go in, then the script checks the blotter and prices positions, looks at PnL, compares dealer quotes, and then writes some simple reports).

I made this because I wanted something more practical than just writing about fixed income or liquidity risk. This repo is basically trying to connect the concepts from actuarial/financial math coursework to a mock front-office workflow.

## What it essentially does

The project covers a small mock book with:

- Government of Canada style bonds
- CAD FX spot and forwards
- simple interest-rate swaps
- bond forwards
- interest-rate futures

My code produces:

- trade blotter checks
- position valuation
- realised / unrealised style PnL, simplified
- DV01, duration, convexity
- FX exposure
- VaR and Expected Shortfall from a small shock file
- dealer quote comparison
- stale / missing / duplicate trade flags
- basic desk report CSVs

## Why this is still a mock project

Obviously, a real desk would have proper market data feeds and curves and confirmations and a lot more controls. I obviously do not have that here.

So, I kept this as a clean student version, which only deals with:

- mock trade data
- manually supplied market data
- simple curve interpolation
- simplified swap PV logic
- simplified bond forward pricing
- no live market data
- no actual execution

## Repo layout

```text
data/
  trades_mock.csv              mock trade blotter
  market_rates.csv             yield / FX / futures / forward inputs
  dealer_quotes.csv            fake dealer quotes for comparison
  historical_shocks.csv        mock market shocks for VaR / ES
  risk_limits.csv              simple mock limits

src/
  main.py                      runs the whole project
  loader.py                    loads CSV files
  checks.py                    blotter checks and data issues
  pricing.py                   bond / FX / swap / future pricing helpers
  risk.py                      DV01, VaR, ES, limit checks
  reports.py                   writes CSV reports
  config.py                    valuation date and file paths

excel/
  vba_refresh_report.bas       rough VBA macro to refresh CSV outputs in Excel
  workbook_notes.md            how I would wire this into an Excel workbook

docs/
  model_notes.md               notes on assumptions and limitations

outputs/
  reports get written here after running the script
```

## How to run it!

Install the small set of packages:

```bash
pip install -r requirements.txt
```

Run the project:

```bash
python src/main.py
```

The reports will show up in `outputs/`.

## Main outputs

After running it, the main files are:

- `outputs/blotter_issues.csv`
- `outputs/position_report.csv`
- `outputs/pnl_report.csv`
- `outputs/risk_summary.csv`
- `outputs/dealer_quote_comparison.csv`
- `outputs/limit_breaches.csv`
- `outputs/desk_pack.txt`

## Important notes on the modelling itself:

I think it's quite clear by now that I am not claiming the pricing is revolutionary.

For bonds, I used basic discounted cash flow pricing and calculate duration / convexity from cash flows.

For FX spot and forwards, I used the supplied rates and forward points (not building a full cross-currency curve here)

For swaps, I used a simplified fixed-vs-floating approximation from a flat/interpolated curve rate (not NECESSARILY how a real swap book would be priced, if im not mistaken!!!).

For VaR and ES, I used a simple historical shock file. Again, not perfect, but good enough for showing how the risk report could work.

Enjoy!

