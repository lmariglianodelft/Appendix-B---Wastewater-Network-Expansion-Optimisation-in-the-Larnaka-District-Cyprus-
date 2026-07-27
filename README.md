# Appendix B - Wastewater Network Expansion Optimisation in the Larnaka District, Cyprus

This repository contains the computational material developed for the MSc thesis **"Wastewater Network Expansion Optimisation in the Larnaka District, Cyprus"**.

The thesis develops a spatial graph-based planning approach to compare wastewater network expansion configurations for the northern part of the Larnaka District, Cyprus. The model supports strategic wastewater infrastructure planning under cost, coverage, existing-infrastructure, and pumping-feasibility constraints.

The workflow is intended for planning-level configuration comparison, not for construction-ready engineering design. It does not determine final pipe diameters, invert levels, pump capacities, pressure-main dimensions, wet-well dimensions, or treatment-plant design. Instead, it provides a transparent computational framework to explore alternative wastewater network layouts and their implications.

## Repository Contents

The repository contains five main Jupyter notebooks, five corresponding HTML exports, and one compressed folder containing the final network maps used to document the spatial outputs of the analysis.

The five main notebooks are:

- `Cyprus_NonBudgetedNetwork.ipynb`
- `Cyprus_BudgetedNetwork.ipynb`
- `Cyprus_CorrectedNetwork.ipynb`
- `Cyprus_PumpingStations.ipynb`
- `Cyprus_ExtraGraphics.ipynb`

The five corresponding HTML exports are:

- `Cyprus_NonBudgetedNetwork.html`
- `Cyprus_BudgetedNetwork.html`
- `Cyprus_CorrectedNetwork.html`
- `Cyprus_PumpingStations.html`
- `Cyprus_ExtraGraphics.html`

The HTML files are exported versions of the corresponding Jupyter notebooks. They are included to make the computational workflow, code structure, intermediate outputs, and generated figures directly readable from a browser without requiring the notebooks to be opened or executed.

The repository also contains:

- `Cyprus_NetworkMaps.zip`

This compressed folder contains the final spatial network maps generated for the thesis. Its contents are organised into three groups:

1. a combined map showing all final network configurations together;
2. a folder containing one complete final-network map for each configuration;
3. a folder containing one map for each configuration showing only the newly generated network expansion.

The map archive is included to allow the final spatial outputs to be inspected without rerunning the full GIS and network-generation workflow.

## Important Note on Running the Code

The code in this repository is not directly runnable from start to finish using only the files currently included.

The full workflow depends on several auxiliary datasets and intermediate files that are not publicly redistributed. These include stakeholder-provided wastewater infrastructure data from the Local District Government Organisation of Larnaka, such as existing sewer conduit geometries and existing pumping-station locations. Some manually processed GIS files and corrected intermediate layers used during the thesis workflow are also not included.

These files were either provided specifically for the thesis case study or produced through manual processing during the modelling workflow. They may be subject to data-sharing restrictions and are therefore not included in this public repository.

For this reason, the repository should be interpreted primarily as documentation of the computational methodology and implementation logic. The included HTML exports allow the code structure, modelling steps, generated outputs, and implementation logic to be inspected even where the full input-data chain cannot be publicly reproduced.

The notebooks also contain local file paths associated with the original thesis working directory. These paths would need to be adapted before attempting to run the code in another environment.

## Code and HTML Files

### `Cyprus_NonBudgetedNetwork`

The `Cyprus_NonBudgetedNetwork` notebook implements the non-budgeted full-coverage reference configurations.

This part of the workflow estimates the infrastructure scale required to connect all modelled urban wastewater demand terminals to the proposed northern wastewater treatment endpoint, referred to as WWTP2, without imposing the available budget constraint.

The implemented components include:

- preparation of the non-budgeted workflow;
- definition of the WWTP2 root node;
- construction of the sewer-to-road helper network;
- generation of the Rooted Dijkstra reference configuration;
- generation of the Prim--Steiner reference configuration;
- verification that the generated layouts are acyclic rooted trees;
- estimation of new-pipe length and pipe-only cost;
- generation of configuration outputs for the non-budgeted networks.

The corresponding HTML export is:

- `Cyprus_NonBudgetedNetwork.html`

This HTML file allows the non-budgeted workflow to be inspected without opening or running the original notebook.

### `Cyprus_BudgetedNetwork`

The `Cyprus_BudgetedNetwork` notebook implements the budget-constrained wastewater network expansion configurations.

