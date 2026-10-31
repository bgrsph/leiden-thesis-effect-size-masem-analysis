# Comparison of Cohen's *d* and Hedges' *g* in One-Stage MASEM

Bachelor thesis project (Leiden University, Methodology & Statistics, 2025) by **Buğra Sipahioğlu**.

This repository archives the thesis and the R code used for the analysis.

## 📄 Thesis

**[Read the full thesis (PDF)](Bachelors_Thesis_Bugra_Sipahioglu.pdf)**

> Click the link above to open the PDF in GitHub's built-in viewer.

## What it's about

Standardized mean differences (Cohen's *d* and Hedges' *g*) are often converted into
point-biserial correlations (*r*pb) before being used in **meta-analytic structural
equation modeling (MASEM)**. Hedges' *g* corrects *d* for small-sample bias in individual
studies, but it is unclear whether that correction matters at the meta-analysis level.

Using a dataset of randomized controlled trials on cognitive behavioral therapy (CBT) for
youth depression (mediated by negative cognition), this project builds two one-stage MASEMs —
one from *d*, one from *g* — and compares their pooled correlations and path coefficients.
The two models yield near-identical results, suggesting the choice between *d* and *g* has
minimal impact on MASEM outcomes when average study sample sizes are large.

## Repository structure

```
.
├── Bachelors_Thesis_Bugra_Sipahioglu.pdf   # The thesis
├── data/
│   ├── ESdata.csv      # Raw effect-size-level data
│   └── unimeta.csv     # Study-level metadata (used to identify CBT trials)
├── src/
│   ├── ESComputationCohensDlu.R   # Compute Cohen's d → rpb, build MASEM input
│   ├── ESComputationHedgesG.R     # Compute Hedges' g → rpb, build MASEM input
│   └── Lavaan Syntax              # lavaan mediation model specification
└── output/
    ├── webMASEMCohensD.csv   # Per-study MASEM input (from Cohen's d)
    └── webMASEMHedgesG.csv   # Per-study MASEM input (from Hedges' g)
```

## How it works

1. The two R scripts (`src/`) read `data/ESdata.csv` and `data/unimeta.csv`, filter to CBT
   studies, compute the effect size (*d* or *g*), convert it to a point-biserial correlation,
   and write one row per study to `output/`.
2. The resulting CSVs are entered into [webMASEM](https://cran.r-project.org/package=webMASEM),
   using the mediation model in `src/Lavaan Syntax`, to fit the one-stage MASEMs.

**Requirements:** R (4.4.2) and the `dplyr` package. The scripts use `file.choose()` to
select the input CSVs interactively.

## Contact

Buğra Sipahioğlu · b.sipahioglu@umail.leidenuniv.nl · [github.com/bgrsph](https://github.com/bgrsph)
