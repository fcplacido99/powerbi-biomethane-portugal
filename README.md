# BioRede+ — Biomethane Potential, Cost and GHG Assessment Dashboard for Mainland Portugal

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Geospatial Analytics](https://img.shields.io/badge/Geospatial-Analytics-0F766E)
![Techno--economic Assessment](https://img.shields.io/badge/Techno--economic-Assessment-1D4ED8)
![GHG Accounting](https://img.shields.io/badge/GHG-Accounting-14532D)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

**BioRede+** is a Power BI portfolio project that assesses **biomethane production potential, economic performance and greenhouse gas (GHG) impacts** at the municipal level across **278 municipalities in mainland Portugal**.

The dashboard combines spatial analytics, scenario-based techno-economic assessment and GHG accounting to support evidence-based reasoning about where biomethane projects may be most promising.

---

## Project highlights

- **Geographic scope:** 278 municipalities in mainland Portugal
- **Timeframes:** 2024 and 2015–2024 average
- **Analytical dimensions:**
  - Biomethane production potential
  - Normalised cost (€/Nm³), biorefinery implementation cost, LCOE and abatement cost
  - GHG emissions, carbon intensity and net emission impact
- **Scenario controls:** technology practice, CHP configuration, time period and municipality selection
- **Decision logic:** municipal implementation feasibility is assessed through the relationship between **LCOE** and the **reference gas price**

---

## Dashboard structure

| Page | Purpose |
|---|---|
| **Menu** | Project entry point and navigation |
| **Biomethane Production Potential** | Municipal maps, top-ranked municipalities, feedstock composition and regional treemap |
| **Cost** | Cost maps, cost-efficient municipalities, biorefinery scale, LCOE and abatement cost |
| **GHG Emissions** | Net emissions maps, largest savings, component-level emissions waterfall and scenario comparison KPIs |
| **Info** | Methodological summary and analytical assumptions |

---

## Key findings

A few dashboard-level findings illustrate the analytical value of the tool:

- The **technical biomethane production potential** reaches approximately **280,017 kNm³ in 2024**, with a municipal average of about **1,007 kNm³**.
- **Bovine residues** and **corn residues** are the dominant production sources in the 2024 technical-potential view, accounting together for roughly **66%** of production.
- Under the **CHP + Best Practice** configuration shown in the GHG dashboard, the 2024 national result reaches approximately **−323.49 kt CO₂-eq/yr** net emission impact, compared with a positive baseline under **Standard Practice + No CHP**.
- Cost performance is strongly driven by capital intensity: **CAPEX accounts for roughly three-quarters of total cost** in the selected cost views.
- Feasibility is not uniform across the territory; the dashboard frames municipal project feasibility through the condition **LCOE < reference gas price**.

A fuller interpretation is available in [`docs/insights_summary.md`](docs/insights_summary.md).

---

## Repository structure

```text
powerbi-biomethane-portugal/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── dashboard/
│   ├── biomethane_dashboard.pbix          
│   └── biomethane_dashboard.pbip/         
│
├── images/
│   ├── menu.png             
│   ├── page_1_biomethane_potential_2024.png   
│   ├── page_2_biomethane_potential_10yr_avg_filtered.png                   
│   ├── page_3_cost_analysis_2024.png    
│   ├── page_4_cost_analysis_10yr_avg_filtered.png         
│   ├── page_5_ghg_emissions_2024.png    
│   ├── page_6_ghg_emissions_10yr_avg_filtered.png        
│
├── data/
│   ├── sample_data.xlsx
│   └── data_dictionary.md
│
├── docs/
│   ├── project_overview.md
│   ├── methodology.md
│   ├── measures_documentation.md
│   └── insights_summary.md
│
└── dax/
    └── key_measures.md
```

---

## Data note

The public file [`data/sample_data.csv`](data/sample_data.csv) is a **simplified illustrative dataset** with **fictitious/example values**. It combines representative fields from the dashboard's production-potential, economic and GHG views so the repository can explain the analytical structure without publishing the full model inputs.

See [`data/data_dictionary.md`](data/data_dictionary.md) for field definitions.

---

## Methodological framing

BioRede+ distinguishes between:

1. **Theoretical potential** — the maximum biomethane that could be generated from available feedstocks under ideal conversion conditions.
2. **Technical potential** — the achievable potential after accounting for recovery rates, realistic process performance and plant configuration.
3. **Implementation potential** — deployment relevance once logistical, infrastructural and economic constraints are considered; this is reflected mainly through the cost and feasibility views rather than being the headline of the potential page.

The GHG assessment follows a **cradle-to-grid** framing, while the economic assessment considers **CAPEX, OPEX, grid injection and biomethane transport**.

More detail is available in [`docs/methodology.md`](docs/methodology.md).

---

## DAX and model logic

The repository documents the Power BI logic behind:

- Municipality-sensitive averages and comparisons
- Single-selection versus multi-selection KPI behaviour
- Cost and LCOE measures
- Baseline comparison logic for carbon intensity and net GHG impact
- Best Practice versus Standard Practice abatement-cost KPIs

See:

- [`docs/measures_documentation.md`](docs/measures_documentation.md)
- [`dax/key_measures.md`](dax/key_measures.md)

---

## How to use the dashboard

1. Download the Power BI file from `dashboard/biomethane_dashboard.pbix`.
2. Open it in **Power BI Desktop**.
3. Use the left navigation panel to move between **Potential**, **Cost**, **GHG Emissions** and **Info** pages.
4. Use the top slicers to choose:
   - Time period: **2024** or **10-year average**
   - Municipality selection
   - Technology practice and CHP configuration
   - Absolute or area-normalised views where available
5. Interpret KPIs together with maps and ranking charts to compare municipalities and scenarios.

---

## PBIX and PBIP

- **PBIX** is the standard single-file Power BI report format and is the easiest file for most users to download and open.
- **PBIP** is the Power BI Project format. It stores report/model definitions in a folder-based, text-friendly structure that is much better suited to Git version control and code review.

For a public portfolio repository, the recommended approach is:

- publish the **`.pbix`** for easy access;
- optionally add a **`.pbip`** version if you save the report as a Power BI Project and want the repository to be more version-control-friendly.

---

## License

This repository is released under the **MIT License**. See [`LICENSE`](LICENSE).

---

## Author

**Francisco Plácido**  
Data Analyst & Data Engineer
