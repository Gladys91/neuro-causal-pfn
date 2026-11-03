# Brief 1: Pre-trained models for treatment-effect estimation

**Date:** 3 November 2026
**Question:** How well do pre-trained, in-context models estimate conditional average treatment effects (CATE) against strong and properly tuned comparators, and under which conditions do they fail?
**Scope:** (i) models that output effects or potential outcomes directly (CausalPFN, Do-PFN, CausalFM and later causal prior-fitted networks, PFNs); (ii) tabular foundation models (TFMs: TabPFN v2 and later, TabICL) used as outcome or propensity models inside meta-learners, double machine learning (DML) or targeted maximum likelihood estimation (TMLE); (iii) benchmarks against Bayesian additive regression trees (BART), Bayesian causal forests (BCF), generalised random forests (GRF) or tuned meta-learners. Window 2019 to 3 November 2026.

**Abbreviations used throughout.** ACIC: Atlantic Causal Inference Conference (data challenge). ATE: average treatment effect. ATT: average treatment effect on the treated. AUC: area under the receiver operating characteristic curve. A-IPTW: augmented inverse probability of treatment weighting. BART, BCF, GRF: see above. CATE: conditional average treatment effect. CEPO: conditional expected potential outcome. CFM: causal foundation model. CI: confidence (or credible) interval. CID: conditional interventional distribution. DGP: data-generating process. DML: double/debiased machine learning. DR-learner: doubly robust learner. EHR: electronic health records. FLAML: Fast and Lightweight AutoML library. HPO: hyperparameter optimisation. ICI: integrated calibration index (medical statistics) or integrated coverage error (CausalPFN paper; defined where used). IHDP: Infant Health and Development Program. IPTW: inverse probability of treatment weighting. IV: instrumental variable. MSE: mean squared error. OOD: out of distribution. PEHE: precision in estimation of heterogeneous effects (root mean squared CATE error). PFN: prior-data fitted network. RCT: randomised controlled trial. RMSE: root mean squared error. S-, T-, X-, DR-, R-, RA-, DA-learner: single-model, two-model, cross, doubly robust, residual (Robinson/Nie–Wager), regression-adjusted and domain-adaptation meta-learners. SCM: structural causal model. TFM: tabular foundation model. TMLE: targeted maximum likelihood estimation.

### Assumptions (how ambiguities in the brief were resolved)
1. **Inclusion rule.** A paper is in the evidence table if it reports an empirical evaluation of (a) a pre-trained in-context model that outputs treatment effects or potential outcomes, or (b) a TFM used as a nuisance model for a treatment-effect estimand, against at least one non-foundation-model comparator or against a known truth. ATE-only papers were included when they test failure modes the brief names (binary outcomes, calibration, coverage, clinical data); this is stated in each row. The seed TabPFN Nature paper is included as a model-description row because the brief names it as a seed, although it contains no causal evaluation.
2. **"Pre-trained model" excluded** models meta-trained inside a single database to predict effects of new interventions (CaML), since they are not applied in context to a new dataset; they appear under near-misses.
3. **Model-capability facts** (context length, feature limits) for TFMs with no causal evaluation (TabICL, TabICLv2, TabPFN-3.5) are given in a separate capability table (§2b) rather than as evidence rows.
4. **Tuning terminology.** "Feasible" selection = criterion computable from observed data (for example cross-validated nuisance loss); "oracle" = uses true effects. Where a paper does not state the selection criterion, the cell says so.
5. **Version read.** For arXiv papers later accepted at a venue, the arXiv version stated was read; the venue was confirmed from the proceedings page where reachable (noted per row).
6. Results reported only in figures are not transcribed as numbers; the cell says "figure only".

### Access limitations
- **Semantic Scholar API** returned HTTP 429 repeatedly; forward citations were obtained for CausalPFN (64), CausalFM (47) and TabPFN (1,769 records returned; the API stopped returning records at offset 2,000, so TabPFN forward chasing is incomplete). Do-PFN forward citations: see search log row S2-5. Backward references of CausalPFN: 123 records.
- **Google Scholar** cannot be queried automatically; substituted by Semantic Scholar, arXiv API, PubMed E-utilities and web search.
- **OpenReview API** (api2.openreview.net) blocked; **iclr.cc**, **link.springer.com**, **www.medrxiv.org**, **ahajournals.org**, **docs.doubleml.org** and **github.com** not reachable. www.nature.com returned HTTP 429; the TabPFN Nature paper was read from PubMed Central (PMC11711098).
- Consequences: FoCAT (Doklady Mathematics 2025) read from Crossref abstract only; Kurmann et al. 2026 (Stroke) read from PubMed abstract only; the DoubleML TabPFN tutorial page could not be opened; CausalFM's ICLR 2026 acceptance could not be confirmed on iclr.cc (the arXiv v3 header states it).

---

## 1. Search log

All searches run 3 November 2026. "Screened" = titles/abstracts read; "Included" = rows in §2 (a paper found by several routes is counted at its first route).

| # | Source | Query / step | Hits | Screened | Included |
|---|---|---|---|---|---|
| S0 | Seeds named in the brief | Balazadeh et al. 2025 (CausalPFN); Hollmann et al. 2025 (TabPFN, Nature) | 2 | 2 | 2 (Rows 1, 2) |
| A1 | arXiv API | `all:"prior-fitted" AND all:causal` | 11 | 11 | 0 new |
| A2 | arXiv API | `all:"foundation model" AND all:"treatment effect"` | 18 | 18 | 3 (Melnychuk; Schulman; Stith) |
| A3 | arXiv API | `all:TabPFN AND all:causal` | 19 | 19 | 1 (Mourão et al.) |
| A4 | arXiv API | `all:TabPFN AND (all:"treatment effect" OR all:"meta-learner" OR all:"double machine learning")` | 4 | 4 | 1 (Zhang et al.) |
| A5 | arXiv API | `all:"in-context" AND all:"treatment effect" AND all:transformer` | 16 | 16 | 0 new |
| A6 | arXiv API | `all:"Do-PFN"` | 3 | 3 | 1 (Do-PFN) |
| A7 | arXiv API | `all:CausalFM OR all:"causal foundation model"` | 20 | 20 | 3 (CausalFM; Reuter et al.; Jung et al.) |
| A8 | arXiv API | `all:TabICL` | 43 | 43 | 0 (capability table only) |
| A9 | arXiv API | `all:"tabular foundation model" AND (all:causal OR all:propensity OR all:CATE)` | 33 | 33 | 0 new |
| A10 | arXiv API | `all:PFN AND (all:survival OR all:"time-to-event")` | 3 | 3 | 0 |
| A11 | arXiv API | `ti:FoCAT OR (au:Utkin AND all:"treatment effect" AND all:foundation)` | 1 | 1 | 0 |
| A12 | arXiv API | `au:Utkin AND au:Konstantinov AND (all:CATE OR all:"treatment effect")` | 5 | 5 | 0 |
| A13 | arXiv API | `ti:"Tabular foundation models can do survival analysis"` | 1 | 1 | 0 |
| A14 | arXiv API | `all:"survival" AND (all:"causal foundation model" OR all:"prior-data fitted" OR all:"prior-fitted") AND all:treatment` | 0 | 0 | 0 |
| A15 | arXiv API | `all:"treatment effect" AND (all:TabPFN OR all:"tabular foundation model") AND (all:"electronic health" OR all:clinical OR all:patients)` | 3 | 3 | 0 new |
| P1 | PubMed (2019–2026) | `TabPFN AND (causal OR "treatment effect" OR propensity OR counterfactual)` | 20 | 20 | 1 (Kurmann et al., abstract only) |
| P2 | PubMed | `("prior-data fitted network" OR "prior-fitted network" OR "tabular foundation model") AND ("treatment effect" OR causal OR propensity)` | 3 | 3 | 0 |
| P3 | PubMed | `CausalPFN OR "Do-PFN" OR CausalFM` | 0 | 0 | 0 |
| P4 | PubMed | `"foundation model" AND "conditional average treatment effect"` | 0 | 0 | 0 |
| S2-1 | Semantic Scholar | Forward citations of CausalPFN (arXiv:2506.07918) | 64 | 64 | 0 new |
| S2-2 | Semantic Scholar | Backward references of CausalPFN | 123 | 123 | 0 new (Do-PFN, TabPFN already in; BBCI, CInA, CaML → near-misses) |
| S2-3 | Semantic Scholar | Forward citations of TabPFN (DOI 10.1038/s41586-024-08328-6), offsets 0–1,999; keyword-filtered titles | 1,769 returned | ≈130 (keyword-filtered titles) | 2 new (Liu et al. IBD; Ebrahim) |
| S2-4 | Semantic Scholar | Forward citations of CausalFM (arXiv:2506.10914) | 47 | 47 | 0 new |
| S2-5 | Semantic Scholar | Forward citations of Do-PFN (arXiv:2506.06039) | blocked (HTTP 429 on all 21 attempts in three rounds over ~20 min) | – | – (substituted by A6, A7, W3) |
| W1 | Web search | `TabPFN double machine learning nuisance estimator treatment effect` | 10 | 10 | 1 (TabPFN-2.5 report) |
| W2 | Web search | `TabPFN propensity score electronic health records treatment effect estimation` | 9 | 9 | 1 (TabPFN-3 report) |
| W3 | Web search | `CausalPFN Do-PFN benchmark comparison BART causal forest CATE evaluation 2026` | 10 | 10 | 0 new |
| W4 | Web search | `tabular foundation model conditional average treatment effect meta-learners TabPFN T-learner X-learner simulation study` | 9 | 9 | 0 new |
| W5 | Web search | `"TabPFN" causal inference "targeted maximum likelihood" OR TMLE OR "doubly robust" 2025 2026` | 9 | 9 | 0 new |
| W6 | Web search | `causal foundation model OR CausalPFN applied electronic health records OR claims data heterogeneous treatment effect` | 9 | 9 | 0 |
| W7 | Web search | `prior-fitted network treatment effect survival time-to-event censored causal in-context learning` | 9 | 9 | 0 |
| W8 | Web search | Venue checks for CausalPFN, Do-PFN (proceedings.neurips.cc), CausalFM (ICLR 2026) | 30 | 3 | 0 |
| V | Proceedings pages | proceedings.neurips.cc (CausalPFN DOI 10.52202/085713-5184; Do-PFN DOI 10.52202/085713-5814); proceedings.mlr.press/v306 (Melnychuk et al.; Reuter et al.) | – | – | – |
| C | Crossref | DOI metadata for FoCAT (10.1134/S1064562425700280) and medRxiv 10.1101/2025.07.21.25331944 | 2 | 2 | 0 |

