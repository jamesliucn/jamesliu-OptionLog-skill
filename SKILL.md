---
name: spx-trade-journal
description: Maintain the user's SPX options trading journal in Google Sheets. Use when the user sends thinkorswim screenshots or trade details and asks to record, update, reconcile, or analyze SPX option trades, especially PCS/bull put credit spreads. Preserve the user's current Google Sheet structure, store trade screenshots in the dedicated Drive screenshot folder, and keep formal trades separate from accidental orders.
---

# SPX Trade Journal

Use this skill to maintain the user's personal SPX options trading journal from thinkorswim screenshots and stated trade details.

## Connected resources

Preferred Google Sheet:
- Title: `SPX PCS 交易日志`
- Existing native Google Sheet. Search Drive by title if the current file ID is unavailable.

Preferred screenshot folder:
- Title: `SPX Option交易日志截图`
- Keep trade screenshots in this dedicated folder, not beside the spreadsheet.

Do not create a replacement spreadsheet if the existing journal can be found. Edit the existing file in place.

## Core bookkeeping rules

1. Only formal, intentional strategy trades count in the journal and performance statistics.
2. Accidental/mistaken orders are not assigned a trade number and are excluded from win rate, returns, expectancy, profit factor, drawdown, and all strategy statistics.
3. Use sequential formal trade IDs: `001`, `002`, `003`, ...
4. When a trade closes, update the existing row. Do not create a second row for the closing transaction.
5. Screenshots are authoritative for actual fills, dates, times, fees, strikes, and quantities.
6. If Delta is visible, record the exact value. If the user gives an approximate value, preserve `≈`. If unknown, write `未记录`.
7. Primary trade timestamps use the timezone shown by the user's thinkorswim workflow: `UTC+8`. Keep this timezone in the column names.
8. Do not invent missing values. Use `待确认` or `未记录` as appropriate.
9. Preserve user edits to column order, formatting, formulas, tabs, and folder organization unless the user explicitly asks to change them.
10. Before editing, read the current sheet headers and relevant row(s). Treat the live Sheet as the source of truth for its current schema.

## Trade interpretation conventions

For a put credit spread / bull put credit spread (PCS):
- Opening order typically displays as `SELL -1 VERTICAL ... TO OPEN`.
- Closing order typically displays as `BUY +1 VERTICAL ... TO CLOSE`.
- `TO OPEN` vs `TO CLOSE` describes position effect, not simply buy vs sell direction.

For the user's standard PCS management rule when explicitly applicable:
- Take profit: capture 50% of opening credit.
- Stop loss: loss equal to 100% of opening credit.
- Example: credit 4.40 => TP 2.20; stop trigger 8.80.
- If the user specifies different prices, record the actual user-defined plan instead.

OCO notes:
- A GTC OCO is preferred for multi-day exit orders when the user intends the orders to remain active across sessions.
- If an OCO was submitted as Day and expired, record a later replacement OCO only as an order-management screenshot, not as a separate trade.

## Fee accounting

Keep commissions and other fees separate when the Sheet has separate fields.

Preferred fee fields:
- `开仓佣金 / Entry Commission`
- `开仓其他费用 / Entry Other Fees`
- `平仓佣金 / Exit Commission`
- `平仓其他费用 / Exit Other Fees`
- `开仓总费用 / Total Entry Fees`
- `平仓总费用 / Total Exit Fees`
- `总费用 / Total Fees`
- `费用占毛利润 / Fees as % of Gross P&L`

For current thinkorswim SPX vertical examples seen in the user's screenshots:
- Commission may appear as `$1.30` per two-leg vertical per side.
- `Equity and Option Exchange Fees` may appear as `$1.04` per side.
- Total single-side fees in those examples: `$2.34`.
- Do not generalize these amounts to future trades unless confirmed by that trade's screenshot or user statement.

Formulas:
- `Gross P&L = (opening credit - closing debit) × 100 × quantity`
- `Final Net P&L = Gross P&L - Total Entry Fees - Total Exit Fees`
- `Premium Capture Rate = Gross P&L / Opening Premium`
- `Fees as % of Gross P&L = Total Fees / Gross P&L` when Gross P&L is nonzero.

If closing fees are not confirmed, do not present a final net profit as exact. Keep final net P&L pending.

## Preferred trade fields

The live Sheet may evolve. Preserve its current order and names. When the fields exist, maintain:

- Trade #
- Open Date
- Open Time (UTC+8)
- Close Date
- Close Time (UTC+8)
- Underlying
- Strategy
- Expiration
- Entry DTE
- SPX at Entry
- Short Put
- Long Put
- Spread Width
- Short Leg Delta
- OTM %
- VIX
- Credit
- Take-Profit Price
- Stop-Loss Price
- Max Theoretical Profit
- Max Theoretical Loss
- Total Entry Fees
- Net Entry Credit
- Close Price
- Total Exit Fees
- Gross P&L
- Final Net P&L
- Premium Capture Rate
- Holding Period
- Exit Reason
- Entry Commission
- Entry Other Fees
- Exit Commission
- Exit Other Fees
- Total Fees
- Fees as % of Gross P&L

Bilingual field names are preferred when adding new columns.

## Screenshot workflow

When the user sends screenshots related to a formal trade:

1. Identify the trade number.
2. Keep only useful evidence screenshots, such as opening confirmation / opening fill, OCO setup, closing fill, and fee detail.
3. Upload or move those screenshots into the Drive folder `SPX Option交易日志截图`.
4. Use descriptive filenames such as `SPX_PCS_002_开仓确认.png`, `SPX_PCS_002_OCO设置.png`, `SPX_PCS_002_平仓成交.png`, `SPX_PCS_002_费用明细.png`.
5. Add or update the `交易截图` tab with the trade number, screenshot type, and a Drive hyperlink to the original image.
6. Do not mix accidental-order screenshots into the formal trade evidence unless the user explicitly wants them archived separately.

## Google Sheets workflow

For every edit:

1. Locate the exact existing spreadsheet `SPX PCS 交易日志` in Google Drive.
2. Read spreadsheet metadata.
3. Read the current header row and the target trade row before writing.
4. Make the smallest necessary update.
5. Preserve formulas and formatting outside the requested cells.
6. If adding a new trade, append the next formal trade row; do not overwrite prior trades.
7. If the user provides a correction, update the existing row rather than adding a duplicate.
8. If the trade is still open, leave close fields pending.
9. If the trade closes, populate the same row and update strategy statistics.
10. After writing, re-read the updated cells to verify the values.

## Strategy statistics

Maintain or support these metrics when enough closed trades exist:
- Official trade count
- Closed trade count
- Winning trades
- Win rate
- Average win
- Average loss
- Payoff ratio
- Expectancy per trade
- Profit Factor
- Cumulative net P&L
- Maximum drawdown
- Maximum consecutive losses
- Average holding period
- Fees as % of gross P&L

Prefer `Final Net P&L` over `Gross P&L` for long-run performance metrics once all fees are confirmed.

## User-facing responses

After recording a trade, reply concisely with:
- trade number
- what was added/updated
- any fields still pending
- a link to the Google Sheet when available

If screenshots were archived, state that they were placed in the dedicated screenshot folder.

Do not claim a trade is closed until an actual closing fill is confirmed.
Do not report final net profit as exact until all required fees are known.
