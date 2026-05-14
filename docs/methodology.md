# Methodology

## 1. Overview

BioRede+ provides a municipal-scale spatial assessment of biomethane deployment opportunities in mainland Portugal.  
The analytical framework combines:

- **feedstock-resource estimation**;
- **technology-configuration scenarios**;
- **GHG accounting**;
- **techno-economic assessment**.

The dashboard covers a baseline year of **2024** and a **2015–2024 average** perspective.

---

## 2. Biomethane production potential

The assessment distinguishes between three levels of potential.

### 2.1 Theoretical potential

The **theoretical biomethane potential** represents the maximum amount of biomethane that could be produced from available feedstocks under ideal conversion conditions.

It is based on:
- feedstock availability and physical properties;
- feedstock composition and methane-generation characteristics.

### 2.2 Technical potential

The **technical biomethane potential** adjusts the theoretical potential to account for realistic conversion performance and operational constraints.

The calculation incorporates:
- sustainable feedstock recovery rates;
- upgrading efficiency;
- process-configuration assumptions.

### 2.3 Implementation potential

The **implementation potential** reflects the biomethane production that can realistically be deployed once logistical, infrastructural and economic constraints are considered.

The modelling framework includes:
- transport distances and logistics;
- plant scale and configuration;
- gas-grid injection pathways or trucking alternatives;
- capital and operational costs;
- GHG mitigation performance.

In the dashboard, this idea is expressed primarily through the **Cost** module and the feasibility screening condition:

```text
LCOE < Reference Gas Price
```

---

## 3. Technology configurations

Four technological dimensions are considered in the modelling framework.

### 3.1 Standard configuration

Represents conventional operational performance observed in existing anaerobic digestion systems.  
It assumes standard methane-leakage levels, conventional digestate management practices and typical upgrading performance.

### 3.2 Best Practice / BAT-style configuration

Represents an optimised plant design with:
- methane leak detection and repair programmes;
- improved digestate storage;
- reduced methane slip during upgrading;
- better energy efficiency.

The dashboard uses the scenario label **Best Practice** for this improved operational configuration.

### 3.3 CHP configuration

A share of produced biogas is combusted in a **combined heat and power (CHP)** unit to supply internal heat and electricity needs.  
This can improve operational self-sufficiency and resilience, while slightly reducing the biomethane volume available for grid injection.

### 3.4 No-CHP configuration

All produced biogas is upgraded to biomethane.  
This maximises biomethane output, but increases dependence on external electricity and heat and can affect both costs and indirect emissions.

---

## 4. GHG assessment

The GHG analysis evaluates:
1. emissions associated with biomethane production; and
2. avoided emissions resulting from system substitution effects.


### Included emission sources
- feedstock collection and handling;
- feedstock transport;
- anaerobic digestion process emissions;
- methane leakage;
- digestate management;
- biogas upgrading;
- plant operational energy use;
- transport to injection point and injection into the gas network.

### Avoided emissions
- displacement of fossil natural gas;
- improved manure and residue management;
- substitution of synthetic fertilisers through digestate use.

The dashboard expresses these effects through:
- **carbon intensity** in g CO₂-eq/MJ;
- **net emission impact** in kt CO₂-eq/yr;
- component-level waterfall charts;
- comparisons against the **Standard Practice + No CHP** baseline.

---

## 5. Economic assessment

The economic assessment evaluates:
- normalised biomethane production cost in **€/Nm³**;
- biorefinery input and output scales;
- levelised cost of energy (**LCOE**, €/MWh);
- marginal abatement cost (**€/t CO₂-eq avoided**).

The cost boundary follows a **cradle-to-grid** perspective and includes:
- capital expenditure (**CAPEX**);
- operational expenditure (**OPEX**);
- grid-injection costs;
- transport to injection points through pipeline or compressed-biomethane road transport.

The dashboard translates this cost assessment into:
- cost maps and rankings;
- cost-component breakdowns;
- municipal feasibility signals through comparison with the reference gas price.

---