Totals: 16 included papers (§2a), 3 capability-only sources (§2b), 30 near-misses (§5). Not searched directly: Google Scholar (no automated access), OpenReview (API blocked; covered indirectly by arXiv and venue checks), AISTATS/CLeaR/UAI proceedings (no hits surfaced by arXiv or web search for in-context CATE models in these venues).

---

## 2a. Evidence table

One card per paper. Every extracted claim carries a page (p.) or section (§) and a short verbatim quotation. "UNVERIFIED" marks anything not confirmed in an opened source. Page numbers are PDF pages from `pdftotext` (form-feed count).

### Row 1. Balazadeh et al. 2025, CausalPFN

| Field | Content |
|---|---|
| Paper | Balazadeh V, Kamkari H, Thomas V, Li B, Ma J, Cresswell JC, Krishnan RG. *CausalPFN: Amortized Causal Effect Estimation via In-Context Learning.* https://arxiv.org/abs/2506.07918v2 |
| Venue and version | NeurIPS 2025, peer reviewed (proceedings DOI 10.52202/085713-5184, confirmed on proceedings.neurips.cc). Read: arXiv v2, 27 Oct 2025 (p.1: "39th Conference on Neural Information Processing Systems (NeurIPS 2025)"). |
| Model and version | CausalPFN, ~20M parameters, 20-layer transformer (p.33 §D.2: "The full model has approximately 20M parameters"). Inference context 4,096 by default (p.33: "CausalPFN’s default maximum context length is set to 4,096 at inference"). |
| Direct or nuisance | Direct: outputs a posterior over CEPOs; CATE = difference of CEPO means (p.5: "These CEPO estimates can also form point estimates for CATEs"). |
| Prior (one line) | Real OpenML and TabPFN-v1-style synthetic base tables; two columns relabelled as CEPOs; random propensity (constant, linear or MLP logits) with positivity and heterogeneity knobs (p.6: "pick two other columns, relabel them as µ0 (X), µ1 (X)"; p.32: "we choose f by randomly selecting one of the following mechanisms"). |
| Identifying assumption | Strong ignorability enforced in the prior; binary treatment only (p.5: "we focus on binary treatments T = {0, 1} under strong ignorability"). Consistency theorem requires an identifiable prior (p.4: "if and only if the prior π is CEPO-identifiable"). |
| Datasets | IHDP (100 realisations), ACIC 2016 (10), Lalonde CPS and PSID via RealCause (100 each) (p.7: "100 realizations of IHDP [95, 40], 10 realizations of ACIC 2016 [27], and the Lalonde CPS and Lalonde PSID cohorts"); five marketing RCTs (Hillstrom, Criteo, X5, Lenta, Megafon) for Qini; synthetic polynomial and sinusoidal DGPs for calibration and size ablations. |
| Sample sizes, covariates | Training causal phase: ≤2,048 rows, ≤100 covariates (p.34 §D.3: "we consider sample sizes up to 2,048 and covariates up to 100"). Benchmarks (sizes from TabPFN-2.5 report Table 3, Row 6): IHDP 747/25, ACIC 2016 4,802/58, Lalonde CPS 16,177/8, PSID 2,675/8. Marketing: 50k subsamples and full tables up to 2.5M rows (p.36 Table 7). |
| Comparators and tuning | EconML T-, S-, X-, DA-, Forest DR-, Forest DML learners: **FLAML AutoML on propensity and outcome models, 900 s budget, 3-fold CV** (p.35 §D.5: "Time budget of 900 seconds, (ii) K-fold cross-validation with K = 3"); feasible nuisance-level criterion (FLAML default loss; the CATE stage is not selected on a CATE criterion). CATENets TARNet, DragonNet, RA-Net: **grid of 16 configurations** (p.35: "Number of layers ∈ {2, 3}"); selection criterion not stated (UNVERIFIED). GRF: internal `tune` option (p.35: "The GRF implementation includes an internal tune option"). **BART untuned** (p.35: "BART, on the other hand, offers no comparable hyperparameter-tuning"). IPW. An untuned table (Table 6, EconML notebook defaults) is also given. TabPFN (latest at the time) as a regression proxy, and TabPFN fine-tuned 48 h on the causal prior (p.9). |
| Extra advantages to the foundation model | None at test time on standard benchmarks (no tuning). For tables beyond the context, retrieval using a gradient-boosting "weak CATE" stratifier (p.33: "we fit a lightweight gradient boosting regressor on the context data"); five-fold honest splitting for Hillstrom (p.8). Optional per-dataset temperature calibration of intervals (p.9: "We fit the temperature by 5-fold calibration on the observational data"). |
| Performance measures | PEHE, ATE relative error, average rank over 310 realisations, normalised Qini, interval coverage (Bayesian coverage vs nominal; integrated coverage error, "ICE"). |
| Main result (numbers) | Tuned comparators, mean PEHE (p.7 Table 1): IHDP 0.58 vs best comparator T-learner 1.73; ACIC 2016 **0.92 vs X-learner 0.60 and BART 0.68 (CausalPFN not best)**; Lalonde CPS 8.96 vs T-learner 9.22 (×10³); PSID 14.40 vs DA-learner 14.55 (×10³); average CATE rank 2.30 vs 3.57 (T-learner). **ATE average rank 4.45 vs T-learner 4.31 and IPW 4.41** (p.7: "competitive for average ATE rank"). Untuned table (p.35 Table 6): on Lalonde PSID the untuned T-learner (13.91) and DA-learner (13.96) beat CausalPFN (14.40). Raw TabPFN beat CausalPFN on ACIC 2016 (0.54 vs 0.92; p.10 Table 3). |
| Failure modes | **Rows > context:** "when we run it on full tables (see Table 7 of Section D.6), we observe a drop in performance" (p.8); full-table Qini average 0.924, last of five methods (p.36 Table 7). **Many covariates:** "the performance gap narrows as the number of covariates grows" (p.34); at 500 covariates PEHE 1.28 equals T-learner 1.28 (p.34 Table 5). **Prior mismatch:** "becomes severely overconfident when evaluated on OOD DGPs" (p.9); fixed by temperature scaling in their synthetic tests. **Sample-size plateau:** "with a slight plateau at very large contexts" (p.34; PEHE 0.29 at 5,000 rows vs 0.31 at 10,000). **Identification:** "Without this condition, CausalPFN has no guarantees of validity" (p.10). **Binary outcomes:** evaluated only via Qini on marketing RCTs with binary visit/conversion outcomes; no PEHE on binary outcomes. **Time-to-event:** not addressed. |
| Code and licence | https://github.com/vdblm/CausalPFN; `pip install causalpfn`. LICENSE file (raw.githubusercontent, main) is titled "CausalPFN License Version 1.0, April 2025" with Apache-2.0-style terms; README states "licensed under the Apache-2.0 License". Code (`src/causalpfn/causal_estimator.py`, main branch, read 3 Nov 2026) reduces dimension when features exceed the model maximum: "the model will apply PCA to reduce the dimensionality" (code comment; implemented with TruncatedSVD). Model-weight licence: UNVERIFIED (Hugging Face not opened). |

### Row 2. Hollmann et al. 2025, TabPFN (v2), Nature (seed; model-description row)

