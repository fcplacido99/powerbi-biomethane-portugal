# Key DAX Measures

This file preserves the main DAX measure definitions supplied for the BioRede+ dashboard and groups them by analytical module.

For a prose explanation of the measure logic, see [`../docs/measures_documentation.md`](../docs/measures_documentation.md).

## Biomethane pages

```DAX
Avg_Bio_methane_kNm3 = 
CALCULATE(
    AVERAGEX(
        VALUES('Municipality'[Municipality]),
        CALCULATE( SUM('Biomethane_potential'[Total Biomethane Production (kNm³)]) )
    ),
    REMOVEFILTERS('Municipality')
)


Avg_Bio_methane_kNm3_SelectedMun = 
VAR _oneMun = HASONEVALUE('Municipality'[Municipality])
RETURN
IF(
    _oneMun,
    -- single municipality: just its value
    SUM('Biomethane_potential'[Total Biomethane Production (kNm³)]),
    -- multiple (or none): average across the municipalities currently selected
    AVERAGEX(
        VALUES('Municipality'[Municipality]),
        CALCULATE( SUM('Biomethane_potential'[Total Biomethane Production (kNm³)]) )
    )
)


vs media = 
VAR _munFiltered = ISFILTERED('Municipality'[Municipality]) || ISFILTERED('Municipality'[Municipality_lower]) || ISFILTERED('Municipality'[Nuts2]) || ISFILTERED('Municipality'[Nuts3])
VAR _avgAll = [Avg_Bio_methane_kNm3]
VAR _avgSel = [Avg_Bio_methane_kNm3_SelectedMun]
VAR _var = _avgSel - _avgAll
VAR _pct = DIVIDE(_var, _avgAll) * 100
VAR _sign = IF(_var > 0, "+", "")
VAR _isTotal = [Area_selected] = "Total"

RETURN
IF(
    _isTotal,
    IF(
        NOT _munFiltered,
        SWITCH(
            TRUE(),
            ABS(_avgAll) > 100,
                "Municipal average: " & FORMAT(_avgAll, "#,##0") & " kNm³",
            ABS(_avgAll) > 1 && ABS(_avgAll) <= 100,
                "Municipal average: " & FORMAT(_avgAll, "#,##0.0") & " kNm³",
            ABS(_avgAll) <= 1,
                "Municipal average: " & FORMAT(_avgAll, "#,##0.00") & " kNm³"
        ),
        SWITCH(
            TRUE(),
            ABS(_var) > 100,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0") & " kNm³",
            ABS(_var) > 1 && ABS(_var) <= 100,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0.0") & " kNm³",
            ABS(_var) <= 1,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0.00") & " kNm³"
        )
    ),
    IF(
        NOT _munFiltered,
        SWITCH(
            TRUE(),
            ABS(_avgAll) > 100,
                "Municipal average: " & FORMAT(_avgAll, "#,##0") & " kNm³/km²",
            ABS(_avgAll) > 1 && ABS(_avgAll) <= 100,
                "Municipal average: " & FORMAT(_avgAll, "#,##0.0") & " kNm³/km²",
            ABS(_avgAll) <= 1,
                "Municipal average: " & FORMAT(_avgAll, "#,##0.00") & " kNm³/km²"
        ),
        SWITCH(
            TRUE(),
            ABS(_var) > 100,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0") & " kNm³/km²",
            ABS(_var) > 1 && ABS(_var) <= 100,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0.0") & " kNm³/km²",
            ABS(_var) <= 1,
                " " & _sign & FORMAT(_pct, "0.00") & "% | " & _sign & FORMAT(_var, "#,##0.00") & " kNm³/km²"
        )
    )
)
```

## Cost pages

