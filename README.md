# FVG Validated Order Blocks

A TradingView Pine Script v5 indicator that marks order blocks using a stricter definition than the usual "last opposite candle" approach. An order block is only valid here if it anchors a Fair Value Gap (FVG) — the candle that sits at the origin of an imbalance created by an impulsive move. Candle color does not matter; what matters is that the block is the foundation of a gap running away from it.

## Overview

<table>
  <tr>
    <td width="50%"><img src="https://www.tradingview.com/x/rPwciMiu/" width="100%"></td>
    <td width="50%"><img src="https://www.tradingview.com/x/G1EjDC2N/" width="100%"></td>
  </tr>
  <tr>
    <td width="50%"><img src="https://www.tradingview.com/x/FoZzI1WD/" width="100%"></td>
    <td width="50%"><img src="https://www.tradingview.com/x/TdU3IyUJ/" width="100%"></td>
  </tr>
</table>

## Core Logic

When price leaves a swing, an impulsive leg often prints several FVGs stacked along it. Many candles could technically qualify as an order block, but they are not equally meaningful. This script selects the **origin-most** one — the deepest FVG-anchoring candle at the base of the move — because that is where the unfilled imbalance and the institutional footprint originate. Secondary gaps further up the leg are ignored.

The engine tracks a rolling set of recent swing highs and lows rather than only the latest one, so clustered swings at tops and bottoms each get their own order block instead of overwriting each other.

## Detection Modes

- **First FVG off Swing** *(default)* — on each confirmed swing, the order block is placed at the origin FVG of the leg.
- **Structure Break (BOS)** — the stricter option: an order block is only sought after price closes beyond a tracked swing, confirming a break of structure. An optional fallback can mark a standard order block (dashed) on break legs that contain no FVG.

## Mitigation

Each order block can be invalidated three ways, selectable in settings:

| Mode | Trigger |
|------|---------|
| **Close Through** | Price closes beyond the far edge of the block |
| **Wick Touch** | Price first trades back into the zone (near edge) |
| **50% Touch** *(default)* | Price reaches the OB midpoint / equilibrium |

A 50% equilibrium line is drawn across every block. Mitigated order blocks and mitigated FVGs can be shown or hidden independently, so you can keep active zones clean while still seeing where spent zones were.

## Features

- ATR-scaled displacement filter to suppress minor order blocks (useful on higher timeframes)
- Optional FVG confluence boxes and "OB"/"FVG" labels
- Fully customizable colors, sizes, and a no-repaint bar-close option
- Performance-bounded: rolling arrays are pruned and the number of drawn blocks is capped, so the chart stays responsive on deep history

## Installation

1. Open TradingView and create a new chart
2. Click **Pine Editor** at the bottom of the screen
3. Copy the entire contents of [`FVG-Validated-Order-Blocks.pine`](FVG-Validated-Order-Blocks.pine)
4. Paste it into the Pine Editor
5. Click **Add to chart**

## How to Use

Order blocks act as potential reaction zones. The 50% line is a common entry reference within a block. Tune **Swing Pivot Length** for the structure size you trade, and raise the **Min Impulse Displacement (ATR)** filter on higher timeframes to keep only significant blocks. Adjust the mitigation mode to match how strictly you want zones to expire.

For Monthly/Weekly charts, raise the displacement filter to ~1.5–3 ATR to suppress minor structure.

## Settings Overview

| Group | Purpose |
|-------|---------|
| 1) Structure / Impulse | Swing detection, lookback window, displacement filter |
| 2) Detection Mode | First-FVG vs BOS, fallback toggle, debug visuals |
| 3) Order Block Boxes | Colors, borders, 50% line |
| 4) Labels | OB/FVG text labels (off by default) |
| 5) FVG Boxes | FVG confluence boxes (off by default) |
| 6) Mitigation | Mitigation mode, mitigated-block visibility |
| 7) Watermark | Credit position |

## Disclaimer

This is an analysis tool, not financial advice. Always combine with your own analysis and risk management. Past chart behavior does not guarantee future results.

## Custom Work / Commissions

Need a tailored version of this indicator, a modified ruleset, or a fully custom Pine Script built for your strategy? Reach out on Telegram — I take on custom indicator commissions.

- Telegram: [@MUH4MM4DSH4KIB](https://t.me/MUH4MM4DSH4KIB)

## Support / Donations

Every contribution — big or small — helps fund new features, bug fixes, and future indicators. Thank you!

### ₿ Crypto Donations

| Currency | Address |
|----------|---------|
| **Bitcoin (BTC)** | `bc1px97s59kkyde66ptvp04amntufahkn3megnys25w7d6hrdy0tqjyszz6gxh` |
| **USDT (ERC-20)** | `0xFFC89D25A6Ff41238982Fd9846D8CE2B22B2b3Cc` |
| **USDT (TRC-20)** | `THssAZhUQEEsw15211rAaRLGRjSWXMX4PW` |

> Every contribution — big or small — helps fund free open-source tools like this one and supports future projects. Thank you!

## Author

**MUHAMMAD SHAKIB**

- GitHub: [@0xSHAK1B](https://github.com/0xSHAK1B)
- Telegram: [@MUH4MM4DSH4KIB](https://t.me/MUH4MM4DSH4KIB)

## License

MIT — see [LICENSE](LICENSE) for details.