| Field | Content |
|---|---|
| Paper | Hollmann N, Müller S, Purucker L, et al. *Accurate predictions on small data with a tabular foundation model.* Nature 637:319–326. https://doi.org/10.1038/s41586-024-08328-6 |
| Venue and version | Nature 2025, peer reviewed. Read: version of record full text from PubMed Central PMC11711098 (nature.com returned HTTP 429). |
| Model and version | TabPFN v2 (classifier and regressor). |
| Direct or nuisance | Neither in this paper: **no treatment-effect evaluation**. TabPFN-family models (various versions) are used as nuisance, base or risk models in Rows 3, 5, 6, 7, 8, 11, 13, 14, 15, 16. |
| Prior (one line) | SCM-based synthetic tables (Results, "Synthetic data based on causal models": "we developed an approach based on structural causal models (SCMs)"), ~100 million datasets per training run. |
| Identifying assumption | Not applicable (predictive model; no identification). |
| Datasets | AutoML Benchmark and OpenML-CTR23: "29 classification datasets and 28 regression datasets that have up to 10,000 samples, 500 features" (Results). |
| Sample sizes, covariates | Designed and evaluated for ≤10,000 samples and ≤500 features (Limitations: "our evaluation focused on datasets with up to 10,000 samples and 500 features"). |
| Comparators and tuning | Default and tuned XGBoost, CatBoost, random forest; AutoGluon 1.0 (4 h tuned ensemble). |
| Extra advantages to the foundation model | Default inference is a small ensemble with varied preprocessing (Methods: "We generally always apply TabPFN in a small ensemble, in which we perform pre-processing or post-processing of the data differently for each ensemble member"); softmax temperature for calibration (Methods: "we apply a softmax temperature (default T = 0.9)"). Anyone using TabPFN as a nuisance model inherits this ensembling. |
| Performance measures | Normalised ROC AUC, accuracy, RMSE. |
| Main result | Default TabPFN beats default CatBoost by 0.187 normalised ROC AUC (Results: "by 0.187 (0.939 compared with 0.752)"). Causal performance: none reported. |
| Failure modes | "For larger datasets and highly non-smooth regression datasets, approaches such as CatBoost9, XGB7 or AutoGluon40 are likely to outperform TabPFN" (Discussion). Propensity calibration, binary-outcome causal use, time-to-event: not evaluated. |
| Code and licence | Code via Zenodo 10.5281/zenodo.13981285; GitHub PriorLabs/TabPFN code Apache-2.0 (LICENSE file read). Weights: README (read 3 Nov 2026) states TabPFN-2 weights are under "the Prior Labs License (Apache 2.0 with an additional attribution requirement)" and that TabPFN-2.5, 2.6, 3 and 3.5 weights "are released under non-commercial licenses". Synthetic-prior code not released (Code availability: "The code to generate synthetic pre-training data has not been released with our models"). |

### Row 3. Robertson et al. 2025, Do-PFN

| Field | Content |
|---|---|
| Paper | Robertson J, Reuter A, Guo S, Hollmann N, Hutter F, Schölkopf B. *Do-PFN: In-Context Learning for Causal Effect Estimation.* https://arxiv.org/abs/2506.06039v3 |
| Venue and version | NeurIPS 2025, peer reviewed (proceedings DOI 10.52202/085713-5814, confirmed). Read: arXiv v3, 20 Nov 2025. Authors include Prior Labs staff (p.1). |
| Model and version | Do-PFN v1 (7.3M parameters, 48 h training) and v1.1 (96 h, graphs up to 60 nodes) (p.6: "Do-PFN has 7.3 million parameters"). |
| Direct or nuisance | Direct: predicts the CID p(y \| do(t), x); CATE = difference of predicted means (p.8 Eq. 6). |
| Prior (one line) | Random DAG SCMs with additive noise and x², ReLU or tanh mechanisms; observational context plus interventional query rows (p.18 §C: "we uniformly at random sample the nonlinearity γ to be one of the following functions"). |
| Identifying assumption | **None enforced**; the prior may contain non-identifiable SCMs (p.5: "since our prior over SCMs does not necessarily imply identifiability of causal effects"). Consistency only up to observational equivalence class (p.6). |
| Datasets | Six synthetic case studies (front-door, back-door, observed/unobserved confounder, mediator), 100 datasets each; RealCause (four datasets); Amazon Sales and Law School (graph-known, outcomes simulated with DoWhy) (p.6–10). |
| Sample sizes, covariates | Prior: context 10 to 2,200 rows (p.18: "drawn uniformly between Mmin = 10 and Mmax = 2, 200"). RealCause: "range from 10-50 features and up to 10,000 samples" (p.23 §E.1). |
| Comparators and tuning | TabPFN-based S-, T-, X-learner and DML (TabPFN at defaults; no tuning described). EconML S-, T-, X-learner with **FLAML for 60 s per base learner** (p.22: "HPO is performed using FLAML where we tune the each base-learner for 60 seconds"); TARNet and DragonNet via CATENets (tuning not stated, UNVERIFIED); Causal Forest DML "tuned using exhaustive search" (p.22; criterion not stated). DoWhy given the **true graph** (an oracle-informed comparator). Selection criteria: FLAML default nuisance loss (feasible); others not stated. |
| Extra advantages to the foundation model | Synthetic case studies are drawn from SCM families close to its own prior ("Data generation ... varying the SCM parameters as described in Appendix C", p.6). |
| Performance measures | Normalised MSE for CID, CATE, ATE; Nemenyi critical-difference tests; prediction-interval coverage. |
| Main result | Synthetic: "Do-PFN significantly outperforms meta-learners (Künzel et al., 2019), a causal forest double machine learning (DML) approach" (p.8). RealCause: "strong performance among competitive baselines on three out of four RealCause datasets" (p.10). Numbers: figure only (Figs 3, 5). Independent numbers in Rows 1, 4, 10, 11, 12: e.g. IHDP PEHE 6.07 vs CausalPFN 0.58 (Row 1, p.40 Table 8). |
| Failure modes | **Large effects:** "TabPFN’s performance diverges as the base ATE grows ... Do-PFN’s performance also seems to diverge in the largest ATE group" (p.24). **Noise:** "using a two-times larger variance of the Gaussian noise drastically hurts performance" (p.9). **Graph size OOD:** "For larger graphs out of its prior-distribution, we observe a significant reduction in Do-PFN-v1’s performance" (p.9). **Unconfounded RealCause favours baselines:** "inherently advantages the baselines over Do-PFN" (p.10). **Outcome type:** treated as continuous; Mourão et al. (Row 7, p.18) state "Do-PFN is currently limited to continuous outcomes". **Time-to-event, EHR:** not addressed. Authors' limitation: "Do-PFN’s generalization capability critically depends on its synthetic prior over SCMs" (p.10). |
| Code and licence | https://github.com/jr2021/Do-PFN (p.6). No LICENSE, LICENSE.md or LICENSE.txt at raw.githubusercontent (main/master): **licence UNVERIFIED**. |

### Row 4. Ma et al. 2026, CausalFM

| Field | Content |
|---|---|
| Paper | Ma Y, Frauen D, Javurek E, Feuerriegel S. *Foundation Models for Causal Inference via Prior-Data Fitted Networks.* https://arxiv.org/abs/2506.10914v3 |
| Venue and version | ICLR 2026 per the arXiv v3 header (p.1: "Published as a conference paper at ICLR 2026"); iclr.cc page not reachable, so venue confirmation is from the paper itself and web search. Read: arXiv v3, 24 Feb 2026. |
| Model and version | CausalFM (separate checkpoints for back-door, front-door, IV); TabPFN-style per-feature transformer, 10 layers, embedding 128, 5-component Gaussian-mixture head (p.25). |
| Direct or nuisance | Direct: outputs a distribution over Y(1) − Y(0) given x (p.25 Eq. 61–62). |
| Prior (one line) | "causality-inspired Bayesian neural networks" generating covariates from DAG-structured SCMs, MLP propensity and MLP potential outcomes (p.1; p.26 §E). |
| Identifying assumption | Strong ignorability for the back-door model (p.27: "Hence strong ignorability holds"); separate front-door and IV priors. |
| Datasets | Ten synthetic datasets; semi-synthetic Jobs; ACIC 2016 (10 settings); IV and front-door synthetic sets (p.9–10, p.32). |
| Sample sizes, covariates | Training: "Each training datasets contain 1024 data samples. The feature dimensions are also different across the datasets, ranging from 10 to 100" (p.27 §E.7). ACIC 2016: "4802 individuals and 58 covariates" (p.32). Test-set sizes for the ten synthetic datasets: not stated (UNVERIFIED). |
| Comparators and tuning | S-, T-, X-, DR-, RA-learner and TARNet from CATENets; CausalPFN and Do-PFN released checkpoints (p.25 §D.3: "we follow the implementation from https://github. com/AliciaCurth/CATENets"). **No tuning procedure described for comparators (UNVERIFIED; appear to be library defaults).** |
| Extra advantages to the foundation model | Whether the ten synthetic test datasets were generated from the same family as the training prior is not stated; Appendix E, headed as synthetic data generation for standard CATE estimation, describes the training prior (p.26–27) (UNVERIFIED leakage risk). |
| Performance measures | PEHE (mean ± SD over 5 seeds). |
| Main result | Synthetic average PEHE: CausalFM 0.515 ± 0.20, CausalPFN 0.557 ± 0.18, X-learner 0.563 ± 0.15, Do-PFN 0.586 ± 0.19 (p.9 Table 2); Jobs: 0.478 vs Do-PFN 0.482 vs CausalPFN 0.528. Differences are well inside one SD. **ACIC 2016: CausalPFN 0.239 vs CausalFM 0.638 vs X-learner 0.519 (CausalFM worse than a default X-learner)** (p.32 Table 6). |
| Failure modes | ACIC 2016 underperformance (above). Using the wrong identification prior raises PEHE (p.34 Table 9: IV data 0.422 correct vs 0.489 back-door). Authors: "The current evaluation is limited to synthetic and semi-synthetic data" (p.10). In external benchmarks CausalFM shrinks ATE towards zero (Row 10: ATE relative error 0.94 on Lalonde CPS). Binary outcomes, time-to-event, EHR: not evaluated. |
| Code and licence | https://github.com/yccm/CausalFM and CausalFM-toolkit; Apache-2.0 (LICENSE files read). |

