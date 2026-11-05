# Brief 5: Methods for heterogeneous treatment effects in routinely collected health data

**Date:** 4 November 2026
**Question:** Which methods are used to estimate, tune, select and validate estimators of heterogeneous treatment effects (HTE) in routinely collected health data (electronic health records (EHR), claims and registries), in any clinical domain? What evidence shows how well they work?

**Scope covered:**
- Estimators:
  - meta-learners (S-, T-, X-learners), doubly robust (DR) and R-learners
  - causal forests and causal survival forests (CSF)
  - Bayesian additive regression trees (BART) and Bayesian causal forests (BCF)
  - targeted maximum likelihood estimation (TMLE)
  - neural estimators
- Tuning and model selection without a known effect.
- Validation:
  - plasmode simulation and semi-synthetic benchmarks
  - emulation of, and benchmarking against, randomised controlled trials (RCTs)
  - calibration and discrimination for benefit, including the c-for-benefit
  - rank-weighted average treatment effect (RATE) and Qini curves
  - negative controls
- High-dimensional code covariates.
- Time-to-event and competing-risk effects.
- Reporting guidance.

**Ranking rule (from the coordinator):**
1. Methods evidence tested against a known truth, plus selection, tuning or validation studies on routine data.
2. Time-to-event or competing-risk methods used on routine data.
3. Reporting guidance.
4. Applied studies that reveal how well a method works.
5. Purely applied studies.

**What is in this document:**
- 41 papers have full evidence cards (section 2). These are 40 ranked papers plus one renal paper added for domain coverage.
- 156 further included papers are listed one line each (section 2F). One more, c0396, is merged into Row 17 as a duplicate. Total included at screening: 198.
- The workflow had three phases:
  - Phase 1: search and screening.
  - Phase 2: full-text extraction of the open papers.
  - Phase 3a: user-supplied PDFs and versions of record.
- Working files are in the scratchpad (`brief5/`): `search_log.md`, `screening.md`, `screening_titles.tsv`, `fetch_list.md`, `verification_log.md`, `extraction/` and `texts/`.

**Abbreviations used throughout:**

| Abbreviation | Meaning |
|---|---|
| ACIC | American Causal Inference Conference |
| AFT | accelerated failure time |
| AIPW | augmented inverse probability weighting |
| ATE | average treatment effect |
| AUTOC | area under the targeting operator characteristic curve |
| BLP | best linear projection |
| CATE | conditional average treatment effect |
| CATT | conditional average treatment effect on the treated |
| CPRD | Clinical Practice Research Datalink |
| DGP | data-generating process |
| GRF | generalized random forests |
| hdPS | high-dimensional propensity score |
| iCF / hdiCF | iterative causal forest / high-dimensional iterative causal forest |
| IPCW | inverse probability of censoring weighting |
| IPW / IPTW | inverse probability (of treatment) weighting |
| ITE | individualised treatment effect |
| MIMIC | Medical Information Mart for Intensive Care |
| NCDB | National Cancer Database |
| NCO | negative control outcome |
| PATH | Predictive Approaches to Treatment effect Heterogeneity |
| PCORI | Patient-Centered Outcomes Research Institute |
| PEHE | precision in estimation of heterogeneous effects |
| PS | propensity score |
| RMSE | root mean squared error |
| RMST | restricted mean survival time |
| SATT | sample average treatment effect on the treated |
| T2D | type 2 diabetes |
| TTE | target trial emulation |
| VoR | version of record |

## 0. Assumptions and access limitations

### Assumptions
1. **"Routinely collected data"** means EHR, claims, administrative data, and disease or national registries.
   - This includes ICU EHR databases such as MIMIC and SICdb, the US National Cancer Database (NCDB), and curated clinico-genomic registries (GENIE BPC).
   - Research cohorts (UK Biobank, NHANES, WHI, ADNI) and RCT-only data were out of scope. The exceptions are seeds and validation-metric or reporting papers.
2. **Type 2 diabetes drug comparisons** are included only as methods contributions (Rows 13, 18; one-line c1094, c0294), because Brief 3 covers them.
3. **Seeds were identified on Crossref.** All six match the brief (search log, seed table).
   - Hoogland 2021 is RCT-based.
   - Wyss 2018 concerns hdPS for *average* effects only.
4. **A plasmode or semi-synthetic study counts as known truth on routinely collected covariates** only if its covariates come from routine data:
   - Wendling: real claims and hospital covariates (Row 1).
   - Doutreligne & Varoquaux: the Linked Births and Infant Deaths Database, a registry (Row 11).
   - SurvHTE-Bench: MIMIC-IV (Row 10).
   - Du et al.: the Premier database (Row 4).
   - Shaw: Kaiser Permanente Washington EHR (Row 6).
   - Wyss: US claims (Row 5).

   Purely synthetic simulations are labelled as such (Rows 9, 13, 14, 15, 26–29). ACIC 2022 is fully synthetic but calibrated to Medicare summaries (Rows 2–3).
5. **Rule 7 applies.** 198 papers qualified at screening. 41 have full cards and the rest are listed one line each, with screening notes taken from abstracts only.

### Access limitations
- **Wiley, Elsevier, OUP, LWW, Project MUSE and Research Square were blocked.** NCBI Bookshelf and the PMC HTML pages served reCAPTCHA, which was not circumvented. The user supplied 11 PDFs (versions of record or preprint).
- **c0489, the PCORI report (Row 20), is abstract only.** The user pasted the abstract from the report PDF. Chapter structure comes from the table of contents only.
- **PMC texts have no page numbers**, so their quotes are located by section (§). PDF quotes give the PDF page (p.).
- **Supplementary material was not read for any paper.** Fields that depend on supplements are marked UNVERIFIED.
- **Some databases could not be queried directly:**
  - Google Scholar.
  - OpenReview and the NeurIPS, ICML, ICLR, AISTATS, CLeaR and UAI proceedings. These were covered through the arXiv API, Semantic Scholar citation chasing and two site-restricted web searches (see the search log).

## 1. Search log

All searches were run on 4 November 2026. The date window is 2019 to November 2026; older seeds are accepted.

- **Pool:** 2,135 de-duplicated records from PubMed, arXiv and Semantic Scholar forward and backward chasing. In addition, 63 arXiv titles and 70 web-search results were read outside the pool.
- **Abstract screening:** 394 records (381 from the pool plus 13 added by hand). Of these, 196 were excluded with reasons and 198 were included.
- **Title screening:** 1,754 records were excluded on title. Title triage used a keyword flag only to order the reading; every title with a health term was read.


