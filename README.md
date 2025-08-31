# Data Engineering End-to-End
# Dataset → Star Schema → Data Marts → Visualizations (End‑to‑End in One Notebook)

An end‑to‑end **data engineering + analytics** walkthrough that takes a public dataset from **raw → cleaned → star schema (fact + dims) → data quality checks → business marts → charts** using a single Jupyter notebook.

- **Tech**: Python, DuckDB (SQL), Pandas, Matplotlib
- **Architecture**: Medallion pattern (**Bronze → Silver → Gold → QA → Marts**)
- **Outcome**: Reusable template to model any tabular dataset into a star schema and publish BI‑ready marts.

> ⚠️ Note: This repo uses a public dataset; you can swap it for any CSV/Parquet or API source. No company‑specific context required.

---

## 📁 Repository Structure

```
.
├── data_engineering.ipynb      # End‑to‑end notebook
└── README.md                   # You are here
```


---

## 🧪 What the Notebook Does

1. **Ingestion (Bronze)**  
   - Loads a public dataset (via `datasets` library) into a DataFrame.
   - Registers it in **DuckDB** to enable fast SQL over in‑memory tables.

2. **Transformation (Silver)**  
   - Cleans & standardizes columns, normalizes repeated structures.

3. **Dimensional Modeling (Gold)**  
   - Builds a **star schema**: one **fact** table + multiple **dimension** tables.  
   - Enforces surrogate keys and referential integrity.

4. **Data Quality (QA)**  
   - Row counts, null checks, FK integrity checks, and valid domain constraints.
   - Notes on how this maps to **dbt tests** in production.

5. **Business Marts (Analytics Layer)**  
   - Derives curated aggregates/views for BI, APIs, or AI features.

6. **Visualizations**  
   - Produces charts from marts to tell the final story.

---

## ▶️ How to Run with Another Dataset

- Replace the ingestion cell with your source (CSV/Parquet/API). Example:
```python
import pandas as pd
df = pd.read_csv("your_data.csv")
# register to DuckDB
import duckdb as ddb
con = ddb.connect()
con.register("bronze_source", df)
```
- Update the **Silver** cleaning and **Gold** SQL to reflect your columns.
- Rerun QA + marts + charts — everything else stays the same.

---

## 🧱 Key Design Choices

- **DuckDB** for local SQL + analytics performance (fast, no server).
- **Medallion pattern** to mirror modern lakehouse practices.
- **Single‑notebook flow** to keep things reproducible and beginner‑friendly.
- **Clear separation** between modeling layers (Bronze/Silver/Gold/QA/Marts).

---

## 📊 Example Questions You Can Answer
- Trend of top categories over time
- Entity‑level leaderboards and distributions
- Time‑to‑X stats with percentiles
- Quality gates: are we missing keys? duplicated dimensions?

---

## 🔄 Reproducibility Notes
- Randomness is avoided; all steps are deterministic.
- Charts are generated from marts to ensure parity with BI tools.

---

## 🔐 Attribution & Ethics
- The included dataset reference is **public/open**.  
- Remove/replace any proper nouns if you plan to present this as a generic case study.
- Do **not** include any confidential or interview‑specific context.

---

## 🧭 Roadmap / Nice‑to‑Haves (anyone interested to contribute?)
- [ ] dbt tests parity (schema + data tests)
- [ ] Export marts to Parquet/CSV for BI
- [ ] ER diagram auto‑generation via `erdantic` or `sqlmesh`
- [ ] Optional Streamlit dashboard fed by marts