### Row 5. Zhang, Tan, Tian, Li 2025, "TabPFN: One Model to Rule Them All?"

| Field | Content |
|---|---|
| Paper | Zhang Q, Tan YS, Tian Q, Li P. https://arxiv.org/abs/2505.20003v2 |
| Venue and version | Preprint (arXiv v2, 27 Nov 2025). Peer-review status UNVERIFIED. |
| Model and version | TabPFN v2 (p.1 footnote: "all experiments and discussion in this paper are based on TabPFNv2"). |
| Direct or nuisance | Nuisance/base learner in S-, T-, X-, DR-learners; TabPFN classifier for propensity (p.17: "we use the TabPFN classifier to estimate the propensity score model"). |
| Prior | TabPFN v2 prior (Row 2). |
| Identifying assumption | Ignorability (p.5 §3.2.2). |
| Datasets | (i) Six simulation setups (A–F) from Foster and Syrgkanis, X ~ Unif([−.5,.5]^6), n = 500 or 2,000, test n = 10,000, 100 repetitions (p.6); (ii) ACIC 2017 semi-synthetic benchmark on IHDP covariates, 24 DGPs × 250 replications = 6,000 datasets (p.17). |
| Sample sizes, covariates | Simulation d = 6; ACIC 2017: "n = 4302 subjects with 8 covariates" (p.17, as stated by the authors). |
| Comparators and tuning | Simulation: same meta-learners with **FLAML AutoML base learners, 5-fold CV** (p.17: "We use the 5fold cross-validation to choose the optimal algorithms and its corresponding hyperparameters"), feasible nuisance criterion; R-learner and oracle R-learner with AutoML only ("TabPFN currently does not support weighted loss minimization", p.6). ACIC 2017: 16 challenge methods incl. GRF, TMLE, BART variants, BCF; results "taken directly from Richard Hahn’s personal website and were not recalculated" (p.17), so their tuning is whatever challenge entrants used (not reported here). |
| Extra advantages to the foundation model | TabPFN at defaults (with its built-in ensemble, Row 2). For strong confounding they add the TabPFN propensity score as a covariate (BCF-style) to S-, T-, X-learners (p.7). |
| Performance measures | Test MSE of CATE (simulation); RMSE of CATE (ACIC 2017). |
| Main result | "using TabPFN as the base learner in a meta-learner strategy greatly improves upon its AutoML counterpart" and S-Learner (TabPFN) "achieves the best accuracy in most settings" (p.6). ACIC 2017: "Under weak selection strength, all TabPFNbased estimators match or outperform the baselines" (p.7). Numbers: figure/Table 7 (medians), not transcribed. |
| Failure modes | **Strong confounding:** "Under strong selection strength, their performance degrades somewhat" (p.7), attributed to regularisation-induced confounding; partly fixed by the propensity covariate. **DR-learner** "does not have the best performance in any setting" (p.7). **Scale:** "Current implementations struggle with dense/high-dimensional regression and > 10K samples" (p.12). Binary outcomes, time-to-event, EHR, propensity calibration: not evaluated. |
| Code and licence | https://github.com/qinglong-tian/tabpfn_study; no LICENSE file at raw (main/master): **licence UNVERIFIED**. |

### Row 6. Grinsztajn et al. 2025, TabPFN-2.5 technical report (causal section)

| Field | Content |
|---|---|
| Paper | Grinsztajn L, Flöge K, Key O, et al. *TabPFN-2.5: Advancing the State of the Art in Tabular Foundation Models.* https://arxiv.org/abs/2511.08667v2 |
| Venue and version | Vendor technical report (Prior Labs), not peer reviewed. Read: arXiv v2. |
| Model and version | TabPFN-2.5 (p.1: "built for datasets with up to 50,000 data points and 2,000 features"). |
| Direct or nuisance | Base learner in T-, X-, S-learners (p.29 §D). |
| Prior | TabPFN-2.5 synthetic prior (not detailed for causal use). |
| Identifying assumption | Unconfoundedness (p.29: "Many causal inference methods require unconfoundedness"). |
| Datasets | RealCause: ACIC 2016 (10 realisations, 4,802 × 58), IHDP (100, 747 × 25), Lalonde CPS (100, 16,177 × 8), Lalonde PSID (100, 2,675 × 8) (p.30 Table 3). |
| Sample sizes, covariates | As above. |
| Comparators and tuning | Meta-learners with TabPFNv2 and with HPO base learners, "Hyperparameter optimization is run for 60 seconds on an H100 per propensity and outcome model using FLAML" (p.9, footnote 5); "specialized tree- and deep-learning-based methods" (identity and tuning not given in text, UNVERIFIED). |
| Extra advantages to the foundation model | Default TabPFN-2.5 (with built-in ensembling) vs 60-s HPO comparators. |
| Performance measures | PEHE. |
| Main result | "PFN-based methods for CATE-estimation dominate the leaderboard, occupying the first seven positions" (p.7); TabPFN-2.5 as a T-learner "achieves the strongest overall performance" (p.9). Numbers: **figure only** (Figs 9–10), not transcribed. |
| Failure modes | The report itself notes the unconfounded setting only ("While we show strong results in unconfounded settings, real-world causal inference often involves imperfect data and latent confounders", p.9). No binary, survival, EHR or calibration evaluation. |
| Code and licence | Weights: "TABPFN-2.5 License v1.0" — "the model, its derivatives, and its outputs cannot be used for any commercial or production purpose" (p.10 §6). |

### Row 7. Mourão et al. 2026, PFNs for causal inference: simulation with real-world clinical scenarios

| Field | Content |
|---|---|
| Paper | Mourão F, Hajage D, Bystrova D, Bouvarel B, Lapidus N, Carrat F, Glemain B. *Prior-Data Fitted Networks for Causal Inference: a Simulation Study with Real-World Scenarios.* https://arxiv.org/abs/2603.15928v2 |
| Venue and version | Preprint (arXiv v2, 13 Apr 2026, stat.AP). |
| Model and version | TabPFN package 2.1.0; CausalPFN package 0.1.4 (p.10: "TabPFN was implemented using the tabpfn Python package, version 2.1.0"). |
| Direct or nuisance | Both: TabPFN as outcome model (single-model g-computation and T-learner) and propensity model (IPTW, Hájek); CausalPFN direct ATE with its own credible interval. |
| Prior | TabPFN v2 prior; CausalPFN prior (Row 1). |
| Identifying assumption | Positivity, conditional exchangeability, consistency hold by construction (p.7). |
| Datasets | Two plasmode-style scenarios built from empirical distributions of real data: Indomethacin trial data (pancreatic sphincterotomy → post-ERCP pancreatitis) and Rotterdam breast-cancer cohort (chemotherapy → death or recurrence at 5 years) (p.11–12). |
| Sample sizes, covariates | n = 200, 500, 1,000; 1,000 simulated datasets each. Confounders binarised into one categorical Z: Indomethacin 14 strata (4 confounders), Rotterdam 98 strata (8 confounders) (p.11–12). **Binary treatment and binary outcome; estimand is ATE (risk difference), not CATE.** |
| Comparators and tuning | Logistic regression without interactions ("this model is misspecified", p.8) and **XGBoost at default settings "without hyperparameter tuning (to limit computational burden)"** (p.5) — a compute-driven choice that weakens the comparator; crude difference in means. 95% CIs by percentile bootstrap, 599 iterations. |
| Extra advantages to the foundation model | None; TabPFN and CausalPFN at defaults. Whether CausalPFN's optional temperature calibration was enabled is not stated (UNVERIFIED). |
| Performance measures | 95% CI coverage, mean width, bias-eliminated coverage, mean error, MSE. |
| Main result | CausalPFN coverage "54.3% and 67.6%, respectively, for the scenarios Indomethacin and Rotterdam with sample size n = 1, 000" (p.15); TabPFN single-model g-computation 88.1% and 86.4%; TabPFN T-learner 93.7% and 91.5%; "TabPFN-based IPTW achieved near-nominal 95% CI coverage rates" (p.15). Mean error ×10³ at n = 1,000 (Indomethacin, true ATE −0.062): CausalPFN 30.73, TabPFN g-computation 25.74, TabPFN IPTW −3.2 (p.13 Table 1). |
| Failure modes | **Binary outcomes, small n:** CausalPFN under-covers at every n; "correcting CIs for bias resulted in only a modest improvement in coverage for CausalPFN" (p.17). **S-learner shrinkage** with TabPFN ("g-computation with TabPFN produced a highly biased estimator, partially corrected by fitting separate models for each treatment group", p.1). **Time-to-event:** Rotterdam outcome was converted to a binary 5-year outcome after excluding patients lost to follow-up (p.12), so censoring was not handled. Authors: "the limited performance of CausalPFN currently preclude their practical use in causal inference" (p.19). |
| Code and licence | https://github.com/franciscomourao/PFNs Causal Inference (URL as printed, p.11); licence UNVERIFIED (GitHub not reachable). Article: "A CC-BY license has been applied by the authors" (p.20). |

### Row 8. Melnychuk et al. 2026, frequentist consistency of PFNs for causal inference

