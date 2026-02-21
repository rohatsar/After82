Data Processing & Lineage (AFTER82)

This document provides a structured, step-by-step description of the AFTER82 data processing and modeling pipeline.

It is intended to support technical transparency and reproducibility while maintaining publication-level abstraction in publicly shared outputs.

1. Inputs (Open Datasets)
1.1 OpenStreetMap-Based Network Layers (OSM)

We started from OSM-derived extracts representing Istanbul’s transportation network and selected infrastructure-related node types.

Example files:

-istanbul_roads.csv – road segments (connectivity backbone)

-istanbul_junctions.csv – junction nodes

-istanbul_bridges.csv – bridge nodes

-istanbul_transport.csv – transport-related nodes

-istanbul_connections.csv – connectivity edges

-istanbul_districts.csv / istanbul_districts.geojson – administrative boundaries

Notes

-OSM tags may vary in completeness and consistency.

-Attributes that could expose operational detail were excluded from publication outputs.

1.2 GEM Global Active Faults

Hazard geometry was derived from:

gem_active_faults_harmonized.geojson

Derived subsets:

-faults_turkey.*

-faults_istanbul.*

-buffer-based exposure derivatives (e.g., 5 km pilot buffer)

1.3 Optional Event Context (USGS)

A small earthquake event set was used for contextual framing only.
Event-level reporting is not included in publication outputs.

1.4 Soil / Ground Proxy

Where available, coarse district-level soil proxies (z_class) were incorporated as vulnerability context indicators.

2. Processing Environment (SAS Viya CAS)

All processing and modeling were conducted in SAS® Viya for Learners using CAS (Cloud Analytic Services).

Primary caslibs:

-CASUSER – personal project workspace

-PUBLIC – avoided for project tables

CAS table management (CASUTIL) was used to:

-Load data into CASUSER

-Manage intermediate tables

-Retain final tables within controlled workspace scope

3. Graph Construction (Nodes & Edges)
3.1 Node Schema

Unified node schema:

-node_id – internal identifier

-lat, lon – used internally only

-node_type – junction / bridge / transport / etc.

-district_name – administrative association

Coordinates are not included in publication-safe exports.

3.2 Edge Schema

Edges represent connectivity:

-source_id, target_id

-weight_km – distance-based weight

-edge_type – road / connection category

3.3 Pilot Scope (Six-District Subset)

A controlled six-district pilot was implemented to ensure interpretability and reproducibility within competition constraints.

Derived tables:

-NODES_6DISTRICTS_ENRICHED_NO_PII

-EDGES_6DISTRICTS_ENRICHED_NO_PII

The pipeline remains scalable to broader geographic scope.

4. Hazard-Context Enrichment
4.1 Fault Exposure Proxy

District-level exposure metric:

-Total fault length within a 5 km buffer

Joined to nodes via district assignment:

-fault_length_5km_km

4.2 District Risk Score

A district-level risk index:

-district_risk_score

4.3 Soil Proxy

Coarse geotechnical indicator:

-z_class

5. Topology Features

Derived from the pilot graph:

-Node degree

-Degree quantiles

-Hub-share summaries

Derived tables:

-NODE_DEGREE_6D

-PAPER_ZONE_TOPOLOGY_6D_SAFE 

6. Scenario Label Generation (Cascade Simulation)

Scenario-derived labels were generated using a diffusion-style propagation rule across discrete time steps.

Outputs include:

-Time-series aggregate counts

-Binary outcome variable: affected_binary

These labels represent controlled simulation scenarios used for modeling feasibility analysis.

7. Predictive Modeling

Models trained in SAS Viya Model Studio:

-Gradient Boosting

-Random Forest

Evaluation metrics:

-ROC AUC

-KS statistic (Youden-based cutoff)

-Lift and captured response

Performance stability across train/validate/test partitions was verified.

Entity-level ranking outputs are not included in publication artifacts.

8. Structured Reporting Layer (Publication-Safe)
8.1 Zone Abstraction
   
To prevent point-level exposure, structural and hazard indicators were aggregated into three percentile-based zones:

-LOW

-MEDIUM

-HIGH

Zone mapping is derived from aggregated proxies rather than facility identity.

8.2 Zone-Level Outputs Used in Paper

-Zone summary table

-Inter-zone edge count heatmap

-Zone topology summaries (average / maximum degree, hub-share)

All shared outputs contain aggregated values only.

9. Reviewer Package (Safe Bundle)

Included:

-Zone-level summary tables

-Model performance plots

-Pipeline documentation

Excluded:

-Node-level coordinates

-Facility-level identifiers

-Targetable rankings

10. Limitations

-OSM tagging variability may affect feature completeness.

-Fault exposure is a proxy; higher-resolution geologic layers could improve precision.

-Pilot scope limits generalization; however, the workflow is designed to scale.

11. Feature Dictionary


<img width="795" height="412" alt="image" src="https://github.com/user-attachments/assets/616a3b81-126a-4036-9a01-08980eb1ff27" />

12. Modeling Design Rationale

Tree-based ensemble models (Random Forest and Gradient Boosting) were selected due to their robustness under mixed feature scales and non-linear structural relationships typical in network-derived datasets.

13. Scalability Note

The six-district pilot was intentionally scoped for transparency and controlled validation. The pipeline is structurally designed to scale to full-city or multi-city contexts without altering the abstraction framework.