| # | Source | Query / action | Hits | Screened (title) | Abstract-screened | Included |
|---|---|---|---|---|---|---|
| 1 | PubMed (E-utilities) [acic] | `("ACIC"[tiab] OR "data challenge"[tiab] OR "causal inference competition"[tiab] OR "data competition"[tiab]) AND (causal[tiab] OR "treatment effect"[tiab]) AND 2019:2026[dp]` | 6 | 6 | 1 | 0 |
| 2 | PubMed (E-utilities) [cml] | `("causal machine learning"[tiab]) AND ("electronic health"[tiab] OR claims[tiab] OR registry[tiab] OR "real-world"[tiab] OR "administrative"[tiab] OR "database"[tiab] OR "routinely"[tiab]) AND 2019:2026[dp]` | 52 | 52 | 22 | 17 |
| 3 | PubMed (E-utilities) [core] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "individual treatment effect*"[tiab] OR "causal forest*"[tiab] OR "meta-learner*"[tiab] OR "X-learner"[tiab] OR "R-learner"[tiab] OR "Bayesian causal forest*"[tiab] OR "Bayesian additive regression tree*"[tiab]) AND ("electronic health record*"[tiab] OR "electronic medical record*"[tiab] OR "claims"[tiab] OR registry[tiab] OR registries[tiab] OR "administrative"[tiab] OR "routinely collected"[tiab] OR "real-world"[tiab] OR "healthcare database*"[tiab] OR "health care database*"[tiab] OR CPRD[tiab] OR Medicare[tiab] OR "insurance"[tiab] OR "observational data"[tiab] OR "nationwide"[tiab]) AND 2019:2026[dp]` | 494 | 494 | 156 | 94 |
| 4 | PubMed (E-utilities) [d_cprd] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (CPRD[tiab] OR "Clinical Practice Research Datalink"[tiab] OR QResearch[tiab] OR SAIL[tiab] OR THIN[tiab] OR "Danish"[tiab] OR "Swedish"[tiab] OR "Norwegian"[tiab] OR "Finnish"[tiab] OR "Korea*"[tiab] OR "Japan*"[tiab] OR "Taiwan*"[tiab] OR "Ontario"[tiab]) AND 2019:2026[dp]` | 81 | 81 | 15 | 11 |
| 5 | PubMed (E-utilities) [d_cv] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (cardiovascular[tiab] OR "atrial fibrillation"[tiab] OR "heart failure"[tiab] OR statin*[tiab] OR antihypertensive*[tiab] OR anticoagul*[tiab] OR "myocardial infarction"[tiab] OR stroke[tiab] OR coronary[tiab]) AND (registry[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "electronic medical"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR database[tiab] OR Medicare[tiab]) AND 2019:2026[dp]` | 96 | 96 | 36 | 23 |
| 6 | PubMed (E-utilities) [d_infect] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (sepsis[tiab] OR antibiotic*[tiab] OR infection*[tiab] OR COVID*[tiab] OR SARS-CoV-2[tiab] OR HIV[tiab] OR antiviral*[tiab] OR vaccin*[tiab] OR tuberculosis[tiab]) AND (registry[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "electronic medical"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR database[tiab] OR MIMIC[tiab] OR Veterans[tiab]) AND 2019:2026[dp]` | 56 | 56 | 22 | 16 |
| 7 | PubMed (E-utilities) [d_mental] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (depress*[tiab] OR antidepress*[tiab] OR psychiatr*[tiab] OR schizophreni*[tiab] OR bipolar[tiab] OR antipsychotic*[tiab] OR lithium[tiab] OR opioid use disorder[tiab] OR ADHD[tiab] OR dementia[tiab]) AND (registry[tiab] OR registries[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "electronic medical"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR "health records"[tiab] OR database[tiab]) AND 2019:2026[dp]` | 33 | 33 | 11 | 6 |
| 8 | PubMed (E-utilities) [d_onc] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (cancer[tiab] OR oncolog*[tiab] OR tumor[tiab] OR tumour[tiab] OR chemotherapy[tiab] OR radiotherapy[tiab] OR immunotherapy[tiab]) AND (registry[tiab] OR SEER[tiab] OR "National Cancer Database"[tiab] OR NCDB[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR database[tiab] OR Flatiron[tiab]) AND 2019:2026[dp]` | 60 | 60 | 15 | 11 |
| 9 | PubMed (E-utilities) [d_renal] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (kidney[tiab] OR renal[tiab] OR dialysis[tiab] OR CKD[tiab] OR "acute kidney injury"[tiab]) AND (registry[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "electronic medical"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR database[tiab] OR MIMIC[tiab]) AND 2019:2026[dp]` | 42 | 42 | 22 | 17 |
| 10 | PubMed (E-utilities) [d_resp] | `("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneity of treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individualised treatment effect*"[tiab] OR "causal forest*"[tiab] OR "causal machine learning"[tiab] OR "meta-learner*"[tiab]) AND (COPD[tiab] OR asthma[tiab] OR "pulmonary"[tiab] OR "respiratory"[tiab] OR pneumonia[tiab] OR "lung function"[tiab] OR ventilat*[tiab]) AND (registry[tiab] OR claims[tiab] OR "electronic health"[tiab] OR "electronic medical"[tiab] OR "real-world"[tiab] OR nationwide[tiab] OR database[tiab] OR MIMIC[tiab]) AND 2019:2026[dp]` | 31 | 31 | 9 | 7 |
| 11 | PubMed (E-utilities) [emul] | `("target trial emulation"[tiab] OR "emulat*"[tiab] OR "benchmark*"[tiab]) AND ("causal forest*"[tiab] OR "heterogeneous treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "meta-learner*"[tiab] OR "causal machine learning"[tiab]) AND 2019:2026[dp]` | 102 | 102 | 25 | 12 |
| 12 | PubMed (E-utilities) [emul2] | `("RCT-DUPLICATE"[tiab] OR ("trial emulation"[tiab] AND (subgroup*[tiab] OR heterogene*[tiab] OR "effect modification"[tiab])) OR ("benchmark*"[tiab] AND "randomized"[tiab] AND (heterogene*[tiab]) AND (observational[tiab] OR claims[tiab] OR registry[tiab]))) AND 2019:2026[dp]` | 346 | 346 | 22 | 13 |
| 13 | PubMed (E-utilities) [hdps] | `("high-dimensional propensity"[tiab] OR "hdPS"[tiab] OR "medical codes"[tiab] OR "claims codes"[tiab] OR "high-dimensional covariate*"[tiab]) AND ("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "effect modification"[tiab] OR "causal forest*"[tiab] OR "conditional average"[tiab]) AND 2019:2026[dp]` | 14 | 14 | 5 | 3 |
| 14 | PubMed (E-utilities) [negctl] | `("negative control*"[tiab]) AND ("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "conditional average"[tiab] OR "causal forest*"[tiab] OR "individualized treatment"[tiab]) AND 2019:2026[dp]` | 9 | 9 | 4 | 0 |
| 15 | PubMed (E-utilities) [neural] | `("neural network*"[tiab] OR "deep learning"[tiab] OR "representation learning"[tiab] OR "embedding*"[tiab] OR autoencoder*[tiab] OR "transformer"[tiab] OR "foundation model*"[tiab]) AND ("individualized treatment effect*"[tiab] OR "individual treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "heterogeneous treatment effect*"[tiab] OR "counterfactual"[tiab]) AND ("electronic health"[tiab] OR "electronic medical"[tiab] OR claims[tiab] OR registry[tiab] OR "real-world"[tiab] OR "observational"[tiab]) AND 2019:2026[dp]` | 84 | 84 | 24 | 9 |
| 16 | PubMed (E-utilities) [plasmode] | `(plasmode[tiab]) AND 2019:2026[dp]` | 48 | 48 | 11 | 3 |
| 17 | PubMed (E-utilities) [rate] | `("heterogeneous treatment effect*"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "causal forest*"[tiab]) AND ("comparison"[tiab] OR "comparing"[tiab] OR "evaluation of"[tiab] OR "performance"[tiab]) AND ("simulation study"[tiab] OR "plasmode"[tiab] OR "semi-synthetic"[tiab] OR "semisynthetic"[tiab]) AND 2019:2026[dp]` | 27 | 27 | 9 | 4 |
| 18 | PubMed (E-utilities) [report] | `("reporting guideline*"[tiab] OR checklist[tiab] OR "consensus statement"[tiab] OR "statement"[ti] OR "recommendations"[ti] OR "guidance"[ti] OR "framework"[ti]) AND ("heterogeneity of treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "heterogeneous treatment effect*"[tiab] OR "predictive approaches"[tiab] OR "individualized treatment effect*"[tiab]) AND 2019:2026[dp]` | 72 | 72 | 17 | 8 |
| 19 | PubMed (E-utilities) [select] | `("model selection"[tiab] OR hyperparameter*[tiab] OR tuning[tiab] OR "validation"[tiab] OR benchmark*[tiab]) AND ("conditional average treatment effect*"[tiab] OR "heterogeneous treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "individual treatment effect*"[tiab]) AND (simulation[tiab] OR "simulated"[tiab] OR plasmode[tiab] OR "semi-synthetic"[tiab]) AND 2019:2026[dp]` | 17 | 17 | 6 | 2 |
| 20 | PubMed (E-utilities) [surv] | `("causal survival forest*"[tiab] OR (("heterogeneous treatment effect*"[tiab] OR "treatment effect heterogeneity"[tiab] OR "conditional average treatment effect*"[tiab] OR "individualized treatment effect*"[tiab] OR "causal forest*"[tiab]) AND ("time-to-event"[tiab] OR survival[tiab] OR "competing risk*"[tiab] OR censor*[tiab] OR "restricted mean"[tiab]))) AND 2019:2026[dp]` | 184 | 184 | 62 | 38 |
| 21 | PubMed (E-utilities) [tmle] | `("targeted maximum likelihood"[tiab] OR "targeted learning"[tiab] OR "doubly robust"[tiab] OR "augmented inverse"[tiab] OR "double machine learning"[tiab] OR "debiased machine learning"[tiab]) AND (heterogene*[tiab] OR "conditional average"[tiab] OR "effect modification"[tiab] OR "individualized"[tiab]) AND ("electronic health"[tiab] OR claims[tiab] OR registry[tiab] OR "administrative"[tiab] OR "real-world"[tiab] OR "healthcare database*"[tiab] OR Medicare[tiab] OR "routinely collected"[tiab]) AND 2019:2026[dp]` | 52 | 52 | 21 | 16 |
| 22 | PubMed (E-utilities) [valid] | `("c-for-benefit"[tiab] OR "c for benefit"[tiab] OR Qini[tiab] OR "rank-weighted average treatment effect"[tiab] OR "targeting operator characteristic"[tiab] OR "calibration for benefit"[tiab] OR "benefit calibration"[tiab] OR "discrimination for benefit"[tiab] OR ("uplift"[tiab] AND ("treatment effect"[tiab] OR causal[tiab]))) AND 2019:2026[dp]` | 50 | 50 | 18 | 14 |
| 23 | arXiv API [acic] | `abs:"ACIC" AND abs:"2022"` | 0 | 0 | 0 | 0 |
| 24 | arXiv API [csf] | `abs:"causal survival forest" OR abs:"causal survival forests" OR (abs:"heterogeneous treatment effect" AND (abs:survival OR abs:"time-to-event" OR abs:"competing risk" OR abs:censoring))` | 42 | 42 | 27 | 8 |
| 25 | arXiv API [hte_ehr] | `(abs:"heterogeneous treatment effect" OR abs:"conditional average treatment effect" OR abs:"individualized treatment effect" OR abs:"treatment effect heterogeneity") AND (abs:"electronic health records" OR abs:"electronic health record" OR abs:claims OR abs:registry OR abs:"real-world data" OR abs:"observational health" OR abs:"health care database" OR abs:"healthcare database")` | 66 | 66 | 18 | 10 |
| 26 | arXiv API [modsel] (run after the pool was built; titles read directly) | `(abs:"model selection" OR abs:"hyperparameter" OR abs:"validation") AND (abs:"conditional average treatment effect" OR abs:"heterogeneous treatment effect" OR abs:"individualized treatment effect") AND (abs:"electronic health" OR abs:"claims" OR abs:"observational health" OR abs:"real-world")` | 37 | 37 | 6 | 0 new (overlap with pool) |
| 27 | arXiv API [plasmode] | `abs:plasmode OR abs:"semi-synthetic" AND (abs:"treatment effect" AND (abs:health OR abs:medical OR abs:clinical))` | 41 | 41 | 17 | 11 |
| 28 | arXiv API [rate] | `abs:"rank-weighted average treatment effect" OR abs:"Qini" AND abs:"treatment effect" OR abs:"c-for-benefit" OR abs:"calibration" AND abs:"individualized treatment effect"` | 7 | 7 | 4 | 2 |
| 29 | arXiv API [repr] (run after the pool was built; titles read directly) | `(abs:"treatment effect" OR abs:"causal effect") AND (abs:"medical codes" OR abs:"claims data" OR abs:"diagnosis codes" OR abs:"EHR embeddings" OR abs:"foundation model" OR abs:"pretrained" OR abs:"representation") AND (abs:"electronic health records" OR abs:"claims")` | 26 | 26 | 6 | 2 new (1905.03297, 2501.07789); 2 already in pool |
| 30 | arXiv API [select] | `(abs:"conditional average treatment effect" OR abs:"heterogeneous treatment effect" OR abs:CATE) AND (abs:"model selection" OR abs:"hyperparameter" OR abs:"validation" OR abs:"evaluation metric") AND (abs:medical OR abs:clinical OR abs:health)` | 26 | 26 | 7 | 2 |
| 31 | Semantic Scholar Graph API | forward (citing papers) of Wendling 2018 (10.1002/sim.7820) (limit=100 pages, 4 s spacing, retries on 429) | 120 | 120 (2019+ records pooled: 115) | 34 | 11 |
| 32 | Crossref API (Semantic Scholar returned no reference list) | backward chasing: reference list of Wendling 2018 (10.1002/sim.7820) | 41 | 41 | 0 | 0 (pre-2019 or software; outside window) |
| 33 | Semantic Scholar Graph API | forward (citing papers) of Wyss 2018 (10.1097/EDE.0000000000000762) (limit=100 pages, 4 s spacing, retries on 429) | 69 | 69 (2019+ records pooled: 59) | 8 | 1 |
| 34 | Crossref API (Semantic Scholar returned no reference list) | backward chasing: reference list of Wyss 2018 (10.1097/EDE.0000000000000762) | 35 | 35 | 0 | 0 (pre-2019 or software; outside window) |
| 35 | Semantic Scholar Graph API | forward (citing papers) of Kent 2020 PATH (10.7326/M18-3667) (limit=100 pages, 4 s spacing, retries on 429) | 400 | 400 (2019+ records pooled: 390) | 58 | 29 |
| 36 | Semantic Scholar Graph API | backward (references) of Kent 2020 PATH (10.7326/M18-3667) (limit=100 pages, 4 s spacing, retries on 429) | 79 | 79 (2019+ records pooled: 3) | 2 | 1 |
| 37 | Semantic Scholar Graph API | forward (citing papers) of Hoogland 2021 (10.1002/sim.9154) (limit=100 pages, 4 s spacing, retries on 429) | 81 | 81 (2019+ records pooled: 79) | 23 | 12 |
| 38 | Semantic Scholar Graph API | backward (references) of Hoogland 2021 (10.1002/sim.9154) (limit=100 pages, 4 s spacing, retries on 429) | 77 | 77 (2019+ records pooled: 14) | 3 | 1 |
| 39 | Semantic Scholar Graph API | forward (citing papers) of Efthimiou 2023 (10.1002/sim.9665) (limit=100 pages, 4 s spacing, retries on 429) | 43 | 43 (2019+ records pooled: 42) | 10 | 8 |
| 40 | Semantic Scholar Graph API | backward (references) of Efthimiou 2023 (10.1002/sim.9665) (limit=100 pages, 4 s spacing, retries on 429) | 50 | 50 (2019+ records pooled: 19) | 3 | 1 |
| 41 | Semantic Scholar Graph API | forward (citing papers) of Cui 2023 (10.1093/jrsssb/qkac001) (limit=100 pages, 4 s spacing, retries on 429) | 147 | 147 (2019+ records pooled: 143) | 52 | 15 |
| 42 | Semantic Scholar Graph API | backward (references) of Cui 2023 (10.1093/jrsssb/qkac001) (limit=100 pages, 4 s spacing, retries on 429) | 83 | 83 (2019+ records pooled: 13) | 1 | 0 |
| 43 | WebSearch | `ACIC 2022 data challenge heterogeneous treatment effects simulated Medicare claims subgroup estimation lessons learned` | 10 | 10 | - | 3 (Thal & Finucane; Kokandakar et al.; Wan & Zhang, the last confirmed via Crossref) |
| 44 | WebSearch | `heterogeneous treatment effects observational claims data compared with randomized trial subgroup replication emulation RCT-DUPLICATE effect modification` | 10 | 10 | - | 0 new (pointed to the PCORI project already in the pool, c0489) |
| 45 | WebSearch | `plasmode simulation heterogeneous treatment effects conditional average treatment effect electronic health records evaluation causal forest BART` | 10 | 10 | - | 0 new (c0203, Karim, Shaw, Wendling already in pool) |
| 46 | WebSearch | `"adjuvant chemotherapy" colon cancer "registry data" "method comparison and validation" randomized trial individual treatment effects Netherlands` | 10 | 10 | - | 0 new (located c1530 preprint; no journal version found) |
| 47 | WebSearch | `"Causal Methods Madness" Thal Finucane 2022 ACIC Observational Studies pdf arXiv` | 10 | 10 | - | 0 (no open version found) |
| 48 | WebSearch | `site:proceedings.mlr.press heterogeneous treatment effect electronic health records OR claims survival CATE evaluation` | 10 | 10 | - | 1 new (Hong, Nirantharakumar, Yau; PMLR 333, 2026) |
| 49 | WebSearch | `site:openreview.net OR site:proceedings.neurips.cc conditional average treatment effect model selection electronic health records benchmark semi-synthetic` | 10 | 10 | - | 0 new |
| 50 | Crossref API | seed DOI checks (6 seeds); title look-ups for Efthimiou 2023, Cui 2023, Hoogland 2021, ACIC 2022 papers, c1530 | - | - | - | seeds confirmed (below) |

### Seed identification (Crossref metadata checked 4 Nov 2026)

| Seed in brief | Identified paper | DOI | Match to brief |
|---|---|---|---|
| Wendling et al. 2018 (Stat Med) | Wendling T, Jung K, Callahan A, Schuler A, Shah NH, Gallego B. Comparing methods for estimation of heterogeneous treatment effects using observational data from health care databases. Stat Med 2018;37(23):3309-24 | 10.1002/sim.7820 | Yes |
| Wyss et al. 2018 (Epidemiology) | Wyss R, Schneeweiss S, van der Laan M, Lendle SD, Ju C, Franklin JM. Using Super Learner prediction modeling to improve high-dimensional propensity score estimation. Epidemiology 2018;29(1):96-106 | 10.1097/EDE.0000000000000762 | Yes, but it concerns average effects and hdPS, not HTE (relevant to high-dimensional code covariates and plasmode). arXiv 1703.02236 is a different paper (Ju et al. 2019). |
| Kent et al. 2020, PATH (Ann Intern Med) | Kent DM, Paulus JK, van Klaveren D, et al. The Predictive Approaches to Treatment effect Heterogeneity (PATH) Statement. Ann Intern Med 2020;172(1):35-45 | 10.7326/M18-3667 | Yes (explanation and elaboration: 10.7326/M18-3668) |
| Hoogland et al. 2021 (Stat Med) | Hoogland J, IntHout J, Belias M, Rovers MM, Riley RD, Harrell FE Jr, et al. A tutorial on individualized treatment effect prediction from randomized trials with a binary endpoint. Stat Med 2021;40(26):5961-81 | 10.1002/sim.9154 | Yes; RCT-focused, no routine data |
| Efthimiou et al. 2023 (Stat Med) | Efthimiou O, Hoogland J, Debray TPA, Seo M, Furukawa TA, Egger M, White IR. Measuring the performance of prediction models to personalize treatment choice. Stat Med 2023;42(8):1188-1206 | 10.1002/sim.9665 | Yes (the 2025 survival extension, 10.1002/sim.70050, is included as c1075) |
| Cui et al. 2023, causal survival forests (JRSS-B) | Cui Y, Kosorok MR, Sverdrup E, Wager S, Zhu R. Estimating heterogeneous treatment effects with right-censored data via causal survival forests. J R Stat Soc Series B 2023;85(2):179-211 | 10.1093/jrsssb/qkac001 | Yes (arXiv 2001.09887v5) |

### Sources not queried, or only partly

- Google Scholar cannot be queried automatically; substituted by Semantic Scholar citation chasing, Crossref and WebSearch.
- OpenReview and the NeurIPS, ICML, ICLR, AISTATS, CLeaR and UAI proceedings were not searched directly (api2.openreview.net blocked). They were covered indirectly through the arXiv API, Semantic Scholar forward citations (which index these venues) and two site-restricted WebSearch queries (PMLR; OpenReview/NeurIPS).
- Semantic Scholar returned no reference lists for Wendling 2018 and Wyss 2018 (publisher-elided); Crossref reference lists were used instead.
- One PubMed record (PMID 40334019, a book record) could not be parsed and was skipped.
- Seed references dated before 2019 were read by title only; they are outside the window and none was added.
- Full texts on Elsevier, Wiley, OUP, LWW, Project MUSE and Research Square were blocked, and NCBI Bookshelf served reCAPTCHA; see fetch_list.md.


### Domain-specific PubMed searches

The d_* queries combine the HTE term block with domain terms (mental health, respiratory, renal, infection, cardiovascular, oncology) and routine-data terms; d_cprd targets named UK, Nordic and Asian routine-data sources. They were run to check domain coverage, not only methods coverage.


## 2. Evidence table (one card per paper)

Each card gives the brief's fields in order: paper; data source and country; clinical domain; sample size; treatments; outcome type; estimators; tuning and selection procedure; validation approach; known truth; subgroups; main result; code availability. The cards also give the link, version and peer-review status. Each extracted claim carries a page (p.) or section (§) reference and a verbatim quotation of fewer than 25 words. The label My judgement marks my own reading. UNVERIFIED marks anything the text read does not support.

### A. Methods tested against a known truth (simulation or plasmode), ranked first

#### Row 1. [S01] (seed) Wendling T, Jung K, Callahan A, Schuler A, Shah NH, Gallego B (2018). Comparing methods for estimation of heterogeneous treatment effects using observational data from health care databases. Stat Med 37(23):3309–3324

- **Link, version, peer review:** https://doi.org/10.1002/sim.7820 — version of record (user-supplied PDF, Wiley download stamp 04/11/2026); peer reviewed.
- **Source text for quotes:** `texts/user_wendling2018_statmed.txt` (coordinator's pdftotext; p. = PDF page; PDF pages 1–16 = journal pp. 3309–3324).
- **Data source and country:** four published US database studies — "the Nationwide Readmissions Database (NRD) and the Truven MarketScan" claims (p.6).
- **Clinical domain:** cardiovascular (TAVR volume, critical limb ischaemia revascularisation, apixaban vs warfarin in NVAF) and type 2 diabetes (insulin glargine vs NPH; methods use, not a drug comparison of interest here).
- **Sample size:** source datasets 4,913 / 74,190 / 163,336 / 182,618 (Table 1, p.8); simulated datasets "capped ... to 10 000 observations" (p.8).
- **Treatments:** low vs high TAVR-volume hospital; endovascular vs surgical CLI therapy; apixaban vs warfarin; insulin GLA vs NPH.
- **Outcome type:** binary (30-day readmission, stroke/SE, etc.); estimand the conditional risk difference (p.1).
- **Estimators:** null estimator, logistic-regression G-computation (LASSO-selected interactions), BART (± propensity), causal forest (grf), causal boosting, bagged causal MARS (p.8–9).
- **Tuning and selection procedure:** "Causal forest was applied using the grf package and its default hyperparameter values"; LASSO "penalty parameters optimized for the deviance by 10‐fold cross‐validation"; causal boosting with cross-validation (p.9). Outcome-generating neural network tuned by grid search on a 20% validation set (p.8).
- **Validation approach:** "real covariate and treatment assignment data are used and only outcomes are simulated based on nonparametric models of the real outcomes" (p.1); outcome model a deep feed-forward network with mean log OR fixed to the original study estimate (p.8); "The only stochastic process ... is the process of sampling the binary outcome variable"; "repeated 50 times in each of the 4 experiments (200 simulated datasets in total)" (p.8).
- **Known truth available (plasmode or simulation):** yes (true CATE per patient).
- **Subgroups:** none; individual CATE RMSE, ATE relative bias, CI coverage for ATE.
- **Main result:** "BART and causal boosting (with cross‐validation) perform consistently well" and "significantly better than causal forest, bagged causal MARS and a logistic regression G‐computation estimator" (p.13). Negative results: in TAVR (tiny heterogeneity) "the null estimator performed better than all other methods" (p.10); in CLI "all methods performed better than the null estimator except for causal MARS and causal forest" (p.10); ATE coverage "just above 60% for the BART methods and as low as 30% for causal forest" in the highly heterogeneous T2DM study (p.10). CATE interval coverage not studied: "We did not investigate the coverage properties for CATEs" (p.14).
- **Code availability:** "available on our Git repository: https://git.aihi.mq.edu.au/twend/HeterogeneousTreatmentEffects/tree/master" (p.10); data not shareable.
- *Covariates:* "at least 86% of the baseline covariates were formatted as binary indicators" of comorbidity, procedure or medication history (p.10); 25–62 covariates (Table 1).
- *Limits stated:* confounding strength cannot be varied ("we cannot vary the magnitude of confounding by simply varying the regression coefficients", p.14); generalisation needs "repeating this evaluation over many independent real studies" (p.14); propose the simulation as "a preliminary step to the actual causal analysis" (p.14).
- *My judgement (link to c0664/c1716):* treatment is kept as observed (a sample-treatment-type design without resampling), so the true propensity is unknown and overlap can only be inspected ("the only way we can assess nonoverlap is by examining the estimated propensity scores", p.10); Shaw et al. and Karim show such designs can mis-rank propensity-based and flexible estimators — the causal-forest/AIPW results here may be affected.
- *Not verified:* supplementary material (if any).

#### Row 2. [M01] Thal DRC, Finucane MM (2023). Causal methods madness: lessons learned from the 2022 ACIC competition to estimate health policy impacts. Observational Studies 9(3):3–27

- **Link, version, peer review:** https://doi.org/10.1353/obs.2023.0023 — version of record (Project MUSE PDF supplied by user; MUSE cover page says pp. 3-27, article header "9.3 (2023): 3-28"); Observational Studies is peer reviewed (competition report).
- **Source text for quotes:** `texts/user_thal2023_obsstudies.txt` (p. = PDF page; PDF p.1 is the MUSE cover sheet).
- **Data source and country:** fully synthetic data calibrated to summaries of a real US Medicare primary-care evaluation — "Although the DGP was designed to mimic summaries of this real data set, covariates, outcomes, and treatment assignment were all simulated" (p.4). Not resampled routine data; the DGP is not public ("we chose not to make the DGP itself public", p.4).
- **Clinical domain:** health policy / primary care (Medicare spending).
- **Sample size:** Track 1 "about 300,000 patients from 500 practices (roughly 200 treated and 300 comparison) over four years" (p.5); Track 2 practice-level aggregates; 3,400 data sets (p.14 "across the 3,400 simulated data sets").
- **Treatments:** practice-level voluntary intervention (confounded participation).
- **Outcome type:** continuous, skewed (monthly Medicare spending); difference-in-differences ignorability (p.8).
- **Estimators:** "20 teams submitted results from 58 estimators" — "8 focusing on modeling the relationship between covariates and participation, 29 focusing on modeling the response surface, and 21 taking a doubly robust approach" (p.10); organiser benchmarks incl. DiD, weighted BCF (wbcf) and a no-heterogeneity benchmark (gumpy).
- **Tuning and selection procedure:** participants' own; organisers ran BCF "using out-of-the-box settings" (p.11).
- **Validation approach:** known-truth competition with four DGP "knobs" (confounding strength, confounding source, heterogeneity source, …) (p.6–7); metrics RMSE, interval coverage, and new DRMSE for subgroup effects relative to the overall effect (p.14).
- **Known truth available (plasmode or simulation):** yes. Caveat: "we could not calibrate confounding and heterogeneity because we don’t know what their real-world values are" (p.6).
- **Subgroups:** SATT overall, subgroup CATTs (e.g. practice type, region), practice-level effects (UTEs) (p.9, p.15).
- **Main result:** prior challenges showed "estimating treatment effect heterogeneity is a substantially taller order than estimating the average treatment effect only" (p.4). "BART-based estimators are more likely to find subgroup signal without overfitting" (Figure 2 title, p.15); methods worse than gumpy on DRMSE "would benefit from more regularization" (p.14). Failure: "For practice UTEs, no estimator obtained satisfactory RMSE while achieving nominal coverage" (Figure 3 title, p.16); only "25 out of 58 submitted estimators even attempted UTE estimation" (p.15). Bootstrap intervals "never achieved nominal coverage" among official submissions (p.13). "doubly robust meta-learner models often performed worse than the standalone methods that they incorporated" (p.19). Patient-level data did not beat practice-level aggregates (abstract, p.2). One BART estimator "had extremely low power to detect subgroup heterogeneity" from over-regularisation (p.12).
- **Code availability:** DGP withheld; data sets/true impacts were published on the competition website per text (p.10 mentions publishing "true impacts to our website") — URL not extracted, UNVERIFIED.
- *Limitations stated (negative for the design):* "the standard deviation of the baseline outcome across patients within a practice was a strong proxy for confounding" (p.19), so a derived covariate drove success; "it was difficult to disentangle performance of estimators from modeling choices" (p.19).
- *Lessons stated:* "Deconfound flexibly"; "Regularize CATT and UTE estimates"; "Quantify uncertainty using model-based approaches" (p.16–17).
- *Not verified:* team-level tables beyond RMSE column (Table 1, pp.21–25); figure values.

#### Row 3. [M02] Kokandakar AH, Kang H, Deshpande SK (2023). Bayesian Causal Forests & the 2022 ACIC Data Challenge: Scalability and Sensitivity. Observational Studies 9(3):29–41

- **Link, version, peer review:** https://arxiv.org/abs/2211.02020v2 (arXiv v2, 11 May 2023; journal_ref Observational Studies 9(3), 29-41) — read the arXiv version; published version (https://doi.org/10.1353/obs.2023.0024) peer reviewed, not compared (Project MUSE unreachable).
- **Source text for quotes:** `texts/M02_arxiv2211.02020v2.txt` (pdftotext; p. = PDF page).
- **Data source and country:** synthetic ACIC 2022 data modelled on US Medicare (p.3: "Each synthetic dataset simulated observations of beneficiary-level Medicare expenditure data over a period of four years").
- **Clinical domain:** health policy / primary care (practice-level intervention).
- **Sample size:** p.3 "a total of 3,400 synthetic datasets consisting of 200 independent realizations of 17 different data generating processes"; "Each beneficiary received care at one of about 500 different medical practices" (p.3). Beneficiary counts per dataset not extracted.
- **Treatments:** practice-level intervention assigned after two years (p.3 "treatment was assigned to some practices after two years").
- **Outcome type:** continuous (medical expenditure), longitudinal.
- **Estimators:** Bayesian causal forests (BCF) via new package flexBCF, with propensity score as covariate (CBPS or gradient boosting, GBM) and sparsity-inducing Dirichlet splitting prior vs uniform (p.2, p.7).
- **Tuning and selection procedure:** none data-driven; sensitivity analysis over 4 configurations (p.7 "we considered four model configurations CBPS(S), CPBS(D), GBM(S), and GBM(D)").
- **Validation approach:** competition truth released after the challenge (p.6 "the organizers provided us with the individual-level treatment effects, which we used to compute the RMSE and uncertainty interval coverage").
- **Known truth available (plasmode or simulation):** yes (synthetic).
- **Subgroups:** 12 subgroup SATTs (Figure 4 caption p.10: "Uncertainty interval coverage for all 12 SATT's"); estimand CATT (p.3).
- **Main result:** beneficiary-level ATT RMSE (coverage) "between 9.2 (33%) to 29.9 (82.5%)" and SATTs "ranged from 10.73 (26.5%) to 39.72 (81%)" for nominal 90% intervals (p.6); results "fairly middling compared to other submissions, especially in the presence of confounding" (p.6). Point predictions "not especially sensitive to these modeling choices" but "flexibly estimated propensity scores often yielded better-calibrated uncertainty intervals" (p.1); sparsity-inducing priors "consistently yielded lower coverage" (p.10). Practice-level fitting raised coverage, which authors "suspect ... is an artifact of sample size" (p.6).
- **Code availability:** yes, flexBCF "available at https: //github.com/skdeshpande91/flexBCF" (p.5; URL split in PDF).
- *Other lessons:* default bcf package did not scale (p.2 "did not scale to the challenge data"); one-hot encoding of practice ID prevented partial pooling (p.5). Authors note "the Challenge provided insufficient context about the data to probe potential violations" (p.3).
- *Not verified:* organisers' overall results and DGP design (in Thal & Finucane, M01, on fetch list); journal-version differences.

#### Row 4. [c0203] Du M, Johnston S, Coplan PM, Strauss VY, Khalid S, Prieto-Alhambra D, et al. (2025). Causal Forests Versus Inverse Probability of Treatment Weighting to Adjust for Cluster-Level Confounding: A Parametric and Plasmode Simulation Study Based on US Hospital Electronic Health Record Data. Pharmacoepidemiol Drug Saf 34(11):e70257

- **Link, version, peer review:** https://doi.org/10.1002/pds.70257 — version of record (OA) via PMC12583492; peer reviewed.
- **Source text for quotes:** `texts/c0203_PMC12583492.txt` (§ = section).
- **Data source and country:** US PINC AI (Premier) Healthcare Database, hospital EHR (§Plasmode Simulation Data Generation Process: "an all‐payer hospital database collected from among over 1000 hospitals in the US"; "includes information from hospitals' electronic health records").
- **Clinical domain:** surgery / medical devices (pancreatectomy cohort).
- **Sample size:** parametric n = 10,000; plasmode source "9981 patients admitted for pancreatectomy between 2015 and 2019" (§Methods, abstract); "341 unique hospital IDs, with an average of 30 patients per hospital" (§Plasmode…).
- **Treatments:** simulated binary treatment with surgeon/hospital-driven allocation.
- **Outcome type:** binary; true effect "OR = 1.5 in all the scenarios" (§Plasmode…).
- **Estimators:** IPTW vs three grf causal forest variants (standard, with cluster IDs, with external PS) — "Three different Causal Forest approaches were implemented using the grf package in R (version 2.2.0)" (§Implementation of Causal Forests). Causal forest used here to estimate an average (not conditional) effect.
- **Tuning and selection procedure:** none — limitation: "this study did not evaluate the tuning parameters for Causal Forests" because "currently there is limited guidance on tuning Causal Forests in epidemiology research" (§Strengths and Limitations).
- **Validation approach:** parametric + plasmode simulation; plasmode "re‐sampling from pre‐selected observed covariates" with exposure and outcome generated (§Plasmode…) — i.e. generate-treatment type design; only age, sex and Charlson index plus hospital covariates resampled.
- **Known truth available (plasmode or simulation):** yes.
- **Subgroups:** none (scenarios vary cluster size and confounding strength).
- **Main result:** "Under weak to moderate surgeon influence, CF and IPTW performed similarly"; with strong confounding "relative bias averaged 11.2% for CF versus 19.9% for IPTW, with similar advantages observed in plasmode simulations" (§Results, abstract). Negative: "Including the cluster‐ID indicator in Causal Forests resulted in higher bias and empirical standard error in scenarios with fewer but larger clusters" (§Summary).
- **Code availability:** "The study code for the study is available on GitHub. Please email mike.du@ndorms.ox.ac.uk for access" (§Data Availability Statement).
- *Relevance to HTE:* indirect (causal forest as an ATE estimator; no CATE evaluation). Plasmode on EHR covariates.
- *Scope flag (Phase 2 fix):* average-effect plasmode/simulation study only (no CATE or subgroup estimand); its design lessons transfer to heterogeneous-effect plasmodes by argument, not by evidence.
- *Not verified:* Figures S1–S2 (supplement); full results tables.

#### Row 5. [S02] (seed) Wyss R, Schneeweiss S, van der Laan M, Lendle SD, Ju C, Franklin JM (2018). Using Super Learner prediction modeling to improve high-dimensional propensity score estimation. Epidemiology 29(1):96–106

- **Link, version, peer review:** https://doi.org/10.1097/EDE.0000000000000762 — version of record (user-supplied PDF); peer reviewed.
- **Source text for quotes:** `texts/user_wyss2018_epidemiology.txt` (coordinator) and `texts/user_wyss2018_epidemiology_raw.txt` (my reading-order pdftotext; quotes from this). p. = PDF page (journal pp. 96–106).
- **Data source and country:** plasmodes "based on three empirical datasets (NSAID dataset, NOAC dataset, and Statin dataset)" from US healthcare claims databases (p.3); dataset details in eAppendix — UNVERIFIED (not supplied).
- **Clinical domain:** pharmacoepidemiology (NSAIDs, novel oral anticoagulants, statins).
- **Sample size:** simulated cohorts 10,000 (5,000 and 20,000 in variants) (Table, p.4); "We simulated 100 datasets for each scenario" (p.4).
- **Treatments:** observed treatment in each source study (e.g. NSAID class comparison) — kept from the data.
- **Outcome type:** binary simulated outcome; null effect except one scenario with OR = 2.
- **Estimators:** logistic hdPS PS models with 25–500 variables, hdPS + Super Learner, scalable collaborative TMLE (patience 10/50), hdPS + lasso (p.4); effect via PS stratification, matching, IPTW, TMLE.
- **Tuning and selection procedure:** how many hdPS variables to adjust for; Super Learner choosing among hdPS models by cross-validated loss.
- **Validation approach:** "Simulated datasets were created by sampling, with replacement, 10,000 individuals from the original study cohort" and simulating outcomes from a fitted outcome model; "Treated and untreated individuals were sampled disproportionately" to set treatment prevalence (p.4). **Treatment is resampled with covariates (the Sample Treatment design that c0664 and c1716 criticise).**
- **Known truth available (plasmode or simulation):** yes (simulated outcome model).
- **Subgroups:** none; **average effects only** (ATE/ATT) — no HTE.
- **Main result:** "the high-dimensional propensity score can be sensitive to the number of variables included for adjustment" and "severe overfitting of the propensity score model can negatively impact the properties of effect estimates"; "Combining the high-dimensional propensity score with Super Learner was the most consistent strategy" (p.1, abstract). Among fixed hdPS models, HDPS 100 "generally performed best" (p.6).
- **Code availability:** "Software ... is available at https://github.com/lendle/hdps and https://github.com/lendle/ TargetedLearning.jl"; "R code for producing plasmode simulations is available upon request" (p.1).
- *Covariates:* high-dimensional propensity score (hdPS) variables from claims codes, "frequent," "sporadic," and "once" indicators (p.2).
- *My judgement:* relevant to Brief 5 only via high-dimensional code covariates and plasmode design; given the Sample Treatment design, PS-based performance estimates may be distorted (per c0664/c1716) — not re-tested here.
- *Not verified:* eAppendix (datasets, cohort sizes).

#### Row 6. [c0664] c0664: Shaw PA, Gruber S, Williamson BD, Desai R, Shortreed SM, Krakauer C, Nelson JC, van der Laan MJ. A cautionary note for plasmode simulation studies in the setting of causal inference

- **Link, version, peer review:** https://doi.org/10.1002/sim.70676 — **version of record** now read (user-supplied PDF; Stat Med 2026; "Received: 2 December 2025 | Revised: 29 April 2026 | Accepted: 7 July 2026"); peer reviewed. Earlier extraction used arXiv v1 (https://arxiv.org/abs/2504.11740v1).
- **Source text for quotes:** VoR `texts/user_shaw2026_statmed_raw.txt` (my reading-order pdftotext; VoR p. = PDF page of 11) and arXiv `texts/c0664_shaw.txt` (p. = arXiv PDF page). Quotes below marked "arXiv p." are from v1; all were checked to have the same content in the VoR (differences below).
- **Data source and country:** Synthetic scenarios 1–4, plus scenario 5 built on Kaiser Permanente Washington (KPWA) EHR data, USA. p.8: "using a source dataset from the Kaiser Permanente Washington (KPWA) EHR system".
- **Clinical domain:** Mental health in the real-data scenario. p.13: "EHR data for 50,337 individuals 13 years and older initiating antidepressant medication or psychotherapy for treatment of depression".
- **Sample size:** Synthetic n = 100, 1,000 and 10,000; plasmode n = 10,000 drawn from 50,337 (p.9: "For the real-data Scenario 5, n = 10, 000").
- **Treatments:** Antidepressant vs psychotherapy initiation (scenario 5); synthetic binary treatment (scenarios 1–4).
- **Outcome type:** Continuous and binary, including rare binary. Self-harm in KPWA, at 5% and 15% outcome rates (p.14).
- **Estimators:** Unadjusted, propensity score (PS) matching, inverse probability of treatment weighting (IPTW), parametric G-computation (glmCM), PS regression (glmPS), targeted maximum likelihood estimation (TMLE) (p.5). Estimands are the **average treatment effect (ATE)** and relative risk (RR); no conditional or heterogeneous estimand.
- **Tuning and selection procedure:** Not applicable. Working models are fixed as correctly specified (p.5: TMLE "is fit using the correctly specified working models").
- **Validation approach:** Two plasmode frameworks are compared. p.3: the Sample Treatment design will "bootstrap sampling covariates and treatment together, then generating the outcome". The Generate Treatment design resamples covariates and simulates treatment.
- **Known truth available (plasmode or simulation):** Yes, by construction.
- **Subgroups:** None.
- **Main result:** 
- **Code availability:** VoR: "Code used to generate the synthetic (computer-generated) data can be obtained by contacting the first author or by going to the GitHub site https://github.com/PamelaShaw/PlasmodeSimulation/" (VoR p.9); arXiv v1 (p.16): data "not publicly available because they contain detailed information from the electronic health records".
- *VoR vs arXiv v1 — substantive differences (my comparison):* (1) the abstract now limits scope to "the evaluation of methods estimating a point treatment estimand" (VoR p.1) — absent in v1; (2) plasmode wording changed from "synthetic data" to "data from a probabilistic model" (VoR p.1); (3) recommendation now says flexible models "can be used to generate computer-generated treatments and outcomes after re-sampling covariates" (VoR p.8) vs "synthetic treatments" in v1; (4) code now public: "https://github.com/PamelaShaw/PlasmodeSimulation/" (VoR Data Availability Statement, p.9) — v1 had no code link. Numerical results quoted below (IPTW bias:SE "nearly 200 times larger", glm-PS/Match "8 times larger", KPWA n = 50,337, TMLE and coverage findings) are unchanged in the VoR (VoR p.6, p.5, p.7–8). No change to conclusions found. - Sample Treatment induces a positivity violation. p.7: "this positivity violation occurs even when there is no violation in the source population". - p.4: "only the latter approach can be reliably used to evaluate the statistical performance". - Synthetic scenarios, arXiv p.12 / VoR p.6: "The bias:SE of glm-PS and Match is 8 times larger under the Sample Treatment approach". - KPWA scenario, p.14: "TMLE has a larger bias:SE for the Sample Treatment than the Generate Treatment approach". Also p.14: "coverage is near the nominal level for all estimators besides the unadjusted estimator, regardless of plasmode strategy". So in the real-data plasmode the coverage penalty was **not** seen. - Recommendation, p.15: "We recommend avoiding simplistic parametric models for the DGM by flexible modeling or machine learning".
- *Relevance to HTE:* This is indirect. The design lesson (generated vs resampled treatment, positivity) bears on any HTE plasmode. The paper itself evaluates only marginal estimands, and it mentions "potentially heterogeneous treatment effects" only as motivation (p.14).
- *Scope flag (Phase 2 fix):* average-effect (ATE, RR, logcOR) plasmode study only; its lessons transfer to HTE plasmodes by argument, not by evidence.
- *Not verified:* supplementary tables S6–S8.

#### Row 7. [c1716] Karim ME (2026b). A Plasmode Benchmark Can Refute but Cannot Certify: Projection and Regularity in Causal-Inference Simulation

- **Link, version, peer review:** https://arxiv.org/abs/2609.26186v1 — arXiv v1, preprint, not peer reviewed.
- **Source text for quotes:** `texts/c1716_karim_b.txt` (pdftotext; p. = PDF page; copied from Brief 3).
- **Data source and country:** theory plus real-data simulation on the RHC cohort (USA; research cohort, public teaching data) (p.7: "right-heart-catheterization cohort [Connors et al., 1996] (n = 5,735; treatment the receipt of a Swan–Ganz catheter, outcome in-hospital death, 50 baseline covariates)").
- **Clinical domain:** critical care; methods.
- **Sample size:** n = 5,735; J = 1,000 replicates (p.8 "J = 1,000 replicates").
- **Treatments:** RHC (Swan–Ganz catheter) vs none.
- **Outcome type:** binary; estimand "the marginal average treatment effect on the risk-difference scale" (p.2).
- **Estimators:** ten arms — parametric (G-computation, subclassification, IPW, AIPW), flexible "AIPW-SL and TMLE—whose outcome and propensity nuisances come from a super learner", and three diagnostic TMLE variants (p.7); super-learner library includes elastic net, MARS, random forests, BART (p.7).
- **Tuning and selection procedure:** super learner with 5-fold CV (Table 3 caption p.13: "super learner at V = 5-fold cross-validation"); cross-fitting vs in-sample nuisances compared (p.12).
- **Validation approach:** theory of plasmode "regularity" (overlap preserved?) and "projection" (injected outcome model favours matching estimators), with a regular-plasmode algorithm.
- **Known truth available (plasmode or simulation):** yes (standardised truth from the generating mechanism).
- **Subgroups:** none (marginal estimand).
- **Main result:** p.1 "Resampling the real treatment with fine-grained covariates destroys it, and the resulting coverage failure falls on flexible, machine-learning-based estimators" while parametric ones "stay near nominal"; failure "disappears once the treatment is regenerated from a bounded propensity or the covariates are coarsened, and cross-fitting removes only part of it" (p.1). Projection "can reverse estimator rankings even when overlap is intact" (p.1). Under sample-treatment parametric estimators kept coverage "g-computation 0.95, IPW 0.96, and the correctly-specified TMLE with logistic nuisances 0.93" (p.9). Conclusion: "A plasmode is a filter against estimators, not a warrant for them" (p.1); "Treat a plasmode as a way to rule estimators out, never to sign one off" (p.12).
- **Code availability:** p.2 "the software is provided" (Web Appendix); repository URL not found in searched text — UNVERIFIED.
- *Relation to c0664:* p.12 "The two accounts agree on the recommendation and differ on its reach."
- *Scope flag (Phase 2 fix):* average-effect plasmode/simulation study only (no CATE or subgroup estimand); its design lessons transfer to heterogeneous-effect plasmodes by argument, not by evidence.
- *Not verified:* Web Appendices A–B and Web Table S2 (not in the PDF text searched); exact super-learner coverage numbers under sample-treatment.

#### Row 8. [c1728] Karim ME (2026a). When bad adjustment looks good: what goes wrong in Plasmode 0.1.0 simulations

- **Link, version, peer review:** https://arxiv.org/abs/2609.24053v1 — arXiv v1, preprint, not peer reviewed.
- **Source text for quotes:** `texts/c1728_karim_a.txt` (pdftotext; p. = PDF page; copied from Brief 3).
- **Data source and country:** synthetic cohort plus SUPPORT/Right Heart Catheterisation (RHC) cohort (USA, critical care study cohort; not EHR/claims) (p.2: "the SUPPORT/Right Heart Catheterisation cohort of 5,735 complete cases with 32 covariates, simulated at 3,000").
- **Clinical domain:** critical care (cardiovascular procedure, RHC); methods audit.
- **Sample size:** synthetic source 4,000 simulated at 2,000; RHC 5,735 simulated at 3,000 (p.2); 200 replicates per strategy (p.1: "We ran 200 null-effect replicates per strategy").
- **Treatments:** RHC vs none (exposure in the plasmode).
- **Outcome type:** binary (risk difference); continuous-outcome function also tested (p.3).
- **Estimators:** five estimators, two fitted "once correctly and once with half the covariates deliberately omitted" (p.3).
- **Tuning and selection procedure:** not applicable.
- **Validation approach:** software audit of the archived CRAN package Plasmode 0.1.0 (generate-treatment design) under identical seeds, as-supplied vs sorted vs alignment-corrected rows.
- **Known truth available (plasmode or simulation):** yes (null injected effect; p.2 "the true risk difference was zero").
- **Subgroups:** none. Estimand is marginal, not HTE.
- **Main result:** p.1 "A sampled subject usually received another subject's exposure probability"; p.1 "With the unmodified generator, all five appeared similarly unbiased", whereas after correction "deliberately misspecified estimators retained risk-difference biases of 0.10–0.11" (p.1). Source-model AUC "was 0.503 before and 0.841 after alignment" (p.1). Implication: a buggy plasmode implementation can certify misspecified adjustment.
- **Code availability:** yes — p.6 "available in the companion repository plasmode-assess-code at https://github.com/ehsanx/plasmode-assess-code" (URL split by line break in PDF).
- *Scope flag (Phase 2 fix):* average-effect plasmode/simulation study only (no CATE or subgroup estimand); its design lessons transfer to heterogeneous-effect plasmodes by argument, not by evidence.
- *Not verified:* whether the package has since been fixed; any later version of the preprint.

#### Row 9. [c1229] Portela GT, Gibbons JB, Schneeweiss S, Desai RJ (2025). Assessment of the conditional exchangeability assumption in causal machine learning models: a simulation study

- **Link, version, peer review:** https://arxiv.org/abs/2510.26700v1 — arXiv v1 preprint. Semantic Scholar metadata lists the venue as AJE Advances: Research in Epidemiology (metadata, not a quote); journal version not seen — peer-review status of the read version: preprint.
- **Source text for quotes:** `texts/c1229_arxiv2510.26700v1.txt` (pdftotext; p. = PDF page).
- **Data source and country:** fully synthetic (not resampled real data), framed for routine data (p.4: "developing causal ML models using routinely collected observational data, such as electronic health records or insurance claims data"); Brigham and Women's pharmacoepidemiology group, USA.
- **Clinical domain:** pharmacoepidemiology (generic).
- **Sample size:** p.8 "13 ‘measured’ covariates (C1-C13) and 1 ‘unmeasured’ covariate (U) in a population of 20,000 observations"; also 5,000 (p.9 "we decreased the overall sample size from 20,000 to 5,000"); "Each scenario was replicated 500 times" (p.9).
- **Treatments:** synthetic binary.
- **Outcome type:** binary primary outcome plus binary negative control outcome (NCO).
- **Estimators:** oracle model, causal forest (grf) and X-learner (LASSO base learners): p.9–10 "constructed with 4,000 trees"; "We used the ‘causal_forest’ function in the grf package"; X-learner with "LASSO with 10-fold cross-validation as the base learner" (p.10).
- **Tuning and selection procedure:** causal forest parameters "tuned these parameters to minimize out-of-bag prediction error" (p.10).
- **Validation approach:** NCOs as diagnostic for subgroup-specific unmeasured confounding, comparing ITE-defined strata effects on outcome and NCO.
- **Known truth available (plasmode or simulation):** yes (synthetic; HTE via three treatment–covariate interactions, p.9 "β11 = -0.30, β12 = -0.10, and β13 = -0.05").
- **Subgroups:** ITE-defined strata.
- **Main result:** p.2 "causal forest and X-learner models failed to recover true treatment effect heterogeneity and, in some cases, falsely indicated heterogeneity when there was none"; "NCOs successfully identified subgroups affected by unmeasured confounding" though "not always pinpointing the subgroup with the largest confounding" (p.2). p.12: "broad misestimation and spurious harm signals from both learners with confounding, remained largely unchanged when using a smaller sample size". Conclusion p.2: violations "substantially limit the validity of ITE estimates from causal ML models in routinely collected observational data".
- **Code availability:** not found in text searched — UNVERIFIED.
- *Not verified:* journal version; Tables 1–3 numeric values.

#### Row 10. [c1640] Noroozizadeh S, Shen X, Weiss JC, Chen GH (2026). SurvHTE-Bench: a benchmark for heterogeneous treatment effect estimation in survival analysis. ICLR 2026

- **Link, version, peer review:** https://arxiv.org/abs/2603.05483v1 — arXiv v1; PDF header "Published as a conference paper at ICLR 2026" (p.1); peer reviewed (conference). Four authors per PDF header.
- **Source text for quotes:** `texts/c1640_arxiv2603.05483v1.txt` (pdftotext; p. = PDF page).
- **Data source and country:** synthetic (40 datasets), semi-synthetic with real covariates from the ACTG 175 HIV trial and MIMIC-IV ICU EHR (US), real Twins and ACTG data (p.5: "pairing real covariates (ACTG HIV trial, MIMIC-IV ICU records) with simulated treatments and outcomes"); MIMIC variants "Derived from 36 covariates in the MIMIC-IV ICU database" (p.8).
- **Clinical domain:** cross-domain survival (critical care via MIMIC; HIV via ACTG).
- **Sample size:** per-dataset n not extracted (Appendix G); 10 repeats.
- **Treatments:** simulated binary treatment; time-to-event, estimand RMST CATE (p.3: "target estimand is RMST up to a user-specified time horizon").
- **Outcome type:** see treatments
- **Estimators:** "53 variants" in three families: outcome-imputation (S/T/X/DR-learners, Double-ML, causal forest with pseudo-obs, Margin, IPCW-T imputations), direct-survival (causal survival forests, SurvITE), survival meta-learners (p.5).
- **Tuning and selection procedure:** family-level comparison selects "the best variant per family ... on validation data" (p.6); hyperparameters in Appendix E (not read).
- **Validation approach:** known-truth CATE RMSE, ATE bias, Borda-count ranks across datasets (p.5).
- **Known truth available (plasmode or simulation):** yes (synthetic, semi-synthetic, Twins); no (ACTG real).
- **Subgroups:** not applicable (CATE functions); assumption-violation configurations (unobserved confounding, no positivity, informative censoring).
- **Main result:** "no single method dominates: performance depends on causal assumptions, censoring, and survival dynamics" (p.2); family ranking "S-Learner-Survival (average rank 3.30 across 11 method families) and Matching-Survival (3.48) maintain their advantage, followed by Double-ML (3.98) and Causal Survival Forests (5.10)" (p.7). Failure result: in one high-censoring scenario "almost all estimators failed under all different causal configurations" (p.8). Semi-synthetic: "survival-oriented methods like SurvITE and survival meta-learners provide robust performance in highly censored EHR-like regimes (MIMIC)" (p.9). My observation (Table 3, p.9): MIMIC CATE RMSEs are tightly clustered across all families (about 7.89–8.01), so the semi-synthetic EHR data discriminate weakly between methods. Real ACTG: "As ground truth is unknown, we cannot determine which approach is more accurate" (p.10).
- **Code availability:** "https://github.com/Shahriarnz14/SurvHTE-Bench" (p.1).
- *Not verified:* Appendices C–I; MIMIC cohort definition and sample size.

#### Row 11. [c1122] Doutreligne M, Varoquaux G (2025). How to select predictive models for decision-making or causal inference. GigaScience 14:giaf016

- **Link, version, peer review:** https://doi.org/10.1093/gigascience/giaf016 — version of record via PMC11927402 (E-utilities JATS); peer reviewed. arXiv preprint 2302.00370v2 also saved.
- **Source text for quotes:** `texts/c1122_doutreligne_giga.txt` (PMC; § = section; LaTeX residue in formula spans), `texts/c1122_doutreligne_arxiv.txt`.
- **Data source and country:** Caussim simulation plus 3 semi-simulated datasets "adding a known synthetic causal effect to a real—nonsynthetic—health care covariate" (§Results/abstract area: "3 health care datasets based on real covariates"). ACIC 2016 on the Collaborative Perinatal Project (an RCT cohort; §Datasets "a randomized controlled trial studying infants’ developmental disorders containing 4,802 indivduals and 55 features"); ACIC 2018 on the "Linked Births and Infant Deaths Database (LBIDD)" (§Datasets) — a US vital-statistics registry, i.e. routinely collected covariates; Twins (US births).
- **Clinical domain:** perinatal/infant (covariates); method is domain-agnostic.
- **Sample size:** ACIC 2016: 4,802 individuals, "770 dataset instances" (§Datasets); others per Appendix A.7 (not extracted).
- **Treatments:** synthetic binary treatment, synthetic outcomes.
- **Outcome type:** see treatments
- **Estimators:** G-computation outcome models; semi-simulated family "gradient boosting trees for both the response surfaces and the treatment" (§Family of candidate estimators).
- **Tuning and selection procedure:** feasible risks (μ-risk = factual MSE, IPW-weighted μ-risk, τ-risk variants, U-risk, R-risk) compared with the oracle τ-risk by relative Kendall tau; nuisances via "a stacked estimator of ridge and boosting classifiers" (§Nuisance estimators).
- **Validation approach:** agreement of selection risk with oracle ranking (known truth).
- **Known truth available (plasmode or simulation):** yes (simulated/semi-simulated effects).
- **Subgroups:** stratified by overlap level, not clinical subgroups.
- **Main result:** "the mean squared error, classically used to evaluate predictive modes, is worse" and "Reweighting it with a propensity score does not bring much improvement in most cases" (§Results, abstract); R-risk "leads to the best performances" and "Nuisance corrections are best estimated with flexible estimators such as a super learner" (§Results, abstract). Negative/limiting: "Model selection for causal inference becomes more and more difficult with increasingly differently treated and control populations" (§Model selection is harder for low population overlap). Practical: "the best split is 90 %/10 %" (§Nuisances can be estimated on the same data as outcome models). Stacked nuisances help except where truth is linear: "For the Twins dataset, there is no improvement for stacked" (Supplementary Fig. S12 legend).
- **Code availability:** GitHub referenced ("available in the readme of the data section of our GitHub [61]"); Twins on Zenodo (§availability section). URL not extracted.
- *Relevance:* the only selection study in this set using registry-derived covariates (LBIDD); no EHR/claims dataset.
- *Not verified:* Appendix A.7/A.8 (supplementary); LBIDD sample sizes.

#### Row 12. [M04] Mahajan D, Mitliagkas I, Neal B, Syrgkanis V (2024). Empirical analysis of model selection for heterogeneous causal effect estimation. ICLR 2024

- **Link, version, peer review:** https://arxiv.org/abs/2211.01939v3 — PDF header "Published as a conference paper at ICLR 2024" (p.1); peer reviewed (camera-ready on arXiv).
- **Source text for quotes:** `texts/M04_mahajan.txt` (pdftotext; p. = PDF page; copied from Brief 3).
- **Data source and country:** semi-synthetic, not EHR/claims/registry: p.7 "75 datasets from the ACIC 2016 competition" (covariates from the Collaborative Perinatal Project, per c1122) plus "LaLonde PSID, LaLonde CPS (LaLonde, 1986), and Twins (Louizos et al., 2017), using RealCause" (p.7). Routinely collected covariates: none (Twins = US birth records, arguably registry).
- **Clinical domain:** none specific (perinatal and labour-economics covariates).
- **Sample size:** "78 datasets over 20 random seeds" (p.7); per-dataset n not extracted.
- **Treatments:** binary treatment; continuous/binary outcomes with known CATE.
- **Outcome type:** see treatments
- **Estimators:** "415 CATE estimators" (p.2) from "7 different types of meta-learners" (p.7).
- **Tuning and selection procedure:** "34 surrogate metrics" (p.2); nuisances tuned by AutoML: "we use AutoML, specifically FLAML (Wang et al., 2021) to select the best-performing nuisance model class as well as its hyperparameters" (p.4); proposed two-level selection (within meta-learner class, then across).
- **Validation approach:** Normalized-PEHE of the selected estimator vs oracle best (p.7).
- **Known truth available (plasmode or simulation):** yes.
- **Subgroups:** none.
- **Main result:** "Doubly Robust and TMLE variants are globally dominating metrics" (p.7); "plug-in metrics based on T-Learner are never dominated by other metrics across all datasets" (p.2). Negative findings (Table 1, p.8, single-level): R Score Normalized PEHE 4.0 on ACIC 2016 vs 0.56 for DR T Score and T Score; Qini DR T Score 2.08e+7 on Twins. Two-level strategy: "better performance in approximately 28.7% cases over all datasets and metrics" and "in no scenario it happens that this strategy gets dominated" (p.8); Qini DR score "was among the worst metrics with the single-level strategy for the TWINS dataset" but dominated with two-level selection (p.9). "metrics with the T-Learner strategy are better than those with S-Learner strategy in all the cases" (p.8).
- **Code availability:** "The code repository can be accessed here: github.com/divyat09/cate-estimator-selection" (p.2 footnote).
- *Contested with c1122:* R-risk was best in Doutreligne & Varoquaux; R Score poor here (different candidate families and nuisance tuning).
- *Not verified:* Appendix D full tables (Tables 7–8) not read.

#### Row 13. [c0342] Wang T, Keil AP, Kim S, Wyss R, Htoo PT, Jonsson Funk M, Buse JB, Kosorok MR, Stürmer T (2024; online 2023). Iterative causal forest: a novel algorithm for subgroup identification. Am J Epidemiol 193(5):764–776

- **Link, version, peer review:** https://doi.org/10.1093/aje/kwad219 — version of record (user-supplied PDF; "Advance Access publication: November 7, 2023"); peer reviewed.
- **Source text for quotes:** `texts/user_wang2024_icf_aje.txt` (coordinator, -layout) and `texts/user_wang2024_icf_aje_raw.txt` (my reading-order pdftotext; quotes from this); p. = PDF page.
- **Data source and country:** simulation (synthetic, Setoguchi-type design) + "a 20% random sample of all fee-for-service US Medicare beneficiaries" 2012–2017 (p.7).
- **Clinical domain:** cardiovascular outcome (hospitalised HF) in SGLT2i vs GLP-1 RA initiators — methods contribution.
- **Sample size:** simulation "n = 20,000 (simulations were repeated for n = 10,000 and 5,000, separately)" (p.5), 500 replicates (p.9); Medicare cohort size in text not extracted — UNVERIFIED.
- **Treatments:** SGLT2i vs GLP-1 RA (application); synthetic binary W (simulation).
- **Outcome type:** simulation continuous; application binary HHF (risk difference, IPTW + IPCW).
- **Estimators:** iCF vs interaction tree (IT), LASSO interactions, FindIt, ROWSi, one causal forest (oneCF) (p.5).
- **Tuning and selection procedure:** cross-validated subgroup decision that "best predicts the treatment effect" (transformed outcome) after plurality votes across depths (p.1).
- **Validation approach:** known-truth simulation with "12 scenarios: no HTEs (scenario 1) and, 2-way, two 2-way, 3-way, 4-way, and 5-way interactions" (p.5), 4 normal + 6 binary synthetic covariates — **not** built on claims covariates.
- **Known truth available (plasmode or simulation):** yes (simulation only).
- **Subgroups:** discovered subgroups (e.g. HF/edema, CVD, age).
- **Main result:** "the iCF and oneCF both outperformed other methods, except for IT, in most scenarios"; "IT had both the highest specificity and highest sensitivity, followed by the iCF and oneCF" (p.9) — i.e. the simple interaction tree beat iCF on interaction identification. iCF beat IT "for two 2-way interactions or interactions involving ordinal X2" but "IT outperformed the iCF for 2-way interactions or interactions involving continuous X2"; "The iCF may have split on the correct variable but often found the wrong splitting value" (p.9). Authors: "As no method outperforms all others in every scenario, we recommend sensitivity analyses using other methods" (p.10). Medicare: largest-CATE subgroup "adjusted RD = –3.92%, 95% confidence interval: −5.98%, −1.87%" (p.9); iCF "did not identify the largest CATE subgroup with a history of heart failure but no CVD" reported earlier (p.10).
- **Code availability:** "R codes for the iCF and simulations are available at" https://github.com/tianshengwang/iCF (Data availability).
- *Not verified:* Web Tables 1–6; Medicare cohort numbers.

#### Row 14. [c0515] Anoke SC, Normand S-L, Zigler CM (2019). Approaches to treatment effect heterogeneity in the presence of confounding. Stat Med 38(15):2797–2815

- **Link, version, peer review:** https://doi.org/10.1002/sim.8143 — author manuscript via PMC6613382; peer reviewed.
- **Source text for quotes:** `texts/c0515_PMC6613382.txt` (§ = section).
- **Data source and country:** simulation (synthetic, not resampled) plus Medicare inpatient data, USA (§Data Structure: "inpatient data on 38 covariates were generated by 54 099 Medicare beneficiaries hospitalized in the continental United States in 2008").
- **Clinical domain:** cardiovascular (stents after AMI).
- **Sample size:** simulation n = 1,500 × 1,000 iterations (§Data Structure and Analysis); Medicare 54,099.
- **Treatments:** drug-eluting (DES) vs bare-metal stents (BMS).
- **Outcome type:** simulation continuous; application binary two-year revascularisation (risk difference).
- **Estimators:** BART (outcome model), generalized boosted models (GBM, propensity), facilitating score (FS, joint), each followed by regression trees to characterise subgroups (§Treatment effect modeling approaches).
- **Tuning and selection procedure:** analyst-chosen partition (deciles in simulation; 500 quantiles in Medicare) — results depend on it: "When the initial partition is too coarse, the resulting subgroups are still heterogeneous" leading "to biased treatment effect estimates" (§CONCLUSIONS).
- **Validation approach:** simulation with eight true subgroups ("the subgroup-specific ATEs are 1, 2, 5, 5, 6, 6, 9, and 10"), scenarios A–D* varying confounding/effect-modifier structure.
- **Known truth available (plasmode or simulation):** yes in simulation (not built on Medicare covariates); none in Medicare.
- **Subgroups:** discovered (exploratory) subgroups.
- **Main result:** BART "proved most promising in the simulation studies" (§Results, Medicare); GBM "is not able to detect effect modifiers that are not associated with treatment" (§CONCLUSIONS) but "is able to alert the analyst to positivity violations", whereas BART "does not require observations in both treatment arms to calculate the subgroup ATE so positivity violations may go unnoticed" (§CONCLUSIONS). Medicare: "None of the estimation methods were able to estimate 500 subgroups"; for BART "several hundreds of patients with the same estimated ITE" (§Results, Medicare).
- **Code availability:** simulation scripts "openly available on GitHub at https://github.com/sanoke/approachesTEH".
- *Not verified:* supplementary Appendix 2; Medicare covariate-level findings.

#### Row 15. [c0838] Lavery JA, Chen Y, Panageas KS, Wang Y (2025). Unveiling non–small cell lung cancer treatment effect heterogeneity: a comparative analysis of statistical methods. J Natl Cancer Inst 117(10):2062–2072

- **Link, version, peer review:** https://doi.org/10.1093/jnci/djaf176 — version of record (user-supplied PDF; "Advance Access Publication Date: July 10, 2025"); peer reviewed. First author's initials garbled in the PDF text (shown as MS1,2); Crossref lists the first author as Lavery.
- **Source text for quotes:** `texts/user_lavery2025_jnci.txt` (coordinator) and `texts/user_lavery2025_jnci_raw.txt` (my reading-order pdftotext; quotes from this); p. = PDF page.
- **Data source and country:** AACR Project GENIE BioPharma Collaborative (BPC) real-world clinico-genomic registry data plus MSKCC institutional data, USA (p.1: "using the American Association for Cancer Research Project Genomics Evidence Neoplasia Exchange BioPharma Collaborative dataset supplemented with institutional data"). Curated registry-type data (routinely collected records abstracted to a common model).
- **Clinical domain:** oncology (advanced NSCLC).
- **Sample size:** "There were 535 patients treated with immunotherapy alone (57%) or chemoimmunotherapy (43%)" (p.3).
- **Treatments:** immunotherapy alone vs chemoimmunotherapy (first line).
- **Outcome type:** time-to-event (PFS; OS), right-censored ("42% were censored" for PFS, p.3).
- **Estimators:** Cox with interactions, accelerated failure time model, finite mixture model (latent subgroups), causal survival forest (CSF estimating "the difference in the survival probability at 1 year", p.3).
- **Tuning and selection procedure:** mixture-model number of subgroups by BIC ("requiring a decrease of 6 or more in the BIC", p.3); CSF settings not extracted — UNVERIFIED (Supplementary Methods).
- **Validation approach:** simulation (settings A–E, varying effect direction/magnitude, PD-L1–subgroup link, censoring, sample size; Table 1) — parametric synthetic DGP, not resampled from GENIE (my reading of Table 1).
- **Known truth available (plasmode or simulation):** yes (simulation).
- **Subgroups:** PD-L1, tumour mutation burden (TMB), stage; latent subgroups.
- **Main result:** real data: mixture model found 2 latent subgroups with ratio of treatment effects "1.62 (95% CI ¼ 1.02 to 2.57)" (p.1; the PDF encodes = as ¼); CSF ranked TMB 1st and PD-L1 3rd in variable importance; "the accelerated failure time and Cox proportional hazards models did not detect any statistically significant heterogeneous treatment effects" (p.1). Null for OS: "None of the methods detected heterogeneity associ­ ated with PD-L1, tumor mutation burden, or cancer stage for the overall survival endpoint" (p.4). Simulation: with latent subgroups "the mixture model detected heterogeneous treatment effects more frequently than the accel­ erated failure time, causal survival forest, and Cox models" when samples were small (p.4); under no heterogeneity, false detection "4.9% (accelerated failure time), 5.1% (finite mixture model), 5.6% (causal survival forest), and 5.7% (Cox)" (p.5) — type I error near nominal for all.
- **Code availability:** GENIE BPC data public via Synapse/cBioPortal (p.9); simulation code on GitHub at https://github.com/jalavery/jnci_unveiling_hetero[…] (URL split across lines in the PDF; p.9).
- *Limitation stated:* Cox, AFT and mixture models "do not adequately handle a large number of covariates" (p.6).
- *Not verified:* Supplementary Methods, Tables S2–S3, Figures S1–S4.

#### Row 16. [c1084] Xia Y, Sadatsafavi M, Gustafson P (2026; online 2025). Evaluating treatment benefit predictors using observational data: contending with identification and confounding bias. Am J Epidemiol 195(4):1056–1062 (doi 10.1093/aje/kwaf239)

- **Link, version, peer review:** https://doi.org/10.1093/aje/kwaf239 — version of record (open access) via PMC13066335; peer reviewed. arXiv 2407.05585v4 exists (not read).
- **Source text for quotes:** `texts/c1084_PMC13066335.txt` (JATS; § = section; much LaTeX residue in formula spans — quotes taken from prose only).
- **Data source and country:** none — conceptual/identification paper with synthetic target populations (Canada-based authors). Motivating example uses primary-care variables: "These variables are often available in routine primary care and can be used to make treatment decisions" (§Example: lung function measure).
- **Clinical domain:** respiratory (illustration: bronchodilator benefit on FEV1).
- **Sample size:** not applicable (population-level synthetic distributions).
- **Treatments:** bronchodilator (illustrative).
- **Outcome type:** continuous FEV1 improvement (plus a continuous-covariate example in Appendix S4).
- **Estimators:** none fitted; four prespecified treatment benefit predictors (TBPs) of a linear-interaction form are evaluated (§Synthetic target populations).
- **Tuning and selection procedure:** not applicable.
- **Validation approach:** identification of discrimination (concentration of benefit index, C_b) and moderate calibration estimands from observational data; quantification of confounding bias in these metrics; sensitivity parameters proposed (§Discussion: they "serve as sensitivity parameters, allowing us to partially recover the performance metrics").
- **Known truth available (plasmode or simulation):** yes (analytic synthetic populations).
- **Subgroups:** none.
- **Main result:** identification shown "by re-expressing the respective estimands in terms of the distribution of observable data only" (§Abstract); "in the absence of full confounding control, bias propagates in a more complex manner than when targeting more commonly encountered estimands" and "general intuition about the direction of bias in causal effect estimates does not hold in the present context" (§Abstract). Negative example: a TBP developed "without controlling for confounder Z during development and evaluation, can falsely suggest moderate calibration" (§Results).
- **Code availability:** not stated in the text searched — UNVERIFIED.
- *Not verified:* Appendices S1–S4 (supplementary).

### B. Selection, tuning, benchmarking or validation on routinely collected data without a known truth

#### Row 17. [c1676] Ling Y, Upadhyaya P, Chen L, Jiang X, Kim Y (2022; arXiv 2021). Heterogeneous treatment effect estimation using machine learning for healthcare application: tutorial and benchmark. J Biomed Inform 2022:104256

- **Link, version, peer review:** https://arxiv.org/abs/2109.12769v5 — arXiv v5 (arXiv journal_ref field: Journal of Biomedical Informatics (2022): 104256); peer-reviewed journal version not compared. Authors confirmed from PDF header. **Duplicate note:** the v5 PDF title is "Emulate Randomized Clinical Trials using Heterogeneous Treatment Effect Estimation for Personalized Treatments: Methodology Review and Benchmark" — the same work as screening record c0396 (J Biomed Inform 2023, "Emulate randomized clinical trials using heterogeneous treatment effect estimation for personalized treatments: Methodology review and benchmark"); the arXiv journal_ref year (2022) and the PubMed year (2023) differ — resolve at write-up; c0396 should be merged into this row.
- **Source text for quotes:** `texts/c1676_arxiv2109.12769v5.txt` (pdftotext; p. = PDF page).
- **Data source and country:** Optum Clinformatics Data Mart, US claims (p.19 "administrative health claims from Jan 2007 to June 2020 for commercial and Medicare Advantage health plan members").
- **Clinical domain:** pharmacoepidemiology (drug repurposing; respiratory drugs → Alzheimer disease).
- **Sample size:** "the final cohort size was 11,285" (2,740 treated, 8,545 controls); split "randomly by 6:2:2" (p.19).
- **Treatments:** leukotriene receptor antagonists (e.g. montelukast) vs other anti-asthma drug classes, emulating NCT03991988 (p.19).
- **Outcome type:** binary AD/ADRD onset ("detected as having either an ADRD diagnosis code or medication", p.20).
- **Estimators:** S-, T-, X-, R-learners (logistic, RF, XGBoost bases), DML, CFRNet, DR-learner (neural), DragonNet, generalized random forest (Table 3, p.21–23).
- **Tuning and selection procedure:** model comparison by two label-free metrics: robustness "“estimated” root mean squared error (ERMSE)" between train/test fits (p.14) and influence-function PEHE (IF-PEHE) (p.14, p.20); PS by random forest (p.20).
- **Validation approach:** no known truth — p.14 "the ground-truth treatment effect is never observed in data; randomized experiments are the only method to obtain the ground truth".
- **Known truth available (plasmode or simulation):** no (despite "benchmark" label).
- **Subgroups:** SHAP feature importance on best model (age; bone/joint disorders) (p.23).
- **Main result:** "S-learner with the Random Forest as the base learner gave the best HTE estimation in both metrics" (p.20) — S-learner RF ERMSE 0.0029, IF-PEHE 9.82 vs R-learner XGBoost 0.5873 / 385.34 (Table 3). Representation-learning methods "had a low ERMSE and high IF-PEHE generally" (p.20). My judgement: the winning S-learner shrinks effects towards zero, which a stability metric rewards; no external truth confirms accuracy.
- **Code availability:** no project repository found in text (only package references) — UNVERIFIED.
- *Covariates:* "the 242 diagnosis codes and three demographics" (p.20; ICD → PheWas codes).
- *Not verified:* supplementary S.2.3–S.2.4; journal version.

#### Row 18. [c0044] Wang T, Pate V, Wyss R, Buse JB, Kosorok MR, Stürmer T (2025; online 2024). High-dimensional iterative causal forest (hdiCF) for subgroup identification using health care claims data. Am J Epidemiol 194(7):2085–2097

- **Link, version, peer review:** https://doi.org/10.1093/aje/kwae322 — version of record (user-supplied PDF; "Advance access publication date September 5, 2024"); peer reviewed.
- **Source text for quotes:** `texts/user_wang2024_hdicf_aje.txt` (coordinator pdftotext -layout; columns interleaved) and `texts/user_wang2024_hdicf_aje_raw.txt` (my pdftotext in reading order, used for column-spanning quotes); p. = PDF page (journal pp. 2085–2097).
- **Data source and country:** "a 20% random sample of fee-for-service Medicare beneficiaries" (p.1), USA, 2016–2019.
- **Clinical domain:** cardiovascular outcome (hospitalised heart failure, HHF) in T2D drug initiators — included as a **methods contribution** (high-dimensional claims codes), not as a T2D drug comparison.
- **Sample size:** "Our cohort included 8075 SGLT2i initiators and 7313 GLP1RA initiators" (p.8).
- **Treatments:** SGLT2i vs GLP-1 RA.
- **Outcome type:** binary 2-year HHF risk (risk difference), initial-treatment analysis (p.5).
- **Estimators:** hdPS-style feature generation + PS trimming + iterative causal forest (iCF, c0342): causal forests grown at depths 2–5 "with 1000 trees and 100 iterations", plurality vote for the most stable tree per depth (p.5; Figure 2).
- **Tuning and selection procedure:** depth/subgroup decision chosen by "5-fold cross-validation" on transformed-outcome prediction error — "subgroup decisions from D5 CF had the smallest prediction error (0.190) and were selected" (p.5); top 5% variables by importance; sensitivity analyses over n, c, m, S parameters (Figure 1 caption: "n = 50, 100, 200; c = 0.01, 0.02, 0.05; m = 15, 20, 25; S = 0.01, 0.05, 0.1"); mean stability of voted trees reported (p.5).
- **Validation approach:** none against truth — **no simulation** in this paper; plausibility against prior trial evidence ("consistent with studies suggesting SGLT2i to be more beneficial for patients with preexisting heart failure or chronic kidney disease", p.1). Screening tier T1 should be **downgraded**: this is selection/tuning on routine data without a known truth.
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** data-driven: ≥2 loop diuretic fills (aRD −2.6%, 95% CI −5.0% to −0.2%) in primary analysis; CKD (aRD −1.8%, 95% CI −3.6% to 0.1%) in sensitivity analyses (p.5; Table 2 p.8). Overall IPTW RD −0.4 (−1.1 to 0.2) (Table 2).
- **Main result:** splits were proxies: "The hdiCF did not identify the subpopulation with HF as the largest CATE" (p.7); high-dimensional splitters "might not have meaningful clinical interpretation as they are likely proxies" (p.7); relies on "no unmeasured confounding" overall and within subgroups; authors state "additional empirical studies are required to evaluate the performance of hdiCF in diverse settings where prior knowledge of HTEs is available" (p.9) and "we did not compare hdiCF to other ML subgrouping methods" (p.9).
- **Code availability:** "R codes for hdiCF are available at https://github.com/tianshengwang/" (URL continues on next line in PDF; Data availability, p.10); Medicare data not shareable.
- *Covariates (high-dimensional codes):* ICD-10-CM, CPT and ATC codes from in/outpatient claims; "the n = 200 most prevalent codes in each dimension requiring prevalence greater than 1%" turned into ordinal frequency variables (p.5; p.2).
- *Not verified:* Supplementary Tables S1–S5 and Appendix S1; exact page of the Discussion quotes (two-column interleaving).

#### Row 19. [c1530] Shen L, Visser E, de Wilt H, Verheul H, van Erning F, Geleijnse G, Kaptein M (2020). Estimating the effect of adjuvant chemo-therapy for colon-cancer using registry data: a method comparison and validation. Research Square preprint

- **Link, version, peer review:** https://doi.org/10.21203/rs.3.rs-19661/v1 — Research Square preprint v1 ("Posted Date: April 27th, 2020"), not peer reviewed (user-supplied PDF). No journal version found.
- **Source text for quotes:** `texts/user_shen2020_researchsquare.txt` (coordinator's extraction) and `texts/user_shen2020_researchsquare_nolinenum.txt` (same with manuscript line numbers stripped; quotes taken from this). p. = PDF page (PDF p.2 = manuscript page 1).
- **Data source and country:** Netherlands Cancer Registry (NCR), the Netherlands, vs published results of the QUASAR RCT (UK) — "we did not have access to the patient-level data of the QUASAR trial" and used published estimates (p.6).
- **Clinical domain:** oncology (stage II/III colon cancer).
- **Sample size:** NCR "N = 52621" colon cancer patients; after QUASAR criteria 45,442 (2-year) and 34,832 (5-year follow-up) (p.12); subsample matched to QUASAR covariate distribution (n = 7,704 per Table 3; QUASAR N = 3,239).
- **Treatments:** adjuvant chemotherapy vs none.
- **Outcome type:** binary survival at 2 and 5 years (ATE as risk difference).
- **Estimators:** crude, direct (logistic regression; BART), IPW (lasso logistic; BART), doubly robust combinations, BART with PS covariate (Table 2) — "BART (IPW/BART) with default setting"; weights trimmed "at 0.1 and 0.9" (p.10).
- **Tuning and selection procedure:** defaults for BART; lasso for logistic; covariate-set choice (3, 5, 13, all) explored (p.13).
- **Validation approach:** benchmark against a trial: NCR subsampled to QUASAR covariate distribution (stage, sex, age strata), then compared with the RCT ATE (p.12–13).
- **Known truth available (plasmode or simulation):** no (trial estimate as reference, at ATE level).
- **Subgroups:** stage II vs III; high-risk stage II (e.g. pT4).
- **Main result:** RCT 2-year ATE "-0.021 (95% CI -0.039, -0.001)" vs crude NCR "-0.069 (95% CI -0.076, -0.062)" (p.13); "methods that can flexibly model the response (i.e., direct estimation and DR estimation) performed consistently superior to the inverse propensity score method" (p.2). **Negative / contested:** "the methods using the least covariates are the closest to the ground truth of RCT" while more covariates "substantially overestimate the ATE" (p.13); simple models "do not properly identify heterogeneous treatment effects in stage II colon cancer" (p.2); the trade-off: closeness to the RCT comes "at the cost of inability to identify the heterogeneity among the population" (p.15). HTE is **not** validated against the trial because "no pathological information was provided in the RCT to identify the heterogeneous treatment effect" (p.15).
- **Code availability:** not stated; data "available from IKNL and CBS but restrictions apply" (p.17).
- *My judgement:* this is an ATE benchmark with an aggregate trial; it cannot validate subgroup or individual effects; the conclusion that registry data support "(individual) treatment effects" (p.2) goes beyond the evidence.
- *Not verified:* Figures 3–5 values; sensitivity-analysis details.

#### Row 20. [c0489] Dahabreh, Robertson (2020). Statistical Methods to Measure Treatment Effect Using Observational Data Versus Randomized Trials. PCORI Final Research Report (doi 10.25302/06.2020.ME.130603758)

- **Link, version, peer review:** https://doi.org/10.25302/06.2020.ME.130603758 — **abstract only (pasted by the user from the report PDF)**; PCORI final research report (PCORI peer review of final reports; not a journal article). Author initials not verified (PubMed lists the surnames Dahabreh and Robertson).
- **Source text for quotes:** `texts/user_dahabreh2020_pcori_abstract.txt` (report §2 Abstract; ligatures restored by the user; no page numbers — quotes located by abstract heading).
- **Data source and country:** "a randomized controlled trial database and various sources of routinely collected data (claims, electronic health records, registries)" (§Methods); specific databases and country UNVERIFIED (USA presumed, not stated in abstract).
- **Clinical domain:** UNVERIFIED (not stated in abstract; CASS in ch. 7 suggests cardiovascular — table of contents only).
- **Sample size:** UNVERIFIED.
- **Treatments:** UNVERIFIED (trials emulated not named in abstract).
- **Outcome type:** UNVERIFIED.
- **Estimators:** simulation compared "inverse probability weighting, outcome regression-based, and doubly robust estimators" (§Results).
- **Tuning and selection procedure:** UNVERIFIED.
- **Validation approach:** emulation of trials with routinely collected data compared against "randomized trials and background knowledge" for marginal effects and heterogeneity (§Objectives); simulation studies (§Methods).
- **Known truth available (plasmode or simulation):** yes in the simulation (per abstract: "In simulation studies, we confirm the theoretical predictions"); none in the emulations.
- **Subgroups:** "Our approach to the assessment of heterogeneity has focused on the assessment of treatment effect variation over baseline risk scores" (§Limitations) — i.e. risk-score strata only.
- **Main result:** estimators "are nearly unbiased, even in fairly small sample sizes"; doubly robust estimators have variance "often substantially smaller than inverse probability weighting estimators" under correct specification (§Results). Emulations: "Good agreement between observational analyses designed to emulate randomized controlled trials and completed randomized studies" (§Conclusions). Limitations stated: risk-score heterogeneity assessments "do not capture all relevant dimensions of treatment effect variation"; emulations "focused on intention-to-treat causal contrasts" (§Limitations). Which trials, how close agreement was, and whether heterogeneity (as opposed to marginal effects) agreed: UNVERIFIED.
- **Code availability:** UNVERIFIED.
- *Structure from the table of contents only (not findings):* chapter 6, on heterogeneity, covers randomised trials only; chapter 7 contains the simulation study and a re-analysis of the Coronary Artery Surgery Study (CASS). Content of these chapters UNVERIFIED.

#### Row 21. [c1776] Baptiste PJ, Wong AYS, Schultze A, Clase CM, Leyrat C, Williamson E, Powell E, Mann JFE, Cunnington M, Teo K, Bangdiwala SI, Gao P, Wing K, Tomlinson L (2024). Effectiveness and risk of ARB and ACEi among different ethnic groups in England: a reference trial (ONTARGET) emulation analysis using UK Clinical Practice Research Datalink Aurum data. PLoS Med 21(9):e1004465

- **Link, version, peer review:** https://doi.org/10.1371/journal.pmed.1004465 — version of record via PMC11441682 (includes peer-review history); peer reviewed. Authors from PMC XML.
- **Source text for quotes:** `texts/c1776_PMC11441682.txt` (§ = section).
- **Data source and country:** CPRD Aurum linked to HES and ONS, England (§Methods and findings: "UK Clinical Practice Research Datalink Aurum data (linked with data from Hospital Episode Statistics and Office for National Statistics)").
- **Clinical domain:** cardiovascular.
- **Sample size:** "Approximately 17,593 Black, 30,805 South Asian, and 524,623 White patients" (§Methods and findings).
- **Treatments:** angiotensin receptor blockers (ARB) vs ACE inhibitors (ACEi).
- **Outcome type:** time-to-event composite (CV death, MI, stroke, HF hospitalisation); angioedema safety; SBP change.
- **Estimators:** "inverse-probability—weighted Cox proportional hazards model ... with heterogeneity by ethnicity assessed on the relative and absolute scale" (§Methods and findings); PS model fitted within ethnicity strata, trimmed (§Statistical analysis: "Propensity scores were trimmed at the 1st percentile in the ACEi group and the 99th percentile in the ARB group").
- **Tuning and selection procedure:** confounders "chosen based on a priori knowledge and the use of a directed-acyclic graph" (§Statistical analysis); no ML.
- **Validation approach:** benchmark against ONTARGET with two prespecified criteria before extending to underrepresented groups.
- **Known truth available (plasmode or simulation):** no (trial as reference for the overall effect).
- **Subgroups:** ethnicity (Black, South Asian, White) — prespecified effect modification.
- **Main result:** overall HR 0.96 (95% CI 0.95–0.98) "meeting the first of 2 prespecified validation criteria ... but not the second, because the CI did not include 1"; a trial-sized random subset (n = 17,687) gave "HR 0.97 (95% CI: 0.89, 1.06)" (§Results: Emulation of the reference RCT). Null HTE for primary outcome: "no evidence of treatment effect heterogeneity by ethnicity for the primary outcome on the multiplicative (Pint = 0.422) or additive scale"; but CV death showed heterogeneity — ARB "associated with more events in Black individuals (HR 1.20 (95% CI: 1.02, 1.40)" (§Methods and findings). Angioedema: heterogeneity on additive but not multiplicative scale.
- **Code availability:** data not shareable; reviewer notes "All the readily available study materials (ICD10 codes and syntax) are now available on a repository" (peer-review history) — repository URL not extracted, UNVERIFIED.
- *Methodological lesson (my judgement):* an example of the benchmark-then-extend logic for subgroup effects in routine data; the benchmark validates only the overall effect, not the ethnic-group contrasts (trial had few minority participants).
- *Not verified:* S1 Appendix (PS model, Tables C–G).

#### Row 22. [c0381] Rekkas A, van Klaveren D, Ryan PB, Steyerberg EW, Kent DM, Rijnbeek PR (2023). A standardized framework for risk-based assessment of treatment effect heterogeneity in observational healthcare databases. NPJ Digit Med 6:58 (doi 10.1038/s41746-023-00794-y)

- **Link, version, peer review:** https://doi.org/10.1038/s41746-023-00794-y — version of record (OA) via PMC10060247; peer reviewed. Authors, volume 6 and article 58 confirmed from the PMC XML.
- **Source text for quotes:** `texts/c0381_PMC10060247.txt` (§ = section).
- **Data source and country:** three US claims databases (OMOP CDM) — "IBM® MarketScan® Commercial Claims and Encounters (CCAE), IBM® MarketScan® Multi-State Medicaid (MDCD), and IBM® MarketScan® Medicare Supplemental Beneficiaries (MDCR)" (§Step 2).
- **Clinical domain:** cardiovascular (hypertension).
- **Sample size:** thiazide initiators 355,826 / 54,835 / 37,882 and ACEi initiators 930,629 / 106,492 / 105,852 in CCAE / MDCD / MDCR (§Step 2).
- **Treatments:** thiazide or thiazide-like diuretics vs ACE inhibitors.
- **Outcome type:** time-to-event (2-year acute MI, stroke, HF hospitalisation; nine safety outcomes).
- **Estimators:** PATH-style risk modelling: internal 2-year acute MI risk model, three risk groups, then PS stratification within risk group; risk-group relative effects by "averaging over the hazard ratio estimates derived from Cox regression models fitted in each propensity score stratum" and absolute effects from Kaplan–Meier differences at 2 years (§Step 4).
- **Tuning and selection procedure:** "LASSO logistic regression with 3-fold cross validation for hyper-parameter selection" (§Step 3), fitted on "the propensity score-matched (1:1) subset".
- **Validation approach:** diagnostics per stratum (PS overlap, balance); empirical calibration with negative controls — "76 negative control outcomes" (§Covariate balance/Systematic error area); prediction-model discrimination reported.
- **Known truth available (plasmode or simulation):** negative controls only (true HR = 1); no known-truth HTE.
- **Subgroups:** strata of predicted acute MI risk (<1%, 1–1.5%, >1.5%).
- **Main result:** "patients at low risk of acute myocardial infarction receive negligible absolute benefits for all three efficacy outcomes" (§ABSTRACT); benefits "mainly driven by patients with predicted acute MI risk above 1.5%" (§Interpretation). Negative-control check failed in one database: "no evidence of residual confounding, except for CCAE" and CCAE hazard ratios "were often significantly larger than 1".
- **Code availability:** yes — "https://github.com/mi-erasmusmc/HteFramework" and R package "https://github.com/ohdsi/RiskStratifiedEstimation" (§Code availability).
- *Not verified:* supplementary tables (prediction performance numbers, Section C negative controls list).

#### Row 23. [c1475] Doutreligne M, Struja T, Abecassis J, Morgand C, Celi LA, Varoquaux G (2025). Step-by-step causal analysis of EHRs to ground decision-making. PLOS Digit Health 4(2):e0000721

- **Link, version, peer review:** https://doi.org/10.1371/journal.pdig.0000721 — version of record via PMC11790099 (JATS, includes peer-review history at end); peer reviewed. Preprint arXiv 2308.01605v4 not compared.
- **Source text for quotes:** `texts/c1475_doutreligne_plos.txt` (from Brief 3; § = section).
- **Data source and country:** MIMIC-IV v2.2, single US hospital ICU EHR (§Data Availability: "We used MIMIC-IV.v2.2").
- **Clinical domain:** infection / critical care (sepsis).
- **Sample size:** "18,121 patients of which 3,559 were treated with a combination of crystalloids and albumin" (§Step 1 area, line ~295).
- **Treatments:** crystalloids + albumin vs crystalloids only within first 24 h.
- **Outcome type:** binary, 28-day mortality (§ABSTRACT PICO).
- **Estimators:** outcome regression, IPW, AIPW, double ML, causal forest (S8 Fig mentions "detailed results with causal forest"); nuisances "random forests and ridge logistic regression implemented with scikit-learn" (§Step 3). CATE: "CATEs can be estimated by regressing an individual’s predictions given by the causal estimator against the sources of heterogeneity" (S7 Appendix referenced).
- **Tuning and selection procedure:** "We chose the hyperparameters with a random search procedure (S5 Appendix)"; estimator choice judged by agreement with RCT meta-analyses (random forests closer "to the consensus across prior studies (no effect) than the logistic regression").
- **Validation approach:** benchmark of the **ATE** against pooled RCTs ("Meta-analyses from multiple pivotal RCTs found no effect of adding albumin to crystalloids"); vibration analysis over design/aggregation/estimator choices (§Step 4).
- **Known truth available (plasmode or simulation):** no (external RCT evidence as reference for the ATE only).
- **Subgroups:** four binary characteristics (age ≥60, sex, septic shock, one more) — "We explore heterogeneity along four binary patient characteristics".
- **Main result:** "a doubly robust estimator (AIPW) with random forests proved to be the most reliable estimator" (§ABSTRACT); "too large treatment-initiation times induce immortal time bias" (§ABSTRACT); subgroups: "treatment efficacy of albumin was better for patients >60 years old, males, and patients with septic shock" (§ABSTRACT). Methodological caveat (my judgement): the heterogeneity step is trusted because the ATE matched trials — "Having validated the analytical pipeline, we can use it to inform decision-making" — no validation targeted the CATE itself; septic-shock finding "consistent with one RCT".
- **Code availability:** "The code for data preprocessing and analyses are available on github https://github.com/soda-inria/causal_ehr_mimic/" (§Data Availability).
- *Not verified:* S5, S7, S8 appendices (supplementary).

#### Row 24. [c0457] Yadlowsky S, Pellegrini F, Lionetto F, Braune S, Tian L (2021; online 2020). Estimation and validation of ratio-based conditional average treatment effects using observational data. J Am Stat Assoc 116(533):335–352

- **Link, version, peer review:** https://doi.org/10.1080/01621459.2020.1772080 — author manuscript via PMC7985957; peer reviewed. arXiv 1912.06977 not compared.
- **Source text for quotes:** `texts/c0457_PMC7985957.txt` (§ = section).
- **Data source and country:** NeuroTransData (NTD) MS registry, Germany (§A motivating example: "includes about 25,000 patients with multiple sclerosis, which represents about 15% of all MS patients in Germany").
- **Clinical domain:** neurology (multiple sclerosis).
- **Sample size:** "1050 MS patients receiving TERI and 1741 patients receiving DMF between January 1, 2009 and July 1, 2018" (§Experimental design).
- **Treatments:** teriflunomide (TERI) vs dimethyl fumarate (DMF).
- **Outcome type:** count (relapse rate; ratio-based CATE); time to relapse in supplement.
- **Estimators:** naïve Poisson regression, boosting, proposed doubly robust contrast regression and two-regression approaches for the ratio CATE (§Method; §Experimental design).
- **Tuning and selection procedure:** baseline rates via boosting "the number of trees is selected via 5-fold cross-validation"; "The proposed CATE score is based on the average of three replicates of 7-fold cross-fitting" (§Experimental design).
- **Validation approach:** validation curve on an independent sample — ATE ratio in subgroups with estimated CATE score above c, confounding-adjusted (doubly robust); "the trend of AD(c) is a natural measure of the quality of the CATE score" (§Validation).
- **Known truth available (plasmode or simulation):** in simulation only (synthetic Gaussian covariates, not routine data); none in registry analysis.
- **Subgroups:** CATE-score-defined groups (e.g. split testing set into halves).
- **Main result:** registry: adjusted relapse rate ratio 1.299 (95% CI 1.018, 1.658) TERI vs DMF (§Results); proposed scores "appear to have a similarly superior performance to naïve regression and boosting in the testing set" and "suggest a moderate treatment effect heterogeneity" (§Results). Negative/limiting: in simulation "When the log-transformed CATE is highly nonlinear ... the ratio of the predictions from boosting outperforms the proposed method" (§Numerical Simulation). Lesson: naïve two-model contrasts "may induce spurious treatment-covariate interaction in observational studies when the regression model is misspecified" (§ABSTRACT).
- **Code availability:** not found in text searched — UNVERIFIED.
- *Not verified:* Supplementary Sections 8–9.

#### Row 25. [c0416] Brooks JM, Chapman CG, Floyd SB, Chen BK, Thigpen CA, Kissenberth M (2022). Assessing the ability of an instrumental variable causal forest algorithm to personalize treatment evidence using observational data: the case of early surgery for shoulder fracture. BMC Med Res Methodol 22:190

- **Link, version, peer review:** https://doi.org/10.1186/s12874-022-01663-0 — version of record (OA) via PMC9275148; peer reviewed. Full title confirmed from JATS.
- **Source text for quotes:** `texts/c0416_PMC9275148.txt` (§ = section).
- **Data source and country:** US fee-for-service Medicare claims, 2011 (§Methods, abstract: "a population of 72,751 fee-for-service Medicare beneficiaries with PHFs in 2011").
- **Clinical domain:** orthopaedics (proximal humerus fracture, PHF).
- **Sample size:** 72,751.
- **Treatments:** early surgery vs conservative care.
- **Outcome type:** binary detriment (death or adverse event 61–365 days) and binary benefit ("process of recovery" E&M-visit based) (§Outcomes).
- **Estimators:** instrumental-variable causal forest algorithm (IV-CFA) with local-area surgical signature instrument (risk-adjusted area surgery ratios by Hospital Referral Region, §Instrumental variable); CART on estimates to form ex-post reference classes; 2SLS within classes.
- **Tuning and selection procedure:** sensitivity to parameters, not selection: "the number of trees had no appreciable effects on the estimates" so they "focused on scenarios using 4000 trees and varied the minimum leaf size" (§Results).
- **Validation approach:** consistency of estimates/classes across algorithm parameters; 2SLS checks against "known 2SLS properties" (§Methods, abstract).
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** ex-post reference classes from CART.
- **Main result:** "estimates for individual patients varied with algorithm parameters" but "CART applied to these estimates revealed ex-post reference classes consistent across algorithm parameters" (§Results, abstract); older, frailer, more comorbid patients "were less likely to benefit and more likely to have detriments from higher rates of early surgery" (§Results, abstract). Caveat: interpretation "remains conditional on the extent of measured information in the data" (§Conclusions).
- **Code availability:** not stated; data from ResDAC (§Availability of data and materials: "obtained from ResDAC upon successful application").
- *Not verified:* supplementary tables of parameter combinations.

### C. Time-to-event and competing-risk HTE methods used on routinely collected data

#### Row 26. [S06] (seed) Cui Y, Kosorok MR, Sverdrup E, Wager S, Zhu R (2023). Estimating heterogeneous treatment effects with right-censored data via causal survival forests. J R Stat Soc Series B 85(2):179–211

- **Link, version, peer review:** https://doi.org/10.1093/jrsssb/qkac001 — **version of record** now read (user-supplied PDF; "Advance access publication 27 February 2023"; JRSS-B 85:179–211); peer reviewed. Earlier extraction used arXiv v5 (https://arxiv.org/abs/2001.09887v5, 28 Feb 2023).
- **Source text for quotes:** VoR `texts/user_cui2023_jrssb_raw.txt` (my reading-order pdftotext; VoR p. = PDF page) and arXiv `texts/S06_arxiv2001.09887v5.txt`. Quotes below without a prefix are from arXiv v5 (p. = arXiv page); each was checked to appear in the VoR with identical wording apart from number formatting (e.g. "2,139" in the VoR).
- **Data source and country:** simulation plus ACTG 175 HIV randomised trial (USA) — **not routinely collected data** (p.16: "The original dataset consists of 2139 HIV-infected subjects").
- **Clinical domain:** infection (HIV) in the application; methods.
- **Sample size:** application: ddI 561 vs ZDV+ddI 522 (p.16); simulations "trained on n = 2000 samples" (Table 1 caption, p.15).
- **Treatments:** ZDV+ddI vs ddI monotherapy.
- **Outcome type:** right-censored time-to-event; estimands RMST and survival probability (p.9).
- **Estimators:** causal survival forest (CSF) — "an adaptation of the causal forest algorithm ... that adjusts for censoring using doubly robust estimating equations" (p.1); comparators virtual twins, survival random forests (SRC1/SRC2), IPCW forest.
- **Tuning and selection procedure:** p.3 Figure 1 example uses "default package tuning parameters"; VoR Remark 5: "The default tuning parameters in grf were chosen based on empirical perform­ ance in a series of experiments" and tuning by n and p was "not taken here" (VoR p.15).
- **Validation approach:** simulation with known CATE (MSE, excess MSE, sign classification error, CI coverage).
- **Known truth available (plasmode or simulation):** yes in simulation (synthetic covariates, p = 15, uniform).
- **Subgroups:** sign of effect; covariate-specific CIs.
- **Main result:** CSF "is superior to ordinary random survival forests which do not target the causal parameter directly"; "when targeting RMST, IPCW performs best" in setting 4 (p.15). CI coverage uneven (Table 3, p.17: e.g. setting 4 coverage 0.37 at one test point for RMST) — negative result for inference in hard settings (my reading of the table). Application treats trial as observational: "we analyze the study as an observational rather than randomized study" (p.16).
- **Code availability:** "available from CRAN and at github.com/grf-labs/grf" (p.2).
- *VoR vs arXiv v5 — substantive differences (my comparison):* none found. Checked: abstract, Table 1 MSE values and "repeated 250 times", Table 3 coverage values (setting 4 RMST row "0.37 0.68 0.96 0.88" identical), Remark 5 on default tuning, the best-linear-projection simulation, the ACTG175 application and the grf code statement. The VoR abstract is shorter than the arXiv one ("In our experiments, we find our approach to perform well relative to a number of baselines", VoR p.1).
- *Inference on CATE summaries (VoR p.17):* doubly robust best linear projection performs well, whereas regressing fitted CATEs directly "can be biased (top row), and badly underestimates the sampling variability of these estimators, thus resulting in poor coverage" — naive-averaging ATE coverage 0.06 vs 0.94 for the doubly robust version (Figure 2, VoR p.13).
- *Relevance:* the reference TTE HTE method; no routine-data application in the seed itself (applied uses are in c0022, c0848, c0049, c0788, c0790).
- *Not verified:* JRSS-B final text; Table 3 test-point definitions.

#### Row 27. [c0279] Bo N, Jeong J, Forno E, Ding Y (2025). Evaluating meta-learners to analyze treatment heterogeneity in survival data: application to electronic health records of pediatric asthma care in COVID-19 pandemic. Stat Med 44(3-4):e10333

- **Link, version, peer review:** https://doi.org/10.1002/sim.10333 — version via PMC11758764 (JATS); peer reviewed. arXiv preprint 2407.01565v1 (screening c1650) is the same work, not compared.
- **Source text for quotes:** `texts/c0279_PMC11758764.txt` (§ = section).
- **Data source and country:** EHR, Children's Hospital of Pittsburgh, USA (§ line 80: "we analyzed EHR data of pediatric asthma patients (2–21 years old) obtained from the Children's Hospital of Pittsburgh").
- **Clinical domain:** respiratory (paediatric asthma).
- **Sample size:** "32 000+ encounters (i.e., visits) from 13 000+ patients" (same passage).
- **Treatments:** written asthma action plan (WAAP) vs none at index ED visit ("25% with WAAP vs. 75% without WAAP", §Estimation of CATE of WAAP).
- **Outcome type:** time-to-ED return (right-censored); CATE = difference in ED-return-free probability at one year.
- **Estimators:** six pseudo-ITE meta-learners (incl. M-, DR-, R-, DEA-learners) plus causal survival forest comparator (§Simulation; §Conclusion); nuisances by random survival forests (RSF) and RF.
- **Tuning and selection procedure:** R-learner chosen for the application "Given the unbalanced allocation of WAAP"; "CATEs were estimated through a 5‐fold cross‐fitting"; "The out‐of‐bag prediction was used for nuisance parameter estimation" (§Estimation of CATE of WAAP).
- **Validation approach:** simulation (RCT and observational settings, independent and covariate-dependent censoring) with known CATE; application uses mean-treatment-difference curve over top CATE quantiles (§Subgroup Analysis).
- **Known truth available (plasmode or simulation):** yes in simulation (synthetic covariates); no in EHR.
- **Subgroups:** data-adaptive top-(1−q) CATE subgroups; kernelSHAP variable attribution.
- **Main result:** recommend "DEA‐ and R‐learner, which produce minimum biases and small RMSEs in CATE estimation" under independent or covariate-dependent censoring "with low to moderate censoring rates" (§Conclusion). Under complex scenario 3 "all methods show more obvious biases except for the DEA‐learner"; "CSF shows comparable biases and RMSEs as DR‐, R‐, and DEA‐learners" (§Observational Studies With Covariate‐Dependent Censoring). Application: "The MTD curve shows a positive benefit from WAAP for all patients" and declines towards the overall value with "the top 75% of patients" (§Subgroup Analysis).
- **Code availability:** "The key functions can be found in Github https://github.com/nab1779321/metalearner_shap_surv" (§Data Availability Statement).
- *Not verified:* Data S1 supplementary figures; exact simulation RMSE values.

#### Row 28. [c0488] Zhu J, Gallego B (2020). Targeted estimation of heterogeneous treatment effect in observational survival analysis. J Biomed Inform, article 103474

- **Link, version, peer review:** https://arxiv.org/abs/1910.08877v2 — arXiv v2 (PDF header "A PREPRINT - O CTOBER 24, 2019"); journal version https://doi.org/10.1016/j.jbi.2020.103474 peer reviewed, not read (Elsevier blocked). Volume not checked.
- **Source text for quotes:** `texts/c0488_arxiv1910.08877v2.txt` (pdftotext; p. = PDF page).
- **Data source and country:** CPRD linked to HES, ONS mortality and IMD, UK (p.8: "The cohort consisted of patients with a diagnosis of AF (either in CPRD or HES datasets) between 1st-Mar-2011 and 31-July-2017").
- **Clinical domain:** cardiovascular (non-valvular AF anticoagulation).
- **Sample size:** age subgroups sum to 28,921 (p.10: "249 observations in [18, 39), 2,992 in [39, 60), 16,587 in [60, 82), and 9,093 in [82, 100]"); Table 2 note mentions "28, 972 estimations" (p.9) — inconsistency within paper, flag.
- **Treatments:** oral anticoagulants vs none (initiation).
- **Outcome type:** time-to-event (death, ischaemic stroke, major bleeding, combined), 24 quarters.
- **Estimators:** two-model super learner for survival potential outcomes; feature selection by an ensemble of adaptive lasso, elastic net, BART and causal forest with Kneedle threshold; CATE in reference classes by kernel local averaging with one-step TMLE adjustment (p.2, p.4).
- **Tuning and selection procedure:** "The training of Super-learner is cross-validated with 10 folds" (p.4); variable inclusion thresholds by Kneedle algorithm.
- **Validation approach:** simulation (synthetic uniform covariates, not CPRD-based) varying confounding, dimension, event rate, subgroup size; bootstrap stability of feature identification in CPRD (Table 2).
- **Known truth available (plasmode or simulation):** yes in simulation only.
- **Subgroups:** age bands; Charlson index.
- **Main result:** simulation: "For D > 10, the PPV and TPR drop below 50% across all algorithms" for feature identification (p.6); BART best for feature identification at n = 3,000 (p.6); confounding increased ATE %bias from "8.41% and 24.55%" at β = 0 vs 2 (p.6). CPRD: "Age is the only feature contributing to all outcomes" (p.10); age HTE "not statistically significant across the smaller age groups [18, 60)"; patients ≥82 show roughly double effect vs 60–82 (p.10). Authors' reflection: "the structure of the potential outcome model matters more than the strategy for handling selection bias" (p.11).
- **Code availability:** not stated in text searched — UNVERIFIED.
- *Not verified:* journal version; Appendices B and D.

#### Row 29. [c0452] Hu L, Ji J, Li F (2021). Estimating heterogeneous survival treatment effect in observational data using machine learning. Stat Med 40(21):4691–4713

- **Link, version, peer review:** https://doi.org/10.1002/sim.9090 — author manuscript via PMC9827499; peer reviewed. arXiv 2008.07044v4 not compared.
- **Source text for quotes:** `texts/c0452_PMC9827499.txt` (§ = section).
- **Data source and country:** simulation (synthetic covariates, p = 10) plus National Cancer Database (NCDB), USA (§CASE STUDY: "the NCDB data including 7730 high-risk localized prostate cancer patients").
- **Clinical domain:** oncology (prostate cancer radiotherapy).
- **Sample size:** simulation n = 500 and 5,000 (§Simulation design); NCDB 7,730.
- **Treatments:** EBRT + androgen deprivation (AD) vs EBRT + brachytherapy ± AD.
- **Outcome type:** time-to-event (individual survival treatment effect, ISTE; median survival differences).
- **Estimators:** AFT-BART (semi- and nonparametric, ± PS covariate), random survival forests, targeted survival HTE estimation (TSHEE = c0488), DeepSurv, censoring-unbiased deep learning (DR-DL, BJ-DL), GAPH, parametric AFT, Cox (§Statistical methods).
- **Tuning and selection procedure:** mostly defaults/fixed settings: "We used the abart function from the R package bart with the default settings"; RSF "with 1000 trees, mtry = p/3 and a nodesize of 3" (§Implementation).
- **Validation approach:** simulation varying confounding/overlap (ψ ∈ {1, 2.5, 5}), heterogeneity settings, censoring, unmeasured confounding; PEHE, bias, regret, coverage.
- **Known truth available (plasmode or simulation):** yes (simulation; not built on NCDB covariates).
- **Subgroups:** second-stage regression of estimated ISTE on covariates (PSA, age) in NCDB.
- **Main result:** "AFT-BART-NP) consistently yields the best performance, in terms of bias, precision, and expected regret"; credible intervals give "close to nominal frequentist coverage for the individual survival treatment effect when the covariate overlap is at least moderate" (§ABSTRACT). Negative: with unmeasured confounding "the performance of all methods deteriorated" though rankings were unchanged (§Sensitivity to unmeasured confounding). NCDB: average effect "not statistically significant at the 0.05 level" but "PSA and age significantly modulated the comparative effect" (§CASE STUDY).
- **Code availability:** "https://github.com/liangyuanhu/ML-DL-TEH" (§DATA AVAILABILITY STATEMENT).
- *Not verified:* Web Tables/Figures (supplement).

#### Row 30. [c0397] Hu L, Ji J, Liu H, Ennis R (2022). A flexible approach for assessing heterogeneity of causal treatment effects on patient survival using large datasets with clustered observations. Int J Environ Res Public Health 19(22):14903

- **Link, version, peer review:** https://doi.org/10.3390/ijerph192214903 — version of record (OA) via PMC9690785; peer reviewed. Short communication (~2,500 words); details in supplement and in earlier riAFT-BART paper (c0413).
- **Source text for quotes:** `texts/c0397_PMC9690785.txt` (§ = section).
- **Data source and country:** NCDB (US hospital-based cancer registry); simulation "based our simulation procedures on real data from the National Cancer Database (NCDB)" (§3.1).
- **Clinical domain:** oncology (high-risk localized prostate cancer).
- **Sample size:** "64,569 high-risk localized prostate cancer patients diagnosed between 2004 and 2015" (§3.2), clustered within institutions.
- **Treatments:** radical prostatectomy (RP), EBRT + AD, EBRT + brachytherapy ± AD.
- **Outcome type:** time-to-event (overall survival; AFT time ratios).
- **Estimators:** riAFT-BART (random-intercept AFT with BART) vs IPW random-intercept Cox, doubly robust random-intercept additive hazards, random-intercept GAPH (§3.1).
- **Tuning and selection procedure:** regularising BART priors (§2); no data-driven selection described.
- **Validation approach:** simulation informed by NCDB (details in Supplement).
- **Known truth available (plasmode or simulation):** yes (simulation built on NCDB structure — details UNVERIFIED, supplement not read).
- **Subgroups:** data-driven subgroups via tree on individual effects (e.g. Gleason ≥9).
- **Main result:** in simulation riAFT-BART "yielded the smallest biases (Figure S1) and root-mean-squared errors" (§3.1). NCDB: RP survival time "1.25 (1.15, 1.37) times as long" vs EBRT + brachy ± AD on average, but "among high-grade cancer patients with a Gleason score ≥ 9, there was no statistically significant treatment benefit associated with RP" (§3.2).
- **Code availability:** "R package riAFT-BART, freely available on CRAN" (§Data Availability Statement).
- *Not verified:* Supplementary simulation design and Figures S1–S3, Table S5.

#### Row 31. [c0022] Kim M, Jeon N, Suh HS (2025). Effects of bisphosphonates after denosumab discontinuation and treatment effect heterogeneity using causal machine learning. Sci Rep 15:44533

- **Link, version, peer review:** https://doi.org/10.1038/s41598-025-28172-6 — version of record (OA) via PMC12738746; peer reviewed.
- **Source text for quotes:** `texts/c0022_PMC12738746.txt` (§ = section).
- **Data source and country:** Korean HIRA national claims database, 2015–2022 (§Data source: "a comprehensive repository for claims data generated in a healthcare reimbursement process").
- **Clinical domain:** musculoskeletal / pharmacoepidemiology (osteoporotic fracture).
- **Sample size:** "the BP and non-BP cohorts comprised 7138 (22.9%) and 24,079 (77.1%) patients" (§Baseline characteristics).
- **Treatments:** bisphosphonates (BP) vs none after denosumab discontinuation.
- **Outcome type:** time-to-event (recurrent osteoporotic fracture; fracture-free probability at 1 year).
- **Estimators:** causal survival forest (doubly robust, censoring-adjusted) for ATE and CATE; IPW Cox for comparison (§Average treatment effects).
- **Tuning and selection procedure:** CSF hyperparameters not described in the text searched — UNVERIFIED (possibly in supplement).
- **Validation approach:** HTE checks: CATE histogram + t-test, targeting operator characteristic (TOC/RATE, AUTOC), box plots, best linear projection (BLP) by covariates (§Heterogeneous treatment effects, Methods).
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** age (≥80 vs <80), prior BP duration, diabetes, peptic ulcer, steroid use, institution type.
- **Main result:** ATE: "fracture-free probability difference: 0.032; 95% CI 0.022–0.042" (§ABSTRACT). **Null calibration-type evidence:** "no significant difference between negative and positive treatment effects (p = 0.393)" and AUTOC "was 0.010 (95% CI  − 0.005 to 0.031), closely approaching zero" implying "minimal heterogeneity in the rank-weighted average treatment effect" (§Heterogeneous treatment effects, Results) — yet abstract reports "Treatment effects varied by age, prior BP use, diabetes without complications, peptic ulcer disease, steroid use, and type of treatment institution" based on graphical stratification. Methodological lesson (my judgement): RATE/TOC null contradicts subgroup claims; illustrates over-interpretation of CSF CATEs.
- **Code availability:** not stated; data "not publicly available due to privacy and ethical restrictions" (§Data availability).
- *Not verified:* Supplementary Figures S2–S5; CSF settings.

#### Row 32. [c0848] Gopukumar D, Menon N, Schoen MW (2024). Medication prescription policy for US veterans with metastatic castration-resistant prostate cancer: causal machine learning approach. JMIR Med Inform 12:e59480

- **Link, version, peer review:** https://doi.org/10.2196/59480 — version of record (OA) via PMC11615563; peer reviewed.
- **Source text for quotes:** `texts/c0848_PMC11615563.txt` (§ = section).
- **Data source and country:** US Department of Veterans Affairs EHR (§Methods line ~72: "stored in the Corporate Data Warehouse").
- **Clinical domain:** oncology (mCRPC).
- **Sample size:** "2886 identified veterans" (§Methods, abstract), African American and White only.
- **Treatments:** enzalutamide vs abiraterone as first-line ARPI.
- **Outcome type:** time-to-event (follow-up days on first-line drug; RMST).
- **Estimators:** causal survival forest (grf), AIPW scores, policy trees (policytree) (§Methods).
- **Tuning and selection procedure:** horizon chosen so that "estimated censoring probabilities are not below 0.2", starting "with a horizon of 2000 days ... and decremented by 100 to 1000"; "The honesty fraction was set to 0.7"; "We set the number of trees to 15,000"; policy tree depth chosen by testing ("We found significance in the prescription policy tree with a depth of 3") (§Methods/§Results). Horizon selection uses the data — potential for optimistic inference (my judgement).
- **Validation approach:** 10-fold cross-fitting with median split of held-out CATE rankings into two groups ("the “unseen” observations in the left-out fold were ranked based on their predictions and split along the median into 2 groups"); policy value on 30% held-out test data.
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** two data-driven CATE groups; policy-tree leaves.
- **Main result:** enzalutamide "associated with an average of 59.94 (95% CI 35.60-84.28) more days of survival than abiraterone"; AIPW subgroup scores 19.36 (95% CI –16.93 to 55.65) vs 100.68 (62.46–138.89), difference "significant (P=.003)" (§Results, abstract); depth-3 policy value "56.38 (95% CI 8.89 to 103.87)" (§Results).
- **Code availability:** not stated; R packages grf and policytree named.
- *Not verified:* multimedia appendices; ASMD diagnostics.

#### Row 33. [c0049] Jun I, Cohen SA, Ser SE, Marini S, Lucero RJ, Bian J, Prosperi M (2023). Optimizing dynamic antibiotic treatment strategies against invasive methicillin-resistant Staphylococcus aureus infections using causal survival forests and G-formula on statewide electronic health record data. Proc Mach Learn Res 218:98–115

- **Link, version, peer review:** https://pubmed.ncbi.nlm.nih.gov/37854935/ — author manuscript via PMC10584043 (PMLR proceedings, peer reviewed). Full title confirmed from JATS.
- **Source text for quotes:** `texts/c0049_PMC10584043.txt` (§ = section).
- **Data source and country:** UF Health EHR (Epic; Integrated Data Repository), Florida, USA (§Ethics Statement, Data Source: "deidentified data from a large university hospital system in Florida, UF Health").
- **Clinical domain:** infection (invasive MRSA).
- **Sample size:** "the final study population comprises the last subset of 427 patients" from 1,433 with confirmed MRSA (§Population Characteristics).
- **Treatments:** vancomycin vs switching to another antibiotic across three sequential time points.
- **Outcome type:** time-to-event, 30-day mortality.
- **Estimators:** causal survival forest (three-point sequence, binary "change" treatment) and parametric g-formula (time-updated strategy) (§Causal Survival Forests and G-formula).
- **Tuning and selection procedure:** two covariate sets (DAG experts vs expanded comorbidities); hyperparameters not reported in text searched — UNVERIFIED.
- **Validation approach:** RATE/AUTOC for heterogeneity; best linear predictor; agreement with RCT knowledge ("consistent with the general knowledge of clinical efficacy of vancomycin", §Discussion).
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** CATE quantiles via TOC.
- **Main result:** ATE of switching: probability of death reduced (Model 1 "Mean = −0.07619, SE=0.02953"); **null heterogeneity**: "In Model 1, there was minimal heterogeneity of treatment effect (AUTOC = 0.01, S.E = 0.06)"; Model 2 AUTOC −0.04 (SE 0.06) (§Estimation of Treatment Effects) — CI includes zero, so the claimed beneficiary group is not supported by RATE (my reading). Small sample (n = 427) limits HTE detection.
- **Code availability:** not stated in text searched — UNVERIFIED.
- *Not verified:* Table 3 BLP values; Figure 4.

#### Row 34. [c1053] Rytgaard HCW, Ekstrøm CT, Kessing LV, Gerds TA (2023). Ranking of average treatment effects with generalized random forests for time-to-event outcomes. Stat Med 42(10):1542–1564

- **Link, version, peer review:** https://doi.org/10.1002/sim.9686 — **version of record** (user-supplied PDF; "Received: 31 August 2021 Revised: 2 February 2023 Accepted: 3 February 2023"); peer reviewed. Earlier extraction used arXiv v1 (https://arxiv.org/abs/2104.13028v1, 27 Apr 2021).
- **Source text for quotes:** VoR `texts/user_rytgaard2023_statmed_raw.txt` (my reading-order pdftotext; p. = PDF page) — quotes below are from the VoR unless marked "arXiv p."; arXiv `texts/c1053_arxiv2104.13028v1.txt`.
- **Data source and country:** linked Danish national registries — "linking Danish population-based registers that contain data on all prescribed medical purchases at pharmacies since 1995" plus hospital data since 1977 (p.10).
- **Clinical domain:** mental health (relapse of severe depression; drug repurposing).
- **Sample size:** "A total of 78 700 patients were included who all had a first-time admission with depression after 2005" (p.10). Simulations: n from 500 to 5,000; "we report results based on M = 2000 simulation repetitions" (M = 1,000 for n = 5,000) (p.6).
- **Treatments:** binary exposures defined by ATC three-digit groups (any purchase in 8 weeks after index; Figure 4 caption, p.10); 33 ATC groups ranked (Figure 5, p.11).
- **Outcome type:** time-to-event with competing risks; effects on crude and net absolute risk at a horizon.
- **Estimators:** generalized random forest on inverse-probability-of-censoring-weighted outcomes ("we propose a two-step procedure for estimation, applying inverse probability weighting to construct time-point specific weighted outcomes as input for the generalized random forest", p.1); censoring weights from a random survival forest (p.5); comparators: G-formula with Fine–Gray regression or two cause-specific Cox models (p.7).
- **Tuning and selection procedure:** censoring RSF "with 100 survival trees for sample sizes smaller than 5000 and 50 survival trees for sample size equal to 5000", all 17 variables tried per split (p.7); authors note RSF tuning "may require a simulation study which synthesizes the setting of the data application" (p.6).
- **Validation approach:** simulation with ten binary treatments, five binary and two continuous covariates (p.6); bias, coverage, frequency of correct rank-1.
- **Known truth available (plasmode or simulation):** yes (synthetic simulation; not built on registry covariates).
- **Subgroups:** none (average effects).
- **Main result:** forest approach "provides unbiased estimation for both settings, but that the regression-based methods are more efficient" when correctly specified; misspecified regressions biased (Figure 2 caption, p.8). Negative: "positivity issues induced by low treatment prevalence and high amount of right-censoring complicates the estimation problem drastically and likely explains the lower coverage" for crude effects; net-effect coverage "was lying nicely around 95%" (p.8). Registry: ranking of 33 ATC groups by net and crude effects (Figure 5, p.11; values not extracted).
- **Code availability:** VoR: "The total of all simulated scenarios can be obtained from the material at https://github.com/helenecharlotte/ forestCausalSearch" (p.22); "Research data are not shared" (p.12).
- *CLASSIFICATION (Phase 2 fix):* this is an **average-treatment-effect ranking method**, not HTE evidence — "we have considered average treatment effect estimation for the purpose of ranking treatments" (p.11). GRF conditional effects are an intermediate step averaged to ATEs. Keep in the brief only as competing-risk causal-forest machinery used on registry data (tier T2 → demote below HTE papers).
- *VoR vs arXiv v1 — substantive differences (my comparison):* (1) simulation redesigned — v1 had three treatments, n = 500, M = 500 and Kaplan–Meier censoring weights ("Kaplan-Meier estimator stratified", arXiv p.6), the VoR uses ten treatments, n = 500–5,000, M = 2,000, random-survival-forest censoring weights and adds Fine–Gray and cause-specific Cox G-formula comparators; (2) the v1 finding that unadjusted censoring weights gave "an incorrect conclusion of a protective effect of treatment A2 on the net probabilities" with 59.6% coverage (arXiv p.9) is not reported in the same form in the VoR; the VoR instead reports lower crude-effect coverage under positivity problems; (3) repository renamed: v1 "https://github.com/helenecharlotte/grfCausalSearch" (arXiv p.13) vs VoR "https://github.com/helenecharlotte/ forestCausalSearch" (p.22; URL split across lines), with function causalhunter(); (4) the registry cohort (78,700) and the ATE-ranking aim are unchanged; the net-versus-crude argument is retained and qualified: net probabilities are "not sensible interpreting the size of the effect, for example, when counseling a patient" (p.12).
- *Not verified:* Appendix E full simulation tables; numeric registry ranks.

### D. Reporting guidance and validation-metric definitions

#### Row 35. [S03] (seed) Kent DM, Paulus JK, van Klaveren D, D'Agostino R, Goodman S, Hayward R, Ioannidis JPA, Patrick-Lake B, Morton S, Pencina M, Raman G, Ross JS, Selker HP, Varadhan R, Vickers A, Wong JB, Steyerberg EW (2020). The Predictive Approaches to Treatment effect Heterogeneity (PATH) Statement. Ann Intern Med 172(1):35–45

- **Link, version, peer review:** https://doi.org/10.7326/M18-3667 — author manuscript via PMC7531587 (JATS); peer reviewed. Explanation & Elaboration (doi 10.7326/M18-3668, PMC7750907) not readable (efetch no body).
- **Source text for quotes:** `texts/S03_PMC7531587.txt` (§ = section).
- **Data source and country:** none (guidance; expert panel, literature reviews, simulations).
- **Clinical domain:** general.
- **Sample size:** not applicable.
- **Treatments:** see sample size
- **Outcome type:** see sample size
- **Estimators:** risk modelling vs effect modelling — "a “risk modeling” approach wherein a multivariable model predicts the risk of an outcome and is applied to disaggregate patients within RCTs" and "an “effect modeling” approach wherein a model is developed on RCT data by incorporating a term for treatment assignment and interactions" (§ABSTRACT).
- **Tuning and selection procedure:** "Avoid one-variable-at-a-time null hypothesis testing or stepwise selection"; avoid "“conventional” unpenalized maximum-likelihood regression" with interaction terms (§Consensus Statements on ... Effect Modeling).
- **Validation approach:** "Avoid evaluating models that predict treatment benefit using only conventional metrics for outcome risk prediction" (§same); report "outcome rates and both relative and absolute risk reduction across risk strata" (§Apply the Model and Report Results).
- **Known truth available (plasmode or simulation):** simulations used in development (details in E&E, not read).
- **Subgroups:** risk strata; credible effect modifiers assessed with "rigorous multidimensional criteria (such as described in the ICEMAN tool)".
- **Main result:** development via "a multidisciplinary technical expert panel; targeted literature reviews; simulations ... and a deliberative process" (§ABSTRACT). Scope explicitly RCT and regression: "The PATH Statement focuses on regression-based prediction in randomized trials" (§Discussion) — no guidance specific to routinely collected data (extended to observational databases by c0381).
- **Code availability:** not applicable.
- *Observational data (Discussion):* "while observational studies appear to offer many important advantages to conventional RCTs for more refined analyses" it "is not well understood when these data may be sufficiently de-biased" (§Discussion).
- *Not verified:* E&E document content.

#### Row 36. [c0030] Wang X, Zou Y, Wang Y, Zhang C (2025). Estimating heterogeneous treatment effects with target trial emulation: a checklist of causal machine learning for observational data. Chest 168(4):856–859

- **Link, version, peer review:** https://doi.org/10.1016/j.chest.2025.05.028 — version of record (user-supplied PDF); a 4-page **CHEST Commentary** ("[ CHEST Commentary ]" header, p.1), editorially reviewed; not a consensus or Delphi-derived guideline.
- **Source text for quotes:** `texts/user_wang2025_chest.txt` (coordinator) and `texts/user_wang2025_chest_raw.txt` (my reading-order pdftotext; quotes from this). p. = PDF page (journal pp. 856–859).
- **Data source and country:** none — reporting/conduct guidance for HTE with target trial emulation (TTE) in "electronic health records, disease registries, administrative claims databases, or cohort studies" (p.1); authors from Cleveland Clinic (critical-care/respiratory journal).
- **Clinical domain:** see data source
- **Sample size:** see data source
- **Treatments:** see data source
- **Outcome type:** see data source
- **Estimators:** causal forests, meta-learners (S-, T-, X-learners), TMLE and double ML — argued to share "the same inferential core" (p.2).
- **Tuning and selection procedure:** "Use cross-validation to tune hyperparameters and select models"; "use cross-ﬁtting to de-correlate nuisance estimation from the conditional average treatment effect estimation" (Table 1, step 4; p.3).
- **Validation approach:** "Assess calibration (observed vs predicted effects across conditional average treatment effect quantiles)" and report "uplift/Qini curves" (Table 1, p.3). Caveat on Qini: "a model could achieve a high Qini coefﬁcient while still providing incorrect treatment effect estimates" and Qini curves "should not be used in isolation" (p.2).
- **Known truth available (plasmode or simulation):** not applicable; notes PEHE "can be computed only in simulations where the true CATE is known" (p.2).
- **Subgroups:** Not applicable (guidance paper, no data analysis).
- **Main result:** a seven-step checklist (Table 1); acknowledges "performance evaluation for HTEs is a rapidly evolving ﬁeld, and best practices may shift" (p.2); warns per-protocol emulations face time-varying confounding and longitudinal TMLE "remain under development" (p.3).
- **Code availability:** not applicable.
- *Sensitivity / reporting items:* E-values or bias analysis for unmeasured confounding; missing-data sensitivity; "Share code used for data preprocessing, modeling, and analysis in a public repository" (Table 1, step 7).
- *My judgement:* useful as the only checklist in the set aimed at causal-ML HTE in observational data, but it is a short commentary without a development process, evidence base or validation of its items; it does not address plasmode/known-truth checks or negative controls.

#### Row 37. [c0382] Segal JB, Varadhan R, Groenwold RHH, Henderson NC, Li X, Nomura K, Kaplan S, Ardeshirrouhanifard S, Heyward J, Nyberg F, Burcu M (2023). Assessing heterogeneity of treatment effect in real-world data. Ann Intern Med 176(4):536–544

- **Link, version, peer review:** https://doi.org/10.7326/M22-1510 — author manuscript via PMC10273137; peer reviewed (Research and Reporting Methods). A correction notice exists (screening c0374).
- **Source text for quotes:** `texts/c0382_PMC10273137.txt` (§ = section).
- **Data source and country:** none (methods guidance for RWD; examples from oncology and T2D).
- **Clinical domain:** see data source
- **Sample size:** see data source
- **Treatments:** Not applicable (guidance paper, no data analysis).
- **Outcome type:** Not applicable (guidance paper, no data analysis).
- **Estimators:** subgroup confirmation, Bayesian descriptive HTE, prognostic- and propensity-score–based HTE, data-driven discovery, CATE prediction (§section headings, Objectives 1–4).
- **Tuning and selection procedure:** guidance-level only; sequencing rule: "Evaluation of HTE necessarily comes after one has generated a valid estimate of the overall effect across all patients" (§What Are the Key Considerations When Using RWD...).
- **Validation approach:** see tuning and selection
- **Known truth available (plasmode or simulation):** not applicable.
- **Subgroups:** four objectives: "to confirm subgroup effects, to describe the magnitude of HTE, to discover clinically important subgroups, and to predict individual effects" (§ABSTRACT).
- **Main result:** extends PATH because "it is tailored to RWD rather than RCTs—the burgeoning literature on RWD does not address HTE assessment" (§What Is Still Needed?). CATEs "may be more realistically estimated with RWD than in RCTs given the size and richness of RWD" (§Objective 4). Discovery objective: "less concern about adequate power and multiple comparisons, but attention to bias and confounding cannot be ignored" (§Objective 3). Stated gaps: "there is a need for principled approaches to using information about newly discovered subgroups" and recommendations "are needed for presenting results clearly" (§What Is Still Needed?).
- **Code availability:** not applicable.
- *Reporting relevance:* a reporting-adjacent guidance paper for RWD HTE (not a checklist).
- *Not verified:* supplementary material; correction content.

#### Row 38. [S04] (seed) Hoogland J, IntHout J, Belias M, Rovers MM, Riley RD, Harrell FE Jr, Moons KGM, Debray TPA, Reitsma JB (2021). A tutorial on individualized treatment effect prediction from randomized trials with a binary endpoint. Stat Med 40(26):5961–5981

- **Link, version, peer review:** https://doi.org/10.1002/sim.9154 — version via PMC9291969 (JATS); peer reviewed (tutorial).
- **Source text for quotes:** `texts/S04_PMC9291969.txt` (§ = section).
- **Data source and country:** simulation plus two RCT examples (acute otitis media IPD; International Stroke Trial) — **no routinely collected data** (§International Stroke Trial: "a large randomized open trial ... in a total of 19 435 patients").
- **Clinical domain:** infection (otitis media), cardiovascular/neurology (stroke) examples; general methods.
- **Sample size:** simulation n = 400, 1,200, 3,600; 250 runs (§Data generating mechanisms; §Simulation study results); IST subset aspirin n = 4,858 vs none 4,860.
- **Treatments:** binary randomised treatment.
- **Outcome type:** binary; ITE on risk-difference scale.
- **Estimators:** logistic homogeneous-effect and interaction models (ML, penalised: ridge/lasso), risk vs effect modelling, tree-based methods (§section headings).
- **Tuning and selection procedure:** "bootstrap internal validation of likelihood‐based measures of overall fit (eg, R2, AIC)" plus Brier score and observed-vs-expected treatment-effect variability "help to choose among competing models"; start from "a homogeneous treatment effect model as a starting point (reference model)" (§Key points and recommendations).
- **Validation approach:** simulation with known ITE: root mean squared prediction error and calibration of predicted ITE.
- **Known truth available (plasmode or simulation):** yes (parametric simulation, synthetic covariates).
- **Subgroups:** not the focus (individualised effects).
- **Main result:** "conditioning on main effects of the available covariates as in a homogeneous treatment effect model was always beneficial"; "HTE model accuracy was especially sensitive to sample size"; "penalization is key" but "does not remove the risk of overfitting for complex models in small sample size" (§Average root mean squared prediction error). Negative: "calibration in individual small samples could be far off even if average performance across simulations was good" (§Calibration). Even with no interaction on the OR scale, a risk model gives "meaningful differentiation in terms of absolute treatment effect" (§Key points).
- **Code availability:** "R scripts to perform the simulation study ... are available for sharing" (on request; §DATA AVAILABILITY STATEMENT).
- *Relevance to routine data:* indirect — RCT-only; identifiability under randomisation emphasised ("randomization of treatment greatly facilitates causal inference").
- *Not verified:* online supplement Part C (calibration plots).

#### Row 39. [S05] (seed) Efthimiou O, Hoogland J, Debray TPA, Seo M, Furukawa TA, Egger M, White IR (2023). Measuring the performance of prediction models to personalize treatment choice. Stat Med 42(8):1188–1206

- **Link, version, peer review:** https://doi.org/10.1002/sim.9665 — author manuscript via PMC7615726; peer reviewed.
- **Source text for quotes:** `texts/S05_PMC7615726.txt` (§ = section).
- **Data source and country:** simulated datasets plus the SUN☺D antidepressant trial (Japan; RCT) — **no routinely collected data** (§Case study: "a two‐step multi‐center trial comparing first‐ and second‐line treatment strategies").
- **Clinical domain:** mental health (depression) in the example; general methods.
- **Sample size:** trial arms N = 502 and N = 530 (§Case study); simulated external validation set "of 10 000 patients" (§Analysis of the simulated dataset).
- **Treatments:** sertraline + mirtazapine vs switch to mirtazapine.
- **Outcome type:** continuous (PHQ-9) and binary (remission).
- **Estimators:** any outcome-prediction model under treatment/control (e.g. regression vs GBM in the example).
- **Tuning and selection procedure:** not the focus; performance measures for selecting "among competing modeling strategies" (§DISCUSSION).
- **Validation approach:** "two dimensions of model accuracy for treatment effects ... discrimination for benefit and calibration for benefit" plus "decision accuracy" (§ABSTRACT); internal validation "10‐fold CV procedure repeated 100 times" (§Analysis of the simulated dataset); grouping by predicted benefit, clustering by covariates, regression for benefit.
- **Known truth available (plasmode or simulation):** yes in simulation ("Since this was a simulated example, we could also calculate the true value of the performance measures").
- **Subgroups:** groups of predicted benefit (Ng = 10, 20).
- **Main result:** proposed measures "can be useful in evaluating and comparing the performance of competing models" (§ABSTRACT). Negative/limiting: methods "are expected to have limited power to find differences between competing models" and "the assessment of treatment benefit was associated with large uncertainty" (§DISCUSSION); in the depression trial "GBMs performed very slightly better for C‐for‐benefit, but confidence intervals greatly overlapped" (§Analysis of the depression dataset). Simulated mean bias estimate 0.04 vs true −0.03 (§Analysis of the simulated dataset).
- **Code availability:** "We implement all methods in the R package pr" + "edieval" (word split across a JATS line break in §ABSTRACT; i.e. R package predieval).
- *Routine-data relevance:* "all methods could in principle also be extended for models developed on observational data" (with refinement of mean bias) (§DISCUSSION) — not done here (see c1084 for observational identification).
- *Not verified:* supplementary material.

#### Row 40. [c1075] Efthimiou O, Hoogland J, Debray TPA, Aponte Ribero V, Knol W, Koek HL, Schwenkglenks M, Henrard S, Egger M, Rodondi N, White IR (2025). Measuring the performance of survival models to personalize treatment choices. Stat Med 44:e70050

- **Link, version, peer review:** https://doi.org/10.1002/sim.70050 — version via PMC11983264 (JATS); peer reviewed.
- **Source text for quotes:** `texts/c1075_PMC11983264.txt` (§ = section).
- **Data source and country:** simulated data plus OPERAM cluster-randomised trial (multinational Europe) — **RCT, not routinely collected data** (§The OPERAM Trial: "a multicenter, cluster randomized, controlled trial of 2008 hospitalized patients ≥ 70 years of age with multimorbidity").
- **Clinical domain:** pharmacotherapy optimisation in multimorbid older adults (all-cause mortality).
- **Sample size:** OPERAM 2,008; simulation size in appendix (not extracted).
- **Treatments:** structured pharmacotherapy optimisation vs standard care.
- **Outcome type:** time-to-event (survival); benefit defined in survival probability, expected or restricted survival time, percentile survival (§Definitions of Treatment Benefit).
- **Estimators:** Weibull model with all treatment–covariate interactions vs random survival forest as S-learner (§The OPERAM Trial, Results).
- **Tuning and selection procedure:** measures proposed for "model selection or for internal validation" (§ABSTRACT); 10-fold CV used.
- **Validation approach:** C-for-benefit (matching on predicted benefit or on covariates), calibration-for-benefit, decision accuracy for survival outcomes.
- **Known truth available (plasmode or simulation):** yes in simulation.
- **Subgroups:** predicted-benefit groups.
- **Main result:** OPERAM C-for-benefit "0.55 [0.52; 0.58] for Weibull, 0.53 [0.50; 0.56] for random forest" (§Results, OPERAM) — near-chance discrimination for benefit; trial ATE weak (HR = 0.90 [0.71; 1.13]). Simulation 10-fold CV C-for-benefit "0.53 [0.50; 0.56]", "slightly lower than the ones from apparent performance" (§Using 10‐Fold Cross‐Validation). Key rationale: "minimizing the error of outcome predictions does not necessarily minimize the error of the benefit predictions" (§Discussion). Limitation: decision accuracy measures may show little population effect "while statistical power may be too low" (§Discussion).
- **Code availability:** "https://github.com/oremiou/performance‐for‐treatment‐benefit‐survival" (§Software Code).
- *Not verified:* appendix simulation design and sizes.

### E. Added for domain coverage (renal; outside the ranked top 40)

#### Row 41. [c0023] Oh W, Takkavatakarn K, Al-taie Z, Kittrell H, Shawwa K, Gomez H, Sawant AS, Tandon P, Kumar G, Sterling M, Hofer I, Chan L, Oropello J, Kohli-Seth R, Charney AW, Kraft M, Kovatch P, Suárez-Fariñas M, Kellum JA, Nadkarni GN, Sakhuja A (2025). Personalized fluid management in patients with sepsis and acute kidney injury: a causal machine learning approach. Crit Care Explor 7(12):e1354

- **Link, version, peer review:** https://doi.org/10.1097/CCE.0000000000001354 — version of record (OA) via PMC12677861; peer reviewed. A medRxiv precursor (policy-tree version) is screening c1814.
- **Source text for quotes:** `texts/c0023_PMC12677861.txt` (§ = section). Backup renal text saved: `texts/c0936_PMC10924888.txt` (not extracted).
- **Data source and country:** ICU EHR databases MIMIC-IV (US, development) and Salzburg Intensive Care database SICdb (Austria, external validation) (§Study Design and Data Sources: "MIMIC-IV served as the development cohort, and SICdb was used for external validation").
- **Clinical domain:** renal (sepsis-associated AKI) / critical care.
- **Sample size:** "11,650 patients from the development cohort (MIMIC-IV) and 1,931 patients from the external validation cohort (SICdb)" (§Results, Study Population).
- **Treatments:** restrictive IV fluids ("< 500 mL fluids within 24 hr after AKI") vs more liberal fluids (§ABSTRACT, Objectives).
- **Outcome type:** binary — early AKI reversal at 24 h (primary); sustained reversal; MAKE30.
- **Estimators:** causal forest (doubly robust) then policy tree (§Development of Causal-ML Approach); comparator: non-causal random forest.
- **Tuning and selection procedure:** details in Supplementary Methods — UNVERIFIED (not read).
- **Validation approach:** RATE/AUTOC in development and in an external cohort; outcome comparison of patients whose received treatment matched the recommendation.
- **Known truth available (plasmode or simulation):** no.
- **Subgroups:** policy-tree recommended group ("44.0%" development; "68.9%" external) (§Policy Tree...).
- **Main result:** AUTOC development "0.73 (95% CI, 0.70–0.76)" vs random forest 0.45; external "0.15 (95% CI, 0.03–0.27), compared with an AUTOC of –0.02 (95% CI, –0.10 to 0.06)" (§Robustness of HTE Estimation by Causal Forest). Recommended-restrictive patients who received restrictive fluids had higher early AKI reversal "(53.9% vs. 33.2%, p < 0.001)" (§ABSTRACT, Results).
- **Code availability:** not stated in text searched — UNVERIFIED.
- *Why extracted (outside the top 40):* coordinator instruction (a) — renal had no paper in the ranked top 40, so the best openable renal paper is extracted in full for domain coverage. Chosen over c0936 (uplift/Qini, Sci Rep) because it reports an external-validation RATE/AUTOC comparison. Top-40 ranking unchanged.
- *Methodological lesson (my judgement):* the five-fold drop in AUTOC from development to external validation shows strong optimism or transport loss; the concordant-vs-discordant outcome comparison is itself confounded (adjusted analysis reported but not read in detail). This is the clearest renal example of external RATE validation.
- *Not verified:* Supplementary Methods (forest/policy-tree settings, adjusted analyses).

## 2F. Remaining included papers (rule 7: one line each)

These lines are screening notes taken from titles and abstracts; the papers were not extracted. Tier codes: T1 = known truth, or selection/validation on routine data; T2 = time-to-event method on routine data; T3 = reporting or validation-metric guidance; T4 = applied study that reveals method performance; T5 = applied study only.

- **M03** — Wan K, Zhang Y (2023). Estimating treatment effects over time with causal forests: an application to the ACIC 2022 Data Challenge. Observational Studies 9(3):59-71. https://doi.org/10.1353/obs.2023.0026 — T1: ACIC 2022 team paper: causal forests over time on known-truth data. — *Domain:* Health policy (Medicare-like).
- **c0684** — Schreck et al. (2024). Statistical plasmode simulations-Potentials, challenges and recommendations. Stat Med. https://doi.org/10.1002/sim.10012 — T1: Statistical plasmode simulations: potentials, challenges, recommendations. — *Domain:* Methods (plasmode).
- **c0337** — Thomas (2024). Methods for the Design and Conduct of Subgroup Analysis in Observational Studies. Book/PCORI report. https://doi.org/10.25302/01.2024/ME.2018C213289 — T1: PCORI report; subgroup analysis after PS adjustment; simulation. — *Domain:* Methods (subgroup analysis, observational).
- **c0346** — Hu (2023). Developing and Testing a New Method for Comparing More Than Two Treatments Using Electronic Health Records. Book/PCORI report. https://doi.org/10.25302/10.2023.ME.2017C39041 — T1: PCORI report; method for >2 treatments with EHR; simulations; confounding-function priors. — *Domain:* Methods (multiple treatments, EHR).
- **c0459** — Li et al. (2021). Robust estimation of heterogeneous treatment effects using electronic health record data. Stat Med. https://doi.org/10.1002/sim.8926 — T1: Robust HTE estimators (outlier-robust R-learner type); simulation + EHR. — *Domain:* Cardiovascular (antihypertensives).
- **c0505** — Chen et al. (2019). Deep representation learning for individualized treatment effect estimation using electronic health records. J Biomed Inform. https://doi.org/10.1016/j.jbi.2019.103303 — T1: Deep representation learning for ITE from EHR (learned representations). — *Domain:* Cross-domain (EHR).
- **c1703** — Junghwan Lee et al. (2024). Inverse Probability of Treatment Weighting with Deep Sequence Models Enables Accurate treatment effect Estimation from Electronic Health Records. arXiv. https://arxiv.org/abs/2406.08851v1 — T1: IPTW with deep sequence models on raw longitudinal EHR/claims; semi-synthetic evaluation (average effect focus to verify). — *Domain:* Cross-domain (EHR/claims codes).
- **c1706** — Henri Arno & Thomas Demeester (2025). Annotation-Assisted Learning of Treatment Policies From Multimodal Electronic Health Records. arXiv. https://arxiv.org/abs/2507.20993v4 — T1: Treatment policies from tabular + text EHR; semi-synthetic. — *Domain:* Cross-domain (multimodal EHR).
- **c1709** — Lei Liu et al. (2026). LLM-Extracted Covariates for Clinical Causal Inference: Rethinking Integration Strategies. Proceedings of the 11th Machine Learning for Healthcare Conference 2026. https://arxiv.org/abs/2604.16763v3 — T1: LLM-extracted covariates from notes for causal estimation; semi-synthetic. — *Domain:* Critical care (MIMIC-IV).
- **c0038** — Wang et al. (2025). A novel high dimensional approach to assess heterogeneous treatment effect in claims data. Am J Epidemiol. https://doi.org/10.1093/aje/kwaf127 — T1: High-dimensional HTE approach in claims (Wang 2025). — *Domain:* Pharmacoepidemiology (high-dimensional claims).
- **c1665** — Dennis Frauen et al. (2024). Model-agnostic meta-learners for estimating heterogeneous treatment effects over time. arXiv. https://arxiv.org/abs/2407.05287v2 — T1: Model-agnostic meta-learners for HTE over time (data to verify). — *Domain:* Cross-domain (longitudinal EHR).
- **c1701** — Rocco Zaccagnino et al. (2026). Learning Who Benefits Most: Multi-Treatment Causal Ranking for Population Health Stratification. arXiv. https://arxiv.org/abs/2610.19782v1 — T1: Multi-treatment causal ranking; semi-synthetic evaluation. — *Domain:* Population health (Italian administrative data, semi-synthetic).
- **c1707** — Ruoqi Liu et al. (2020). Estimating Individual Treatment Effects with Time-Varying Confounders. arXiv. https://arxiv.org/abs/2008.13620v2 — T1: ITE with time-varying and hidden confounders; semi-synthetic. — *Domain:* Critical care (EMR, semi-synthetic).
- **c1711** — Olivia Jullian Parra et al. (2026). Joint Treatment Effect Estimation from Incomplete Healthcare Data: Temporal Causal Normalizing Flows with LLM-driven Evolutionary MNAR Imputation. arXiv. https://arxiv.org/abs/2605.05125v1 — T1: Temporal causal normalizing flows for incomplete EHR; semi-synthetic. — *Domain:* Cross-domain (EHR, semi-synthetic).
- **M07** — Hong N, Nirantharakumar K, Yau C (2026). Structured treatment modeling in deep survival analysis via hazard factorization. Proceedings of the Conference on Health, Inference, and Learning, PMLR 333. https://proceedings.mlr.press/v333/hong26a.html — T2: Deep survival model with treatment-specific hazard factorisation and IPW subgroup assignment on EHR (PMLR page opened; PDF at raw.githubusercontent.com). — *Domain:* Cross-domain survival (EHR; data source to verify).
- **c0962** — McCoy D & Li Y (2026). Targeted Deep Survival Contrasts: Valid Inference for Treatment-Specific Survival Benefit with Neural Networks. arXiv preprint. https://arxiv.org/abs/2608.20598 — T2: Targeted deep survival contrasts with valid inference (claims application to verify). — *Domain:* Cross-domain survival (claims).
- **c1646** — Tijn Jacobs et al. (2026). Bayesian fusion forests for heterogeneous treatment effects on survival from randomised and real-world data. arXiv. https://arxiv.org/abs/2607.29295v1 — T2: Bayesian fusion forests for survival HTE combining RCT and RWD. — *Domain:* Survival (RCT + real-world cohort).
- **c0257** — Ye et al. (2025). Integrative analysis of high-dimensional RCT and RWD subject to censoring and hidden confounding. Lifetime Data Anal. https://doi.org/10.1007/s10985-025-09654-1 — T2: Integrative RCT + RWD with censoring and hidden confounding. — *Domain:* Survival (RCT + registry).
- **c0861** — Hu (2024). A new method for clustered survival data: Estimation of treatment effect heterogeneity and variable selection. Biom J. https://doi.org/10.1002/bimj.202200178 — T2: riAFT-BART HTE and variable selection; clustered survival. — *Domain:* Infection (COVID-19 inpatients).
- **c0413** — Hu et al. (2022). A flexible approach for causal inference with multiple treatments and clustered survival outcomes. Stat Med. https://doi.org/10.1002/sim.9548 — T2: riAFT-BART for multiple treatments, clustered survival, sensitivity analysis. — *Domain:* Oncology (NCDB).
- **c0788** — Shi et al. (2026). Heterogeneity in Postoperative Survival Benefit Associated With Neoadjuvant Therapy in Esophageal Squamous Cell Carcinoma: A Causal Survival Forest Analysis. Int J Cancer. https://doi.org/10.1002/ijc.70729 — T2: Causal survival forest; c-for-benefit and AUTOC reported (hospital cohort). — *Domain:* Oncology (oesophageal cancer).
- **c0790** — Xu et al. (2026). Exploring heterogeneity in survival benefit of neoadjuvant therapy for triple-negative breast cancer using causal survival forests. Eur J Surg Oncol. https://doi.org/10.1016/j.ejso.2026.112108 — T2: Causal survival forests; AUTOC, c-for-benefit, calibration. — *Domain:* Oncology (breast cancer).
- **c0039** — Ser et al. (2024). Emulation of a Target Trial to Estimate the Effect of Selective Serotonin Reuptake Inhibitors on the Development of Antimicrobial-Resistant Infections using Electronic Health Record Data and Causal Machine Learning. AMIA Annu Symp Proc. https://pubmed.ncbi.nlm.nih.gov/40417572/ — T2: Target trial emulation + causal survival forest in EHR (SSRIs). — *Domain:* Infection (antimicrobial resistance).
- **c0841** — Akahoshi et al. (2025). Heterogeneity of Survival Benefit Conferred By Letermovir. Transplant Cell Ther. https://doi.org/10.1016/j.jtct.2025.04.010 — T2: Heterogeneity of survival benefit of letermovir; causal forest. — *Domain:* Infection (CMV, transplant).
- **c0820** — Velasco-Regulez et al. (2025). The first causal inference analysis of the Catalan Arthroplasty Register shows a positive effect of antibiotic-loaded bone cement on knee prosthesis survival. J Exp Orthop. https://doi.org/10.1002/jeo2.70574 — T2: Causal survival forests on Catalan Arthroplasty Register. — *Domain:* Infection / orthopaedics (registry).
- **c0851** — Shuryak et al. (2024). Understanding the impact of radiotherapy fractionation on overall survival in a large head and neck squamous cell carcinoma dataset: a comprehensive approach combining mechanistic and machine learning models. Front Oncol. https://doi.org/10.3389/fonc.2024.1422211 — T2: Causal survival forests for radiotherapy fractionation. — *Domain:* Oncology (head and neck).
- **c0859** — Hechtman et al. (2024). Heterogeneity of Benefit from Earlier Time-to-Antibiotics for Sepsis. Am J Respir Crit Care Med. https://doi.org/10.1164/rccm.202310-1800OC — T2: Heterogeneity of benefit from earlier antibiotics; causal forest; 273,255 patients. — *Domain:* Infection (sepsis).
- **c0523** — Wang et al. (2026). Estimating Individualized Survival Benefit of Consolidative Metastasis-Directed Radiotherapy Following Chemoimmunotherapy in Nasopharyngeal Carcinoma With Exclusive Distant Metastasis. MedComm (2020). https://doi.org/10.1002/mco2.71089 — T2: Individualised survival benefit, T-learner. — *Domain:* Oncology (metastasis-directed RT).
- **c0723** — Iwamoto et al. (2026). Treatment-Effect Heterogeneity and a Simple Framework for Estimating Survival Benefit Associated With Local Therapy in Nonmetastatic Advanced Prostate Cancer: A Multicenter KAMU-ON Cohort Study. Int J Urol. https://doi.org/10.1111/iju.70668 — T2: Simple framework for survival benefit of local therapy. — *Domain:* Oncology (urology).
- **c0833** — Xu et al. (2025). Survival impact of adjuvant radiotherapy in early stage low risk elderly male breast cancer patients treated with breast conserving surgery. Sci Rep. https://doi.org/10.1038/s41598-025-17083-1 — T2: Causal forest survival benefit of adjuvant RT. — *Domain:* Oncology (male breast cancer, SEER).
- **c0473** — Seo et al. (2020). Evaluation of conditional treatment effects of adjuvant treatments on patients with synovial sarcoma using Bayesian subgroup analysis. BMC Med Inform Decis Mak. https://doi.org/10.1186/s12911-020-01305-9 — T2: Bayesian subgroup conditional effects. — *Domain:* Oncology (sarcoma, SEER).
- **c0350** — Taguchi et al. (2023). Heterogeneous treatment effects of adjuvant therapy for patients with cervical cancer in the intermediate-risk group. Cancer Med. https://doi.org/10.1002/cam4.6460 — T2: HTE of adjuvant therapy, nationwide cohort. — *Domain:* Oncology (cervical cancer).
- **c0239** — Huang et al. (2025). A partially heterogeneous weighted fusion learning method for potential heterogeneous treatment effect in multi-site survival study. BMC Med Res Methodol. https://doi.org/10.1186/s12874-025-02612-3 — T2: Weighted fusion learning for HTE in multi-site survival data; simulation + SEER. — *Domain:* Oncology (multi-site survival, SEER).
- **c0890** — Henderson et al. (2020). Individualized treatment effects with censored data via fully nonparametric Bayesian accelerated failure time models. Biostatistics. https://doi.org/10.1093/biostatistics/kxy028 — T2: Nonparametric Bayesian AFT (BART) model for ITE with censored data. — *Domain:* Survival (data source to verify).
- **c0882** — Yu et al. (2020). Developing New Methods for Determining Treatment Benefits Based on Individual Patient Traits. Book/PCORI report. https://doi.org/10.25302/10.2020.ME.140921219 — T3: PCORI report on methods for treatment benefit by patient traits (data to verify). — *Domain:* Methods (HTE, PCORI).
- **c0929** — Yadlowsky et al. (2025). Evaluating Treatment Prioritization Rules via Rank-Weighted Average Treatment Effects. J Am Stat Assoc. https://doi.org/10.1080/01621459.2024.2393466 — T3: Rank-weighted average treatment effect / Qini-type evaluation of prioritisation rules. — *Domain:* Validation metric (RATE).
- **c1050** — Yizhe Xu & Steve Yadlowsky (2022). Calibration Error for Heterogeneous Treatment Effects. International Conference on Artificial Intelligence and Statistics. https://arxiv.org/abs/2203.13364 — T3: Calibration error for heterogeneous treatment effects. — *Domain:* Validation metric (calibration).
- **c1068** — Sadatsafavi M et al. (2025). Nonparametric Assessment of the Calibration of Individualized Treatment Effects. Statistics in Medicine. https://doi.org/10.1002/sim.70724 — T3: Nonparametric assessment of ITE calibration. — *Domain:* Validation metric (calibration).
- **c0776** — Hoogland et al. (2024). Evaluating individualized treatment effect predictions: A model-based perspective on discrimination and calibration assessment. Stat Med. https://doi.org/10.1002/sim.10186 — T3: Model-based perspective on discrimination and calibration of ITE predictions. — *Domain:* Validation metric.
- **c0717** — Maas et al. (2023). Performance metrics for models designed to predict treatment effect. BMC Med Res Methodol. https://doi.org/10.1186/s12874-023-01974-w — T3: Calibration and overall performance metrics for treatment-effect models; R package. — *Domain:* Validation metric.
- **c1369** — Xia Y et al. (2022). Methodological concerns about “concordance-statistic for benefit” as a measure of discrimination in predicting treatment benefit. Diagnostic and Prognostic Research. https://doi.org/10.1186/s41512-023-00147-z — T3: Methodological concerns about c-for-benefit. — *Domain:* Validation metric.
- **c1090** — van Klaveren D et al. (2023). Measuring the performance of prediction models to personalize treatment choice: Defining observed and predicted pairwise treatment effects. Statistics in Medicine. https://doi.org/10.1002/sim.9719 — T3: Defining observed and predicted pairwise benefit for c-for-benefit. — *Domain:* Validation metric.
- **c1092** — Keogh RH & Van Geloven N (2023). Prediction Under Interventions: Evaluation of Counterfactual Performance Using Longitudinal Observational Data. Epidemiology. https://doi.org/10.1097/EDE.0000000000001713 — T3: Counterfactual performance of interventional predictions with longitudinal observational data; liver transplantation. — *Domain:* Validation (counterfactual prediction, observational).
- **c1135** — Boyer CB et al. (2023). Estimating and Evaluating Counterfactual Prediction Models. Statistics in Medicine. https://doi.org/10.1002/sim.70287 — T3: Estimating and evaluating counterfactual prediction models; statin-naive CVD risk. — *Domain:* Validation (counterfactual prediction).
- **c0930** — Palumbo (2026). Qini Curves for Potential Impact Assessment of Risk Predictive Models Informing Intervention Policies. Value Health. https://doi.org/10.1016/j.jval.2025.01.024 — T3: Qini curves for impact assessment of risk models informing interventions. — *Domain:* Validation metric (Qini).
- **c0769** — Kent et al. (2020). The Predictive Approaches to Treatment effect Heterogeneity (PATH) Statement: Explanation and Elaboration. Ann Intern Med. https://doi.org/10.7326/M18-3668 — T3: PATH statement explanation and elaboration. — *Domain:* Reporting.
- **c1375** — Xu J et al. (2022). Protocol for the development of a reporting guideline for causal and counterfactual prediction models in biomedicine. BMJ Open. https://doi.org/10.1136/bmjopen-2021-059715 — T3: Protocol for PRECOG reporting guideline (causal/counterfactual prediction models). — *Domain:* Reporting.
- **c0312** — Selby et al. (2025). Potential clinical impact of predictive modeling of heterogeneous treatment effects: scoping review of the impact of the PATH Statement. medRxiv. https://doi.org/10.1101/2024.05.06.24306774 — T3: Scoping review of PATH Statement impact. — *Domain:* Reporting.
- **c0172** — Möller et al. (2026). Estimating Heterogeneous Treatment Effects With Real-World Health Data: A Scoping Review of Machine Learning Methods. Value Health. https://doi.org/10.1016/j.jval.2026.01.013 — T3: Scoping review of ML HTE methods with real-world data; calls for evaluation and reporting standards. — *Domain:* Reporting / review (RWD).
- **c0063** — Wang & Borah (2026). Machine learning in comparative effective research of pharmacological interventions: a scoping review. Expert Rev Pharmacoecon Outcomes Res. https://doi.org/10.1080/14737167.2026.2746821 — T3: Scoping review of ML in comparative effectiveness of drugs. — *Domain:* Reporting / review (pharmacoepidemiology).
- **c0271** — Thelen & Hennessy (2025). Characterizing Treatment Effect Heterogeneity Using Real-World Data. Clin Pharmacol Ther. https://doi.org/10.1002/cpt.3627 — T3: Review of HTE methods using RWD. — *Domain:* Review (pharmacoepidemiology).
- **c1198** — Komura T et al. (2026). Estimating and discovering heterogeneous treatment effects using machine learning in epidemiological studies: a practical guide. International Journal of Epidemiology. https://doi.org/10.1093/ije/dyag092 — T3: Practical guide to HTE with ML in epidemiological studies. — *Domain:* Guidance (epidemiology).
- **c0775** — Sverdrup et al. (2025). Estimating Treatment Effect Heterogeneity in Psychiatry: A Review and Tutorial With Causal Forests. Int J Methods Psychiatr Res. https://doi.org/10.1002/mpr.70015 — T3: Review and tutorial of causal forests in psychiatry (incl. Qini/selection). — *Domain:* Mental health (guidance).
- **c0263** — Abécassis et al. (2025). From Prediction to Prescription: Machine Learning and Causal Inference for the Heterogeneous Treatment Effect. Annu Rev Biomed Data Sci. https://doi.org/10.1146/annurev-biodatasci-103123-095750 — T3: Prediction to prescription: ML and causal inference for HTE (claims/EHR). — *Domain:* Review.
- **c1353** — Brantner CL et al. (2023). Methods for Integrating Trials and Non-experimental Data to Examine Treatment Effect Heterogeneity. Statistical Science. https://doi.org/10.1214/23-sts890 — T3: Methods integrating trials and non-experimental data for HTE. — *Domain:* Review.
- **c1242** — Anon (2025). Direct Effect Modeling Methods to Estimate Heterogeneity of Treatment Effects. JAMA Network Open. https://doi.org/10.1001/jamanetworkopen.2025.22397 — T3: JAMA Netw Open guide to direct effect modelling for HTE (abstract not available in record). — *Domain:* Reporting / guidance.
- **c1428** — Anon (2021). Reporting heterogeneity of treatment effects. Headache. https://doi.org/10.1111/head.14083 — T3: Reporting heterogeneity of treatment effects (Headache; abstract not available in record). — *Domain:* Reporting.
- **c0493** — Watson & Holmes (2020). Graphing and reporting heterogeneous treatment effects through reference classes. Trials. https://doi.org/10.1186/s13063-020-04306-1 — T3: Graphing and reporting HTE through reference classes. — *Domain:* Reporting (RCT).
- **c1093** — Chalkou K et al. (2023). Combining randomized and non‐randomized data to predict heterogeneous effects of competing treatments. Research Synthesis Methods. https://doi.org/10.1002/jrsm.1717 — T4: Combining randomised and non-randomised data for HTE of competing treatments (data to verify). — *Domain:* Neurology (MS) / evidence synthesis.
- **c0353** — Yang et al. (2023). Elastic integrative analysis of randomised trial and real-world data for treatment heterogeneity estimation. J R Stat Soc Series B Stat Methodol. https://doi.org/10.1093/jrsssb/qkad017 — T4: Elastic integrative analysis of trial and real-world data for HTE. — *Domain:* Methods (RCT + RWD).
- **c0339** — Wu & Yang (2023). Transfer learning of individualized treatment rules from experimental to real-world data. J Comput Graph Stat. https://doi.org/10.1080/10618600.2022.2141752 — T4: Transfer learning of ITRs from experimental to real-world data. — *Domain:* Methods (RCT to RWD).
- **c0422** — Moler-Zapata et al. (2022). Local Instrumental Variable Methods to Address Confounding and Heterogeneity when Using Electronic Health Records: An Application to Emergency Surgery. Med Decis Making. https://doi.org/10.1177/0272989X221100799 — T4: Local IV methods in EHR for confounding and heterogeneity. — *Domain:* Surgery (emergency).
- **c0469** — Adhikari et al. (2020). Nonparametric Bayesian Instrumental Variable Analysis: Evaluating Heterogeneous Effects of Coronary Arterial Access Site Strategies. J Am Stat Assoc. https://doi.org/10.1080/01621459.2019.1688663 — T4: Nonparametric Bayesian IV for heterogeneous effects (registry). — *Domain:* Cardiovascular (PCI access).
- **c0229** — Wang et al. (2025). Glucagon-like Peptide-1 Receptor Agonists in Asthma Exacerbations: An Application of High-Dimensional Iterative Causal Forest to Identify Subgroups. Pharmacoepidemiol Drug Saf. https://doi.org/10.1002/pds.70192 — T4: hdiCF applied in claims: GLP-1 RA and asthma exacerbations. — *Domain:* Respiratory (asthma).
- **c0046** — Wang et al. (2024). Glucagon-like Peptide 1 Receptor Agonists and Asthma Exacerbations: Which Patients Benefit Most?. Ann Am Thorac Soc. https://doi.org/10.1513/AnnalsATS.202309-836OC — T4: GLP-1 RA and asthma exacerbations: which patients benefit (claims, causal forest). — *Domain:* Respiratory (asthma).
- **c1094** — Venkatasubramaniam et al. (2022). Comparison of causal forest and regression-based approaches to evaluate treatment effect heterogeneity: an application for type 2 diabetes precision medicine. BMC Medical Informatics and Decision Making. https://doi.org/10.1186/s12911-023-02207-2 — T4: Causal forest vs regression; trial-developed, CPRD-validated. — *Domain:* Type 2 diabetes (methods comparison; covered in Brief 3).
- **c0294** — Lugo-Palacios et al. (2025). Going beyond randomised controlled trials to assess treatment effect heterogeneity across target populations. Health Econ. https://doi.org/10.1002/hec.4903 — T4: Beyond RCTs to assess HTE across target populations (CPRD). — *Domain:* Type 2 diabetes (methods; covered in Brief 3).
- **c0231** — Dai et al. (2025). Variational temporal deconfounder network for individualized treatment effect estimation with longitudinal observational data. J Biomed Inform. https://doi.org/10.1016/j.jbi.2025.104880 — T4: Variational temporal deconfounder network for ITE. — *Domain:* Critical care (MIMIC-III).
- **c0111** — Chen et al. (2025). FEDERATED LEARNING OF ROBUST INDIVIDUALIZED DECISION RULES WITH APPLICATION TO HETEROGENEOUS MULTIHOSPITAL SEPSIS POPULATION. Ann Appl Stat. https://doi.org/10.1214/25-aoas2017 — T4: Federated robust individualised decision rules. — *Domain:* Infection (sepsis, multi-hospital EHR).
- **c0139** — Yin et al. (2026). Federated Inverse Probability Treatment Weighting for Individual Treatment Effect Estimation. ACM Trans Intell Syst Technol. https://doi.org/10.1145/3787464 — T4: Federated IPTW for ITE. — *Domain:* Critical care (eICU).
- **c0137** — Yuan et al. (2026). Revised Deep Learning Semiparametric Regression for Testing and Estimating Treatment Effect Heterogeneity in Observational Studies: A Lung Transplant Case Study. bioRxiv. https://doi.org/10.64898/2026.04.13.718254 — T4: Deep semiparametric regression for testing/estimating HTE. — *Domain:* Respiratory (lung transplant registry).
- **c1653** — Xiaodi Li et al. (2026). Optimizing Clinical Trial Protocols Using EHR-Derived Heterogeneous Treatment Effects. arXiv. https://arxiv.org/abs/2607.16934v1 — T4: EHR-derived HTE to optimise trial protocols. — *Domain:* Cross-domain (EHR trial emulation).
- **c0283** — Jo et al. (2024). Machine learning evaluation of intensified conditioning on haematopoietic stem cell transplantation in adult acute lymphoblastic leukemia patients. Commun Med (Lond). https://doi.org/10.1038/s43856-024-00680-y — T4: Bayesian causal forest for intensified conditioning. — *Domain:* Oncology (HSCT registry).
- **c0403** — Jiao et al. (2022). Does Clinical Evidence of Heterogeneity Impact Treatment Selection? A Case Study of Abiraterone for Metastatic Prostate Cancer. J Natl Compr Canc Netw. https://doi.org/10.6004/jnccn.2022.7044 — T4: Does evidence of heterogeneity change treatment selection (EMR). — *Domain:* Oncology (prostate).
- **c0425** — van Amsterdam et al. (2022). Individual treatment effect estimation in the presence of unobserved confounding using proxies: a cohort study in stage III non-small cell lung cancer. Sci Rep. https://doi.org/10.1038/s41598-022-09775-9 — T4: ITE with proxies for unobserved confounding. — *Domain:* Oncology (NSCLC).
- **c0050** — Ngufor et al. (2023). Identifying treatment heterogeneity in atrial fibrillation using a novel causal machine learning method. Am Heart J. https://doi.org/10.1016/j.ahj.2023.02.015 — T4: Novel causal ML method for HTE in AF (OptumLabs claims; trial comparison to verify). — *Domain:* Cardiovascular (AF).
- **c0051** — Marafino et al. (2020). Predicting preventable hospital readmissions with causal machine learning. Health Serv Res. https://doi.org/10.1111/1475-6773.13586 — T4: Causal ML to target preventable readmissions (EHR). — *Domain:* Health services (readmissions).
- **c0435** — Meid et al. (2022). Can Machine Learning from Real-World Data Support Drug Treatment Decisions? A Prediction Modeling Case for Direct Oral Anticoagulants. Med Decis Making. https://doi.org/10.1177/0272989X211064604 — T4: ITE from claims for DOAC choice; X-learner; c-for-benefit. — *Domain:* Cardiovascular (DOAC).
- **c0994** — Watanabe et al. (2025). Machine learning-based high-benefit approach versus traditional high-risk approach in statin therapy: the Shizuoka Kokuho database study. Scientific Reports. https://doi.org/10.1038/s41598-025-11236-y — T4: High-benefit (causal forest) vs high-risk approach. — *Domain:* Cardiovascular (statins, Japanese claims).
- **c0925** — Chen et al. (2025). Machine Learning to Predict Individualized Treatment Effects of Sodium Bicarbonate for Patients With Out-of-Hospital Cardiac Arrest. Crit Care Med. https://doi.org/10.1097/CCM.0000000000006792 — T4: ITE of sodium bicarbonate; c-for-benefit, Qini. — *Domain:* Cardiovascular (OHCA).
- **c0927** — Huber et al. (2025). Uplift modeling to determine which fluid-norepinephrine regime results in a postoperative acute kidney injury-free recovery in patients scheduled for cystectomy and urinary diversions. Front Med (Lausanne). https://doi.org/10.3389/fmed.2025.1542797 — T4: Uplift modelling with Qini. — *Domain:* Renal (postoperative AKI).
- **c0936** — Li et al. (2024). Uplift modeling to predict individual treatment effects of renal replacement therapy in sepsis-associated acute kidney injury patients. Sci Rep. https://doi.org/10.1038/s41598-024-55653-x — T4: Uplift modelling for RRT ITE; Qini. — *Domain:* Renal (sepsis-associated AKI).
- **c1814** — Oh et al. (2025). Personalized Fluid Management in Patients with Sepsis and AKI: A Policy Tree Approach. medRxiv. https://doi.org/10.1101/2024.08.06.24311556 — T4: Policy tree for restrictive fluids. — *Domain:* Renal (sepsis + AKI).
- **c0091** — Nakamura et al. (2026). Heterogeneous Treatment Effects of Renal Replacement Therapy in Critically Ill Patients: A Multicenter Observational Study Using a Japanese ICU Registry. Crit Care Med. https://doi.org/10.1097/CCM.0000000000007282 — T4: HTE of RRT, multicentre; causal forest; trial comparison to verify. — *Domain:* Renal (RRT, ICU).
- **c1832** — Yu & Qin (2026). Machine learning phenotypes and heterogeneous albumin effects in cirrhotic AKI: a causal inference study. Intern Emerg Med. https://doi.org/10.1007/s11739-026-04446-3 — T4: ML phenotypes and heterogeneous albumin effects. — *Domain:* Renal / hepatology (cirrhotic AKI).
- **c1833** — Kang et al. (2025). Exploring the therapeutic effects of continuous kidney replacement therapy in patients with severe acidosis using deep learning-based causal inference. Sci Rep. https://doi.org/10.1038/s41598-025-20555-z — T4: Therapeutic effects of CKRT, causal ML. — *Domain:* Renal (CKRT in acidosis).
- **c0135** — Tseng et al. (2026). Multifactorial attribution for vancomycin-associated acute kidney injury. Br J Clin Pharmacol. https://doi.org/10.1002/bcp.70592 — T4: X-learner attribution in EHR. — *Domain:* Renal / infection (vancomycin AKI).
- **c0373** — Liu et al. (2023). Estimating treatment effects for time-to-treatment antibiotic stewardship in sepsis. Nat Mach Intell. https://doi.org/10.1038/s42256-023-00638-0 — T4: Time-to-treatment antibiotic effects (Nat Mach Intell). — *Domain:* Infection (sepsis, MIMIC).
- **c0455** — Han et al. (2021). Identifying High-Risk Subphenotypes and Associated Harms From Delayed Antibiotic Orders and Delivery. Crit Care Med. https://doi.org/10.1097/CCM.0000000000005054 — T4: Subphenotypes and harms from delayed antibiotics; causal forests (EHR). — *Domain:* Infection (sepsis).
- **c0812** — Zhang et al. (2026). Early Antibiotic Therapy in Sepsis Without Shock: A Multimethod Study of Heterogeneous Treatment Effects in ICU Patients. Infect Dis Ther. https://doi.org/10.1007/s40121-026-01316-5 — T4: Multimethod HTE of early antibiotics. — *Domain:* Infection (sepsis).
- **c1290** — Yan et al. (2024). Identifying Veterans Who Benefit From Nirmatrelvir-Ritonavir: A Target Trial Emulation. Clinical Infectious Diseases. https://doi.org/10.1093/cid/ciae202 — T4: Who benefits from nirmatrelvir-ritonavir; target trial emulation. — *Domain:* Infection (COVID-19, VA).
- **c0225** — Mengistu et al. (2025). Application of causal forest double machine learning (DML) approach to assess tuberculosis preventive therapy's impact on ART adherence. Sci Rep. https://doi.org/10.1038/s41598-025-14460-8 — T4: Causal forest DML for TB preventive therapy. — *Domain:* Infection (TB/HIV).
- **c1106** — Lan Y et al. (2026). Heterogeneity in the Association Between Pneumococcal Vaccination and the Risk of Severe Community-Acquired Pneumonia in Elderly Inpatients: A Causal Forest Analysis. Vaccines. https://doi.org/10.3390/vaccines14010090 — T4: Causal forest heterogeneity in elderly. — *Domain:* Infection / respiratory (pneumococcal vaccine).
- **c1817** — Lengerich et al. (2022). Automated interpretable discovery of heterogeneous treatment effectiveness: A COVID-19 case study. J Biomed Inform. https://doi.org/10.1016/j.jbi.2022.104086 — T4: Automated interpretable discovery of HTE (multitask ML). — *Domain:* Infection (COVID-19).
- **c0014** — Krakowski et al. (2026). Development and validation of a precision treatment rules for first-line antipsychotic recommendations in first episode psychosis jointly incorporating effectiveness, side effects and patient preferences. Transl Psychiatry. https://doi.org/10.1038/s41398-026-03914-w — T4: Precision treatment rules for antipsychotics (EHR). — *Domain:* Mental health (first-episode psychosis).
- **c0033** — Nuutinen et al. (2025). Effect of discontinuing antipsychotic medications on the risk of hospitalization in long-term care: a machine learning-based analysis. BMC Med. https://doi.org/10.1186/s12916-025-04304-7 — T4: Causal forest, DML, X-learner in long-term care registry. — *Domain:* Mental health (antipsychotic discontinuation).
- **c0165** — Dedebant et al. (2026). Treatment Effects of Cholinesterase Inhibitors in Alzheimer's Disease: a Causal Machine Learning Approach. medRxiv. https://doi.org/10.64898/2026.02.11.26346078 — T4: Causal ML for cholinesterase inhibitors (cohort/registry). — *Domain:* Mental health / neurology (Alzheimer).
- **M05** — Nagpal C, Wei D, Vinzamuri B, Shekhar M, Berger SE, Das S, Varshney KR (2020). Interpretable subgroup discovery in treatment effect estimation with application to opioid prescribing guidelines. ACM CHIL 2020. https://arxiv.org/abs/1905.03297v3 — T4: Interpretable subgroup discovery in claims (CHIL 2020). — *Domain:* Mental health / pharmacoepidemiology (opioids).
- **c0908** — Malkki et al. (2026). Targeted Learning for Optimal Patient Assignment to Psychotherapy. Psychother Res. https://doi.org/10.1080/10503307.2025.2517567 — T4: Targeted learning for optimal assignment (registry). — *Domain:* Mental health (psychotherapy).
- **c0153** — Surcinelli et al. (2026). Comparative effectiveness of anti-CD20 therapies and S1P receptor modulators in late-onset multiple sclerosis: real-world evidence from the MSBase registry. Ther Adv Neurol Disord. https://doi.org/10.1177/17562864261430084 — T4: Causal forest in late-onset MS registry. — *Domain:* Neurology (MS).
- **c0348** — Jiang et al. (2023). Overall and patient-specific comparative effectiveness of dimethyl fumarate versus teriflunomide: A novel approach to precision medicine applied to the German NeuroTrans Data Multiple Sclerosis Registry. Mult Scler J Exp Transl Clin. https://doi.org/10.1177/20552173231194353 — T4: Patient-specific comparative effectiveness DMF vs teriflunomide (registry). — *Domain:* Neurology (MS).
- **c0412** — Simoneau et al. (2022). Overall and patient-level comparative effectiveness of dimethyl fumarate and fingolimod: A precision medicine application to the Observatoire Français de la Sclérose en Plaques registry. Mult Scler J Exp Transl Clin. https://doi.org/10.1177/20552173221116591 — T4: Patient-level comparative effectiveness DMF vs fingolimod (registry). — *Domain:* Neurology (MS).
- **c0228** — Andersson et al. (2026). Predicting high excess risk of hyponatraemia among thiazide users. Eur J Prev Cardiol. https://doi.org/10.1093/eurjpc/zwaf474 — T4: Excess risk of hyponatraemia; causal forest; calibration. — *Domain:* Pharmacoepidemiology (thiazides).
- **c0061** — Terry et al. (2026). Identification of Heterogenous Treatment Response to Corticosteroids Among Patients With Ventilator-Dependent Respiratory Failure: An Observational Cohort Study. CHEST Crit Care. https://doi.org/10.1016/j.chstcc.2026.100258 — T4: Heterogeneous corticosteroid response; MIMIC-III; DR. — *Domain:* Respiratory (ventilator-dependent failure).
- **c0528** — Fang et al. (2026). Machine Learning Prediction and Causal Forest Analysis of Severe Acute Kidney Injury in ICU Patients with COPD: A MIMIC-IV Study. Int J Chron Obstruct Pulmon Dis. https://doi.org/10.2147/COPD.S611985 — T4: Causal forest for severe AKI in COPD (MIMIC-IV). — *Domain:* Respiratory (COPD in ICU).
- **c0079** — Nguyen et al. (2026). Personalized comfort settings in positive airway pressure machines using a causal inference approach: a retrospective observational analysis. Front Sleep. https://doi.org/10.3389/frsle.2026.1883557 — T4: Causal forest for PAP comfort settings (Medicare/Medicaid?). — *Domain:* Respiratory (sleep apnoea PAP).
- **c0080** — Lu et al. (2026). Heterogeneous effects of preoperative beta blockers on 30-day mortality after coronary artery bypass surgery. Ann Med. https://doi.org/10.1080/07853890.2026.2719256 — T4: Causal forest for preoperative beta blockers (registry). — *Domain:* Cardiovascular (CABG).
- **c0155** — Hassan et al. (2026). Causal Machine Learning for Personalized Surgical Decision-Making in Aortic Dissection: A National Fairness-Aware Clinical AI Framework. Ann Vasc Surg. https://doi.org/10.1016/j.avsg.2026.03.031 — T4: Causal forest/DML with calibration (national insurance data). — *Domain:* Cardiovascular (aortic dissection).
- **c0240** — Zhang et al. (2025). AI-based identification of patients who benefit from revascularization: a multicenter study. medRxiv. https://doi.org/10.1101/2025.06.11.25329295 — T4: AI to identify benefit; registry and trial comparison. — *Domain:* Cardiovascular (revascularisation).
- **c1136** — Lolak S et al. (2023). Application of Dragonnet and Conformal Inference for Estimating Individualized Treatment Effects for Personalized Stroke Prevention: Retrospective Cohort Study. JMIR Cardio. https://doi.org/10.2196/50627 — T4: Dragonnet with conformal inference. — *Domain:* Cardiovascular (stroke prevention).
- **c0261** — Tran et al. (2025). A Transformer-Based Framework for Counterfactual Estimation of Antihypertensive Treatment Effect on COVID-19 Infection Risk - A Proof-of-Concept Study. Am J Hypertens. https://doi.org/10.1093/ajh/hpaf055 — T4: Transformer counterfactual estimation of antihypertensive effect on COVID-19. — *Domain:* Cardiovascular / infection.
- **c0009** — Yu (2026). Crossover effect: causal machine learning reveals opposing mortality responses to mean arterial pressure targets among phenotypically distinct hypertensive patients with septic shock. Intern Med J. https://doi.org/10.1111/imj.70515 — T4: T-learner causal ML in ICU database. — *Domain:* Critical care (MAP targets).
- **M06** — Virkud A, Edwards JK, Jonsson Funk M, Chang P, Kshirsagar AV, Gower EW, Kosorok MR (2025). Using statistical precision medicine to identify optimal treatments in a heart failure setting. arXiv preprint. https://arxiv.org/abs/2501.07789v1 — T4: Statistical precision medicine algorithms in a heart failure setting. — *Domain:* Cardiovascular (heart failure).
- **c0355** — Yang et al. (2024). Tree-based subgroup discovery using electronic health record data: heterogeneity of treatment effects for DTG-containing therapies. Biostatistics. https://doi.org/10.1093/biostatistics/kxad014 — T4: Tree-based subgroup discovery using EHR (Biostatistics 2024); TMLE. — *Domain:* Infection (HIV, dolutegravir ART).
- **c0454** — Qi et al. (2021). Explaining heterogeneity of individual treatment causal effects by subgroup discovery: An observational case study in antibiotics treatment of acute rhino-sinusitis. Artif Intell Med. https://doi.org/10.1016/j.artmed.2021.102080 — T4: Subgroup discovery explaining ITE heterogeneity; 24,392 primary-care patients. — *Domain:* Infection (antibiotics, primary care).
- **c0519** — Winn et al. (2019). Using Group-based Trajectory Models and Propensity Score Weighting to Detect Heterogeneous Treatment Effects: The Case Study of Generic Hormonal Therapy for Women With Breast Cancer. Med Care. https://doi.org/10.1097/MLR.0000000000001019 — T4: Group-based trajectory models + PS weighting to detect HTE. — *Domain:* Oncology (SEER-Medicare).
- **c0323** — Lee et al. (2023). Heterogeneous Treatment Effect Estimation with Subpopulation Identification for Personalized Medicine in Opioid Use Disorder. Proc IEEE Int Conf Data Min. https://doi.org/10.1109/icdm58522.2023.00127 — T4: HTE with subpopulation identification (data source to verify). — *Domain:* Mental health (opioid use disorder).
- **c0371** — Ghosh et al. (2022). DR-VIDAL - Doubly Robust Variational Information-theoretic Deep Adversarial Learning for Counterfactual Prediction and Treatment Effect Estimation on Real World Data. AMIA Annu Symp Proc. https://doi.org/10.21203/rs.3.rs-1055169/v1 — T4: DR-VIDAL deep doubly robust counterfactual model. — *Domain:* Cross-domain (EHR/registry).
- **c1657** — Theresa Blümlein et al. (2022). Learning Optimal Dynamic Treatment Regimes Using Causal Tree Methods in Medicine. In Machine Learning for Healthcare Conference (pp. 146-171). PMLR 2022. https://arxiv.org/abs/2204.07124v2 — T4: Optimal dynamic treatment regimes with causal tree methods in EHR. — *Domain:* Cross-domain (EHR).
- **c0109** — Zhao et al. (2026). Comparative effectiveness and safety of proton pump inhibitors after myocardial infarction on dual antiplatelet therapy: Insights from a target trial emulation. Br J Clin Pharmacol. https://doi.org/10.1002/bcp.70650 — T4: Target trial emulation in EHR with risk-based (XGBoost prognostic) HTE. — *Domain:* Cardiovascular / pharmacoepidemiology (PPIs after MI).
- **c0291** — Moler-Zapata et al. (2024). An Approach for Combining Clinical Judgment with Machine Learning to Inform Medical Decision Making: Analysis of Nonemergency Surgery Strategies for Acute Appendicitis in Patients with Multiple Long-Term Conditions. Med Decis Making. https://doi.org/10.1177/0272989X241289336 — T4: Combining clinical judgement with ML for subgroup comparative effectiveness. — *Domain:* Health services (administrative data, N=24,312).
- **c0477** — Meid et al. (2020). Using the Causal Inference Framework to Support Individualized Drug Treatment Decisions Based on Observational Healthcare Data. Clin Epidemiol. https://doi.org/10.2147/CLEP.S274466 — T4: Concept for routine-data prediction-based individualised drug decision rules. — *Domain:* Pharmacoepidemiology (concept).
- **c0502** — Lauve et al. (2020). LocalControl: An R Package for Comparative Safety and Effectiveness Research. J Stat Softw. https://doi.org/10.18637/jss.v096.i04 — T4: LocalControl R package for comparative safety/effectiveness (incl. competing risks). — *Domain:* Pharmacoepidemiology (software).
- **c0093** — Zhang et al. (2026). Severity-stratified vasopressor-escalation strategies in septic shock: a cross-fitted doubly robust analysis with external replication. Front Pharmacol. https://doi.org/10.3389/fphar.2026.1876555 — T4: Cross-fitted doubly robust severity-stratified analysis with external replication. — *Domain:* Infection (septic shock, MIMIC-IV/eICU).
- **c0083** — Fan et al. (2026). Peritonitis and Mortality Risks of Gastric Acid Suppressants in Patients Undergoing Peritoneal Dialysis. Kidney Int Rep. https://doi.org/10.1016/j.ekir.2026.106991 — T5: Acid suppressants and peritonitis/mortality (EHR); HTE component to verify. — *Domain:* Renal (peritoneal dialysis).
- **c0377** — Seib et al. (2023). Estimated Effect of Parathyroidectomy on Long-Term Kidney Function in Adults With Primary Hyperparathyroidism. Ann Intern Med. https://doi.org/10.7326/M22-2222 — T5: Effect on kidney function; heterogeneity to verify. — *Domain:* Renal (parathyroidectomy, VA).
- **c2042** — Goto et al. (2025). Polygenic scores for precision psychiatry: a study on the effect heterogeneity of antidepressants. medRxiv. https://doi.org/10.1101/2024.11.02.24316657 — T5: Polygenic scores and HTE of antidepressants (data source to verify). — *Domain:* Mental health (antidepressants).
- **c0922** — Emran & Al Islam (2026). Domain adaptive uplift modeling across heterogeneous mental health cohorts. iScience. https://doi.org/10.1016/j.isci.2026.116027 — T5: Domain-adaptive uplift across cohorts (data to verify). — *Domain:* Mental health.
- **c0021** — Chen & Li (2026). Early metoprolol use in ICU patients with congestive heart failure is associated with increased 30-day mortality: a causal machine learning study. Front Pharmacol. https://doi.org/10.3389/fphar.2026.1771969 — T5: Causal forest, MIMIC-IV. — *Domain:* Cardiovascular (ICU heart failure).
- **c0069** — Chen et al. (2026). Endovascular Thrombectomy for Minor Ischemic Stroke: A Machine Learning Study of Treatment Effect Heterogeneity. AJNR Am J Neuroradiol. https://doi.org/10.3174/ajnr.A9622 — T5: Causal forest, nationwide database. — *Domain:* Cardiovascular / neurology (stroke EVT).
- **c0174** — Doheim et al. (2026). Individualized Treatment in Distal and Medium Vessel Occlusion Stroke Using a Validated Explainable Counterfactual Treatment Estimation Model. Ann Neurol. https://doi.org/10.1002/ana.78168 — T5: Counterfactual T-learner model. — *Domain:* Cardiovascular / neurology (stroke DMVO).
- **c0152** — Duan et al. (2026). Heterogeneity of Treatment Effect for Intra-Aortic Balloon Pump Use Across Lactate Trajectories in Cardiogenic Shock Patients Supported by VA-ECMO: An Analysis of the Chinese Extracorporeal Life Support Registry. MedComm (2020). https://doi.org/10.1002/mco2.70698 — T5: HTE across lactate trajectories (registry). — *Domain:* Cardiovascular (IABP).
- **c0013** — Kiltz et al. (2026). Using causal machine learning and real world data to improve dose response decision making for secukinumab in psoriatic arthritis. Sci Rep. https://doi.org/10.1038/s41598-026-47976-8 — T5: DML for secukinumab dose-response with RWD. — *Domain:* Rheumatology.
- **c0187** — Tani et al. (2025). Effectiveness of rehabilitation dose heterogeneity for improving functional outcomes of patients with acute stroke: a nationwide observational study. Sci Rep. https://doi.org/10.1038/s41598-025-32006-w — T5: Causal forest, nationwide database. — *Domain:* Stroke rehabilitation.
- **c0147** — Tani et al. (2026). Heterogeneity in the Effectiveness of Rehabilitation Dose on Activities of Daily Living in Post-Acute Stroke: Target Trial Emulation. J Am Med Dir Assoc. https://doi.org/10.1016/j.jamda.2026.106202 — T5: Doubly robust HTE of rehabilitation dose (claims). — *Domain:* Stroke rehabilitation.
- **c0017** — Jiang et al. (2026). Comparative Mortality Risk of Aripiprazole, Olanzapine, Quetiapine, and Risperidone in Alzheimer's Disease: A Real‑World Retrospective Cohort Study with Treatment Effect Heterogeneity Analysis. CNS Drugs. https://doi.org/10.1007/s40263-026-01286-9 — T5: TMLE + causal ML HTE in Truveta EHR. — *Domain:* Mental health (antipsychotics in Alzheimer disease).
- **c1812** — Shen et al. (2025). Analysis of the heterogeneous treatment effect of vasoactive drug dosage and time on hospital mortality across different sepsis phenotypes: a retrospective cohort study. Eur J Med Res. https://doi.org/10.1186/s40001-025-02660-x — T5: HTE of vasoactive dose/time by phenotype. — *Domain:* Infection (sepsis, MIMIC-IV/eICU).
- **c0084** — You et al. (2026). Intra-aortic balloon pump use and in-hospital mortality in acute myocardial infarction with Killip class III or IV: a nationwide cohort study. Biomark Res. https://doi.org/10.1186/s40364-026-00993-1 — T5: BART-based heterogeneity. — *Domain:* Cardiovascular (IABP in AMI, nationwide).
- **c0806** — Kang et al. (2026). Impact of post-transfusion hemoglobin levels on survival in critically Ill patients: a machine learning-based causal inference analysis. Sci Rep. https://doi.org/10.1038/s41598-026-50363-y — T5: Causal forest + DML. — *Domain:* Critical care (transfusion, MIMIC/eICU).
- **c0831** — Yang et al. (2025). Investigating the feasibility of machine learning to guide personalized red blood cell (RBC) transfusion: analyzing the heterogeneity of RBC transfusion in septic patients with hemoglobin levels of 7-9 g/dL based on the causal forest model. Front Pharmacol. https://doi.org/10.3389/fphar.2025.1615618 — T5: Causal forest heterogeneity. — *Domain:* Critical care (RBC transfusion, MIMIC).
- **c0807** — Sohn et al. (2026). Individualized strategy of treatment for ruptured abdominal aortic aneurysm using causal inference model: a retrospective observational study. Ann Surg Treat Res. https://doi.org/10.4174/astr.2026.110.4.259 — T5: X-learner individualised strategy with calibration. — *Domain:* Cardiovascular (ruptured AAA).
- **c0808** — Vattipally et al. (2026). Variable Treatment Effects of Cranial Surgery in Pediatric Severe Traumatic Brain Injury. Neurosurgery. https://doi.org/10.1227/neu.0000000000003997 — T5: Causal forest variable treatment effects. — *Domain:* Neurosurgery (paediatric TBI database).
- **c0813** — Nelson et al. (2026). Survival effect of prehospital emergency anaesthesia with intubation in risk-stratified patients with major trauma: a causal modelling study. Lancet Respir Med. https://doi.org/10.1016/S2213-2600(25)00370-4 — T5: Doubly robust survival effect in risk strata. — *Domain:* Trauma (prehospital anaesthesia, registry).
- **c0795** — Lasington et al. (2026). Causal Effects of Endoscopy Timing on Outcomes in Critically Ill Patients With Upper Gastrointestinal Bleeding: A Double Machine Learning Analysis. Cureus. https://doi.org/10.7759/cureus.112126 — T5: DML. — *Domain:* Critical care (UGIB endoscopy timing, MIMIC-IV).
- **c0893** — Jiang et al. (2026). Heterogeneity in the association between antihypertensive medications and Alzheimer's disease and related dementias risk: A multidimensional machine learning analysis to inform drug repurposing. J Alzheimers Dis. https://doi.org/10.1177/13872877261469115 — T5: Heterogeneity of antihypertensive associations with ADRD. — *Domain:* Cardiovascular / dementia (Medicare).
- **c1056** — Anon (2024). Causal Forest Models with Double Machine Learning for Heterogeneous Treatment Effects in Antihypertensive Therapy: A Position Paper on Personalized Prescribing from Observational EHR Data. Journal of Artificial Intelligence for Healthcare Systems. https://doi.org/10.68159/e366460051 — T5: Causal forest + DML position paper (abstract empty in record). — *Domain:* Cardiovascular (antihypertensives, EHR).
- **c0369** — Mizuguchi & Sawamura (2023). Machine learning-based causal models for predicting the response of individual patients to dexamethasone treatment as prophylactic antiemetic. Sci Rep. https://doi.org/10.1038/s41598-023-34505-0 — T5: DML / DR causal models. — *Domain:* Pharmacoepidemiology (dexamethasone prophylaxis, EHR).
- **c0011** — Rekkas et al. (2026). Feasibility of Causality-Aware Machine Learning for Drug Safety on OMOP-CDM. Stud Health Technol Inform. https://doi.org/10.3233/SHTI260141 — T5: Feasibility of causality-aware ML on OMOP-CDM. — *Domain:* Pharmacoepidemiology (drug safety, OMOP).
- **c0086** — Chen et al. (2026). Endovascular thrombectomy versus medical management in patients with dementia and acute ischaemic stroke. Age Ageing. https://doi.org/10.1093/ageing/afag241 — T5: Interaction and subgroup analyses after PS matching. — *Domain:* Cardiovascular / neurology (EVT in dementia, NRD).
- **c0206** — Chen et al. (2026). Middle meningeal artery embolization as a surgical adjunct for non-acute subdural hematoma: real world outcomes and treatment effect heterogeneity. J Neurointerv Surg. https://doi.org/10.1136/jnis-2025-024312 — T5: Sources of treatment effect heterogeneity explored (nationwide data). — *Domain:* Neurosurgery (MMA embolization).
- **c0269** — Tapper et al. (2025). Testosterone Replacement Reduces Morbidity and Mortality for Most Patients With Cirrhosis. Clin Gastroenterol Hepatol. https://doi.org/10.1016/j.cgh.2025.02.004 — T5: Target trial emulation; substantial HTE across subgroups. — *Domain:* Hepatology (testosterone in cirrhosis).
- **c1114** — Anon (2025). Variation in effectiveness of blood transfusion by hospital day: a multi-center retrospective study. Journal of Hospital Medicine. https://doi.org/10.1002/jhm.70133 — T5: Heterogeneity of transfusion effect by hospital day. — *Domain:* Critical care (transfusion timing, Premier).
- **c0842** — Chaudhuri & Das (2025). Heterogeneous treatment effects of BCG vaccine on Alzheimer's disease risk. J Alzheimers Dis Rep. https://doi.org/10.1177/25424823251317955 — T5: ML HTE in retrospective cohort. — *Domain:* Neurology / oncology (BCG and ADRD).
- **c0097** — Zhou et al. (2026). Progression-free survival outcomes of PARP inhibitors in ovarian cancer: an exploratory analysis of treatment heterogeneity based on organ vulnerability. Front Oncol. https://doi.org/10.3389/fonc.2026.1768842 — T5: Causal forest + G-computation, n=479. — *Domain:* Oncology (PARP inhibitors, small cohort).
- **c0198** — Baird et al. (2025). Toward precision stroke rehabilitation: an integrated causal machine learning and clinician feedback approach. JAMIA Open. https://doi.org/10.1093/jamiaopen/ooaf146 — T5: Causal ML with clinician feedback. — *Domain:* Stroke rehabilitation (n=484).
- **c0332** — Feng et al. (2024). Real-World Effectiveness of Lung Cancer Screening Using Deep Learning-Based Counterfactual Prediction. Stud Health Technol Inform. https://doi.org/10.3233/SHTI230999 — T5: DL-based ITE methods in a cohort. — *Domain:* Oncology (lung cancer screening).

Total: 156 entries; c0396 is a duplicate merged into Row 17, so it is not counted separately. c0023 is excluded here because it has a full card (Row 41).

## 2G. Domain coverage

Counts are over all 197 included papers (excluding the merged duplicate c0396). A paper can count in more than one domain. The second column counts papers with full cards (Rows 1–41), using the domain labels in the table that follows.

| Domain | Included (all) | With full card |
|---|---|---|
| Cardiovascular | 30 | 9 |
| Oncology | 22 | 5 |
| Infection | 25 | 6 |
| Mental health | 13 | 3 |
| Renal | 10 | 1 |
| Respiratory | 8 | 2 |
| Pharmacoepidemiology (general / high-dimensional codes) | 21 | 7 |

Domain of each paper with a full card:

| Row | id | Domain |
|---|---|---|
| 1 | S01 | Pharmacoepidemiology (general); cardiovascular |
| 2 | M01 | Health policy |
| 3 | M02 | Health policy |
| 4 | c0203 | Surgery/devices |
| 5 | S02 | Pharmacoepidemiology (general) |
| 6 | c0664 | Mental health (KPWA depression treatment); pharmacoepidemiology |
| 7 | c1716 | Critical care |
| 8 | c1728 | Critical care |
| 9 | c1229 | Pharmacoepidemiology (general) |
| 10 | c1640 | Critical care; infection (HIV) |
| 11 | c1122 | Perinatal registry |
| 12 | M04 | Cross-domain |
| 13 | c0342 | Cardiovascular (heart failure) |
| 14 | c0515 | Cardiovascular |
| 15 | c0838 | Oncology |
| 16 | c1084 | Respiratory (illustration) |
| 17 | c1676 | Pharmacoepidemiology (drug repurposing) |
| 18 | c0044 | Cardiovascular (heart failure); high-dimensional claims codes |
| 19 | c1530 | Oncology |
| 20 | c0489 | Unverified (cardiovascular per table of contents) |
| 21 | c1776 | Cardiovascular |
| 22 | c0381 | Cardiovascular |
| 23 | c1475 | Infection (sepsis) |
| 24 | c0457 | Neurology (MS) |
| 25 | c0416 | Orthopaedics |
| 26 | S06 | Infection (HIV trial) |
| 27 | c0279 | Respiratory (asthma) |
| 28 | c0488 | Cardiovascular (AF) |
| 29 | c0452 | Oncology |
| 30 | c0397 | Oncology |
| 31 | c0022 | Musculoskeletal / pharmacoepidemiology |
| 32 | c0848 | Oncology |
| 33 | c0049 | Infection (MRSA) |
| 34 | c1053 | Mental health (depression) |
| 35 | S03 | General |
| 36 | c0030 | General (critical-care journal) |
| 37 | c0382 | General |
| 38 | S04 | Infection/stroke examples (trials) |
| 39 | S05 | Mental health (depression trial) |
| 40 | c1075 | Older adults / pharmacotherapy (trial) |
| 41 | c0023 | Renal (sepsis-associated AKI) |

Renal coverage from full text rests on Row 41 (c0023), which was added for domain coverage. The other renal papers are one-line entries: c0927, c0936, c1814, c0091, c1832, c1833, c0135, c0083, c0377.

## 3. Synthesis (established, contested, missing)

Row numbers refer to the evidence cards in section 2. The label My judgement marks claims that are my reading rather than the authors' statements.

### What is established

**1. Known-truth evidence on routine-data covariates is scarce, and the methods differ less than their reputations.**
- Only one study evaluates HTE estimators against a known truth on real routine-data covariates (Row 1). It used four US claims or hospital-database studies with simulated outcomes.
  - BART and causal boosting gave the lowest error in conditional risk differences, and causal forest did worse.
  - Where true heterogeneity was tiny, a null estimator beat every method.
  - With strong heterogeneity, coverage of the average effect fell to 30–60%.
- In the ACIC 2022 competition (synthetic data calibrated to Medicare; Rows 2–3):
  - BART-based estimators found subgroup signal best without overfitting.
  - No estimator achieved acceptable error with nominal coverage for practice-level effects.
  - Bootstrap intervals did not reach nominal coverage.
  - The authors themselves found that a derived covariate acted as an accidental proxy for confounding (Row 2).
- In semi-synthetic survival data built on MIMIC-IV covariates, all estimator families had almost the same CATE error. No single method dominated, and almost all failed under very heavy censoring (Row 10).

**2. Plasmode design changes the verdict.**
- Resampling each patient's observed treatment together with their covariates induces a positivity violation. This penalises propensity-score estimators (Row 6) and flexible, machine-learning-based doubly robust estimators (Row 7).
- A buggy plasmode implementation made misspecified estimators look unbiased (Row 8).
- A plasmode can refute an estimator but cannot certify one (Row 7).
- Two of the classic routine-data plasmodes keep the observed treatment: Wendling (Row 1) and Wyss (Row 5).
- All of Rows 4–8 estimate average effects only. Their lessons transfer to HTE by argument, not by evidence.

**3. Unmeasured confounding produces false heterogeneity.**
- In simulation, causal forest and X-learner missed true heterogeneity and produced spurious heterogeneity when confounding was unmeasured. Negative control outcomes flagged the affected strata (Row 9).
- Empirical calibration with negative controls in OHDSI claims detected residual confounding in one of three databases (Row 22).

**4. Measures of how well HTE models rank patients are often near the null when applied to real data.**
- C-for-benefit was 0.53–0.55 in the OPERAM trial (Row 40). In the depression trial (Row 39), confidence intervals for competing models overlapped heavily.
- AUTOC confidence intervals included zero in two applied causal-survival-forest analyses of routine data (Rows 31, 33). Both papers nonetheless described subgroup heterogeneity; in Row 31 this rested on graphical stratification.
- In the renal example, AUTOC fell from 0.73 in development to 0.15 on external validation (Row 41).

**5. The tools are known; their validity in observational data is less settled.**
- Identification of discrimination and calibration for benefit in observational data has been worked out (Row 16). However, bias under incomplete confounding control is unpredictable.

### What is contested

**1. Which selection metric to use.**
- The R-risk was best for model selection with registry-derived semi-synthetic covariates (Row 11).
- The R-score did poorly in a larger benchmark, where doubly robust, TMLE and T-learner plug-in scores dominated (Row 12).
- The candidate families and nuisance tuning differed between the two studies.

**2. Which survival learner to use.**
- AFT-BART led in one simulation (Row 29).
- DEA- and R-learners were recommended in another (Row 27).
- Survival S-learners and matching learners ranked highest in SurvHTE-Bench (Row 10).
- Mixture models had the most power when latent subgroups were present (Row 15).

**3. Whether label-free model choice can be trusted.**
- On claims data without a truth, stability-based scores (ERMSE) and influence-function PEHE chose an S-learner (Row 17). My judgement: an S-learner tends to shrink effects towards zero, which such scores reward.
- Cross-validated transformed-outcome selection (Rows 13, 18) has no truth check on claims. In simulation, a simple interaction tree beat iCF at identifying interactions (Row 13).

**4. Whether agreement with trials supports subgroup claims.**
- Trial benchmarks validate the *average* effect, not the heterogeneity: Row 19 (registry vs the published QUASAR trial), Row 21 (CPRD vs ONTARGET), Row 23 (MIMIC vs RCT meta-analyses).
- The PCORI report reports good agreement in its conclusions (Row 20, abstract only). Its heterogeneity analysis covers only baseline risk scores.

### What is missing

- No known-truth evaluation of HTE estimators on UK primary-care (CPRD) covariates. CPRD appears only as an application (Rows 21, 28).
- No HTE plasmode on routine data that uses the generate-treatment design recommended in Rows 6–7.
- No systematic evaluation of causal survival forest tuning. Applied papers use defaults or data-driven horizons (Rows 26, 31–33).
- No validation of subgroup or individual effects against trials in routine data.
- Little evaluation of learned representations of coded records for HTE. Rows 18 and 5 use hdPS-type codes; the neural papers appear only as one-line entries.
- No consensus reporting guideline for HTE analyses of observational data. There is a commentary checklist (Row 36), narrative guidance (Row 37), PATH for trials (Row 35) and the protocol for the PRECOG guideline (one-line c1375).

## 4. Answers to the four explicit questions

**Q1. Which validation approaches have been tested against a known truth?**

| Approach | Rows |
|---|---|
| Plasmode with real routine-data covariates and simulated outcomes | 1 (HTE); 4, 5, 6 (average effects) |
| Plasmode design itself, with theory and simulation | 6, 7, 8 |
| Synthetic competition calibrated to Medicare | 2, 3 |
| Semi-synthetic benchmarks: registry covariates | 11 |
| Semi-synthetic benchmarks: MIMIC covariates | 10 |
| Semi-synthetic benchmarks: perinatal, Twins and labour-economics data | 12 |
| Negative control outcomes as an HTE diagnostic (synthetic simulation) | 9 |
| Best-linear-projection inference (synthetic simulation) | 26 |
| Benefit discrimination and calibration metrics (simulation with known truth) | 39, 40 |
| Benefit discrimination and calibration metrics (analytic synthetic populations) | 16 |
| Interval coverage for survival CATE (synthetic simulation) | 26, 29 |

Not tested against a truth:
- Benchmarking against trials (Rows 19–23).
- RATE/AUTOC and Qini as used in applications (Rows 31, 33, 41).
- Empirical negative-control calibration (Row 22).

**Q2. Which selection criteria have been evaluated on covariates from routinely collected data?**

| Evaluation | Rows | Known truth? |
|---|---|---|
| R-risk and other selection risks on Linked Births and Infant Deaths Database covariates | 11 | Yes |
| Selecting the best variant per family on validation data, MIMIC-IV covariates | 10 | Yes |
| ERMSE and influence-function PEHE on Optum claims | 17 | No |
| Cross-validated transformed-outcome error on Medicare claims | 13 (its simulation is synthetic), 18 | No |

The main metric study (Row 12) does not use routine-data covariates.

**Q3. Which time-to-event methods for HTE have been used in such data?**

| Method | Rows and data |
|---|---|
| Causal survival forests | 31 (Korean claims), 32 (VA EHR), 33 (Florida EHR); one-line list: c0788, c0790, c0039, c0820, c0851 |
| Pseudo-outcome survival meta-learners | 27 (paediatric EHR) |
| TMLE-based survival HTE | 28 (CPRD) |
| AFT-BART / riAFT-BART | 29, 30 (NCDB) |
| Mixture, AFT and Cox models | 15 (GENIE BPC) |
| IPW Cox by subgroup | 21 (CPRD) |
| Risk-stratified Cox and Kaplan–Meier | 22 (US claims) |
| GRF with censoring weights for competing risks | 34 (Danish registries; average-effect ranking) |
| Deep survival learners | one-line list: M07, c0962, c1640 benchmark (Row 10) |

**Q4. Which reporting standards exist?**
- PATH statement for RCTs (Row 35) and its explanation and elaboration document (one-line c0769).
- Guidance on HTE in real-world data (Row 37).
- Checklist for causal machine-learning HTE with target trial emulation (Row 36). It is a commentary, not a consensus product.
- Methods guidance on ITE prediction (Row 38) and on benefit-performance metrics (Rows 39, 40).
- Protocol for the PRECOG reporting guideline (one-line c1375).
- Scoping reviews that call for better reporting (one-line c0172, c0063, c0312).

## 5. Corrections, downgrades and version comparisons (Phases 2 and 3a)

### Corrections and downgrades
- **c1676 = c0396.** The arXiv v5 of c1676 carries the title of c0396 (J Biomed Inform). They are merged into Row 17, and c0396 is not counted separately.
- **c1053 (Row 34) is reclassified.** It is an average-treatment-effect ranking method with competing risks, not HTE evidence. It is moved to the end of section C.
- **Average-effect flags.** Rows 4–8 (c0203, S02, c0664, c1716, c1728) estimate average effects only.
- **c0044 hdiCF (Row 18) is downgraded.** The version of record contains no simulation. It moves from the known-truth tier to selection on claims without a truth.
- **c1530 Shen (Row 19)** benchmarks only the average effect against *published* QUASAR estimates; the authors had no patient-level trial data. Subgroups were not validated.
- **c0030 (Row 36)** is a four-page CHEST Commentary, not a consensus guideline.
- **c0489 PCORI (Row 20)** is abstract only.
- **c0488 (Row 28)** has an internal count inconsistency: 28,972 estimations versus age subgroups that sum to 28,921.
- **Wendling (Row 1) and Wyss (Row 5)** keep the observed treatment in their plasmodes. They are therefore open to the critique in Rows 6–7.
- **c1640 (Row 10):** on the MIMIC semi-synthetic data, CATE error was tightly clustered across all families, so these data separate the methods weakly.
- **Seeds without routine data.** S03, S04, S05 (Rows 35, 38, 39) and S06 (Row 26) use trials or no data.

### Versions of record versus preprints
- **Shaw (Row 6):** version of record versus arXiv v1. The scope wording is narrowed to point-treatment estimands, the plasmode description is reworded, and a GitHub code link is added. Results and conclusions are unchanged.
- **Rytgaard (Row 34):** version of record versus arXiv v1. The simulation was redesigned: ten treatments, n from 500 to 5,000, 2,000 repetitions, random-survival-forest censoring weights, and Fine–Gray and cause-specific Cox comparators. The v1 result of 59.6% coverage with unadjusted weights is not reported in the same form. The repository was renamed.
- **Cui (Row 26):** version of record versus arXiv v5. No substantive differences were found.
- **Read as preprints only, no version of record compared:**
  - c1229 (Row 9), c1716 (Row 7) and c1728 (Row 8): arXiv.
  - c1640 (Row 10): ICLR camera-ready on arXiv.
  - c1676 (Row 17): arXiv v5.
  - c0488 (Row 28): arXiv v2.
  - c1530 (Row 19): Research Square.

## 6. Excluded near-misses

Each near-miss below has a specific reason for exclusion. All other abstract-stage exclusions, with coded reasons, are in `brief5/screening.md` section C, and title-stage exclusions are in `brief5/screening_titles.tsv`.


| id | Citation | Link | Reason for exclusion |
|---|---|---|---|
| c0001 | Tong et al. (2026). FLAT-WHITE: from target trial emulation to federated high-throughput causal machine learning using decentralized real-world data. Npj Health Syst | https://doi.org/10.1038/s44401-026-00160-6 | Federated target trial emulation; average-effect focus per abstract. |
| c0008 | Zhao et al. (2026). Disparities in severe infection risk associated with SLE: evidence from a causal forest analysis. Rheumatology (Oxford) | https://doi.org/10.1093/rheumatology/keag362 | Exposure (SLE), not a treatment. |
| c0019 | Lai et al. (2026). The heterogeneous treatment effects of statins on dementia: a target trial emulation with causal machine learning using integrated genetic and real-world data. Alzheimers Dement | https://doi.org/10.1002/alz.71178 | UK Biobank research cohort, not routinely collected data as primary source (statins/dementia, causal forest). |
| c0035 | Weberpals et al. (2025). Opportunities for Causal Machine Learning in Precision Oncology. NEJM AI | https://doi.org/10.1056/AIp2500277 | Perspective on causal ML in oncology; no new evidence. |
| c0103 | Krzykalla et al. (2026). Tree-based exploratory identification of predictive biomarkers in non-randomized data. BMC Med Res Methodol | https://doi.org/10.1186/s12874-026-02928-8 | Predictive biomarker trees for non-randomised data, illustrated on trial/study data, not routine data. |
| c0116 | Wang et al. (2026). Federated target trial emulation for time-to-event outcomes via POLARIS: Pooled-equivalent One-shot Likelihood Aggregation for Real-world Inference in Survival. Res Sq | https://doi.org/10.21203/rs.3.rs-9613167/v1 | Federated target trial emulation for time-to-event outcomes; pooled average effects, not HTE. |
| c0118 | Chen et al. (2026). Heterogeneity of Treatment Effects Across Nine Glucose-Lowering Drug Classes in Type 2 Diabetes: Extension of the LEGEND-T2DM Network Study. Diabetes Obes Metab | https://doi.org/10.1111/dom.70918 | LEGEND-T2DM HTE extension, covered in Brief 3. |
| c0166 | Knowlton & Parast (2026). Assessing surrogate heterogeneity in real world data using meta-learners. J Causal Inference | https://doi.org/10.1515/jci-2025-0033 | Heterogeneity of surrogacy, not of a treatment effect. |
| c0208 | Yang et al. (2025). Doubly Robust Estimators for Heterogeneous Treatment Effects in Heteroskedastic Survival Data. Stat Med | https://doi.org/10.1002/sim.70301 | Survival HTE estimators applied to NHANES (survey), not routine data. |
| c0216 | Li et al. (2026). Inotrope selection in mixed cardiogenic shock with sepsis: a comparative analysis between milrinone and dobutamine. Ann Am Thorac Soc | https://doi.org/10.1513/AnnalsATS.202503-339OC | Comparative effectiveness (claims); no HTE aim stated in abstract. |
| c0221 | Mori et al. (2026). Heterogeneous cardiovascular effects of sodium-glucose cotransporter 2 inhibitors in type 2 diabetes: a causal forest and target trial emulation study. Eur J Prev Cardiol | https://doi.org/10.1093/eurjpc/zwaf539 | T2D drug comparison (SGLT2i, causal forest), covered in Brief 3. |
| c0224 | Toya et al. (2025). Machine Learning Algorithm to Explore Patients With Heterogeneous Treatment Effects of Clinically Significant CMV Infection and Non-Relapse Mortality After HSCT. EJHaem | https://doi.org/10.1002/jha2.70117 | Heterogeneity of an exposure (CMV infection) rather than a treatment; registry. |
| c0234 | Deng et al. (2025). Heterogeneity of Cardiovascular Effects of Second-Line Glucose-Lowering Therapies in Adults With Type 2 Diabetes Across the Range of Moderate Baseline Cardiovascular Risk. J Am Heart Assoc | https://doi.org/10.1161/JAHA.124.040217 | T2D second-line drug HTE across CV risk, applied. |
| c0241 | Dávila-García et al. (2025). Heterogeneity of treatment effects of glucose-lowering drug classes for type 2 diabetes: LEGEND-T2DM network real-world evidence. J Diabetes Complications | https://doi.org/10.1016/j.jdiacomp.2025.109114 | LEGEND-T2DM HTE, T2D drug comparison. |
| c0249 | Tang et al. (2025). Heterogeneous treatment effects of GLP-1RAs and SGLT2is on risk of Alzheimer's disease and related dementia in patients with type 2 diabetes: Insights from a real-world target trial emulation. Alzheimers Dement | https://doi.org/10.1002/alz.70313 | T2D drug comparison (GLP-1 RA vs SGLT2i, dementia), applied. |
| c0266 | Liu et al. (2025). Heterogeneous effects of obesity on all-cause mortality: A causal forest analysis of hospitalized patients in China. Diabetes Obes Metab | https://doi.org/10.1111/dom.16391 | Exposure (obesity), not a treatment. |
| c0299 | Barbati et al. (2024). Effectiveness of PCSK9 inhibitors: A Target Trial Emulation framework based on Real-World Electronic Health Records. PLoS One | https://doi.org/10.1371/journal.pone.0309470 | Target trial emulation of PCSK9 inhibitors in EHR; average effects. |
| c0303 | Zhang et al. (2024). Machine Learning Methods to Estimate Individualized Treatment Effects for Use in Health Technology Assessment. Med Decis Making | https://doi.org/10.1177/0272989X241263356 | Overview of ML ITE methods for HTA; no routine-data evaluation stated in abstract. |
| c0305 | Siriyotha et al. (2024). Individual treatment effects of sodium-glucose co-transporter-2 inhibitors on the risk of chronic kidney disease in patients with type 2 diabetes: A counterfactual prediction model based on real-world data. Diabetes Obes Metab | https://doi.org/10.1111/dom.15793 | T2D drug comparison (SGLT2i, CKD), applied. |
| c0320 | Brooks et al. (2024). Assessing the properties of patient-specific treatment effect estimates from causal forest algorithms under essential heterogeneity. BMC Med Res Methodol | https://doi.org/10.1186/s12874-024-02187-5 | Causal forest under essential heterogeneity: pure simulation not built on routine data. |
| c0322 | Goto et al. (2024). Machine learning for detection of heterogeneous effects of Medicaid coverage on depression. Am J Epidemiol | https://doi.org/10.1093/aje/kwae008 | Oregon Health Insurance Experiment (randomised). |
| c0328 | Dandl et al. (2024). Heterogeneous treatment effect estimation for observational data using model-based forests. Stat Methods Med Res | https://doi.org/10.1177/09622802231224628 | Model-based forests for observational data: simulation + ALS trial database (not routine data). |
| c0338 | Curth et al. (2024). Using Machine Learning to Individualize Treatment Effect Estimation: Challenges and Opportunities. Clin Pharmacol Ther | https://doi.org/10.1002/cpt.3159 | Review of ML for ITE; no new evidence. |
| c0343 | Post et al. (2024). Flexible Machine Learning Estimation of Conditional Average Treatment Effects: A Blessing and a Curse. Epidemiology | https://doi.org/10.1097/EDE.0000000000001684 | Flexible CATE estimation commentary/simulation; no routine-data component in abstract. |
| c0347 | Kaas-Hansen et al. (2024). Real-world causal evidence for planned predictive enrichment in critical care trials: A scoping review. Acta Anaesthesiol Scand | https://doi.org/10.1111/aas.14321 | Scoping review of predictive enrichment in critical care trials. |
| c0374 | Anon (2023). Correction: Assessing Heterogeneity of Treatment Effect in Real-World Data. Ann Intern Med | https://doi.org/10.7326/L23-0162 | Correction notice for c0382. |
| c0386 | Feng et al. (2023). Variational Temporal Deconfounder for Individualized Treatment Effect Estimation with Longitudinal Observational Data. Res Sq | https://doi.org/10.21203/rs.3.rs-2536079/v1 | Duplicate/preprint of c0231 (VTDNet). |
| c0394 | Peng et al. (2022). Restricted Mean Survival Time Analysis to Estimate SGLT2i-Associated Heterogeneous Treatment Effects on Primary and Secondary Prevention of Cardiorenal Outcomes in Patients With Type 2 Diabetes in Taiwan. JAMA Netw Open | https://doi.org/10.1001/jamanetworkopen.2022.46928 | SGLT2i RMST HTE: applied T2D drug comparison (Brief 3 scope). |
| c0460 | Crown (2021). Decomposition analysis as a framework for understanding heterogeneity of treatment effects in non-randomized health care studies. Pharm Stat | https://doi.org/10.1002/pst.2111 | Conceptual decomposition framework; no routine-data HTE estimation. |
| c0481 | Yang et al. (2021). Heterogeneous Treatment Effects on Cardiovascular Diseases With Dipeptidyl Peptidase-4 Inhibitors Versus Sulfonylureas in Type 2 Diabetes Patients. Clin Pharmacol Ther | https://doi.org/10.1002/cpt.2058 | T2D drug comparison (DPP-4i vs SU), applied. |
| c0506 | McConnell & Lindner (2019). Estimating treatment effects with machine learning. Health Serv Res | https://doi.org/10.1111/1475-6773.13212 | ML estimators for average effects (simulation + hospital data). |
| c0509 | Zhang et al. (2019). MetaPred: Meta-Learning for Clinical Risk Prediction with Limited Patient Electronic Health Records. KDD | https://doi.org/10.1145/3292500.3330779 | Meta-learning for risk prediction, not causal. |
| c0553 | Dai et al. (2025). Heterogeneous Effects of Sodium-Glucose Cotransporter-2 Inhibitors on Acute Kidney Injury: A Causal Learning Approach. medRxiv | https://doi.org/10.1101/2025.11.23.25340831 | SGLT2i and AKI in T2D, applied. |
| c0574 | Sun et al. (2024). Comparing algorithms for characterizing treatment effect heterogeneity in randomized trials. Biom J | https://doi.org/10.1002/bimj.202100337 | HTE algorithms in randomised trials. |
| c0598 | Desai et al. (2024). Individualized Treatment Effect Prediction with Machine Learning - Salient Considerations. NEJM Evid | https://doi.org/10.1056/EVIDoa2300041 | Review (NEJM Evidence) of ITE prediction considerations; no new evidence. |
| c0659 | Ghosh et al. (2021). Deep propensity network using a sparse autoencoder for estimation of treatment effects. J Am Med Inform Assoc | https://doi.org/10.1093/jamia/ocaa346 | Deep propensity network (sparse autoencoder), average effects. |
| c0662 | Künzel et al. (2019). Metalearners for estimating heterogeneous treatment effects using machine learning. Proc Natl Acad Sci U S A | https://doi.org/10.1073/pnas.1804597116 | Meta-learner foundations (PNAS); simulation and non-health applications. |
| c0665 | Desai et al. (2026). A Plasmode Simulation-Based Bias Analysis for Residual Confounding by Unmeasured Variables Leveraging Information-Rich Subsets. Pharmacoepidemiol Drug Saf | https://doi.org/10.1002/pds.70383 | Plasmode bias analysis for residual confounding, average effects only. |
| c0669 | Meng & Huang (2026). REFINE2: a simplified simulation tool to help epidemiologists evaluate the suitability and sensitivity of effect estimation within user-specified data. Am J Epidemiol | https://doi.org/10.1093/aje/kwaf195 | REFINE2 simulation tool for average effect estimators. |
| c0670 | Hossain et al. (2025). High-Dimensional Disease Risk Score for Dealing With Residual Confounding Bias in Estimating Treatment Effects With a Survival Outcome. Pharmacoepidemiol Drug Saf | https://doi.org/10.1002/pds.70172 | High-dimensional disease risk score plasmode, average effects only. |
| c0671 | Stolte et al. (2025). Simulation study to evaluate when Plasmode simulation is superior to parametric simulation in comparing classification methods on high-dimensional data. PLoS One | https://doi.org/10.1371/journal.pone.0322887 | Plasmode vs parametric simulation for classification methods, not treatment effects. |
| c0674 | Karim & Lei (2025). How Effective Are Machine Learning and Doubly Robust Estimators in Incorporating High-Dimensional Proxies to Reduce Residual Confounding?. Pharmacoepidemiol Drug Saf | https://doi.org/10.1002/pds.70155 | Plasmode with high-dimensional proxies, but average effects only. |
| c0678 | Guo et al. (2024). Machine learning methods for propensity and disease risk score estimation in high-dimensional data: a plasmode simulation and real-world data cohort analysis. Front Pharmacol | https://doi.org/10.3389/fphar.2024.1395707 | Plasmode, ML propensity/disease risk scores, average effects only. |
| c0679 | Ress & Wild (2024). Comparing methods for estimating causal treatment effects of administrative health data: A plasmode simulation study. Health Econ | https://doi.org/10.1002/hec.4891 | Plasmode on administrative data, average effects only. |
| c0686 | Souli et al. (2023). Longitudinal plasmode algorithms to evaluate statistical methods in realistic scenarios: an illustration applied to occupational epidemiology. BMC Med Res Methodol | https://doi.org/10.1186/s12874-023-02062-9 | Longitudinal plasmode for marginal structural models (occupational), average effects. |
| c0720 | Rekkas et al. (2023). Estimating individualized treatment effects from randomized controlled trials: a simulation study to compare risk-based approaches. BMC Med Res Methodol | https://doi.org/10.1186/s12874-023-01889-6 | ITE methods simulation for RCTs. |
| c0846 | Maas et al. (2024). Quantifying absolute treatment effect heterogeneity for time-to-event outcomes across different risk strata: divergence of conclusions with risk difference and restricted mean survival difference. medRxiv | https://doi.org/10.1101/2024.12.19.24319347 | Risk-based absolute HTE for time-to-event in clinical trials. |
| c0867 | Xu et al. (2023). Principled estimation and evaluation of treatment effect heterogeneity: A case study application to dabigatran for patients with atrial fibrillation. J Biomed Inform | https://doi.org/10.1016/j.jbi.2023.104420 | RCT data only (RE-LY); survival meta-learners and evaluation metrics, but not routinely collected data. |
| c0898 | Kundu et al. (2026). Privacy-enhancing sequential learning under heterogeneous selection bias in multi-site electronic health records data. J Am Med Inform Assoc | https://doi.org/10.1093/jamia/ocag083 | Disease-risk parameters across EHR sites, not HTE. |
| c0948 | Zhu et al. (2019). Feature Exploration and Causal Inference on Mortality of Epilepsy Patients Using Insurance Claims Data. IEEE EMBS Int Conf Biomed Health Inform | https://doi.org/10.1109/bhi.2019.8834638 | Mortality prediction/causal feature exploration in claims; not treatment HTE. |
| c0955 | Anon (2026). Evaluation of Machine-Learning Methods to Estimate Conditional Average Treatment Effects From Randomized Clinical Trial Data With Time-To-Event Outcomes. Cancer Informatics | https://doi.org/10.1177/11769351261491717 | CATE ML methods on RCT time-to-event data. |
| c0960 | Zijun Gao et al. (2026). Causal Survival Forests with Negative Controls. | https://arxiv.org/abs/2608.19749 | Negative-control causal survival forest; simulations only in abstract. |
| c1000 | Dennis Frauen et al. (2025). Orthogonal Survival Learners for Estimating Heterogeneous Treatment Effects from Time-to-Event Data. Neural Information Processing Systems | https://arxiv.org/abs/2505.13072 | Survival HTE learners evaluated on simulations only (no routine data in abstract). |
| c1002 | Daijiro Kabata et al. (2025). Quantifying uncertainty of individualized treatment effects in right-censored survival data: a comparison of Bayesian additive regression trees and causal survival forest. Health Services & Outcomes Research Methodology | https://doi.org/10.1007/s10742-025-00362-9 | BART vs CSF interval coverage; simulation only in abstract. |
| c1040 | Anon (2023). Machine-learning-based high-benefit approach versus conventional high-risk approach in blood pressure management. International Journal of Epidemiology | https://doi.org/10.1093/ije/dyad037 | High-benefit approach in RCT data (SPRINT-type). |
| c1051 | Alicia Curth et al. (2021). SurvITE: Learning Heterogeneous Treatment Effects from Time-to-Event Data. Neural Information Processing Systems | https://arxiv.org/abs/2110.14001 | SurvITE: survival HTE neural method; no routinely collected data stated in abstract. |
| c1100 | Anon (2026). Heterogeneity in the treatment effect of sodium-glucose cotransporter-2 inhibitor on chronic kidney disease risk reduction: a prevalent new user cohort study applying double/debiased machine learning. Diabetology & Metabolic Syndrome | https://doi.org/10.1186/s13098-026-02249-2 | T2D drug comparison (SGLT2i, CKD), applied. |
| c1127 | Anon (2024). A Two‐Step Framework for Validating Causal Effect Estimates. Pharmacoepidemiology and Drug Safety | https://doi.org/10.1002/pds.5873 | Two-step validation of causal estimates vs RCT, average effects (abstract only). |
| c1206 | Anon (2026). Comparison of disease risk score methods to study treatment effect heterogeneity: a simulation study. American Journal of Epidemiology | https://doi.org/10.1093/aje/kwag050 | Disease risk score HTE simulation for randomised trials. |
| c1490 | Reagan Mozer et al. (2023). Leveraging text data for causal inference using electronic health records. arXiv.org | https://arxiv.org/abs/2307.03687 | Text-derived covariates in EHR for causal inference; HTE not stated in abstract. |
| c1510 | Anon (2021). ADCB: An Alzheimer's disease benchmark for evaluating observational estimators of causal effects. arXiv.org | https://arxiv.org/abs/2111.06811 | Alzheimer benchmark built on ADNI (research cohort), not routine data. |
| c1522 | Anon (2020). RealCause: Realistic Causal Inference Benchmarking. arXiv.org | https://arxiv.org/abs/2011.15007 | RealCause benchmark generator; not health routine data in abstract. |
| c1547 | Anon (2021). Really Doing Great at Estimating CATE? A Critical Look at ML Benchmarking Practices in Treatment Effect Estimation. NeurIPS Datasets and Benchmarks | n/a | Critique of CATE benchmarking practice on IHDP/ACIC; not routinely collected data (useful background). |
| c1566 | Anon (2022). Machine learning for improving high‐dimensional proxy confounder adjustment in healthcare database studies: An overview of the current literature. Pharmacoepidemiology and Drug Safety | https://doi.org/10.1002/pds.5500 | hdPS + ML overview, average effects (covered in Brief 3). |
| c1568 | Anon (2022). Synthetic Negative Controls: Using Simulation to Screen Large-Scale Propensity Score Analyses. Epidemiology | https://doi.org/10.1097/EDE.0000000000001482 | Synthetic negative controls for large-scale PS analyses; average effects. |
| c1574 | Xiang Meng & Jonathan Huang (2021). REFINE2: A tool to evaluate real-world performance of machine-learning based effect estimators for molecular and clinical studies. | https://arxiv.org/abs/2105.13148 | REFINE2 preprint (average effects). |
| c1583 | Anon (2020). Implementing high‐dimensional propensity score principles to improve confounder adjustment in UK electronic health records. Pharmacoepidemiology and Drug Safety | https://doi.org/10.1002/pds.5121 | hdPS in UK EHR, average effects. |
| c1624 | Anon (2019). Models with interactions overestimated heterogeneity of treatment effects and were prone to treatment mistargeting. Journal of Clinical Epidemiology | https://doi.org/10.1016/j.jclinepi.2019.05.029 | Interaction models overestimate HTE: simulation based on trial data. |
| c1649 | Alicia Curth & Mihaela van der Schaar (2023). Understanding the Impact of Competing Events on Heterogeneous Treatment Effect Estimation from Time-to-Event Data. arXiv | https://arxiv.org/abs/2302.12718v1 | Competing events and HTE: theory and simulation only. |
| c1688 | Haining Yu & Yizhou Sun (2024). Do Contemporary Causal Inference Models Capture Real-World Heterogeneity? Findings from a Large-Scale Benchmark. arXiv | https://arxiv.org/abs/2410.07021v2 | Large CATE benchmark on field datasets, not routinely collected health data. |
| c1712 | Ilker Demirel et al. (2024). Benchmarking Observational Studies with Experimental Data under Right-Censoring. arXiv | https://arxiv.org/abs/2402.15137v1 | Censoring-aware benchmarking of observational vs RCT data, but uses Women's Health Initiative (research cohort/trial), not routine data. |
| c1714 | Hugo Gobato Souto & Francisco Louzada Neto (2024). K-Fold Causal BART for CATE Estimation. arXiv | https://arxiv.org/abs/2409.05665v1 | Semi-synthetic IHDP benchmark, not routinely collected data. |
| c1730 | M. Ehsan Karim & Wanqing Hu (2026). Which Regularized Propensity-Score and Doubly Robust Methods Are Best Calibrated When Exposures or Outcomes Are Rare? A Plasmode Study of Proxy-Based Confounding Adjustment. arXiv | https://arxiv.org/abs/2607.07065v1 | Plasmode calibration of PS/DR methods, average effects only. |
| c1732 | Aman Singh (2026). A Large-Scale Empirical Comparison of Meta-Learners and Causal Forests for Heterogeneous Treatment Effect Estimation in Marketing Uplift Modeling. arXiv | https://arxiv.org/abs/2604.06123v1 | Marketing uplift data (Criteo), not health data. |
| c1758 | Bornkamp et al. (2024). Predicting subgroup treatment effects for a new study: Motivations, results and learnings from running a data challenge in a pharmaceutical corporation. Pharm Stat | https://doi.org/10.1002/pst.2368 | Subgroup data challenge on pharma RCT data. |
| c1822 | Tang et al. (2024). Heterogeneous treatment effects of metformin on risk of dementia in patients with type 2 diabetes: A longitudinal observational study. Alzheimers Dement | https://doi.org/10.1002/alz.13480 | Metformin and dementia in T2D, applied. |
| c1973 | Htoo et al. (2026). Post hoc Population Standardization of Trial Emulation Studies in Claims Data: An RCT-DUPLICATE Analysis. Clin Pharmacol Ther | https://doi.org/10.1002/cpt.70241 | RCT-DUPLICATE population standardisation: average effects, not HTE. |
| c2101 | Heyard et al. (2024). Design differences and variation in results between randomised trials and non-randomised emulations: meta-analysis of RCT-DUPLICATE data. BMJ Med | https://doi.org/10.1136/bmjmed-2023-000709 | RCT vs emulation design differences, average effects. |