| Field | Content |
|---|---|
| Paper | Melnychuk V, Balazadeh V, Feuerriegel S, Krishnan RG. *Frequentist Consistency of Prior-Data Fitted Networks for Causal Inference.* https://arxiv.org/abs/2603.12037v3 ; https://proceedings.mlr.press/v306/melnychuk26a.html |
| Venue and version | ICML 2026 (PMLR 306), peer reviewed (listing confirmed on proceedings.mlr.press). Read: arXiv v3, 22 Jul 2026. |
| Model and version | TabPFN, CausalPFN, CausalFM (as Bayesian ATE estimators), plus the authors' martingale-posterior one-step posterior correction (MP-OSPC). |
| Direct or nuisance | Both: TabPFN propensity (p.8: "we employ the propensity score estimated with TabPFN"); CausalPFN outcome posteriors. |
| Prior | Analyses the implicit priors of existing PFNs. |
| Identifying assumption | Ignorability (potential-outcomes framework). |
| Datasets | Synthetic (Curth & van der Schaar generator, observed confounding Δ ≈ −0.5); IHDP (n = 672 + 75, dx = 25); 77 ACIC 2016 datasets (n = 4,802, dx = 82) (p.8). |
| Sample sizes, covariates | As above; synthetic n varied up to >5,000. |
| Comparators and tuning | Reference is the asymptotic A-IPTW distribution; baselines are naive CausalPFN plug-ins at several temperatures and MP plug-ins. **No CATE comparators (ATE only).** |
| Extra advantages to the foundation model | Not applicable (methodological paper). |
| Performance measures | Total-variation distance to the A-IPTW asymptotic law; Kolmogorov–Smirnov distance of posterior CDF at the truth (frequentist calibration). |
| Main result | Existing PFNs' priors concentrate observed confounding near zero: "∆ is still highly concentrated around zero for the PFNs" (p.5), giving "prior-induced confounding bias" (p.1). MP-OSPC "consistently improves upon the corresponding plug-in baselines" on ACIC 2016 (p.9). |
| Failure modes | **Propensity scores from TabPFN:** "This appears to be a limitation of TabPFN in accurately recovering propensity score posteriors, particularly in regions where the true propensity scores are close to 0 or 1" (p.9). **Strong confounding:** prior shrinks confounding (above). **Large n:** "current PFNs lack formal asymptotic guarantees ... and, thus, are mainly useful for medium-sized datasets" (p.9). **CATE:** "the extension to the heterogeneous treatment effects is an open research problem" (p.9). |
| Code and licence | Not checked (UNVERIFIED). |

### Row 9. Schulman, Bynum, Wald 2026, unit-level aggregation breaks coverage

| Field | Content |
|---|---|
| Paper | *Unit-level aggregation breaks coverage in causal foundation models.* https://arxiv.org/abs/2610.22770v1 |
| Venue and version | Preprint (arXiv v1, 16 Oct 2026). |
| Model and version | Released CausalPFN (no retraining), plus the authors' conditional and latent neural-process heads on a frozen CausalPFN. |
| Direct or nuisance | Direct (CausalPFN intervals for subset-CATEs and ATE). |
| Prior | CausalPFN's; heads trained on "a broader prior with n between 100 and 5000 and up to 60 covariates" (p.8). |
| Identifying assumption | No unobserved confounding, positivity (p.5); notes "IHDP and some ACIC 2016 settings have limited overlap" (p.5). |
| Datasets | Six benchmarks: Hill-A, Hill-B, Friedman, Kang–Schafer, IHDP, ACIC 2016, 40 datasets each; a synthetic family with three covariates and n = 500 (p.7–8, p.20). |
| Sample sizes, covariates | As above; ACIC 2016 4,802 units. |
| Comparators and tuning | No non-foundation CATE estimators; comparison is between aggregation rules. CausalPFN's built-in temperature calibration enabled on benchmarks (p.8). |
| Extra advantages to the foundation model | Calibration enabled (favours CausalPFN). |
| Performance measures | Coverage of nominal 95% intervals for subset-CATEs as subset size grows. |
| Main result | On ACIC 2016 CausalPFN's full-sample interval "contains the true full-sample average in only 8 of the 40 datasets we use when calibrated and in 18 of 40 when not" (p.2). Over six benchmarks, NP heads cover the full-sample average "in 90% and 89% of 240 datasets, against 25% and 52% for unit-level aggregation from the same weights and 53% for CausalPFN" (p.3). |
| Failure modes | Interval coverage for group averages (ATE, subgroups) degrades with group size because unit errors are correlated through posterior uncertainty about the SCM (p.2). "rescaling unit-level intervals to be calibrated did not help in our experiments" (p.10). |
| Code and licence | https://github.com/gabeschulman-nyu/subset-cate-coverage (p.11); licence UNVERIFIED. |

### Row 10. Stith, Rahmani, Cresswell 2026, "Causal Foundation Models" (tutorial with benchmark)

| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.03003v1 |
| Venue and version | Preprint (arXiv v1, Sep 2026). Authors at Layer 6 AI; Cresswell is a CausalPFN co-author (Row 1): not independent of CausalPFN. |
| Model and version | Frozen released checkpoints of Do-PFN, CausalPFN, CausalFM (p.19). |
| Direct or nuisance | Direct. |
| Prior | Those of Rows 1, 3, 4. |
| Identifying assumption | Ignorability (RealCause guarantees it, p.18). |
| Datasets | RealCause Lalonde-CPS (16,177) and Lalonde-PSID (2,675), 10 realisations (p.18: "We evaluate on the semi-synthetic Lalonde-CPS (16,177 samples) and Lalonde-PSID (2,675 samples) cohorts"). |
| Sample sizes, covariates | 8 covariates (Row 6 Table 3). |
| Comparators and tuning | EconML S-, T-, X-, DR-learner, DML, IPW with **FLAML per nuisance, per estimator, per realisation, 900-s budget, 3-fold CV; R² for outcome models, ROC-AUC for propensity models** (p.18) — feasible nuisance-level criteria; DR final stage causal forest (1,000 trees, 5-fold CV, degree-3 polynomial features); DML linear final stage. |
| Extra advantages to the foundation model | None (frozen, untuned); covariates and outcomes standardised identically for all CFMs (p.20). |
| Performance measures | PEHE, ATE relative error, average rank. |
| Main result | PEHE ×10³ (p.20 Table 3): CPS CausalPFN 8.97 vs T-learner 9.04; **PSID T-learner 13.65 vs CausalPFN 14.00**; average PEHE rank T-learner 1.40 vs CausalPFN 1.75; Do-PFN 11.96/20.20; CausalFM 12.34/22.27. "our CausalPFN results independently replicate the values reported by Balazadeh et al. (2025)" (p.20). |
| Failure modes | Do-PFN and CausalFM "remain near a relative error of 1 on both cohorts (0.88 and 0.94)", i.e. "a systematic shrinkage of the predicted effect toward zero" (p.20). |
| Code and licence | https://github.com/layer6ai-labs/cfms, MIT (LICENSE read). |

### Row 11. Jung et al. 2026, CausalIDView benchmark

| Field | Content |
|---|---|
| Paper | Jung H, Seo G, Byun H, Lee J, Song K. *What You Observe Determines How You Identify Causal Effects: Evaluating Causal Models across Observational Views.* https://arxiv.org/abs/2609.36881v1 |
| Venue and version | Preprint (arXiv v1, 29 Sep 2026). |
| Model and version | CausalPFN, Do-PFN, CausalFM released checkpoints "without fine-tuning" (p.26); TabPFN-v3.5 as nuisance model. |
| Direct or nuisance | Both. TabPFN-3.5 inside S-, X-, DR-learners (back-door), front-door plug-in, IV Wald ratio, proximal P-learner (p.7). |
| Prior | Not applicable (benchmark). |
| Identifying assumption | Back-door, front-door, IV, proximal views of one SCM; hidden-confounding stress view (p.2–5). |
| Datasets | 40 synthetic "worlds"; ACIC 2016 (40 settings), RealCause Lalonde-PSID/CPS (40 realisations); null-effect tests on three RCTs using pre-treatment outcomes: ACTG 175 (HIV; baseline CD4), Pennsylvania and Illinois re-employment experiments (p.5–6, p.29–30). |
| Sample sizes, covariates | Synthetic: 1,024 context, 100 query units, X ∈ R^50 plus confounder (p.21). Semi-synthetic: 1,024 context, 100 query; ACIC 58 columns; RealCause 8 covariates (p.29–30). RCTs: context 768, 1,024, 2,048 (p.30). |
| Comparators and tuning | Causal Tree, TARNet, GRF/Causal Forest, CFRNet; XGBoost (300 trees, depth 3), MLP, ExtraTrees: **"All remaining parameters use the corresponding package defaults and we perform no hyperparameter optimization"** (p.27). So no arm was tuned. |
| Extra advantages to the foundation model | TabPFN-3.5 at defaults (with its built-in ensembling). CausalPFN/Do-PFN received auxiliary variables "as ordinary covariates without role annotations" (p.26), a disadvantage in non-back-door views. |
| Performance measures | sPEHE² (scaled PEHE squared), ATE error², centred sPEHE², Stay/Move structural-response errors, null-CATE error. |
| Main result | ACIC 2016 sPEHE² (p.9 Table 1): TabPFN-3.5 X-learner 1.11, DR 1.17, S 1.25 vs CausalPFN 3.24, GRF 8.30, CausalFM 23.56, Do-PFN 31.48. Lalonde-PSID: CFRNet 18.4, TabPFN-DR 42.8, CausalPFN 44.0; Lalonde-CPS: CausalPFN 11.2, TabPFN-DR 15.3. "no consistently best estimator" (p.9). |
| Failure modes | "CausalPFN shows relatively large Stay errors ... Do-PFN shows consistently large Move errors" (p.8). Rankings change across identification regimes (p.1). Omitting a confounder: "Most models show pronounced error increases" (p.8). TabPFN-X-learner is worst on Lalonde-PSID (456 vs CFRNet 18.4, p.9 Table 1). |
| Code and licence | https://github.com/MLAI-Yonsei/CausalIDView (p.1); licence UNVERIFIED. |

