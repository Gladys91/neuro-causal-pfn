# Brief 4: A training prior for a causal PFN built from scratch

**Date:** 3 November 2026
**Question:** What should the training prior contain so that a prior-fitted network (PFN) trained from scratch estimates conditional average treatment effects (CATE) well in the two applications, and how should that prior be kept separate from the mechanisms used to evaluate it?
**Applications served:** (A) semi-synthetic virtual trials using brain-lesion representations, randomised and confounded allocation, binary outcomes, 300 to 3,000 patients per trial; (B) Clinical Practice Research Datalink (CPRD) Aurum electronic health records (EHR), 56,337 people starting sodium-glucose co-transporter 2 (SGLT2) or dipeptidyl peptidase-4 (DPP-4) inhibitors, about 40 expert covariates plus up to 500 code indicators, glycated haemoglobin (HbA1c) at one year, later time-to-event outcomes.
**Scope:** how published priors were built (TabPFN v1, v2, 2.5, 3, 3.5; TabICL and TabICLv2; CausalPFN; Do-PFN; CausalFM; later causal PFNs); real-data-anchored (plasmode-style) and domain-informed priors; ablations of prior components; theory and evidence on prior–target mismatch; fine-tuning versus training from scratch; out-of-prior generalisation; survival PFNs.

**Abbreviations used throughout.** ACIC: Atlantic Causal Inference Conference (data challenge). AIPTW / A-IPTW: augmented inverse probability of treatment weighting. ANM: additive noise model. ATE: average treatment effect. AUC: area under the receiver operating characteristic curve. BNN: Bayesian neural network. CATE: conditional average treatment effect. C-DAG: cluster directed acyclic graph. CEPO: conditional expected potential outcome, E[Y(t) | X = x]. CEPO-PPD: posterior predictive distribution of the CEPO. CFM: causal foundation model. CI: confidence (or credible) interval. CID: conditional interventional distribution. CPRD: Clinical Practice Research Datalink. DAG: directed acyclic graph. DGP: data-generating process. DR-learner: doubly robust learner. EHR: electronic health records. Elo: Elo rating (pairwise-comparison score). GP: Gaussian process. HbA1c: glycated haemoglobin. HDLSS: high-dimensional low-sample-size. IBS: integrated Brier score. IHDP: Infant Health and Development Program (semi-synthetic benchmark). IV: instrumental variable. KL: Kullback–Leibler divergence. MAR / MNAR / MCAR: missing at random / not at random / completely at random. MCMC: Markov chain Monte Carlo. MLP: multilayer perceptron. NLL: negative log-likelihood. OOD: out of distribution. OpenML-CC18: OpenML Curated Classification benchmark 2018. OSPC: one-step posterior correction. PEHE: precision in estimating heterogeneous effects (root mean squared CATE error unless stated). PFN: prior-data fitted network (prior-fitted network). PICB: prior-induced confounding bias. PO: proportional odds. PPD: posterior predictive distribution. RCT: randomised controlled trial. SCM: structural causal model. SGLT2 / DPP-4: sodium-glucose co-transporter 2 / dipeptidyl peptidase-4. TFM: tabular foundation model. T-, S-, X-learner: two-model, single-model and cross meta-learners.

