# jamesliu-OptionLog-skill

一个用于维护 **SPX 期权交易日志** 的 ChatGPT Skill，当前主要针对 thinkorswim / Schwab 中的 **SPX Put Credit Spread（PCS / Bull Put Credit Spread）** 交易。

## 用途

这个 Skill 的目标是把“交易截图 + 口头补充信息”整理成结构化、可长期复盘的交易记录，并同步维护 Google Sheets 与 Google Drive 中的交易证据。

适合这样的工作流：

> 开仓截图 → 记录交易 → 设置 OCO → 补充 Delta / VIX 等信息 → 平仓截图 → 计算净利润与费用 → 更新策略统计

## 主要功能

- 从 thinkorswim 截图中提取开仓、平仓、行权价、到期日、Credit、费用等信息。
- 使用连续交易编号：`001`、`002`、`003`……
- 开仓和平仓写在同一行，避免一笔交易被拆成多条记录。
- 区分正式交易与误操作；误操作不进入胜率、收益率、Expectancy、Profit Factor 等统计。
- 记录 Short Put / Long Put、Spread Width、DTE、Short Leg Delta、OTM%、VIX 等交易环境信息。
- 记录 TP / SL / OCO，并区分计划价格和实际成交价格。
- 按 `UTC+8` 保存用户 thinkorswim 中显示的交易时间。
- 拆分记录 Commission、Exchange Fees、Total Fees。
- 计算 Gross P&L、Final Net P&L、Premium Capture Rate、Holding Period、Fees as % of Gross P&L。
- 在长期数据积累后维护 Win Rate、Average Win/Loss、Payoff Ratio、Expectancy、Profit Factor、Maximum Drawdown 等策略指标。
- 自动将正式交易截图归档到 Google Drive 专用截图文件夹。
- 在 Google Sheet 的 `交易截图` 标签中保存原始截图链接。
- 尊重并保留用户对 Google Sheet 的字段、公式、格式和目录结构修改。

## 关键记账原则

1. **截图是实际成交信息的主要依据。**
2. **不猜数据。** Delta、VIX、费用、时间等缺失时标记为 `未记录` 或 `待确认`。
3. **误操作不记账。** 不分配正式交易编号，也不计入策略统计。
4. **同一笔交易只占一行。** 平仓时更新原交易行。
5. **净利润必须扣除完整费用。** 平仓费用未确认时，不把 Final Net P&L 当作精确值。
6. **优先维护现有日志。** 不随意重建 Google Sheet，也不覆盖用户自己的结构调整。

## 默认资源

Skill 默认会寻找：

- Google Sheet：`SPX PCS 交易日志`
- Google Drive 截图目录：`SPX Option交易日志截图`

如果资源仍存在，应直接更新原文件，而不是新建替代版本。

## 目录

```text
.
├── README.md
├── SKILL.md
└── references/
    └── example-workflow.md
```

## 示例

假设一笔 PCS：

- Short Put: 7350
- Long Put: 7300
- Credit: 4.40
- Short-leg Delta: ≈ -0.15
- VIX: ≈ 16
- TP: 2.20
- Stop trigger: 8.80

Skill 会把开仓信息写入正式交易行；如果交易尚未平仓，则平仓日期、价格、最终净利润等字段保持待确认。等收到真实平仓成交截图后，再更新同一行并计算最终结果。

## 文件说明

- **SKILL.md**：完整的 Skill 行为规则与记账逻辑。
- **references/example-workflow.md**：开仓 → OCO → 平仓的示例工作流。

## 说明

当前规则是根据实际 SPX PCS 交易日志流程定制的。随着交易样本增加，可以继续扩展：

- MAE / MFE
- Delta / DTE / VIX 分组统计
- 最大回撤
- 连续亏损
- Roll 记录
- 资金占用与年化收益
- 多策略支持