### Row 12. Reuter et al. 2026, causal foundation models with partial graphs

| Field | Content |
|---|---|
| Paper | Reuter A, Dhir A, Diaconu C, Robertson J, Ossen O, Hutter F, Weller A, van der Wilk M, Schölkopf B. *Use What You Know: Causal Foundation Models with Partial Graphs.* https://arxiv.org/abs/2602.14972v3 ; https://proceedings.mlr.press/v306/reuter26a.html |
| Venue and version | ICML 2026 (PMLR 306), peer reviewed (listing confirmed). Read: arXiv v3. |
| Model and version | Graph-conditioned CFM (attention bias + graph-convolutional encoder); compared with CausalPFN, CausalFM, Do-PFN. |
| Direct or nuisance | Direct. |
| Prior | "complex-mechanism prior" over SCMs (p.9). |
| Identifying assumption | Varies; RealCause runs supply partial ancestral information encoding unconfoundedness (p.9). |
| Datasets | RealCause IHDP, ACIC, CPS, PSID, and a rebalanced PSID (p.33 Table 3). |
| Sample sizes, covariates | PSID: "141 individuals" treated vs "2266 individuals" untreated (p.24 §F.3). |
| Comparators and tuning | Only foundation models (no BART/GRF/meta-learners). |
| Extra advantages to the foundation model | Not applicable. |
| Performance measures | √PEHE, ATE relative error. |
| Main result | CausalPFN best on all RealCause datasets, e.g. IHDP √PEHE 0.58 vs CausalFM 5.86, Do-PFN 6.07, graph-conditioned 5.49 (p.33 Table 3). |
| Failure modes | **Prior–benchmark alignment:** CausalPFN's advantage is attributed "to its training data closely mimicking the RealCause data-generating process" (p.33). **Weak overlap / imbalance:** on PSID "all methods achieve suboptimal performance, which we find is due to the highly imbalanced distribution of treated versus untreated individuals" (p.9). |
| Code and licence | Not checked (UNVERIFIED). |

### Row 13. Grinsztajn et al. 2026, TabPFN-3 technical report (causal section)

| Field | Content |
|---|---|
| Paper | *TabPFN-3: Technical Report.* https://arxiv.org/abs/2605.13986v2 |
| Venue and version | Vendor technical report (Prior Labs), not peer reviewed; arXiv v2. |
| Model and version | TabPFN-3 (p.1: "scale state-of-the-art performance to datasets with 1M training rows"). |
| Direct or nuisance | Base learner in T-, X-, S-learners. |
| Prior / assumption | TabPFN-3 prior; unconfoundedness. |
| Datasets | RealCause; scikit-uplift RCTs "with up to 50k samples" (p.50). |
| Comparators and tuning | TabPFN-2.5 meta-learners; others not described in text (UNVERIFIED). |
| Main result | Uplift: "all TabPFN-3 meta-learners improve over TabPFN-2.5" (p.21). Figure only. |
| Failure modes | **A stronger predictive model did not give better CATE:** "we observe slightly worse performance compared to TabPFN-2.5 on RealCause" (p.21), described as "characterized by smaller sample sizes" (p.51). |
| Code and licence | Weights non-commercial (Row 2 README). |

### Row 14. Liu et al. 2026, TabPFN outcome models as virtual controls in a paediatric Crohn's disease cohort

| Field | Content |
|---|---|
| Paper | Liu D, Dankar FK, deBruyn JC, Ricciuto A, Griffiths AM, et al. *Machine learning models for estimating counterfactuals in a single-arm inflammatory bowel disease study.* https://arxiv.org/abs/2604.23465v1 |
| Venue and version | Preprint (arXiv v1, Apr 2026). |
| Model and version | TabPFN (version not stated, UNVERIFIED). |
| Direct or nuisance | Nuisance: outcome model trained on the infliximab (IFX) arm, applied to adalimumab (ADA) patients to impute counterfactuals (an ATT-type T-learner arm). |
| Prior / assumption | TabPFN prior; no unmeasured confounding implicitly (compared against a propensity-matched reference). |
| Datasets | Canadian Children IBD Network (CIDsCaNN): "a prospective national multicenter cohort study" (p.8) — a research cohort, not routinely collected EHR or claims. |
| Sample sizes, covariates | "613 children and 29 baseline predictor variables" (p.8); 437 IFX for training, 147 matched ADA. Binary 1-year outcomes. |
| Comparators and tuning | LightGBM, XGBoost, random forest, logistic regression with Bayesian optimisation in nested 5-fold CV; "Bayesian optimization for hyperparameter tuning was applied only to the non-pretrained models" (p.9). TabPFN untuned. |
| Extra advantages | None (TabPFN at defaults); synthetic-data augmentation tested for all models. |
| Performance measures | AUC and ICI (integrated calibration index) of the outcome model; odds ratio vs propensity-score-matched reference (no true effect). |
| Main result | "TabPFN achieves the highest baseline AUC and lowest baseline ICI in both outcome scenarios" (p.13), but "LGBM provides OR estimates that are consistently closest to the original ORs across all settings" (p.13). |
| Failure modes | Better outcome-model calibration did not translate into the closest effect estimate; no ground truth. |
| Code and licence | Not checked (UNVERIFIED). |

### Row 15. Kurmann et al. 2026, TabPFN risk model for heterogeneity of endovascular treatment effect in DISTAL (abstract only)

| Field | Content |
|---|---|
| Paper | Kurmann C, Fischer U, Rommers N, et al. *Differential Effect of Endovascular Treatment in Medium or Distal Vessel Occlusion: A Distal Secondary Analysis.* Stroke 2026. https://doi.org/10.1161/STROKEAHA.126.057558 (PMID 42961033) |
| Venue and version | Stroke, peer reviewed, online ahead of print 30 Oct 2026. **Abstract only** (PubMed); full text not reachable. |
| Model and version | TabPFN (version UNVERIFIED). |
| Direct or nuisance | Nuisance-like: a prognostic (risk) model under best medical treatment, used to stratify an RCT (risk-based heterogeneity analysis, not CATE estimation). |
| Prior / assumption | Randomisation in DISTAL. |
| Datasets | Development: Bernese Stroke Registry, n = 257; application: DISTAL RCT, 270 BMT vs 269 EVT+BMT (abstract). Predictors: UNVERIFIED (not listed in abstract; whether imaging-derived is unknown). |
| Comparators and tuning | NIHSS-alone model (abstract: "A model using admission NIHSS alone showed comparable discrimination (area under the receiver operating characteristic curve 0.71)"). |
| Main result | External AUC 0.73; "A significant interaction was found between predicted EENO and treatment effect (Pinteraction=0.012)" (abstract). |
| Failure modes | TabPFN risk model no better than a single clinical score for stratification (comparable AUC 0.73 vs 0.71). No ground-truth CATE. |
| Code and licence | UNVERIFIED. |

### Row 16. Ebrahim 2026, calibration of TFM risk predictions against the true risk (indirect evidence for nuisance-model calibration)

| Field | Content |
|---|---|
| Paper | Ebrahim EK. *Tabular foundation models are not a shortcut to calibrated clinical risk prediction: a pre-registered simulation against the true risk.* https://arxiv.org/abs/2610.39065v1 |
| Venue and version | Preprint (arXiv v1, 28 Oct 2026), pre-registered (OSF). |
| Model and version | TabPFN-3.5, TabICLv2, Mitra-v2 at shipped settings (p.4: "Shipped softmax temperature: TabPFN-3.5 1.0, TabICLv2 0.9; Mitra-v2 has none"). |
| Direct or nuisance | Neither directly: binary-outcome risk models. Relevant because such models are the outcome and propensity components of meta-learners, IPTW and DML. **Not a treatment-effect paper.** |
| Datasets | 48 core scenarios: four outcome shapes × event rate 3%, 10%, 30% × n 200, 500, 1,000, 3,000; 1,000 random designs with 4–30 predictors; four clinical datasets with a plasmode tier (p.3, p.14). |
| Comparators and tuning | Firth logistic regression with intercept correction (FLIC, reference), maximum-likelihood, ridge logistic, GAM, LightGBM with Platt scaling (p.3). |
| Performance measures | True ICI, true calibration slope and intercept (against known risk). |
| Main result | "Foundation models were not a shortcut to calibration" (p.1); "Even 3,000 patients were often not enough" (p.1); "TabICLv2 did worse" (p.1); "On real data, no model resisted a change in event rate between populations; recalibration on 500 local patients largely repaired it" (p.1). |
| Failure modes | Calibration at small n and rare events; transport across event rates. |
| Code and licence | Code doi:10.5281/zenodo.23737378 (arXiv comment); licence UNVERIFIED. |

## 2b. Capability table: context length and feature limits (no causal evaluation in these sources unless stated)

