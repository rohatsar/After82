AFTER82 – Privacy-Preserving Cascade Modeling
Overview

AFTER82 is a privacy-first urban resilience modeling framework developed for the Curiosity Cup 2026 – A Global SAS® Student Competition.

The project proposes a zone-based abstraction approach for modeling cascading impacts in urban transportation networks while strictly avoiding disclosure of sensitive infrastructure details.

Using SAS® Viya, we construct an anonymized directed transport graph, simulate disruption propagation via a diffusion-style process, and train supervised models to predict cascade susceptibility all reported exclusively at aggregated zone level.

Core Idea

Traditional infrastructure risk studies often expose node-level or facility-level vulnerabilities. AFTER82 introduces:

A structural-hazard abstraction layer that enforces privacy by design.

Instead of reporting specific nodes or facilities, all structural and hazard indicators are aggregated into three structural-hazard categories:

-LOW

-MEDIUM

-HIGH

This enables systemic interpretation without operational exposure.

Methodological Pipeline

1.Graph Construction

-Directed weighted network built from OpenStreetMap road geometries

-Node–edge representation suitable for graph analytics

2.Hazard Enrichment

-GEM Global Active Fault proximity aggregation

-District-level ground classification

-Hazard proxies computed without publishing coordinates

3.Zone-Based Privacy Layer

-Percentile-based grouping using structural and hazard intensity

-Aggregation ensures non-disclosure of node-level identifiers

4.Cascade Simulation

-Viral-style diffusion process over discrete time steps

-Generates affected_binary label

5.Predictive Modeling

-Gradient Boosting

-Random Forest

-Evaluation via ROC AUC, KS statistic, misclassification rate

Repository Structure
data/
  safe/                 # Aggregated zone-level CSV outputs only

outputs/
  figures/              # Paper-safe visualizations (heatmaps, summaries)

docs/
  paper/                # Submitted paper versions (if shared)

src/                    # Optional reproducibility scripts

Data Policy

This repository intentionally excludes:

Raw coordinates

Facility names

Node-level identifiers

Sensitive infrastructure metadata

Only aggregated, publication-safe outputs are included.

Raw open-source inputs (OSM, GEM, etc.) must be obtained independently.

Reproducibility Notes

To reproduce results:

1.Place raw data locally under data/raw/ (not included in repo).

2.Execute graph construction and enrichment pipeline.

3.Run cascade simulation.

4.Generate zone-level aggregated outputs.

5.Train predictive models in SAS Model Studio.

This repository ships only final aggregated outputs for transparency and academic communication.

Ethical & Privacy Statement

AFTER82 adopts a strict “privacy-by-design” principle:

-No operational targeting

-No infrastructure vulnerability exposure

-No publication of location-specific insights

All reported findings reflect systemic structural patterns at aggregated zone level.

Competition Context

Developed for:
Curiosity Cup 2026 – A Global SAS® Student Competition

This project demonstrates how privacy-preserving graph analytics can deliver high-discrimination predictive signals while enforcing structural non-disclosure constraints.

License

Open for academic reference.
Not intended for operational risk targeting.
