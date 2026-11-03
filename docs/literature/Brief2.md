# Brief 2: Treatment effects from images

**Date:** 3 November 2026
**Question:** How have treatment effects, or individual treatment rules (ITRs), been estimated from medical images or from representations derived from images? How were the estimators evaluated? Which semi-synthetic benchmarks with a known effect exist?
**Scope covered, in priority order:**
1. Stroke and other neurological imaging: lesion maps, magnetic resonance imaging (MRI), computed tomography (CT), perfusion, and ITRs for thrombectomy or thrombolysis.
2. Medical imaging in general: radiology, histopathology, chest radiographs and others.
3. Semi-synthetic image benchmarks with a known effect. The seed is Giles et al. 2025 and the InterSynth framework.
4. Shared-representation networks applied to images. These include the treatment-agnostic representation network (TARNet), Dragonnet and the causal effect variational autoencoder (CEVAE).
5. Causal representation learning for medical images.
6. Work that separates the error due to the representation from the error due to the estimator.

Each included paper has a card in section 2 with every field the brief asks for: paper; imaging modality; sample size; representation method; estimators; tuning of estimators; source of the true effect; performance measures; main result; stated limitations. Section 4 answers the question on separating representation error from estimator error.

**Other abbreviations used throughout:**
- Effects: average treatment effect (ATE); conditional average treatment effect (CATE); individual treatment effect (ITE).
- Error and evaluation measures: precision in estimation of heterogeneous effects (PEHE); root mean squared error (RMSE); mean squared error (MSE); area under the receiver operating characteristic curve (AUC); rank-weighted average treatment effect (RATE).
- Study design: randomised controlled trial (RCT).
- Learners and estimators: S-learner (single outcome model with treatment as an input); T-learner (one outcome model per arm); X-learner (cross-fitted learner of Künzel et al.); double machine learning (DML).
- Lesion representations: variational autoencoder (VAE); autoencoder (AE); principal component analysis (PCA); non-negative matrix factorisation (NMF).
- MRI sequences and maps: diffusion-weighted imaging (DWI); apparent diffusion coefficient (ADC); fluid-attenuated inversion recovery (FLAIR).

### Assumptions (how ambiguities in the brief were resolved)

**1. The seed paper.**
- *Giles et al. 2025* is D. Giles, C. Foulon, G. Pombo, J.K. Ruffle, T. Xu, H.R. Jäger, J. Cardoso, S. Ourselin, G. Rees, A. Jha and P. Nachev, *Individualized prescriptive inference in ischaemic stroke*, Nature Communications 16:8968 (2025), doi:10.1038/s41467-025-64593-7.
- Its preprint is arXiv:2301.10748. Versions v1 (25 Jan 2023) to v4 (18 Sep 2025) exist, and v1 carried the British spelling "Individualised".

**2. The InterSynth framework.**
- The original InterSynth paper is D. Giles, R. Gray, C. Foulon, G. Pombo, T. Xu, J.K. Ruffle, H.R. Jäger, J. Cardoso, S. Ourselin, G. Rees, A. Jha and P. Nachev, *InterSynth: A Semi-Synthetic Framework for Benchmarking Prescriptive Inference from Observational Data*. It appeared in *Machine Learning for Multimodal Healthcare Data* (ML4MHD 2023 workshop), Lecture Notes in Computer Science (LNCS), pp. 172–188, doi:10.1007/978-3-031-47679-2_13 (row 2).
- Neither the Nature Communications version nor arXiv v1 or v4 of the seed contains the word "InterSynth" (text search of all three files found 0 hits). The link between the two papers rests on the shared authors and the shared design. The InterSynth paper itself could not be opened (see Access limitations).

**3. Later benchmarks built on InterSynth.** None was found:
- forward citations of the seed DOI and the arXiv record: 6 each;
- forward citations of InterSynth: 1;
- web searches.

The only citing works are reviews or lesion-deficit mapping papers (near-misses N15–N16).

**4. "Treatment effects from images".** I included three kinds of study:
- (a) studies that estimate effects with images or image-derived features as covariates or effect modifiers;
- (b) semi-synthetic benchmarks whose effect is simulated from real medical images or image-derived features;
- (c) methods papers on image representations for confounding adjustment, if they contain a medical-image experiment.

Two further rules:
- Studies in which the "treatment" is a brain-structure exposure, such as atrophy, were included only if they offer a semi-synthetic benchmark with a known effect (row 13). Otherwise they are near-misses.
- Prognostic models used to choose a treatment, with no causal estimand, are near-misses.

**5. Date window.** 2019 to November 2026. One exception is Xu et al. 2018 (row 3), included as the direct backward precursor of the seed (Nachev group) and flagged as pre-window. MR PREDICTS (Venema 2017) is listed as a near-miss.

**6. Trial-based imaging subgroup analyses.**
- The literature of conventional single-marker subgroup analyses of stroke trials (core volume, mismatch, collaterals) is large.
- I included two recent examples:
  - row 6: the perfusion-diffusion mismatch, a classic imaging marker;
  - row 5: a deep-learning-derived imaging marker.
- I did not try to cover the whole subgroup literature. Section 4 states this limit.

### Access limitations
- **InterSynth (row 2) could not be read.**
  - link.springer.com served a JavaScript challenge page.
  - The green open-access copy at discovery.ucl.ac.uk was refused by the proxy. WebFetch could not resolve that host.
  - icml.cc, OpenAlex, DBLP and Europe PMC were refused.
  - The Semantic Scholar record has its abstract elided by the publisher, and Crossref has no abstract.
  - Only the metadata (title, authors, venue, pages) is verified. The whole row is UNVERIFIED for content.
- **Nakano & Shiinoki 2026 (row 16)** is abstract only: Springer served a challenge page.
- **The Nature Communications PDF returned HTTP 429.** The HTML version of record was used instead, so quotes are located by section (§). Supplementary tables were read from arXiv v4, which bundles the supplement and has page numbers.
- **PMC web pages were not used.** All PMC texts are NCBI E-utilities XML, so they carry no page numbers and are located by section heading.
- **github.com is blocked.** Licences were read from raw.githubusercontent.com LICENSE files and READMEs. Where no file was found, the cell says so.
- **Supplements not opened.** Supplementary appendices were not opened for rows 5, 7, 8, 9, 11, 15 and 20, except where they are included in the arXiv PDF. Tuning details that live only in those appendices are marked UNVERIFIED.
- **Sources not queried directly:**
  - Google Scholar cannot be queried automatically.
  - OpenReview and the NeurIPS, ICML, ICLR, AISTATS, CLeaR and UAI proceedings sites were not queried. They were covered through the arXiv API, Semantic Scholar citation graphs and WebSearch. Expanded, these are the Conference on Neural Information Processing Systems (NeurIPS), the International Conference on Machine Learning (ICML), the International Conference on Learning Representations (ICLR), the International Conference on Artificial Intelligence and Statistics (AISTATS), the Conference on Causal Learning and Reasoning (CLeaR) and the Conference on Uncertainty in Artificial Intelligence (UAI).
- **Semantic Scholar** returned HTTP 429 on most first attempts. Every call eventually succeeded after backoff.

---

## 1. Search log

All searches were run on 3 November 2026. In the queries below, double quotes inside arXiv and PubMed syntax are written as single quotes.

Column key:
- **Hits:** records returned, or the total count where the source reports one.
- **Scr.:** records whose title or abstract was screened.
- **Inc.:** new inclusions, by row number.

