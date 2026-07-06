# Appendix B - Wastewater Network Expansion Optimisation in the Larnaka District, Cyprus

This repository contains the computational material developed for the MSc thesis **"Wastewater Network Expansion Optimisation in the Larnaka District, Cyprus"**.

The thesis develops a spatial graph-based planning approach to compare wastewater network expansion scenarios for the northern part of the Larnaka District, Cyprus. The model supports strategic wastewater infrastructure planning under cost, coverage, existing-infrastructure, and pumping-feasibility constraints.

The workflow is intended for planning-level scenario comparison, not for construction-ready engineering design. It does not determine final pipe diameters, invert levels, pump capacities, pressure-main dimensions, wet-well dimensions, or treatment-plant design. Instead, it provides a transparent computational framework to explore alternative wastewater network layouts and their implications.

## Repository Contents

The repository contains four main code files and four corresponding HTML exports.

The four main code files are:

- `Cyprus_NonBudgetedNetwork`
- `Cyprus_BudgetedNetwork`
- `Cyprus_CorrectedNetwork`
- `Cyprus_PunpingStations`

The four corresponding HTML exports are:

- `Cyprus_NonBudgetedNetwork.html`
- `Cyprus_BudgetedNetwork.html`
- `Cyprus_CorrectedNetwork.html`
- `Cyprus_PunpingStations.html`

These HTML files are exported versions of the corresponding code files. They are included to make the computational workflow readable and inspectable directly from the browser, without requiring the notebooks or scripts to be executed.

The combined `Network_Maps` file is not included in this repository because the generated visualisation files were too large to upload.

## Important Note on Running the Code

The code in this repository is not directly runnable from start to finish using only the files currently included.

The full workflow depends on several auxiliary datasets and intermediate files that are not publicly redistributed. These include stakeholder-provided wastewater infrastructure data from the Local District Government Organisation of Larnaka, such as existing sewer conduit geometries and existing pumping-station locations. Some manually processed GIS files and corrected intermediate layers used during the thesis workflow are also not included.

These files were either provided specifically for the thesis case study or produced through manual processing during the modelling workflow. They may be subject to data-sharing restrictions and are therefore not included in this public repository.

For this reason, the repository should be interpreted primarily as documentation of the computational methodology and implementation logic. The included HTML exports allow the code structure, modelling steps, and implementation logic to be inspected even where the full input-data chain cannot be publicly reproduced.

## Code and HTML Files

### `Cyprus_NonBudgetedNetwork`

The `Cyprus_NonBudgetedNetwork` file implements the non-budgeted full-coverage reference scenarios.

This part of the workflow estimates the infrastructure scale required to connect all modelled urban wastewater demand terminals to the proposed northern wastewater treatment endpoint, referred to as WWTP2, without imposing the available budget constraint.

The implemented components include:

- preparation of the non-budgeted workflow;
- definition of the WWTP2 root node;
- construction of the sewer-to-road helper network;
- generation of the Rooted Dijkstra reference scenario;
- generation of the Prim--Steiner reference scenario;
- estimation of new-pipe length and pipe-only cost;
- generation of scenario outputs for the non-budgeted networks.

The corresponding HTML export is:

- `Cyprus_NonBudgetedNetwork.html`

This HTML file allows the non-budgeted workflow to be inspected without opening or running the original code file.

### `Cyprus_BudgetedNetwork`

The `Cyprus_BudgetedNetwork` file implements the budget-constrained wastewater network expansion scenarios.

This part of the workflow applies a maximum admissible new-pipe length derived from the available sewer-network budget. Instead of connecting all demand immediately, the code explores how different planning priorities affect coverage, cost, and spatial distribution under a fixed investment constraint.

The implemented budgeted heuristics include:

- Shared-trunk expansion;
- Urban-priority expansion;
- Municipality-targets expansion.

The purpose of this part of the workflow is to compare alternative budget-constrained strategies: one that maximises shared-corridor efficiency, one that prioritises dense urban clusters, and one that improves municipal balance across the northern service area.

The corresponding HTML export is:

- `Cyprus_BudgetedNetwork.html`

This HTML file allows the budgeted scenario-generation workflow to be inspected without running the original code file.

### `Cyprus_CorrectedNetwork`

The `Cyprus_CorrectedNetwork` file implements the correction and brownfield reconciliation stage.

After the non-budgeted and budgeted networks are generated, the model must interpret how the proposed northern system, WWTP2, relates to the existing southern wastewater system, WWTP1. This file supports that step by correcting spatial inconsistencies and refining the assignment of existing conduits between the two systems.

The implemented components include:

- correction of generated network outputs;
- reconciliation with existing sewer conduits;
- WWTP1/WWTP2 allocation;
- correction of spatial inconsistencies;
- removal or adjustment of unrealistic isolated fragments;
- preparation of corrected final networks for pumping-feasibility screening.

This step should be interpreted as a strategic brownfield allocation. It is not a hydraulically verified reassignment of real wastewater flows.

The corresponding HTML export is:

- `Cyprus_CorrectedNetwork.html`

This HTML file allows the correction and reconciliation workflow to be inspected without running the original code file.

### `Cyprus_PunpingStations`

The `Cyprus_PunpingStations` file implements the pumping-feasibility screening.

This part of the workflow screens the generated and corrected network scenarios using terrain information and planning-level hydraulic assumptions. The goal is to identify locations where gravity conveyance may become unrealistic and where pumping stations may be required.

The implemented components include:

- loading of corrected network scenarios;
- terrain-based gravity-cover screening;
- excavation-depth evaluation;
- identification of mandatory and optional pumping-station candidates;
- comparison with existing pumping-station locations;
- pumping-station count per scenario;
- pumping CAPEX estimation;
- generation of pumping-related scenario outputs.

The pumping analysis is a feasibility screening only. It does not size pumps, pressure mains, wet wells, or detailed hydraulic profiles.

The corresponding HTML export is:

- `Cyprus_PunpingStations.html`

This HTML file allows the pumping-feasibility screening workflow to be inspected without running the original code file.

## Main Dependencies

The workflow was developed in Python and relies on geospatial and network-analysis libraries such as:

- GeoPandas;
- Shapely;
- NetworkX;
- OSMnx;
- Rasterio;
- Pandas;
- NumPy;
- Folium;
- Matplotlib.

Additional packages may be required depending on the local environment and the specific version of the code.
