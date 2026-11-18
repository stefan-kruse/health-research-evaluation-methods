# Health Research & Evaluation Methods in R

**Reproducible examples of quantitative research methods for health services research, public health, and policy evaluation.**

This repository contains applied, step-by-step analyses written in **R** and **Quarto**. The aim is to demonstrate how research designs, statistical models, and simulation methods can be implemented and interpreted in the evaluation of health interventions.

The examples are designed for methodological learning and reproducibility. They combine annotated code, explanations of underlying assumptions, results, and limitations.

> **Data and evidence disclaimer:** All patient-, practice-, and health-insurance-like data used here are entirely synthetic. The scenarios, parameters, and intervention effects are illustrative, not empirical evidence for the effectiveness of telemonitoring or any other intervention.

## Available modules

| Module | Focus | Methods and concepts |
|---|---|---|
| **01 · Cluster-randomized trial analysis** | Analysis of a simulated telemonitoring evaluation for heart failure | Intention-to-treat analysis, Poisson regression, incidence rate ratios, cluster-robust inference, secondary outcomes |
| **02 · RCT design and statistical power** | Planning a cluster-randomized study through simulations | Stratified cluster randomization, Gamma–Poisson simulation, intracluster correlation, power estimation, Monte Carlo uncertainty, Type I error |

The modules are complementary but use **separately simulated datasets**. Module 01 analyzes supplied synthetic CSV files, while Module 02 generates new data directly in R.

### Planned extensions

Future modules may address observational causal inference, survival analysis, and health economic modeling. These are not included in the current release.

## Getting started

### Requirements

- R
- Quarto
- An R environment such as RStudio


### Running the analyses

Download or clone the repository, open the project folder, and render the relevant Quarto document.

If the modules are stored in `analysis/01-randomized-evaluation/`, use:

`quarto render analysis/01-randomized-evaluation/01-cluster-rct.qmd`

`quarto render analysis/01-randomized-evaluation/02-rct-design-and-power.qmd`

Module 01 requires the synthetic input files `praxen.csv`, `versicherte.csv`, and `hf_aufnahmen.csv` in the repository's `data/` folder. Module 02 is self-contained and requires no external datasets.

The simulations use a fixed random seed for reproducibility. Their execution time increases with the number of repetitions.

## Methodological scope and limitations

These are **illustrative methodological exercises**, not reports of completed real-world clinical trials.

The intervention effects, event rates, and intracluster correlations are simulation assumptions rather than clinical estimates. The examples simplify real-world complications such as incomplete follow-up and varying cluster sizes. In particular, the power module evaluates empirical Type I error alongside power because cluster-robust inference may be imperfect with relatively few clusters.

The analyses are intended to explain and demonstrate methods, not to guide clinical decisions.

## Author

**Stefan Kruse** — quantitative social research, health and policy evaluation.

[GitHub profile](https://github.com/stefan-kruse)

## License

Distributed under the **MIT License**. See `LICENSE` for details.