| # | Source | Query / action | Hits | Scr. | Inc. (new) |
|---|---|---|---|---|---|
| 1 | Crossref | `query.bibliographic=Giles Foulon Nachev` | 15 | 15 | rows 1, 2 |
| 2 | Crossref | `InterSynth Nachev` | ≥4 (my parser stopped at a record with no title) | 4 | (row 2, duplicate) |
| 3 | Crossref | `Giles Nachev Nature Communications 2025 imaging heterogeneous treatment effects semi-synthetic` | error (empty response) | 0 | 0 |
| 4 | arXiv API | `all:InterSynth` | 0 | 0 | 0 |
| 5 | arXiv API | `au:Nachev` (50 most recent) | 50 | 50 | 0 new; preprint 2301.10748 of row 1 identified |
| 6 | Springer, UCL Discovery, icml.cc, OpenAlex, DBLP, Europe PMC | full text / abstract of InterSynth | blocked | – | – |
| 7 | WebSearch | `InterSynth semi-synthetic framework benchmarking prescriptive inference observational data Giles pdf` | 9 | 9 | 0 (located green OA copy, unreachable) |
| 8 | WebSearch (extended) | `'InterSynth' OR 'Individualized prescriptive inference in ischaemic stroke' semi-synthetic lesion treatment effect benchmark` | 10 | 10 | 0 |
| 9 | Semantic Scholar | forward citations of DOI 10.1038/s41467-025-64593-7, of arXiv:2301.10748, and of the InterSynth DOI | 6 / 6 / 1 | 13 | 0 (N15, N16 near-misses) |
| 10 | Backward chase | reference list of row 1 (94 references, Nature HTML) | 94 | 94 | row 3 |
| 11 | PubMed | `High-dimensional therapeutic inference in the focally damaged human brain` | 1 | 1 | (row 3, full text) |
| 12 | PubMed | `(individual treatment effect OR conditional average treatment effect OR heterogeneous treatment effect) AND (MRI OR magnetic resonance) AND (deep learning OR machine learning)` | 1,287 | 60 (most recent) | row 18 identified |
| 13 | PubMed | `('treatment effect'[tiab]) AND (multiple sclerosis[tiab]) AND (deep learning[tiab] OR neural network[tiab]) AND (MRI[tiab])` | 1 | 1 | 0 |
| 14 | PubMed | `('individual treatment effect'[tiab] OR 'individualized treatment effect'[tiab] OR 'conditional average treatment effect'[tiab] OR 'heterogeneous treatment effect'[tiab] OR 'treatment effect heterogeneity'[tiab]) AND stroke[tiab] AND (imaging OR CT OR MRI OR perfusion OR lesion)[tiab]` | 6 | 6 | row 6 |
| 15 | PubMed | `('treatment effect'[tiab]) AND (thrombectomy OR thrombolysis OR alteplase)[tiab] AND (machine learning OR deep learning OR causal forest)[tiab]` | 9 | 9 | rows 5, 7; N4 |
| 16 | PubMed | `Falet JR[au] AND treatment effect`; `Durso-Finley J[au]`; `Arbel T[au] AND (treatment effect OR causal)` | 3 / 2 / 20 | 25 | row 9 |
| 17 | PubMed | `(MR PREDICTS[tiab]) OR (individual treatment benefit[tiab] AND endovascular[tiab])` | 7 | 7 | 0 (N3, N5) |
| 18 | PubMed | `(deep learning OR convolutional)[tiab] AND (randomized OR randomised OR trial)[tiab] AND (treatment benefit OR treatment effect OR predictive biomarker)[tiab] AND (stroke OR thrombectomy)[tiab]` | 3 | 3 | 0 new |
| 19 | PubMed | `HERMES[tiab] AND (machine learning OR individualized OR heterogeneity of treatment effect)[tiab] AND thrombectomy` | 2 | 2 | 0 |
| 20 | PubMed | `(artificial intelligence OR deep learning)[tiab] AND (digital pathology OR histopatholog* OR whole-slide)[tiab] AND predictive[tiab] AND (randomized OR randomised)[tiab] AND (benefit OR treatment effect)[tiab] AND interaction[tiab]` | 6 | 6 | row 15 |
| 21 | PubMed | `Spratt DE[au] AND multimodal artificial intelligence AND androgen deprivation` | 5 | 5 | 0 new |
| 22 | PubMed | `(deep learning OR radiomics)[tiab] AND (heterogeneous treatment effect* OR 'individualized treatment effect' OR 'individual treatment effect' OR 'conditional average treatment effect' OR 'causal forest' OR uplift)[tiab]` | 46 | 46 | rows 17, 18 |
| 23 | arXiv API | `au:Durso_Finley` | 0 | 0 | 0 (author-format miss; covered by 24–25) |
| 24 | arXiv API | `abs:'treatment effect' AND abs:image AND (abs:medical OR abs:MRI OR abs:radiology)` | 22 | 22 | rows 10, 12; N9, N12 |
| 25 | arXiv API | `abs:'treatment effect' AND abs:'multiple sclerosis'` | 12 | 12 | row 11 |
| 26 | arXiv API | `abs:'treatment effect' AND abs:images AND abs:confound*` | 10 | 10 | row 22; N10, N13 |
| 27 | arXiv API | `abs:'semi-synthetic' AND abs:image AND (abs:'treatment effect' OR abs:'causal effect')` | 6 | 6 | 0 (N11) |
| 28 | arXiv API | `abs:'causal effect' AND (abs:'chest X-ray' OR abs:radiograph OR abs:histopathology OR abs:'whole slide' OR abs:retinal OR abs:fundus)` | 2 | 2 | 0 |
| 29 | arXiv API | `(abs:CEVAE OR abs:TARNet OR abs:Dragonnet) AND (abs:image OR abs:images OR abs:imaging)` | 7 | 7 | 0 (all off-topic) |
| 30 | arXiv API | `abs:'causal representation learning' AND (abs:medical OR abs:MRI OR abs:clinical) AND abs:imag*` | 7 | 7 | 0 (N18) |
| 31 | arXiv API | `abs:'treatment effect' AND (abs:'whole slide' OR abs:histopatholog* OR abs:pathology) AND (abs:deep OR abs:learning)` | 5 | 5 | 0 (N7) |
| 32 | arXiv API | `abs:'treatment effect' AND (abs:'chest X-ray' OR abs:'X-ray' OR abs:CXR OR abs:CT OR abs:radiolog*)` | 17 | 17 | row 4 |
| 33 | arXiv API | `abs:'individualized treatment' AND (abs:imaging OR abs:image OR abs:MRI)` | 29 | 29 | rows 14, 20 |
| 34 | arXiv API | `abs:'treatment effect' AND abs:stroke` | 22 | 22 | 0 (N1, N2) |
| 35 | Backward chase | references of row 20 (refs 9, 11, 12, 16, 17, 26, 27, 28, 37, 50 inspected) | 10 | 10 | rows 8, 21; N6, N8 |
| 36 | Known-item lookup | arXiv id_list for leads from prior knowledge or reference lists: 2006.13135, 2007.00163, 2206.06417, 2502.01334 (each verified by opening) | 4 | 4 | row 13; N8, N14, N16 |
| 37 | Semantic Scholar | forward citations of arXiv:2204.01702 (row 10), DOI 10.1038/s41467-022-33269-x (row 9), arXiv:2406.02534 (row 20) and arXiv:2506.14329 (row 22) | 12 / 33 / 1 / 5 | 51 | rows 16, 19; N17, N19 |
| 38 | PubMed | `Nakano H[au] AND (treatment effect OR causal OR I-SPY2 OR BiomedCLIP)`; `(foundation model OR BiomedCLIP OR self-supervised)[tiab] AND (treatment effect OR causal forest OR RATE)[tiab] AND (MRI OR CT OR radiograph* OR pathology)[tiab]` | 2,038 / 52 | 20 / 52 | 0 new |
| 39 | Crossref | venue checks for rows 4, 8, 11, 12, 13, 20 | 6 | 6 | – |

**Totals:**
- Screened: about 700 titles or abstracts.
- Full text or abstract opened for 22 included papers and 20 near-misses.

---

## 2. Evidence table

### 2a. Overview (detail in the cards below)

