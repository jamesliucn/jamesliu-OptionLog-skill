# Example workflow

## Opening a formal PCS

User sends an opening confirmation screenshot and says:
- short-leg Delta ≈ -0.15
- VIX ≈ 16

Actions:
1. Identify next trade number.
2. Record opening date/time, strikes, DTE, credit, fees, Delta, VIX.
3. Calculate net entry credit if fees are confirmed.
4. Leave closing fields pending.
5. Upload the opening screenshot to the dedicated screenshot folder.
6. Add the image link to `交易截图`.

## Adding an exit OCO while trade remains open

User sends GTC OCO setup:
- TP at 2.20
- Stop at 8.80
- `TO CLOSE / TO CLOSE`

Actions:
1. Update TP and stop fields on the same trade row.
2. Do not fill close date/time or close price.
3. Archive the OCO screenshot as `OCO设置`.

## Closing the trade

User sends closing fill:
1. Record actual fill price and UTC+8 timestamp.
2. Record exit commissions and other fees from fee detail if known.
3. Compute gross P&L, total fees, final net P&L, premium capture rate, holding period.
4. Record exit reason, e.g. `TP止盈`, `SL止损`, `DTE规则`, `手动平仓`, `Roll`.
5. Archive the closing-fill screenshot.
6. Update statistics.