This part of the workflow applies a maximum admissible new-pipe length derived from the available sewer-network budget. Instead of connecting all demand immediately, the code explores how different planning priorities affect coverage, cost, and spatial distribution under a fixed investment constraint.

The implemented budgeted heuristics include:

- Shared-trunk expansion;
- Urban-priority expansion;
- Municipality-targets expansion;
- verification that the generated layouts are acyclic rooted trees.

The purpose of this part of the workflow is to compare alternative budget-constrained strategies: one that maximises shared-corridor efficiency, one that prioritises dense urban clusters, and one that improves municipal balance across the northern service area.

The corresponding HTML export is:

- `Cyprus_BudgetedNetwork.html`

This HTML file allows the workflow for generating the budgeted configurations to be inspected without running the original notebook.

### `Cyprus_CorrectedNetwork`

The `Cyprus_CorrectedNetwork` notebook implements the correction and brownfield reconciliation stage.

After the non-budgeted and budgeted networks are generated, the model must interpret how the proposed northern system, WWTP2, relates to the existing southern wastewater system, WWTP1. This notebook supports that step by correcting spatial inconsistencies and refining the assignment of existing conduits between the two systems.

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

This HTML file allows the correction and reconciliation workflow to be inspected without running the original notebook.

### `Cyprus_PumpingStations`

The `Cyprus_PumpingStations` notebook implements the pumping-feasibility screening.

This part of the workflow screens the generated and corrected network configurations using terrain information and planning-level hydraulic assumptions. The goal is to identify locations where gravity conveyance may become unrealistic and where pumping stations may be required.

The implemented components include:

- loading of corrected network configurations;
- terrain-based gravity-cover screening;
- excavation-depth evaluation;
- identification of mandatory and optional pumping-station candidates;
- comparison with existing pumping-station locations;
- pumping-station count per configuration;
- pumping CAPEX estimation;
- generation of pumping-related configuration outputs.

The pumping analysis is a feasibility screening only. It does not size pumps, pressure mains, wet wells, or detailed hydraulic profiles.

The corresponding HTML export is:

- `Cyprus_PumpingStations.html`

This HTML file allows the pumping-feasibility screening workflow to be inspected without running the original notebook.

### `Cyprus_ExtraGraphics`

The `Cyprus_ExtraGraphics` notebook generates the additional figures used in the thesis that are not directly produced within the four principal modelling notebooks.

These figures were created to support the explanation of the case study, input data, methodology, initial demand conditions, scenario comparison, and final infrastructure allocation.

The generated material includes, among others:

- the Larnaka study-area map;
- the road-network and building-footprint input map;
- the initial demand-node coverage map;
- methodology diagrams for the Rooted Dijkstra and Prim--Steiner approaches;
- methodology diagrams for the Shared-trunk, Urban-priority, and Municipality-targets heuristics;
- final allocation of existing pumping stations between WWTP1 and WWTP2;
- additional comparative graphics used in the thesis.

The notebook does not implement an additional optimisation stage. Its purpose is to reproduce the supplementary visual material used to explain and document the modelling workflow and results.

The corresponding HTML export is:

- `Cyprus_ExtraGraphics.html`

This HTML file allows all supplementary plotting code and generated graphics to be inspected without opening or running the notebook.

## Network Map Archive

### `Cyprus_NetworkMaps.zip`

The `Cyprus_NetworkMaps.zip` archive contains the final interactive or static spatial representations of the generated wastewater-network configurations.

The archive includes:

- one combined map containing all final network configurations;
- one folder containing a separate complete final-network map for each configuration;
- one folder containing a separate map for each configuration showing only the newly generated expansion network.

The complete final-network maps may include the reconciled existing infrastructure, the proposed expansion network, treatment-plant allocation, existing pumping stations, and newly identified pumping-station candidates, depending on the map layer configuration.

The expansion-only maps isolate the new network generated by each optimisation approach. They are included to facilitate direct comparison of the spatial form and extent of the proposed expansions without the visual complexity of the existing infrastructure.

The archive is provided as a compressed folder because the complete set of visualisation files is more conveniently distributed and downloaded together.

## Main Dependencies

The workflow was developed in Python and relies on geospatial, raster-processing, visualisation, and network-analysis libraries such as:

- GeoPandas;
- Shapely;
- NetworkX;
- OSMnx;
- Rasterio;
- Pandas;
- NumPy;
- SciPy;
- Folium;
- Matplotlib;
- Contextily;
- Fiona;
- AdjustText.

Additional packages may be required depending on the local environment and the specific version of the code.
