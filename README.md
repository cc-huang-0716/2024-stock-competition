# Stock Research Competition Utilities

本專案整理自一次股票研究競賽期間所使用的小型分析工具，主要用於台股個股估值、股利成長率分析、Beta 值估算與基礎篩選。
這些 Notebook 並非完整交易系統，而是競賽研究過程中用來快速驗證估值假設、蒐集市場資料與輔助投資分析的工具集合。

> 本專案僅供研究、學習與競賽紀錄使用，不構成任何投資建議。

---

## Project Overview

本專案主要包含以下幾類分析：

* 使用 Yahoo Finance 資料抓取個股與市場指數價格
* 估算個股 Beta 值
* 使用 CAPM 計算要求報酬率
* 使用 DDM / Gordon Growth Model 進行股利折現估值
* 使用自由現金流與終值模型進行簡化版 DCF 估值
* 針對多檔股票進行股利成長率與估值篩選

---

## Repository Structure

```text
.
├── 1707股價估值.ipynb
├── 估值定案.ipynb
├── 個股Beta值估算.ipynb
├── 個股股利與成長率分析.ipynb
└── README.md
```

---

## Notebook Description

### 1. `1707股價估值.ipynb`

此 Notebook 用於個股估值與股價資料視覺化，主要流程包含：

* 使用 `yfinance` 抓取台股個股歷史收盤價
* 匯出指定期間的收盤價資料
* 根據 CAPM 設定要求報酬率
* 使用 DDM / Gordon Model 估算股利折現價值
* 繪製個股收盤價走勢圖

適合用於快速檢查特定標的的歷史股價與簡單股利估值結果。

---

### 2. `估值定案.ipynb`

此 Notebook 以現金流估值為主，主要流程包含：

* 輸入過去數期每股自由現金流或淨現金流
* 計算現金流成長率與 CAGR
* 推估未來數期現金流
* 使用折現率計算未來現金流現值
* 使用終值模型估算長期價值
* 加總現金流現值與終值現值，估算每股合理價值

此工具主要作為競賽最終估值假設與結果整理使用。

---

### 3. `個股Beta值估算.ipynb`

此 Notebook 用於估算個股相對於市場指數的 Beta 值，主要流程包含：

* 使用 `yfinance` 抓取個股歷史價格
* 抓取台灣加權指數 `^TWII` 歷史價格
* 合併個股與市場指數資料
* 計算日報酬率
* 使用共變異數法估算 Beta
* 使用線性回歸輔助檢查 Beta 結果

Beta 值可作為後續 CAPM 要求報酬率估算的參數。

---

### 4. `個股股利與成長率分析.ipynb`

此 Notebook 用於多檔股票的股利成長率與估值篩選，主要流程包含：

* 設定目標股票清單
* 抓取各股票歷史股利資料
* 計算過去股利 CAGR
* 使用 CAPM 估算要求報酬率
* 使用 DDM 估算當期與未來內在價值
* 根據價值成長幅度篩選符合條件的股票

此工具適合用於建立簡化版的股利成長型股票篩選流程。

---

## Methodology

本專案使用的核心財務模型包括：

### CAPM

用於估算個股要求報酬率：

```text
Required Return = Risk-free Rate + Beta × (Market Return - Risk-free Rate)
```

### Dividend Discount Model, DDM

用於根據股利與成長率估算股票內在價值：

```text
Intrinsic Value = D1 / (r - g)
```

其中：

* `D1`：下一期預期股利
* `r`：要求報酬率
* `g`：股利成長率

### Discounted Cash Flow, DCF

用於根據未來現金流與終值估算每股價值：

```text
Firm / Equity Value = Present Value of Future Cash Flows + Present Value of Terminal Value
```

---

## Data Source

本專案主要透過 `yfinance` 抓取 Yahoo Finance 上的市場資料，包括：

* 台股個股歷史價格
* 台灣加權指數資料
* 個股股利資料

由於資料來源可能受到 Yahoo Finance 更新、缺漏或代碼格式影響，實際使用前應再次確認資料完整性。

---

## Requirements

建議使用 Python 3.9 以上版本。

主要套件包含：

```text
yfinance
pandas
numpy
matplotlib
scipy
openpyxl
jupyter
```

可使用以下指令安裝：

```bash
pip install yfinance pandas numpy matplotlib scipy openpyxl jupyter
```

---

## How to Run

可以使用 Jupyter Notebook 或 Google Colab 開啟各 Notebook。

若在本機執行：

```bash
jupyter notebook
```

或：

```bash
jupyter lab
```

接著開啟對應的 `.ipynb` 檔案即可。

---

## Notes

本專案是競賽期間快速建立的研究工具，因此部分參數仍保留在 Notebook 中手動設定，例如：

* 股票代碼
* 分析期間
* 股利資料
* 折現率
* 市場報酬率
* Beta 值
* 成長率假設

若要正式使用，建議將這些參數整理成設定檔或函數參數，以提升可重複性與可維護性。

---

## Limitations

本專案仍有以下限制：

* 模型假設較簡化，未完整納入產業景氣、財務結構與風險因子
* DDM 對成長率與折現率假設非常敏感
* Beta 估算結果會受到資料期間選擇影響
* Yahoo Finance 資料可能存在缺漏或更新延遲
* Notebook 主要作為研究輔助工具，尚未模組化為完整分析套件

---

## Future Improvements

未來可進一步改善方向包括：

* 將重複程式整理成 Python functions
* 建立統一的股票代碼與參數設定檔
* 加入更多估值模型，例如 PE、PB、EV/EBITDA 等相對估值法
* 加入財報資料自動化整理
* 加入敏感度分析與情境分析
* 建立批次化股票篩選流程
* 將 Notebook 重構為可重複執行的 Python scripts

---

## Disclaimer

This project is for educational and research purposes only.
The analysis results should not be interpreted as financial advice, investment recommendations, or trading signals.
Users should conduct their own research and risk assessment before making any investment decisions.
