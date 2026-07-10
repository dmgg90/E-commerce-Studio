# E-commerce-Studio
# Global E-Commerce & Supply Chain Analysis (SQL)

End-to-end SQL analysis of a multi-table e-commerce dataset, using Python/pandas for ingestion and SQLite/SQL for all analytical querying. Built to demonstrate direct SQL competency (joins, CTEs, window functions) beyond what a single-table pandas EDA can show.

## Dataset

[Global E-Commerce and Supply Chain Database](https://www.kaggle.com/datasets/parsakh/global-e-commerce-and-supply-chain-database) (Kaggle), five related tables:

| Table | Rows | Description |
|---|---|---|
| `customers` | 8,000 | Demographics, registration date, premium status |
| `products` | 500 | Product name, category, brand |
| `suppliers` | 998 | Supplier cost data |
| `transactions` | 100,000 | Order-level revenue, cost, profit, shipping cost, channel, status |
| `inventory` | 500 | Stock levels by product |

## Tech Stack

- **Python / pandas** — CSV ingestion and cleaning
- **SQLite** — relational storage
- **SQL** — all analytical querying (joins, CTEs, window functions)
- **Seaborn / Matplotlib** — visualization
- **Kaggle API (`kagglehub`)** — reproducible data download

## Methodology

1. Download the dataset via the Kaggle API (`kagglehub`)
2. Load each CSV into a local SQLite database (`ecommerce_supply_chain.db`)
3. Run all analysis as SQL queries against the database, returning results as pandas DataFrames
4. Visualize key results with Seaborn/Matplotlib

## Key Insights

- **Customer value is concentrated in a small, high-frequency group.** The top customer by purchase frequency has 1,671 completed transactions and $762K in lifetime revenue — over 1.5x the next-highest customer. Only 1 of the top 10 most frequent buyers is flagged `is_premium`, suggesting the existing premium flag under-captures true high-value customers.
- **Revenue is highly seasonal**, peaking in December at roughly 2.5x the February low, consistent with holiday-driven demand.
- **Revenue is geographically concentrated**, led by the USA, roughly double the next-largest market (UK).
- **BoldEdge is the leading brand overall**, broken down further by country and by customer age profile to check whether that lead is broad-based or concentrated.
- **Stockout risk identified via sell-through ratio.** An initial stock-vs-sales query was corrected after producing implausible results (grouping by raw stock level mixed unrelated products that happened to share a stock count). The corrected version computes units sold ÷ current stock per individual product, surfacing a defensible restocking priority list for BoldEdge's top SKUs.

## Known Limitations & Next Steps

- **Supplier cost data (`suppliers` table) not yet analyzed.** The natural next step is joining supplier cost to product margin — is BoldEdge's popularity also profitable, or is it high-volume but thin-margin? This is the one part of the "supply chain" half of this dataset not yet covered.
- **No explicit primary/foreign keys enforced in the schema** — tables were loaded via `pandas.to_sql()`, which infers types but doesn't enforce relational constraints.
- **Data loading uses `if_exists="append"`** — re-running the ingestion cell against an existing database file will duplicate rows. Delete `ecommerce_supply_chain.db` before re-running, or switch to `if_exists="replace"`. **Verify row counts before trusting any totals** (`SELECT COUNT(*) FROM transactions` should return exactly 100,000).
- **Two chart cells previously had no output** (never executed) — confirm these have been run before publishing.

## How to Run

```bash
pip install kagglehub pandas seaborn matplotlib
```

```python
import kagglehub
path = kagglehub.dataset_download("parsakh/global-e-commerce-and-supply-chain-database")
```

Then run `Analysis.ipynb` top to bottom. The notebook builds `ecommerce_supply_chain.db` from the downloaded CSVs and runs all analysis against it.

## Repo Structure

```
├── Analysis.ipynb              # Main analysis notebook
├── ecommerce_supply_chain.db   # Generated SQLite database (not committed — build locally)
└── README.md
```