| Model | Rows (n) | Features | Outcome types | Source (verbatim) |
|---|---|---|---|---|
| CausalPFN | Trained ≤2,048; default inference 4,096; tested to 50,000 in context; retrieval beyond | Trained ≤100; SVD/PCA reduction above the model maximum (code) | Continuous target; binary outcomes only via Qini | Row 1, p.34: "we consider sample sizes up to 2,048 and covariates up to 100" |
| Do-PFN | Prior 10–2,200 | RealCause 10–50 tested | Continuous | Row 3, p.18; Row 7, p.18 |
| CausalFM | Training tables 1,024 rows | 10–100 | Continuous | Row 4, p.27 |
| TabPFN v2 | ≤10,000 | ≤500 | Classification, regression | Row 2, Limitations |
| TabPFN-2.5 | ≤50,000 | ≤2,000 | Classification, regression | Row 6, p.1 |
| TabPFN-3 | to 1M training rows | "200 features" in large-data benchmark | Classification, regression | arXiv 2605.13986v2 p.1: "datasets up to 1M training rows and 200 features" |
| TabPFN-3.5 | ≤1,000,000 | ≤20,000 | Classification, regression | PriorLabs/TabPFN README (read 3 Nov 2026): "accept up to **1,000,000 rows** and **20,000 features**"; report arXiv 2609.17895v2 (no causal content found) |
| TabICL | "capable of handling 500K samples" | not stated in abstract | **Classification only** (v1) | Qu et al., ICML 2025, arXiv 2502.05564v2 abstract: "a tabular foundation model for classification, pretrained on synthetic datasets with up to 60K samples" |
| TabICLv2 | "million-scale datasets under 50 GB" GPU memory | not checked | Regression and classification | Qu et al., ICML 2026, arXiv 2602.11139v2 abstract; no causal evaluation found in full text |

No TabICL or TabICLv2 paper was found that uses them as nuisance models for a treatment effect; TabICLv2 appears only in Row 16 (risk calibration).

---

## 3. Synthesis (what is established, contested, missing)

**Established.**
1. On standard semi-synthetic back-door benchmarks (IHDP, ACIC 2016, RealCause Lalonde), the released CausalPFN reaches CATE error comparable with or better than tuned meta-learners without any per-dataset tuning, and an independent replication reproduced its numbers (Rows 1, 10). Its average CATE rank is best in its own paper (2.30 vs 3.57) but second to a FLAML-tuned T-learner in the replication (1.75 vs 1.40), and it is not best on ACIC 2016 (Row 1: 0.92 vs X-learner 0.60) nor on Lalonde-PSID against a tuned T-learner (Row 10).
2. TabPFN used as the base learner of standard meta-learners is a strong, cheap comparator: it beat AutoML-based meta-learners in simulations, matched or beat BART, BCF and GRF on ACIC 2017 under weak confounding, and gave the lowest error on ACIC 2016 in an untuned benchmark (Rows 5, 11; vendor claims Rows 6, 13). The base learner matters as much as the meta-learner (Row 5, p.7).
3. Interval calibration is the main documented weakness of the direct models. CausalPFN credible intervals are overconfident out of prior (Row 1), under-cover the ATE in binary-outcome clinical simulations (54–68% at n = 1,000; Row 7), and lose coverage for group averages because unit-level errors are correlated (Row 9). PFN priors concentrate observed confounding near zero, which can prevent frequentist consistency for the ATE (Row 8).
4. The other direct models (Do-PFN, CausalFM) are clearly worse than CausalPFN on IHDP, ACIC 2016 and RealCause Lalonde, and shrink the ATE towards zero there (Rows 4, 10, 11, 12), although CausalFM was marginally better on its own synthetic sets and semi-synthetic Jobs data (Row 4).

**Contested.**
1. Whether CausalPFN's benchmark advantage reflects generality or prior–benchmark alignment: Reuter et al. attribute it to CausalPFN's prior "closely mimicking the RealCause data-generating process" (Row 12). Do-PFN and CausalFM evaluations also used test data from families close to their priors (Rows 3, 4).
2. Whether direct models beat TabPFN-based meta-learners: CausalPFN beat raw TabPFN on three of four benchmarks (Row 1), but TabPFN-3.5 meta-learners beat CausalPFN on ACIC 2016 and on two of three RCT null tests in an untuned benchmark (Row 11); a newer TabPFN (3) was slightly worse than 2.5 for CATE (Row 13).
3. Rankings change with confounding strength, overlap and identification regime (Rows 5, 11, 12).

**Missing.**
1. No study evaluates any pre-trained model on routinely collected EHR or claims data for CATE (see §4.1).
2. No study uses image-derived covariates (§4.2).
3. No causal PFN or TFM-based estimator handles censored time-to-event outcomes for treatment effects (§4.3).
4. No study gives comparators equal, CATE-targeted tuning; all tuned arms used nuisance-level, feasible criteria with short budgets, and some arms were untuned (§4.4).
5. No study directly checks the calibration of TFM propensity scores (§4.5).

**Relevance to application A (lesion representations, binary outcomes, 300–3,000 patients, randomised and confounded).** Sample size is within every model's trained range (CausalPFN trained to 2,048 rows, default context 4,096; TabPFN v2 to 10,000; §2b), so context length is not the constraint. The constraints are: (i) binary outcomes, where the only clinical simulation found reports poor CausalPFN coverage and biased single-model TabPFN g-computation, while TabPFN T-learner and IPTW behaved better (Row 7); (ii) representation width: if lesion embeddings exceed ~100 dimensions, CausalPFN projects them by SVD and its advantage disappears by 500 covariates (Row 1, Table 5); (iii) synthetic-to-synthetic evaluation risks the prior-alignment problem of Row 12 if the semi-synthetic mechanisms resemble a model's prior. (Inference, not a finding of any row: in the randomised arm of the virtual trials the propensity is known by design, so the TabPFN propensity weakness near 0 and 1 reported in Row 8 matters only for the confounded arm.)

**Relevance to application B (CPRD Aurum, 56,337 people, ~540 features, HbA1c and later time-to-event outcomes).** n exceeds CausalPFN's default context by ~14× and TabPFN v2's limit by ~5.6×; CausalPFN degraded on full-size marketing tables with retrieval (Row 1, Table 7); TabPFN-2.5 (50,000/2,000), TabPFN-3 and TabPFN-3.5 (to 1M rows) and TabICLv2 nominally cover this size (§2b) but have no causal evaluation at that scale (the largest causal evaluations are 50k-row uplift subsamples, Rows 1 and 13), and the 2.5+ weights are licensed non-commercially (Rows 2, 6). Around 540 features exceed CausalPFN's 100-feature training range and TabPFN v2's 500-feature range. HbA1c is a continuous outcome, which the direct models handle; time-to-event outcomes have no causal-PFN or TFM-nuisance evidence at all. The closest clinical evidence (Rows 14, 15, 16) concerns prognostic or risk models, not CATE, and shows that strong discrimination or calibration of the outcome model did not guarantee the best effect estimate (Row 14) and that TFM risk calibration needs thousands of patients and local recalibration (Row 16).

---

## 4. Answers to the "Answer explicitly" questions

### 4.1 Is there any evidence on EHR or claims data?
**No evidence for CATE estimation by pre-trained in-context models on EHR or claims data.** Closest items: Row 7 builds plasmode-style scenarios from a trial dataset and a tumour-bank cohort (ATE, binary, ≤1,000 patients, ≤8 binarised confounders); Row 14 applies TabPFN as an outcome model in a prospective multicentre research cohort (613 children, 29 predictors), validated only against a propensity-matched estimate; Row 15 uses a registry-trained TabPFN risk model to stratify an RCT (abstract only). Row 11 uses three RCTs (ACTG 175, Pennsylvania, Illinois) for null-effect tests. CaML (near-miss N3) uses "large-scale medical claims", but it is meta-trained inside that claims database to predict effects of unseen drugs, not an in-context model applied to a new dataset. No CPRD study was found.

### 4.2 Is there evidence on image-derived covariates?
**None.** No included study uses imaging-derived covariates or learned image representations as inputs to a causal PFN or a TFM-based effect estimator. Row 15 concerns a stroke trial, but the abstract does not state whether any predictor is imaging-derived (UNVERIFIED). TabPFN-3.5 advertises image support for prediction (arXiv 2609.17895v2 abstract: "tables with strings, text and images"), with no causal evaluation.

### 4.3 Is there evidence on time-to-event outcomes?
**None for treatment effects.** No causal PFN (Rows 1, 3, 4, 12) handles censored outcomes; Row 7 converted a survival outcome to a 5-year binary outcome after excluding the ~4% lost to follow-up (p.12). Survival prediction PFNs and TFM adaptations exist (SurvPFN, Survival In-Context, SurvFM, "Staying Alive", Pham et al.; near-misses N19–N23) but none estimates treatment effects. Stith et al. list these as broader directions only (Row 10 source, p.24 §5.4.2).