### Assumptions (how ambiguities in the brief were resolved)
1. **Inclusion rule.** A paper is in the evidence table if it (a) specifies a PFN training prior in enough detail to extract at least two of the brief's fields (components, mixture weights, n/p sampling, outcome types, identification, scale), or (b) reports an ablation or a mismatch/out-of-prior test of a PFN prior, or (c) gives theory on PFN posterior consistency or misspecification, or (d) builds a prior or a continued-pretraining corpus from real data. Prediction-only TFM papers are included only under (a)–(d). Pure benchmark papers on causal PFNs are included only when they test mechanisms outside the training priors (rows 30–31).
2. **Brief 1 overlap.** Rows 1–3, 5–10, 17, 18, 29–31 use papers also in Brief 1. Their texts were re-read for the Brief 4 fields; no Brief 1 cell was copied. The texts are copied into `brief4/texts/`.
3. **Held out of the prior** is judged at three levels: covariates/data (were evaluation tables excluded from the prior's base tables?), mechanisms (are the evaluation's functional families different from the prior's?), and selection (were prior hyperparameters or checkpoints chosen on the evaluation sets?). Where a paper is silent, the cell says *not stated* and gives my reading separately, marked **(my reading)**.
4. **Mixture weights** are reported only when stated numerically. "Not stated" means not found in the main text and appendices read.
5. **Figures only.** Results shown only in figures are not transcribed as numbers.
6. **Compute** is mentioned only where a scale choice limits the scientific conclusion (O'Prior, SurvICL ablations, TabPFN v1 sample cap).

### Access limitations
- Semantic Scholar returned HTTP 429 repeatedly. Forward citations were obtained for CausalPFN (64), Do-PFN (69, after 6 tries), CausalFM (47) and Melnychuk et al. 2026 (8). Mourão et al. 2026 forward citations were never returned (7 tries). Google Scholar cannot be queried automatically. OpenReview API, github.com and Wiley are blocked.
- The TabPFN v2 Nature paper was read from the PubMed Central XML (no page numbers; cited by section heading).
- The CausalPFN prior's OpenML catalogue (a GitHub CSV) and all code repositories were not opened (github.com blocked), so code-level prior details (for example how binary outcomes or mixture probabilities are set in code) are **UNVERIFIED** where noted.
- *CausalEcon* (a causal foundation model reportedly pre-trained on economic panel data, listed in Semantic Scholar forward citations without an arXiv ID) could not be located by web search; not assessed.

---

## 1. Search log

All searches run 3 November 2026, date window 2019 to November 2026. "Screened" = titles/abstracts read; "Included" = rows in §2 counted at first route. Hit counts are as returned by each source.

| # | Source | Query / step | Hits | Screened | Included |
|---|---|---|---|---|---|
| S0 | Brief-named seeds | CausalPFN; Do-PFN; CausalFM; TabPFN v1, v2 (Nature), 2.5, 3, 3.5; TabICL; TabICLv2 | 10 | 10 | 10 (rows 1–10) |
| B1 | Reuse of Brief 1 texts | Full texts saved in this session for Brief 1 (`brief1/texts/`), re-read for Brief 4 fields | 16 rows + 30 near-misses | 46 | counted under the search route below that also returned them |
| A1 | arXiv API | `(all:"prior-fitted" OR all:"prior-data fitted") AND (all:"treatment effect" OR all:causal)` | 36 | 36 | 4 (Melnychuk 2026a; Mourão; Melnychuk 2026b debiased; Zhou) |
| A2 | arXiv API | `(all:"prior-fitted" OR all:"prior-data fitted" OR all:PFN) AND (all:misspecification OR all:"prior mismatch" OR all:"out-of-distribution")` | 4 | 4 | 1 (separability gap) |
| A3 | arXiv API | `(all:"prior-fitted" OR all:"prior-data fitted" OR all:"tabular foundation model") AND (all:"synthetic prior" OR all:"prior mixture" OR all:"mixture of priors")` | 21 | 21 | 5 (Mitra; O'Prior; Mind the Gap; Structural coverage; Hülskamp) |
| A4 | arXiv API | `(… PFN or TFM …) AND (all:"fine-tuning" OR all:finetuning) AND (all:causal OR all:"treatment effect")` | 8 | 8 | 1 (CausalMixFT) |
| A5 | arXiv API | `(all:plasmode OR all:"semi-synthetic") AND (all:"in-context" OR all:"foundation model" OR all:"prior-fitted") AND all:causal` | 21 | 21 | 0 |
| A6 | arXiv API | `(… PFN or TFM …) AND (all:survival OR all:"time-to-event" OR all:censoring)` | 17 | 17 | 4 (SIC; SurvivalPFN; SurvICL; SurvPFN) |
| A7 | arXiv API | `(… "prior-fitted" OR "in-context" …) AND (all:"domain-informed" OR all:"domain-specific prior" OR all:"domain knowledge") AND all:prior` | 85 | 85 (titles) | 0 |
| A8 | arXiv API | `(… PFN or "causal foundation model" …) AND (all:clinical OR all:medical OR all:"electronic health")` | 13 | 13 | 0 new |
| A9 | arXiv API | `(… causal PFN …) AND (all:survival OR all:"time-to-event") AND (all:"treatment effect" OR all:counterfactual)` | 0 | 0 | 0 |
| A10 | arXiv API | `(all:CausalPFN OR all:"Do-PFN" OR all:CausalFM) AND (all:"fine-tuning" OR all:finetune OR all:"continued pre-training" OR all:"post-training")` | 1 | 1 | 0 new |
| A11 | arXiv API | `(… causal PFN …) AND (all:"out-of-distribution" OR all:"distribution shift" OR all:generalization) AND all:"treatment effect"` | 4 | 4 | 0 new |
| A12 | arXiv API | `(all:"causal foundation model" OR all:"prior-data fitted") AND (all:"effect heterogeneity" OR all:overlap OR all:positivity OR all:"confounding strength")` | 11 | 11 | 1 (TabPFN-Wide) |
| A13 | arXiv API | `(all:amortized OR all:"in-context") AND all:"treatment effect" AND (all:"real-world covariates" OR all:"real covariates" OR all:"semi-synthetic prior")` | 0 | 0 | 0 |
| S2-1 | Semantic Scholar | Forward citations of CausalPFN (arXiv:2506.07918) | 64 | 64 | (union of S2-1 to S2-4: 98 unique titles screened) |
| S2-2 | Semantic Scholar | Forward citations of Do-PFN (arXiv:2506.06039) | 69 | 69 | – |
| S2-3 | Semantic Scholar | Forward citations of CausalFM (arXiv:2506.10914) | 47 | 47 | – |
| S2-4 | Semantic Scholar | Forward citations of Melnychuk et al. 2026 (arXiv:2603.12037) | 8 | 8 | 3 new from S2-1–4 (Jung CausalIDView; Stith CFM tutorial; Reuter partial graphs) |
| S2-5 | Semantic Scholar | Forward citations of Mourão et al. 2026 (arXiv:2603.15928) | blocked (HTTP 429, 7 tries) | – | – |
| BW | Backward chasing (reference lists of included texts) + arXiv ID lookup | Müller 2022 (cited by all PFN papers); Nagler 2023 (cited by Do-PFN, CausalFM); Müller 2025 position (cited by SurvivalPFN, Hülskamp); RealCause (cited by CausalPFN, Do-PFN); Real-TabPFN (cited by TabPFN-2.5); Rubachev 2025 (cited by Mitra, O'Prior, CausalMixFT, SurvICL) | 6 | 6 | 6 (rows 15, 16, 21, 22, 23, 24) |
| ID2 | arXiv API id_list | Abstract screening of 25 candidates from A1–A12 and S2 (e.g. PerturbPFN, CAFE, Computational Identifiability, IV-ICL, KnowsTFM, InCOPE) | 25 | 25 | counted above; rest → near-misses |
| P1 | PubMed (2019–2026) | `("prior-data fitted network" OR "prior-fitted network" OR TabPFN) AND (prior OR synthetic) AND (causal OR "treatment effect")` | 8 | 8 | 0 (prediction-only clinical applications; Kurmann et al. is Brief 1 row 15) |
| P2 | PubMed | `("prior-data fitted" OR "prior-fitted" OR "tabular foundation model") AND (survival OR "time-to-event")` | 13 | 13 | 0 (prediction-only) |
| P3 | PubMed | `plasmode AND (transformer OR "foundation model" OR "in-context")` | 0 | 0 | 0 |
| W1 | Web search | `CausalEcon foundation model pre-trained on global economic panel data zero-shot causal effect estimation` | 10 | 10 | 0 (not found) |
| W2 | Web search | `prior-fitted network treatment effect prior built from real covariates semi-synthetic plasmode pretraining causal` | 10 | 10 | 0 new |
| W3 | Web search | `causal foundation model survival time-to-event treatment effect prior-fitted network counterfactual survival 2026` | 10 | 10 | 0 new (confirms no causal survival PFN) |
| V | Venue checks | Headers of PDFs read (NeurIPS 2025, ICLR 2022/2023/2026, ICML 2023/2025/2026, workshops) and arXiv comment/journal-ref fields | – | – | – |

Totals: **35 included papers** (§2), **28 near-misses** (§5). Not searched directly: Google Scholar (no automated access); OpenReview (API blocked; covered indirectly by arXiv); AISTATS, CLeaR and UAI proceedings (no in-scope hit surfaced by arXiv or web search; one UAI 2026 paper, Tugnoli et al., is a near-miss).

---

## 2. Evidence table

Fields (as in the brief): **Paper** (link, version read, status); **Prior components**; **Mixture weights**; **How n and p are sampled**; **Outcome types**; **Identifying assumptions**; **Training scale**; **Ablation results**; **Evaluation benchmarks**; **Evaluation mechanisms held out of the prior?** Each card keeps every field. Rows 1–3 are the core causal PFNs; rows 4–14 are predictive TFM priors; rows 15–21 theory; rows 22–28 real-data-anchored, domain-informed and fine-tuning work; rows 29–31 out-of-prior evaluation of causal PFNs; rows 32–35 survival PFNs.

### A. Causal PFNs

#### Row 1. Balazadeh et al. 2025, *CausalPFN: Amortized Causal Effect Estimation via In-Context Learning*
- **Paper:** https://arxiv.org/abs/2506.07918v2 (arXiv v2 read). Peer reviewed: NeurIPS 2025 (p.1: "39th Conference on Neural Information Processing Systems (NeurIPS 2025)").
- **Prior components:** Base table drawn from real OpenML tables or synthesised (p.31: "We draw the base tables from two sources: (i) real-world tables from OpenML, and (ii) fully synthetic data."); 337 OpenML tables (p.6: "We use 337 OpenML tables [12], checked to avoid leakage"); synthetic tables from the TabPFN v1 random networks (p.31: "we generate synthetic tables using the random neural networks used to train TabPFN v1"). Two table columns become the CEPOs; heterogeneity is shrunk by a parameter γ (p.32: "γ = 0 yields a dataset with a zero variance CATE (fully homogeneous), whereas γ = 1 recovers the original heterogeneity"). Heteroscedastic noise from two further table columns (p.32: "The input-dependent scale factors ηt (x) allow for heteroscedastic noises"). Treatment logits from one of three mechanisms (p.32: "Randomized treatments (RCT). Treatments are independent of covariates"; "Linear logits."; "Non-linear logits. Feed x into a randomly initialized MLP"). Positivity degraded on purpose (p.32: "exacerbate extreme propensity scores to mimic poor positivity").
- **Mixture weights:** γ uniform on [0, 1] (p.32: "a heterogeneity hyperparameter γ, which we sample uniformly from"); positivity parameter ξ ∈ [0, 1] (sampling law not stated); the three propensity mechanisms are chosen "randomly" (probabilities not stated); proportion of OpenML versus synthetic base tables not stated.
- **n and p:** p.34: "During the causal phase of training, we consider sample sizes up to 2,048 and covariates up to 100." Covariates zero-padded to 100 (p.33: "padded to length F = 100"). Distribution within these ranges not stated.
- **Outcome types:** Continuous CEPO columns plus zero-mean noise (p.32: "we sample ϵt from a Gaussian"). No binary-outcome generator is described in the sections read (code not opened: **UNVERIFIED** whether binary base-table columns can be selected as CEPOs). Binary outcomes appear only in evaluation (p.8: "The outcome is whether a website visit occurred within two weeks (binary).").
- **Identifying assumptions:** Strong ignorability and positivity by construction (p.6: "This approach guarantees strong ignorability by design"). Consistency theorem: posterior-mean CEPO converges for almost all prior draws (p.4: "if and only if the prior π is CEPO-identifiable"). Design rule (p.4: "(i) π must rule out non-identifiable cases, and, once identifiability is secured, (ii) broadening π increases the chance").
- **Training scale:** p.33: "The full model has approximately 20M parameters and is trained in two stages": a predictive phase (context up to 16K) then a causal phase (context 2,048). Number of prior datasets: not found in the sections read (**UNVERIFIED**).
- **Ablation results:** (i) Sample size, Table 4 (10 covariates, polynomial DGPs): PEHE 1.34 at 10 rows, 0.46 at 500, 0.29 at 5,000, 0.31 at 10,000 (p.34: "with a slight plateau at very large contexts"). (ii) Covariate count, Table 5 (1,000 rows): PEHE 0.40 at 10, 1.01 at 100, 1.32 at 1,000, equal to the DA-learner's 1.32 (p.34: "likely due to training exposure being limited to up to 100 dimensions"). (iii) Out-of-family calibration: trained on one polynomial degree or sinusoid frequency band and tested on others (p.36: "We train on one degree family and test on the others to probe generalization."); result (p.9: "becomes severely overconfident when evaluated on OOD DGPs"); temperature scaling fitted on observed outcomes removes the overconfidence (figure only). (iv) Causal prior versus predictive prior: TabPFN v2 fine-tuned on the CausalPFN prior for 48 hours improved PEHE on IHDP (0.95 to 0.90), ACIC 2016 (0.54 to 0.47), Lalonde CPS (9.45 to 8.97 ×10³) and PSID (18.7 to 14.90 ×10³) (Table 3, p.10). Note: the fine-tuned TabPFN beat CausalPFN on ACIC 2016 (0.47 vs 0.92). No ablation of γ, ξ, the OpenML/synthetic split or the propensity mechanisms is reported. Authors' limitation (p.10: "Investigating robustness to prior misspecification and developing finite-sample guarantees remain open problems.").
- **Evaluation benchmarks:** IHDP (100 realisations), ACIC 2016 (10), Lalonde CPS and PSID with effects from RealCause (p.7: "with their causal effects provided by RealCause (each with 100 realizations)"); marketing uplift trials (Hillstrom, Criteo, X5, Lenta, Megafon); synthetic polynomial and sinusoidal families.
- **Held out?** Covariates: yes, by stated exclusion (p.31: "none of the tables that share covariates or outcomes with our test sets (Lalonde, IHDP, ACIC, Criteo, Megafon, Hillstrom, Lenta, X5) are included in training"). Mechanisms: the propensity post-processing is "inspired by RealCause" (p.32: "inspired by RealCause [82], to better control the positivity level") while two benchmarks use RealCause effects, so mechanism ideas are partly shared **(my reading)**. Synthetic families: explicit train-one-family/test-another design (p.36). Selection: not stated how prior settings or checkpoints were chosen.

#### Row 2. Robertson et al. 2025, *Do-PFN: In-Context Learning for Causal Effect Estimation*
- **Paper:** https://arxiv.org/abs/2506.06039v3 (arXiv v3 read). Peer reviewed: NeurIPS 2025 (p.1: "39th Conference on Neural Information Processing Systems (NeurIPS 2025)").
- **Prior components:** Random DAG over K nodes; additive-noise mechanisms (p.18: "to take the form of an additive noise model (ANM)") with one of three nonlinearities per node, quadratic, ReLU or tanh (p.18); Kaiming-uniform weights (p.18: "The weights of the SCM are sampled using a Kaiming initialization"); interventional samples reuse each unit's noise (p.19: "this process can also be seen as simulating counterfactuals or single potential outcomes."). The prior is not restricted to identifiable graphs (see identifying assumptions).
- **Mixture weights:** Nonlinearity chosen uniformly (p.19: "The nonlinearities fa are sampled uniformly at random"); graph-size and edge distributions beyond the maximum not stated.
- **n and p:** p.18: "the number of data points is drawn uniformly between Mmin = 10 and Mmax = 2, 200." Covariate count is set by graph size: v1 up to 50 nodes and v1.1 up to 60 (p.9: "which was trained on graph sizes up to 60 nodes").
- **Outcome types:** Continuous outcome; binary treatment (p.3: "performing an intervention do(t) for a binary variable T"). How T is binarised in the prior: not described in the sections read (**UNVERIFIED**).
- **Identifying assumptions:** None imposed (p.5: "since our prior over SCMs does not necessarily imply identifiability of causal effects"). Stated limit: concentration only up to an equivalence class (p.6: "the posterior conditional interventional distribution concentrates up to the Markov-equivalence class").
- **Training scale:** p.6: "Do-PFN has 7.3 million parameters"; v1 and v1.1 trained 48 and 96 hours on one GPU. Number of prior datasets not stated in sections read.
- **Ablation results:** (i) Effect size: p.24: "This result is likely explained by the high probability of low-ATE datasets in our prior", i.e., error rises for the largest-ATE datasets. (ii) Dataset size 5–2,000: CATE error falls with n (figure only). (iii) Noise: robust to Laplace, t, Gumbel and mixtures, but (p.9: "using a two-times larger variance of the Gaussian noise drastically hurts performance"). (iv) Mechanisms: (p.9: "testing on the pointwise average of the functions used during training does lead to a notable decrease in performance"). (v) Graph size (p.9: "For larger graphs out of its prior-distribution, we observe a significant reduction in Do-PFN-v1's performance"), recovered by v1.1 trained on larger graphs. (vi) Uncertainty: slightly under-confident when effects are identifiable (p.9: "slightly under-confident for theoretically identifiable case studies"). Independent head-to-head in CausalPFN's paper: Do-PFN PEHE 6.07 vs CausalPFN 0.58 on IHDP (CausalPFN Table 8, p.40).
- **Evaluation benchmarks:** Six synthetic case studies (confounder, mediator, front-door, back-door, unobserved confounder) plus three ablation case studies; RealCause (four datasets); Amazon Sales and Law School with DoWhy-fitted mechanisms.
- **Held out?** Synthetic case studies: no, they reuse the prior's parameter distributions (p.6: "varying the SCM parameters as described in Appendix C."). Semi-synthetic: RealCause and DoWhy-fitted mechanisms are fitted to real data, a different family from the prior **(my reading)**; authors note RealCause (p.10: "simulated to perfectly satisfy the unconfoundedness assumption, which inherently advantages the baselines over Do-PFN"). Explicit OOD tests for noise, nonlinearity and graph size (above).

#### Row 3. Ma, Frauen, Javurek, Feuerriegel 2026, *Foundation Models for Causal Inference via Prior-Data Fitted Networks* (CausalFM)
- **Paper:** https://arxiv.org/abs/2506.10914v3 (arXiv v3 read). Peer reviewed: ICLR 2026 per the PDF header (p.1: "Published as a conference paper at ICLR 2026"); iclr.cc not opened.
- **Prior components:** One prior per identification setting, built on a cluster DAG (C-DAG). Clusters with latent nodes get a TabPFN-style network (p.7: "we assign a clustered Bayesian neural network (BNN) prior to Ci"); treatment and outcome get an observational BNN. Back-door constraint (p.7: "ensuring that all SCMs satisfy the positivity assumption"); front-door (p.7: "ensuring positivity for both treatments and mediators"); IV with an instrument unconnected to the confounder (p.7: "an unobserved confounder U that is a joint parent of A and Y has no edge to the instrument Z") and an additively separable outcome in U (p.7). Covariates: tanh MLP-DAG with random noise families, then discretisation (p.24: "apply randomized thresholds to discretize or binarize a subset, yielding mixed-type covariates"). Treatment: inconsistently described as thresholded (p.24: "compute a scalar propensity score, then threshold to assign a binary treatment") and as Bernoulli(sigmoid) (App. E.2, p.26).
- **Mixture weights:** Architecture hyperparameters uniform over small ranges (App. E.5, p.27); noise type per node (p.27: "draw a type in {Normal, Uniform, Laplace, Logistic}"). No mixture across identification settings: separate models per setting (Table 9 compares models trained under different designs).
- **n and p:** p.27: "We sample 10000 synthetic training datasets from data prior with different data generation mechanism. Each training datasets contain 1024 data samples."; features (p.27: "ranging from 10 to 100").
- **Outcome types:** Continuous only (p.26: "sampling covariates X, treatment A, and continuous outcomes Y").
- **Identifying assumptions:** Back-door, front-door or IV, each enforced in its prior. Theorem 4.3: a well-specified prior must put zero mass on identifiability-violating SCMs (p.17: "places nonzero mass on SCMs that violate the identifiability conditions of the chosen setting, then the resulting posterior predictive interventional distribution is necessarily misspecified").
- **Training scale:** 10,000 datasets of 1,024 rows (above); p.9: "batch size 16, and sequence length 1024 for up to 150 epochs". This is far smaller than CausalPFN or TabPFN corpora.
- **Ablation results:** (i) Wrong identification design: IV data PEHE 0.422 (IV prior) vs 0.489 (back-door prior); front-door data 0.847 vs 0.876 (Table 9 is on p.34. Quotation, p.33: "This highlights the importance of including the correct identifiability assumption into the prior specification"). (ii) Unobserved-confounding strength α ∈ [0, 1] varied (p.33: "we vary the strength of unobserved confounding in the data-generating process"); described as robust (figure only). Results: synthetic PEHE 0.515 vs CausalPFN 0.557, Do-PFN 0.586, X-learner 0.563 (Table 2, p.9). Negative: on ACIC 2016, CausalFM 0.638 vs CausalPFN 0.239 and X-learner 0.519 (Table 6, p.32).
- **Evaluation benchmarks:** Ten synthetic back-door datasets, semi-synthetic Jobs, ACIC 2016, ten binary-IV and ten continuous-IV datasets, front-door datasets.
- **Held out?** Not stated. The synthetic test sets use the prior's generator (p.9: "We benchmark our model on ten synthetic datasets generated under diverse mechanisms, with implementation details in Appendix D."), so synthetic results are in-family **(my reading)**. Jobs and ACIC 2016 outcome generators are external to the prior.

### B. Predictive tabular PFN priors (structure inherited by causal PFNs)

#### Row 4. Hollmann et al. 2023, *TabPFN: A Transformer That Solves Small Tabular Classification Problems in a Second* (TabPFN v1)
- **Paper:** https://arxiv.org/abs/2207.01848v6 (arXiv v6 read). Peer reviewed: ICLR 2023 (p.1: "Published as a conference paper at ICLR 2023").
- **Prior components:** SCM prior (random DAG, random functions, sampled feature and target nodes) and a BNN prior; hyperparameters are themselves sampled (p.4: "we use distributions instead of point-estimates for almost all of our prior's hyperparameters"); simplicity bias (p.4: "We base our priors on a notion of simplicity").
- **Mixture weights:** SCM and BNN with equal probability (p.5: "from either one or the other prior with equal probability").
- **n and p:** Up to 1,024 rows (p.9: "we limited synthetic data to a maximum size of 1 024"); uniform over 1–1,023 per Nagler (row 16, p.4); up to 100 features (p.16: "we limit the number of features to 100").
- **Outcome types:** Classification; regression outputs converted to classes (p.4: "Since our SCM and BNN priors only yield regression tasks, we show how to convert them to classification tasks").
- **Identifying assumptions:** Not applicable (predictive).
- **Training scale:** p.3: "we trained a 12-layer Transformer for 18 000 batches of 512 synthetically generated datasets each".
- **Ablation results:** Table 4 (p.20): ROC AUC 0.865 (BNN), 0.881 (SCM), 0.883 (SCM+BNN); (p.20: "mixing BNN and SCM prior does not seem to make a big difference on our test set compared to a pure SCM prior."). Missing component, a failure: (p.16: "we did not consider the existence of many uninformative features in our prior, leading to performance degradation when such features are added"). Size extrapolation (p.9: "our models generalize beyond sample sizes seen during training").
- **Evaluation benchmarks:** 30 OpenML-CC18 datasets (18 numerical), 149 validation datasets, OpenML AutoML Benchmark.
- **Held out?** Prior development focused on the numerical datasets (p.7: "which we focussed the development of our TabPFN prior on"); a separate list of "150 meta-validation datasets" exists (p.17), but the AutoML benchmark overlaps the test sets (p.17: "these datasets are not disjoint from our evaluation datasets").

#### Row 5. Hollmann et al. 2025, *Accurate predictions on small data with a tabular foundation model* (TabPFN v2), Nature 637:319–326
- **Paper:** https://doi.org/10.1038/s41586-024-08328-6; version of record read via PubMed Central PMC11711098 (XML; cited by section). Peer reviewed.
- **Prior components:** Section *Synthetic data based on causal models*: sampled high-level hyperparameters, DAG, edge mappings including neural networks, categorical discretisation and trees ("discretization mechanisms for generating categorical features and decision tree structures to encode local, rule-based dependencies"); edge noise ("At each edge, we add Gaussian noise"); post-processing with Kumaraswamy warping, quantisation and MCAR missingness (section *Post-processing*: "according to the missing completely at random strategy"). Graph size (section *Graph structure sampling*: "N is sampled from a log-uniform distribution"). Targets (section *Target generation*: "To generate target labels for regression tasks, we select a randomly chosen continuous feature without post-processing.").
- **Mixture weights:** Not stated. Prior hyperparameters were tuned (section *Training details*: "We chose the hyperparameters for the prior based on random searches").
- **n and p:** Section *Training details*: "We sample the number of training samples for each dataset uniformly up to 2,048"; "We sample the number of features using a beta distribution (k = 0.95, b = 8.0) that we linearly scale to the range 1–160."
- **Outcome types:** Regression and classification (up to 10 classes).
- **Identifying assumptions:** Not applicable.
- **Training scale:** Section *Training details*: "trained on around 130,000,000 synthetically generated datasets each".
- **Ablation results:** No ablation of prior components found in the sections read.
- **Evaluation benchmarks:** AutoML Benchmark (29 classification) and OpenML-CTR23 (28 regression) datasets up to 10,000 rows.
- **Held out?** Selection data were separated: section *Development datasets*: "To decide on the hyperparameters of TabPFN, as well as our hyperparameter search spaces, we considered another set of datasets, our development datasets." The prior is synthetic, so no covariate reuse.

#### Row 6. Grinsztajn et al. 2025, *TabPFN-2.5* technical report
- **Paper:** https://arxiv.org/abs/2511.08667v2 (arXiv v2). Preprint (technical report).
- **Prior components:** Described only qualitatively (p.4: "We improved our prior data generation substantially, broadened the set of distributions and scaled up to more data points and more features"). A real-data variant fine-tuned on 43 OpenML/Kaggle datasets (p.4).
- **Mixture weights; n and p:** Not stated.
- **Outcome types:** Regression and classification.
- **Identifying assumptions:** Not applicable (used as a meta-learner nuisance model on RealCause).
- **Training scale:** Not stated in sections read. About 100 models trained to tune ~50 architecture, training and prior hyperparameters (p.5).
- **Ablation results:** None for prior components.
- **Evaluation benchmarks:** TabArena and internal suites; RealCause for causal use.
- **Held out?** Prior tuned on internal data (p.5: "evaluated them on a curated in-house validation suite"). Real-data fine-tuning was deduplicated (p.28: "to ensure that no training dataset overlaps with, or is derived from, any evaluation dataset").

#### Row 7. Prior Labs 2026, *TabPFN-3* technical report
- **Paper:** https://arxiv.org/abs/2605.13986v2 (arXiv v2). Preprint (technical report).
- **Prior components:** SCM prior with new graph samplers, combiner mechanisms, reworked categorical variables, high-frequency oscillators, spatial, many-class, temporal (dynamic SCM) and OOD components (p.12: "Out-of-distribution prior. We add out-of-distribution prediction tasks").
- **Mixture weights; n and p:** Not stated.
- **Outcome types:** Regression and classification.
- **Identifying assumptions:** Not applicable.
- **Training scale:** p.10: "our final TabPFN-3 model was trained on more than 8 trillion tokens."
- **Ablation results:** No component ablation; for causal meta-learning, a regression from version 2.5 (p.21: "we observe slightly worse performance compared to TabPFN-2.5 on RealCause").
- **Evaluation benchmarks:** TabArena and others; scikit-uplift and RealCause for causal use.
- **Held out?** Not stated for prior design.

#### Row 8. Prior Labs 2026, *TabPFN-3.5* technical report
- **Paper:** https://arxiv.org/abs/2609.17895v2 (arXiv v2). Preprint (technical report).
- **Prior components:** p.11: "Our synthetic data generation pipeline closely follows TabPFN-3"; adjusted toward wide and grouped tables (p.11: "we adjusted our prior to generate more realistic datasets with large feature counts and grouped data").
- **Mixture weights; n and p; training scale:** Not stated.
- **Outcome types:** Regression and classification.
- **Identifying assumptions:** Not applicable.
- **Ablation results:** Effect of prior changes shown on BeyondArena slices (figure only).
- **Evaluation benchmarks:** TabArena, BeyondArena, STRABLE and others.
- **Held out?** Not stated.

#### Row 9. Qu et al. 2025, *TabICL: A Tabular Foundation Model for In-Context Learning on Large Data*
- **Paper:** https://arxiv.org/abs/2502.05564v2 (arXiv v2). Peer reviewed: ICML 2025 (p.1: "PMLR 267, 2025").
- **Prior components:** TabPFN v1 SCMs with more activation functions plus tree-based SCMs (p.16: "The tree-based SCM prior replaces the linear and activation layers in the SCM prior by XGBoost models fitted on random data").
- **Mixture weights:** p.6: "we combine SCMs (70%) ... with tree-based SCMs (30%)".
- **n and p:** p.13: "TabICL was pretrained using curriculum learning that progressively scales the number of samples from 1,024 to 60K. The number of features was sampled uniformly up to 100".
- **Outcome types:** Classification only (p.9: "Currently, TabICL is limited to classification").
- **Identifying assumptions:** Not applicable.
- **Training scale:** 512 datasets per step; stage 1 (p.6: "NB = 4 with a fixed size of 1,024 for 160K steps"); about 83 million datasets according to TabICLv2 (row 10, p.5).
- **Ablation results:** p.9: "Tree-based SCMs prove beneficial." (relative improvement across 200 datasets, figure only, at a reduced 20K-step budget).
- **Evaluation benchmarks:** TALENT (200 classification datasets) and others.
- **Held out?** TabPFN v2's development datasets were removed from the main comparison (p.24: "For a fair comparison, we excluded these development datasets from the main paper."). TabICL's own prior-selection data are not stated.

#### Row 10. Qu et al. 2026, *TabICLv2*
- **Paper:** https://arxiv.org/abs/2602.11139v2 (arXiv v2). Peer reviewed: ICML 2026 (p.1: "PMLR 306, 2026").
- **Prior components:** New SCM prior combining TabICL and TabPFN v2 ideas, with many new sampling mechanisms (App. E); prior filtering.
- **Mixture weights:** Not stated in the main text read (App. E not transcribed).
- **n and p:** Three stages, 1,024 rows, then 400–10,240, then 400–60K (log-uniform), up to 100 features (p.5).
- **Outcome types:** Classification and regression.
- **Identifying assumptions:** Not applicable.
- **Training scale:** About 35 million datasets (p.5).
- **Ablation results:** Prior choice dominates (p.8: "The prior yields the largest effect."); with the old prior (p.5: "pretraining TabICLv2 with the TabICL prior yields substantially lower performance"); edge noise added in the TabPFN v2 style (p.21: "this modification has negligible impact on performance across all metrics.").
- **Evaluation benchmarks:** TALENT, TabArena.
- **Held out?** Designed to avoid tuning on validation data (p.5: "the new prior is developed mostly without experimental feedback, since fine-grained ablations are impractical and prone to overfitting validation datasets").

#### Row 11. Zhang et al. 2025, *Mitra: Mixed Synthetic Priors for Enhancing Tabular Foundation Models*
- **Paper:** https://arxiv.org/abs/2510.21204v1 (arXiv v1). Peer reviewed: NeurIPS 2025 (p.1 footer: "39th Conference on Neural Information Processing Systems (NeurIPS 2025)").
- **Prior components:** SCM prior plus tree-based priors: extra trees (ET), gradient boosting (GB), decision tree (DT), random forest (RF) and a random-forest variant (DSRF). Prior choice is guided by three properties (p.4: "(1) Performance, quantified by a higher value of Pi ; (2) Diversity, quantified by a lower diagonal value Gii").
- **Mixture weights:** Table 6 ablation uses (p.9: "consisting of 50% SCM and 50% TBPs with equal weighting"); final weights wi are sampled proportionally (p.5), with values not transcribed.
- **n and p:** Not found in the sections read.
- **Outcome types:** Classification and regression.
- **Identifying assumptions:** Not applicable.
- **Training scale:** Not transcribed.
- **Ablation results:** Table 6 (TabRepo, Elo): RF alone 815, SCM alone 1000, SCM+ET 1063, SCM+ET+GB 1076, full mixture 1062. p.9: "GSCM shows the highest importance"; "despite being the second-best stand-alone prior, GDSRF contributes the least when added to the mixture". Adding priors beyond three did not improve Elo.
- **Evaluation benchmarks:** TabRepo, TabZilla, AutoML Benchmark, TabArena.
- **Held out?** No for selection: the prior-importance ablation is run on TabRepo (p.9: "TabRepo 10-fold classification ablation study"), which is also a main evaluation benchmark, and the "performance vector" uses real datasets (p.4).

#### Row 12. Bouadi et al. 2026, *Shaping the Prior: How Synthetic Task Distributions Determine Tabular Foundation Model Quality* (O'Prior)
- **Paper:** https://arxiv.org/abs/2605.18971v2 (arXiv v2, 23 Oct 2026). Preprint.
- **Prior components:** Hybrid SCM meta-generator, a realism engine (heterogeneous marginals, MAR/MNAR missingness, target transforms), a stress module (p.6: "Latent confounding. To model shared unobserved causes, the generator samples a latent vector"), and a curriculum.
- **Mixture weights:** Task-level Bernoulli switches (p.6); values not transcribed.
- **n and p:** p.7: "40, 000 synthetic datasets per prior, each of size T ∈ [512, 1024] rows and d ∈ [3, 50] features".
- **Outcome types:** Classification.
- **Identifying assumptions:** Not applicable (confounding here creates spurious prediction shortcuts).
- **Training scale:** 40,000 datasets with nanoTabPFN. This small scale is a compute-driven choice, and the authors themselves attribute some negative interactions to it (p.9: "it is a budget-dependent constraint"), which limits generalisation of the ablation.
- **Ablation results:** p.10: "structural mechanism diversity is the dominant source of transfer improvement"; stronger realism beat moderate realism on all six metric–benchmark pairs; the full curriculum did not dominate static priors (p.10: "Curriculum is not a universally superior strategy").
- **Evaluation benchmarks:** TabArena v0.1 (21 datasets), OpenML-CC18 filtered (31).
- **Held out?** A leakage-safe preprocessing rule (p.2: "all fitted statistics are Fn -measurable, computed exclusively from support rows"); separation of prior selection from benchmarks is not stated.

#### Row 13. *From Synthetic Priors to Model Behavior: Structural Coverage in Tabular Foundation Models* (2026)
- **Paper:** https://arxiv.org/abs/2609.06912v1 (arXiv v1). Preprint. Authors not transcribed (abstract and first pages read).
- **Prior components / weights / n, p / outcomes / identification / scale:** Analysis paper; reconstructs the generators of four TFMs.
- **Ablation results:** Abstract: "stronger synthetic-to-benchmark support is generally associated with better relative model performance."
- **Evaluation benchmarks:** Two tabular benchmarks (names not transcribed).
- **Held out?** Not applicable; offers a coverage diagnostic (abstract: "structural coverage provides a useful diagnostic for characterizing synthetic pretraining priors").

#### Row 14. *Mind the Gap? A Distributional Comparison of Real and Synthetic Priors for Tabular Foundation Models* (2026)
- **Paper:** https://arxiv.org/abs/2605.06343v1 (arXiv v1). Preprint. Abstract and introduction read.
- **Prior components:** Compares the TabICL synthetic prior with curated (TabFM) and web-scraped (T4) real corpora.
- **Weights / n, p / outcomes / identification / scale:** Not applicable.
- **Ablation results:** Abstract: "the TabICL synthetic prior occupies a narrow region of the space of real tables, that this mismatch cannot be closed by optimising prior hyper-parameters across more than 86 thousand configurations"; yet the gap (abstract: "has a clearly detectable effect on performance under neither feature-based proximity measures"). This contradicts row 13 (see §3).
- **Evaluation benchmarks / held out:** Not applicable.

### C. Theory and evidence on prior–target mismatch

#### Row 15. Müller et al. 2022, *Transformers Can Do Bayesian Inference*
- **Paper:** https://arxiv.org/abs/2112.10510v7 (arXiv v7). Peer reviewed: ICLR 2022 (arXiv comment "Published at ICLR 2022").
- **Fields:** Foundational result: the prior-data loss is the expected cross-entropy to the PPD (p.4: "The proposed objective ℓθ is equal to the expectation of the cross-entropy between the PPD and its approximation qθ"), hence an expected KL (p.4: "The loss ℓθ equals the expected KL-Divergence"). The guarantee holds only under the prior's own data distribution; it says nothing about data outside the prior. Priors studied: GPs and BNNs. Evaluation: GP and BNN posteriors against MCMC and variational inference (VI), small tabular sets.

#### Row 16. Nagler 2023, *Statistical Foundations of Prior-Data Fitted Networks*
- **Paper:** https://arxiv.org/abs/2305.11097v1 (arXiv v1). Peer reviewed: ICML 2023, PMLR 202 (p.1).
- **Fields:** Prior failure modes (p.4: "the prior may wash out very slowly or not at all if it puts too much mass in unfavorable regions"); outside the support, the PPD converges to a KL-optimal member of the support (Theorem 3.1, p.4). For a fixed trained network, variance falls with n but bias need not (p.1: "the bias vanishes only if it is appropriately localized around the test feature"; "in current PFN implementations ensures only the former"). Training-size prior: TabPFN v1 used uniform {1,…,1023} (p.4). Implication for this brief: the n distribution in the prior acts as a regulariser on model complexity (p.4).

#### Row 17. Melnychuk, Balazadeh, Feuerriegel, Krishnan 2026, *Frequentist Consistency of Prior-Data Fitted Networks for Causal Inference*
- **Paper:** https://arxiv.org/abs/2603.12037v3 (arXiv v3). Peer reviewed: ICML 2026, PMLR 306 (p.1).
- **Prior components examined:** The implicit priors of TabPFN, CausalPFN and CausalFM.
- **Key finding on confounding strength:** p.2: "the PFN's posterior is concentrated on nearly unconfounded data-generating processes, so the ATE estimates can be biased even as the sample size grows"; measured on prior samples (p.5: "∆ is still highly concentrated around zero for the PFNs."). Mechanism (p.5: "they rarely depend on the same subsets of covariates").
- **Identifying assumptions:** Consistency, strong overlap, unconfoundedness (p.4).
- **Remedy:** One-step posterior correction (OSPC) via martingale posteriors, restoring frequentist consistency for the ATE (abstract). This is a post-hoc correction, not a change to the prior.
- **Evaluation:** Synthetic and semi-synthetic ATE experiments (figure-level results not transcribed). ATE only, not CATE.

#### Row 18. Melnychuk et al. 2026, *Debiased Prior-Data Fitted Networks for Amortized Bayesian Semi-Parametric Inference*
- **Paper:** https://arxiv.org/abs/2610.28314v1 (arXiv v1). Preprint.
- **Fields:** Breadth–rate trade-off (p.1: "can become slower as the prior becomes more diverse"); empirical claim about TabPFN versions (p.6: "we empirically show that more recent versions of TabPFN") having slower L2 concentration (v2 to 2.5 to 3). Remedies: label correction and prior correction based on efficient influence functions. Targets are finite-dimensional (for example the ATE), not CATE.

#### Row 19. Hülskamp, Kobialka, Sommer, Nagler, Rügamer 2026, *How Well Do Prior-Data Fitted Networks Amortize Bayesian Inference?*
- **Paper:** https://arxiv.org/abs/2610.13764v2 (arXiv v2). Preprint.
- **Fields:** Deployment error split into prior, context and amortisation error (p.1: "the prior error arises when the deployment tasks differ from the prior"). In-prior approximation is good, except (p.1: "parts of the residual amortization error persist, especially in rare settings under the prior pretraining distribution"). Remedy (p.8: "deep ensembles of PFNs deliver most of the attainable gain"). Evaluated on TabICLv2 and nanoTabPFN only (p.8).

#### Row 20. *Characterizing the Separability Gap in Prior-Data Fitted Networks* (2026)
- **Paper:** https://arxiv.org/abs/2610.14989v1 (arXiv v1). Preprint. Abstract and introduction read.
- **Fields:** Common SCM priors couple the feature distribution and the label mechanism (abstract: "We show that common PFN priors are non-separable, even in simple settings."). Under misspecification (abstract: "prior non-separability can favor better feature fit at the expense of conditional label fit"). This is relevant when real covariates (lesion latents, EHR codes) lie outside the prior's covariate law.

#### Row 21. Müller, Hollmann, Hutter et al. 2025, *Position: The Future of Bayesian Prediction Is Prior-Fitted*
- **Paper:** https://arxiv.org/abs/2505.23947v1 (arXiv v1). Peer reviewed as a position paper: ICML 2025 (arXiv comment).
- **Fields:** p.7: "PFNs approximate Bayesian prediction, which fundamentally requires the dataset to have support in the prior."; and even inside it (p.7: "PFNs might yield poor approximations even within the support"). Limitation (p.5: "it is less clear what data they work well on").

### D. Real-data-anchored, domain-informed and fine-tuned priors

#### Row 22. Neal, Huang, Raghupathi 2020, *RealCause: Realistic Causal Inference Benchmarking*
- **Paper:** https://arxiv.org/abs/2011.15007v2 (arXiv v2). Preprint.
- **Prior components (as a plasmode generator):** p.2: "we fit generative models Pmodel (T | W ) and Pmodel (Y | T,W ) that closely match the real analogs"; real covariates are resampled (p.2: "first sampling W from the real data").
- **Identifying assumptions:** Unconfoundedness given W by construction (p.2).
- **Relevance:** This is the template for plasmode-style priors and a benchmark used by CausalPFN, Do-PFN and TabPFN-2.5/3. That makes it a source of mechanism leakage (row 1) if its ideas enter the prior.

#### Row 23. Garg et al. 2025, *Real-TabPFN: Improving Tabular Foundation Models via Continued Pre-training With Real-World Data*
- **Paper:** https://arxiv.org/abs/2507.03971v1 (arXiv v1). Workshop paper: 1st ICML Workshop on Foundation Models for Structured Data (p.1).
- **Prior components:** Stage 2 uses real data only (p.3: "Stage 2 continues pre-training exclusively on a curated collection of heterogeneous real-world tables.").
- **Ablation results:** OpenML plus Kaggle beat either alone (+0.022 vs +0.015 for Kaggle alone, p.4); (p.4: "outperforms the default TabPFNv2 on most of the datasets").
- **Held out?** Five-step contamination filter (p.2: "We generated hashes of both rows and columns to identify potential data duplications at a granular level."), plus only datasets over 10,000 rows.

#### Row 24. Rubachev et al. 2025, *On Finetuning Tabular Foundation Models*
- **Paper:** https://arxiv.org/abs/2506.08982v2 (arXiv v2). Preprint.
- **Fields:** Abstract: "Our findings establish full finetuning as the most practical solution for TabPFNv2"; negative result: "on datasets with gradual temporal shifts and rich feature sets, TabPFNv2 is less stable and prior methods remain better." This is per-dataset fine-tuning, not prior fine-tuning.

#### Row 25. Kolberg et al. 2026, *TabPFN-Wide: Continued Pre-Training for Extreme Feature Counts*
- **Paper:** https://arxiv.org/abs/2510.06162v2 (arXiv v2, 29 Mar 2026). Preprint.
- **Prior components:** TabICL prior followed by feature widening (p.4: "we first sample a dataset with a moderate number of features m from the TabICL prior and subsequently widen it to a target dimension"), using sparse linear maps plus noise for continuous features and sparse copying for categorical ones.
- **Ablation / result:** Abstract: existing PFNs "are currently not suited to handle large feature counts (> 500)"; the widened model "matches or exceeds its base model's performance" and scales beyond 30,000 features. Evaluated on omics data.
- **Held out?** Not stated.

#### Row 26. *Causal Data Augmentation for Robust Fine-Tuning of Tabular Foundation Models* (CausalMixFT, 2025)
- **Paper:** https://arxiv.org/abs/2601.04110v2 (arXiv v2). Workshop paper: EurIPS 2025 Workshop on AI for Tabular Data (arXiv comment).
- **Fields:** A target-anchored prior. Abstract: "generating structurally consistent synthetic samples using Structural Causal Models (SCMs) fitted on the target dataset"; median normalised ROC-AUC gain 0.10 to 0.12; (abstract: "it narrows the median validation-test performance correlation gap from 0.67 to 0.30"). Classification only; not causal estimation.

#### Row 27. Zhou 2026, *When and Why LLM Causal Priors Help: Closed-Loop Prior Selection for Amortized Causal Inference*
- **Paper:** https://arxiv.org/abs/2609.06941v1 (arXiv v1). Preprint (single author).
- **Prior components:** Domain-informed priors from causal graphs distilled by a large language model (LLM), injected by post-training a Do-PFN base for 20k steps (p.10).
- **Fine-tuning finding:** p.10: "the officially released weights perform well but are insensitive to continued training, while a weaker locally retrained base (denoted v2) is plastic".
- **Ablation results:** In-domain gain (abstract: "attains a formally significant 2.75× gain on the primary evaluation domain"). Boundary (abstract: "injection yields significant gains only when the base is underfit on the task domain, the prior domain matches the task domain, and the task lies within the support of the base's training prior"). Cross-domain cost: the injected prior degraded IHDP PEHE (p.21: "degrades significantly on IHDP (∆ = +2.09, p < 0.0001)"). Out-of-support dimension (p.21: "the IHDP benchmark's 26 dimensions far exceed the prior-support dimension range [1, 6]"). Negative: (abstract: "averaging multiple distillation sources dilutes gains, and synthetic probe metrics systematically diverge from real-domain transfer").
- **Held out?** No. The selection score is dominated by primary-domain generalisation (p.7: "with real-domain generalization weighted above half"), and the final verdict is also on the primary domain (p.10: "The primary metric is the normalized mean-squared error (NMSE) on that domain, the final adjudication criterion."). The author notes the score (p.6: "is not an unbiased estimate"). IHDP/Lalonde serve as external checks.

#### Row 28. Reuter et al. 2026, *Use What You Know: Causal Foundation Models with Partial Graphs*
- **Paper:** https://arxiv.org/abs/2602.14972v3 (arXiv v3). Peer reviewed: ICML 2026, PMLR 306 (p.1).
- **Fields:** Domain knowledge enters as conditioning input rather than as a restricted prior (abstract: "in their current state, they do not allow for the incorporation of any domain knowledge"). Result (abstract: "allows a general-purpose CFM to match the performance of specialised models trained on specific causal structures"). Prior: Do-PFN-style SCMs extended into a TFM prior (p.6). Evaluation on synthetic case studies from the same prior family (p.7) **(my reading: in-family)**.

### E. Out-of-prior evaluation of causal PFNs

#### Row 29. Mourão et al. 2026, *Prior-Data Fitted Networks for Causal Inference: a Simulation Study with Real-World Scenarios*
- **Paper:** https://arxiv.org/abs/2603.15928v2 (arXiv v2). Preprint.
- **Fields:** Plasmode-style evaluation outside every PFN prior: binary confounders, treatment and outcome, with laws taken from real data (p.7: "Each simulation scenario was defined by the empirical distributions"); n = 200, 500, 1,000. Outcome type: binary; target is the ATE. Result (p.15: "CausalPFN yielded 95% CI coverage rates of 54.3% and 67.6%"); bias correction helped little (p.17). Identification: positivity, exchangeability and consistency hold by design (p.7).

#### Row 30. Jung et al. 2026, *What You Observe Determines How You Identify Causal Effects* (CausalIDView)
- **Paper:** https://arxiv.org/abs/2609.36881v1 (arXiv v1). Preprint.
- **Fields:** Benchmark SCMs are the authors' own construction, not taken from any CFM prior **(my reading: held out of all three priors)**; observational views vary the identification regime. Abstract: "no CFM consistently performs best and model rankings vary substantially". Exact-zero effects tested with pre-treatment outcomes in three RCTs (p.6: "implying τ0 (x) = E[Y pre (1) − Y pre (0) |"; true CATE 0). Null-CATE mean squared error, ACTG 175: CausalFM 0.0053, CausalPFN 0.0146, Do-PFN 0.0203, TabPFN-3.5 S-learner 0.0008 (Table 2, p.9). Illinois: Do-PFN 0.1249 vs CausalFM 0.0016.

#### Row 31. Stith, Rahmani, Cresswell 2026, *Causal Foundation Models* (tutorial)
- **Paper:** https://arxiv.org/abs/2609.03003v1 (arXiv v1). Preprint.
- **Fields:** Evidence gap stated directly (p.17: "So far, no research has been published on the quality of priors for CFMs."). Desired property (p.25: "automatic detection of mismatch between the target DGP and the training prior"). Describes the CausalPFN-style CEPO-node construction (p.17).

### F. Survival PFNs (no treatment effects in any of them)

#### Row 32. Qi, Balazadeh, Cooper, Greiner, Krishnan 2026, *SurvivalPFN*
- **Paper:** https://arxiv.org/abs/2605.15488v1 (arXiv v1). Preprint.
- **Prior components:** Random-MLP covariates; event and censoring times from two further MLPs (p.6: "we then sample two additional random MLPs, and then apply them on the generated covariates to sample event/censoring times"); four generator families (naive, survival-distribution, Weibull/log-normal mixture, kitchen-sink); four censoring mechanisms (p.6: "uniform censoring", random, administrative, conditionally independent).
- **Identifying assumptions:** Conditionally independent censoring (p.3: "Assumption 2.1 (Conditional independent censoring)"); consistency claimed for identifiable priors (p.5).
- **Ablation results:** p.46: "the survival-distribution prior is consistently stronger than the naive prior"; kitchen-sink (p.46: "performs competitively but does not clearly dominate the survival-distribution prior"). Predictive pretraining first (CausalPFN-style) is "generally helpful but not uniformly decisive" (p.47).
- **Evaluation / held out:** 61 datasets; default checkpoint is (p.46) "the best validation run"; separation of validation from benchmark datasets not stated.

#### Row 33. *SurvICL: a Foundation Model for in-context Survival Analysis* (2026)
- **Paper:** https://arxiv.org/abs/2610.22242v1 (arXiv v1). Preprint.
- **Prior components:** TabICLv2-style SCM covariates (2–32 nodes, 1–100 features, p.5) and a proportional-odds event-time prior (p.5: "hazard ratios then vary over time and may vanish in the long run, a common pattern in clinical data that Cox priors cannot generate").
- **Ablation results:** On development datasets with a smaller model (p.9: "our proportional-odds prior outperforms Cox (77.6) and mixed priors (84.0)"); also beats the SurvPFN, SurvivalPFN and SIC priors. Negative: a censoring-head variant reduced performance (81.0).
- **Held out?** Yes, the strongest safeguard found (p.2: "all results are reported on 63 held-out datasets never used during development"). Abstract: "no existing TFM beats the half-century-old Cox model". On large data, boosting remains best (p.8).

#### Row 34. Seletkov et al. 2026, *Survival In-Context* (SIC)
- **Paper:** https://arxiv.org/abs/2603.29475v2 (arXiv v2). Preprint.
- **Fields:** SCM covariates plus continuous (closed-form inverse cumulative hazards) and discrete (monotonic network) event-time priors; censoring (p.5: "we draw censoring times Tcens using the same sampling mechanism as for event times with the risk scores (η1 , η2 ) set to 0"), plus administrative cutoff. Abstract: "explicit control over covariates and time-event distributions".

#### Row 35. Böhm et al. 2026, *SurvPFN: Towards Foundation Models for Survival Predictions*
- **Paper:** https://arxiv.org/abs/2606.04564v2 (arXiv v2). Workshop paper: ICML 2026 Foundation Models for Structured Data workshop (arXiv comment).
- **Fields:** p.2: "Event times are drawn from a Weibull distribution under both proportional and non-proportional hazard assumptions, with non-informative censoring applied on top."; covariates (p.2: "Each dataset has d ∈ {2, . . . , 10} covariates and up to 1000 rows."). Small prior range; weakest prior in SurvICL's comparison (row 33).

---

## 3. Synthesis (what is established, contested, missing)

**Established.**
1. *Identification must be built into the prior.* Two separate proofs say a PFN converges to the true effect only if the prior puts no mass on non-identified DGPs (row 1, Proposition 1; row 3, Theorem 4.3). Do-PFN, which does not enforce this, concentrates only up to an equivalence class (row 2). Training under the wrong identification design worsened PEHE in CausalFM's own test (row 3, Table 9). These results are asymptotic and in-prior; neither gives finite-sample rates (row 1 limitation).
2. *The prior is the dominant design lever for predictive TFMs.* Swapping the prior with the architecture fixed changed TabICLv2 more than any architectural choice (row 10). SCM priors beat BNN priors (row 4), and tree-based components add to SCMs (rows 9, 11). Mechanism diversity was the largest component in O'Prior's ablation (row 12).
3. *Performance degrades outside the prior's n, p or mechanism range.* Seen with more covariates than trained (row 1, Table 5), larger graphs (row 2), higher noise variance or averaged mechanisms (row 2), and out-of-family DGPs (row 1, overconfidence). Feature counts above 500 need a widened prior (row 25). Moderate extrapolation in n works (rows 1, 4).
4. *Existing priors encode almost no observed confounding.* Measured confounding in TabPFN, CausalPFN and CausalFM prior draws is concentrated near zero, which biases ATE posteriors (row 17). Do-PFN's prior is dominated by small effects (row 2).
5. *Real-data continued pretraining helps prediction* when strict deduplication is applied (rows 6, 23).

**Contested.**
- *Does coverage of real data matter?* Row 13 finds that better coverage goes with better performance; row 14 finds a large synthetic–real gap with no detectable performance effect.
- *Is broader always better?* CausalPFN's design rule says broadening the identified prior helps (row 1). Debiased-PFN theory and the TabPFN version comparison suggest broader priors slow posterior concentration (row 18). Kitchen-sink survival priors did not beat a targeted family (rows 32, 33), and averaging LLM-distilled priors diluted gains (row 27).
- *Causal PFN versus modular TFM plus identification.* CausalPFN leads on IHDP (rows 1, 27). Outside their priors, rankings flip: no CFM is consistently best, and TabPFN-based meta-learners were best on two of three null-effect RCTs (row 30). CausalPFN interval coverage on binary-outcome plasmode scenarios was 54–68% (row 29).
- *Fine-tuning a released causal model.* Fine-tuning TabPFN on a causal prior helped (row 1, Table 3). Released Do-PFN weights barely moved under continued training (row 27). No study compares fine-tuning a causal PFN with training from scratch on the same target prior.

**Missing.**
- No published ablation of a causal prior's components: confounding strength (except unobserved α in row 3), overlap ξ, heterogeneity γ, noise, mixture weights, or the real/synthetic base-table split. Row 31 states this gap.
- No causal prior generates **binary outcomes** natively in a described way (rows 1–3 are continuous); the only binary-outcome test is negative (row 29).
- No prior contains **sparse or deterministic effects with many exact zeros**. CausalPFN's γ = 0 gives homogeneous effects, not sparse ones (row 1). Exact-zero behaviour has been tested only post hoc (row 30).
- **No survival PFN estimates treatment effects** (rows 32–35; searches A9 and W3 returned none).
- No PFN has been trained on a prior anchored on **EHR or imaging-derived covariates**. CausalPFN's OpenML base tables are the only real-covariate causal prior (row 1).
- Few studies separate prior-design data from evaluation data. The exceptions are SurvICL (row 33) and the TabPFN v2 development sets (row 5).

---

## 4. Extra output 1: candidate prior specifications

Evidence strength codes: **E** = direct ablation or theorem in a causal PFN; **I** = indirect (predictive-TFM ablation or theory transferred to causal use); **J** = judgement with thin or no evidence.

### 4.1 Application A: lesion-representation virtual trials (binary outcome, n = 300–3,000, randomised and confounded)

| # | Component | Proposed specification | Evidence (rows) | Strength |
|---|---|---|---|---|
| A1 | Identification class | Back-door only: treatment depends only on observed covariates; positivity enforced; no prior mass on unobserved confounding. Train a separate model if IV or front-door designs are ever needed. | 1 (Prop. 1), 3 (Thm 4.3, Table 9), 2 (no identifiability → equivalence-class concentration) | E |
| A2 | Covariate source | Mixture of (a) **real lesion-latent covariate tables** drawn from a training-only anatomy pool, plasmode-style, and (b) synthetic SCM covariate tables in the TabPFN/TabICL style (SCM plus tree mechanisms). Suggested start 50/50, then set the weight on a development set disjoint from evaluation. | 1 (OpenML base tables plus synthetic), 22 (plasmode template), 23 (real-data gains), 4, 9, 11 (SCM + tree mixtures; 50/50 and 70/30 used) | I; weight J |
| A3 | Covariate dimension p | Cover the encoder latent dimension plus clinical covariates with margin. Train above the deployed p (for example up to 2× it), because performance drops beyond the training maximum. | 1 (Table 5), 2 (graph size), 27 (out-of-support dimension) | E |
| A4 | Sample size n | Log-uniform over about 100–6,000 so that 300–3,000 sits inside the support. Include small n to regularise. | 1 (Table 4), 2 (dataset-size ablation), 4, 16 (n prior as regulariser) | I |
| A5 | Allocation | Mixture of constant propensity (randomised trials) and linear and nonlinear logits (confounded). Use a positivity-degradation parameter ξ as in CausalPFN. Oversample strong *observed* confounding so that the prior's confounding distribution is not concentrated at zero. RCT share about one third (J). | 1 (D.1 mechanisms, ξ), 17 (PICB: Δ near 0 in existing priors) | E for mechanisms; weights J |
| A6 | Outcome mechanism | Binary Y ~ Bernoulli(p_t(x)), with p_t from SCM/tree/MLP functions of covariates and t, plus a varied baseline-risk intercept. **Train on the CEPO (risk) target, not on noisy Y**, so the model learns epistemic uncertainty about the risk difference. | 1 (CEPO loss), 2 vs 1 (Appendix E of row 1 on aleatoric noise), 29 (binary-outcome failure of CausalPFN) | J (no published binary causal prior) |
| A7 | Effect heterogeneity | Mix four regimes: homogeneous (CausalPFN γ = 0), smooth heterogeneity (γ ∈ (0, 1]), **sparse effects with exact zeros** (effect non-zero only in an anatomically or latently defined subset), and a global null (τ ≡ 0). Effect-size distribution wide, so that large effects are not rare. | 1 (γ control), 2 (low-ATE prevalence harms large-effect cases), 30 (null-effect behaviour varies by CFM) | J (no ablation exists) |
| A8 | Mechanism families | SCM with diverse activations, tree-based mechanisms and hybrid multi-family DAGs. Hold some families out (A-leak 2). | 10, 11, 12 (diversity dominant), 9 | I |
| A9 | Noise | Varied, including heavy-tailed; for binary outcomes this enters through the risk function. Edge-noise details matter little for prediction. | 2 (sensitive to noise variance), 10 (edge noise negligible) | I |
| A10 | Training path | Two-stage training as in CausalPFN: predictive phase, then CEPO phase. Optionally initialise from a released predictive TFM. Do not rely on continued training of released causal weights. | 1 (two-stage; TabPFN fine-tuned on a causal prior improved), 27 (released Do-PFN weights not plastic), 23 | I/J |
| A11 | Uncertainty | Temperature-scale on observed outcomes; ensemble independently pretrained models; check coverage of subgroup averages separately from unit-level coverage. | 1 (temperature scaling), 19 (ensembles), 29 | I |

Thin points: A6 and A7 have no direct evidence. The A2 weighting and the A5 shares are judgements.

### 4.2 Application B: CPRD Aurum SGLT2 versus DPP-4 (n = 56,337; ~40 covariates + ≤500 code indicators; HbA1c at 1 year; later time-to-event)

| # | Component | Proposed specification | Evidence (rows) | Strength |
|---|---|---|---|---|
| B1 | Identification class | Back-door (no unmeasured confounding given covariates) with positivity. Report sensitivity separately, because the prior cannot represent violations without losing consistency. | 1, 3, 17 | E |
| B2 | Context size n | Training contexts up to several thousand rows (TabICL-style curriculum to tens of thousands), plus retrieval or stratified subsampling at inference for 56,337 rows. | 1 (retrieval for large tables; performance drop on largest tables), 9, 10 (curricula to 60K) | I |
| B3 | Feature count and type | p up to about 600: about 40 dense mixed-type covariates plus a **wide block of sparse binary indicators**, many uninformative or correlated. Use widening as in TabPFN-Wide and explicitly inject uninformative features. | 4 (uninformative-feature failure), 25 (widening prior; >500 unsupported), 5 (p ≤ 160), 1 (Table 5) | I |
| B4 | Covariate source | Synthetic SCM covariates mixed with **plasmode base tables from a CPRD extract disjoint from the analysis cohort** (different practices or calendar period), or another UK primary-care source. | 1, 22, 23, 20 (non-separable priors misfit off-support covariates) | I/J |
| B5 | Allocation | Strong observed confounding by indication is the norm. Oversample large propensity–outcome overlap in the covariates driving both. Positivity degradation ξ with mass near poor overlap. No RCT component needed, though a small share is harmless. | 17 (Δ ≈ 0 in priors), 1 (ξ) | E/J |
| B6 | Outcome, continuous | HbA1c at one year as CEPO with heteroscedastic noise. Include baseline-HbA1c-dependent effects and regression-to-the-mean structure (J). | 1 (heteroscedastic construction) | I/J |
| B7 | Outcome, time-to-event | Potential event times T(0), T(1) from survival-distribution families (proportional odds with time-varying hazard ratios; Weibull/log-normal mixtures) and independent or administrative censoring. Target the CATE on a defined scale, for example the restricted mean survival time difference. **No published causal survival PFN exists; this is untested.** | 32, 33, 34, 35 (survival priors and censoring), 33 (held-out protocol) | J |
| B8 | Missingness | MAR and MNAR missingness in dense covariates; absence-of-code semantics for indicators. | 5 (MCAR), 12 (MAR/MNAR realism helped) | I |
| B9 | Effect heterogeneity | Same four regimes as A7, with effects tied to few covariates (for example kidney function, baseline HbA1c). | 1, 2, 30 | J |
| B10 | Uncertainty | Do not trust ATE posteriors without correction (OSPC/debiasing) or calibration checks; ensembles. | 17, 18, 19, 29 | I |

Thin points: B7 has no evidence for causal survival. B4 and B5 weights are judgements. Context scale for n = 56,337 relies on retrieval evidence from CausalPFN, which itself degraded on its largest tables (row 1).

---

## 5. Extra output 2: leakage risks between training prior and evaluation mechanisms

| # | Risk | Where seen in the literature | Concrete safeguard |
|---|---|---|---|
| L1 | **Same anatomy or patients** in the prior's real base tables and in the evaluation virtual trials (Application A) | CausalPFN excluded OpenML tables sharing covariates with test sets (row 1); Real-TabPFN and TabPFN-2.5 hash-deduplicated (rows 23, 6) | Split the lesion pool at patient level *before* building any prior table. Keep a written manifest of IDs per split. Hash rows and latent vectors to prove disjointness. Fit the encoder only on prior-split lesions or on an external set, so that latents of evaluation patients are never used in prior construction. |
| L2 | **Effect-function families shared** between prior and benchmark (for example the evaluation's severity/location/network effect processes reused in the prior) | Do-PFN synthetic case studies reuse prior parameter laws (row 2); CausalFM synthetic tests use the prior generator (row 3) | Define evaluation effect families first and freeze them. Exclude them, or parameter ranges of them, from the prior. Report in-family and held-out-family results separately, as CausalPFN did for polynomial/sinusoid families (row 1). |
| L3 | **Shared post-processing or benchmark code** (positivity or heterogeneity transforms from the benchmark generator used in the prior) | CausalPFN positivity and heterogeneity transforms "inspired by RealCause", with RealCause effects in Lalonde benchmarks (row 1) | Do not import the evaluation generator's code or transforms into the prior. If unavoidable, label that benchmark as in-family. |
| L4 | **Covariate distributions reused** (CPRD cohort covariates both in the plasmode prior and in plasmode evaluation; Application B) | No causal paper addresses it; row 20 shows feature-law coupling matters under misspecification | Build prior base tables from a disjoint extract (other practices, other years or another database). Measure structural coverage of the evaluation cohort by the prior (row 13) and report it. |
| L5 | **Tuning the prior on the test benchmarks** (mixture weights, hyperparameters, checkpoint choice) | Mitra ablation on TabRepo, also an evaluation benchmark (row 11); Zhou selection and verdict on the same domain (row 27); SurvivalPFN "best validation run" (row 32) | Pre-specify a development suite disjoint from final evaluation, following SurvICL's 40 development / 63 held-out split (row 33) and TabPFN v2's development datasets (row 5). Freeze the prior before opening final evaluation. Register the number of prior variants tried. |
| L6 | **Query-row information in preprocessing** (normalisation or encoding fitted on query and test rows) | O'Prior contract (row 12) | Fit every preprocessing statistic on context rows only, in both prior generation and evaluation pipelines. |
| L7 | **Identification assumptions identical in prior and benchmark**, which flatters in-prior performance (benchmarks unconfounded by construction) | RealCause unconfoundedness strictly holds (rows 2, 22); Mourão positivity guaranteed (row 29) | Add stress tests outside the prior (hidden confounding, near-violations of positivity) as a separate, clearly labelled robustness arm. Do not pool them with in-assumption results. |
| L8 | **Real trial or real cohort used for both selection and validation** | Not reported in causal PFN papers | Hold out the real-trial validation data from every design decision. Fix the model before unblinding, as for a prespecified analysis. |
| L9 | **Effect-size or sparsity regimes chosen to match the benchmark truth** (for example adding exact-zero effects only after seeing the null-effect benchmark) | Null-effect tests in row 30 were post hoc to all CFM priors | Specify heterogeneity regimes (A7/B9) from clinical reasoning before evaluation. Keep the null-effect and negative-control tests (row 30 design) as external checks. |

---

## 6. Excluded near-misses

| # | Citation | Link | Reason for exclusion |
|---|---|---|---|
| N1 | Bynum et al. 2025, *Black Box Causal Inference* | https://arxiv.org/abs/2503.05985v1 | Amortised ATE meta-prediction with an MSE loss on low-dimensional synthetic SCMs; prior too sparse to extract the Brief 4 fields; Brief 1 near-miss. |
| N2 | Zhang et al. 2023, *Towards Causal Foundation Model* (CInA) | https://arxiv.org/abs/2310.00809v3 | ATE via covariate balancing; not a PFN prior. |
| N3 | Nilforoshan et al. 2023, *Zero-shot causal learning* (CaML) | https://arxiv.org/abs/2301.12292v4 | Meta-learning within one claims database; no synthetic prior. |
| N4 | Kirpichenko et al. 2025, *FoCAT* (Doklady Mathematics) | https://doi.org/10.1134/S1064562425700280 | Full text not reachable (Brief 1 Crossref abstract only); prior details unverifiable. |
| N5 | Zhu et al. 2026, *A Causal Foundation Model for Structure and Outcome Prediction* | https://arxiv.org/abs/2606.26467v1 | Interventional prediction with graph output; no prior ablation relevant to CATE. |
| N6 | Zhang Z. 2026, *Learning to Fluctuate* | https://arxiv.org/abs/2609.26290v2 | ATE sampling-law pretraining; its attenuation example (p.1) is hypothetical, not an experiment. |
| N7 | Javurek et al. 2026, *Amortizing Causal Sensitivity Analysis via PFNs* | https://arxiv.org/abs/2605.10590v1 | Bounds under hidden confounding; not a point-identified CATE prior. |
| N8 | Muller et al. 2026, *ProximalFM* | https://arxiv.org/abs/2610.08078v2 | Proximal identification; outside both applications' design. |
| N9 | Bellot, Dhir 2026, *Foundation Models for Partial Causal Identification* | https://arxiv.org/abs/2608.20841v1 | Discrete observables; bounds only. |
| N10 | Gao et al. 2026, *CIDER-FM* | https://arxiv.org/abs/2609.39523v1 | Combines experimental regimes; interventional distributions. |
| N11 | Stith et al. 2026, *Causal Foundation Models with Continuous Treatments* | https://arxiv.org/abs/2605.15133v2 | Continuous treatments; both applications have binary treatment. |
| N12 | Zare et al. 2026, *CausalLongPFN* | https://arxiv.org/abs/2606.05797v2 | Longitudinal counterfactual prediction. |
| N13 | Chen et al. 2026, *PICLE-PFN* | https://arxiv.org/abs/2610.32863v1 | Longitudinal dynamic policies. |
| N14 | Sauter et al. 2025, *ACTIVA* | https://arxiv.org/abs/2503.01290v4 | Variational model of interventional distributions; no CATE prior ablation. |
| N15 | *IV-ICL* 2026 | https://arxiv.org/abs/2605.12924v1 | IV bounds; abstract only. |
| N16 | Schulman, Bynum, Wald 2026, *Unit-level aggregation breaks coverage in causal foundation models* | https://arxiv.org/abs/2610.22770v1 | Interval aggregation at inference, not prior design (relevant to A11; see Brief 1 row 9). |
| N17 | Chen et al. 2026, *TabCF* | https://arxiv.org/abs/2605.05993v1 | Control-function IV estimation. |
| N18 | *CAFE: Counterfactual Prediction via Fast Posterior Estimation* 2026 | https://arxiv.org/abs/2609.32167v1 | Individual counterfactuals in ANMs; abstract only. |
| N19 | *PerturbPFN* 2026 | https://arxiv.org/abs/2607.23447v1 | Drug-perturbation expression modelling; abstract only. |
| N20 | *Computational Identifiability* 2026 | https://arxiv.org/abs/2606.19361v1 | Conceptual identification framework, not PFN priors; abstract only. |
| N21 | *InCOPE: PFNs for In-Context Off-Policy Evaluation* 2026 | https://arxiv.org/abs/2610.34035v1 | Markov decision process policy values, not static CATE; abstract only. |
| N22 | *KnowsTFM* 2026 | https://arxiv.org/abs/2606.30258v1 | Knowledge-graph fine-tuning for prediction; abstract only. |
| N23 | *Causal Pre-training Under the Fairness Lens* 2026 | https://arxiv.org/abs/2601.17912v2 | Fairness of TabPFN predictions. |
| N24 | Tugnoli et al. 2026, *Improving TabPFN's Synthetic Data Generation by Integrating Causal Structure* (UAI 2026) | https://arxiv.org/abs/2603.10254v3 | TabPFN as a data generator, not a training prior. |
| N25 | Lyu et al. 2026, *SurvFM*; Kim et al. 2026, *TFMs Can Do Survival Analysis*; Vargas Vieyra 2026; Pham et al. 2026 | https://arxiv.org/abs/2607.09577v2 ; https://arxiv.org/abs/2601.22259v2 ; https://arxiv.org/abs/2606.03689v1 ; https://arxiv.org/abs/2606.12006v1 | Adapt existing TFMs to survival; no new prior (abstract level). |
| N26 | *Effortless, Simulation-Efficient Bayesian Inference using TFMs* (NPE-PFN) 2025 | https://arxiv.org/abs/2504.17660v2 | Simulation-based inference with TabPFN; not a causal prior. |
| N27 | Ye et al. 2026 (TabCon); Shi et al. 2026 (TabCUQ) | https://arxiv.org/abs/2609.33114v1 ; https://arxiv.org/abs/2610.39558v1 | Inference/uncertainty for generic targets; no prior construction (Brief 1 screening). |
| N28 | *CausalEcon* (economic-panel causal foundation model) | (no arXiv ID; Semantic Scholar title only) | Could not be located (search W1); not assessed. |

---

*Verification log:* `/tmp/claude-0/-home-user-neuro-causal-pfn/4e9e7a9b-8303-5353-a6ff-c116b3e7e89c/scratchpad/brief4/verification_log.md`. Full texts are in `.../scratchpad/brief4/texts/` (layout and raw `pdftotext` outputs).
