# Predicting Complications Following Cancer Surgery

Analysis code and notebooks from my MSc Applied Data Science thesis (Utrecht University), carried out as an internship at the Department of Rehabilitation Medicine, Amsterdam UMC. The thesis builds a preoperative prediction model for postoperative complications following upper gastrointestinal cancer surgery, using a cohort of 1,022 oesophageal cancer patients from the Dutch Upper Gastrointestinal Cancer Audit (DUCA), treated at Amsterdam UMC between 2016 and 2025.

## About

- Title: Predicting Complications Following Cancer Surgery
- Subtitle: A preoperative prediction model for postoperative complications following upper gastrointestinal cancer surgery
- Programme: MSc Applied Data Science, Department of Information and Computing Sciences, Faculty of Science, Utrecht University

## Thesis and poster

The full thesis and the conference poster are in the `docs/` folder:

- [Thesis](docs/thesis_report.pdf)
- [Poster](docs/poster_presentation.pdf)

## Research question

The central question is how far complications after upper gastrointestinal cancer surgery can be predicted from routinely available information, and whether prediction improves by adding the operative course or the preoperative physiotherapy assessment. The work therefore evaluates three layers of information in turn: a preoperative surgical model from routinely collected variables, a perioperative model that adds the operative course, and the preoperative physiotherapy assessment together with ICF coded functioning.

## Data

No data are included in this repository. All analyses were run inside a secure research environment (MyDRE), and the source data never leave that environment.

The data are governed by a non-WMO ethics waiver (METc 2020.277), a GDPR opt-out model, and a non-disclosure agreement. Patient-level records, registry extracts, and identifiable information are therefore not shareable and are not part of this repository. The code is published for transparency and reproducibility of the methods, not to redistribute data.

Data sources referenced in the code:

- DUCA (Dutch Upper Gastrointestinal Cancer Audit), Amsterdam UMC, for the oesophageal cohort used in the thesis
- DLSA (Dutch Lung Surgery Audit), for the supplementary lung analysis
- ICF category scores produced by the A-PROOF ICF classifier (CLTL, VU Amsterdam) applied to clinical notes

## Repository structure

```
.
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── docs/
│   ├── thesis_report.pdf
│   └── poster_presentation.pdf
├── upper_gi_analysis/
│   ├── 01_preprocessing.ipynb
│   ├── 02_descriptives.ipynb
│   ├── 03_modelling.ipynb
│   ├── 04_sensitivity_analyses.ipynb
│   ├── 05_icf_assessment_analysis.ipynb
│   ├── 06_icf_prediction.ipynb
│   ├── 07_icf_trajectory.ipynb
│   └── 08_thesis_figures.ipynb
├── lung_analysis/
│   ├── 01_exploration.ipynb
│   └── 02_baseline_model.ipynb
└── figures/
```

### upper_gi_analysis (thesis)

| Notebook | Purpose |
| --- | --- |
| `01_preprocessing` | Builds the oesophageal cohort from DUCA, applies the exclusions down to 1,022 patients, recodes registry sentinel values, and derives the outcomes (any complication, Clavien Dindo grades, major complication, pulmonary, reintervention, prolonged stay, readmission, textbook outcome, mortality). |
| `02_descriptives` | Cohort description, outcome prevalences, and the comparison of patient characteristics by outcome reported in the thesis tables. |
| `03_modelling` | The thirteen predictor preoperative surgical model, the preoperative versus perioperative comparison, and the logistic, lasso, and random forest models, with discrimination, calibration, and decision curve analysis. |
| `04_sensitivity_analyses` | Robustness checks, including the surgery year adjustment for prolonged stay, the events-per-variable checks, and the comparison of the flexible models against the logistic model. |
| `05_icf_assessment_analysis` | Links the preoperative physiotherapy risk conclusions and the classifier-coded ICF functioning to the cohort, and summarises the functioning levels. The ICF functioning is coded from the clinical notes of all healthcare professionals, not physiotherapy alone. |
| `06_icf_prediction` | Tests whether the preoperative physiotherapy risk conclusion and the ICF functioning scores add predictive value for complications. |
| `07_icf_trajectory` | Examines ICF based risk in relation to recovery. |
| `08_thesis_figures` | Generates the figures and tables used in the thesis. |

### lung_analysis (supplementary)

Exploratory work on the lung surgery registry (DLSA). This is supplementary and not part of the thesis.

| Notebook | Purpose |
| --- | --- |
| `01_exploration` | Defines the lung cohort using the registration group, recodes sentinel values, inventories candidate outcomes, and summarises the cohort. |
| `02_baseline_model` | A preoperative baseline logistic model for any complication on the primary lung cohort, reporting cross-validated discrimination and calibration. |

## Methods

Models are estimated using complete-case analysis with no imputation. The preoperative surgical model uses thirteen routinely available predictors. Discrimination is reported as the cross-validated area under the ROC curve, and calibration is summarised by the calibration slope and the Brier score with calibration curves. The added value of the operative course is tested with a paired bootstrap on the held-out predictions. Clinical utility is assessed with decision curve analysis. The number of events per variable is monitored to keep models parsimonious. Reporting follows the TRIPOD+AI guideline.

## Key findings

- Preoperative models predict the principal outcomes only modestly, with cross-validated AUCs between 0.55 and 0.60.
- Adding the operative course raises discrimination for major complications, from 0.594 to 0.638 (paired bootstrap probability 0.995), but does not help the other outcomes.
- More flexible models, the lasso and a random forest, do not improve on the logistic model.
- The preoperative physiotherapy assessment and the ICF coded functioning add no discrimination beyond the surgical model.
- Calibration varies by outcome, from good for the textbook outcome (slope 0.99) to moderate for major complications and prolonged stay (0.81 and 0.82) and poor for pulmonary complications (0.48).

## Environment

Developed with Python 3.9.7. Core packages:

- pandas 1.3.4
- numpy 1.20.3
- scikit-learn (liblinear solver)
- matplotlib

See `requirements.txt`. Because the analysis ran in a fixed secure environment, pinning versions to that environment is recommended for exact reproducibility.

## Reproducibility

The notebooks are provided so the analysis steps and modelling choices can be inspected and reproduced on equivalent data. The source data are not provided and cannot be redistributed, so the notebooks are not runnable end to end without access to the original registries through the appropriate governance route.

## Author and supervision

Author: Amandeep Singh, MSc Applied Data Science, Utrecht University.

Supervision:

- Edwin Geleijn, Daily supervisor, Department of Rehabilitation Medicine, Amsterdam UMC
- Prof. Dr. G.T. Barkema, Academic supervisor, Utrecht University

## Acknowledgements

With thanks to the Department of Rehabilitation Medicine at Amsterdam UMC, to Marike van der Leeden for statistical guidance, to the DUCA and DLSA registries (DICA), and to the A-PROOF ICF classifier developed by CLTL at VU Amsterdam.

## License

See `LICENSE`. Confirm any institutional requirements from Utrecht University and Amsterdam UMC before finalising the license.
