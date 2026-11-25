# Health Research & Evaluation Methods in R

**Reproducible, step-by-step examples of quantitative research methods for health services research, public health, and policy evaluation.**

This repository contains applied analyses written in **R** and **Quarto**. It illustrates how randomized and observational study designs, statistical models, causal inference approaches, and simulation methods can be implemented, diagnosed, and interpreted in the evaluation of health interventions.

Each module combines annotated R code with explanations of the research question, estimands, assumptions, diagnostic checks, results, and methodological limitations. The accompanying Quarto documents are written in German.

**Disclaimer:** All patient-, practice-, hospital-, and health-insurance-like data are **entirely synthetic**. Scenarios, parameters, and estimated intervention effects are illustrative.

## Available modules

The five available analyses are organized into two complementary tracks.

### 01 · Randomized evaluation and trial design

| Analysis | Focus | Methods and concepts | Files |
| --- | --- | --- | --- |
| **01.1 · Cluster-randomized trial evaluation** | Evaluation of a simulated telemonitoring intervention for heart failure across 48 medical practices and approximately 2,000 insured persons | Stratified cluster randomization, **intention-to-treat (ITT)**, Poisson regression with exposure offsets, **incidence rate ratios (IRRs)**, practice-clustered standard errors, negative-binomial sensitivity analysis, mortality, and *days alive and out of hospital* (DAOH) | [Quarto source](analysis/01-randomized-evaluation/01-cluster-rct-evaluation.qmd) · [HTML report](analysis/01-randomized-evaluation/01-cluster-rct-evaluation.html) |
| **01.2 · RCT design and statistical power** | Planning a cluster-randomized study using repeated simulations | Stratified allocation of practices, **Gamma–Poisson simulation**, within-practice dependence and **intracluster correlation (ICC)**, design effects, Monte Carlo power estimation, effects of cluster count and size, and **empirical Type I error** under the null | [Quarto source](analysis/01-randomized-evaluation/02-rct-design-and-power.qmd) · [HTML report](analysis/01-randomized-evaluation/02-rct-design-and-power.html) |

These two analyses use **separately simulated data**. The evaluation module reads the synthetic RCT CSV files provided in `data/`; the power module generates its own datasets in R and requires no CSV input.

### 02 · Observational studies and causal inference

The following three analyses build on a **shared synthetic observational dataset** comprising 2,000 insured persons observed from **2023 to 2025**. Telemonitoring participation begins in 2025 and is **not randomized**. The analyses therefore examine how alternative adjustment strategies affect the comparison between participants and nonparticipants.

| Analysis | Focus | Methods and concepts | Files |
| --- | --- | --- | --- |
| **02.1 · Group comparisons and regression adjustment** | Comparing HF-related hospitalizations in 2025 before and after adjustment for observed baseline differences | Descriptive group comparisons; **OLS, Poisson, and negative-binomial regression**; absolute differences versus relative rates; offsets for observed person-time; robust standard errors; checks for overdispersion and model instability | [Quarto source](analysis/02-observational-causal-inference/01-poisson regression.qmd) · [HTML report](analysis/02-observational-causal-inference/01-poisson regression.html) |
| **02.2 · Propensity score matching and weighting** | Making intervention and control groups more comparable using observed characteristics | Logistic propensity-score estimation; **common support**; nearest-neighbor **matching**; **standardized mean differences (SMDs)** and love plots; **ATT** versus **ATE**; stabilized **inverse probability of treatment weighting (IPTW)**; weight trimming and sensitivity analysis; weighted OLS and Poisson estimation | [Quarto source](analysis/02-observational-causal-inference/02-propensity-score-matching & weighting.qmd) · [HTML report](analysis/02-observational-causal-inference/02-propensity-score-matching & weighting.html) |
| **02.3 · Difference-in-Differences (DiD)** | Comparing changes in annualized HF hospitalization rates before and after the 2025 program start | Group trajectories for **2023–2025**; descriptive DiD contrasts; **two-way fixed effects** with person and year effects; person-clustered inference; pre-period trend comparisons; **IPTW-weighted DiD**; follow-up duration and mortality as interpretation challenges | [Quarto source](analysis/02-observational-causal-inference/03-difference-in-differences.qmd) · [HTML report](analysis/02-observational-causal-inference/03-difference-in-differences.html) |

