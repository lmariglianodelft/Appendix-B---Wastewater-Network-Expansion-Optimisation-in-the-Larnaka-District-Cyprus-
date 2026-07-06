# Appendix-B---Wastewater-Network-Expansion-Optimisation-in-the-Larnaka-District-Cyprus-

This repository contains the computational workflow developed for the MSc thesis **"Wastewater Network Expansion Optimisation in the Larnaka District, Cyprus"**. The code supports a spatial graph-based planning approach for comparing wastewater network expansion scenarios under cost, coverage, existing-infrastructure, and pumping-feasibility constraints.

The workflow is designed for strategic planning rather than construction-ready engineering design. It represents wastewater demand, road-based construction corridors, existing sewer conduits, pumping stations, terrain data, and treatment endpoints within a graph-based framework. The resulting model is used to generate and compare alternative sewer network expansion scenarios for the northern municipalities of the Larnaka District.

## Repository Contents

The repository includes four main Jupyter notebooks:

### `Cyprus_NonBudgetedNetwork.ipynb`

This notebook generates the non-budgeted full-coverage reference scenarios. These scenarios estimate the pipe length and cost required to connect all modelled urban demand terminals to the proposed northern wastewater treatment endpoint, referred to as WWTP2.

Implemented scenarios include:

- Rooted Dijkstra baseline
- Prim--Steiner routing heuristic
- WWTP2 site selection
- Sewer-to-road helper network construction
- Cross-scenario comparison outputs

### `Cyprus_BudgetedNetwork.ipynb`

This notebook generates the budget-constrained network expansion scenarios. These scenarios apply a maximum admissible pipe-length constraint derived from the available sewer-network budget and explore different planning priorities for partial expansion.

Implemented heuristics include:

- Shared-trunk expansion
- Urban benefit-cost prioritisation
- Municipality target-progression
- Budgeted heuristic comparison
- Downstream processing for each generated scenario

### `Cyprus_CorrectedNetwork.ipynb`

This notebook performs post-processing and manual correction of the generated network outputs. It supports the final brownfield reconciliation step by refining the assignment of existing conduits and demand areas between the existing southern treatment system, WWTP1, and the proposed northern treatment endpoint, WWTP2.

The purpose of this notebook is to improve spatial consistency after automatic allocation and avoid unrealistic isolated fragments in the final network interpretation.

### `Cyprus_PunpingStations.ipynb`

This notebook performs the pumping-station feasibility screening for the generated WWTP2 network scenarios. It uses terrain information and planning-level hydraulic assumptions to identify locations where gravity conveyance may become unrealistic and where pumping stations may be required.

The workflow includes:

- Hydraulic design assumptions
- Existing pumping-station classification
- Gravity-cover and excavation-depth screening
- Scenario-level pumping-station candidate detection
- Summary outputs for cost and feasibility comparison

> Note: the filename preserves the original working name used during development. In a cleaned repository version, it is recommended to rename this file to `Cyprus_PumpingStations.ipynb`.

## Methodological Scope

The code implements a planning-level modelling workflow. It does not produce final pipe diameters, invert levels, pump capacities, pressure-main designs, or construction-ready sewer alignments. Instead, it supports early-stage comparison of alternative wastewater network configurations.

The workflow can be used to assess:

- new-pipe length;
- pipe-only construction cost;
- population coverage;
- municipal coverage distribution;
- WWTP1/WWTP2 brownfield allocation;
- likely pumping-station requirements;
- total cost including pumping-station CAPEX;
- trade-offs between full coverage, budget feasibility, and municipal balance.

## Data Requirements

The workflow uses a combination of public and stakeholder-provided datasets. Public datasets include OpenStreetMap road data, building footprints, municipal population data, and terrain elevation data. Stakeholder-provided datasets include existing sewer conduits and existing pumping-station locations.

Because some wastewater infrastructure data were provided by local stakeholders, these restricted input files are not necessarily redistributed in this repository. Full numerical reproduction of the thesis results therefore requires access to the same local infrastructure datasets used in the original case study.

## Main Dependencies

The notebooks rely on Python geospatial and network-analysis libraries, including:

- GeoPandas
- Shapely
- NetworkX
- OSMnx
- Rasterio
- Pandas
- NumPy
- Folium
- Matplotlib
