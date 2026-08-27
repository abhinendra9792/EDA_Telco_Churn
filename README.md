# Telco Customer Churn — Exploratory Data Analysis

![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=flat-square&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-2.1.3-013243?style=flat-square&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.2.3-150458?style=flat-square&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat-square&logo=plotly&logoColor=white)

> Which customer attributes are most strongly associated with churn in a telecom subscriber base?

An exploratory analysis of 7,043 telecom customers, examining how contract type, tenure, and billing relate to customer attrition — and where the data stops supporting conclusions.

---

## The Headline Finding

Churn rate by contract length:

| Contract | Churn Rate | Customers |
|---|---|---|
| Month-to-month | **42.7%** | 3,875 |
| One year | **11.3%** | 1,473 |
| Two year | **2.8%** | 1,695 |

Month-to-month customers churn at roughly **15×** the rate of two-year customers. Overall churn sits at 26.5%.

---

## What the Data Shows

**Churn is an early-lifetime event.** Median tenure is 10 months for churners against 38 for retained customers.

**Churners pay more but contribute less.** Mean monthly charge of 74.44 versus 61.27 — they leave before their spending compounds.

**Monthly charges are bimodal, not normal.** A spike of ~1,389 customers near 18–25 (phone-only subscribers) and a broad concentration across 70–110. The mean of 64.76 falls in the sparse gap between them and describes no typical customer.

**Tenure and contract type are distinct signals.** At equal tenure, month-to-month customers still churn more — the two variables aren't restating each other.

---

## A Note on Causation

Contract length is strongly associated with retention. It has **not** been shown to cause it.

Two readings fit the same numbers equally well: a long contract may restrain a customer from leaving, or customers who already intended to stay may be the ones who choose long contracts. This dataset is a single snapshot with no record of *when* contracts were chosen relative to churn, so it cannot distinguish between them.

Every finding here is an association observed at one point in time.

---

## The Bug Worth Mentioning

`df.isnull().sum()` reported zero missing values. The dataset looked clean.

`TotalCharges` was stored as **text**, with 11 blank entries — every one belonging to a customer with `tenure = 0`, who had not yet been billed. Blanks were filled with 0 rather than dropped, since a customer billed for zero months has genuinely accumulated zero charges.

The failure mode was the interesting part: plotting a text column doesn't raise an error. Matplotlib rendered 7,043 string values as category labels and produced a chart that looked broken rather than one that stopped. This is the argument for EDA in one example — a standard null check passed while the column was unusable.

---

## Repository Contents
The notebook runs top to bottom without manually created intermediate state.

---

## Techniques Covered

**NumPy** — array creation (`array`, `zeros`, `ones`, `arange`, `linspace`), properties (`shape`, `ndim`, `dtype`, `size`, `itemsize`), 1D/2D/3D indexing and slicing, `reshape`/`flatten`/`ravel`/`transpose`, vectorization, broadcasting, aggregation, axis-based summaries, Boolean and fancy indexing, seeded random generation.

**Analysis** — data-type classification, quality auditing, distribution analysis, categorical comparison, multivariate visualisation.

All random operations use a fixed seed, so reported figures reproduce exactly on any machine.

---

## Dataset

[Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) — 7,043 rows, 21 columns. Customer IDs are anonymous codes; no personally identifiable information is present.

---

## Limitations

- Single snapshot, no history — causal direction is unrecoverable
- Imbalanced classes (26.5% / 73.5%) — absolute counts favour the larger group
- No complaint records, outage data, or competitor pricing
- Tenure capped at 72 months, truncating long-term behaviour

---

## Running It

Open in [Google Colab](https://colab.research.google.com/), upload the CSV, and run all cells. Requires `numpy`, `pandas`, `matplotlib`, `seaborn`, `plotly` — all pre-installed in Colab.

---

**Course:** CSB314 — Exploratory Data Analysis · Minor Project 01
