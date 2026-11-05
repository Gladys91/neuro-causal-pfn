# Brief 6: Pre-training of tabular foundation models, general and causal

**Date:** 4 November 2026

**Question:** Which aspects of pre-training determine how tabular foundation models (TFMs) generalise? What is known, or testable, about carrying them over to causal prior-fitted networks (PFNs) used with image-derived latents and with electronic health records (EHR)?

**Applications served:**
- **(A) Image-latent virtual trials:** effects estimated from brain-lesion representations in semi-synthetic virtual trials, with binary outcomes and 300 to 3,000 patients per trial.
- **(B) Primary-care records:** effects estimated from primary-care EHR, with about 56,000 patients, about 540 covariates, and continuous (later time-to-event) outcomes.

**Scope:**
- papers citing the two named seeds;
- studies that isolate one pre-training dimension (prior design and mixtures, real-data or continued pre-training, architecture, training objective, curriculum, scale, context length and retrieval, fine-tuning versus in-context use) with the others held fixed;
- causal PFN papers that ablate any of these;
- TFMs applied to learned image latents;
- individual-effect prediction or retrieval with in-context models in stroke and in EHR.

The *content* of causal priors was covered by Brief 4 and is not repeated here.

**Abbreviations used throughout.**
ADNI: Alzheimer's Disease Neuroimaging Initiative. ATE: average treatment effect. AUC / AUROC: area under the receiver operating characteristic curve. AUPRC / AUPR: area under the precision-recall curve. BMT: best medical treatment. CAPO: conditional average potential outcome. CATE: conditional average treatment effect. CI: confidence interval. CLIP: Contrastive Language-Image Pre-training (image encoder). CPRD: Clinical Practice Research Datalink. Ctd: time-dependent concordance index. DINO: self-distillation with no labels (image encoder family; DINOv2, DINOv3). Elo: Elo rating, a pairwise-comparison score. EENO: excellent early neurological outcome. EVT: endovascular treatment. FSP: fluctuation-supervised pre-training. GBDT: gradient-boosted decision trees. GIST: Generator-state-Informed Supervision for TFMs. HTE: heterogeneity of treatment effect. IBS: integrated Brier score. ICL: in-context learning. ICU: intensive care unit. IF-PEHE: influence-function-based PEHE. IID: independent and identically distributed. IQM: interquartile mean. JEPA: joint-embedding predictive architecture. kNN: k nearest neighbours. MISE: mean integrated squared error. MLP: multilayer perceptron. MRI: magnetic resonance imaging. NIHSS: National Institutes of Health Stroke Scale. NLL: negative log-likelihood. OOD: out of distribution. PCA: principal component analysis. PEHE: precision in estimating heterogeneous effects. PET: positron emission tomography. RMSE: root mean squared error. RSF: random survival forest. SCM: structural causal model. SD: standard deviation. SSL: self-supervised learning. TFM: tabular foundation model. TTE: time-to-event. Also: AIPW: augmented inverse probability weighting. BO: Bayesian optimisation. CNN: convolutional neural network. CN / MCI / AD: cognitively normal / mild cognitive impairment / Alzheimer's disease. CRPS: continuous ranked probability score. DML: double machine learning. DOI: digital object identifier. DR, S, T, X learners: doubly robust, single-model, two-model and cross meta-learners. DSRF, DT, ET, GB, RF: prior families in Mitra (DSRF as named by its authors; decision tree, extra trees, gradient boosting, random forest). ECE: expected calibration error. F1: harmonic mean of precision and recall. FMSD: the ICML workshop on Foundation Models for Structured Data. GCN: graph convolutional network. HDLSS: high-dimensional, low-sample-size. IDH: isocitrate dehydrogenase. LLM: large language model. LVO: large vessel occlusion. ML: machine learning. MoCA: Montreal Cognitive Assessment. MSE: mean squared error. OEE: overall equipment effectiveness. OU: Ornstein–Uhlenbeck. PMC / PMID: PubMed Central identifier / PubMed identifier. RCT: randomised controlled trial. ROC: receiver operating characteristic. SDE: stochastic differential equation. SFT: supervised fine-tuning. SNP: single-nucleotide polymorphism. SSM: state-space model. TCGA: The Cancer Genome Atlas. UCI: University of California, Irvine (machine-learning repository). UTI: urinary tract infection. VLDB: International Conference on Very Large Data Bases.

### Assumptions (how ambiguities in the brief were resolved)

1. **Inclusion test.** A study counts as *direct* evidence on a dimension when it varies that dimension and states, or visibly arranges, that the other dimensions are held fixed (same architecture, data, budget or checkpoint). A study that compares whole models, or that changes several factors at once, counts at most as *indirect* evidence. Each row states what was held fixed and what was varied, quoting the paper.
2. **Phase-1 labels revised from full text.** Labels assigned at screening were re-checked against the full text. Where a paper did not hold fixed what screening assumed, it was moved down, either to the indirect band (rows 35 to 40) or to the one-line list (section 2b). Each such move is stated in the row or the list.
3. **Causal relevance.** *Transfers to causal estimation* is split into the authors' own claim (quoted) and our judgement (unquoted, marked as ours).
4. **Seeds.** The two named seeds were identified as arXiv preprints. *Curriculum Matters* was identified as arXiv:2607.29120v1. The predecessor of the Shaheen seed (arXiv:2511.09665v1) was used for citation chasing. It is listed in section 2b.
5. **Figures only.** Results shown only in figures are described in words from the authors' text and marked as figure-only. No numbers were read off plots.
6. **Compute.** Purely compute-motivated studies (throughput, latency, memory) were excluded under shared rule 4.
7. **Page numbers** are PDF page numbers from pdftotext form-feed counts. For the AMIA paper, printed page = PDF page + 603. CURE (PMC XML) is cited by section heading.

### Access limitations

- **Semantic Scholar** answered the citation queries, with retries after HTTP 429.
- **Google Scholar** cannot be queried automatically. The OpenReview API and forum pages are blocked (browser verification). The neurips.cc listings were readable.
- **Publishers:** ahajournals.org (Stroke), Springer and siim.org are refused by the proxy. The PMC PDF for the AMIA paper returned an HTML page.
- **User-supplied PDFs (read in full):** Kurmann et al. 2026 (Stroke), Huang et al. 2025 (MICCAI), Zhu et al. 2026 (AMIA), and Vision-TabPFN. The Vision-TabPFN file is the **anonymised NeurIPS 2026 submission**, not the camera-ready paper; its authorship is taken from the neurips.cc listing, not from the PDF. The text of each supplied PDF was checked to be identical to my own pdftotext extraction.
- **Not supplied:** a SIIM 2025 abstract (section 4, N74).
- **Code repositories** (github.com blocked) and **supplementary files** were not opened unless stated.

---

## 1. Search log

All searches were run on 4 November 2026, with a date window of 2019 to November 2026.
- *Hits* = records returned. Where a source capped the list, the number listed is in brackets.
- *Screened* = titles read, plus abstracts where plausibly in scope.
- *Included* = papers that entered the included set, counted at the first route that found them.

Raw outputs, the full query strings and the per-route detail are in the scratchpad file `brief6/search_log.md`.

### 1a. Seeds

| # | Source | Step | Result |
|---|---|---|---|
| S0a | arXiv API | `ti:"surprising generalization" AND ti:tabular`; `au:Shaheen AND all:tabular` | Shaheen, Ma, Labach, Hutter, Thomas, Caterini, arXiv:2608.17957v1 (18 Aug 2026; only version). The arXiv comment says it extends arXiv:2511.09665. The neurips.cc listing (poster 150354) shows it as a NeurIPS 2026 poster. |
| S0b | arXiv API | `id_list=2609.06912` | Zhao, Thompson, Steinberg, Rahman, Bonilla, Ong, arXiv:2609.06912v1 (7 Sep 2026; only version), preprint. |
| S0c | arXiv API | `id_list=2607.29120` | Abolhasani and Ganapathy, arXiv:2607.29120v1 (31 Jul 2026). Accepted at the VLDB 2026 TaDA workshop. |

### 1b. Citation chasing

| # | Source | Step | Hits | Screened | Included |
|---|---|---|---|---|---|
| F1 | Semantic Scholar | Papers citing Shaheen et al. | 4 | 4 | 1 (TabDPT-Turbo); Zhao seed also cites it; 2 excluded |
| F2 | Semantic Scholar | Papers citing Zhao et al. | 2 | 2 | 1 (Hülskamp et al.); 1 excluded (arXiv:2601.21731, mechanistic) |
| F3 | Semantic Scholar | Papers citing the Shaheen predecessor (arXiv:2511.09665) | 4 | 4 | 0 new |
| F4 | Semantic Scholar | Papers citing *Curriculum Matters* | 1 | 1 | 1 (graph relational PFN curriculum) |
| F5 | arXiv full-text grep (fallback) | All 177 arXiv papers on TFMs/PFNs submitted 18 Aug to 5 Nov 2026, downloaded and grepped for each seed's ID and title | 177 | 177 | 0 new; confirmed F1, F2 and F4 |
| F6 | arXiv full text | Manual check of two Semantic Scholar items outside the F5 date filter | 2 | 2 | Both citations confirmed in the reference lists |
| F7 | WebSearch | Seed titles in quotes; Shaheen et al. "cited" | 28 | 28 | 0 |
| B1 to B3 | Semantic Scholar plus PDF | Backward references of the three seeds (35, 25 and 0 items; the *Curriculum Matters* list was read from its PDF) | 60 + 13 | 73 | counted under the dimension searches |

**Completeness of the citing sets.**
- *Shaheen et al.:* 4 citing papers. Semantic Scholar and the full-text grep agree; TabDPT-Turbo v2 was found by Semantic Scholar only, because its first version predates the seed.
- *Zhao et al.:* 2 citing papers (arXiv:2601.21731v4 was found by Semantic Scholar only, for the same reason).
- *What would be missed:* the grep covers every arXiv paper since the seed dates whose abstract names TFMs, TabPFN or PFNs. It would miss papers outside arXiv, arXiv papers using none of these terms, revised versions of older papers, and anything indexed only by Google Scholar.
- *Judgement:* close to complete for arXiv papers on TFMs; unknown otherwise.

### 1c. Dimension searches (arXiv API)

`TF` = `(abs:"tabular foundation model(s)" OR abs:TabPFN OR abs:"prior-data fitted" OR abs:"prior-fitted network(s)" [OR abs:"tabular in-context"])`.

| # | Dimension | Query (abridged) | Hits [listed] | Screened | Included (new) |
|---|---|---|---|---|---|
| A1 | ablations | `TF AND (abs:ablation OR …) AND (abs:pretraining OR abs:pre-training OR abs:prior)` | 15 | 15 | 6 |
| A2 | curriculum | `TF AND abs:curriculum` | 4 | 4 | 2 |
| A3 | real data / continued pre-training | `TF AND (abs:"real data" OR abs:"continued pre-training" OR …)` | 31 | 31 | 6 |
| A4 | scale | `TF AND (abs:"scaling law(s)" OR abs:scaling) AND (…)` | 116 [100] | 100 | 7 |
| A5 | architecture | `TF AND (abs:architecture OR abs:attention) AND (abs:ablation OR abs:"held fixed" OR …)` | 77 [60] | 60 | 7 |
| A6 | objective | `TF AND (abs:objective OR abs:"self-supervised" OR abs:"loss function" OR …)` | 49 | 49 | 2 |
| A7 | context / retrieval | `TF AND (abs:retrieval OR abs:"context length" OR abs:"nearest neighbors" OR …)` | 50 | 50 | 7 |
| A8 | fine-tuning versus ICL | `TF AND (abs:"fine-tuning" OR …) AND (abs:"in-context" OR abs:"zero-shot")` | 60 [50] | 50 | 5 |
| A9 | prior / scale / curriculum (titles) | `(ti:tabular OR ti:PFN …) AND (ti:scaling OR ti:prior OR ti:curriculum …) AND (…)` | 61 | 61 | 6 |
| A10 to A12 | image few-shot; length generalisation; prior design | (see scratchpad log) | 2; 4; 230 [40] | 46 | 0 |
| C1 to C4 | causal PFNs | `(abs:"prior-data fitted" OR abs:"causal foundation model" OR …) AND (abs:"treatment effect" OR abs:CATE OR …)`; title search; ablation filter | 506 [150]; 31; 334 [149]; 23 | 353 | 26 causal candidates |
| I1 to I5 | image latents, brain, stroke | `TF AND (abs:image OR abs:MRI OR abs:pathology …) AND (abs:embedding OR abs:latent …)` and variants | 20; 3; 2; 5; 666 [60] | 90 | 14 |
| FC | forward pool re-screened by topic | 177 titles from F5 | 177 | 177 | counted above |
| AB | arXiv `id_list` | abstracts of 160 candidates | 160 | 160 | – |

### 1d. PubMed (E-utilities, 2019 to 2026)

| # | Query (abridged) | Hits | Screened | Included |
|---|---|---|---|---|
| P1 | `(TabPFN OR "tabular foundation model(s)" OR "prior-data fitted" OR "in-context learning")[tiab] AND (stroke OR thrombectomy)[tiab]` | 8 | 8 | 1 (Kurmann et al.) |
| P2 | `(… OR "causal foundation model")[tiab] AND ("treatment effect(s)" OR individualized OR counterfactual …)[tiab]` | 11 | 11 | 0 new |
| P3 | `(…)[tiab] AND ("electronic health record(s)" OR EHR OR "primary care" OR claims OR registry)[tiab]` | 30 | 30 | 1 (Zhu et al., AMIA) |
| P4 | `(…)[tiab] AND ("deep features" OR embeddings OR latent OR autoencoder …)[tiab]` | 11 | 11 | 1 (Patil et al.) |
| P5 | `(…)[tiab] AND (MRI OR "computed tomography" OR imaging OR histopathology …)[tiab] AND (…)` | 22 | 22 | 1 (Huang et al., MICCAI) |
| P6 | `(…)[tiab] AND ("fine-tuning" OR "continued pre-training" OR pretraining OR ablation)[tiab]` | 25 | 25 | 1 (Gozeten et al.) |
| P7 | `CURE[ti] AND "treatment effect"[ti] AND pre-training` | 1 | 1 | 1 (CURE) |

### 1e. Web searches (discovery only)

Ten searches (W1 to W10) on stroke individual effects, TFMs on image embeddings, EHR retrieval, Vision-TabPFN, scaling laws, CURE, TabPFN CATE in EHR, TabPFN in thrombectomy, OpenReview prior ablations, and causal PFN fine-tuning. Together they returned 100 results, all screened. They added Vision-TabPFN and CURE.

### 1f. Totals

| Quantity | n |
|---|---|
| Unique titles screened | about 1,000 (754 arXiv IDs; 35 further Semantic Scholar items; 85 PubMed records; web results) |
| Abstracts read | 176 |
| Included | 99 (97 at phase 1, plus 2 screened candidates omitted from the phase-1 table by error and added in phase 3: rows 34 and 40) |
| Extracted in full (section 2a) | 40, plus the 2 user-supplied one-line papers (Huang et al.; Zhu et al.), also extracted in full |
| One-line list (section 2b) | 59 (57 listed plus 2 compact rows, S1 and S2) |
| Excluded near-misses (section 4) | 74 (73 excluded after screening plus 1 not screened) |

**Not searched separately:**
- Google Scholar: no automated access.
- OpenReview: blocked.
- Proceedings of NeurIPS, ICML, ICLR, AISTATS, CLeaR and UAI: covered through arXiv, since TFM papers in these venues are posted there; venues were read from arXiv comments and from neurips.cc.

---
## 2. Evidence table

### 2a. Rows extracted from full text (ranked)

The rows fall into five bands:
- **Band 0** (rows 1 and 2): seeds with direct ablations.
- **Band A** (rows 3 to 11): causal PFNs and pre-trained causal models with a controlled ablation.
- **Band B** (rows 12 to 27): direct ablations on general TFMs.
- **Band C** (rows 28 to 34): EHR, stroke and image-latent applications.
- **Band D** (rows 35 to 40): indirect evidence, or papers whose design did not isolate a dimension.

Each row has exactly the fields of the brief. Every extracted claim carries a page (or section) and a verbatim quote of under 25 words. Text marked UNVERIFIED could not be checked against the source. Null and negative results are reported inside the *Main result* field.

#### Band 0: seeds

