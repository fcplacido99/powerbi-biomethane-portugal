# Project Overview

## 1. Project purpose

**BioRede+** is a Power BI portfolio project designed to assess the municipal geography of biomethane deployment in mainland Portugal.  
It brings together three complementary analytical perspectives:

1. **Resource availability and production potential**
2. **Economic performance and project feasibility**
3. **Climate mitigation performance**

The dashboard is intended as a decision-support interface for comparing municipalities, scenarios and technology configurations in a clear and policy-relevant way.

---

## 2. Analytical scope

| Dimension | Scope |
|---|---|
| Geography | 278 municipalities in mainland Portugal |
| Time periods | 2024 and 2015–2024 average |
| Production analysis | Theoretical and technical biomethane potential |
| Economic analysis | Normalised cost, biorefinery scale, LCOE, reference gas price and abatement cost |
| GHG analysis | Carbon intensity, net emissions impact and component-level emissions breakdown |
| Scenarios | Standard Practice vs Best Practice; CHP vs No CHP |

---

## 3. Dashboard pages

### Landing page
The opening page frames the project and provides navigational entry points for the three analytical modules:
- Biomethane production potential
- Cost
- GHG emissions
- Info

### Biomethane Production Potential
This section focuses on spatial distribution and biomass-source composition. It includes:
- Municipality-level maps
- Top 10 ranking of municipalities by biomethane production potential
- Feedstock-source donut chart
- Regional/municipal treemap
- KPI card comparing the selected geography with the municipal average

### Cost
The cost section translates production opportunities into implementation-oriented signals. It includes:
- Municipality-level cost mapping
- Ranking of the most cost-efficient municipalities
- Cost breakdown by CAPEX, OPEX, grid injection and transport
- Biorefinery scale card with input/output metrics
- LCOE and abatement-cost KPI blocks
- Feasibility logic based on `LCOE < reference gas price`

### GHG Emissions
The GHG section presents scenario-sensitive climate outcomes. It includes:
- Net-emissions maps
- Top 10 largest net GHG emission savings
- Waterfall chart showing positive and avoided emission components
- Carbon intensity KPI with comparison to the baseline scenario
- Net emission impact KPI with comparison to the baseline scenario

### Info
The information page summarises the methodological framework that underpins the dashboard and clarifies the meanings of the analytical outputs.

---

## 4. Interaction design

The dashboard is built around coordinated slicers and scenario buttons. Users can:

- switch between **2024** and the **10-year average** view;
- filter municipalities, including multi-selection;
- compare technology practices and plant configurations;
- move between absolute and area-normalised indicators where relevant;
- interpret national and municipal performance through dynamically updating KPI cards.

The DAX layer is designed to adapt text, aggregation logic and benchmark comparisons to the selection state.

---

## 5. Feasibility framing

The cost module links the techno-economic assessment to a simple and transparent project-feasibility condition:

```text
A municipal biorefinery project is treated as economically feasible when:
LCOE < Reference Gas Price
```

This criterion supports a screening-level view of implementation potential. It is intended for territorial prioritisation, not as a substitute for full site-specific project development.

---

## 6. Repository publication choices

This repository is structured to work well as a **portfolio project**:

- the **PBIX** file provides a readily downloadable Power BI report;
- the optional **PBIP** structure can support Git-friendly version control;
- public **sample data** are illustrative rather than raw production data;
- methodology and DAX files make the analytical reasoning auditable;
- an insights summary highlights the most decision-relevant outputs.
