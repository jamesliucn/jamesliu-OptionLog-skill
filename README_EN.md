**[中文](README.md) | English**

# jamesliu-OptionLog-skill

A ChatGPT Skill for maintaining a structured **SPX options trading journal**, currently optimized for **SPX Put Credit Spreads (PCS / Bull Put Credit Spreads)** traded through thinkorswim / Schwab.

## Purpose

This Skill turns trading screenshots and supplemental trade details into a structured, auditable trading journal. It maintains the user's Google Sheets trade log, archives supporting screenshots in Google Drive, calculates trading costs and performance, and keeps strategy statistics consistent over time.

Typical workflow:

> Entry screenshot → Log trade → Record OCO exits → Add Delta / VIX context → Closing fill → Calculate net P&L and fees → Update strategy statistics

## Key Features

- Extracts entry and exit information from thinkorswim screenshots.
- Maintains sequential official trade IDs such as `001`, `002`, `003`.
- Keeps entry and exit information for the same trade on a single row.
- Separates official strategy trades from accidental or mistaken orders.
- Records Short Put, Long Put, spread width, DTE, short-leg Delta, OTM%, VIX, credit, TP and SL.
- Distinguishes planned order prices from actual fill prices.
- Records timestamps in `UTC+8` to match the user's thinkorswim workflow.
- Separates commissions, exchange/other fees, and total transaction costs.
- Calculates Gross P&L, Final Net P&L, Premium Capture Rate, Holding Period, and Fees as % of Gross P&L.
- Supports strategy metrics including Win Rate, Average Win/Loss, Payoff Ratio, Expectancy, Profit Factor, Maximum Drawdown, and consecutive losses.
- Archives official trade screenshots in a dedicated Google Drive folder.
- Maintains screenshot links in the Google Sheet's `交易截图` tab.
- Preserves user modifications to spreadsheet fields, formulas, formatting, and folder organization.

## Core Bookkeeping Principles

1. **Actual fills are authoritative.** Screenshots are the primary evidence for execution details.
2. **Never invent missing data.** Unknown Delta, VIX, fees, timestamps, or fills remain marked as pending or unrecorded.
3. **Mistaken orders do not count.** Accidental trades receive no official trade number and are excluded from strategy statistics.
4. **One trade, one row.** Closing information updates the original trade row.
5. **Net P&L includes all confirmed costs.** Final Net P&L is not treated as exact until the required fees are known.
6. **Preserve the existing journal.** The Skill updates the live Google Sheet instead of rebuilding or replacing the user's customized structure.

## Default Resources

The Skill looks for the existing:

- Google Sheet: `SPX PCS 交易日志`
- Google Drive screenshot folder: `SPX Option交易日志截图`

When these resources exist, the Skill updates them in place rather than creating duplicates.

## Repository Structure

```text
.
├── README.md
├── README_EN.md
├── SKILL.md
└── references/
    └── example-workflow.md
```

## Example

For an SPX PCS with:

- Short Put: 7350
- Long Put: 7300
- Credit: 4.40
- Short-leg Delta: ≈ -0.15
- VIX: ≈ 16
- Take Profit: 2.20
- Stop trigger: 8.80

the Skill records the confirmed entry data while leaving closing fields pending. Once an actual closing-fill screenshot is provided, it updates the same trade row and calculates the final result.

## Files

- **README.md** — Chinese overview and usage documentation.
- **README_EN.md** — English overview and usage documentation.
- **SKILL.md** — Complete operational rules for the trading-journal workflow.
- **references/example-workflow.md** — Example workflow from entry through OCO management and closing.

## Future Extensions

The workflow can be expanded to support:

- MAE / MFE
- Delta / DTE / VIX segmented analysis
- Maximum drawdown
- Consecutive-loss analysis
- Roll tracking
- Capital efficiency and annualized returns
- Additional options strategies

## Disclaimer

This Skill is designed for trade journaling, bookkeeping, and retrospective analysis. It does not provide personalized investment advice or guarantee trading outcomes.
