# 🛒 Retail Orders — End-to-End Data Analysis Project

> A full-cycle EDA and feature engineering project built on a real retail orders dataset, covering business analysis, advanced Pandas, time-series trends, and SQL-ready data export.

---

## 📌 Project Overview

This project performs a comprehensive analysis of a retail orders dataset (~10,000 orders) spanning 2 years across 4 regions, 3 categories, and 17 sub-categories. The goal was to extract actionable business insights while simultaneously sharpening core data analysis skills in **Pandas, NumPy, and Matplotlib**.

The final output is a clean, enriched CSV loaded into SQL for further querying.

---

## 📂 Dataset

| Property | Detail |
|---|---|
| Total Orders | 9,994 |
| Time Period | January 2022 – December 2023 |
| Regions | Central, East, South, West |
| Categories | Furniture, Office Supplies, Technology |
| Sub-Categories | 17 |
| Key Columns | Order Id, Order Date, Ship Mode, Segment, Category, Sub Category, List Price, Cost Price, Quantity, Discount Percent |

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue) ![Pandas](https://img.shields.io/badge/Pandas-EDA-green) ![NumPy](https://img.shields.io/badge/NumPy-Feature%20Engineering-orange) ![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-red)

---

## 🔑 Engineered Features

| Column | Description |
|---|---|
| `selling_price` | List Price after discount applied |
| `revenue` | selling_price × quantity |
| `cost` | cost_price × quantity |
| `profit` | revenue − cost |
| `profit_margin` | (profit / revenue) × 100 |
| `discount_bucket` | Discount ranges using `pd.cut()` |
| `profit_label` | High / Medium / Low Profit / Loss using `np.select()` |
| `high_discount_loss_flag` | Boolean — high discount AND negative profit |
| `shipping_priority` | Urgent / Standard / Low Priority from Ship Mode |
| `business_score` | Composite 0–6 score from margin + quantity + discount |
| `order_segment` | Premium vs Regular using selling price + margin thresholds |
| `revenue_rank` | Rank of revenue within each Category using `.rank()` |
| `cumulative_revenue` | Running revenue total per Region using `.cumsum()` |
| `regional_avg_revenue` | Regional average per row using `.transform()` |
| `regional_vs_avg_revenue` | How each order compares to its regional average |

---

## 📊 Analysis Sections

### 1. 📋 Descriptive & Business Overview
- Total revenue: **$11.08M** | Total profit: **$1.04M**
- Consumer segment dominates with **52% of orders**
- Technology leads revenue ($3.93M), but Furniture is close behind ($3.72M)

### 2. 🗺️ Geographic & Regional Performance
- **West** is the most profitable region ($305K), **South** lags at $202K (~33% gap)
- Only 5 cities show negative profit — all with negligible losses
- All regions operate within a tight margin band of **5.0%–5.4%**

### 3. 💸 Discount & Pricing Impact Analysis
- Higher discounts → slightly higher revenue but **significantly lower margins**
- Margin drops from **7.0% → 3.7%** as discount increases from 1–2% to 4–5%
- **Fasteners** incur losses in **17 out of 24 months** under aggressive discounting
- Discounting is associated with losses — but does not necessarily cause them

### 4. 📦 Product-Level Performance
- **Chairs** and **Phones** are the top two most profitable sub-categories
- **Copiers** have the highest avg margin (8.8%) despite only 68 orders
- No sub-category operates at a net loss overall — healthy product portfolio

### 5. ⚙️ Advanced Feature Engineering
- **81% of individual orders** are either Loss or Low Profit — profitability is driven by a small number of high-value orders
- Only **8.2% of orders qualify as Premium** (high price + high margin)
- Premium orders generate **~5x more revenue per order** than Regular orders
- Business score distribution is bell-shaped, peaking at score 2

### 6. 🪟 Window & Analytical Operations
- Revenue is heavily concentrated in **top 1–2 sub-categories per category**
- All regions show consistent cumulative growth over 2 years
- Central region revenue is highly skewed — mean inflated by a few large orders

### 7. 🔄 Pivoting & Reshaping
- West leads in Furniture & Office Supplies; East leads in Technology
- All categories have nearly identical avg discount rates (~3.49%) — discounting is applied uniformly

### 8. 📈 Time-Series Analysis
- Monthly revenue is volatile — swings from **-46% to +68% MoM**
- No strong linear growth trend; **Q4 months tend to be stronger** (retail seasonality)
- Discount rates remain constant across months — ruling out discounting as a cause of revenue dips
- Revenue dips appear to be demand-driven, not discount-driven

### 9. 🧹 Data Quality & Optimisation
- Zero negative revenue orders — clean dataset
- 507 null profit margins fixed (caused by zero-revenue / cancelled orders)
- Memory optimised from **9.1 MB → 4.2 MB (54% reduction)** via categorical dtype conversion

---

## 💡 Key Business Insights

1. **Discounting is eroding margins** — the 4–5% discount tier yields nearly half the margin of the 1–2% tier
2. **Fasteners and Labels need a discount cap** — they repeatedly lose money under aggressive discounting
3. **South region is consistently underperforming** — worth investigating pricing or cost structure
4. **Premium orders (8.2%) are disproportionately valuable** — a focus on high-price, high-margin products could significantly improve profitability
5. **Most orders contribute little** — 81% are Loss or Low Profit; a few large orders drive overall results

---

## 🧠 Concepts Practised

| Concept | Applied In |
|---|---|
| Granularity awareness | Throughout |
| Weighted vs simple average | Profit margin calculations |
| "Consistently" = time dimension | Q3.3 — discount loss analysis |
| Wide vs Long format | Pivot & Melt |
| Threshold setting from percentiles | Business score, Premium segmentation |
| Skewness awareness | Regional revenue analysis |
| Correlation ≠ Causation | Discount & loss interpretation |

---

## 📤 Output

A clean, enriched CSV with all engineered features exported for SQL loading, validated for:
- ✅ No negative revenue
- ✅ No invalid profit margins
- ✅ Null values resolved
- ✅ Memory optimised with categorical dtypes

---

## 🚀 How to Run

```bash
# Clone the repository
git clone <your-repo-url>

# Install dependencies
pip install pandas numpy matplotlib

# Open the notebook
jupyter notebook retail_orders.ipynb
```

---

## 👤 Author

Built as a portfolio project to develop end-to-end data analysis skills across EDA, feature engineering, time-series analysis, and SQL-ready data preparation.

---

*"Data is only as valuable as the questions you ask of it."*
