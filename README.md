# 📈 APEX TRADE — Binary Option Game

A browser-based binary options trading simulator with live candlestick charts and real-time price simulation. Built with pure HTML, CSS, and vanilla JavaScript — no frameworks, no dependencies.

![Game Preview](https://img.shields.io/badge/status-playable-00e5a0?style=for-the-badge)
![HTML](https://img.shields.io/badge/HTML-pure-orange?style=for-the-badge&logo=html5)
![CSS](https://img.shields.io/badge/CSS-vanilla-blue?style=for-the-badge&logo=css3)
![JS](https://img.shields.io/badge/JS-vanilla-yellow?style=for-the-badge&logo=javascript)

---

## 🎮 How to Play

1. **Set your investment** — enter an amount or use quick buttons ($10 / $25 / $50 / $100)
2. **Choose expiry time** — 5s, 10s, 15s, 30s, or 60s
3. **Predict the direction:**
   - Click **▲ HIGHER** if you think the price will be higher when the timer expires
   - Click **▼ LOWER** if you think the price will be lower
4. **Wait** — watch the live candlestick chart while the countdown runs
5. **Result:**
   - Correct prediction → win **85% profit** on your investment
   - Wrong prediction → lose your investment

> **Example:** Invest $100, predict HIGHER with 10s expiry.
> BTC price at entry: $42,350. Price after 10s: $42,410 → **WIN +$85**

---

## ✨ Features

- **Live candlestick chart** — BTC/USD price simulated via Geometric Brownian Motion (GBM), renders every 200ms
- **Entry line indicator** — dashed line on chart shows your entry price during active trade
- **Countdown ring** — circular SVG timer that changes color (green → amber → red) as time runs out
- **Live P&L indicator** — shows real-time winning/losing status as price moves during the trade
- **Animated result card** — win/lose overlay with profit details after each trade
- **Trade history** — timestamped log with entry/exit prices and P&L
- **Session statistics** — Balance, Wins, Losses, Win Rate, Net P&L
- **Bloomberg terminal aesthetic** — dark theme with grid background, scanline overlay, IBM Plex Mono font
- **Responsive layout** — works on desktop and mobile

---

## 🧮 Price Simulation

The BTC/USD price is generated using a **Geometric Brownian Motion (GBM)**-inspired model:

```js
// Trend drift — slowly shifts direction over time
trend += (Math.random() - 0.5) * 0.002;
trend = clamp(trend, -0.003, 0.003);

// Price update
const noise = (Math.random() - 0.5) * volatility * price;
const drift = trend * price * 0.1;
price = price + noise + drift;
```

- Price ticks every **200ms**
- Candlesticks form every **10 ticks** (2 seconds per candle)
- Volatility: `0.08%` per tick
- Price bounds: `$30,000 – $80,000`

---

## 💰 Payout Structure

| Outcome              | Return                            |
|----------------------|-----------------------------------|
| Correct prediction   | Investment + 85% profit           |
| Wrong prediction     | Lose investment (0% return)       |

```
Payout   = investment × 1.85
Net profit = investment × 0.85
```

The effective house edge is **~8%** (pays 85% on a ~50/50 game).

---

## 📁 Project Structure

```
apex-trade/
└── index.html      # Single-file game — everything included
```

No build step. No npm install. Just open `index.html` in a browser.

---

## 🚀 Getting Started

```bash
git clone https://github.com/yourusername/apex-trade.git
cd apex-trade
open index.html
```

Or simply drag `index.html` into any modern browser.

---

## 🎨 Tech Stack

| Layer      | Technology                                        |
|------------|---------------------------------------------------|
| Chart      | HTML5 Canvas (2D) — custom candlestick renderer   |
| Styling    | Pure CSS (custom properties, keyframes, SVG ring) |
| Logic      | Vanilla JavaScript (setInterval, GBM price model) |
| Fonts      | Google Fonts — Orbitron, Barlow Condensed, IBM Plex Mono |

---

## ⚙️ Configuration

Tweak these variables in the `<script>` block:

| Variable       | Default  | Description                          |
|----------------|----------|--------------------------------------|
| `balance`      | `1000`   | Starting balance ($)                 |
| `PAYOUT_RATE`  | `0.85`   | Profit rate on winning trades        |
| `TICK_MS`      | `200`    | Price update interval (milliseconds) |
| `CANDLE_TICKS` | `10`     | Ticks per candlestick                |
| `volatility`   | `0.0008` | Price volatility per tick            |
| `HISTORY_LEN`  | `250`    | Max price history length             |

---

## 📸 Preview

```
┌──────────────────────────────────────────────────────┐
│  APEX TRADE  Binary Options         Balance: $1,000  │
├────────────────────────────────┬─────────────────────┤
│  BTC/USD  $42,350.00  +0.023%  │  New Trade          │
│                                │  Investment: $50    │
│  [Live Candlestick Chart]      │  Expiry:  [10s] ✓  │
│                                │  Payout: +$42.50    │
│  ----entry $42,350----         │  [▲ HIGHER][▼ LOWER]│
│                     ⏱ 7s      ├─────────────────────┤
│                                │  Active Trade       │
│                                │  ▲ HIGHER           │
│                                │  Entry: $42,350     │
│                                │  Current: $42,391   │
│                                │  ▲ Winning +$42.50  │
├────────────────────────────────┴─────────────────────┤
│  Balance   Wins   Losses   Win Rate   Net P&L        │
│  $1,042    3      1        75%        +$77.50        │
└──────────────────────────────────────────────────────┘
```

---

## 🔄 How It Differs from Crash Games

| Feature        | Moonshot (Crash)          | Apex Trade (Binary Option)     |
|----------------|---------------------------|--------------------------------|
| Mechanic       | Cash out before crash     | Predict UP or DOWN direction   |
| Timing         | Player-controlled         | Fixed expiry (5s – 60s)        |
| Risk           | Variable (multiplier)     | Fixed (lose all or win 85%)    |
| Skill element  | Timing & nerve            | Market direction reading       |
| Chart type     | Line (multiplier curve)   | Candlestick (price chart)      |

---

## ⚠️ Disclaimer

This is a **simulation game** for entertainment and educational purposes only. No real money is involved. The price data is entirely simulated and does not reflect actual market conditions.

Binary options trading with real money carries significant risk and is heavily regulated or prohibited in many jurisdictions. This project does not encourage real trading.

---

## 📄 License

MIT License — free to use, modify, and distribute.