| Row | Paper (link) | Status | Modality | n | Source of the true effect |
|---|---|---|---|---|---|
| 1 | Giles 2025, [doi:10.1038/s41467-025-64593-7](https://doi.org/10.1038/s41467-025-64593-7) | peer reviewed | DWI lesion masks and disconnectomes, stroke | 4,119 images / 2,830 patients | Simulated from known lesion–deficit and responsiveness maps |
| 2 | Giles 2023 InterSynth, [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13) | peer-reviewed workshop | UNVERIFIED | UNVERIFIED | UNVERIFIED |
| 3 | Xu 2018, [doi:10.1093/brain/awx288](https://doi.org/10.1093/brain/awx288) | peer reviewed (pre-window) | DWI lesion maps, stroke | 1,172 | Simulated hypothetical interventions (known effect size) on real outcomes |
| 4 | Herzog 2025, [arXiv:2507.03046v1](https://arxiv.org/abs/2507.03046v1); LNCS [doi:10.1007/978-3-032-07945-9_8](https://doi.org/10.1007/978-3-032-07945-9_8) | arXiv v1 read; peer-reviewed LNCS version exists | non-contrast CT and CT angiography, stroke | 449 | None (RCT; no ITE ground truth) |
| 5 | van Poppel 2025, [doi:10.1186/s13244-025-02095-2](https://doi.org/10.1186/s13244-025-02095-2) | peer reviewed | non-contrast CT white-matter lesions | 614 | None (RCT subgroup interaction) |
| 6 | Schiphorst 2026, [doi:10.5853/jos.2025.01200](https://doi.org/10.5853/jos.2025.01200) | peer reviewed | MR perfusion/diffusion mismatch | 102 | None (RCT subgroup interaction) |
| 7 | Debs 2021, [doi:10.1016/j.nicl.2020.102548](https://doi.org/10.1016/j.nicl.2020.102548) | peer reviewed | DWI/ADC/perfusion MRI | 109 | None (factual final infarct only) |
| 8 | Ma 2023, [arXiv:2307.12858v1](https://arxiv.org/abs/2307.12858v1); [doi:10.1007/978-3-031-43904-9_69](https://doi.org/10.1007/978-3-031-43904-9_69) | arXiv v1 read; MICCAI 2023 | head CT, intracerebral haemorrhage | 504 | None (observational; factual metrics) |
| 9 | Falet 2022, [doi:10.1038/s41467-022-33269-x](https://doi.org/10.1038/s41467-022-33269-x) | peer reviewed | MRI-derived scalar lesion and volume metrics, multiple sclerosis (MS) | 3,830 | None (held-out RCT subgroup ATE) |
| 10 | Durso-Finley 2022, [arXiv:2204.01702v4](https://arxiv.org/abs/2204.01702v4) | arXiv v4 read; MIDL 2022 (PMLR) | multi-sequence MRI, MS | 1,817 | None (RCT uplift bins) |
| 11 | Durso-Finley 2023, [arXiv:2305.03829v4](https://arxiv.org/abs/2305.03829v4); [doi:10.1007/978-3-031-43904-9_46](https://doi.org/10.1007/978-3-031-43904-9_46) | arXiv v4 read; MICCAI 2023 | multi-sequence MRI, MS | 2,389 | None (bounds on ITE error from RCT ATE) |
| 12 | Durso-Finley 2024, [arXiv:2406.12807v1](https://arxiv.org/abs/2406.12807v1); [doi:10.1007/978-3-031-72384-1_38](https://doi.org/10.1007/978-3-031-72384-1_38) | arXiv v1 read; MICCAI 2024 | 3D MRI, MS | >3,600 | None (factual trajectories) |
| 13 | Pölsterl 2021, [arXiv:2006.13135v4](https://arxiv.org/abs/2006.13135v4); [doi:10.1007/978-3-030-78191-0_4](https://doi.org/10.1007/978-3-030-78191-0_4) | arXiv v4 read; IPMI 2021 | T1 MRI-derived volumes | 11,800 (semi-synthetic); 711 (ADNI) | Synthetic outcome from real image-derived volumes |
| 14 | Li & Kosorok 2023, [arXiv:2304.13003v1](https://arxiv.org/abs/2304.13003v1) | preprint | FDG-PET (Alzheimer's) | 441 (real); synthetic 40×40 images | Fully synthetic simulation; none for real data |
| 15 | Spratt 2023, [doi:10.1056/EVIDoa2300023](https://doi.org/10.1056/EVIDoa2300023) | peer reviewed | prostate histopathology slides | 5,727 | None (RCT validation of rule) |
| 16 | Nakano 2026, [doi:10.1007/s10278-026-02344-w](https://doi.org/10.1007/s10278-026-02344-w) | peer reviewed (abstract only) | breast DCE-MRI | 739 | None (RCT; RATE) |
| 17 | Wei 2026, [doi:10.1108/atsip-06-2025-0051](https://doi.org/10.1108/atsip-06-2025-0051) | peer reviewed | head-and-neck CT | 3,346 | None (observational) |
| 18 | Yuan 2026, [doi:10.1186/s12880-026-02533-7](https://doi.org/10.1186/s12880-026-02533-7) | peer reviewed | T1 MRI radiomics, osteosarcoma | 34 | None (observational) |
| 19 | Aknin 2023, [arXiv:2304.07787v1](https://arxiv.org/abs/2304.07787v1) | preprint | oesophageal biopsy histology | 112 | None (RCT policy value) |
| 20 | Xiao 2025, [arXiv:2406.02534v2](https://arxiv.org/abs/2406.02534v2); [doi:10.1109/wacv61041.2025.00443](https://doi.org/10.1109/wacv61041.2025.00443) | arXiv v2 read; WACV 2025 | CMNIST, birds, dermoscopy (ISIC 2018), lung CT (NSCLC-Radiomics) | 415–11,788 per dataset | Synthetic outcomes from annotated image features |
| 21 | Jiang 2023 (CMDE), [arXiv:2301.11351](https://arxiv.org/abs/2301.11351) | arXiv read; ICML 2023 | chest radiographs (COVID-19 collection) | 857 | Synthetic outcomes from diagnosis labels and demographics |
| 22 | Schulte 2025, [arXiv:2506.14329v1](https://arxiv.org/abs/2506.14329v1) | arXiv v1 read; ICML 2025, PMLR 267 | paediatric chest radiographs | 3,769 | Synthetic outcome; constant ATE = 2 |

### 2b. Cards

**Row 1. Giles D, Foulon C, Pombo G, Ruffle JK, Xu T, Jäger HR, Cardoso J, Ourselin S, Rees G, Jha A, Nachev P. *Individualized prescriptive inference in ischaemic stroke*. Nat Commun 16:8968 (2025).** [doi:10.1038/s41467-025-64593-7](https://doi.org/10.1038/s41467-025-64593-7). Version read: journal HTML (version of record) for the main text; arXiv v4 for the supplement; arXiv v1 for the earlier methods. Peer reviewed.
- **Imaging modality:** acute DWI, with automatically segmented ischaemic lesion masks in standard brain-template (MNI) space and derived disconnectomes (§Patient population: "This dataset comprises 4,119 irrevocably anonymized DWI from 2830 unique patients.").
- **Sample size:**
  - The image pool is 4,119 images. Each functional-network trial recruits a subset.
  - With lesion masks, trial n ranges from 31 to 495 (arXiv v4 Supp. Table 1, p. 40). With disconnectomes it ranges from 297 to 3,078 (Supp. Table 2, p. 40).
  - There were 22,528 trial conditions in all (§Prescriptive inference with virtual interventional trials: "yielded 22,528 separate virtual clinical trial conditions").
- **Representation method:**
  - 3D VAE and 3D AE, NMF and PCA, each at 2 to 50 dimensions.
  - Baselines: vascular-territory atlas labels (anterior or posterior circulation, and six arterial territories).
  - Quote (§Results): "Each trial was thus evaluated with 46 representations: two low-dimensional baselines and eleven incrementally higher dimensional ones across four representational rationales."
- **Estimators:** S-learner and T-learner with extremely randomised trees, random forest, Gaussian process, XGBoost and logistic regression (§Prescriptive inference: "We infer treatment effects using two frameworks"; §Models).
- **Tuning of estimators:**
  - Published version: none. §Models says "each with default parameter settings"; PCA likewise "with default parameters" (§Principal component analysis).
  - **Version discrepancy:** arXiv v1 reported tuning (p. 28): "full evaluation over 10-fold crossvalidation across the range of conditions was performed using hyperparameter-optimised (using nested K-fold crossvalidation)".
  - arXiv v1 also tested "shared representation approaches: causal multitask Gaussian process" in preliminary analyses (p. 28). These were dropped after "selection for prescriptive performance" (p. 28).
  - The "optimal" representation and estimator reported in the supplement (VAE with two-model ExtraTrees; arXiv v4 Supp. Fig. 75 title, p. 78) is the best of 460 configurations evaluated on the same validation folds. No separate selection step is described. This is my reading of §Model evaluation and Supp. Table 4, not a statement by the authors.
- **Source of the true effect:** simulated from known lesion–deficit and lesion–responsiveness maps.
  - A deficit is present when the lesion overlaps at least 5% of a NeuroQuery-derived functional network (§Lesion-deficit and treatment response simulation: "A lesion intersecting with ≥5% of a subnetwork was designated as causing a corresponding deficit.").
  - Responsiveness to treatment A or B is set by overlap with subnetworks defined from receptor positron emission tomography (PET) or Allen transcriptome maps.
  - Outcomes are binary, with noise set by the treatment effect and recovery effect (TE and RE) hyperparameters (§Response noise: "A synthetic ground truth with TE = 1 and RE = 0 would therefore have no response noise").
- **Confounding mechanism:**
  - Observable confounding: allocation probability rises along the lesion-centroid axis (§Observable confounding: "We used the co-ordinates of the lesion centroid to simulate the treatment–outcome confounding effects").
  - Unobservable confounding (§Unobservable confounding: "This mechanism makes treatment allocation depend on true treatment responsiveness").
- **Performance measures:**
  - Balanced accuracy of the recommended treatment, and PEHE.
  - PEHE is secondary (§Comparison: "For this reason, we include PEHE only for completeness.").
- **Main result:**
  - Lesion masks, ideal conditions: "balanced accuracy for inferring the optimal treatment from the 50-dimensional VAE representation, averaged across all 16 functional networks, was 0.793". The baseline gave "vs 0.523 (95% CI [0.50, 0.55]) for a simple vascular baseline" (§Prescriptive inference is limited less by allocation policy…).
  - Disconnectomes: "balanced accuracy from the 50-dimensional VAE representation was 0.875 (95% CI [0.83, 0.92]), vs 0.546" (same section).
  - Rich representations under confounding were "almost always at least non-inferior" to randomised allocation with low-dimensional baselines (same section).
  - The randomised comparator used only the low-dimensional baseline (§Comparison: "This baseline was computed with unconfounded allocation, as a surrogate for RCTs.").
- **Null and negative results:**
  - In the noisiest settings, "no statistical distinction could be made" (§Results).
  - S-learner logistic regression was below chance (balanced accuracy 0.484) for every representation (arXiv v4 Supp. Table 4, p. 77: "NMF Logistic regression One 0.484085").
- **Stated limitations:**
  - (§Discussion) "It is not possible to model all forms of confounding in the observational setting".
  - DWI availability: "Though brain imaging is widely mandated in acute stroke, policies on the use of highly expressive modalities such as DWI vary".
  - Timing of imaging was not modelled.
- **Code, data and licence:**
  - Code, lesion masks and atlases are released (§Data availability: "Data and code relating to this article are available publicly from https://github.com/high-dimensional/individualized_prescriptive_inference").
  - Licence is CC BY-NC-SA 4.0 (README "## Licence"; LICENCE file "Attribution-NonCommercial-ShareAlike 4.0 International").

**Row 2. Giles D, Gray R, Foulon C, Pombo G, Xu T, Ruffle JK, Jäger HR, Cardoso J, Ourselin S, Rees G, Jha A, Nachev P. *InterSynth: A Semi-Synthetic Framework for Benchmarking Prescriptive Inference from Observational Data*. LNCS, ML4MHD 2023, pp. 172–188.** [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13). Version read: metadata only (Crossref; Semantic Scholar). Peer-reviewed workshop proceedings.
- **Modality, sample size, representation method, estimators, tuning, source of the true effect, performance measures, main result and stated limitations:** all UNVERIFIED, because neither the full text nor the abstract could be opened (see Access limitations).
- **Licence:** Semantic Scholar marks a green open-access PDF with licence "null".

**Row 3 (pre-window precursor). Xu T, Jäger HR, Husain M, Rees G, Nachev P. *High-dimensional therapeutic inference in the focally damaged human brain*. Brain 141:48–54 (2018).** [doi:10.1093/brain/awx288](https://doi.org/10.1093/brain/awx288). Version read: PMC copy (PMC5837627). Peer reviewed.
- **Imaging modality:** DWI lesion maps registered to template space (§Materials and methods: "yielding 5789 binary variables per patient").
- **Sample size:** (Abstract) "Studying 1172 patients with anatomically registered focal brain lesions".
- **Representation method:** 5,789 binary voxels at 6 mm resolution. These feed a transductive linear support vector machine that predicts gaze recovery. Its output is added as a prognostic covariate.
- **Estimators:**
  - Linear regression of outcome on treatment, age, sex and lesion volume. This is a test of the ATE, not the CATE.
  - The "high-dimensional" model adds the classifier score (§Results).
- **Tuning of estimators:** not reported.
- **Source of the true effect:** simulated hypothetical randomised interventions of known size. Either a responder proportion of 10–90% was imposed, or lesions were shrunk with recovery decided by the classifier's weights (§Results).
- **Performance measures:** the "therapeutic threshold", meaning the effect size detected in 50% of 600 randomisations.
- **Main result:**
  - Lesion-non-altering interventions: "this analysis yielded a monotonic therapeutic function with a therapeutic threshold corresponding to 62.9%", falling to "significantly shifting the therapeutic function leftward to 56.0%".
  - Lesion-altering interventions: "this analysis yielded a therapeutic function with a threshold at an effect size of 78.4%", falling to "The therapeutic function shifted leftward to 55.0%" (§Results).
- **Stated limitations:** (§Discussion) "our estimates are likely to be conservative". Gaze is only one behaviour.

**Row 4. Herzog L, Bühler P, de la Rosa E, Sick B, Wegener S. *Outcome prediction and individualized treatment effect estimation in patients with large vessel occlusion stroke*. LNCS (Image Analysis in Stroke Diagnosis and Interventions) pp. 73–82, 2025.** [arXiv:2507.03046v1](https://arxiv.org/abs/2507.03046v1). Version read: arXiv v1 preprint. The peer-reviewed LNCS version ([doi:10.1007/978-3-032-07945-9_8](https://doi.org/10.1007/978-3-032-07945-9_8)) was not opened.
- **Imaging modality:** non-contrast CT and CT angiography from the Multicenter Randomized Clinical Trial of Endovascular Treatment for Acute Ischemic Stroke in the Netherlands (MR CLEAN).
- **Sample size:** (p. 6) "Of the 500 patients in the MR CLEAN trial, 449 were considered for analysis."
- **Representation method:**
  - Frozen and then fine-tuned encoders from CT foundation models (SwinUNETR or SegResNet), with a small classification head (p. 5).
  - This is an encoder swap with the estimator held fixed. Both encoders "yielded comparable results" (p. 6).
- **Estimators:**
  - Ordinal neural-network transformation models (ONTRAMs). These are proportional-odds models with a linear clinical part and an image term.
  - The ITE is the difference in the predicted probability of a modified Rankin Scale (mRS) score of 0–2.
  - No treatment–covariate interaction (p. 5): "no terms for treatment-covariate interactions were incorporated, i.e. a homogenous treatment effect was assumed".
- **Tuning of estimators:**
  - Fixed settings: 10,000 epochs with default Adam for the clinical part. For the image part, the authors "train the classification head with a batch size of 2, learning rate of 1e-4" (p. 5).
  - No search is reported.
- **Source of the true effect:** none. This is an RCT, so ITEs cannot be checked.
- **Performance measures:** AUC, negative log-likelihood, Brier score, C-for-benefit, and the ATE minus the mean of the ITEs (p. 6).
- **Main result (null for imaging):**
  - (p. 6) "Regarding ITE estimation, all models performed similarly". For clinical variables alone, Table 1 (p. 7) gives "C-ben 0.551 [0.48, 0.62]"; the other input combinations range from 0.549 to 0.570.
  - "As in case of prediction performance, clinical features seemed to carry most of the predictive signal for ITE estimation."
- **Stated limitations:**
  - (p. 8) "A limitation of our study is the small sample size."
  - The homogeneous-effect specification is noted as future work. T- and X-learners are planned.

**Row 5. van Poppel LM et al. *White matter lesion effect modification of aspirin and unfractionated heparin during endovascular stroke treatment*. Insights Imaging 16 (2025).** [doi:10.1186/s13244-025-02095-2](https://doi.org/10.1186/s13244-025-02095-2). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** baseline non-contrast CT (Abstract: "WML volume was automatically determined using deep learning-based segmentation on baseline non-contrast CT scans"). WML is white-matter lesion.
- **Sample size:** (Abstract) "Of 628 patients, 614 with baseline CT were included." These are from the Multicenter Randomized Clinical Trial of Periprocedural Medication in Endovascular Treatment (MR CLEAN-MED).
- **Representation method:** a single scalar, WML volume, from an nnU-Net segmentation model (nnU-Net is a self-configuring U-Net segmentation framework) (§Assessment of WML characteristics).
- **Estimators:** (Abstract) "Multivariable logistic regression evaluated treatment effect and effect modification." The model has a multiplicative interaction term.
- **Tuning of estimators:** not applicable (parametric model).
- **Source of the true effect:** none. This is a secondary analysis of an RCT.
- **Performance measures:** interaction p-values and adjusted odds ratios.
- **Main result:** (Abstract) "WML volume significantly modified the effect of aspirin on sICH (p = 0.01), but not on functional outcome (p = 0.95)". sICH is symptomatic intracranial haemorrhage.
- **Null result:** (Key Points) "No WML-volume-based patient subgroup was identified where aspirin or heparin treatment demonstrated safe clinical benefit."
- **Stated limitations:** post-hoc design. The appendix was not opened, so the full limitations list is UNVERIFIED.

**Row 6. Schiphorst AT et al. *Does the Benefit of Thrombectomy in Large Strokes Depend on Perfusion–Diffusion Mismatch? A Large Stroke Therapy Evaluation Trial Post Hoc Analysis*. J Stroke (2026).** [doi:10.5853/jos.2025.01200](https://doi.org/10.5853/jos.2025.01200). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** MR perfusion-weighted imaging and diffusion imaging, in the Large Stroke Therapy Evaluation (LASTE) trial.
- **Sample size:** 102 of the 324 trial patients had baseline perfusion imaging (Abstract).
- **Representation method:** a binary hand-crafted marker (Abstract: "defined as a mismatch ratio ≥1.2").
- **Estimators:** generalised odds ratios with a heterogeneity test.
- **Tuning of estimators:** not applicable.
- **Source of the true effect:** none (RCT).
- **Performance measures:** ratio of generalised odds ratios and the heterogeneity p-value.
- **Main result (null):**
  - (Abstract) "No significant treatment effect heterogeneity by diffusion-perfusion mismatch was observed for the primary outcome".
  - The interaction estimate was "ratio of GenORs: 1.63 [95% CI, 0.71 to 3.74]; P for heterogeneity=0.24".
- **Stated limitations:** (Abstract) "An individual participant-data meta-analysis of RCT is needed for definitive conclusions."

**Row 7. Debs N et al. *Impact of the reperfusion status for predicting the final stroke infarct using deep learning*. NeuroImage Clin 29 (2021).** [doi:10.1016/j.nicl.2020.102548](https://doi.org/10.1016/j.nicl.2020.102548). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** baseline DWI, ADC and perfusion maps (Tmax, cerebral blood flow and cerebral blood volume). Outcome is the final infarct on FLAIR.
- **Sample size:** (§Patients and imaging protocol) "In total, 109 patients were analyzed as shown in Fig. 1." Of these, "Early reperfusion was observed in 74 patients, while 35 had no reperfusion".
- **Representation method:** an end-to-end late-fusion U-Net (a convolutional segmentation network) on 2D slices.
- **Estimators:**
  - Separate networks for reperfused and non-reperfused patients. This works like a T-learner on images, with reperfusion status as the "treatment" (§Introduction: "We hypothesized that training CNNs from reperfusion status-specific subcohorts could improve their performance."; CNN is convolutional neural network).
  - Reperfusion is a post-baseline state, not a randomised treatment.
- **Tuning of estimators:** UNVERIFIED. The training configuration is in Appendix B, which was not opened.
- **Source of the true effect:** none. Only the factual final infarct was observed, and the counterfactual infarct is never checked.
- **Performance measures:** Dice similarity coefficient, volumetric similarity, precision, recall, Hausdorff distance and AUC.
- **Main result:**
  - (§Results) "The predicted infarct volumes were significantly larger with the non-reperfused compared to the reperfused model". Median 39.7 versus 17.5 mL.
  - "CNN-based models achieved higher AUC values compared to those of perfusion-diffusion mismatch models".
- **Stated limitations:** (§Limitations) "Patients were included from two cohorts with different treatment protocols". Reperfusion was assessed differently in the two cohorts.

**Row 8. Ma W, Chen C, Abrigo J, Mak CH-K, Gong Y, Chan NY, Han C, Liu Z, Dou Q. *Treatment Outcome Prediction for Intracerebral Hemorrhage via Generative Prognostic Model with Imaging and Tabular Data*. MICCAI 2023 (LNCS).** [arXiv:2307.12858v1](https://arxiv.org/abs/2307.12858v1); [doi:10.1007/978-3-031-43904-9_69](https://doi.org/10.1007/978-3-031-43904-9_69). Version read: arXiv v1. Peer reviewed (conference).
- **Imaging modality:** head CT in intracerebral haemorrhage (ICH).
- **Sample size:** (p. 6) "The dataset comprises 504 cases who underwent head CT scans and were diagnosed with ICH." Of these, 364 were managed conservatively and 140 had surgery.
- **Representation method:** a 3D ResNet-34 image encoder plus a tabular multilayer network. The two are combined by product-of-experts into a VAE "prognostic score" latent (pp. 4–5).
- **Estimators:**
  - The proposed generative prognostic model.
  - Comparators were the balancing neural network (BNN), counterfactual regression with the Wasserstein distance (CFR-WASS), the local similarity preserved individual treatment effect estimator (SITE), β-Intact-VAE, and the dynamic affine feature map transform (DAFT).
  - Comparators share the image encoder (p. 7: "we utilized the same feature extraction architectures as our approach").
- **Tuning of estimators:**
  - Fixed: Adam optimiser, with training "consisting of 1000 epochs with a batch size of 128" (pp. 6–7).
  - No search is reported for the method or the comparators.
- **Source of the true effect:** none. The data are real and observational. Selection bias was increased on purpose (p. 6: "To address the selection bias resulting from the non-randomized controlled trials, we intentionally increased the imbalance of the dataset.").
- **Performance measures:** policy risk, and factual AUC and accuracy by arm.
- **Main result:** (p. 7) "Our proposed method demonstrated a significant improvement in model performance compared to other methods, as evaluated using all five metrics." Results are from three runs (p. 7: "Our reported results are the average and standard deviation obtained from three independent runs.").
- **Stated limitations:** none stated in the main text.
- **Code and licence:** code on GitHub (med-air/TOP-GPM), Apache License 2.0 (LICENSE file).

**Row 9. Falet J-PR et al. *Estimating individual treatment effect on disability progression in multiple sclerosis using deep learning*. Nat Commun 13 (2022).** [doi:10.1038/s41467-022-33269-x](https://doi.org/10.1038/s41467-022-33269-x). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** MRI-derived scalars only. These were T2 lesion volume, count of gadolinium-enhancing (Gad) lesions and normalised brain volume (§Introduction: "scalar MRI metrics (lesional and volumetric) obtained at the screening visit").
- **Sample size:** (Abstract) "Leveraging data from six randomized clinical trials (n = 3,830)".
- **Representation method:** 19 tabular clinical and MRI features. No learned image representation was used.
- **Estimators:**
  - A multi-headed multilayer perceptron (MLP) with a shared trunk, pre-trained on relapsing-remitting MS and fine-tuned on primary progressive MS.
  - (§Treatment effect modeling) "This multi-headed approach can be seen as a variant of the T-Learner".
  - Comparators: ridge regression and Cox proportional hazards (CPH) T-learners, and single-feature scores.
- **Tuning of estimators:**
  - (§Training) "A random search was used to identify the hyperparameters with the best validation performance".
  - Comparators received the same procedure (§Baseline models: "Hyperparameter tuning was done on the same folds and with the same metrics as for the MLP.").
- **Source of the true effect:** none. Held-out RCT arms were used, and the effect was evaluated as the ATE in predicted-responder subgroups.
- **Performance measures:** hazard ratios in predicted responder groups, and ADwabc, an area-between-curves metric defined in the supplement, which was not opened.
- **Main result:** (Abstract) "the average treatment effect was larger for the 50% (HR, 0.492; 95% CI, 0.266-0.912; p = 0.0218)". This compares with HR 0.743 for the whole held-out group (HR is hazard ratio). The ridge and CPH T-learners "compare favorably on one of the two datasets" (§Comparison to baseline models).
- **Stated limitations:** (§Discussion) MRI scalars "could potentially ignore more subtle predictive features found within the MRI voxel-level data".
- **Code:** github.com/jpfalet/ms-predictive-enrichment. No licence file was found on raw.githubusercontent.com.

**Row 10. Durso-Finley J, Falet J-PR, Nichyporuk B, Arnold DL, Arbel T. *Personalized Prediction of Future Lesion Activity and Treatment Effect in Multiple Sclerosis from Baseline MRI*. MIDL 2022 (PMLR).** [arXiv:2204.01702v4](https://arxiv.org/abs/2204.01702v4). Version read: arXiv v4. Peer reviewed (MIDL, Medical Imaging with Deep Learning).
- **Imaging modality:** baseline five-sequence brain MRI plus lesion masks.
- **Sample size:** (p. 1) "validated on a proprietary federated dataset of 1817 multi-sequence MRIs acquired from MS patients during four multi-centre randomized clinical trials".
- **Representation method:** a ResNet encoder learned end to end as a shared trunk (p. 3: "Our network is based on TARNET (Shalit et al., 2017) and its multi-treatment extension").
- **Estimators:** a multi-head TARNet-style network with five arms. CATE is computed relative to placebo.
- **Tuning of estimators:**
  - Fixed values only (p. 15: "with a learning rate of .0001 and a batch size of 8").
  - 4×4 nested cross-validation is used for evaluation and ensembling. No search procedure is reported.
- **Source of the true effect:** none (RCT data).
- **Performance measures:** average precision for the binary outcome of no new or enlarging T2 lesions (MEDA-T2); MSE; uplift bins; and risk-adjusted outcome under the recommended treatment.
- **Main result:** (p. 7) "individuals predicted to respond most (top 33%) have a significantly greater reduction in lesion count over the entire group".
- **Failure mode:** the regression could not beat the mean for the high-efficacy arm, because of near-zero variance (p. 6).
- **Stated limitations:**
  - (p. 7) "Individual potential outcome predictions cannot be evaluated due to the lack of ground truth".
  - (p. 8) "highly effective suppression of new lesion formation may have only a modest effect on long term disability progression".

**Row 11. Durso-Finley J, Falet J-P, Mehta R, Arnold DL, Pawlowski N, Arbel T. *Improving Image-Based Precision Medicine with Uncertainty-Aware Causal Models*. MICCAI 2023 (LNCS) pp. 472–481.** [arXiv:2305.03829v4](https://arxiv.org/abs/2305.03829v4); [doi:10.1007/978-3-031-43904-9_46](https://doi.org/10.1007/978-3-031-43904-9_46). Version read: arXiv v4. Peer reviewed.
- **Imaging modality:** multi-sequence MRI with lesion maps.
- **Sample size:** (p. 5) "Excluding patients with incomplete data resulted in a dataset with n = 2389 patients."
- **Representation method:** the multi-head ResNet of row 10, made probabilistic.
- **Estimators:** a Bayesian multi-head network giving a Gaussian distribution for each potential outcome.
- **Tuning of estimators:** not reported in the main text. The architecture appendix is not in the arXiv PDF (UNVERIFIED).
- **Source of the true effect:** none. The authors bound the ITE error using the trial ATE (p. 4: "given that ground truth for the individual treatment effects are not available, we cannot compute MSE").
- **Performance measures:** factual MSE as a function of uncertainty; upper and lower bounds on the ITE MSE; and the expected response under proposed treatments (ERUPT) metric.
- **Main result:**
  - (p. 6) "Taking all treatments in aggregate, the model achieves an MSE of 0.59 ± 0.03."
  - The bounds on the ITE error fall as uncertainty falls.
  - Laquinimod, which failed at the group level, helps an uncertainty-selected subgroup (p. 6).
- **Stated limitations:** none explicit. The authors note that the evaluation does not depend on the choice of uncertainty method.

**Row 12. Durso-Finley J, Barile B, Falet J-P, Arnold DL, Pawlowski N, Arbel T. *Probabilistic Temporal Prediction of Continuous Disease Trajectories and Treatment Effects Using Neural SDEs*. MICCAI 2024 (LNCS) pp. 400–410.** [arXiv:2406.12807v1](https://arxiv.org/abs/2406.12807v1); [doi:10.1007/978-3-031-72384-1_38](https://doi.org/10.1007/978-3-031-72384-1_38). Version read: arXiv v1. Peer reviewed.
- **Imaging modality:** baseline 3D MRI plus tabular data, from six MS RCTs.
- **Sample size:** (p. 3) "Extensive experiments are performed on a large (over 3600 patients), multi-centre, proprietary dataset of 3D MRI".
- **Representation method:** an encoder trained end to end into a latent space. The latent is evolved by a neural stochastic differential equation (SDE).
- **Estimators:** a neural SDE with treatment as an input. The ITE is the difference between latent trajectories.
- **Tuning of estimators:** (p. 6) "the remaining 3 folds were used for training, validation and hyperparameter tuning". The search space is not reported.
- **Source of the true effect:** none (RCTs).
- **Performance measures:** factual MSE of the Expanded Disability Status Scale (EDSS) score over time, and uncertainty-filtered subsets.
- **Main result:** numerical results were not extracted (see the verification log).
- **Stated limitations:** not extracted (UNVERIFIED).

**Row 13. Pölsterl S, Wachinger C. *Estimation of Causal Effects in the Presence of Unobserved Confounding in the Alzheimer's Continuum*. IPMI 2021 (LNCS).** [arXiv:2006.13135v4](https://arxiv.org/abs/2006.13135v4); [doi:10.1007/978-3-030-78191-0_4](https://doi.org/10.1007/978-3-030-78191-0_4). Version read: arXiv v4. Peer reviewed (IPMI, Information Processing in Medical Imaging).
- **Imaging modality:** T1-weighted MRI reduced to FreeSurfer volumes and cortical thickness (FreeSurfer is a brain-segmentation package).
- **Sample size:**
  - Semi-synthetic experiment (p. 9): "We use T1-weighted magnetic resonance imaging brains scans from N = 11,800 subjects from UK Biobank".
  - Real-data analysis: 711 subjects from the Alzheimer's Disease Neuroimaging Initiative (ADNI) (p. 9).
- **Representation method:** 19 FreeSurfer volumes. A substitute confounder comes from probabilistic PCA or Bayesian probabilistic matrix factorisation (BPMF) (the deconfounder approach).
- **Estimators:** logistic regression with no adjustment, adjustment for age only, adjustment for the substitute confounder, or adjustment for all confounders (oracle).
- **Tuning of estimators:** the number of substitute confounders was fixed (K = 5), and a posterior predictive check was used (p. 9).
- **Source of the true effect:** synthetic outcomes from real image-derived volumes (p. 9: "create a synthetic binary outcome").
  - Sparse true effects. The unobserved confounder comes from k-means clusters of principal components.
  - The confounding strength is varied (Table 1, p. 8).
- **Performance measures:** RMSE of the estimated effects against the true effects, over 1,000 simulations.
- **Main result:**
  - The substitute confounder "achieves an improvement 2.9 – 5.5 higher than that of the age-only model" (p. 9).
  - But "using all confounders (Oracle) leads to the lowest RMSE" (p. 9).
- **Stated limitations:** (p. 9) "there is a cost to using a substitute confounder". The "treatment" is brain anatomy, not an intervention.
- **Code and licence:** code on GitHub (ai-med/causal-effects-in-alzheimers-continuum), GNU General Public License v3 (LICENSE file on the master branch).

**Row 14. Li X, Kosorok MR. *Functional Individualized Treatment Regimes with Imaging Features*. arXiv:2304.13003v1 (2023).** [arXiv:2304.13003v1](https://arxiv.org/abs/2304.13003v1). Version read: arXiv v1. Preprint.
- **Imaging modality:** fluorodeoxyglucose PET in Alzheimer's disease (ADNI). The simulations use synthetic 2D images.
- **Sample size:**
  - Real data (p. 14): "We now analyze the records from 441 participants through the ADNI1 and ADNI GO phases."
  - Simulation: synthetic images "at a grid of Ns = 40 × 40 pixels" (p. 13), with 100 Monte Carlo replications.
- **Representation method:** a multi-dimensional functional principal component basis built on bivariate splines over triangulations (p. 2).
- **Estimators:** Q-learning, a regression-based method for estimating an optimal treatment regime.
- **Tuning of estimators:** the number of basis functions is chosen by two criteria (p. 13: "we adopt both PVE and PAVE criteria to select the leading PC bases"). PVE is percentage of variance explained; PAVE is percentage of association-variation explained.
- **Source of the true effect:**
  - Simulation: a fully synthetic linear model, so the optimal regime is known.
  - ADNI: none. Treatment is observational medication use, under an ignorability assumption.
- **Performance measures:** value of the estimated regime against the optimal regime, and coefficient MSE.
- **Main result:** in simulation, both criteria give values "close to those with optimal treatment regime" (p. 13).
- **Stated limitations:** ignorability is "not in general empirically verifiable in observational studies" (p. 6). The extension to binary outcomes and multi-stage decisions is future work (p. 20).

**Row 15. Spratt DE et al. *Artificial Intelligence Predictive Model for Hormone Therapy Use in Prostate Cancer*. NEJM Evid 2(8) (2023).** [doi:10.1056/EVIDoa2300023](https://doi.org/10.1056/EVIDoa2300023). Version read: PMC copy (PMC11195914). Peer reviewed.
- **Imaging modality:** digitised haematoxylin-and-eosin prostate biopsy slides.
- **Sample size:**
  - (Abstract) "digital pathology images from pretreatment prostate tissue and clinical data from 5727 patients enrolled in five phase 3 randomized trials".
  - Validation was in NRG Oncology / Radiation Therapy Oncology Group (NRG/RTOG) trial 9408 (n = 1,594).
- **Representation method:** (§Image feature extraction model development) "A Resnet-50 feature extraction model was trained on image patches using self-supervised learning." The training used Momentum Contrast v2 (MoCo-v2) without outcomes.
- **Estimators:**
  - A multimodal model optimising the difference in ADT benefit, giving a "delta" score; ADT is androgen deprivation therapy.
  - It was dichotomised at the 67th percentile.
  - In development, each arm came from a different trial (§Downstream multimodal predictive model development: "each contributed to one treatment type of interest"). The comparison of arms during development is therefore between trials, not within a randomisation. This is my reading.
- **Tuning of estimators:** (§Downstream…) "randomly split into training (60%) and tuning (40%) sets for model training and hyperparameter tuning". The cut-off was also chosen on the tuning set.
- **Source of the true effect:** none. The locked rule was validated in a separate RCT through the treatment-by-subgroup interaction.
- **Performance measures:** Fine–Gray subdistribution hazard ratios by subgroup, interaction tests, and restricted mean survival time.
- **Main result:**
  - Model-positive patients: "(subdistribution hazard ratio, 0.34; 95% CI, 0.19 to 0.63; P<0.001)".
  - Model-negative patients: "(subdistribution hazard ratio, 0.92; 95% CI, 0.59 to 1.43; P=0.71)" (§Short-term ADT predictive model).
- **Null result:** "We did not observe differential treatment benefits between predictive model subgroups on the exploratory end points MFS and overall survival" (MFS is metastasis-free survival).
- **Stated limitations:** generalisability; choice of end point (§Discussion).

**Row 16. Nakano H, Shiinoki T. *Separating Ranking Signal, Incremental Feature Value, and Evaluation-Induced Optimism in Breast MRI Treatment-Effect Analysis: Foundation Model and Radiomic Representations*. J Imaging Inform Med (2026).** [doi:10.1007/s10278-026-02344-w](https://doi.org/10.1007/s10278-026-02344-w). Version read: **abstract only** (PubMed). Peer reviewed.
- **Imaging modality:** pretreatment dynamic contrast-enhanced (DCE) breast MRI from the I-SPY2 RCT, accessed through the MAMA-MIA dataset.
- **Sample size:** (Abstract) "The human epidermal growth factor receptor 2-negative cohort (n = 739)". This was split into 370 for training and 369 for evaluation.
- **Representation method:** clinical variables, radiomics, and BiomedCLIP foundation-model features (Abstract: "Six clinical, radiomic, and foundation-model configurations were evaluated against one common imaging-free doubly robust score").
- **Estimators:** doubly robust scoring with RATE and AUTOC (area under the targeting operator characteristic). Further detail is UNVERIFIED.
- **Tuning of estimators:** UNVERIFIED (abstract only).
- **Source of the true effect:** none (RCT).
- **Performance measures:** RATE / AUTOC with bootstrap uncertainty and Holm adjustment.
- **Main result (null):**
  - (Abstract) "No configuration demonstrated treatment-effect prioritization after Holm adjustment across six tests."
  - Reusing the same sample inflated performance: "same-sample model development and evaluation increased apparent RATE in all six configurations".
- **Stated limitations:** (Abstract) "These findings do not establish incremental imaging value and do not demonstrate absence of treatment-effect heterogeneity."

**Row 17. Wei Y et al. *Individualized Treatment Effect Inference of Head and Neck Cancer with Multimodal Data*. APSIPA Trans Signal Inf Process 15(2) (2026).** [doi:10.1108/atsip-06-2025-0051](https://doi.org/10.1108/atsip-06-2025-0051). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** pretreatment CT from the public RADCURE dataset.
- **Sample size:** (Abstract) "comprising 3,346 HNC cases with CT scans and multiple clinical variables". HNC is head and neck cancer.
- **Representation method:**
  - A 3D Swin Transformer or 3D ResNet18 backbone, with bi-stage adaptive instance normalisation (Bi-AdaIN) fusion of the clinical factors.
  - This is an encoder swap with the rest held fixed. Quote (§Results): "the 3D Swin Transformer backbone consistently yields better results than the 3D ResNet18".
- **Estimators:**
  - A multi-treatment survival network with either adversarial or mutual-information disentanglement.
  - Comparators: simple concatenation and adversarial training.
- **Tuning of estimators:** fixed optimiser settings (AdamW, learning rate 1×10⁻⁴). Only λ was searched (§Experimental setup: "The hyperparameter λ was determined through a grid search.").
- **Source of the true effect:** none. The data are observational.
- **Performance measures:**
  - Factual MSE and mean absolute error (MAE), and the bias-adjusted treatment effect (BATE).
  - Quote (§Causal Effect Estimation): "Since ground-truth counterfactuals are unobservable, we evaluated the model’s ability to estimate causal effects using the Bias-Adjusted Treatment Effect (BATE)".
  - **Concern (my reading):** as defined, BATE is the gap between the model's ATE and the *unadjusted* observed difference. The authors write "A small BATE means the model has successfully adjusted for the initial differences between the treatment groups." Under confounding, a well-adjusted estimate need not match the naive difference. So BATE does not measure accuracy against a known effect.
- **Main result:** mutual-information disentanglement gave the lowest BATE, with a small loss in factual MAE and MSE (§Results).
- **Stated limitations:** (§Discussion) "our study is retrospective and relies on the RADCURE dataset". The radiotherapy-plus-EGFR-inhibitor arm is small (EGFR is epidermal growth factor receptor).

**Row 18. Yuan Z et al. *Radiomics-based causal machine learning for exploratory treatment-effect estimation of neoadjuvant chemotherapy cycle intensity in osteosarcoma: a proof-of-concept study*. BMC Med Imaging 26 (2026).** [doi:10.1186/s12880-026-02533-7](https://doi.org/10.1186/s12880-026-02533-7). Version read: PMC copy. Peer reviewed.
- **Imaging modality:** pretreatment T1-weighted MRI.
- **Sample size:** (Abstract) "This retrospective single-center study included 34 patients with osteosarcoma".
- **Representation method:** radiomic features selected by the least absolute shrinkage and selection operator (LASSO) with 10-fold cross-validation, keeping 14 features.
- **Estimators:** S-, T- and X-learners, with AutoGluon base models.
- **Tuning of estimators:** (§Causal machine learning framework…) "model training was implemented using the AutoGluon framework to provide a standardized exploratory modeling workflow with reduced dependence on manual hyperparameter tuning".
- **Source of the true effect:** none. The data are observational.
- **Performance measures:** AUC, F1 score and accuracy for the outcome models, and the ATE with a confidence interval.
- **Main result (failure):**
  - (§Results) The S-learner and X-learner gave negative ATE estimates and the T-learner a positive one. Quote: "S-Learner and X-Learner yielding negative estimates (-0.081 and − 0.107, respectively) and the T-Learner yielding a small positive estimate (0.020)".
  - The training AUCs of the T-learner components were 0.500.
- **Stated limitations:** (Abstract) "the findings should be regarded as hypothesis-generating rather than clinically actionable".

**Row 19. Aknin E, Larey A, et al. (CEGIR). *Harnessing Digital Pathology And Causal Learning To Improve Eosinophilic Esophagitis Dietary Treatment Assignment*. arXiv:2304.07787v1 (2023).** [arXiv:2304.07787v1](https://arxiv.org/abs/2304.07787v1). Version read: arXiv v1. Preprint.
- **Imaging modality:** whole oesophageal biopsy slides, processed by an AI histology platform.
- **Sample size:** (p. 1) "112 symptomatic adults aged 18-60 years with active EoE". These patients were randomised to one of two elimination diets. EoE is eosinophilic oesophagitis.
- **Representation method:** AI-derived histological features (p. 1: "we utilize AI for inferring histological features from the entire biopsy slide").
- **Estimators:** S- and T-learners with multilayer perceptron or XGBoost base models.
- **Tuning of estimators:**
  - (p. 6) "We trained both learners with different architectures and various hyperparameters and reported the best results."
  - The best configuration was therefore selected on the same 6-fold cross-validation used for evaluation.
- **Source of the true effect:** none. The policy value was estimated from the RCT.
- **Performance measures:** policy value (improvement rate) against random, single-diet and peak-eosinophil-count rules.
- **Main result:** (p. 1) "the best treatment strategy was obtained using T-learner with two XGBoost modules". The authors claim "our causal model yields a significantly better improvement rate of 58.4%".
- **Stated limitations:** a small single trial. The optimism from configuration selection is not discussed.

**Row 20. Xiao S, Klein L, Petersen J, Vollmuth P, Jaeger PF, Maier-Hein KH. *Enhancing predictive imaging biomarker discovery through treatment effect analysis*. WACV 2025.** [arXiv:2406.02534v2](https://arxiv.org/abs/2406.02534v2); [doi:10.1109/wacv61041.2025.00443](https://doi.org/10.1109/wacv61041.2025.00443). Version read: arXiv v2. Peer reviewed (WACV, Winter Conference on Applications of Computer Vision).
- **Imaging modality:**
  - Colour MNIST (CMNIST), a coloured version of the MNIST handwritten-digit images.
  - Bird photographs (CUB-200-2011).
  - Dermoscopy (ISIC 2018).
  - 3D lung CT (NSCLC-Radiomics).
- **Sample size:**
  - ISIC: 2,594 training images and 100 evaluation images.
  - NSCLC: 415 CT volumes, with 332 used for 5-fold cross-validation and 83 for testing.
  - CUB: 5,994 training and 5,794 test images (p. 5).
  - CMNIST: size not extracted.
- **Representation method:** a learned convolutional encoder (p. 3: "we modify a TARNet model [45], originally designed for tabular inputs").
- **Estimators:** a two-headed TARNet against a single-head baseline.
- **Tuning of estimators:** UNVERIFIED. Implementation details are in Supplement A.4, which is not in the arXiv PDF.
- **Source of the true effect:** synthetic outcomes from annotated or radiomic image features.
  - Quote (p. 3): "the outcome data Yi used in our experiments are simulated with image features from ground truth annotations and randomly assigned treatments T".
  - The outcome is linear, with prognostic and predictive strengths varied.
  - There is no confounding (p. 5: "We split all datasets randomly into two equally sized subsets").
- **Performance measures:** the t-value ratio between the predictive and prognostic terms of the estimated CATE in a treatment-interaction regression.
  - Bounds come from plugging in the ground-truth biomarkers. This is an oracle-feature bound on the evaluation statistic.
  - Attribution maps are also used.
- **Main result:** the two-headed model exceeds the baseline on all datasets.
- **Weakness (p. 8):** "weaker performance is observed for CUB200-2011, ISIC 2018, and NSCLC-Radiomics, particularly when bpred /bprog is high".
- **Stated limitations:** (p. 8) "due to the current unavailability of public RCT image datasets with verified predictive imaging biomarkers". Only a linear biomarker–outcome relation is used, and confounding is left as future work.
- **Code and licence:** code on GitHub (MIC-DKFZ/predictive_image_biomarker_analysis), Apache License 2.0 (LICENSE file).

**Row 21. Jiang Z, Hou Z, Liu Y, Ren Y, Li K, Carlson D. *Estimating Causal Effects using a Multi-task Deep Ensemble* (CMDE). ICML 2023.** [arXiv:2301.11351](https://arxiv.org/abs/2301.11351). Version read: arXiv; the version number was not recorded (unversioned URL). The arXiv comment says the paper was published at ICML 2023. Peer reviewed.
- **Imaging modality:** chest radiographs from a public COVID-19 image collection.
- **Sample size:** (App. D.3.1) "After data cleaning and imputation, 857 samples are used in our analysis". The split was 40:20:40.
- **Representation method:**
  - A convolutional neural network on the images, and fully connected networks on the tabular data.
  - The inputs were compared: image only, demographics only, or both (CMDE-mul).
- **Estimators:**
  - The causal multi-task deep ensemble (CMDE).
  - Comparators: counterfactual regression network (CFRNet), deep counterfactual network with propensity dropout (DCN-PD) and DONUT (a deep orthogonal network for estimating unconfounded treatment effects).
- **Tuning of estimators:** fixed per-model hyperparameters are listed (App. Table 3: "Model hyperparameters used for CMDE and other deep causal benchmark models"). No search procedure is reported.
- **Source of the true effect:**
  - Synthetic potential outcomes, linear with Kronecker-product interactions between demographics and diagnosis-category labels (App. D.3.1: "For image, we categorize the diagnosis of the X-ray into the following categories").
  - The effect therefore depends on image *labels*, which the network must infer from pixels.
  - Confounding: logistic propensity on the covariates, five imbalance levels, plus a randomised setting (App.: "In randomized study setting, treatment does not depend on any covariates.").
- **Performance measures:** √PEHE (square root of PEHE).
- **Main result:** (p. 8) "CMDE-mul achieves the lowest PEHE compared to other benchmarks with only the X-ray images as covariates".
- **Stated limitations:** none specific to the image experiment.
- **Code, data and licence:**
  - Repository jzy95310/ICK, MIT licence (LICENSE file).
  - The paper says "All other files and scripts are released under a CC BY-NC-SA 4.0 license." Individual images carry their own licences.

**Row 22. Schulte R, Rügamer D, Nagler T. *Adjustment for Confounding using Pre-Trained Representations*. ICML 2025, PMLR 267:53557–53580.** [arXiv:2506.14329v1](https://arxiv.org/abs/2506.14329v1). Version read: arXiv v1. Peer reviewed.
- **Imaging modality:** paediatric chest radiographs (Kermany et al. data).
- **Sample size:** (p. 19) "This reduces the effective sample size to 3,769 chest X-rays." The CNN comparison used 500 or all 3,769 images.
- **Representation method:**
  - Frozen 1024-dimensional last-layer features from TorchXRayVision DenseNet-121 models (DenseNet is a densely connected convolutional network).
  - Training data did not include the study images (p. 19).
  - Intrinsic dimension was compared across five pre-trained encoders.
  - CNNs trained from scratch were the alternative.
- **Estimators:**
  - Naive and oracle estimators.
  - S-learners with linear, lasso, random forest or neural-network outcome models.
  - DML with the same nuisance learners.
  - Quote (p. 19): "The Oracle estimator uses a linear regression of outcome on both treatment and the true label".
- **Tuning of estimators:**
  - Lasso penalties were chosen by cross-validation (p. 20).
  - Random forests used scikit-learn defaults, with the number of trees "varied in certain experiments to improve numerical stability" (p. 20).
  - The neural networks were fixed at depth 100 and width 50. The from-scratch CNN used early stopping (p. 21).
  - No systematic search is reported.
- **Source of the true effect:** synthetic outcome with a constant effect (p. 19: "In all of the experiments, the true average treatment effect was chosen to be two.").
  - Label confounding: pneumonia raises the treatment probability, 0.7 against 0.3 (p. 7: "children with pneumonia have a higher chance of receiving treatment compared to healthy children").
  - Complex confounding is defined on 5-dimensional AE codes of the pre-trained features themselves (p. 19: "we first train an autoencoder (AE) with 5-dimensional latent space on the pre-trained representations").
- **Performance measures:** bias and 95% confidence-interval coverage over 5 simulation repeats.
- **Main result:**
  - DML with neural-network nuisances had good coverage. S-learners did not (p. 8: "While the S-Learner’s confidence intervals are too optimistic, the DML estimator shows high coverage").
  - Pre-trained features beat CNNs trained from scratch inside DML (p. 9): pre-training "yields unbiased ATE estimates and well-calibrated confidence intervals, while DML without pre-training (DML (CNN)) does not".
  - Lasso and random-forest nuisances were biased.
- **Stated limitations:**
  - (p. 9) "we focused on the estimation of the ATE in this paper".
  - Only a single non-tabular source of confounding was studied.
- **Code and licence:** code on GitHub (rickmer-schulte/Pretrained-Causal-Adjust), MIT licence (LICENSE file).

---

## 3. Synthesis

**Established**

1. **One family of benchmarks has stroke lesions and a known effect.**
   - InterSynth and Giles et al. 2025 are the only benchmarks found that simulate treatment effects from real stroke lesion anatomy with a known ground truth (rows 1, 2).
   - The Nachev group's precursor (row 3) simulated ATE detection only.
   - Within this framework, richer lesion representations beat vascular-territory labels in balanced accuracy, even under strong simulated confounding (row 1).
   - However, the result is conditional on a generator in which responsiveness *is* a function of voxel-level overlap. The comparator (randomisation with a two-category baseline) is a design choice, not a tuned rival (row 1).
2. **Real-image ITE models are judged without a ground truth.** Every ITE model on real images uses one of these proxies:
   - ATE in predicted-responder subgroups of held-out RCTs (rows 9, 15);
   - uplift bins or bounds (rows 10, 11);
   - C-for-benefit (row 4);
   - RATE (row 16);
   - policy value (rows 8, 19);
   - BATE (row 17).
   None checks ITE accuracy directly.
3. **Imaging adds little in the two most rigorous RCT analyses.**
   - In MR CLEAN, CT foundation-model features did not improve C-for-benefit, which stayed around 0.55. The model also assumed no treatment interaction (row 4).
   - In I-SPY2, no clinical, radiomic or foundation-model configuration showed treatment-effect prioritisation once evaluation was kept independent (row 16).
   - Conventional imaging-marker subgroup analyses of stroke trials were also null or mixed: perfusion–diffusion mismatch in LASTE (row 6), and WML volume in MR CLEAN-MED except for aspirin-related sICH (row 5).
4. **Shared-representation (TARNet-like) multi-head networks are the default image architecture** (rows 9, 10, 11, 20). The comparators are usually other neural causal models with the same encoder (rows 8, 21) or simple linear and Cox T-learners (row 9). CEVAE- or Dragonnet-style image models with medical data were not found (search log row 29).

**Contested**

1. **Tuning and selection.**
   - Equal tuning effort for comparators is documented only in row 9.
   - Several studies select the best configuration on the evaluation folds (rows 1, 19).
   - Some report only fixed hyperparameters (rows 4, 8, 10, 21, 22).
   - The seed changed from nested-CV tuning (arXiv v1) to default settings (published version) (row 1).
   - Row 16 shows directly that reusing the same sample inflates RATE.
2. **Meta-learner instability in small samples.** S-, T- and X-learners gave ATEs of opposite sign at n = 34 (row 18). S-learner logistic regression was below chance in the seed's own results (row 1).
3. **Metrics that do not measure the effect.** BATE as defined in row 17 rewards agreement with the unadjusted contrast. Factual AUC or MSE (rows 7, 8, 12) does not measure the error in effect estimation.

**Missing**

1. **No semi-synthetic benchmark combines all four features** (see the table in section 4):
   - real medical images;
   - confounding;
   - non-linear heterogeneity;
   - a public release of the generator.

   The nearest candidates each lack one or more features:
   - InterSynth lacks a tabular-covariate block and has binary outcomes only.
   - Xiao 2025 (row 20) has no confounding.
   - CMDE (row 21) uses diagnosis labels, not image features.
   - Schulte 2025 (row 22) has a constant ATE.
2. **No study on medical images formally separates representation error from estimator error.** See section 4.
3. **No time-to-event semi-synthetic image benchmark was found.** Only real survival analyses exist (rows 15, 17).
4. **No study used a stroke RCT with raw images *and* interaction terms** (the closest is row 4, which assumed homogeneity).
5. **Overlap and calibration of the propensity score on image representations are not assessed in any included study.** Row 13 uses posterior predictive checks only.
6. **Causal representation learning applied to treatment effects in medical images was not found** beyond the methods in rows 13 and 22 (near-miss N18 is a general survey).

---

## 4. Brief-specific answers

### 4a. Semi-synthetic image benchmarks with known effects

| Benchmark (row) | Modality | Sample size | How the effect is generated | Confounding mechanism | Code / data | Licence |
|---|---|---|---|---|---|---|
| Giles 2025 / InterSynth (1, 2) | DWI lesion masks and disconnectomes (MNI) | 4,119 images, 2,830 patients. Per-network trials: 31–495 (masks), 297–3,078 (disconnectomes) | Binary outcome. The deficit is lesion overlap ≥5% with one of 16 NeuroQuery networks. Responsiveness is set by overlap with receptor- or transcriptome-defined subnetworks. Treatment effect and recovery noise are added | Observable: allocation ramp along the lesion-centroid axis (b_obs; deterministic above 0.5). Unobservable: allocation tied to the true optimal treatment (b_un_obs) | Code, lesion masks and atlases on GitHub | CC BY-NC-SA 4.0 (README and LICENCE file). InterSynth chapter: UNVERIFIED |
| Xu 2018 (3) | DWI lesion maps | 1,172 | Imposed responder fraction, or lesion shrinkage passed through a trained classifier; real gaze outcome. Effect size only (ATE) | None (randomised by design) | Not stated | – |
| Xiao 2025 (20) | CMNIST, CUB, ISIC 2018 dermoscopy, NSCLC CT | ISIC 2,594/100; NSCLC 415; CUB 11,788 | Linear outcome in annotated prognostic and predictive features, with varied strength | None (50:50 random) | GitHub | Apache-2.0 (code); dataset licences not read |
| CMDE (21) | COVID-19 chest radiographs | 857 | Linear outcome with Kronecker interactions of demographics and diagnosis-category labels | Logistic propensity on covariates, five imbalance levels; also randomised | GitHub (ICK) | MIT (repo); scripts CC BY-NC-SA 4.0; images individually licensed |
| Schulte 2025 (22) | Paediatric chest radiographs | 3,769 | Constant ATE = 2 plus a confounder term | Label (pneumonia) confounding; "complex" confounding on AE codes of the pre-trained features | GitHub | MIT |
| Pölsterl 2021 (13) | T1 MRI → 19 FreeSurfer volumes (UK Biobank) | 11,800 | Sparse linear-logistic effects of the volumes | Unobserved cluster confounder from principal components; age as observed confounder; strength varied | GitHub | GPL-3.0 |
| Li & Kosorok 2023 (14) | Synthetic 40×40 images (not real) | n varies; 100 replications | Linear functional model | None stated | Not checked | – |

### 4b. Is there work that separates representation error from estimator error?

**No study on medical images reports a formal decomposition of effect-estimation error into representation and estimator components.** The closest designs are below.

**Oracle features:**
- Row 22 has an oracle that adjusts for the true confounding label. It compares this with pre-trained features under several nuisance learners. It also compares pre-trained encoders against CNNs trained from scratch with DML held fixed. This is the cleanest encoder-swap with a fixed estimator. However, it covers the ATE only, and its "complex" confounding is defined on the representation itself.
- Row 13 has an oracle that includes all confounders, against a substitute confounder, with a fixed logistic estimator. The features there are FreeSurfer volumes, not learned representations.
- Row 20 plugs the ground-truth biomarkers into its evaluation regression to give upper and lower bounds. This is an oracle for the *evaluation statistic*, not for the CATE error.

**Factorial representation × estimator grids without an oracle:**
- Row 1 evaluates 46 representations × 5 learners × S/T configurations against a known truth (Supp. Tables 4–7). The grid would allow a descriptive decomposition, but none is reported. No oracle representation is included, such as the true subnetwork-overlap features that generate the truth.

**Encoder swaps without a ground truth:**
- Row 4: SwinUNETR against SegResNet.
- Row 17: Swin against ResNet18.
- Row 16: six feature configurations against a common doubly robust score.

### 4c. Coverage of trial-based imaging HTE and ITRs for thrombectomy or thrombolysis

HTE is heterogeneous treatment effects.

**Included:**
- MR CLEAN with raw CT (row 4);
- MR CLEAN-MED with deep-learning WML volume (row 5);
- LASTE with perfusion mismatch (row 6).

**Near-misses:**
- MR PREDICTS, which is pre-window and uses hand-extracted imaging variables (N5);
- TRAM-DAG, MR CLEAN external validation with no imaging (N1);
- IST and CAST causal machine learning with no imaging, but an important null on the internal and external validity of 17 causal machine-learning methods (N2).

**No ITR for thrombolysis built from images was found.**

---

## 5. Excluded near-misses

| # | Citation and link | Reason for exclusion |
|---|---|---|
| N1 | Herzog L, Dürr O, et al. *Estimating ITEs in acute ischemic stroke with causal transformation models (TRAM-DAG)*, [arXiv:2606.12623v3](https://arxiv.org/abs/2606.12623v3) (2026) | Full text read. Stroke ITEs validated against MR CLEAN, but the model uses clinical variables only; no imaging inputs |
| N2 | Chen H, Aebersold H, Puhan MA, Serra-Burriel M. *Causal Machine Learning Methods for Estimating Personalised Treatment Effects: Insights on validity from two large trials*, [arXiv:2501.04061v1](https://arxiv.org/abs/2501.04061v1); Am J Epidemiol 2026, doi:10.1093/aje/kwag065 | Abstract read. Stroke trials IST (International Stroke Trial) and CAST (Chinese Acute Stroke Trial), with 17 causal machine-learning methods, none of which validated. No imaging covariates. Relevant negative result for Brief 1 and Brief 3 |
| N3 | Doheim MF et al. *Individualized Treatment in Distal and Medium Vessel Occlusion Stroke…*, Ann Neurol 2026, [doi:10.1002/ana.78168](https://doi.org/10.1002/ana.78168) | Full text read. Observational elastic net with inverse probability of treatment weighting and a T-learner comparison; perfusion and infarct volumes were excluded for missingness, so no image-derived inputs |
| N4 | Chen H et al. *Endovascular Thrombectomy for Minor Ischemic Stroke: A Machine Learning Study of Treatment Effect Heterogeneity*, AJNR 2026, [doi:10.3174/ajnr.A9622](https://doi.org/10.3174/ajnr.A9622) | Abstract read. Causal forest on the US Nationwide Readmissions Database; no imaging |
| N5 | Venema E et al. *Selection of patients for intra-arterial treatment for acute ischaemic stroke…* (MR PREDICTS), BMJ 2017, [doi:10.1136/bmj.j1710](https://doi.org/10.1136/bmj.j1710) | Abstract read. Pre-2019. Ordinal regression on clinical and hand-scored radiological variables from MR CLEAN and IMS III (Interventional Management of Stroke III); not image-derived representations |
| N6 | Lou B et al. *An image-based deep learning framework for individualizing radiotherapy dose*, Lancet Digit Health 2019, [doi:10.1016/S2589-7500(19)30058-5](https://doi.org/10.1016/S2589-7500(19)30058-5) | Full text (PMC) read. CT "Deep Profiler" prognostic model used to set dose. No counterfactual estimand or confounding adjustment; prognostic, not a causal effect |
| N7 | Li X et al. *CRCNet: Deep-learning models for survival and benefit of adjuvant chemotherapy in stage II/III colorectal cancer*, [arXiv:2111.03532v1](https://arxiv.org/abs/2111.03532v1) | Full text read. Treatment benefit inferred by stratifying a prognostic risk score in observational cohorts, with no confounding adjustment (p. 13: "Despite the potential confounding between treatment allocations and clinical risk factors") |
| N8 | Jerzak CT, Johansson F, Daoud A. *Image-based Treatment Effect Heterogeneity*, CLeaR 2023, [arXiv:2206.06417v5](https://arxiv.org/abs/2206.06417v5) | Abstract read. Satellite images in anti-poverty RCTs; not medical |
| N9 | Jerzak CT, Daoud A. *CausalImages: An R Package…*, [arXiv:2310.00233v3](https://arxiv.org/abs/2310.00233v3) | Full text read. Software. "Although our examples focus on satellite images"; no medical benchmark |
| N10 | Klaassen S et al. *DoubleMLDeep: Estimation of Causal Effects with Multimodal Data*, [arXiv:2402.01785v1](https://arxiv.org/abs/2402.01785v1) | Abstract read. Semi-synthetic text and image confounders, not medical images. Relevant design for the representation question |
| N11 | Thorat A et al. *I See, Therefore I Do: Estimating Causal Effects for Image Treatments* (NICE), [arXiv:2412.06810v1](https://arxiv.org/abs/2412.06810v1) | Abstract read. Images as treatments, not as covariates; non-medical semi-synthetic data |
| N12 | Shi L, Lyu Q. *SIRNET: Causal Adaptation of Pretrained Embeddings…*, [arXiv:2610.14011v1](https://arxiv.org/abs/2610.14011v1) | Abstract read (full text downloaded). Brain-MRI embeddings in the Anti-Amyloid Treatment in Asymptomatic Alzheimer's Disease (A4) trial used as *post-treatment surrogates* for the ATE; not pretreatment effect modifiers or CATE |
| N13 | Shimizu Y. *Econometrics with Pre-Trained Embeddings for Unstructured Data*, [arXiv:2607.17378v2](https://arxiv.org/abs/2607.17378v2) | Abstract read. Theory for embedding error in DML; economics applications, no medical images |
| N14 | Jesson A et al. *Identifying Causal-Effect Inference Failure with Uncertainty-Aware Models*, [arXiv:2007.00163v2](https://arxiv.org/abs/2007.00163v2) | Abstract read. Uncertainty for neural CATE models; the image experiments are not medical (MNIST-based benchmark not verified from full text) |
| N15 | Tangwiriyasakul C et al. *Deep generative computed perfusion-deficit mapping of ischaemic stroke*, [arXiv:2502.01334v2](https://arxiv.org/abs/2502.01334v2); Commun Biol 2026 | Abstract read. Cites the seed; lesion- and perfusion-deficit mapping, no treatment effects |
| N16 | Semantic Scholar forward citations of the seed: Brain Struct Funct 2025 meta-analysis of stimulation sites; Cephalalgia 2024 review; J Educ Health Sport 2026 review; *Deep Variational Lesion-Deficit Mapping* (arXiv:2305.17478) | Titles screened. Reviews or lesion-deficit mapping; no treatment-effect estimation |
| N17 | Spatio-temporal conditional diffusion models for MS lesion masks conditioned on treatments, [arXiv:2508.07006v1](https://arxiv.org/abs/2508.07006v1) (MICCAI 2025 LMID workshop) | Abstract read. Counterfactual image generation from RCT MRI; evaluated on factual lesion masks. Could be added as an "image-outcome" row in a later pass |
| N18 | Lu C. *A Survey on Causal Representation Learning and Future Work for Medical Image Analysis*, [arXiv:2210.16034v1](https://arxiv.org/abs/2210.16034v1) | Abstract read. Survey of causal representation learning for robustness and out-of-distribution generalisation; no treatment-effect estimation |
| N19 | Melnychuk V et al. *Orthogonal Representation Learning for Estimating Causal Quantities*, [arXiv:2502.04274v4](https://arxiv.org/abs/2502.04274v4) | Abstract read. Theory linking representations and Neyman-orthogonal learners; no medical-image experiment found in the abstract |
| N20 | Dai H et al. *Causal relationship between amyloid-beta accumulation and AD progression via counterfactual inference* (GVCNet), [arXiv:2307.01389v1](https://arxiv.org/abs/2307.01389v1) | Abstract read. The "treatment" is amyloid PET burden (an exposure), with no known-effect benchmark |
