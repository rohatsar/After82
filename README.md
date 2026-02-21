AFTER82 – Data Processing & Modeling Framework

This repository documents the analytical workflow developed for the AFTER82 Curiosity Cup project.

The project focuses on modeling cascading impacts in urban transport networks using open datasets, while ensuring structured abstraction in public reporting.

The repository emphasizes reproducibility, transparency, and responsible data handling.
Only aggregated, publication-safe outputs are included.

Repository Scope

This repository contains:

-Description of open data sources and derived datasets

-Data processing steps (cleaning, filtering, enrichment, aggregation)

-High-level SAS® Viya (CAS) workflow notes

-Aggregated outputs used for figures and tables in the competition paper

It serves as documentation of the modeling framework rather than a deployable system.

Data Handling Approach

The following elements are intentionally excluded from this repository:

-Personal data

-Node-level infrastructure identifiers

-Point-level geographic coordinates in exported datasets

-Per-node predictive outputs

All publicly shared outputs are aggregated at zone level.

Analytical Pipeline Overview

1. Data Ingestion

-OpenStreetMap transport network extracts

-District boundary data

-GEM Global Active Faults dataset

-Optional USGS event summaries

2. Graph Construction

-Directed, distance-weighted transport graph

3. Pilot Subset Filtering

-Six-district subset for controlled experimentation

4. Hazard Context Enrichment

-Aggregated fault exposure metrics

-District-level risk indicators

-Geotechnical proxy variables

5. Scenario Label Generation

-Diffusion-style cascade simulation

-Binary cascade outcome variable

6. Predictive Modeling

-Gradient Boosting

-Random Forest

-Evaluation via ROC AUC and related performance metrics

7. Structured Reporting Layer

-Percentile-based zone abstraction (LOW / MEDIUM / HIGH)

-Inter-zone connectivity summaries

-Aggregated topology indicators

Reproducibility

Detailed workflow documentation is provided in:
docs/DATA_PROCESSING.md

Users must independently obtain the referenced open datasets to replicate the modeling pipeline.

Intended Use

This repository supports academic transparency and competition review.
It is not designed for operational infrastructure assessment.
