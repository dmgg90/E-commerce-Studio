# 🛒 E-Commerce & Supply Chain Analysis

A structured multi-notebook data analysis project built on a global e-commerce dataset, covering financial performance, customer behaviour, and inventory management. Each notebook is self-contained and exports clean DataFrames for Power BI visualisation.

---

## 📁 Repository Structure

```
ecommerce-analysis/
│
├── 01_sales_report/
│   └── sales_report.ipynb         ← Revenue, burn rate, cash flow, brand performance
│
├── 02_marketing_analysis/
│   └── marketing_analysis.ipynb   ← RFM, customer segments, CAC, LTV, ideal customer
│
├── 03_inventory_analysis/
│   └── inventory_analysis.ipynb   ← Stock vs sales, turnover, overstock, stockout risk
│
└── README.md
```

---

## 📓 Notebooks

### 1 · Sales Report
Financial performance analysis of the e-commerce operation.

**Covers:** Monthly & yearly revenue trends · Gross and net burn rate · Monthly cash flow · MoM and YoY growth · Brand revenue and profitability · Top 3 brands by revenue share

**Key queries:** CTEs, LAG window functions, date aggregation with `strftime`, multi-table joins filtered on completed transactions.

---

### 2 · Marketing Analysis
Customer behaviour and acquisition efficiency.

**Covers:** RFM scoring (Recency, Frequency, Monetary) · Customer segmentation · Premium customer identification · Customer Acquisition Cost (CAC) · Lifetime Value (LTV) · LTV:CAC ratio · Repeat purchase rate · Ideal customer profile

---

### 3 · Inventory & Stock Analysis
Stock health and supply chain efficiency.

**Covers:** Stock vs units sold by product and brand · Overstock identification · Stockout risk flagging · Inventory turnover rate · Days of Inventory Outstanding (DIO) · Sell-through rate · Dead stock valuation

---

## 🛠️ Stack

| Tool | Role |
|---|---|
| `kagglehub` | Dataset download |
| `pandas` | Data manipulation |
| `SQLite` | Structured querying and storage |
| `seaborn` / `matplotlib` | Visualisation |
| `Power BI` | Dashboard layer |

---

## 📊 Dataset

**[Global E-Commerce and Supply Chain Database](https://www.kaggle.com/datasets/parsakh/global-e-commerce-and-supply-chain-database)** — Kaggle

Tables used: `transactions`, `products`

---

## 🚀 How to Run

1. Clone the repository
2. Install dependencies: `pip install kagglehub pandas matplotlib seaborn scikit-learn`
3. Run notebooks in order: `01` → `02` → `03`
4. Each notebook downloads the dataset automatically via `kagglehub` — no manual file setup required
```
