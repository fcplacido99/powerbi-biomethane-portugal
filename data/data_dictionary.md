# Data Dictionary — `sample_data.xlsx`

## Purpose of the sample workbook

`sample_data.xlsx` is a **multi-sheet illustrative workbook** prepared for the public GitHub repository.  
It mirrors the worksheet structure and column names of the source analytical workbook used by BioRede+, while replacing the original values with **arbitrary example data**.

The sample file:

- preserves the **same worksheet names** as the uploaded analytical workbook;
- preserves the **same column names** in each worksheet;
- uses **fictitious municipalities and arbitrary numerical values**;
- avoids accented letters in the generated text values;
- is intended for **repository documentation and schema illustration only**.

It should **not** be used to reproduce the dashboard outputs, validate the research results, or draw conclusions about real Portuguese municipalities.

---

## Workbook structure

| Worksheet | Purpose | Sample rows excluding header |
|---|---|---:|
| `Biomethane_potential` | Biomethane potential structure for the 2024-style view | 48 |
| `Biomethane_potential_avg` | Biomethane potential structure for the 2015-2024 average-style view | 48 |
| `Cost` | Cost and implementation-related structure for the 2024-style view | 48 |
| `Cost_avg` | Cost and implementation-related structure for the 2015-2024 average-style view | 48 |
| `GHG` | GHG, carbon intensity and net impact structure for the 2024-style view | 48 |
| `GHG_avg` | GHG, carbon intensity and net impact structure for the 2015-2024 average-style view | 48 |
| `Municipality` | Municipality dimension table used for territorial slicing | 12 |
| `Nuts2` | NUTS2 lookup table | 7 |
| `Nuts3` | NUTS3 lookup table | 24 |

---

## 1. `Biomethane_potential`

The `Biomethane_potential` and `Biomethane_potential_avg` sheets share the same structure.

