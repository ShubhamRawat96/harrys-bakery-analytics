 Harrys Bread Market & Sales Analysis

 📌 Project Objective
Analyze Harrys (France) sales, cost structure and competitive position to produce actionable insights:
- Track monthly sales & growth
- Understand factory-level costs
- Evaluate marketing spend effectiveness
- Benchmark market share vs competitors

📂 Repo structure (what's included)
Harrys/
├── Data_Raw/ # Original CSV/Excel files (Costing, Sales, Marketing & Competition)
├── Data_Processed/ # Cleaned CSVs and KPI outputs
│ ├── Clean_File/ # Cleaned CSVs: costing_data_clean.csv, sales_data_clean.csv, marketing_data_clean.csv
│ └── KPI_File/ # KPI exports (cost_breakdown_per_factory.csv, marketing_roi.csv, etc.)
├── Visuals/ # PNG charts used in report & PPT (sales_growth.png, cost_breakdown.png, etc.)
├── scripts/ # Python scripts
│ ├── load_and_clean.py
│ ├── validation.py
│ └── generate_kpi.py
├── Notebooks/ # Jupyter / Colab notebooks (analysis.ipynb)
├── dashboard/ # Power BI (.pbix) or Excel dashboard file
├── Reports/ # Final report (PDF / DOCX)
├── temp/ # temporary files (optional)
└── README.md


🔧 Tools / Environment
- Python 3.x — Pandas, NumPy, openpyxl
- Jupyter / Google Colab — EDA and plots
- Power BI Desktop (recommended) or Excel — interactive dashboard
- Matplotlib / Seaborn — visuals
- Git + GitHub — project hosting

Install dependencies (local):
```bash
python -m pip install --upgrade pip
python -m pip install pandas numpy openpyxl matplotlib seaborn


How to reproduce (high level)

Place raw files into Data_Raw/ (exact names used in scripts: costing_data.csv, sales_data.csv, marketing_and_competition_data.csv).
Run cleaning script:
python scripts/load_and_clean.py
Output: cleaned CSVs in Data_Processed/Clean_File/.
Run validation:
python scripts/validation.py
Output: Data_Processed/validation_report.txt
Generate KPIs:
python scripts/generate_kpi.py
Output: KPI CSVs in Data_Processed/KPI_File/
Open Notebooks/analysis.ipynb (or Colab) for EDA and visuals. Saved PNGs are in Visuals/.
Open dashboard/harrys_dashboard.pbix (if present) to interactively explore.

Key deliverables

Cleaned datasets: Data_Processed/Clean_File/*
KPI outputs: Data_Processed/KPI_File/*
Visuals: Visuals/*.png
Dashboard: dashboard/harrys_dashboard.pbix
Final report: Analysis/harrys_report.pdf
Presentation: Reports/harrys_presentation.pptx

Notes & assumptions

Data in Data_Raw/ is simulated/collected for Harrys in France (Paris & South France).
Dates standardized to ISO (YYYY-MM-DD) where possible.
Currency: EUR (€).

Contact / Author

Project by: Shubham Rawat
Repo status: Final polish pending (Dashboard + PPT + GitHub push)


---

# 2) Power BI dashboard plan (recommended — build this next)

**Why Power BI**: interactive filters, slicers, publish to PowerBI.com (if needed). If you prefer Excel let me know and I’ll give Excel steps.

## Data model (import these CSVs)
- `sales_data_clean.csv` → Sales table (columns: Month, Region, Sales Channel, Product Type, Units Sold, Revenue (€))
- `costing_data_clean.csv` → Costing table (Factory ID, Month, Raw Material Cost (€), Labor Cost (€), Packaging (€), Distribution (€), Total Cost (€))
- `marketing_data_clean.csv` → Marketing table (Month, Region, Channel, Marketing Spend (€), Competitor Sales Jacquet (€), Competitor Sales La Boulangère (€))
- (Optional) Create a **Date** table (Calendar) and link `Month` fields to it.

### Relationships
- Date[Date] ←→ Sales[Month_parsed] (many-to-one)
- Date[Date] ←→ Costing[Month_parsed]
- Date[Date] ←→ Marketing[Month_parsed]
- (If you have Region/Channel keys, link as needed)

### Recommended Measures (DAX)
Create these Measures in Power BI:

```dax
Total Revenue = SUM('Sales'[Revenue (€)])

Total Cost = SUM('Costing'[Total Cost (€)])

Profit = [Total Revenue] - [Total Cost]

Profit Margin % = DIVIDE([Profit], [Total Revenue], 0) * 100

Monthly Revenue =
    CALCULATE([Total Revenue], DATESINPERIOD('Date'[Date], LASTDATE('Date'[Date]), -1, MONTH))

MoM Growth % =
VAR curr = [Total Revenue]
VAR prev = CALCULATE([Total Revenue], DATEADD('Date'[Date], -1, MONTH))
RETURN DIVIDE(curr - prev, prev, 0) * 100

Marketing Spend = SUM('Marketing'[Marketing Spend (€)])

Revenue per € Marketing =
DIVIDE([Total Revenue], [Marketing Spend], 0)

Harrys Market Size = [Total Revenue] + SUM('Marketing'[Competitor Sales Jacquet (€)]) + SUM('Marketing'[Competitor Sales La Boulangère (€)])

Harrys Market Share % = DIVIDE([Total Revenue], [Harrys Market Size], 0) * 100

Pages & visuals

Page 1 — Executive Overview

KPI cards: Total Revenue, Total Cost, Profit, Profit Margin %, Avg MoM Growth %

Line chart: Monthly revenue trend (with MoM % as tooltip)

Donut / Bar: Revenue share by Channel

Slicers: Month (range), Region, Channel

Page 2 — Costs & Factory Efficiency

Stacked bar: Cost components per Factory (Raw Material, Labor, Packaging, Distribution)

Bar: Cost per unit (if units available) or Cost per Factory (Total Cost)

Table: Factory-level KPIs (Wastage %, Cost per unit, Units produced)

Page 3 — Marketing & ROI

Bar: Marketing Spend by Channel

Line or scatter: Revenue per € Marketing by Channel

Map or region bar: Spend vs Revenue by Region

Page 4 — Competition & Market Share

Line: Harrys market share % over time

Clustered bar: Harrys vs Jacquet vs La Boulangère (per month or region)

Commentary text box: Key takeaways

Interactivity

Add slicers for Region, Channel, Product Type

Enable cross-filtering between visuals

Use bookmarks for 1-page executive view (toggle details)

Export

Export each visual as PNG (Power BI export) to Visuals/ for PPT/report.

3) PPT (what to fill & quick steps)

Use the outline we discussed before. Create slides and insert the PNGs from /Visuals/.

If you want I can auto-generate a PPT file for you and place PNGs into their slides (I can produce a .pptx content layout or give you the code snippet to create it with python-pptx). Tell me if you want me to create the PPT automatically.

4) GitHub: what to commit & .gitignore

Files to commit (recommended):

README.md

scripts/*

Data_Raw/* (small CSVs) — be mindful of sharing sensitive data

Data_Processed/Clean_File/* (clean CSVs)

Data_Processed/KPI_File/*

Notebooks/analysis.ipynb

Visuals/*

Reports/* (PDF)

dashboard/harrys_dashboard.pbix (optional — pbix can be large but ok to include)

Final checklist (what we’ll do now, step-by-step)

Save README.md (I pasted above) — ✅ you can paste into the root.

Build Power BI dashboard using the plan above — I can give DAX code and visuals step-by-step if you want.

Export PNGs from Power BI (or use existing images) and assemble PPT — I can auto-generate PPT or give you python-pptx script.

Final repo cleanup and push to GitHub.