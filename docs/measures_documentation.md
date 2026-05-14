# Measures Documentation

## 1. Purpose

This document explains the main DAX measures used in the BioRede+ dashboard.  
The full measure definitions are available in [`../dax/key_measures.md`](../dax/key_measures.md).

The measures are designed around three recurring modelling needs:

1. **Selection-aware aggregation** — national view, single municipality and multi-municipality selections behave differently where appropriate.
2. **Scenario sensitivity** — practice, CHP configuration and other slicers alter both values and explanatory text.
3. **Benchmark communication** — KPI cards compare selections with national averages or baseline scenarios.

---

## 2. Biomethane Potential page

### `Avg_Bio_methane_kNm3`
Calculates the national municipal average biomethane potential by averaging municipality-level totals while removing municipality filters.

**Use in dashboard:**  
Provides the comparison benchmark for national-view KPI cards.

### `Avg_Bio_methane_kNm3_SelectedMun`
Returns:
- the selected municipality's value when exactly one municipality is selected;
- the average across currently selected municipalities when multiple municipalities or a broader regional filter is active.

**Use in dashboard:**  
Drives the selected-geography comparison against the national municipal average.

### `vs media`
Builds the dynamic comparison text shown in the KPI card.  
Its output adapts to:
- total vs per-area units;
- no municipality selection vs selected geography;
- magnitude-sensitive number formatting.

**Use in dashboard:**  
Generates explanatory KPI text such as municipal average or percentage difference versus the average.

---

## 3. Cost page

### `Input_sum` and `Output_sum`
Aggregate biorefinery scale inputs and outputs:
- biomass/residue input in **kt**;
- biomethane output in **kNm³**.

### `KPI_input_kt` and `KPI_output_kt`
Apply readable unit-aware formatting to input and output totals.

**Use in dashboard:**  
Populate the biorefinery-scale visual with compact, formatted values.

### `Cost_€_per_Nm3_per_muni`
Returns the municipality-specific normalised cost under the current scenario-filter context.

**Filter logic:**  
Uses `TREATAS` to apply slicer selections for:
- feedstock supply;
- CHP configuration;
- practice configuration.

### `Cost_total_or_median`
Implements adaptive cost KPI behaviour:
- for a single municipality, it multiplies unit cost by biomethane output to produce a total project cost;
- for grouped or national views, it returns a cross-municipality aggregated unit-cost benchmark.

**Use in dashboard:**  
Feeds the textual KPI that switches between total-cost language and normalised-cost language.

### `sentence_kpi_input_outout`
Creates the explanatory text shown below the biorefinery-scale card:
- `Total cost` for a single municipality;
- `Average cost` for aggregate views.

### `Cost_€_per_MWh_per_muni`
Returns municipality-specific LCOE under the active scenario selections.

### `Avg_cost_€_per_MWh_adaptive`
Adapts LCOE aggregation to the selection context:
- single municipality: selected LCOE;
- grouped/national view: cross-municipality aggregation.

### `sentence_lcoe`
Formats the LCOE KPI text displayed in the dashboard.

### `sentence_baseline_ng_price`
Displays the gas-price benchmark:
- a fixed national reference value in the all-country view;
- a municipality-specific threshold in filtered views.

### `AbatementCost_Best_Practice` and `AbatementCost_Standard`
Calculate scenario-specific abatement cost benchmarks for the two practice configurations.  
The KPI labels are then built by:
- `KPI_AC_Best_practice`
- `KPI_AC_Standard`

---

## 4. GHG Emissions page

### `Avg_carbon_intensity`
Returns the median carbon intensity under the current GHG scenario selection.

### `Avg_STANDARD_NO_CHP`
Returns the baseline carbon intensity associated with the **Standard Practice + No CHP** comparison state.

### `sentence1_CI`
Formats the carbon-intensity baseline explanatory line.

### `sentence2_CI`
Calculates and formats the carbon-intensity delta relative to baseline.

### `SUM_net_em_impact`
Returns total net GHG impact in kt CO₂-eq/yr under the current selection.

### `SUM_NET_STANDARD_NO_CHP`
Returns the baseline net GHG impact under **Standard Practice + No CHP**.

### `sentence1_NEI`
Formats the net-emissions baseline explanatory line.

### `sentence2_NEI`
Calculates and formats the delta in net emission impact relative to baseline.

---

## 5. Baseline-comparison logic

The GHG dashboard uses a fixed interpretive baseline:

```text
Standard Practice + No CHP
```

This baseline is held in dedicated columns and then used in KPI narratives to communicate:
- the current selected scenario;
- the baseline outcome;
- the magnitude of improvement or deterioration.

---

## 6. Selection behaviour

The dashboard distinguishes between:
- **no explicit municipality selection**;
- **single municipality selection**;
- **multiple municipalities or regional selection**.

This design allows the report to switch between:
- total project cost and average/benchmark unit cost;
- single-location performance and portfolio-style summaries;
- selected-municipality value and national municipal average.

---

## 7. Model note

Some DAX measures refer to supporting slicer/dimension tables used inside the Power BI model, such as a feedstock-supply dimension.  
These model-support tables are not represented in the public illustrative CSV file, which is intentionally simplified for repository documentation.

---

## 8. Publication note

The DAX code in this repository is documented as supplied for the current dashboard.  
Before a final public release, it is good practice to review naming consistency and remove any helper variables or conditional branches that are no longer needed.