```DAX
Input_sum = IF (
    ISFILTERED('Cost'[Municipality]),
    SUM('Cost'[BioReferiny Scale Input (tonnes)])/1000,
    SUM('Cost'[BioReferiny Scale Input (tonnes)])/1000
)


KPI_input_kt = 
SWITCH(
    TRUE(),
    [Input_sum] > 10,
        FORMAT([Input_sum], "#,##0") & " kt",
    [Input_sum] > 1 && [Input_sum] <= 10,
        FORMAT([Input_sum], "#,##0.0") & " kt",
    [Input_sum] <= 1, 
        FORMAT([Input_sum], "#,##0.00") & " kt"
)


Output_sum = IF (
    ISFILTERED('Cost'[Municipality]),
    SUM('Cost'[BioRefinery Scale Output Nm⁻³ ])/1000,
    SUM('Cost'[BioRefinery Scale Output Nm⁻³ ])/1000
)


KPI_output_kt = 
SWITCH(
    TRUE(),
    [Output_sum] > 10,
        FORMAT([Output_sum], "#,##0") & " kNm³",
    [Output_sum] > 1 && [Output_sum] <= 10,
        FORMAT([Output_sum], "#,##0.0") & " kNm³",
    [Output_sum] <= 1, 
        FORMAT([Output_sum], "#,##0.00") & " kNm³"
)


Cost_€_per_Nm3_per_muni = 
CALCULATE(
    MAX('Cost'[TOTAL €/Nm-3]),
    TREATAS(VALUES('Supply'[Supply]), 'Cost'[Supply]),
    TREATAS(VALUES('CHP'[CHP_or_not]), 'Cost'[CHP_or_not]),
    TREATAS(VALUES('Practice'[Practice]), 'Cost'[Practice])
)


Cost_total_or_median = 
VAR muniSel = VALUES('Municipality'[Municipality])
VAR nMuni   = COUNTROWS(muniSel)

VAR cost_single =
    CALCULATE(
        SUM('Cost'[TOTAL €/Nm-3]),
        TREATAS(VALUES('Supply'[Supply]), 'Cost'[Supply]),
        TREATAS(VALUES('CHP'[CHP_or_not]), 'Cost'[CHP_or_not]),
        TREATAS(VALUES('Practice'[Practice]), 'Cost'[Practice])
    )
    *
    CALCULATE(
        SUM('Cost'[BioRefinery Scale Output Nm⁻³ ]),
        TREATAS(VALUES('Supply'[Supply]), 'Cost'[Supply]),
        TREATAS(VALUES('CHP'[CHP_or_not]), 'Cost'[CHP_or_not]),
        TREATAS(VALUES('Practice'[Practice]), 'Cost'[Practice])
    )

VAR muniWithData =
    FILTER(
        muniSel,
        NOT ISBLANK( CALCULATE([Cost_€_per_Nm3_per_muni]) )
    )

VAR median_cost =
    AVERAGEX(
        muniWithData,
        CALCULATE([Cost_€_per_Nm3_per_muni])
    )

RETURN
SWITCH(
    TRUE(),
    nMuni = 1, cost_single,
    -- 0 or 2+ municipalities: median €/Nm³ of the municipalities currently in context
    median_cost
)



sentence_kpi_input_outout = 
VAR nMuni = COUNTROWS(VALUES('Municipality'[Municipality]))
VAR v = [Cost_total_or_median]
RETURN
IF(
    nMuni = 1,
    "Total cost: " & FORMAT(v/1e6, "#,##0.00") & " M€",
    "Average cost: " & FORMAT(v, "#,##0.00") & " €/Nm³"
)


Cost_€_per_MWh_per_muni = 
CALCULATE(
    MAX('Cost'[LCOE municipality (€/MWh)]),
    TREATAS(VALUES('Supply'[Supply]), 'Cost'[Supply]),
    TREATAS(VALUES('CHP'[CHP_or_not]), 'Cost'[CHP_or_not]),
    TREATAS(VALUES('Practice'[Practice]), 'Cost'[Practice])
)


Avg_cost_€_per_MWh_adaptive = 
VAR muniSel = VALUES('Municipality'[Municipality])
VAR nMuni   = COUNTROWS(muniSel)
VAR muniWithData =
    FILTER(
        muniSel,
        NOT ISBLANK( CALCULATE([Cost_€_per_MWh_per_muni]) )
    )
RETURN
SWITCH(
    TRUE(),
    nMuni = 0,
        AVERAGEX(muniWithData, CALCULATE([Cost_€_per_MWh_per_muni])),
    nMuni = 1,
        CALCULATE([Cost_€_per_MWh_per_muni]),
    AVERAGEX(muniWithData, CALCULATE([Cost_€_per_MWh_per_muni]))
)


LCOE_Avg_cost_€_per_MWh_adaptive = 
VAR _pci_GJ_per_NM3  = 0.03797
VAR _pci_MWh_per_NM3 = _pci_GJ_per_NM3 / 3.6
VAR v = [Avg_cost_€_per_MWh_adaptive]
RETURN
v


sentence_lcoe = 

VAR v = [LCOE_Avg_cost_€_per_MWh_adaptive]
RETURN
IF(
    ISBLANK(v),
    "n/a €/MWh",
    "Average LCOE: " & FORMAT(v, "#,##0") & " €/MWh"
)


sentence_baseline_ng_price = 
IF (
    ISFILTERED('Municipality'[Municipality]),
    "Reference gas price: " & FORMAT(AVERAGE('Cost'[Municipality threshold (€/MWh)]), "#,##0.00") & " €/MWh",
    "Reference gas price: 93 €/MWh"
)


AbatementCost_Best_Practice = 

VAR isMainland = [Municipio_selecionado] = "Mainland Portugal"

RETURN
CALCULATE(
    IF(
        isMainland,
        AVERAGE('GHG'[Abatement Cost €/ t CO₂-eq yr⁻¹])/1000,
        AVERAGE('GHG'[Abatement Cost €/ t CO₂-eq yr⁻¹])/1000
    ),
    REMOVEFILTERS('Practice'[Practice]),
    'Practice'[Practice] = "Best Practice"
)


KPI_AC_Best_practice = "Best practice: " & FORMAT([AbatementCost_Best_Practice], "#,##0.00") & " €/tCO₂e"


AbatementCost_Standard = 

VAR isMainland = [Municipio_selecionado] = "Mainland Portugal"

RETURN
CALCULATE(
    IF(
        isMainland,
        AVERAGE('GHG'[Abatement Cost €/ t CO₂-eq yr⁻¹])/1000,
        AVERAGE('GHG'[Abatement Cost €/ t CO₂-eq yr⁻¹])/1000
    ),
    REMOVEFILTERS('Practice'[Practice]),
    'Practice'[Practice] = "Standard"
)


KPI_AC_Standard = "Standard practice: " & FORMAT([AbatementCost_Standard], "#,##0.00") & " €/tCO₂e"
```

