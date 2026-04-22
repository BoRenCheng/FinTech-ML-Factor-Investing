# FinTech-ML-Factor-Investing
基於機器學習與深度學習之台股多因子選股模型實證研究 (1999-2025)
# 使用線性迴歸(OLS)、隨機森林（RF）、類神經網路(NN)等機器學習進行因子預測分析

# 以規模、帳面市值比、動能當因子運用AI機器學習來建構市場投資組合

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Financial-Tech](https://img.shields.io/badge/Domain-FinTech-green.svg)
![Quant](https://img.shields.io/badge/Strategy-Factor_Investing-orange.svg)

本專案為「金融科技創新與應用」課程之期末研究成果。研究目標在於運用傳統統計與現代 AI 模型，針對台灣股市 26 年（1999-2025）的歷史資料，預測財務因子的**資訊係數 (Information Coefficient, IC)**，進而建構多空投資組合並進行量化回測。

---

## 研究背景與資料描述

面對大數據時代，本專案探討非線性模型（機器學習、深度學習）在金融時間序列預測上，是否能比傳統線性模型提供更穩健的超額報酬（Alpha）。

* **資料來源**：TEJ Pro (台灣經濟新報)
* **時間跨度**：1999 年 01 月 — 2025 年 01 月
* **研究樣本**：台灣上市櫃公司，總計 964 檔股票。
* **回測窗口**：2014 年 01 月 — 2025 年 01 月。

---

## 特徵工程與模型建構

本研究選用 Fama-French 三因子理論作為基礎，並實作多達 10 種模型進行交叉驗證：

### 1. 因子定義 (Input Features)
* **Size (規模因子)**：`log10(市值)`。
* **BM (價值因子)**：股價淨值比的倒數。
* **Momentum (動能因子)**：過去 12 個月對數報酬率。

### 2. 模型演算法
* **Baseline**: 傳統線性迴歸 (OLS)。
* **Ensemble Learning**: 隨機森林 (Random Forest, 100 棵樹)、XGBoost。
* **Deep Learning**: 
  * 5 種不同深度的類神經網路 (**NN1 ~ NN5**)，導入 L1 正則化與 Early Stopping 防止過擬合。
  * **LSTM** (Long Short-Term Memory) 捕捉時序特性。

---

## 核心成果分析 (Performance Analysis)

我們對 964 檔股票進行了不同精細度（10 等分至 964 等分）的排序與回測。以下為核心發現：

### 1. 模型勝率 (Win Rate)
| 投資組合等分 | OLS (預測) | 隨機森林 (RF) | 神經網路 (NN5) | XGBoost |
| :--- | :--- | :--- | :--- | :--- |
| **192 等分** | 52.9% | **61.9%** | 56.7% | 50.0% |
| **241 等分** | 55.2% | **61.9%** | 58.2% | 51.5% |

### 2. 風險收益比 (Sharpe Ratio)
在 20 等分與 50 等分的穩定投資策略下，**隨機森林 (RF)** 與 **NN5** 展現出極高的穩健度：
* **RF / NN5 夏普比率**：**0.432** (在 50 等分下)。
* **大盤同期夏普比率**：0.173。
* **結論**：AI 模型所建構的選股策略，其風險調整後收益為大盤的 **2.5 倍**。

### 3. 累積報酬回測
隨機森林在 241 等分下取得最佳累積報酬（約 4.63），顯示在台灣市場中，集成學習對於財務因子的非線性捕捉能力優於純深度學習。

---
```text
FinTech-ML-Factor-Investing/
├── docs/                       # 存放報告與技術文件
│   └── 金融科技_期末報告.pdf
├── results/                    # 核心數據區 (所有 CSV 放置處)
│   ├── summary/                # 跨模型績效總結指標
│   ├── cumulative_returns/     # 各分組等分的累積報酬趨勢
│   └── model_details/          # 單一模型深入指標
│       ├── rf/                 # 隨機森林相關
│       └── nn_series/          # NN1 至 NN5 相關
├── .gitignore                  # 忽略不必要的系統暫存檔
└── README.md                   # 專案說明文件
