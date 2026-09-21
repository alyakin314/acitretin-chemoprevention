# Acitretin chemoprevention of keratinocyte carcinoma

Analysis and figure-generation code for the multi-site retrospective study of acitretin for chemoprevention of cutaneous squamous cell carcinoma (SCC) in immunocompetent and immunosuppressed patients.

`main_analysis.ipynb` is the notebook that produced every figure, table and estimate reported in the manuscript. `figures/` holds the figures it generates.

## Data

The patient-level data are not included. The notebook expects two files in the same folder:

- `Final Dataset 9_21_26.xlsx`, the REDCap export with the study team's corrections
- `discontinuation_reason_coding.csv`, the adverse-effect coding of the free-text discontinuation reasons (columns `free_text`, `adverse_effect`, `category`)

## Running

```
python -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace main_analysis.ipynb
```

Figures are written to `figures/`. Tables, and the one figure labelled by patient, are written to `outputs/final_10yearszero/`; they contain patient-level rows and are not part of this repository.

## Methods summary

- Cohort: at least one biopsy-proven invasive SCC in the 10 years before the first acitretin dose, on acitretin for the first 3 consecutive months, and a recorded Year-1 pre-treatment SCC count. The patient flow is written to `table_patient_flow.csv`.
- Follow-up is censored at the first month with a zero or missing dose.
- Primary analysis: paired, self-controlled negative binomial GEE of SCC counts on an on-drug indicator, offset by log person-months, clustered by patient, exchangeable working correlation, robust standard errors.
- Mean cumulative function: Nelson-Aalen estimator with the Lawless-Nadeau robust variance.
- Analyses over a multi-year pre-treatment window include only patients with a recorded count in every year of that window.

---

Code by [@alyakin314](https://github.com/alyakin314), with friend Claude.