| Column | Type | Unit | Description |
|---|---|---|---|
| `Municipality` | Text | — | Fictitious municipality name used in the sample workbook. |
| `Biomethane_potential` | Text | — | Potential level represented by the row: `Theoretical` or `Technical`. |
| `Total_per_area` | Text | — | Display mode represented by the row: `Total` or `Per area`. |
| `Wine Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit, depending on row mode | Illustrative biomethane contribution associated with wine residues. |
| `Olive OIl Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with olive oil residues. |
| `Bovine  Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with bovine residues. |
| `Swine Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with swine residues. |
| `Olive Prunings  Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with olive pruning residues. |
| `Vine  Prunings  Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with vine pruning residues. |
| `Wheat Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with wheat residues. |
| `Corn Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with corn residues. |
| `Rice  Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with rice residues. |
| `Other Cerealst Residue Biomethane Production (Nm³)` | Numeric | Nm³ or Nm³ per area unit | Illustrative biomethane contribution associated with other cereal residues. |
| `Biomethane Potential Nm³/ m²` | Numeric | Dataset-defined potential metric | Illustrative aggregate biomethane potential field preserved with the original workbook column name. |
| `Municipality Area` | Numeric | Area unit used by the source model | Illustrative municipality area used to support total/per-area representations. |
| `Municipality_lower` | Text | — | Lowercase municipality label used for matching and joins. |
| `Nuts2` | Text | — | NUTS2 territorial grouping. |
| `Nuts3` | Text | — | NUTS3 territorial grouping. |

---

## 2. `Cost`

The `Cost` and `Cost_avg` sheets share the same structure.

| Column | Type | Unit | Description |
|---|---|---|---|
| `Municipality` | Text | — | Fictitious municipality name used in the sample workbook. |
| `CHP_or_not` | Text | — | Plant-energy configuration: `CHP` or `NO CHP`. |
| `Practice` | Text | — | Operational scenario: `Standard` or `Best Practice`. |
| `BioReferiny Scale Input (tonnes)` | Numeric | tonnes | Illustrative amount of bioresource input processed by the biorefinery. |
| `BioRefinery Scale Output Nm⁻³ ` | Numeric | Nm³ | Illustrative biomethane output associated with the biorefinery scale. |
| `CAPEX €/Nm⁻³ ` | Numeric | €/Nm³ | Illustrative capital expenditure contribution to normalised cost. |
| `OPEX €/Nm⁻³ ` | Numeric | €/Nm³ | Illustrative operational expenditure contribution to normalised cost. |
| `GRID INJECTION €/Nm⁻³ ` | Numeric | €/Nm³ | Illustrative cost contribution associated with injection into the gas grid. |
| `TRANSPORT €/Nm⁻³ ` | Numeric | €/Nm³ | Illustrative transport cost contribution. |
| `Municipality_lower` | Text | — | Lowercase municipality label used for matching and joins. |
| `Nuts2` | Text | — | NUTS2 territorial grouping. |
| `Nuts3` | Text | — | NUTS3 territorial grouping. |
| `Municipality threshold (€/MWh)` | Numeric | €/MWh | Illustrative municipality-level comparison threshold for the gas-price feasibility screen. |
| `LCOE municipality (€/MWh)` | Numeric | €/MWh | Illustrative levelised cost of biomethane energy. |

---

## 3. `GHG`

The `GHG` and `GHG_avg` sheets share the same structure, except for the original source workbook wording of the grid injection emissions column.

| Column | Type | Unit | Description |
|---|---|---|---|
| `Municipality` | Text | — | Fictitious municipality name used in the sample workbook. |
| `CHP_or_not` | Text | — | Plant-energy configuration: `CHP` or `NO CHP`. |
| `Practice` | Text | — | Operational scenario: `Standard` or `Best Practice`. |
| `BioRefinery Emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Illustrative direct and process emissions associated with the biorefinery. |
| `Feedstock Transport Emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Illustrative emissions associated with feedstock transport. |
| `Grid injection transport emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Grid injection transport-related emissions field used in the `GHG` sheet. |
| `Grid injection emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Grid injection emissions field used in the `GHG_avg` sheet. |
| `Fertilizer Avoided Emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Illustrative avoided emissions from synthetic fertiliser substitution. |
| `Waste Management Avoided Emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Illustrative avoided emissions from improved residue or manure management. |
| `NG Avoided Emissions kt CO₂-eq yr⁻¹` | Numeric | kt CO₂-eq/yr | Illustrative avoided emissions from fossil natural gas substitution. |
| `Net Emissions kt` | Numeric | kt CO₂-eq/yr | Illustrative net emissions result after combining positive and avoided components. |
| `Abatement Cost €/ t CO₂-eq yr⁻¹` | Numeric | €/t CO₂-eq | Illustrative marginal abatement cost field. |
| `g CO₂-eq / MJ` | Numeric | g CO₂-eq/MJ | Illustrative carbon intensity of biomethane under the row scenario. |
| `kg CO₂-eq / m3` | Numeric | kg CO₂-eq/m³ | Illustrative volumetric carbon-intensity metric. |
| `Municipality_lower` | Text | — | Lowercase municipality label used for matching and joins. |
| `Nuts2` | Text | — | NUTS2 territorial grouping. |
| `Nuts3` | Text | — | NUTS3 territorial grouping. |
| `STANDARD_NO_CHP` | Numeric | g CO₂-eq/MJ | Carbon-intensity benchmark for the Standard Practice and No CHP scenario. |
| `STANDARD_CHP` | Numeric | g CO₂-eq/MJ | Carbon-intensity benchmark for the Standard Practice and CHP scenario. |
| `BP_NO_CHP` | Numeric | g CO₂-eq/MJ | Carbon-intensity benchmark for the Best Practice and No CHP scenario. |
| `BP_CHP` | Numeric | g CO₂-eq/MJ | Carbon-intensity benchmark for the Best Practice and CHP scenario. |
| `Difference Potential` | Numeric | g CO₂-eq/MJ | Illustrative difference between the Standard/No CHP benchmark and the current row scenario. |
| `Net_STANDARD_NO_CHP` | Numeric | kt CO₂-eq/yr | Illustrative net emissions benchmark for the Standard Practice and No CHP baseline. |

**Note on the grid injection column:**  
The source workbook uses `Grid injection transport emissions kt CO₂-eq yr⁻¹` in `GHG`, and `Grid injection emissions kt CO₂-eq yr⁻¹` in `GHG_avg`. The sample workbook preserves this distinction exactly.

---

## 4. `Municipality`

| Column | Type | Unit | Description |
|---|---|---|---|
| `Municipality` | Text | — | Fictitious municipality name. |
| `Nuts2` | Text | — | NUTS2 territorial grouping associated with the municipality. |
| `Nuts3` | Text | — | NUTS3 territorial grouping associated with the municipality. |
| `Municipality_lower` | Text | — | Lowercase municipality label used for matching and joins. |

---

## 5. `Nuts2`

| Column | Type | Unit | Description |
|---|---|---|---|
| `Nuts2` | Text | — | NUTS2 lookup value used for territorial filtering. |

---

## 6. `Nuts3`

| Column | Type | Unit | Description |
|---|---|---|---|
| `Nuts2` | Text | — | Parent NUTS2 territorial grouping. |
| `Nuts3` | Text | — | NUTS3 lookup value used for territorial filtering. |

---

## Relationship to the full Power BI model

The sample workbook is designed to **communicate the public data structure** behind the dashboard without publishing the real analytical inputs or outputs.

It mirrors the major table families used by the Power BI report:

- biomethane potential tables;
- economic and implementation-oriented tables;
- GHG assessment tables;
- territorial lookup tables.

The workbook values are intentionally fabricated and should be treated as **schema examples**, not as research findings.
