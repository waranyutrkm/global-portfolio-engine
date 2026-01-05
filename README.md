# 🏛️ Global Portfolio Engine v30.5  
**Professional Quant Portfolio Analytics Suite (Client-Side Web App)**

![Status](https://img.shields.io/badge/status-active-success)
![Type](https://img.shields.io/badge/type-quant%20research-blue)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 🚀 Live Demo
👉 **https://waranyutrkm.github.io/global-portfolio-engine/**

> Fully client-side • No backend • No API keys required

---

## 📌 Overview

**Global Portfolio Engine** คือเครื่องมือวิเคราะห์พอร์ตเชิงปริมาณ (Quantitative Portfolio Analytics)  
ที่ออกแบบมาเพื่อ:
- วิเคราะห์กลยุทธ์การจัดสรรสินทรัพย์ (Asset Allocation)
- เปรียบเทียบ Momentum / Risk-Based Strategies
- สำรวจผลลัพธ์เชิงลึกผ่าน Visualization แบบมืออาชีพ

ทั้งหมดทำงาน **บน Browser 100%** โดยไม่ต้องใช้ Server

---

## 🧠 Key Capabilities

```
## 📊 Strategy & Allocation (Complete Mathematical Definition)

ด้านล่างคือกลยุทธ์การจัดสรรสินทรัพย์ทั้งหมดที่ใช้ในระบบ  
พร้อม **สูตรคำนวณน้ำหนัก (Weighting Formula)** อย่างชัดเจน

---

### 1️⃣ Equal Weight (1/N)

**แนวคิด:**  
กระจายน้ำหนักเท่ากันทุกสินทรัพย์ใน Universe

**Formula:**
```

w_i = 1 / N

```

- N = จำนวนสินทรัพย์ทั้งหมด
- w_i = น้ำหนักของสินทรัพย์ตัวที่ i

---

### 2️⃣ Rank All (Momentum Weighted)

**แนวคิด:**  
เรียงสินทรัพย์ตามค่า Momentum (สูง → ต่ำ)  
ให้น้ำหนักลดหลั่นตามอันดับ

**Formula:**
```

Rank_i = ลำดับของ Momentum (1 = ดีที่สุด)

w_i = (N - Rank_i + 1) / Σ(N - Rank_j + 1)

```

- N = จำนวนสินทรัพย์ทั้งหมด
- Σ = ผลรวมทุกสินทรัพย์

---

### 3️⃣ Top 3 Leader (Equal Weight)

**แนวคิด:**  
เลือกเฉพาะ 3 ตัวที่ Momentum สูงสุด  
แล้วกระจายน้ำหนักเท่ากัน

**Formula:**
```

w_i = 1 / K   ,  i ∈ Top K
w_i = 0       ,  otherwise

```

- K = 3 (หรือ ≤ N ถ้ามีน้อยกว่า 3)

---

### 4️⃣ Top 3 Leader (Rank Weighted)

**แนวคิด:**  
เลือก 3 ตัวที่ดีที่สุด  
ให้น้ำหนักตามอันดับ (Rank-based)

**Formula:**
```

Rank_i ∈ {1, 2, 3}

w_i = (K - Rank_i + 1) / Σ(K - Rank_j + 1)

```

- K = 3
- Σ = ผลรวมเฉพาะ Top 3

---

### 5️⃣ Top 50% Selection

**แนวคิด:**  
ลงทุนเฉพาะครึ่งบนของสินทรัพย์ที่มี Momentum สูงสุด

**Formula:**
```

K = ceil(N / 2)

w_i = 1 / K   ,  i ∈ Top 50%
w_i = 0       ,  otherwise

```

---

### 6️⃣ Absolute Momentum (ROC > 0)

**แนวคิด:**  
ลงทุนเฉพาะสินทรัพย์ที่ Momentum เป็นบวก  
ที่เหลือถือเป็น Cash (Implicit)

**Momentum Definition:**
```

ROC_i = P_t / P_(t-L) - 1

```

**Weight Formula:**
```

w_i = 1 / M   ,  ROC_i > 0
w_i = 0       ,  ROC_i ≤ 0

```

- M = จำนวนสินทรัพย์ที่ ROC > 0

---

### 7️⃣ Dual Momentum (Relative + Absolute)

**แนวคิด:**  
ต้องผ่าน 2 เงื่อนไขพร้อมกัน:
1. อยู่ในกลุ่ม Top K (Relative Momentum)
2. ROC > 0 (Absolute Momentum)

**Formula:**
```

Eligible_i = { i | Rank_i ≤ K  AND  ROC_i > 0 }

w_i = 1 / |Eligible|   ,  i ∈ Eligible
w_i = 0                ,  otherwise

```

- K = 3
- |Eligible| = จำนวนสินทรัพย์ที่ผ่านเงื่อนไข

---

### 8️⃣ Inverse Volatility (Risk Parity)

**แนวคิด:**  
ให้น้ำหนักผกผันกับความผันผวน  
สินทรัพย์ที่เสี่ยงน้อย → น้ำหนักมาก

**Volatility Definition:**
```

σ_i = StdDev(returns_i)

```

**Weight Formula:**
```

w_i = (1 / σ_i) / Σ(1 / σ_j)

```

- σ_i = Volatility ของสินทรัพย์ i
- Σ = ผลรวมทุกสินทรัพย์

---

## 📐 Rebalancing & Transaction Cost

### Rebalance Condition
```

Rebalance ทุก ๆ RB วัน

```

### Turnover
```

Turnover = Σ |w_i(new) - w_i(old)|

```

### Transaction Cost Impact
```

Equity_after_fee = Equity_before × (1 - Turnover × Fee)

```

- Fee = % ต่อการปรับพอร์ต

---

## 🧠 Summary Table

| Strategy | Selection | Weighting Logic |
|--------|----------|----------------|
| Equal | All | Equal |
| Rank | All | Rank-based |
| Top3 | Top 3 | Equal |
| Top3Rank | Top 3 | Rank-based |
| Top50 | Top 50% | Equal |
| AbsMom | ROC > 0 | Equal |
| DualMom | Top K + ROC > 0 | Equal |
| InvVol | All | Inverse Volatility |
```


### 📈 Portfolio Analytics
- CAGR
- Sharpe Ratio
- Max Drawdown
- Turnover & Transaction Cost Impact
- Benchmark Comparison

### 🔬 Advanced Quant Visualization
- Equity Curve (Linear / Log Scale)
- Drawdown Waterfall
- Hyper-Parameter Sharpe Surface
- Monte Carlo Simulation (1Y Forward)
- Asset Correlation Matrix
- Monthly Return & Drawdown Heatmaps
- Full Rebalance & Allocation Logs

---

## 🧩 Tech Stack

| Layer | Technology |
|------|-----------|
| UI | HTML5, TailwindCSS |
| Charts | Chart.js, Plotly.js |
| Math | Math.js |
| Runtime | Vanilla JavaScript |
| Deployment | GitHub Pages |

> ⚡ Zero backend • Zero build step • Instant deploy

---

## 🖥️ How It Works (Conceptual Flow)

```

Asset Universe
↓
Signal Generation (Momentum / Volatility)
↓
Strategy Weighting Logic
↓
Rebalancing Engine
↓
Portfolio Simulation
↓
Risk & Performance Analytics

```

---

## ▶️ Usage

1. Open the **Live Demo**
2. Select:
   - Strategy Logic
   - Lookback & Rebalance Windows
   - Asset Universe
3. Click **🚀 RUN QUANT ENGINE**
4. Explore results across:
   - KPIs
   - Charts
   - Optimization Matrix
   - Strategy Logs

---

## 🧪 Data Model

> This project uses **stochastic market simulation** (Geometric Brownian Motion)  
> to demonstrate portfolio behavior and analytics logic.

📌 **Not connected to real-time market data**

---

## ⚠️ Disclaimer

This project is for:
- Educational
- Research
- Strategy prototyping purposes only

❗ **Not investment advice**  
❗ **Do not use for live trading decisions**

---

## 🗂️ Project Structure

```

global-portfolio-engine/
└── index.html   # Entire application (UI + Engine)

````

---

## 🛠️ Local Development

```bash
# No install needed
# Just open index.html in your browser
````

Or use a simple local server:

```bash
python -m http.server
```

---

## 📜 License

MIT License
Free to use, modify, and distribute with attribution.

---

## 👤 Author

**Waranyutr T.**
Quant Research & Portfolio Analytics

---

## ⭐ Acknowledgement

Inspired by:

* Quantitative Asset Allocation
* Momentum Investing
* Risk Parity Frameworks

---

> If you find this project useful, feel free to ⭐ star the repository
