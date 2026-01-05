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

## 📊 Strategy & Allocation  
### Complete Mathematical Definition

ด้านล่างคือกลยุทธ์การจัดสรรสินทรัพย์ทั้งหมดที่ใช้ในระบบ  
พร้อมสูตรคำนวณน้ำหนัก (Weighting Formula) อย่างชัดเจน

---

### 1️⃣ Equal Weight (1/N)

**Formula**
```

w_i = 1 / N

```

- N = จำนวนสินทรัพย์ทั้งหมด

---

### 2️⃣ Rank All (Momentum Weighted)

**Formula**
```

Rank_i = ลำดับ Momentum (1 = สูงสุด)

w_i = (N - Rank_i + 1) / Σ(N - Rank_j + 1)

```

---

### 3️⃣ Top 3 Leader (Equal Weight)

**Formula**
```

w_i = 1 / K   , i ∈ Top K
w_i = 0       , otherwise

```

- K = 3

---

### 4️⃣ Top 3 Leader (Rank Weighted)

**Formula**
```

Rank_i ∈ {1,2,3}

w_i = (K - Rank_i + 1) / Σ(K - Rank_j + 1)

```

---

### 5️⃣ Top 50% Selection

**Formula**
```

K = ceil(N / 2)

w_i = 1 / K   , i ∈ Top 50%
w_i = 0       , otherwise

```

---

### 6️⃣ Absolute Momentum (ROC > 0)

**Momentum**
```

ROC_i = P_t / P_(t-L) - 1

```

**Weight**
```

w_i = 1 / M   , ROC_i > 0
w_i = 0       , ROC_i ≤ 0

```

- M = จำนวนสินทรัพย์ที่ ROC > 0

---

### 7️⃣ Dual Momentum (Relative + Absolute)

**Formula**
```

Eligible_i = { i | Rank_i ≤ K AND ROC_i > 0 }

w_i = 1 / |Eligible| , i ∈ Eligible
w_i = 0              , otherwise

```

- K = 3

---

### 8️⃣ Inverse Volatility (Risk Parity)

**Volatility**
```

σ_i = StdDev(returns_i)

```

**Weight**
```

w_i = (1 / σ_i) / Σ(1 / σ_j)

```

---

## 📐 Rebalancing & Transaction Cost

**Rebalance Rule**
```

Rebalance every RB days

```

**Turnover**
```

Turnover = Σ |w_i(new) - w_i(old)|

```

**Transaction Cost**
```

Equity_after = Equity_before × (1 - Turnover × Fee)

```

---

## 🧠 Strategy Summary

| Strategy | Selection | Weighting |
|--------|----------|-----------|
| Equal | All | Equal |
| Rank | All | Rank-based |
| Top3 | Top 3 | Equal |
| Top3Rank | Top 3 | Rank-based |
| Top50 | Top 50% | Equal |
| AbsMom | ROC > 0 | Equal |
| DualMom | Top K + ROC > 0 | Equal |
| InvVol | All | Inverse Volatility |

---

## 📈 Portfolio Analytics
- CAGR
- Sharpe Ratio
- Max Drawdown
- Turnover
- Benchmark Comparison

---

## 🔬 Visualization
- Equity Curve (Linear / Log)
- Drawdown Curve
- Sharpe Surface (LB × RB)
- Monte Carlo Simulation
- Correlation Matrix
- Monthly Heatmaps
- Rebalance Logs

---

## 🧩 Tech Stack

| Layer | Technology |
|------|-----------|
| UI | HTML5, TailwindCSS |
| Charts | Chart.js, Plotly |
| Math | Math.js |
| Runtime | Vanilla JS |
| Deploy | GitHub Pages |

---

## 🧪 Data Model

Uses **stochastic market simulation (GBM)**  
Not connected to real market data.

---

## ⚠️ Disclaimer

For educational & research purposes only.  
**Not investment advice.**

---

## 📜 License
MIT License

---

## 👤 Author
**Waranyu Teerakomen**  
Quant Research & Portfolio Analytics