## GHG pages

```DAX
Avg_carbon_intensity = 
MEDIAN('GHG'[g CO₂-eq / MJ])

Avg_STANDARD_NO_CHP = 
MEDIAN('GHG'[STANDARD_NO_CHP])

sentence1_CI = 
VAR _media = [Avg_STANDARD_NO_CHP]
RETURN
    "vs Baseline (Standard Practice, No CHP): " & FORMAT(_media, "#,0.00") & " g CO₂-eq / MJ" 

sentence2_CI = 
VAR _ci   = [Avg_carbon_intensity]
VAR _base = [Avg_STANDARD_NO_CHP]
VAR _d    = _ci - _base
VAR _d_percentagem = _d/_base * (100)
VAR _sign = IF(_d > 0, "+", "")
RETURN
"Δ = " & _sign & FORMAT(_d, "0.00") & " g CO₂-eq / MJ"// & " (" & _sign & FORMAT(_d_percentagem, "0.00") & "%)"


SUM_net_em_impact = 
SUM('GHG'[Net CO2eq yr-1])


SUM_NET_STANDARD_NO_CHP = 
SUM('GHG'[Net_STANDARD_NO_CHP])


sentence1_NEI = 
VAR _media = [SUM_NET_STANDARD_NO_CHP]
RETURN
    "vs Baseline (Standard Practice, No CHP): " & FORMAT(_media, "#,0.00") & " kt CO₂-eq / yr"


sentence2_NEI = 
VAR _ci   = [SUM_net_em_impact]
VAR _base = [SUM_NET_STANDARD_NO_CHP]
VAR _d    = _ci - _base
VAR _d_percentagem = _d/_base * (100)
VAR _sign = IF(_d > 0, "+", "")
RETURN
"Δ = " & _sign & FORMAT(_d, "0.00") & " kt CO₂-eq / yr"// & " (" & _sign & FORMAT(_d_percentagem, "0.00") & "%)
```