### 4.4 Did comparators get comparable tuning effort?
**No study gave comparable, CATE-targeted tuning, and the direction of imbalance varies.**
- Foundation models were always used untuned, but they carry built-in ensembling/preprocessing (TabPFN, Row 2) and, for CausalPFN, optional per-dataset temperature calibration (Rows 1, 9).
- Tuned comparators used **feasible, nuisance-level** criteria with fixed budgets: FLAML 900 s, 3-fold CV (Rows 1, 10; R² and ROC-AUC in Row 10); FLAML 60 s per model (Rows 3, 6); FLAML 5-fold CV (Row 5). None selected the final CATE model with a CATE-targeted criterion (for example an R-loss or DR pseudo-outcome loss), and none used oracle selection.
- Untuned or weakly tuned comparators: BART untuned (Row 1); XGBoost default "to limit computational burden" and misspecified logistic regression (Row 7); all arms at defaults (Row 11); CATENets defaults in CausalFM (Row 4, UNVERIFIED); Do-PFN's neural baselines (Row 3, UNVERIFIED). ACIC 2017 baselines were taken from challenge submissions (Row 5).
- Oracle-informed comparators: DoWhy given the true graph (Row 3).
- Where tuning was heavier (Row 10, 900 s per nuisance per realisation), a tuned T-learner matched or beat CausalPFN.

### 4.5 Were propensity scores from tabular foundation models checked for calibration?
**Not directly.** No study reports calibration curves, calibration slope or ICI for TFM propensity scores. Indirect evidence: Melnychuk et al. found TabPFN's propensity posteriors inaccurate "close to 0 or 1" (Row 8, p.9); TabPFN-based IPTW gave near-nominal ATE coverage in two simple binary-confounder scenarios (Row 7); Zhang et al. used TabPFN propensity scores as a covariate to reduce regularisation-induced confounding (Row 5); outcome-risk (not propensity) calibration of TFMs was poor at small n and rare events and did not transport across event rates without local recalibration (Row 16), and TabPFN gave the best outcome-model ICI in one clinical cohort (Row 14).

---

## 5. Excluded near-misses

| # | Citation | Link | Reason for exclusion |
|---|---|---|---|
| N1 | Bynum et al. 2025, *Black Box Causal Inference: Effect Estimation via Meta Prediction* (preprint) | https://arxiv.org/abs/2503.05985v1 | Amortised effect estimation, but CATE only in low-dimensional synthetic SCMs against a per-dataset MLP; IHDP evaluated for sample ATE only (p.9–10); no BART/GRF/meta-learner comparators. |
| N2 | Zhang et al. 2023, *Towards Causal Foundation Model: on Duality between Causal Inference and Attention* (CInA) | https://arxiv.org/abs/2310.00809v3 | Zero-shot ATE via covariate balancing; not CATE. |
| N3 | Nilforoshan et al. 2023, *Zero-shot causal learning* (CaML), NeurIPS 2023 | https://arxiv.org/abs/2301.12292v4 | Uses "large-scale medical claims" (p.1) but meta-trains within one database to predict effects of novel interventions; not an in-context model applied to a new dataset. |
| N4 | Kirpichenko, Konstantinov, Utkin 2025, *FoCAT: Foundation Model for Estimating the Conditional Average Treatment Effect*, Doklady Mathematics 112(1):279–287 | https://doi.org/10.1134/S1064562425700280 | In scope by title, but full text not reachable (Springer blocked); Crossref abstract gives no datasets, comparators or numbers. Should be checked by hand. |
| N5 | Zhu et al. 2026, *A Causal Foundation Model for Structure and Outcome Prediction* (TabPFN-CFM), ICML 2026 workshop | https://arxiv.org/abs/2606.26467v1 | Evaluates interventional/counterfactual outcome MSE on synthetic SEMs and two graph-known datasets; no CATE benchmark. |
| N6 | Zhang Z. 2026, *Learning to Fluctuate: Statistical Foundations for Causal Tabular Pretraining* | https://arxiv.org/abs/2609.26290v2 | ATE only (fluctuation-supervised pretraining); single-author theory with S-learner comparators. |
| N7 | Shi, Liu, Guo 2026, *TabCUQ* | https://arxiv.org/abs/2610.39558v1 | Uncertainty quantification for TFM conditional means/group ATEs; not a CATE accuracy comparison. |
| N8 | Melnychuk, Javurek, Feuerriegel 2026, *Debiased PFNs for Amortized Bayesian Semi-Parametric Inference* | https://arxiv.org/abs/2610.28314v1 | Theory for finite-dimensional targets (ATE); no CATE benchmark. |
| N9 | Javurek et al. 2026, *Amortizing Causal Sensitivity Analysis via PFNs* | https://arxiv.org/abs/2605.10590v1 | Sensitivity bounds under unobserved confounding; not CATE point estimation. |
| N10 | Muller et al. 2026, *ProximalFM* | https://arxiv.org/abs/2610.08078v2 | Proximal identification under hidden confounding; outside back-door scope. |
| N11 | Chen et al. 2026, *TabCF* | https://arxiv.org/abs/2605.05993v1 | Control-function/IV distributional effects. |
| N12 | Bellot, Dhir 2026, *Foundation Models for Partial Causal Identification* | https://arxiv.org/abs/2608.20841v1 | Bounds, discrete observables. |
| N13 | Gao et al. 2026, *CIDER-FM* | https://arxiv.org/abs/2609.39523v1 | Combines observational and surrogate-experimental data; interventional distributions. |
| N14 | Stith et al. 2026, *Causal Foundation Models with Continuous Treatments* | https://arxiv.org/abs/2605.15133v2 | Continuous treatments. |
| N15 | Zare et al. 2026, *CausalLongPFN* | https://arxiv.org/abs/2606.05797v2 | Longitudinal counterfactual prediction; not static CATE. |
| N16 | Chen et al. 2026, *PICLE-PFN* | https://arxiv.org/abs/2610.32863v1 | Longitudinal dynamic policies. |
| N17 | Sauter et al. 2025, *ACTIVA* | https://arxiv.org/abs/2503.01290v4 | Interventional distributions in synthetic and gene-expression simulations; no CATE benchmark. |
| N18 | Zhou 2026, *When and Why LLM Causal Priors Help* | https://arxiv.org/abs/2609.06941v1 | Prior selection for Do-PFN; relevant to Brief 4, not to CATE accuracy against comparators. |
| N19 | Böhm et al. 2026, *SurvPFN* (ICML 2026 workshop) | https://arxiv.org/abs/2606.04564v2 | Survival prediction, no treatment effects. |
| N20 | Seletkov et al. 2026, *Survival In-Context* | https://arxiv.org/abs/2603.29475v2 | Survival prediction, no treatment effects. |
| N21 | Lyu et al. 2026, *SurvFM* | https://arxiv.org/abs/2607.09577v2 | RMST prediction with TFMs, no treatment effects. |
| N22 | Vargas Vieyra 2026, *Staying Alive: Uncensored Survival Analysis with TFMs* | https://arxiv.org/abs/2606.03689v1 | Survival regression, no treatment effects. |
| N23 | Pham et al. 2026, *TFMs for Clinical Survival Analysis via Survival-Aware Adaptation* | https://arxiv.org/abs/2606.12006v1 | MIMIC-IV/eICU survival prediction; no treatment effects. Also Kim et al. 2026, *Tabular Foundation Models Can Do Survival Analysis*, https://arxiv.org/abs/2601.22259v2 (title/abstract screened only). |
| N24 | Utkin, Kogan, Konstantinov 2026, *Surv-IPTB* | https://arxiv.org/abs/2608.06288v1 | Attention model trained per dataset (not pre-trained); synthetic survival data only. |
| N25 | Panagopoulos 2026, *Real vs. Semi-Simulated: Rethinking Evaluation for Treatment Effect Estimation* | https://arxiv.org/abs/2605.10430v2 | Benchmark of meta-learners and causal ML; no TFM or causal PFN (zero mentions of TabPFN/CausalPFN in full text). |
| N26 | Cerqua 2026, *Looking Forward to Constructing Better Causal Comparisons* | https://arxiv.org/abs/2611.02061v1 | TFMs used for prognostic-score matching/weighting (ATT-type designs); not S/T/X/DR/R-learners, DML or TMLE; no CATE. |
| N27 | Liu, Zhu, Wang 2026, *Conformal Selection Framework for Individual Treatment Beneficiaries* | https://arxiv.org/abs/2606.31954v1 | Mentions TabPFN/TabICL as possible base learners (p.4) but evaluates linear regression, random forests, Super Learner, BART and BMA only (p.23). |
| N28 | Brockschmidt et al. 2026, *ConfoundingSHAP* | https://arxiv.org/abs/2605.10533v1 | TabPFN used to attribute confounding strength, not to estimate CATE. |
| N29 | Du et al. 2025, *Double Machine Learning for Causal Inference in High-Dimensional EHR* (medRxiv) | https://doi.org/10.1101/2025.07.21.25331944 | EHR plasmode DML study, but Crossref abstract mentions no TFM; full text not reachable (medRxiv blocked). |
| N30 | Ye et al. 2026, *Can Tabular Foundation Models Amortize Statistical Inference?* (TabCon); Hülskamp et al. 2026, *How Well Do PFNs Amortize Bayesian Inference?* | https://arxiv.org/abs/2609.33114v1 ; https://arxiv.org/abs/2610.13764v2 | Confidence intervals / amortisation error for generic targets; no CATE evaluation (abstract screened). |

Also screened and excluded at title/abstract level (not causal-effect papers or not pre-trained): DoubleML documentation page *Causal Machine Learning with TabPFN* (could not be opened; documentation, not a study); Swelam et al. 2025 *Does TabPFN Understand Causal Structures?* (causal discovery); MOCA (Wang & Ghosh 2026, per-dataset transformer); Li & Simchi-Levi 2026 (adaptive experiments).