The observational modules are **independently executable**: each imports and prepares its own data rather than relying on objects created by another analysis. They use the same underlying CSV files and variable definitions, but address different estimands and identifying assumptions. **Regression adjustment, PSM/IPTW, and DiD do not automatically eliminate unobserved confounding.**

Where a rendered `.html` report is included alongside a `.qmd` source file, it can be downloaded and opened in a web browser. GitHub's file preview does not necessarily render HTML reports as a webpage.

### Planned extensions

Further modules may address **survival analysis**, competing risks, and **health economic modeling**. These topics are not included among the five analyses listed above.

## Getting started

### Requirements

- [R](https://www.r-project.org/)
- [Quarto](https://quarto.org/)
- An R environment such as [RStudio](https://posit.co/download/rstudio-desktop/)

The required R packages are listed in the individual `.qmd` files. To install the packages used across the current modules, run:

```r
install.packages(c(
  "dplyr", "ggplot2", "knitr", "fixest", "modelsummary",
  "labelled", "vtable", "explore", "MatchIt", "cobalt", "broom"
))
```

### Running the analyses

1. **Clone or download** this repository, keeping the `analysis/` and `data/` folders together.
2. Open the relevant `.qmd` file in RStudio, or run `quarto render` from the repository root.
3. Inspect the generated HTML report, tables, and figures. The examples document their assumptions and any model diagnostics in the accompanying text.

For example:

```bash
quarto render analysis/01-randomized-evaluation/01-cluster-rct-evaluation.qmd
quarto render analysis/01-randomized-evaluation/02-rct-design-and-power.qmd
```

For the observational track, open the selected `.qmd` file in `analysis/02-observational-causal-inference/` and render it from RStudio or the command line.

### Synthetic input data

**Cluster-RCT evaluation (01.1):**

- `data/praxen.csv` — synthetic medical practices and randomized study arms.
- `data/versicherte.csv` — synthetic insured persons and baseline information.
- `data/hf_aufnahmen.csv` — synthetic heart-failure hospitalization events.

**Observational analyses (02.1–02.3):**

- `data/01_versicherte_baseline.csv` — baseline characteristics and program participation.
- `data/02_versichertenjahre_panel.csv` — person-year outcomes, costs, and observation time for 2023–2025.
- `data/03_ereigniszeit_2025.csv` — 2025 event and follow-up information.
- `data/datenwoerterbuch.csv` — variable descriptions used to label the analyses.

**RCT design and power (01.2)** does not need external CSV files. It simulates its data from specified assumptions and uses a fixed random seed; runtime depends on the number of Monte Carlo repetitions.

Keep these files in the `data/` folder: the Quarto scripts reference them through relative paths such as `../../data/`.

## Methodological scope and limitations

These modules are **methodological demonstrations, not real-world clinical evaluations**:

- Simulated treatment effects, hospitalization rates, and ICCs are teaching assumptions, not estimates of clinical effectiveness.
- **Randomized and observational examples use different synthetic datasets** and should not be interpreted as alternative estimates from the same experiment.
- In the cluster-RCT analyses, treatment assignment is randomized at the **practice level**, and inference must account for that clustering. The power module also examines empirical Type I error because conventional inference may be imperfect with relatively few clusters.
- The observational analyses depend on stronger identifying assumptions: regression adjustment and propensity-score methods cannot rule out residual or unmeasured confounding; DiD additionally relies on **parallel untreated trends** and the absence of relevant differential shocks.
- Differences between **absolute changes in annualized individual rates** and **relative incidence rate ratios** matter, particularly when follow-up times vary. Mortality may also affect the interpretation of hospitalization outcomes.

The repository is intended for **methodological learning, reproducibility, and research training**, not for clinical decision-making.

## Author

**Stefan Kruse** — quantitative social research, health services research, and policy evaluation.

[GitHub profile](https://github.com/stefan-kruse)

## License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.