#### Row 1. Abolhasani and Ganapathy 2026, *Curriculum Matters: Data-Efficient Relational PFN Pretraining with Synthetic Data* (seed)
<!-- SRC: texts/2607.29120v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2607.29120v1. Workshop paper (peer review not described). |
| Venue and version | arXiv v1, 31 Jul 2026, read in full. VLDB 2026 workshop on Tabular Data Analysis (p.1: "Tabular Data Analysis (TaDA).") |
| Dimension studied | Curriculum: the order in which synthetic tables are shown. Secondary: substituting the generator (PluRel for RDB-PFN's own prior), and single-table versus relational pre-training. |
| What was held fixed | Architecture and code (p.2: "training code, modifying only the synthetic data source."). For the main contrast (p.3: "Identical data, identical optimizer, identical compute budget"). Model of 0.7M parameters (p.3: "0.7M-parameter PFN"); every table has 150 rows (p.2: "All tables contain 150 rows."). |
| What was varied | A width-progressive curriculum from 7 to 17 columns (p.2: "3,300 tables with 7 columns (denoted TF07)"), versus the same corpus with no ordering (p.2: "exactly the same TF07-TF17 PluRel corpus but mixed into a sin-"). Relational families vary the single-table warm-up and the relational ordering. |
| Evaluation (benchmarks, held-out families) | Single-table evaluation on 23 Grinsztajn classification tasks (p.2: "uses 23 classification tasks from the Grinsztajn et al. [1] benchmark;"). Relational evaluation on RelBench and 4DBInfer (p.2: "19 tasks from RelBench [10] and 4DBIn-"). ROC-AUC at context 64 and 1024. Evaluation tables are real data, disjoint from the synthetic pre-training. |
| Main result with numbers | **Curriculum:** 0.703 average ROC-AUC with the curriculum, against all-at-once training on the same data (p.3: "only 0.541, a 16.2-point absolute gap below the curriculum’s 0.703."). **Relational:** relational curriculum from scratch 0.638; all-at-once relational training after warm-up 0.620; all-at-once without warm-up 0.596 (Table 4, p.4). **Null and negative:** dedicated relational data adds little over the single-table model (p.3: "Family D: single-table model 0 0.605 0.631"). **Caveats:** no seeds or intervals reported. RDB-PFN comparisons use its *reported* numbers (p.3: "88% of RDB-PFN’s reported 0.725"). The optimiser and steps per stage are not given (p.2: "hyperparameters follow the original paper"). UNVERIFIED: run-to-run variance. |
| Transfers to causal estimation: authors' claim | No causal claim. For relational PFNs (p.4: "curriculum ordering is the domi-") nant training-recipe variable. |
| Transfers to causal estimation: our judgement | A clean single-factor test, and directly testable for a causal PFN, for example a curriculum over covariate count to reach about 540 EHR covariates. The effect size comes from one run of a 0.7M-parameter model on 150-row tables, so it may not hold at CausalPFN or TabICL scale. |

#### Row 2. Shaheen, Ma, Labach, Hutter, Thomas, Caterini 2026, *Understanding the Surprising Generalization Properties of Tabular Foundation Models* (seed)
<!-- SRC: texts/2608.17957v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2608.17957v1. Peer reviewed (NeurIPS 2026 poster per neurips.cc); arXiv v1 read because the proceedings are not yet out. |
| Venue and version | arXiv v1, 18 Aug 2026 (only version); sections 1 to 6 read. Extends arXiv:2511.09665v1. |
| Dimension studied | Real-data pre-training: one table versus many, and which tables. Number of pre-training tasks. Corpus curation (deduplication, filtering, column-level pre-processing). Training context length and model size, each with and without pre-processing. |
| What was held fixed | Architecture and procedure (p.2: "we fix both the model architecture and the pre-training procedure throughout"). No retrieval during pre-training (p.2: "we choose not to use retrieval mechanisms (as used in TabDPT) during pre-training"). Corpus variants (p.5: "individually by training a separate model for every combination"). |
| What was varied | 88 single training tables, each training its own model. The number of tasks drawn from a table (p.4: "we vary the number of tasks the model is allowed to pre-train on"). Corpus: full (1,732 tables), deduplicated (1,535) or at least 30 features (607). Column operations. Context lengths of 1k, 2k and 4k. |
| Evaluation (benchmarks, held-out families) | CC-18 (72 classification datasets) and CTR-23 (35 regression); TabArena (51 tasks) for the scaled models. Evaluation sets are excluded from pre-training (p.5: "excluding datasets from the CC-18, CTR-23, and TabArena"). Metric: IQM with 95% CI. |
| Main result with numbers | **Table quality:** a meta-model of table properties (p.3: "achieves an R2 of 0.67"). Feature count dominates (p.4: "as by far the strongest predictor of downstream transfer performance"); instance count (p.4: "shows negligible predictive power"). **Task count:** (p.4: "increasing the number of tasks from 5 to tens of thousands drives the performance from"; "barely above random (AUC = 0.5) to good"). **Corpus (Table 1, p.6):** average score 0.9039 for the baseline, 0.9038 deduplicated, 0.8927 filtered, 0.9097 for the best column-level setting. **Scaled models:** (p.6: "on 67% of tasks, 2k+pp beats 2k on 61%, and 1k+pp beats 1k on 63%"). **Null:** deduplication (p.5: "statistically indistinguishable on CC-18 and CTR-23"); no within-domain advantage (p.3: "within-domain generalization is not higher"). **Limits:** only real-data training (p.10: "extend to scenarios in which models are trained exclusively on synthetic data") and only row attention (p.10: "our results only used row-based attention following TabDPT and TabPFNv1"). UNVERIFIED: tied query-key results (figure only). |
| Transfers to causal estimation: authors' claim | No causal claim. Their mechanism (p.7: "is a sufficient explanation for these models’ capabilities") is learned retrieval, while conceding (p.7: "could be occurring in models trained with broader distributions") approximate Bayesian inference. |
| Transfers to causal estimation: our judgement | Testable for causal PFNs: vary the number of distinct covariate-treatment-outcome structures at fixed data volume. If generalisation is retrieval, effect estimates depend on finding similar patients in context, which matters for 56,000 EHR patients and a context of 2k to 4k. Evidence is from real-data SSL training, not causal priors. |

#### Band A: causal PFNs and pre-trained causal models with a controlled ablation

#### Row 3. Zhang 2026, *Learning to Fluctuate: Statistical Foundations for Causal Tabular Pretraining* (FSP)
<!-- SRC: texts/2609.26290v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.26290v2. Preprint (single author). |
| Venue and version | arXiv v2, 24 Sep 2026. Abstract, introduction and section 4 read; appendix N protocol lines checked. |
| Dimension studied | Training objective of a causal PFN: supervision by the latent mechanism effect θ(P) versus ATE plus its efficient influence-function fluctuation, mixed by λ. |
| What was held fixed | (p.9: "with the same architecture, M = 32768 training tables, optimizer and five seeds."). For the λ sweep (p.9: "Holding generator, network, optimizer and budget fixed, the seven-point λ"). Appendix (p.35: "The matched raw pair changes only supervision."). |
| What was varied | Supervision target (λ from 0 to 1; FSP versus latent-effect labels); input format (Summary versus Raw). |
| Evaluation (benchmarks, held-out families) | Synthetic deployment tables (mechanism × context-length cells), effect-shift settings and weak overlap. Real randomised data: National Supported Work and a turnout trial. Comparators: CausalPFN-S checkpoint, S/T/X/DR learners, AIPW/DML and Do-PFN. Target: ATE, not CATE. |
| Main result with numbers | **λ sweep:** response coefficient (p.9: "from 0.105 to 0.895"); label defect (p.9: "8.72-fold") lower. **Effect shift:** (p.9: "FSP lowering shifted RMSE by 54.2% and teacher defect by 99.0%"). **Against CausalPFN-S:** (p.9: "Summary FSP lowers both RMSE (10–13%)"). **Null and negative:** (p.9: "S-learner has lower point RMSE than FSP") at the typical mechanism. Latent-effect supervision wins near the prior centre (p.9: "shrinkage improves point risk near the prior center but attenuates shifted effects"). Weak-overlap coverage (p.9: "native/oracle-V coverage was .706/.998"). Real trials (p.9: "lower ensemble RMSE coexisted with residual attenuation"). UNVERIFIED: covariate dimension of the mechanisms; network size. |
| Transfers to causal estimation: authors' claim | Latent-effect supervision, used by existing causal PFNs, rewards shrinkage (p.1: "shrinkage"), whereas FSP targets the repeated-sample response. |
| Transfers to causal estimation: our judgement | The cleanest objective ablation found on a causal PFN. Its warning applies to both applications: a prior centred near zero effect attenuates large effects. Shown for ATE in low-dimensional mechanisms only; CATE with 540 covariates is untested. |

#### Row 4. Sextro, Kłos, Dernbach 2026, *MapPFN: Learning Causal Perturbation Maps in Context*
<!-- SRC: texts/2601.21092v4.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2601.21092v4. Peer reviewed (NeurIPS 2026 per the arXiv comment). |
| Venue and version | arXiv v4, 26 Oct 2026. Section 7 and Table 4 read. |
| Dimension studied | Synthetic pre-training versus training from scratch on real data; fine-tuning versus in-context use; prior design (counterfactually paired data); context content (interventional data). |
| What was held fixed | Architecture (p.8: "Random init trains the same architecture from scratch on real data, without"); for the context ablation (p.7: "model architecture remains unchanged"). |
| What was varied | Pre-trained only, pre-trained then fine-tuned, random initialisation on real data; without the paired prior; without interventional context. |
| Evaluation (benchmarks, held-out families) | Single-cell perturbation data (melanoma and leukaemia), (p.8: "Mean ± std over five data splits, each averaged over ten resampling seeds."). Targets are post-intervention gene-expression distributions, not CATE. |
| Main result with numbers | **Melanoma (Table 4, p.8), RMSE:** pre-trained 0.32 ± 0.04, fine-tuned 0.09 ± 0.01, random init 0.31 ± 0.02. **AUPRC:** 0.34, 0.62 and 0.09. Without the paired prior, RMSE 0.94; without interventional context, 0.65. The authors (p.7: "Random initialization performs worse on all metrics") than fine-tuned MapPFN. **Null:** without fine-tuning, pre-training gives no gain over random init on RMSE (0.32 versus 0.31). **Out of prior:** leukaemia overshoot (p.7: "distributional metrics degrade and MR indicates an overshoot of the ground-truth effect"). UNVERIFIED: architecture ablation in appendix E.3. |
| Transfers to causal estimation: authors' claim | (p.7: "prediction on diverse synthetic causal mechanisms improves performance") |
| Transfers to causal estimation: our judgement | A controlled test of pre-training plus real-data fine-tuning against real-only training, the design needed to justify fine-tuning a causal PFN on EHR-derived semi-synthetic data. Domain and estimand are far from CATE, and the leukaemia overshoot is an out-of-prior warning. |

#### Row 5. Thumm and Chen 2026, *Market Impact Estimation via Causal Foundation Models*
<!-- SRC: texts/2610.12537v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.12537v1. Peer reviewed (ICAIF '26 per the arXiv comment). |
| Venue and version | arXiv v1, 8 Oct 2026, read in full (8 pages). |
| Dimension studied | Inputs and architecture: the intervention (do) inputs removed, in a "do-ablated twin". Encoding of the intervention. Backbone (transformer versus recurrent state-space). Training recipe. |
| What was held fixed | For the twin (p.4: "the identical architecture, training prior, and train-"; "ing seed with the five do-information inputs (target, kind, value,"). Model (p.4: "eters, 5,000 steps"). |
| What was varied | Do-inputs present or zeroed; backbone and recipe. The authors note the two backbones (p.3: "differ in training recipe as well as architecture") and test the recipe separately. |
| Evaluation (benchmarks, held-out families) | Synthetic suites (p.4: "of 500 episodes at each pinned 𝛾"), where γ is confounding strength. Zero-shot transfer to a limit-order-book simulator and to real crypto and equity flows (no counterfactual ground truth). |
| Main result with numbers | **Twin:** the PFN (p.1: "tracks the unbiased true-") parameter oracle, while the twin (p.1: "collapses onto the") pre-window mean. **Recurrent variant bias:** (p.3: "+0.16 [0.09, 0.23] at 𝛾=0 rising to +0.52 [0.38, 0.66]"), against the transformer's (p.3: "+0.16 [0.05, 0.28]"). **Recipe test:** a transformer (p.3: "retrained with the recurrent pair’s recipe reaches +0.80"). **Negative:** real-data evidence is (p.1: "consistent with, though not proof of, causal transfer"). UNVERIFIED: transformer seed protocol. |
| Transfers to causal estimation: authors' claim | Transfer depends on encoding (p.1: "the metaorder as added flow rather than a clamped price level, not") on more training. |
| Transfers to causal estimation: our judgement | A well-controlled single-factor input ablation on a causal PFN, with the recipe confound tested. For binary-treatment CATE the transferable lesson is that treatment encoding and recipe can matter more than the backbone. |

#### Row 6. Reuter, Dhir, Diaconu, Robertson et al. 2026, *Use What You Know: Causal Foundation Models with Partial Graphs*
<!-- SRC: texts/2602.14972v3.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2602.14972v3. Peer reviewed (ICML 2026, arXiv journal reference). |
| Venue and version | arXiv v3, 27 Sep 2026. Sections 4 and 5 read. |
| Dimension studied | Architecture: how graph or ancestor knowledge enters a causal PFN (soft attention bias, hard mask, graph-convolutional adapter, combinations). |
| What was held fixed | Training: the baseline (p.8: "baseline that does not support graph conditioning but is otherwise trained identically"); (p.23: "We implement the baseline with an identical architecture compared to the graph-conditioning methods"). |
| What was varied | Conditioning mechanism; adjacency versus ancestor matrix. |
| Evaluation (benchmarks, held-out families) | Held-out synthetic tasks from the priors. NLL, MSE and R² relative to the baseline, with (p.7: "95-percent bootstrap confidence") intervals for the median. |
| Main result with numbers | Figure only. (p.7: "graph-conditioned variants outperform the baseline"); soft attention, alone or with the adapter, (p.7: "consistently outperform both Hard Attention and the GCN-") only variants. **Null-leaning:** (p.7: "it is small in absolute terms across all metrics"). UNVERIFIED: appendix H.1 numbers. |
| Transfers to causal estimation: authors' claim | Soft biases plus a graph encoder are (p.2: "an effective and robust mechanism to enable the") use of partial ancestral information. |
| Transfers to causal estimation: our judgement | A controlled architecture test in a causal PFN, relevant to injecting known confounder roles for EHR. Gains are small and shown only on synthetic priors. |

#### Row 7. Stith, Barath, Balazadeh, Cresswell et al. 2026, *Causal Foundation Models with Continuous Treatments* (CCPFN)
<!-- SRC: texts/2605.15133v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2605.15133v2. Preprint (p.1: "Preprint."). |
| Venue and version | arXiv v2, 13 Jul 2026. Sections 3 to 6 and appendix D read. |
| Dimension studied | Training objective (loss); prior design choices. |
| What was held fixed | Other design choices at their defaults within each ablation table. Steps and seeds for the ablation runs are not stated (UNVERIFIED). |
| What was varied | A histogram cross-entropy loss (p.4: "L = 1024 bins from [−10, 10] (after z-standardization)") versus (p.20: "continuous ranked probability score"). A single versus three-MLP prior (p.20: "a simplified prior design that uses a single MLP"). Corruption during versus after generation. Positivity enforced or not. |
| Evaluation (benchmarks, held-out families) | Six semi-synthetic continuous-treatment benchmarks (MVICU, Debt, Warfarin, TCGA, News, NewsHet). MISE and dosage policy error with (p.9: "with 5-fold cross-validation"). No benchmark data in pre-training (p.8: "the model does not see any evaluation data during pre-training"). |
| Main result with numbers | **Loss (Table 7, p.20):** Debt MISE 2.22 for cross-entropy versus 3.06 for CRPS; CRPS (p.20: "on TCGA, but otherwise is not as effective"). **Positivity (Table 5, p.11):** Debt MISE 2.22 versus 9.98 without it. **Mixed:** the 1-MLP prior wins on Warfarin (27.2 versus 36.6) and TCGA (4.23 versus 8.63). **Weak on policy error:** CCPFN ranks 6.0 on dosage policy error (Table 3, p.9). **Inconsistency:** the ablation-table Warfarin MISE (36.6, p.20) differs from main Table 2 (40.4 ± 5.7, p.9), and the ablations give no SD. |
| Transfers to causal estimation: authors' claim | The 3-MLP prior and the histogram loss are the better choices. Limited by (p.10: "the lack of broad, large-scale causal evaluation datasets for the continuous"). |
| Transfers to causal estimation: our judgement | A single-factor loss ablation in a causal PFN that mildly favours the binned cross-entropy loss. Benchmark-dependent, unreplicated, and for continuous treatments; indirect for binary-treatment CATE. |

#### Row 8. Balazadeh, Kamkari, Thomas, Li et al. 2025, *CausalPFN: Amortized Causal Effect Estimation via In-Context Learning*
<!-- SRC: texts/2506.07918v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2506.07918v2. NeurIPS 2025 per Semantic Scholar; venue UNVERIFIED in the text read. |
| Venue and version | arXiv v2, 27 Oct 2025. Section 5, appendices D.1 to D.3 and Table 3 read. |
| Dimension studied | Continued pre-training of a predictive TFM on a causal prior (TabPFN versus TabPFN⋆). Staged training (not ablated). Context size and covariate dimension at inference. Retrieval for long tables. |
| What was held fixed | For TabPFN versus TabPFN⋆, the same TabPFN model, with fine-tuning on the causal prior added (p.9: "isolate the benefit of training on a causal prior, compared to the predictive non-identifiable prior in"). The size sweeps use one trained CausalPFN (p.34: "mean ± standard error over 50 datasets drawn from"). |
| What was varied | Causal-prior fine-tuning of TabPFN; rows (10 to 10,000); covariates (1 to 1,000). Training is staged (p.33: "trained in two stages: (i) a predictive") with a context of (p.33: "16K in the first phase and 2,048 in the second"). |
| Evaluation (benchmarks, held-out families) | IHDP, ACIC 2016, Lalonde CPS and PSID (Table 3). Size and dimension sweeps are *in-prior* (polynomial prior). |
| Main result with numbers | **Table 3 (p.10), PEHE on IHDP:** TabPFN 0.95 ± 0.20, TabPFN⋆ 0.90 ± 0.16, CausalPFN 0.58 ± 0.07. **ACIC 2016:** TabPFN⋆ 0.47 ± 0.05 beats CausalPFN 0.92 ± 0.11. **Lalonde PSID ATE relative error:** 0.60 to 0.22 with causal fine-tuning. **Rows (Table 4, p.34):** PEHE 1.34 at 10 rows to 0.29 at 5,000, then (p.34: "a slight plateau at very large contexts"). **Covariates (Table 5, p.34):** 0.08 at 1, 1.01 at 100, 1.28 at 500, 1.32 at 1,000, against 1.30 to 1.33 for meta-learners. **Negative:** (p.34: "covariates grows—likely due to training exposure being limited to up to 100 dimensions"). |
| Transfers to causal estimation: authors' claim | (p.9: "the performance and confirms the added value of identifiable priors for causal effect estimation.") |
| Transfers to causal estimation: our judgement | Only TabPFN versus TabPFN⋆ isolates a pre-training dimension, and its gain is modest except on Lalonde PSID. The dimension result is the most important finding for the EHR application: with about 540 covariates, a model trained up to 100 dimensions loses its advantage, so wider training (row 21) or reduction is needed. |

#### Row 9. Thumm, Wiedemann, Chen 2026, *Towards Continuous-time Causal Foundation Models*
<!-- SRC: texts/2605.28880v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2605.28880v1. Workshop paper (p.1: "Structured Data (FMSD), Seoul, South Korea. Non-archival."). |
| Venue and version | arXiv v1, 26 May 2026. Sections 3 to 5 read. |
| Dimension studied | Architecture (time encoder: positional versus time-aware) crossed with prior simulation (naive versus fine-grid SDE integration). |
| What was held fixed | (p.4: "baseline, enabling a controlled ablation."). Training (p.4: "(10 k steps, single seed)"). |
| What was varied | A 2 × 2 grid of encoder × integrator, on a linear Ornstein-Uhlenbeck prior and a neural-drift prior. |
| Evaluation (benchmarks, held-out families) | In-prior held-out evaluations (p.4: "from the same prior; multi-seed replication is future work."). Regular and mixed observation schedules. |
| Main result with numbers | **OU, regular:** naive 0.3714 / 0.3641 versus fine 0.3578 / 0.3575 (Table 1, p.4). (p.4: "every cell (4/4)"). **Encoder:** (p.4: "integration the encoder choice is empirically inert"). **Mixed schedule:** (p.4: "+0.0018 → +0.0057 on OU, +0.0048 → +0.0088 on") neural drift. **Caveats:** (p.4: "multi-seed replication is needed to harden the cross-prior"); pharmacokinetic transfer (p.8: "the naive baseline is hard to beat on RMSE"). |
| Transfers to causal estimation: authors' claim | Fine-grid integration (p.4: "produces models that transfer") better. |
| Transfers to causal estimation: our judgement | Controlled, but single-seed, in-prior and with tiny effects. Suggests architecture choices can be inert once the prior is simulated correctly, which bears on future time-to-event work. |

#### Row 10. Liu, Wu, Zhang 2024, *KG-TREAT: Pre-training for Treatment Effect Estimation by Synergizing Patient Data with Knowledge Graphs*
<!-- SRC: texts/2403.03791v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2403.03791v1. Peer reviewed (AAAI 2024 per the arXiv comment). Not a PFN: pre-train then fine-tune. |
| Venue and version | arXiv v1, 6 Mar 2024. Setup and Tables 1 and 3 read. |
| Dimension studied | Pre-training versus training from scratch; knowledge-graph input; fusion architecture. |
| What was held fixed | Architecture (p.5: "w/o pre-train: directly trained on the downstream pa-"; "tient data and KGs using the same model architecture as"). (p.6: "The results are averaged over 20 random runs."). |
| What was varied | Pre-training removed; knowledge graphs removed; both removed; fusion module replaced. |
| Evaluation (benchmarks, held-out families) | MarketScan claims, coronary artery disease, four drug comparisons emulating RCTs. IF-PEHE, an effect proxy with no ground truth. |
| Main result with numbers | **IF-PEHE (Table 1, p.6), full / without pre-training / without both:** 0.171 / 0.231 / 0.239 (rivaroxaban vs aspirin); 0.149 / 0.189 / 0.198; 0.160 / 0.200 / 0.213; 0.191 / 0.241 / 0.247. **Caveats:** no SD shown; proxy metric. |
| Transfers to causal estimation: authors' claim | Removing pre-training costs more than removing the knowledge graphs (p.5: "mance decline in the w/o pre-train scenario compared to"). |
| Transfers to causal estimation: our judgement | A same-architecture pre-training ablation on claims data with an effect proxy; directionally supports pre-training on routinely collected records. Not a PFN, and the uncertainty is unknown. |

#### Row 11. Liu, Chen, Zhang 2024, *CURE: A deep learning framework pre-trained on large-scale patient data for treatment effect estimation*
<!-- SRC: texts/cure_PMC11240182.txt -->
| Field | Content |
|---|---|
| Paper | https://doi.org/10.1016/j.patter.2024.100973. Peer reviewed (Patterns 5(6):100973). Not a PFN. |
| Venue and version | Version of record in PMC (PMC11240182), read from the XML. Cited by section. |
| Dimension studied | Pre-training versus none; pre-training data volume; fine-tuning data volume; embedding design. |
| What was held fixed | Architecture (§Baselines: "Base Model directly trains on the downstream datasets using the same architecture as CURE."). Data-size curves are averaged (§Effect of pre-training data size: "(average of 20 runs)"). |
| What was varied | Fraction of pre-training data (0% = base model); fraction of labelled data; time and type embeddings. |
| Evaluation (benchmarks, held-out families) | Pre-training data (§Pre-training data: "we obtain 2,955,399 patient sequences for pre-training"), MarketScan 2012 to 2017. Four RCT emulations in coronary artery disease (§Downstream tasks: "we end up with 4 RCTs that meet all of the above criteria"). AUC/AUPR factual; IF-PEHE. |
| Main result with numbers | **CURE versus same-architecture base (Table 2; AUC, AUPR, IF-PEHE), rivaroxaban vs aspirin:** ("Base Model0.758±0.0290.406±0.0370.180±0.038") versus ("CURE0.803±0.0110.469±0.0230.173±0.038"). **Data size:** (§Effect of pre-training data size: "Generally, the performance improves with the increase of pre-train data."), shown for AUC only. **Null:** the IF-PEHE gain for rivaroxaban vs aspirin is within 1 SD, and the base model alone is already competitive (§Comparison: "even without pre-training, the base model of CURE attains a similar performance to the best baseline"). UNVERIFIED: values of the data-size curves (figures). |
| Transfers to causal estimation: authors' claim | (§Effect of pre-training data size: "pre-training is beneficial for downstream tasks by learning contextualized patient representations from large-scale unlabeled patient data") |
| Transfers to causal estimation: our judgement | The scale evidence concerns factual-outcome AUC, not effect accuracy. Relevant to EHR outcome and nuisance models, but it does not show that self-supervised pre-training improves heterogeneous-effect estimation. |

#### Band B: direct ablations on general TFMs

#### Row 12. Bouadi, Bouarour, Kulkarni, Dubey et al. 2026, *Shaping the Prior: How Synthetic Task Distributions Determine Tabular Foundation Model Quality* (O'Prior)
<!-- SRC: texts/2605.18971v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2605.18971v2. Preprint. Venue UNVERIFIED (a possibly related ICML 2026 listing has a different title). |
| Venue and version | arXiv v2, 23 Oct 2026. Sections 3.1 to 3.2.1 and Tables 1 and 2 read. |
| Dimension studied | Prior design and mixtures (generator components); curriculum over realism severity. |
| What was held fixed | (p.7: "the model architecture, optimizer, training budget, and evaluation pipeline fixed across all conditions and vary only"). Model nanoTabPFN. Budget (p.7: "40, 000 synthetic datasets per prior") and (p.7: "training, without hyperparameter tuning between conditions."). |
| What was varied | Three baseline generators (TabPFN v1, TabICL-v1, TabICL-v2) and nine variants: SCM diversity, hybrid SCM, moderate or strong realism, shift stress, and the full pipeline with curriculum. |
| Evaluation (benchmarks, held-out families) | (p.8: "52 tabular classification tasks in total"): TabArena v0.1 and OpenML-CC18. ROC-AUC, accuracy, F1. |
| Main result with numbers | **TabArena ROC-AUC (Table 2, p.8):** TabPFN prior 0.5758, TabICL-v2 prior 0.7910, hybrid SCM 0.8335, full curriculum pipeline 0.8194. **Mechanism diversity:** (p.9: "realism perturbations and no shift stress, accounts for the majority of the gap"). **Negative:** (p.10: "Curriculum is not a universally superior strategy; it is a schedule-dependent design choice."). **Caveats:** single runs, no intervals for Table 2. The curriculum arm also adds components, so curriculum is not isolated. Small model and budget. |
| Transfers to causal estimation: authors' claim | (p.9: "first-order determinant of model quality.") |
| Transfers to causal estimation: our judgement | Clean fixed-architecture evidence that mechanism diversity within tables drives transfer; testable for causal priors by mixing outcome-mechanism families. The curriculum conclusion is confounded. |

#### Row 13. Zhang, Maddix, Yin, Erickson et al. 2025, *Mitra: Mixed Synthetic Priors for Enhancing Tabular Foundation Models*
<!-- SRC: texts/2510.21204v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2510.21204v1. Peer reviewed (NeurIPS 2025 per the arXiv comment). |
| Venue and version | arXiv v1, 24 Oct 2025. Sections 3 to 4.7 and appendix C.3 read. |
| Dimension studied | Prior mixtures (which priors, with what weights); transfer of the mixture to a 1D-attention architecture. |
| What was held fixed | Architecture and training per row. (p.29: "We begin with ranking the performance of the model pretrained on data drawn from each prior"). For 1D (p.7: "when pretrained with the same mixture of priors, M ITRA 1D also outperforms"). |
| What was varied | Forward selection over SCM, extra-trees, gradient-boosting, decision-tree, random-forest and DSRF priors (p.8: "adding the best-performing prior at each step"); the SCM-to-tree mixing proportion. |
| Evaluation (benchmarks, held-out families) | (p.5: "66 TabRepo classification datasets, 75 TabZilla classification datasets, and 10 TabRepo") regression, plus AMLB. Elo with 95% CI. The ablation is on TabRepo, which is also an evaluation benchmark. |
| Main result with numbers | **Table 6 (p.9), Elo:** SCM 1000, SCM+ET 1063, SCM+ET+GB 1076, full mixture 1062; single tree priors 815 to 899. (p.9: "combining GSCM with every tree-based prior improves over either alone"). **Negative:** the full mixture does not beat the 3-prior mix; (p.9: "despite being the second-best stand-alone prior, GDSRF contributes") the least. **Caveat:** prior selection was tuned on an evaluation benchmark. |
| Transfers to causal estimation: authors' claim | The mixture is (p.7: "model-agnostic") |
| Transfers to causal estimation: our judgement | The best controlled evidence that complementary mechanism families help, which suggests mixing tree-like and SCM outcome models in a causal prior. Gains are optimistic because selection and evaluation are not separated. |

#### Row 14. Türkmen, Kaya, Pfefferle, Hutter 2026, *Towards Evaluating Data Priors for Tabular Foundation Models*
<!-- SRC: texts/2606.29241v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2606.29241v1. Workshop paper (p.1: "Proceedings of the 2 nd ICML Workshop on Foundation Models"). |
| Venue and version | arXiv v1, 28 Jun 2026. Sections 1 to 5 read. |
| Dimension studied | Prior design: 11 public priors compared under one architecture. Generation dimensions (features × samples). |
| What was held fixed | (p.2: "of training tasks used to train an identical nanoTabPFN"); (p.3: "we keep the model architecture fixed throughout."); (p.3: "we apply the same batch size"). |
| What was varied | The prior (TabPFN, TabICL, TabForest and TICL generators; real tables with default or random targets). Feature-sample settings (p.4: "(10, 200), (30, 200),"). |
| Evaluation (benchmarks, held-out families) | (p.3: "16 tasks") from TabArena v0.1 classification, three folds each. Duplicates against the evaluation pool are removed for the real-data priors. |
| Main result with numbers | **Table 1 (p.3), raw ROC-AUC / average rank:** tabicl mix scm 0.865 / 2.69; ticl 0.866 / 2.94; tabpfn mlp 0.852 / 6.00; real random targets 0.844 / 7.31; real default targets 0.781 / 10.19. **Caution:** (p.3: "observed differences should be interpreted"). **Dimensions:** (p.4: "of features while keeping the sample size fixed usually led") to worse performance; best at (10, 500). **Null:** (p.4: "No single prior was uniformly best"). UNVERIFIED: number of seeds. |
| Transfers to causal estimation: authors' claim | Data-level similarity is (p.4: "an informative but incom-") plete proxy for downstream similarity. |
| Transfers to causal estimation: our judgement | Matching the prior's feature-to-sample ratio to the target is testable: about 0.01 for EHR; latent dimension over 300 to 3,000 for trials. Agrees with row 2 that many targets per real table beat one fixed target. Small model, 16 tasks, no intervals. |

#### Row 15. Qu, Holzmüller, Varoquaux, Le Morvan 2026, *TabICLv2: A better, faster, scalable, and open tabular foundation model*
<!-- SRC: texts/2602.11139v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2602.11139v2. Peer reviewed (ICML 2026 per the arXiv comment). |
| Venue and version | arXiv v2, 16 Sep 2026. Sections 4 to 8 and the Figure 10 caption read. |
| Dimension studied | Architecture × prior interaction; individual architecture and pre-training components. |
| What was held fixed | (p.8: "ablation modifies one component of the reference model"); runs (p.8: "pretrained for 280K steps"). |
| What was varied | One component at a time. The new architecture on the old TabICL prior, and the old architecture on the new prior. |
| Evaluation (benchmarks, held-out families) | TALENT and TabArena (normalised accuracy, Elo, log-loss). |
| Main result with numbers | Figure only. (p.8: "Pretraining TabICLv2 with the TabICL prior fails"): (p.8: "the performance remains below TabICL and the"; "validation loss degrades in the second half of the pretraining."). The old architecture with the new prior (p.8: "has limited ability to exploit increased prior diversity."). (p.8: "The prior yields the largest effect."); three components give (p.8: "comparable, significant gains (≈100 Elo, 64% win") rate. **Limits:** (p.5: "An ablation using the TabPFNv2 prior is not possible, as it is"). UNVERIFIED: Elo values (figures). |
| Transfers to causal estimation: authors' claim | (p.8: "This suggests that the TabICLv2 architecture requires higher") prior diversity to generalise. |
| Transfers to causal estimation: our judgement | A larger architecture can fail on a narrower prior. Causal-PFN experiments should therefore co-vary architecture and prior, not tune them separately. |

#### Row 16. Zhao, Zhuang, Duan, Wang et al. 2026, *Architecture Alignment With Sparse Priors in Tabular Foundation Models*
<!-- SRC: texts/2609.36883v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.36883v1. Preprint. |
| Venue and version | arXiv v1, 29 Sep 2026. Sections 1 to 4 read. |
| Dimension studied | Architecture (row-token versus cell-token alternating-axis attention) × prior sparsity. |
| What was held fixed | (p.2: "streamlined row-token and cell-token alternating-axis transformers under identical priors and"); (p.5: "Both models use the same embedding width and similar parameter counts"); (p.6: "show the mean ± SD across three training seeds, each evaluated on 32,000 shared test tasks."). |
| What was varied | Architecture; prior sparsity k and dimension d. Separately, null features added to inputs of released models. |
| Evaluation (benchmarks, held-out families) | Controlled part: exact Bayes targets on synthetic sparse tasks. Observational part: Friedman tasks and OpenML regression with added null features. |
| Main result with numbers | (p.6: "has substantially lower excess error under sparse priors, with a gap of Erow,k − Ealternating,k ≈ 0.34 (respectively"; "≈ 0.627) at k = 1 and d = 10 (respectively d = 20)."). (p.6: "is positive for all three training seeds"); the gap becomes negligible for dense priors. **Observational:** TabDPT is (p.2: "more sensitive") to null features. **Limit:** (p.13: "replication across alternating-axis training seeds remain outside the present"). |
| Transfers to causal estimation: authors' claim | (p.2: "stronger inductive bias toward irrelevant-feature suppression than row-token architectures.") |
| Transfers to causal estimation: our judgement | Relevant to about 540 EHR covariates with few true effect modifiers. Testable in a causal PFN by varying the number of modifiers. Shown on synthetic linear tasks only. |

#### Row 17. Vaidhya, Sahu, Rish 2026, *Recurrent In-Context Learning for Tabular Foundation Models* (Tab-Loop)
<!-- SRC: texts/2610.14998v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.14998v1. Preprint. |
| Venue and version | arXiv v1, 10 Oct 2026. Abstract and sections 3 to 5 checked. |
| Dimension studied | Architecture: tied (looped) versus untied in-context blocks. |
| What was held fixed | (p.1: "4 tied blocks applied k times and changes nothing else: the encoders, decoder,"; "synthetic prior and training recipe are shared with an untied baseline trained for"). Matched pre-training and inference compute. |
| What was varied | 4 tied looped blocks versus 12 untied blocks; a parameter-matched 4-block untied control; number of loops. |
| Evaluation (benchmarks, held-out families) | Held-out prior tables; 200 TALENT datasets; 38 TabArena datasets. |
| Main result with numbers | (p.1: "held-out log loss is 0.4583 vs. 0.4588,"; "mean accuracy on 200 TALENT datasets is 84.10% vs. 83.92%, and Elo on 38"). The parameter-matched control trails both: (p.1: "both (83.46%; Elo 1343)"). **Caveat:** (p.7: "With one seed, we read this as equivalence, not superiority."). |
| Transfers to causal estimation: authors' claim | (p.1: "the ICL stage of a tabular foundation model needs depth more than it") needs distinct parameters. |
| Transfers to causal estimation: our judgement | A single-factor architecture result, directly testable in a causal PFN for parameter savings. One seed; predictive tasks only. |

#### Row 18. Schnurr, Sarnthein, Hofmann, Schlag 2026, *Adapting Linear-Time Architectures for Tabular In-Context Learning*
<!-- SRC: texts/2609.36337v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.36337v1. Preprint (p.6: "Preprint"). |
| Venue and version | arXiv v1, 28 Sep 2026. Sections 3 to 6 and Tables 2 and 3 read. |
| Dimension studied | Architecture (sequence mixer; causal versus non-causal); training setup; context-length generalisation. |
| What was held fixed | (p.1: "We perform a controlled study to disentangle training design,"). Size-matched controlled backbones with shared pre-training hyperparameters (Tables 5 and 6, p.17). Released baselines are (p.6: "not matched in parameter count"). |
| What was varied | Softmax, linear attention, gated linear attention, DeltaNet, Mamba-2; final-state readout; a write-rate decay; test context size. |
| Evaluation (benchmarks, held-out families) | Preprocessed OpenML-CC18 and TabArena, 5-fold cross-validation, with significance classes. |
| Main result with numbers | **Table 2 (p.6), CC18 ROC-AUC:** softmax 0.8900, DeltaNet 0.8860. **Table 3 (p.9):** DeltaNet with final-state readout and decay 0.8884 / 0.8139 versus softmax 0.8900 / 0.8172. **Negative:** (p.5: "simply replacing it with linear or recurrent updates reduces performance on both benchmarks"); (p.5: "Mamba-2 trails the rest across all metrics"). DeltaNet (p.1: "degrades beyond 2-4×") the pre-training context length. UNVERIFIED: length-generalisation curves (figures). |
| Transfers to causal estimation: authors' claim | Decay plus final-state readout (p.1: "closely match a") softmax baseline. |
| Transfers to causal estimation: our judgement | For EHR contexts far larger than training, linear-time models fail beyond 2 to 4 times the trained length unless stabilised, so retrieval or longer training contexts are needed. |

#### Row 19. Ma, Thomas, Hosseinzadeh, Labach et al. 2025, *TabDPT: Scaling Tabular Foundation Models on Real Data*
<!-- SRC: texts/2410.18164v3.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2410.18164v3. Peer reviewed (p.1: "39th Conference on Neural Information Processing Systems (NeurIPS 2025)."). |
| Venue and version | arXiv v3, 17 Jan 2026. Sections 3 to 4.6 and appendix B.1 read. |
| Dimension studied | Real versus synthetic pre-training; SSL objective; retrieval in training and inference; context size; scale. |
| What was held fixed | One component removed at a time (Figure 4a). The real-versus-synthetic contrast uses (p.8: "the TabPFN [31] synthetic data generator for this experiment") at (p.8: "the same compute budget"). |
| What was varied | SSL (p.7: "use the original target for each table during training"); training retrieval; inference retrieval; context 256; model (p.9: "from 33K to 78M") parameters; data (p.9: "from 52M cells (104K rows) to 2B cells (32M rows)"). |
| Evaluation (benchmarks, held-out families) | CC18 and CTR23 (p.6: "total of 107 datasets"). Training data (p.6: "123 datasets, with a total of 32M rows and 2B cells"). Contamination check (p.17: "similarities were manually evaluated and those found to be related were removed from training"). |
| Main result with numbers | **Scaling:** (p.9: "we estimate the scaling exponents as α = 0.42 and β = 0.39,"). **Ablations (figure only):** no SSL gives (p.7: "a large loss in performance") and (p.7: "starts to overfit after around 50 epochs"); no training retrieval (p.8: "leads to a consistent drop"), (p.8: "smaller in magnitude than drop from removing SSL"); real data (p.8: "consistently outperforms training on synthetic data across all"). **Null-leaning:** context 256 (p.8: "does not decrease"). **Caveat:** the synthetic comparator is the old TabPFN v1 generator. UNVERIFIED: ablation magnitudes. |
| Transfers to causal estimation: authors' claim | None. |
| Transfers to causal estimation: our judgement | Supports retrieval-aligned training for long contexts (EHR). Real-data SSL cannot supply counterfactual labels, so it transfers to outcome and nuisance modelling rather than to effect targets. |

#### Row 20. Garg, Ali, Hollmann, Purucker et al. 2025, *Real-TabPFN: Improving Tabular Foundation Models via Continued Pre-training With Real-World Data*
<!-- SRC: texts/2507.03971v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2507.03971v1. Workshop paper (p.1: "Proceedings of the 1 st ICML Workshop on Foundation Models for"). |
| Venue and version | arXiv v1, 5 Jul 2025. Main text read. |
| Dimension studied | Continued pre-training on real data; corpus choice; context size during continued pre-training. |
| What was held fixed | Base TabPFN v2 and recipe (p.3: "We continued pre-training for 20,000 steps with a batch"). Evaluation (p.2: "the same 29 datasets from the OpenML"), with contamination filtering (p.2: "ally inspected metadata to ensure no training and evaluation"). |
| What was varied | Corpus: curated OpenML plus Kaggle (71 tables), each alone, about 97,000 CommonCrawl tables or 658 GitTables tables. Context of 2,048 to 20,000 rows. |
| Evaluation (benchmarks, held-out families) | 29 AutoML-benchmark classification datasets; mean normalised ROC-AUC. |
| Main result with numbers | (p.3: "improves the mean normalized ROC-AUC from 0.954 to") 0.976. **Corpus (Figure 6 labels, p.4):** CommonCrawl −0.003, GitTables +0.010, OpenML & Kaggle +0.022. **Context:** (p.3: "accuracy increases with a larger context size."). **Negative:** CommonCrawl hurt (p.4: "data points and 7 features on average per dataset"). No seeds or intervals. |
| Transfers to causal estimation: authors' claim | A small curated corpus of large real tables beats web-scale corpora. |
| Transfers to causal estimation: our judgement | The analogue for causal PFNs is continued pre-training on real covariate tables (for example CPRD-like covariates with simulated outcomes). Effects are small (about 0.02) and unreplicated. |

#### Row 21. Kolberg, Kreuer, Huurdeman, Ouaari et al. 2026, *TabPFN-Wide: Continued Pre-Training for Extreme Feature Counts* (promoted in phase 3)
<!-- SRC: texts/2510.06162v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2510.06162v2. Preprint (journal template placeholder in the PDF). |
| Venue and version | arXiv v2, 29 Mar 2026. Main text read. |
| Dimension studied | Continued pre-training on a widened synthetic prior; maximum feature count during training. |
| What was held fixed | Base model (p.4: "For our continued pre-training setup, we start from the original") TabPFNv2. No ensembling (p.5: "not used for TabPFN-Wide, TabPFNv2, TabICL, and RealMLP-TD"). |
| What was varied | Prior (p.4: "the TabICL prior and subsequently widen it to a target dimension") with noise and sparsity; maximum width (p.4: "dmax ∈ {1,500, 5,000, 8,000}"). |
| Evaluation (benchmarks, held-out families) | TCGA (5 datasets), 15 HDLSS datasets, synthetic SNP tasks; 21 TabArena tasks (p.5: "samples and ≤ 500 features)"). (p.5: "5-fold cross-validation for our biomedical datasets"). |
| Main result with numbers | **HDLSS:** (p.5: "92.0% win rate"). **No forgetting:** (p.5: "datasets does not negatively impact performance on standard"); (p.5: "This suggests that there is no indication of catastrophic"). **SNP noise:** (p.5: "TabPFN-Wide and XGBoost exhibit the smallest") degradation. **Base models fail when wide:** (p.5: "exhibit inferior performance consistent with"). **Cap:** (p.4: "5,000 features due to memory constraints"). UNVERIFIED: TCGA AUROC values (figure). |
| Transfers to causal estimation: authors' claim | (p.1: "capability of foundation models for high-dimensional data") is enhanced by prior-informed adaptation. |
| Transfers to causal estimation: our judgement | Directly addresses the CausalPFN dimension limit (row 8). Continued pre-training on wide, mostly irrelevant covariates is testable for a 540-covariate causal PFN. Training samples are small (40 to 400), unlike EHR. |

#### Row 22. Peng, Shi, Zhang, Luo 2026, *GIST: Generator-state-Informed Supervision for Tabular Foundation Models*
<!-- SRC: texts/2610.12904v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.12904v1. Preprint. |
| Venue and version | arXiv v1, 9 Oct 2026. Abstract, section 4 and Tables 1 and 2 read. |
| Dimension studied | Training objective: soft targets from generator states versus sampled hard labels. |
| What was held fixed | (p.1: "ules, GIST improves mean rank across three architectures on both TabArena and"; "TALENT without changing architecture or inference."). Against (p.7: "same-architecture Hard"). |
| What was varied | Supervision target, bundled with a generator change (p.1: "GIST jointly designs task generation and query su-"). |
| Evaluation (benchmarks, held-out families) | TabArena (38) and TALENT (188) in-distribution splits; BeyondArena out-of-distribution splits. |
| Main result with numbers | **TALENT AUC (Table 1, p.7), hard versus GIST:** TabICLv2 0.8804 versus 0.8817; TabSwift 0.8713 versus 0.8726; TabPFN-2.5 0.8863 versus 0.8864. **TabArena multiclass log-loss, TabPFN-2.5:** 0.2884 versus 0.2536. (p.1: "GIST wins 62.1% of paired dataset-level comparisons against"). **Null:** tiny AUC gains; some cells worsen (TabICLv2 TabArena log-loss 0.2541 to 0.2549). UNVERIFIED: seeds; whether the TabPFN-2.5 arm is a reimplementation. |
| Transfers to causal estimation: authors' claim | Averaging (p.1: "serves the population objective and yields no larger gradient covariance"). |
| Transfers to causal estimation: our judgement | Directly transferable: a causal prior knows the true potential-outcome means, so training on them (or on the CATE) rather than on sampled outcomes is testable. Related to row 3. Predictive evidence only, with small effects. |

#### Row 23. Jeon, Cho, Suh 2026, *A JEPA Recipe for Tabular Foundation Models*
<!-- SRC: texts/2609.25541v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.25541v1. Preprint. |
| Venue and version | arXiv v1, 22 Sep 2026. Abstract and introduction read. |
| Dimension studied | Training objective: adding a JEPA latent loss beside the cell-value loss. |
| What was held fixed | Prior and data (p.1: "the data are unlimited and drawn from one distribution for both objectives"); stopping rule (p.1: "both arms train until a plateau rule stops them, with no fixed step budget."). |
| What was varied | The objective, with the wiring needed to make it train (p.1: "the value head reads the encoder field rather than the predictor, and the"). |
| Evaluation (benchmarks, held-out families) | 147 real datasets (classification and regression). |
| Main result with numbers | **Negative:** (p.1: "arm trails the value-only arm across 147 real datasets, 32:70 wins to losses on classification"); (p.1: "8:24 on regression"); (p.1: "needs 1.42 times as many steps as the value-only"). **Earlier collapse:** (p.1: "the encoder ended at a constant map on every other prior we trained it"). **Method:** (p.1: "A fixed horizon had confounded a slowdown with a ceiling"). One run per arm. |
| Transfers to causal estimation: authors' claim | None beyond the recipe. |
| Transfers to causal estimation: our judgement | A negative objective result. Its protocol lesson (compare objectives at convergence, not at fixed steps) applies to any causal-PFN objective comparison. |

#### Row 24. Thomas, Ma, Hosseinzadeh, Golestan et al. 2024, *Retrieval & Fine-Tuning for In-Context Tabular Models* (LoCalPFN)
<!-- SRC: texts/2406.05207v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2406.05207v1. NeurIPS 2024 per Semantic Scholar; venue UNVERIFIED in the PDF. |
| Venue and version | arXiv v1, 7 Jun 2024. Sections 3 to 4.4 and appendix A.5 read. |
| Dimension studied | Context construction (kNN retrieval versus random global context; context size); fine-tuning versus in-context use, separately and jointly. |
| What was held fixed | The base TabPFN; the same 95 datasets for all variants. |
| What was varied | Random context; kNN context; fine-tuning with random context; kNN after naive fine-tuning; joint retrieval-aware fine-tuning; ensembles; embeddings. |
| Evaluation (benchmarks, held-out families) | (p.7: "95 datasets, 47 small datasets, and 48"); IQM AUC with CI. Figure 1 points (p.2: "averaged over 25 seeds"). |
| Main result with numbers | **Table 8 (p.20), all datasets, IQM AUC:** TabPFN 0.917; fine-tuned 0.934; fine-tuned then kNN 0.938; kNN only 0.943; LoCalPFN 0.958 [0.956 to 0.960]. **Negative:** (p.8: "TabPFN-kNN on top of a naïvely fine-tuned model does not improve performance further."). Global ensembles (p.8: "are still not competitive even with our") kNN variant. |
| Transfers to causal estimation: authors' claim | (p.8: "it is crucial to fine-tune the model end-to-end with the retrieval") |
| Transfers to causal estimation: our judgement | Retrieval of similar patients is the obvious route for 56,000 EHR patients. But covariate-similarity retrieval may unbalance treated and control units in context; this is untested (row 8 retrieves by weak CATE estimates). |

#### Row 25. Rubachev, Kotelnikov, Kartashev, Babenko 2025, *On Finetuning Tabular Foundation Models*
<!-- SRC: texts/2506.08982v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2506.08982v2. Preprint. |
| Venue and version | arXiv v2, 11 Jun 2025. Abstract and sections 3 to 5 read. |
| Dimension studied | Fine-tuning versus in-context use for TabPFNv2; fine-tuning variants; pre-trained versus from scratch, by dataset size. |
| What was held fixed | Checkpoint and architecture; (p.5: "validation and test sets are the same") across subsamples. Arms: (p.5: "the finetuned TabPFNv2 model, original TabPFNv2 model, and the model with the"; "TabPFNv2 architecture trained from scratch on each of the subsampled versions of each dataset."). |
| What was varied | Adaptation method; training size (from 1/32 to full); initialisation. |
| Evaluation (benchmarks, held-out families) | Academic IID datasets; TabReD subsamples with temporal shift. |
| Main result with numbers | (p.1: "Our findings establish full finetuning as the most practical solution for") TabPFNv2. **Size study (figure only):** (p.6: "finetuning TabPFNv2 provides more benefits for larger target datasets"); for small data (p.6: "are often statistically insignificant compared to pure in-context learning."). **Negative:** (p.1: "rich feature sets, TabPFNv2 is less stable and prior methods remain better."). |
| Transfers to causal estimation: authors' claim | Fine-tuning works by (p.1: "improving the retrieval-based prediction logic"). |
| Transfers to causal estimation: our judgement | For trials of 300 to 3,000 patients, fine-tuning gains are likely small. For EHR it may help, but instability under temporal shift matters for records spanning calendar time. |

#### Row 26. den Breejen, Bae, Cha, Yun 2024, *Fine-tuned In-Context Learning Transformers are Excellent Tabular Data Classifiers* (TabForest)
<!-- SRC: texts/2405.13396v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2405.13396v2. Preprint. |
| Venue and version | arXiv v2, 23 Jan 2025. Sections 1 and 5 read. |
| Dimension studied | Prior mixtures (TabPFN generator, forest generator, both) × fine-tuning versus zero-shot; pre-training versus none. |
| What was held fixed | The authors' implementation: (p.6: "TabPFN (retrained) is our implementation of TabPFN, trained by us on the TabPFN-dataset."); (p.6: "TabForest is trained by us on our forest dataset."); (p.6: "TabForestPFN is trained by us on both the TabPFN-dataset and our forest dataset."); (p.6: "TabScratch is not pretrained."). |
| What was varied | Generator × adaptation. |
| Evaluation (benchmarks, held-out families) | WhyTrees (23 datasets) and TabZilla (94 datasets); normalised accuracy. |
| Main result with numbers | **WhyTrees (Table 2, p.6), mixed / numerical.** Zero-shot: TabPFN-retrained 0.481 / 0.635; TabForest 0.388 / 0.536; TabForestPFN 0.473 / 0.655. Fine-tuned: TabScratch 0.481 / 0.570; TabPFN-retrained 0.775 / 0.817; TabForest 0.853 / 0.854; TabForestPFN 0.842 / 0.849. (p.6: "fine-tuning are important."). **Negative:** (p.2: "the zero-shot performance of TabForest is significantly lacking"). |
| Transfers to causal estimation: authors' claim | (p.1: "we recommend always using it over zero-shot when the number of observations exceeds") a thousand. |
| Transfers to causal estimation: our judgement | Prior choice and fine-tuning interact: a poor zero-shot prior can be best after fine-tuning. A causal prior should be judged under its intended use (zero-shot for trials; possibly fine-tuned for EHR). |

#### Row 27. Hülskamp, Kobialka, Sommer, Nagler, Rügamer 2026, *How Well Do Prior-Data Fitted Networks Amortize Bayesian Inference?* (cites the Zhao seed)
<!-- SRC: texts/2610.13764v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.13764v2. Preprint. |
| Venue and version | arXiv v2, 16 Oct 2026. Abstract and sections 2 to 3 read. |
| Dimension studied | Scale (number of pre-training datasets; model size) versus amortisation error; ensembles of independently pre-trained PFNs. |
| What was held fixed | (p.20: "All members share optimizer settings, M and model size and only random seeds and pretraining data") differ. |
| What was varied | (p.4: "pretraining datasets M (data axis) and the model size"); ensemble type. |
| Evaluation (benchmarks, held-out families) | Amortisation error against a sampling-based reference under a realistic prior; TabArena and TALENT (p.21: "results on the remaining 255 datasets (170 classification, 85 regression)"). nanoTabPFN and TabICLv2. |
| Main result with numbers | Figure only for scaling. (p.1: "find that parts of the residual amortization"; "error persist, especially in rare settings under"; "scaling the model size"). Averaging (p.1: "can consistently reduce") uncertainty; (p.27: "The gain persists at full scale."). UNVERIFIED: values in Figure 3. |
| Transfers to causal estimation: authors' claim | Residual error leaves (p.1: "uncertainty about the predic-") tor at inference. |
| Transfers to causal estimation: our judgement | Amortisation error concentrates in rare regions of the prior, which for effects means poor-overlap regions. Ensembles of causal PFNs are a cheap, testable remedy. |

#### Band C: EHR, stroke and image-latent applications

#### Row 28. Kurmann, Fischer, Rommers, Brehm et al. 2026, *Differential Effect of Endovascular Treatment in Medium or Distal Vessel Occlusion: A Distal Secondary Analysis*
<!-- SRC: texts/kurmann2026_stroke.txt -->
| Field | Content |
|---|---|
| Paper | https://doi.org/10.1161/STROKEAHA.126.057558 (PMID 42961033). Peer reviewed. User-supplied PDF, read in full. |
| Venue and version | Stroke, online ahead of print (p.1: "Stroke. 2027;58:00–00. DOI: 10.1161/STROKEAHA.126.057558"). |
| Dimension studied | None of the pre-training dimensions. Application: an in-context model as the prognostic score for risk-based HTE in a stroke trial. |
| What was held fixed | Not applicable. The model is the off-the-shelf TabPFN (p.3: "package tabpfn (version 2.1.0)."). The comparator is NIHSS alone. |
| What was varied | Risk model: TabPFN with clinical and perfusion predictors (p.3: "volume of tissue at risk"), versus NIHSS alone. |
| Evaluation (benchmarks, held-out families) | TabPFN (p.1: "was trained to predict EENO") in a single-centre registry of patients given BMT alone (n = 257). Applied to the DISTAL randomised trial (p.1: "(55 centers and 11"), 270 BMT and 269 EVT plus BMT. Interaction with treatment on the 90-day modified Rankin Scale. |
| Main result with numbers | **Internal:** AUROC (p.4: "of 0.88 (95% CI, 0.83–0.93)"), slope (p.4: "of 0.84 (95% CI, 0.64–1.04)"). **External:** AUROC 0.73 (p.1: "moderate external discrimination (area under the receiver operating characteristic curve 0.73)"); slope (p.4: "of 0.60 (95% CI, 0.59–0.62),"). **Interaction:** (p.1: "found between predicted EENO and treatment effect (Pinteraction=0.012)"); harm in the predicted-good group (p.1: "was associated with worse 90-day modified Rankin Scale score (common odds ratio, 0.48 [95% CI, 0.27–0.84])"). **Null:** NIHSS alone was comparable (AUROC 0.71; p.1: "(Pinteraction=0.029)"); the multivariable model is (p.8: "able deep-learning model is not yet empirically justified"); overfitting (p.8: "consistent with overfitting"); selection in training data (p.8: "confounding by indication into the"). UNVERIFIED: supplementary tables. |
| Transfers to causal estimation: authors' claim | EVT (p.1: "was harmful in patients with medium or distal vessel occlusion predicted to achieve EENO") with BMT alone. |
| Transfers to causal estimation: our judgement | The only stroke study found that uses an in-context model for treatment-effect heterogeneity. It is risk-based HTE, not CATE estimation, and uses no imaging latents. Lessons for application A: poor calibration on transport from a small registry, and a single strong prognostic variable matching the TFM. |

#### Row 29. Pham, Nguyen Ho, Dao, Mai et al. 2026, *Retrieval-aligned Tabular Foundation Models Enable Robust Clinical Risk Prediction in Electronic Health Records Under Real-world Constraints* (AWARE)
<!-- SRC: texts/2604.01841v4.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2604.01841v4. Preprint (p.1: "Not peer-reviewed"). |
| Venue and version | arXiv v4, 25 Aug 2026. Abstract and sections 2.1 to 2.4 read. |
| Dimension studied | Context construction by retrieval for frozen in-context models; adapter tuning. A post-training dimension. |
| What was held fixed | (p.5: "The pretrained PFN backbones remain frozen"). Cumulative design (p.5: "This cumulative design allows the performance"). Seeds varied (p.13: "random seeds to estimate performance variability."). |
| What was varied | Task-aligned retrieval encoder, attention weighting, balanced sampling, ensembling, adapter; backbones (kNN-PFN, TabDPT, kNN). Stress tests on data scale, dimensionality and outcome rarity. |
| Evaluation (benchmarks, held-out families) | Small clinical datasets plus MIMIC-IV and eICU cohorts; AUROC and AUPRC. Prediction only. |
| Main result with numbers | (p.1: "by up to 7.0% under high feature dimensionality and 12.2% under extreme outcome imbalance."). On eICU with kNN, AUPRC (p.5: "by approximately 140%, compared with a more moder-"; "ate AUROC gain of 23.8%."). **Negative:** in-context models (p.1: "degrade quickly as feature heterogeneity and class imbalance increase."). Each ablation step is conditional on the earlier ones. |
| Transfers to causal estimation: authors' claim | (p.1: "retrieval quality and retrieval–inference coupling") are the bottlenecks. |
| Transfers to causal estimation: our judgement | The closest EHR evidence on retrieval with in-context models: high dimension and rare outcomes, as in CPRD. For effect estimation, retrieval must also keep both treatment arms in context, which is not addressed. |

#### Row 30. Pham, Cotugno, Cernei, Sîrbu et al. 2026, *Adaptation Interfaces for In-Context Tabular Foundation Models in Time-to-Event Prediction*
<!-- SRC: texts/2609.04901v2.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.04901v2. Preprint (not peer reviewed per the arXiv comment). |
| Venue and version | arXiv v2, 12 Sep 2026. Abstract and sections 3 to 5.2 read. |
| Dimension studied | Fine-tuning versus zero-shot use for time-to-event outcomes (temporal zero-shot reformulation, classification fine-tuning, survival heads), by data size. |
| What was held fixed | Frozen backbones. Context (p.7: "The reported benchmarks use R = 5 context samples for both single-risk and"). Leakage control (p.6: "observations are ever included in a support context"). |
| What was varied | Interface; size regime (p.12: "size into small (N < 500), medium (500 ≤ N < 4,000), and large (N ≥ 4,000) regimes."); backbone. |
| Evaluation (benchmarks, held-out families) | (p.1: "frozen TabFM backbones on 74 single-risk data sets, and we additionally study 4 competing-"); Ctd and IBS. |
| Main result with numbers | Rankings are in figures and Table 5 (not transcribed). (p.13: "On small data sets, RSF ranks best overall"; "and zero-shot TabPFN remains competitive for Ctd"). (p.13: "TabFMs lead for both Ctd and IBS, while zero-shot and CE variants fall substantially behind."). **Negative:** classification fine-tuning (p.1: "remains weaker for probabilistic prediction"). UNVERIFIED: per-regime numbers. |
| Transfers to causal estimation: authors' claim | (p.1: "Overall, our results indicate that effective TabFM transfer depends on the data regime and on") the interface. |
| Transfers to causal estimation: our judgement | For later time-to-event EHR outcomes at about 56,000 patients (large regime), zero-shot predictive TFMs fall behind adapted survival heads. A causal survival PFN would need a survival-native objective or adaptation. |

#### Row 31. Zhong, Huang, Zhang, Nie et al. 2026, *M²PFN: End-to-End Disentangled Alignment for Generalizable Multimodal In-Context Learning in Alzheimer's Disease*
<!-- SRC: texts/2609.28836v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.28836v1. Preprint (under review). |
| Venue and version | arXiv v1, 23 Sep 2026. Abstract, sections 3 to 4.4 and Table 3 read. |
| Dimension studied | How learned 3D-MRI latents enter a frozen TFM: end-to-end encoder training through the frozen engine versus frozen embeddings; alignment loss; a gated tabular shortcut; in-context engine versus MLP. |
| What was held fixed | (p.1: "shortcut. Because the ICL engine stays frozen, its in-context mechanism is preserved for test-"). Each row (p.10: "Table 3: Component ablation on the ADNI test set. Each row removes one mechanism from the"). |
| What was varied | Removal of disentangled alignment, of end-to-end training, of both, of the shortcut; TabPFN replaced by an MLP. |
| Evaluation (benchmarks, held-out families) | ADNI (p.1: "On ADNI (n = 2240, three-class CN/MCI/AD), M2 PFN attains 65.55% macro-F1 and 82.21%"); external cohorts OASIS-3 and SCAN without retraining. |
| Main result with numbers | **Table 3 (p.10), macro-F1 / AUC (%):** full 65.55 ± 1.26 / 82.21 ± 0.54; without alignment 64.36 / 81.41; without end-to-end 64.29 / 81.72; without both 62.33 / 80.77; without shortcut 61.00 / 79.30; MLP instead of ICL 59.32 ± 3.74 / 76.18 ± 2.13. Against frozen-embedding MMPFN, the authors attribute the gain to the fact that M²PFN (p.10: "optimizes the imaging encoder end-to-end through the ICL transformer."). **Caveat:** most component gains are 1 to 2 points, about 1 to 2 SD. |
| Transfers to causal estimation: authors' claim | End-to-end alignment of the image pathway beats ICL on frozen embeddings alone. |
| Transfers to causal estimation: our judgement | The closest evidence to application A: a frozen TFM on learned brain-MRI representations. Removing ICL hurts most, and adapting the encoder to the TFM helps. Test frozen versus TFM-aligned lesion encoders. Prediction only. |

#### Row 32. Arora 2026 (authorship per neurips.cc), *Vision-TabPFN: An Efficient Tabular Prior for Few-Shot Vision*
<!-- SRC: texts/arora2026_visiontabpfn.txt -->
| Field | Content |
|---|---|
| Paper | https://openreview.net/forum?id=VjMTFZhSZc (listing https://neurips.cc/virtual/2026/156953); no DOI or arXiv version. User-supplied PDF, read in full. |
| Venue and version | **Anonymised review version**, not camera-ready (p.1: "Submitted to 40th Conference on Neural Information Processing Systems (NeurIPS 2026). Do not distribute."). The PDF shows Anonymous Author(s); the author name and acceptance come from neurips.cc, not from the PDF. |
| Dimension studied | Fine-tuning depth versus frozen use of a TFM on frozen CLIP image embeddings. |
| What was held fixed | (p.3: "share frozen CLIP ViT-B/16 features, disjoint train/val/test class splits, the same episode sampler"); (p.4: "every run") layers 0 to 19 frozen; the projection head always trained. |
| What was varied | Projection head only (all TabPFN layers frozen) versus fine-tuning the last 2 or 4 layers; nine few-shot baselines. |
| Evaluation (benchmarks, held-out families) | CIFAR-100, miniImageNet, CUB, BloodMNIST (medical microscopy), EuroSAT. (p.3: "600 test episodes, with mean accuracy reported alongside 95% con-"). |
| Main result with numbers | **Depth (Table 1, p.4):** (p.4: "CIFAR-100 5w1s: proj. head only 35.69±1.23; L=4 80.14±0.83."). miniImageNet 5-shot: 93.57 head only, 96.14 with L = 2. **Domain shift:** (p.3: "V ISION -TAB PFN reaches 93.77%, +18.8 pp over the next-"; "best method (FOMAML, 74.96%)"). **Negative:** (p.4: "and CAML by 6–15 pp") at 1-shot; (p.4: "failure mode (46.5% vs. ProtoNet 86.8%)"); (p.4: "also limited to CLIP ViT-B/16."). No training seeds. UNVERIFIED: appendices absent from the PDF. |
| Transfers to causal estimation: authors' claim | (p.4: "Early TAB PFN layers transfer as a general in-context inference algorithm; only late layers and a"; "projection head require visual calibration."). |
| Transfers to causal estimation: our judgement | Frozen use of a TFM on image latents can fail; a learned projection plus late-layer fine-tuning fixed it here. This is a concrete design factor for a causal PFN on lesion latents. Few-shot classification; review version only. |

#### Row 33. Zhang, Zhong, Zhu, Huang et al. 2026, *TabPFN beyond Tabular Data: Calibration and Accuracy on Multimodal Embeddings*
<!-- SRC: texts/2607.11007v3.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2607.11007v3. Preprint. |
| Venue and version | arXiv v3, 28 Jul 2026. Abstract and sections 3 to 5 read. |
| Dimension studied | A TFM as a zero-gradient head on frozen encoder embeddings (image, text, audio); shots; embedding dimension; frozen versus adapted backbone. |
| What was held fixed | Pipeline (p.2: "encode → PCA-reduce → TabPFN"), with (p.4: "a fixed dimension of d = 64") in the main setting; the same embeddings for all nine heads. |
| What was varied | Classification head; shots k; PCA dimension d; encoder (11); backbone adaptation. |
| Evaluation (benchmarks, held-out families) | (p.1: "22,820 evaluation episodes spanning 14"; "datasets, 11 encoders, and three modalities"). NLL, ECE, accuracy. |
| Main result with numbers | TabPFN (p.1: "48–62% and ECE by 2.1–5.3× relative to the average of"; "eight baselines while matching or exceeding their average"). **Conditional:** (p.1: "the accuracy advantage is conditional: it concentrates at"; "dimensions (k ≥ 50, d ≤ 32), and diminishes when labeled"). UNVERIFIED: identity of the medical-imaging dataset. |
| Transfers to causal estimation: authors' claim | The calibration benefit (p.1: "transfers broadly") |
| Transfers to causal estimation: our judgement | For lesion latents the accuracy gain depends on embedding dimension (best at 32 or fewer), so latent dimension reduction is a testable factor. Calibration matters for binary-outcome effects. |

#### Row 34. Walter, Agnihotri, Keuper 2026, *Images as Tables: In-Context Learning with TabPFN for Low-Data Detection of AI-Generated Images* (promoted in phase 3)
<!-- SRC: texts/2606.00872v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2606.00872v1. Workshop paper (ICML 2026 FMSD, per the arXiv comment). |
| Venue and version | arXiv v1, 30 May 2026. Main text and appendices A, C and E read. |
| Dimension studied | A TFM on learned image latents: encoder (DINOv3, DINOv2, hand-crafted frequency features) and head (TabPFN versus an MLP on the same latents). |
| What was held fixed | (p.9: "The MLP baseline uses the same DINOv3 visual features"); for DINOv2 (p.9: "follows the same pipeline as DINOv3 + TabPFN"); PCA to (p.8: "to N × 500 feature rows, matching the feature limit of the"). |
| What was varied | Encoder; head; training size k (25 to 625); cross-generator protocols. |
| Evaluation (benchmarks, held-out families) | GenImage (eight generators); accuracy, F1, ROC-AUC; cross-generator transfer; comparator LATTE. |
| Main result with numbers | (p.4: "racy already at k = 25 and outperforms"; "LATTE by up to 8.2% at the smaller shared"). **Reversal at high n:** (p.4: "LATTE becomes stronger at k = 625, ex-"; "ceeding DINOv3-PCA-TabPFN by 7.4%"). (p.3: "MLP baseline are weaker in the low-data regime."). **Negative:** (p.10: "does not evaluate degraded inputs such as JPEG compres-"). UNVERIFIED: TabPFN version; seeds. |
| Transfers to causal estimation: authors' claim | TFMs as (p.1: "mentary adaptation mechanism") in low data. |
| Transfers to causal estimation: our judgement | The in-context advantage on image latents is largest at small n and reverses at larger n. The encoder choice is first order. Both are relevant to trials of 300 to 3,000 patients. Not medical. |

#### Band D: indirect evidence (labels revised from full text)

#### Row 35. Zhao, Thompson, Steinberg, Rahman, Bonilla, Ong 2026, *From Synthetic Priors to Model Behavior: Structural Coverage in Tabular Foundation Models* (seed)
<!-- SRC: texts/2609.06912v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2609.06912v1. Preprint. |
| Venue and version | arXiv v1, 7 Sep 2026 (only version). Sections 3 to 5 read. |
| Dimension studied | Prior design, measured as structural coverage of benchmark tasks by each generator. |
| What was held fixed | Nothing across models. The authors say so: (p.5: "descriptive rather than causal: generator identity is confounded with model architecture, optimization,"). |
| What was varied | Generator together with model: TabICLv1 and TabICLv2 (generators reproduced exactly), and Mitra and TabSwift (p.5: "paper-based proxies"). (p.5: "1,024 distinct generator mechanisms") per generator. |
| Evaluation (benchmarks, held-out families) | TabArena (p.5: "38 classification and 13 regression datasets") and TALENT. Checkpoint performance as released. Overlap between the benchmarks noted (p.5: "independent: 26 TABA RENA dataset names also appear in TALENT"). |
| Main result with numbers | TabICLv2 (p.5: "achieves coverage of 0.579, meaning that 57.9% of benchmark datasets lie within at least one"). TabSwift (p.5: "TABA RENA classification dataset") reached none at the default boundary. **Rank concordance (Table 2, p.6):** median ρ from −0.316 to −0.500, with 71.8% to 85.7% of datasets negative. **Null:** (p.5: "uniform: a nontrivial fraction of datasets exhibit the opposite ordering or no rank concordance."). Correlations use only (p.6: "three or four models"). |
| Transfers to causal estimation: authors' claim | The association (p.6: "interpreted causally") should not be read causally. |
| Transfers to causal estimation: our judgement | The coverage diagnostic transfers as a tool: compute coverage of a causal prior against descriptors of lesion latents or EHR tables before training. There is no causal evidence that coverage drives performance. |

#### Row 36. Robertson, Reuter, Guo, Hollmann et al. 2025, *Do-PFN: In-Context Learning for Causal Effect Estimation*
<!-- SRC: texts/2506.06039v3.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2506.06039v3. Peer reviewed (NeurIPS 2025 per the arXiv comment). |
| Venue and version | arXiv v3, 20 Nov 2025. Sections 4.4 to 4.6 and appendix E.2 read. |
| Dimension studied | Pre-training scale (v1 versus v1.1); in-prior sweeps of dataset size, base-rate ATE and graph size for one model. |
| What was held fixed | Architecture. But v1 and v1.1 (p.6: "are pretrained for 48 hours and 96 hours respectively on a single RTX"), and v1.1 was also (p.9: "trained on graph sizes up to 60 nodes"). Two factors change together. |
| What was varied | Training length plus prior range; at inference, dataset size (p.24: "between 5 and 2000") samples, base-rate ATE and graph size. |
| Evaluation (benchmarks, held-out families) | Synthetic case studies, in-prior sets of 500 datasets, OOD noise, non-linearity and graph size; RealCause. CATE MSE. |
| Main result with numbers | Figure only. v1 (p.9: "larger graph sizes (right), which is recovered by Do-PFN (v1.1) via larger-scale pre-training."). Dataset size: (p.24: "MSE in predicting CATE values decreases"). **Negative:** (p.24: "seems to diverge in the largest ATE group"), attributed to (p.24: "low-ATE datasets in our prior"); out of prior (p.9: "a significant reduction in Do-PFN-v1’s performance"). UNVERIFIED: figure values. |
| Transfers to causal estimation: authors' claim | The failure (p.24: "highlights the need for future research in synthetic causal data-generation"). |
| Transfers to causal estimation: our judgement | The v1 versus v1.1 comparison cannot separate scale from prior range, and the other ablations are inference-time. Large-effect attenuation agrees with row 3 and matters for trials with strong effects. |

#### Row 37. Chen, Gan, Lu, Jing et al. 2026, *A Foundation Model for Policy In-Context Longitudinal Causal Effect Estimation* (PICLE-PFN)
<!-- SRC: texts/2610.32863v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.32863v1. Preprint (p.9: "Preprint"). |
| Venue and version | arXiv v1, 23 Oct 2026. Sections 5 to 6 and Table S.5 read. |
| Dimension studied | Context size at inference; target policies outside the prior; an input channel (training-speed ablation). |
| What was held fixed | The trained model for the context and out-of-prior tests. Baselines (p.9: "are re-tuned and re-trained at every size."). |
| What was varied | Context n ∈ {100, 300, 1000}; target policy; unobserved-confounding strength. |
| Evaluation (benchmarks, held-out families) | Synthetic and MIMIC-based semi-synthetic longitudinal tasks (p.24: "mimic extract 1t"); CAPO RMSE, (p.24: "mean±SD over 20 tasks"). |
| Main result with numbers | **Table S.5 (p.24), horizon 2:** PICLE-PFN 0.456 ± 0.145 at n = 100 and 0.377 ± 0.125 at n = 1000; IGC-Net 0.447 ± 0.079 at n = 100. Authors (p.9: "all methods as sample decreases, but PICLE-PFN remains more robust."). Unseen policies (p.9: "comparable performance with the two strong baselines on the both unseen policies"). **Negative and limits:** standard deviations overlap; intervals (p.8: "interpreted as credible intervals for CAPO"); the channel ablation only (p.16: "accelerates convergence"). |
| Transfers to causal estimation: authors' claim | Policy conditioning (p.9: "can generalize beyond the policy") families in the prior. |
| Transfers to causal estimation: our judgement | Robustness evidence for a fixed causal PFN on MIMIC-derived data, not a pre-training ablation. Contexts of up to 1,000 are far below EHR scale. |

#### Row 38. Talupula and Sharma 2026, *Temporal Causal Prior-Data Fitted Networks for Panel Data with Learned Reliability Signals* (TCPFN)
<!-- SRC: texts/2606.20889v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2606.20889v1. Preprint. |
| Venue and version | arXiv v1, 18 Jun 2026. Abstract and sections 3.4, 4.2 and 6.4 to 6.6 read. |
| Dimension studied | Curriculum (phased auxiliary losses); prior mixture (a null-effect regime); a pre-processing variant. |
| What was held fixed | Not stated as a controlled protocol. |
| What was varied | (p.11: "Phase 1 (steps 0–20K): CATE only"), then null and confounding heads, then (p.11: "Add regime + identifiability + mediation"). Inclusion of an independent regime. Standardisation. |
| Evaluation (benchmarks, held-out families) | (p.2: "19 zero-shot benchmark datasets across five domains"), mainly causal discovery; PEHE on effect shapes from the prior. |
| Main result with numbers | **Curriculum:** (p.17: "JudgmentLoss grew to 60+ and EffectLoss degraded from 3.0 to 5.2."), a training-loss observation only. **Prior:** (p.17: "Without this regime, null F1 remained at 0.00 throughout training."). **Negative:** global standardisation (p.26: "per-shape PEHE rises by 0.31–0.78 across every effect shape"); not evaluated out of prior (p.17: "judgment head on structures outside the training prior"). |
| Transfers to causal estimation: authors' claim | (p.25: "We found that (1) a curriculum schedule is essential") |
| Transfers to causal estimation: our judgement | The curriculum claim rests on a training-loss anecdote with no held-out comparison. Moved down from the causal band. |

#### Row 39. Zhu, Mansoldo, Wang, Groha 2026, *A Causal Foundation Model for Structure and Outcome Prediction* (TabPFN-CFM)
<!-- SRC: texts/2606.26467v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2606.26467v1. Workshop paper (ICML 2026 FMSD, per the arXiv comment). |
| Venue and version | arXiv v1, 25 Jun 2026. Appendices E.5 and F read. |
| Dimension studied | Architecture and training-procedure changes to a Do-PFN-style backbone. |
| What was held fixed | Data only (p.14: "The training and validation datasets are identical on all setups to isolate the effect of architecture changes."). |
| What was varied | Changes applied cumulatively (p.14: "We sequentially apply each of the architectural changes on top of previous changes"), including an optimiser switch (p.13: "Muon optimizer for matrices instead of AdamW") and width (p.13: "Total parameters increase from 10.28M to 22.97M."). |
| Evaluation (benchmarks, held-out families) | Prediction and adjacency loss on synthetic validation data, figure only (p.14: "for 30k steps"). |
| Main result with numbers | (p.14: "Both prediction and adjacency losses decrease with the changes."). The authors caution (p.14: "with each other in nonlinear ways and some changes only show in longer training runs"). No downstream causal metric for the ablation. |
| Transfers to causal estimation: authors' claim | The changes (p.13: "significantly improve training stability and") efficiency. |
| Transfers to causal estimation: our judgement | A training-efficiency study with optimiser, width and architecture confounded. It gives no guidance on generalisation. |

#### Row 40. Cheng, Han, Suo, Wang 2026, *Two Is Enough: Binary Classification Priors Suffice for Multi-Class In-Context Tabular Prediction* (promoted in phase 3)
<!-- SRC: texts/2610.27569v1.txt -->
| Field | Content |
|---|---|
| Paper | https://arxiv.org/abs/2610.27569v1. Preprint. |
| Venue and version | arXiv v1, 20 Oct 2026. Sections 1 to 4 read. |
| Dimension studied | Prior design: the class-count cap of TabICLv2's prior (2 versus 10). |
| What was held fixed | (p.5: "lr, optimizer, weight decay, dropout, micro-batch, grad-accum,"; "sequence-length distribution"). |
| What was varied | Class cap **and** schedule: a (p.5: "(max_classes=2, from-scratch two-stage retrain, 540K steps)") against the official default at (p.5: "(max_classes=10, three-stage schedule, 550K steps)"). (p.5: "A strictly single-variable run (class count the"; "sole difference) is in progress"). |
| Evaluation (benchmarks, held-out families) | (p.1: "38 TabArena classification datasets (200 bootstrap rounds, anchored at default RF = 1000), the"); 60 credit-scoring institutions. Reference models' Elo taken (p.6: "without rerunning"). |
| Main result with numbers | **Elo:** 1590.1 versus 1568.0. (p.6: "The bootstrap intervals overlap (+75.2/−63.3 vs. +76.5/−66.8), so this is a directional advantage,"); the prior's contribution (p.6: "remains unisolated (Limitation 2)"). **Credit:** (p.1: "improves test AUC on 44 of 60 institutions (paired Wilcoxon p = 0.0007 for AUC, p = 0.0002"). **Failure boundary:** (p.2: "appears when K is large, when classes are severely imbalanced, and when class labels are ordinal."). |
| Transfers to causal estimation: authors' claim | Class count works (p.2: "as a tunable hyperparameter rather than a capability boundary"). |
| Transfers to causal estimation: our judgement | Weak support that a binary-outcome prior need not limit application A. The reported design is two-factor. The failures with imbalance and ordinal labels matter for rare outcomes and for the modified Rankin Scale. |

### 2b. Remaining included papers (one line each; shared rule 7)

These papers qualify but rank below the top 40. Each line is from title-and-abstract screening, with full-text checks where noted; they were not extracted. Entries 55 to 57 were moved down from the top 40 after full-text reading. The two user-supplied papers in this band (Huang et al. 2025; Zhu et al. 2026) were read in full and are given as compact rows after the list.

1. Ma et al. 2025, *Generalization Can Emerge in Tabular Foundation Models From a Single Table* (arXiv v1). https://arxiv.org/abs/2511.09665v1. *Dimension:* real-data single-table pre-training (seed predecessor). Predecessor of the Shaheen seed (same group, arXiv v1); the seed states it extends this work. One line here; read alongside the seed.
2. Abolhasani and Ganapathy 2026, *Path to Prior-Data Fitted Relational Models via Learned Latent Multi-table Representations* (arXiv v1). https://arxiv.org/abs/2610.23073v1. *Dimension:* curriculum (graph relational PFN). Curriculum learning for synthetic pre-training of the message-passing relational model Griffin. Cites Curriculum Matters.
3. Qu et al. 2025, *TabICL: A Tabular Foundation Model for In-Context Learning on Large Data* (arXiv v2). https://arxiv.org/abs/2502.05564v2. *Dimension:* curriculum over context size; architecture. TabICL (ICML 2025): curriculum on number of samples during pre-training; column-then-row architecture.
4. Pfeiffer et al. 2026, *TabH2O: A Unified Foundation Model for Tabular Prediction* (arXiv v2). https://arxiv.org/abs/2605.18383v2. *Dimension:* curriculum vs single-stage pre-training. TabH2O: stability changes allow single-stage training in place of multi-stage curriculum.
5. Kong et al. 2026, *TabFM: A Zero-Shot Foundation Model for Tabular Data* (arXiv v1). https://arxiv.org/abs/2609.37959v1. *Dimension:* curriculum scaling; synthetic prior. TabFM (400M parameters): synthetic pre-training with curriculum scaling; mostly whole-model.
6. Cheng et al. 2026, *TabAbax: A Tabular Foundation Model Technical Report* (arXiv v1). https://arxiv.org/abs/2611.00562v1. *Dimension:* prior-only ablation. TabAbax: unmodified TabICLv2 architecture trained with the improved prior isolates the prior change.
7. Wang et al. 2026, *SOMTab: Set-Order Mamba for Efficient Tabular In-Context Learning* (arXiv v1). https://arxiv.org/abs/2608.27882v1. *Dimension:* architecture (attention vs Mamba) controlled ablation. SOMTab: controlled early-training ablation of where attention is needed.
8. Zhang et al. 2025, *LimiX: Unleashing Structured-Data Modeling Capability for Generalist Intelligence* (arXiv v2). https://arxiv.org/abs/2509.03505v2. *Dimension:* training objective (masked joint-distribution modelling); scale. LimiX technical report; mostly whole-model.
9. Zhang et al. 2026, *LimiX-2: A Contextual Mechanism Network Towards General Structured-Data Intelligence* (arXiv v1). https://arxiv.org/abs/2609.17488v1. *Dimension:* scaling laws; objective. LimiX-2: scaling-law section guiding model and data scaling.
10. Wang et al. 2026, *LimiX-2M: Mitigating Low-Rank Collapse and Attention Bottlenecks in Tabular Foundation Models* (arXiv v2). https://arxiv.org/abs/2606.04485v2. *Dimension:* architecture (tokenisation, routing). LimiX-2M (ICML 2026): tokenisation and attention-routing ablations.
11. Tao et al. 2026, *Mitra-v2 Technical Report* (arXiv v1). https://arxiv.org/abs/2609.04540v1. *Dimension:* prior scale; context; fine-tuning. Mitra-v2 technical report; fine-tuning context-cap ablation.
12. Davies et al. 2026, *Mind the Gap? A Distributional Comparison of Real and Synthetic Priors for Tabular Foundation Models* (arXiv v1). https://arxiv.org/abs/2605.06343v1. *Dimension:* real vs synthetic pre-training corpora. Mind the Gap: distributional comparison of synthetic prior and real corpora and effect on performance.
13. Bouadi et al. 2026, *From Behavior to Provenance: Attributing Tabular Foundation Models to Synthetic Pretraining Data* (arXiv v1). https://arxiv.org/abs/2610.02347v1. *Dimension:* prior components: attribution by retraining. Attribution of TFM behaviour to O'Prior pre-training components with counterfactual retraining.
14. Ozturk et al. 2026, *Speedrunning Tabular Foundation Model Pretraining* (arXiv v1). https://arxiv.org/abs/2606.03681v1. *Dimension:* training procedure and optimisation. Speedrunning nanoTabPFN: accumulated pre-training changes to reach a fixed target.
15. Abolhasani and Ganapathy 2026, *PluRel-to-RDB-PFN: Schema-Guided Synthetic Relational Pretraining* (arXiv v1). https://arxiv.org/abs/2607.29129v1. *Dimension:* synthetic generator swap (relational). PluRel as an external data source for RDB-PFN.
16. Wang et al. 2026, *Relational In-Context Learning via Synthetic Pre-training with Structural Prior* (arXiv v5). https://arxiv.org/abs/2603.03805v5. *Dimension:* curriculum: single-table warm-up then relational (baseline). RDB-PFN: the relational PFN whose warm-up recipe Curriculum Matters compares against.
17. Xu et al. 2024, *Mixture of In-Context Prompters for Tabular PFNs* (arXiv v1). https://arxiv.org/abs/2405.16156v1. *Dimension:* retrieval (mixture of prompters) and fine-tuning. MixturePFN: nearest-neighbour context and bootstrapped fine-tuning.
18. Feuer et al. 2024, *TuneTables: Context Optimization for Scalable Prior-Data Fitted Networks* (arXiv v3). https://arxiv.org/abs/2402.11137v3. *Dimension:* context optimisation (prompt tuning) vs fine-tuning. TuneTables (NeurIPS 2024).
19. Guta 2026, *Localized TabICLv2: Scaling Tabular In-Context Learning through k-NN* (arXiv v1). https://arxiv.org/abs/2608.16429v1. *Dimension:* retrieval (k-NN context) for TabICLv2. Localized TabICLv2 (ICML 2026 FMSD workshop).
20. Ning et al. 2026, *Test-Time Compute for Tabular Foundation Models: Mechanisms, Gains, and Limits* (arXiv v1). https://arxiv.org/abs/2610.12005v1. *Dimension:* test-time adaptation, aggregation, context construction. Test-time compute for TFMs: adaptation vs in-context, context construction.
21. Sergazinov and Yin 2025, *Chunked TabPFN: Exact Training-Free In-Context Learning for Long-Context Tabular Data* (arXiv v2). https://arxiv.org/abs/2509.00326v2. *Dimension:* context length beyond pre-training size. Chunked TabPFN (ICLR 2026 blogpost).
22. Abdullah 2026, *Understanding Context Sampling in TabPFN on Small Tabular Datasets* (arXiv v1). https://arxiv.org/abs/2607.26628v1. *Dimension:* context size and sampling. Context sampling in TabPFN on small datasets.
23. Chen et al. 2026, *VIP-COP: Context Optimization for Tabular Foundation Models* (arXiv v2). https://arxiv.org/abs/2605.12904v2. *Dimension:* context selection beyond pre-training size. VIP-COP context optimisation.
24. Tanna et al. 2026, *Exploring Fine-Tuning for Tabular Foundation Models* (arXiv v1). https://arxiv.org/abs/2601.09654v1. *Dimension:* fine-tuning vs zero-shot. Exploring fine-tuning for TFMs.
25. Tanna et al. 2025, *TabTune: A Unified Library for Inference and Fine-Tuning Tabular Foundation Models* (arXiv v3). https://arxiv.org/abs/2511.02802v3. *Dimension:* fine-tuning strategies (library benchmark). TabTune: library with comparisons of fine-tuning strategies.
26. Kim et al. 2026, *Parameter-Efficient Distributionally Robust Adaptation of Tabular Foundation Models under Subpopulation Shift* (arXiv v1). https://arxiv.org/abs/2610.01143v1. *Dimension:* parameter-efficient fine-tuning under shift. DR-TFM.
27. Nguyen et al. 2026, *TFM-Retouche: A Lightweight Input-Space Adapter for Tabular Foundation Models* (arXiv v2). https://arxiv.org/abs/2605.06047v2. *Dimension:* input-space adapter vs fine-tuning. TFM-Retouche.
28. Pham et al. 2026, *Tabular Foundation Models for Clinical Survival Analysis via Survival-Aware Adaptation* (arXiv v1). https://arxiv.org/abs/2606.12006v1. *Dimension:* survival-aware adaptation (EHR). TFMs for clinical survival analysis (MIMIC-IV, eICU).
29. Gozeten et al. 2025, *Test-Time Training Provably Improves Transformers as In-context Learners* (arXiv v2). https://arxiv.org/abs/2503.11842v2. *Dimension:* test-time training vs pure ICL. Test-time training for TabPFN (ICML 2025; PubMed P6).
30. Bühler et al. 2026, *Causal Data Augmentation for Robust Fine-Tuning of Tabular Foundation Models* (arXiv v2). https://arxiv.org/abs/2601.04110v2. *Dimension:* fine-tuning with causal data augmentation. CausalMixFT (EurIPS 2025 workshop).
31. Howell 2026, *Model of Models: When Does Emitting a Specialist Beat Attending, Adapting, or Tuning?* (arXiv v1). https://arxiv.org/abs/2608.21386v1. *Dimension:* in-context vs fine-tuning vs hypernetwork, held fixed. Model of Models: four specialisation mechanisms compared with the rest held fixed, incl. clinical classification.
32. Balef and Eggensperger 2026, *LoopICL: Looping a single transformer block to solve tabular tasks* (arXiv v1). https://arxiv.org/abs/2609.36108v1. *Dimension:* architecture (looped single block). LoopICL.
33. Cannistraci and Vogt 2026, *Tabular Foundation Models Are Effectively Shallow* (arXiv v1). https://arxiv.org/abs/2610.13253v1. *Dimension:* architecture depth (post-hoc translation of skipped blocks). TFMs are effectively shallow; no retraining from scratch.
34. Grabocka 2026, *FTFM: Factorized Tabular Foundation Models* (arXiv v1). https://arxiv.org/abs/2610.25558v1. *Dimension:* architecture (factorised cell states). FTFM.
35. Liu and Ye 2026, *TabSwift: An Efficient Tabular Foundation Model with Row-Wise Attention* (arXiv v1). https://arxiv.org/abs/2606.07345v1. *Dimension:* architecture (row-wise attention). TabSwift (ICML 2026).
36. Arbel et al. 2025, *EquiTabPFN: A Target-Permutation Equivariant Prior Fitted Networks* (arXiv v4). https://arxiv.org/abs/2502.06684v4. *Dimension:* architecture (target equivariance). EquiTabPFN.
37. Zeng et al. 2025, *TabFlex: Scaling Tabular Learning to Millions with Linear Attention* (arXiv v1). https://arxiv.org/abs/2506.05584v1. *Dimension:* architecture (linear attention). TabFlex (ICML 2025).
38. Bartz-Beielstein 2026, *Structured Priors: Towards an algebra of component priors for prior-data fitted networks* (arXiv v1). https://arxiv.org/abs/2611.04056v1. *Dimension:* prior mixtures (algebra of component priors). Structured Priors working paper (5 pages).
39. Hosseinzadeh et al. 2026, *TabDPT-Turbo: Efficient In-Context Learning for Tabular Prediction* (arXiv v2). https://arxiv.org/abs/2608.01400v2. *Dimension:* long-context pre-training replacing retrieval; real data. TabDPT-Turbo (ICML 2026 FMSD workshop, non-archival). Cites the Shaheen seed.
40. Muller et al. 2026, *ProximalFM: Amortized Proximal Causal Inference under Hidden Confounding* (arXiv v2). https://arxiv.org/abs/2610.08078v2. *Dimension:* context size (causal PFN, proximal). ProximalFM: performance vs context size.
41. Thumm and Chen 2026, *Interventional Time Series Priors for Causal Foundation Models* (arXiv v2). https://arxiv.org/abs/2603.11090v2. *Dimension:* prior mixture of intervention types (causal PFN, time series). Interventional time-series priors: intervention-type ablation.
42. Yu et al. 2026, *Prior-Data Fitted Networks for In-Context Off-Policy Evaluation* (arXiv v1). https://arxiv.org/abs/2610.34035v1. *Dimension:* pre-training vs current-task data (PFN for off-policy evaluation). InCOPE.
43. Jung et al. 2026, *What You Observe Determines How You Identify Causal Effects: Evaluating Causal Models across Observational Views* (arXiv v1). https://arxiv.org/abs/2609.36881v1. *Dimension:* context length (causal PFNs, fixed checkpoints). CausalIDView: context-length table with released checkpoints; whole-model comparisons otherwise.
44. Ye et al. 2026, *Can Tabular Foundation Models Amortize Statistical Inference?* (arXiv v1). https://arxiv.org/abs/2609.33114v1. *Dimension:* supervised fine-tuning variant (amortised inference). TabCon: SFT and global variants as ablation.
45. Zhang et al. 2023, *Towards Causal Foundation Model: on Duality between Causal Inference and Attention* (arXiv v3). https://arxiv.org/abs/2310.00809v3. *Dimension:* zero-shot amortised vs per-dataset; alternative objectives (causal). CInA.
46. Bhattacharjee et al. 2026, *Towards Trustworthy Biological Alignment in TabPFN-Probed Pathology Foundation Models* (arXiv v1). https://arxiv.org/abs/2609.29523v1. *Dimension:* TFM probing pathology foundation-model embeddings. TabPFN probe on H&E foundation-model embeddings.
47. Zhong et al. 2026, *PromptDx: Differentiable Prompt Tuning for Multimodal In-Context Alzheimer's Diagnosis* (arXiv v1). https://arxiv.org/abs/2605.08585v1. *Dimension:* prompt tuning vs ICL on 3D-MRI features. PromptDx (Alzheimer's).
48. Kim et al. 2026, *MultiModalPFN: Extending Prior-Data Fitted Networks for Multimodal Tabular Learning* (arXiv v3). https://arxiv.org/abs/2602.20223v3. *Dimension:* TFM extended to image and text embeddings. MultiModalPFN (CVPR 2026).
49. Arazi et al. 2026, *MulTaBench: Benchmarking Multimodal Tabular Learning with Text and Image* (arXiv v3). https://arxiv.org/abs/2605.10616v3. *Dimension:* frozen vs tuned image/text embeddings with TFMs. MulTaBench (NeurIPS 2026 spotlight).
50. Lafrance 2026, *When Tabular Foundation Models Transfer Across Modalities: A Systematic Evaluation Across 95 Datasets, 7 Modalities, and Two Regimes* (arXiv v1). https://arxiv.org/abs/2606.02106v1. *Dimension:* TFM on fixed embeddings across 7 modalities. Cross-modality transfer evaluation (95 datasets).
51. Nakerst et al. 2026, *Tabular foundation models for non-tabular tasks* (arXiv v1). https://arxiv.org/abs/2608.22594v1. *Dimension:* TFM on images (PCA of pixels) and other non-tabular inputs. TFMs for non-tabular tasks.
52. Patil, Gandhi, Karabacak, Carr, Margetis 2026, *MRI-based deep learning radiomics model for automated classification of disc degeneration in the lumbar spine*, Sci Rep 16:24695 (peer reviewed). https://doi.org/10.1038/s41598-026-56056-w. *Dimension:* TFM on frozen ResNet50 MRI features (null result). Patil et al. 2026 (Sci Rep): frozen ImageNet ResNet50 features added nothing over radiomics for TabPFN.
53. Nilforoshan et al. 2023, *Zero-shot causal learning* (arXiv v4). https://arxiv.org/abs/2301.12292v4. *Dimension:* meta-learned individual effects of new interventions (claims). CaML (NeurIPS 2023): zero-shot effect prediction for unseen interventions in claims data; ablations.
54. Jia et al. 2026, *VT-Bench: A Unified Benchmark for Visual-Tabular Multi-Modal Learning* (arXiv v3). https://arxiv.org/abs/2605.08146v3. *Dimension:* visual-tabular benchmark incl. TFMs. VT-Bench; whole-model comparisons.
55. Gao, Reuter, Guo, Dhir et al. 2026, *CIDER-FM: Foundation Models for Causal Inference from Diverse Experimental Regimes* (arXiv v1). https://arxiv.org/abs/2609.39523v1. *Dimension:* architecture (three-axis attention). Moved down from the top 40 after full-text reading: its architecture ablation reports throughput only (compute; shared rule 4). Extraction note r14.
56. Ma, Frauen, Javurek, Feuerriegel 2026, *Foundation Models for Causal Inference via Prior-Data Fitted Networks* (arXiv v3; ICLR 2026). https://arxiv.org/abs/2506.10914v3. *Dimension:* prior-content robustness only. Moved down: its fine-tuning baselines are per-dataset estimators, not fine-tuned CausalFM, so it has no pre-training-dimension ablation. Prior content is covered in Brief 4. Extraction note r17.
57. Hollet, Robinson, Georgiou, Ermis et al. 2026, *A Benchmark of (MRI-) Foundation Models to Predict IDH Mutational Status in Glioma* (arXiv v2). https://arxiv.org/abs/2606.23172v2. *Dimension:* representation choice (MRI foundation-model latents with a linear head versus radiomics with TabPFN). Moved down: TabPFN is applied only to hand-crafted radiomics, not to learned latents. Indirect evidence. Extraction note r39.

#### Row S1 (one-line band, user PDF read in full). Huang, Zhong, Shi 2025, *Multistage Alignment and Fusion for Multimodal Multiclass Alzheimer's Disease Diagnosis*
<!-- SRC: texts/huang2025_miccai.txt -->
| Field | Content |
|---|---|
| Paper | https://doi.org/10.1007/978-3-032-05182-0_37 (PMID 41347112). Peer reviewed. |
| Venue and version | Publisher version (p.1: "MICCAI 2025, LNCS 15974, pp. 375–385, 2026."). |
| Dimension studied | None (application). A frozen TFM on learned brain-imaging latents (aligned T1 MRI, tau PET and diffusion features) plus MoCA, with TabPFN used without training (p.5: "the TabPFN does not require training or ﬁne tuning"). |
| What was held fixed | Splits and features across heads (p.6: "ing the same training, validation and test sets across all models"). Tabular baselines used (p.6: "the features generated by our models"). |
| What was varied | Classifier on the same latents; modality subsets; alignment method. |
| Evaluation (benchmarks, held-out families) | ADNI (p.6: "Our model is trained and tested using the ADNI [24,25] dataset (n = 1147),"), a single random 60/20/20 split, three-class diagnosis. |
| Main result with numbers | **Accuracy, AUC (Table 2, p.7):** proposed 0.7321, 0.8625; XGBoost 0.7143, 0.8317; LightGBM 0.7076, 0.8338. **Caveats:** one split, no intervals. Table 3 modality labels were lost in extraction (UNVERIFIED). The confusion matrix sums to 448 cases, against about 229 expected in a 20% test set; TabPFN was tested (p.6: "on the validation and") test sets, which may explain this (UNVERIFIED). |
| Transfers to causal estimation: authors' claim | TabPFN's pre-trained priors avoid (p.2: "additional feature alignment") |
| Transfers to causal estimation: our judgement | A frozen TFM on brain-imaging latents is at least as good as boosted trees on the same features, in one split. Weak evidence; prediction only. |

#### Row S2 (one-line band, user PDF read in full). Zhu, Zhou, Liang, Scherer, Xu, Ohno-Machado 2026, *Large Models for Small Tables: Adapting Tabular Foundation Models to EHR Data*
<!-- SRC: texts/zhu2026_amia.txt -->
| Field | Content |
|---|---|
| Paper | https://pmc.ncbi.nlm.nih.gov/articles/PMC13274287/ (PMID 42317857; no DOI). Peer reviewed. |
| Venue and version | AMIA Joint Summits on Translational Science Proceedings 2026:604–613 (PMC version). Page tags are PDF pages; printed page = PDF page + 603. |
| Dimension studied | Claimed: fine-tuning a TFM for EHR prediction. **No non-fine-tuned TabPFN arm is reported**, so fine-tuning versus in-context use is not isolated. This is a whole-model comparison. |
| What was held fixed | (p.5: "All models are trained on the same training splits and evaluated on the same test sets"). Fine-tuning hyperparameters fixed across datasets (p.6: "we keep TabPFN’s fine-tuning hyperparameters fixed across"); baselines tuned. |
| What was varied | Model: fine-tuned TabPFN versus logistic regression, XGBoost, LightGBM, CatBoost, MLP. |
| Evaluation (benchmarks, held-out families) | (p.5: "six public medical tabular datasets"), mostly UCI benchmarks; only the UTI set (120 encounters) is called (p.5: "small structured EHR dataset"). Protocol described both as (p.5: "validation, preserving class proportions in every split") with 10-fold cross-validation and as a single split (p.5: "In the Overall Results section, we instead use a single 80/20"). |
| Main result with numbers | **Accuracy (Table 1, p.6):** Arrhythmia 0.8362 versus XGBoost 0.8171; Heart 0.8769 versus logistic regression 0.8248; Pima 0.8338 versus 0.7760; UTI 1.0000 for all models. **Caveats:** ceiling effects; n of 120 to 768; large EHR untested (p.8: "testing on large-scale, multi-institutional EHR databases like MIMIC-IV or TriNetX"). UNVERIFIED: number of seeds; which protocol produced Table 1. |
| Transfers to causal estimation: authors' claim | Fine-tuned TFMs combine (p.1: "that large models for small tables can advance healthcare AI by combining rich prior knowledge with domain-specific") fine-tuning. |
| Transfers to causal estimation: our judgement | No evidence on fine-tuning versus in-context use, and none at CPRD scale. |

---
## 3. Synthesis

Every statement points to rows in section 2. *Our judgement* marks inference beyond what the papers show.

**What is established.**

1. **Prior design matters, and matters most, when other factors are fixed.**
   - With architecture, optimiser and budget fixed, changing only the synthetic prior moves performance more than any other single factor tested. This holds across O'Prior, the evaluation of public priors, Mitra and TabForest (rows 12, 13, 14, 26).
   - TabICLv2 reaches the same ordering by ablating one component at a time (row 15).
   - Mixing complementary mechanism families helps: SCMs with tree-based generators (row 13), and several mechanism families within one table (row 12).
2. **Prior and architecture interact.** A larger architecture can fail on a narrower prior (row 15). Cell-token attention suppresses irrelevant features only when the prior is sparse (row 16).
3. **Task diversity counts more than volume.** For real-data pre-training, the number of distinct tasks and the feature count drive transfer, more than rows or tokens (row 2). Random target columns beat fixed targets (row 14).
4. **Curated real tables help in continued pre-training.**
   - Continued pre-training on curated large real tables beats web-scale corpora (row 20).
   - Continued pre-training on a widened synthetic prior extends a TFM to thousands of features without forgetting (row 21).
5. **Retrieval helps with large data.** Retrieval-aligned context improves large-data performance, and fine-tuning helps most when combined with retrieval (rows 19, 24).
6. **Fine-tuning helps more as data grow.** Gains grow with target size and are often insignificant for small data (rows 25, 26, 30).
7. **Architecture can often be simplified at no cost.** Tied looped blocks match untied ones (row 17). Linear-time mixers lose accuracy and fail beyond 2 to 4 times the trained context unless stabilised (row 18).

**What is contested or weak.**

- **Curriculum.** The one clean test shows a large effect on identical data (row 1), but it is a single run with a 0.7M-parameter model. The O'Prior curriculum arm is confounded with its component set and did not win (row 12). The TCPFN curriculum claim rests on training-loss behaviour (row 38).
- **Training objective.**
  - Soft generator targets give small, mixed gains (row 22).
  - A latent JEPA loss hurts (row 23).
  - On a causal PFN, changing only the target (fluctuation supervision) reduces attenuation under effect shift, but S-learners still win near the prior centre (row 3).
- **Scale.** Scaling laws exist for real-data TFMs (row 19), but scaling model size does not remove amortisation error in rare regions of the prior (row 27). No causal study isolates scale: Do-PFN's v1 versus v1.1 confounds training time with prior range (row 36), and CURE's data-size curve is for outcome AUC (row 11).
- **Coverage.** Structural coverage of benchmarks is associated with performance, but generator and model are confounded (row 35).

**Causal PFNs specifically.** Controlled ablations of non-content dimensions are few:
- objective (row 3);
- intervention inputs (row 5);
- graph-conditioning architecture (row 6);
- loss and prior choices for continuous treatments (row 7);
- time encoder × prior integrator, single seed (row 9);
- synthetic pre-training plus fine-tuning versus real-only training, outside CATE (row 4).

Continued pre-training of TabPFN on a causal prior gave modest gains (row 8). Two findings recur:
- **Attenuation of large effects** when the prior concentrates near zero effect (rows 3, 36).
- **Loss of advantage beyond the training dimension.** CausalPFN trained up to 100 covariates is no better than meta-learners at 500 to 1,000 covariates (row 8).

**Application A (image-latent virtual trials; binary outcomes; 300 to 3,000 patients).**
- TFMs on frozen image latents work best at small n and modest embedding dimension (32 or fewer in row 33; PCA to 500 in row 34), and their advantage can reverse at larger n (row 34).
- Frozen use can fail without a learned projection or late-layer fine-tuning (row 32).
- Aligning the image encoder to a frozen TFM beats frozen embeddings for 3D brain MRI, and removing in-context learning hurts most (row 31).
- The one stroke application (row 28) used an in-context model only as a prognostic score: it mis-calibrated on transport (slope 0.60) and was no better than NIHSS alone.
- *Our judgement:* the testable design factors for a causal PFN on lesion latents are latent dimension, frozen versus TFM-aligned encoders, and a prior whose effect sizes are not concentrated near zero (rows 3, 36). Binary-only outcome priors look acceptable for multi-class prediction (row 40), but that comparison is two-factor and fails with imbalance and ordinal labels.

**Application B (EHR; about 56,000 patients; about 540 covariates; continuous, later time-to-event outcomes).**
- The covariate dimension is beyond what current causal PFNs were trained for (row 8). Wide continued pre-training is the closest tested remedy, shown for prediction only (row 21).
- Cell-token architectures suit sparse relevance (row 16).
- The data far exceed trained contexts, so retrieval is needed (rows 19, 24, 29). Retrieval quality is the bottleneck in EHR prediction (row 29).
- Fine-tuning is likely to help at this size (row 25), and time-to-event outcomes favour adapted survival heads over zero-shot use (row 30).
- Pre-training on claims sequences improved outcome AUC and effect proxies (rows 10, 11), but against trial emulations without ground truth.
- *Our judgement:* retrieving neighbours by covariate similarity may break treatment-arm balance in context. No study tests retrieval for effect estimation except CausalPFN's weak-CATE windowing (row 8).

**What is missing.**
- No causal PFN study isolates curriculum, scale, context length or fine-tuning versus in-context use for CATE accuracy.
- No study puts a causal PFN on image latents.
- No study tests retrieval-based context construction for heterogeneous effects in EHR.
- Most direct ablations are single-seed, small-model and predictive (rows 1, 12, 14, 17, 23).
- Results transcribed from figures could not be checked (rows 6, 15, 19, 27).

---
## 4. Excluded near-misses

73 papers were excluded at abstract or full-text screening, and 1 item (N74) could not be screened. Each has a link and the specific reason. Reasons citing shared rule 4 are compute-only studies. Studies first marked in phase 1 but moved down to the one-line list after full-text reading are *not* here; they remain included (section 2b, entries 55 to 57).

| # | Citation | Link | Reason for exclusion |
|---|---|---|---|
| N1 | Wahdany et al. 2026, *Dataset Inference for Data Provenance and Privacy Auditing in Tabular Foundation Models*; arXiv v1 | https://arxiv.org/abs/2610.24278v1 | cites Shaheen. Dataset inference / privacy auditing of TFMs; no pre-training dimension varied. |
| N2 | Zhou and Akoglu 2026, *When Less Compute Is More: Adaptive Early Exit Improves Pretrained Outlier Detection*; arXiv v1 | https://arxiv.org/abs/2609.32898v1 | cites Shaheen. Inference-time early exit for pretrained outlier detection; not pre-training. |
| N3 | Sharma et al. 2026, *Mechanistic Evidence for Spectral Structures in Prior-Data Fitted Networks*; arXiv v4 | https://arxiv.org/abs/2601.21731v4 | cites Zhao. Mechanistic study of spectral structure in PFNs; no pre-training dimension isolated. |
| N4 | Schindler et al. 2026, *Enhancing Tabular Learners with Context-Aware Semantic Embeddings*; arXiv v2 | https://arxiv.org/abs/2608.03565v2 | cites Shaheen predecessor. LLM semantic embeddings for tabular learners; out of scope. |
| N5 | Hu and Ghelichi 2026, *Topological Signatures of Context-Level Reliability in TabPFN*; arXiv v1 | https://arxiv.org/abs/2607.17962v1 | cites Shaheen predecessor. Topology of TabPFN representations; analysis only. |
| N6 | Polewczyk et al. 2026, *FlexTab: A Flexible Encoder-Decoder Architecture for In-Context Learning Across Diverse Tabular Tasks*; arXiv v3 | https://arxiv.org/abs/2606.30336v3 | cites Shaheen predecessor. FlexTab encoder-decoder architecture for multiple tasks; whole-model, no isolated pre-training dimension in abstract. |
| N7 | Tugnoli et al. 2026, *Improving TabPFN's Synthetic Data Generation by Integrating Causal Structure*; arXiv v3 | https://arxiv.org/abs/2603.10254v3 | TabPFN as a synthetic data generator (feature ordering); not pre-training. |
| N8 | Bergna et al. 2026, *Decoupled PFNs: Identifiable Epistemic-Aleatoric Decomposition via Structured Synthetic Priors*; arXiv v1 | https://arxiv.org/abs/2605.06413v1 | Decoupled PFNs for epistemic/aleatoric split in BO; not TFM generalisation. |
| N9 | Liu et al. 2026, *Causal Pre-training Under the Fairness Lens: An Empirical Study of TabPFN*; arXiv v2 | https://arxiv.org/abs/2601.17912v2 | Fairness of TabPFN and fine-tuned variants; outcome is fairness, not generalisation. |
| N10 | Swelam et al. 2025, *Does TabPFN Understand Causal Structures?*; arXiv v1 | https://arxiv.org/abs/2511.07236v1 | Probing TabPFN embeddings for causal structure; no pre-training dimension. |
| N11 | Xu et al. 2026, *Why Tabular Foundation Models Excel on Relational Data They Have Never Seen*; arXiv v2 | https://arxiv.org/abs/2611.02936v2 | Single-table TFMs on relational data; inference design, not pre-training. |
| N12 | Cagiano et al. 2026, *Graph-to-Table Interfaces Control Relational Generalisation*; arXiv v1 | https://arxiv.org/abs/2610.25993v1 | Graph-to-table interface components; not pre-training. |
| N13 | Schindler et al. 2025, *TabGemma: Text-Based Tabular ICL via LLM using Continued Pretraining and Retrieval*; arXiv v1 | https://arxiv.org/abs/2511.03570v1 | TabGemma: LLM continued pre-training; LLM text-based, outside TFM/PFN scope. |
| N14 | Gardner et al. 2024, *Large Scale Transfer Learning for Tabular Data via Language Modeling*; arXiv v2 | https://arxiv.org/abs/2406.12031v2 | TabuLa-8B: LLM-based tabular transfer; outside scope. |
| N15 | Rubachev et al. 2026, *On Data Scaling in Tabular ML: More Data, Better Generalization?*; arXiv v1 | https://arxiv.org/abs/2610.26794v1 | Data scaling for GBDTs/MLPs trained per task; not TFM pre-training. |
| N16 | Kim et al. 2025, *Table Foundation Models: on knowledge pre-training for tabular learning*; arXiv v2 | https://arxiv.org/abs/2505.14415v2 | Knowledge pre-training of table embeddings (not in-context TFM). |
| N17 | Purucker et al. 2026, *Beyond IID: How General Are Tabular Foundation Models, Really?*; arXiv v2 | https://arxiv.org/abs/2606.30410v2 | Benchmark software for TFM evaluation; no pre-training dimension. |
| N18 | Team et al. 2026, *Xiaomi-TabLDM: A Tabular Foundation Model Technical Report*; arXiv v2 | https://arxiv.org/abs/2609.03880v2 | Xiaomi-TabLDM technical report; no ablation section found; whole-model. |
| N19 | Eo et al. 2026, *EXAONE Tabular 1.0 : Technical Report*; arXiv v1 | https://arxiv.org/abs/2608.25774v1 | EXAONE Tabular technical report; no ablation section found; whole-model. |
| N20 | Schambach et al. 2026, *Benchmarking Attention for Tabular Foundation Models*; arXiv v3 | https://arxiv.org/abs/2609.31306v3 | Attention kernels for TFMs: compute only (rule 4). |
| N21 | Komisarczyk et al. 2026, *ElTab: Elastically Looped Tabular Transformers*; arXiv v1 | https://arxiv.org/abs/2610.41819v1 | ElTab elastic looping: compute/early-stopping motivation (rule 4). |
| N22 | Gong et al. 2026, *When Does Depth Help? Understanding Layerwise Inference in Tabular Foundation Models*; arXiv v1 | https://arxiv.org/abs/2610.19814v1 | Layerwise inference analysis; no retraining. |
| N23 | Bouadi et al. 2026, *OrionMoE-v1.0: A Mixture-of-Experts Foundation Model for Tabular In-Context Learning*; arXiv v2 | https://arxiv.org/abs/2610.20418v2 | OrionMoE: whole-model. |
| N24 | Bouadi et al. 2025, *Orion-Bix: Bi-Axial Attention for Tabular In-Context Learning*; arXiv v2 | https://arxiv.org/abs/2512.00181v2 | Orion-Bix: whole-model. |
| N25 | Bouadi et al. 2025, *Orion-MSP: Multi-Scale Sparse Attention for Tabular In-Context Learning*; arXiv v3 | https://arxiv.org/abs/2511.02818v3 | Orion-MSP: whole-model. |
| N26 | Ye et al. 2025, *A Closer Look at TabPFN v2: Understanding Its Strengths and Extending Its Capabilities*; arXiv v2 | https://arxiv.org/abs/2502.17361v2 | Analysis of TabPFN v2 internals; no pre-training dimension varied. |
| N27 | Komisarczyk et al. 2026, *Tydra: An Efficient Hybrid Model for Tabular Data*; arXiv v1 | https://arxiv.org/abs/2608.21199v1 | Tydra hybrid SSM: efficiency motivated (rule 4). |
| N28 | Cai et al. 2026, *Thinking in Depth: Retrospective Inference for Tabular Foundation Models*; arXiv v1 | https://arxiv.org/abs/2610.10317v1 | Retrospective inference at test time; not pre-training. |
| N29 | Dudley and Oymak 2026, *Latent Chain-of-Thought Improves Structured-Data Transformers*; arXiv v2 | https://arxiv.org/abs/2605.11262v2 | Latent chain-of-thought recurrence; test-time compute; no ablation section found. |
| N30 | Müller et al. 2023, *MotherNet: Fast Training and Inference via Hyper-Network Transformers*; arXiv v2 | https://arxiv.org/abs/2312.08598v2 | MotherNet hypernetwork; different paradigm (weights emitted), whole-model. |
| N31 | Zhou et al. 2026, *What Do Tabular Foundation Models Compute In Context? In-Situ Representation Refinement through Attention-Gated Updates*; arXiv v2 | https://arxiv.org/abs/2609.27679v2 | In-context representation refinement mechanism; not pre-training. |
| N32 | Landsgesell 2026, *Joint Optimization of Neural Autoregressors via Scoring rules*; arXiv v1 | https://arxiv.org/abs/2601.05683v1 | Multivariate scoring-rule output head; not generalisation of TFMs. |
| N33 | Jamalidinan et al. 2026, *ARASH: Adaptive Retrieval And Shot Selection for Tabular Prediction*; arXiv v1 | https://arxiv.org/abs/2608.17856v1 | LLM few-shot prompting for tabular data. |
| N34 | Zeldes 2026, *Closing the Context Gap: Activation Alignment for Tabular In-Context Learning*; arXiv v1 | https://arxiv.org/abs/2610.06679v1 | Activation alignment to cut context cost (rule 4). |
| N35 | Furuya et al. 2026, *Universality and Generalization of Causal Transformers Across Context Lengths*; arXiv v1 | https://arxiv.org/abs/2609.35055v1 | Theory of causally masked transformers across lengths; not causal inference or TFMs. |
| N36 | Heredge et al. 2026, *CRUMB: Efficient Prior Fitted Network Inference via Distributionally Matched Context Batching*; arXiv v1 | https://arxiv.org/abs/2606.11473v1 | CRUMB: inference compute (rule 4). |
| N37 | Lin and Li 2026, *Context-Constrained Transfer Learning for Tabular Foundation Models via Data Distillation*; arXiv v1 | https://arxiv.org/abs/2607.04809v1 | Transfer learning via data distillation for context limits; not pre-training. |
| N38 | Küken et al. 2025, *Early Stopping Tabular In-Context Learning*; arXiv v2 | https://arxiv.org/abs/2506.21387v2 | Early stopping ICL: compute (rule 4). |
| N39 | Cho et al. 2026, *Causilo Technical Report*; arXiv v1 | https://arxiv.org/abs/2609.22866v1 | Causilo: TFM technical report (name only causal); no ablation found. |
| N40 | Zhou 2026, *When and Why LLM Causal Priors Help: Closed-Loop Prior Selection for Amortized Causal Inference*; arXiv v1 | https://arxiv.org/abs/2609.06941v1 | Prior selection for Do-PFN with LLM priors; prior content (Brief 4 row 27). |
| N41 | Zare et al. 2026, *Causal Longitudinal Prior-Fitted Networks for Counterfactual Outcome Prediction*; arXiv v2 | https://arxiv.org/abs/2606.05797v2 | CausalLongPFN: no ablation of a pre-training dimension found in text. |
| N42 | Javurek et al. 2026, *Amortizing Causal Sensitivity Analysis via Prior Data-Fitted Networks*; arXiv v1 | https://arxiv.org/abs/2605.10590v1 | Sensitivity-analysis PFN; only optimisation warm-start ablation. |
| N43 | Bellot and Dhir 2026, *Foundation Models for Partial Causal Identification*; arXiv v1 | https://arxiv.org/abs/2608.20841v1 | Partial identification PFN; no pre-training ablation. |
| N44 | Melnychuk et al. 2026, *Frequentist Consistency of Prior-Data Fitted Networks for Causal Inference*; arXiv v3 | https://arxiv.org/abs/2603.12037v3 | Theory of frequentist consistency (Brief 4 row 17); no pre-training dimension. |
| N45 | Melnychuk et al. 2026, *Debiased Prior-Data Fitted Networks for Amortized Bayesian Semi-Parametric Inference*; arXiv v1 | https://arxiv.org/abs/2610.28314v1 | Theory of debiased PFNs; no pre-training dimension. |
| N46 | Mourao et al. 2026, *Prior-Data Fitted Networks for Causal Inference: a Simulation Study with Real-World Scenarios*; arXiv v2 | https://arxiv.org/abs/2603.15928v2 | Mourão et al.: evaluation of existing PFNs; whole-model. |
| N47 | Stith et al. 2026, *Causal Foundation Models*; arXiv v1 | https://arxiv.org/abs/2609.03003v1 | Causal foundation model tutorial/benchmark; whole-model comparisons. |
| N48 | Schulman et al. 2026, *Unit-level aggregation breaks coverage in causal foundation models*; arXiv v1 | https://arxiv.org/abs/2610.22770v1 | Coverage of aggregated CFM estimates; no pre-training dimension. |
| N49 | Choi et al. 2026, *Amortized Off-Policy Evaluation for LLMs*; arXiv v1 | https://arxiv.org/abs/2610.10848v1 | Amortised off-policy evaluation for LLMs; not TFM. |
| N50 | Xu et al. 2026, *When Does Pre-Trained Capacity Help Causal Learning? From Scalar Prediction to Counterfactual Post-Training*; arXiv v1 | https://arxiv.org/abs/2610.33311v1 | Pre-trained LLM capacity for causal tasks; LLM, not TFM/PFN. |
| N51 | Sauter et al. 2025, *ACTIVA: Amortized Causal Effect Estimation via Variational Autoencoders*; arXiv v4 | https://arxiv.org/abs/2503.01290v4 | ACTIVA: no ablation of a pre-training dimension found. |
| N52 | Bynum et al. 2025, *Black Box Causal Inference: Effect Estimation via Meta Prediction*; arXiv v1 | https://arxiv.org/abs/2503.05985v1 | Black Box Causal Inference: no ablation found. |
| N53 | Wang and Ghosh 2026, *MOCA: A Transformer-based Modular Causal Inference Framework with One-way Cross-attention and Cutting Feedback*; arXiv v2 | https://arxiv.org/abs/2604.23107v2 | MOCA: trained per dataset, not pre-trained. |
| N54 | Robertson et al. 2024, *FairPFN: Transformers Can do Counterfactual Fairness*; arXiv v1 | https://arxiv.org/abs/2407.05732v1 | FairPFN: counterfactual fairness; no pre-training ablation. |
| N55 | Lu et al. 2026, *Pretraining Reusable Inference Across Views with Synthetic Task Priors*; arXiv v1 | https://arxiv.org/abs/2608.19115v1 | Multi-view synthetic task prior; not tabular/causal effect estimation. |
| N56 | Saretzky et al. 2025, *Integrating a Causal Foundation Model into a Prescriptive Maintenance Framework for Optimising Production-Line OEE*; arXiv v2 | https://arxiv.org/abs/2512.00969v2 | Application of a causal foundation model in manufacturing; whole-model. |
| N57 | Luo et al. 2025, *TIME: TabPFN-Integrated Multimodal Engine for Robust Tabular-Image Learning*; arXiv v1 | https://arxiv.org/abs/2506.00813v1 | TIME: TabPFN encodes the tabular modality, image features come from a CNN; not a TFM on image latents. |
| N58 | Tran 2026, *Image Dehazing as In-Context Tabular Inference*; arXiv v1 | https://arxiv.org/abs/2610.25142v1 | Image dehazing with TFM on pixel/patch features, not learned latents. |
| N59 | Kekwick et al. 2026, *MMAP: Multimodal Missing-Aware Pretraining for Longitudinal Alzheimer's Prediction*; arXiv v1 | https://arxiv.org/abs/2609.26617v1 | MMAP: own multimodal pre-training, no TFM. |
| N60 | Ding et al. 2025, *Longitudinal Progression Prediction of Alzheimer's Disease with Tabular Foundation Model*; arXiv v2 | https://arxiv.org/abs/2508.17649v2 | L2C-TabPFN: tabular biomarkers, not learned image latents. |
| N61 | Ye et al. 2026, *Evaluating TabPFN for Mild Cognitive Impairment to Alzheimer's Disease Conversion in Data Limited Settings*; arXiv v2 | https://arxiv.org/abs/2604.27195v2 | TabPFN on TADPOLE tabular features (not learned latents); prediction only. |
| N62 | Rheude et al. 2026, *Prior-Fitted and Frozen Scorers for Multimodal Contrastive Learning*; arXiv v1 | https://arxiv.org/abs/2610.14770v1 | PFN as contrastive scoring function; not prediction or effects. |
| N63 | Herzog et al. 2025, *Outcome prediction and individualized treatment effect estimation in patients with large vessel occlusion stroke*; arXiv v1 | https://arxiv.org/abs/2507.03046v1 | Individualised effects in LVO stroke with deep models; not an in-context model. |
| N64 | Herzog et al. 2026, *Estimating Individualized Treatment Effects in Acute Ischemic Stroke with Causal Transformation Models (TRAM-DAG): A Multi-Centre Observational Study with External RCT Validation*; arXiv v3 | https://arxiv.org/abs/2606.12623v3 | TRAM-DAG individualised effects in stroke; not an in-context model. |
| N65 | Zheng 2026, *Cohort-Anchored Foundation Models for Electronic Health Records: From Risk Scores to Auditable Peer Cohorts*; arXiv v1 | https://arxiv.org/abs/2606.21885v1 | Cohort-anchored EHR foundation models: position paper, no in-context effect model. |
| N66 | Schuessler et al. 2025, *Statistical Learning for Heterogeneous Treatment Effects: Pretraining, Prognosis, and Prediction*; arXiv v2 | https://arxiv.org/abs/2505.00310v2 | Pretraining for HTE means pooled lasso pre-fitting; not foundation-model pre-training. |
| N67 | Delouee et al. 2026, *A Correspondence Score for Validating Learned Patient Representations in Clinical Tabular Data*; arXiv v1 | https://arxiv.org/abs/2608.27489v1 | Patient-representation similarity score; not TFM pre-training. |
| N68 | Delouee et al. 2026, *A Comparative Framework for Evaluating Foundation Models on Tabular Data: A Case Study in Healthcare*; arXiv v1 | https://arxiv.org/abs/2609.22154v1 | Framework for choosing TFMs in healthcare; whole-model. |
| N69 | Ebrahim 2026, *Tabular foundation models are not a shortcut to calibrated clinical risk prediction: a pre-registered simulation against the true risk*; arXiv v1 | https://arxiv.org/abs/2610.39065v1 | Calibration of TFM risk predictions (Brief 1 row 16); whole-model comparison, prediction only. |
| N70 | Li et al. 2026, *Utilizing prior-data-fitted networks and in-context learning … predicting symptomatic intracranial hemorrhage after successful recanalization*, Front Neurol (PMID 41602981) | https://doi.org/10.3389/fneur.2025.1698741 | TabPFN risk prediction after thrombectomy; prediction only, no treatment effects. |
| N71 | Liu et al. 2026, *Machine learning models for estimating counterfactuals in a single-arm inflammatory bowel disease study* (Brief 1 row 14) | https://arxiv.org/abs/2604.23465v1 | TabPFN as outcome model for counterfactuals in a prospective research cohort (not EHR, not stroke); no pre-training dimension. |
| N72 | TabPFN on hand-crafted radiomics features: PMIDs 41209261, 40910573, 40696844, 42169789, 40948925, 42288610 | https://pubmed.ncbi.nlm.nih.gov/41209261/ | Hand-crafted radiomics features, not learned latent representations; prediction only. |
| N73 | Kita et al. 2026, transformer multimodal model for lean mass from chest radiographs and EHR, J Transl Med (PMID 41928289) | https://doi.org/10.1186/s12967-026-08079-0 | Own multimodal transformer, not a TFM. |
| N74 | SIIM 2025 abstract *In-Context Prior Data Fitted …* (found by WebSearch W8) | https://siim.org/wp-content/uploads/2025/08/In-Context-Prior-Data-Fitted_An.pdf | **Not screened: source unreachable and not supplied.** siim.org refused by the proxy; the user did not supply the abstract. The title suggests TabPFN in imaging; content unknown. |

---
## 5. Extra output: pre-training dimensions against evidence strength

How to read the cells:
- **Direct ablation:** the dimension was varied with the other dimensions held fixed (rows cited).
- **Indirect:** whole-model comparisons, multi-factor changes, inference-time sweeps, or associations.
- **None:** no study found.

*Causal* covers causal PFNs and pre-trained treatment-effect models. Rows are from section 2a; *2b* marks one-line papers not extracted.

| Dimension | General TFMs | Causal PFNs / causal pre-training | Image latents | EHR / stroke | Overall strength |
|---|---|---|---|---|---|
| Prior design and mixtures (beyond prior content) | Direct: 12, 13, 14, 15, 26. Indirect: 35, 40; 2b (Mind the Gap, TabAbax prior-only) | Direct (content-level): 4 (paired prior), 7 (prior choices). Indirect: 36, 38 | None | None | **Direct** for general TFMs; thin for causal |
| Real-data or continued pre-training | Direct: 2, 19, 20, 21 | Direct: 8 (TabPFN continued on a causal prior), 4 (synthetic plus fine-tuning versus real-only); non-PFN: 10, 11 | None | Direct, non-PFN: 10, 11 (claims; proxy or AUC metrics) | **Direct** (general); limited (causal) |
| Architecture | Direct: 15, 16, 17, 18 | Direct: 5, 6, 9 (single seed). Indirect: 39 | Direct (component removal): 31 | None | **Direct** (general); small, few (causal) |
| Training objective | Direct: 19 (SSL), 22 (bundled with a generator change), 23 (negative) | Direct: 3, 7 | None | None | **Direct**, few studies |
| Curriculum | Direct: 1 (single run). Indirect: 12 (confounded); 2b (TabICL, TabH2O, graph PFN curriculum) | Indirect: 38 (training-loss anecdote) | None | None | **Weak:** one direct study |
| Scale (data, model) | Direct: 19 (scaling exponents), 27 (scale versus amortisation error) | Indirect: 36 (confounded with prior range) | None | Indirect: 11 (AUC, not effects) | Direct (general); **none** for effect accuracy |
| Context length and retrieval | Direct: 18 (length generalisation), 19, 20, 24 | Indirect: 8, 36, 37 (inference-time sweeps) | Indirect: 33, 34 (shots) | Direct (frozen backbone, cumulative): 29 | Direct (general, EHR prediction); **indirect** (causal) |
| Fine-tuning versus in-context use | Direct: 24, 25, 26 | Direct: 4 (outside CATE). Indirect: 8 | Direct: 32 (fine-tuning depth). Indirect: 31 | Direct: 30 (time-to-event). Indirect: S2 (no in-context arm) | Direct (general); **none** for CATE |

---

## 6. UNVERIFIED cells (summary)

Most of these items are numbers shown only in figures, or unread appendices and supplements:

- **Figure-only values:**
  - Row 2: tied query-key experiment.
  - Row 6: appendix H.1.
  - Row 11: data-size curves.
  - Row 15: Elo curves.
  - Row 18: length-generalisation curves.
  - Row 19: ablation magnitudes.
  - Row 21: TCGA AUROC.
  - Row 27: Figure 3.
  - Row 30: per-regime ranks.
  - Row 36: Figures 4 and 9.
- **Missing protocol details:**
  - Row 1: run-to-run variance; optimiser and steps.
  - Row 3: mechanism dimension; network size.
  - Row 5: transformer seed protocol.
  - Row 7: steps and seeds of the ablation runs.
  - Row 14: number of seeds.
  - Row 22: seeds; whether the TabPFN-2.5 arm was retrained.
  - Row 34: TabPFN version; seeds.
  - Row S2: number of seeds; which protocol produced Table 1.
- **Venue not printed in the PDF read:**
  - Row 8 (CausalPFN, NeurIPS 2025 per Semantic Scholar).
  - Row 12 (O'Prior).
  - Row 24 (LoCalPFN, NeurIPS 2024 per Semantic Scholar).
- **Unread material:**
  - Row 4: appendix E.3.
  - Row 28: supplementary tables.
  - Row 32: the review PDF has no appendices.
  - Row 33: identity of the medical-imaging dataset.
- **Unresolved inconsistencies:**
  - Row S1: modality labels of Table 3; evaluated sample size.
  - Row 7: ablation tables versus main Table 2.
