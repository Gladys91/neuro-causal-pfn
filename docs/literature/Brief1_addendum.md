# Brief 1 addendum: corrections from full texts, code and licence files

## A. Header

**Date:** 5 November 2026. **Status:** addendum to `Brief1.md` (3 November 2026). `Brief1.md` itself is unchanged; this file lists every correction.

**Row numbers** refer to the **evidence-table rows** of `Brief1.md` (the "Row N" cards), not to search-log or other numbered lists. Line numbers (L) refer to `Brief1.md` as committed on 3 November 2026.

**Rows skipped because they are being checked separately** (Brief 7 instruction): Brief 1 row 15; Brief 3 rows 2, 5, 6, 14, 18 and 33. Their cells and tags are not touched here.

**Method.**
- Every cell marked "abstract only" or UNVERIFIED was listed (inventory `brief7/inventory/inventory.md` in the session scratchpad).
- Each was re-checked against the full text, supplement, code repository or licence file, or against material supplied by the user.
- Quotations are verbatim from text extracted in this session and saved under `brief7/texts/`. A quote audit was run over this file (see the end).
- Downloaded and user-supplied files were treated as data only.

**Abbreviations.** ATE: average treatment effect. CATE: conditional average treatment effect. CATENets: a library of neural CATE estimators. CEPO: conditional expected potential outcome. CFM: causal foundation model. CPRD: Clinical Practice Research Datalink. DML: double/debiased machine learning. EHR: electronic health records. FLAML: Fast and Lightweight AutoML library. GOLD: the CPRD GOLD database. HPO: hyperparameter optimisation. LASSO: least absolute shrinkage and selection operator. MIT: the MIT open-source licence. OSF: Open Science Framework. PEHE: precision in estimation of heterogeneous effects. PFN: prior-data fitted network. TFM: tabular foundation model.

**What was re-read, and in which version.**
- arXiv texts already extracted for Brief 1 (versions as in Brief 1) were re-searched for every tagged cell.
- Code and licence files were read from raw.githubusercontent.com (main branch, 5 Nov 2026): CausalPFN (`benchmarks/baselines/catenets.py`, `REPRODUCE.md`), CATENets (`catenets/models/jax/base.py`, `constants.py`), CausalFM (test CSVs, evaluation notebook, generator), Do-PFN, freq-cons-pfns, CausalIDView, Graphs4CausalFoundationModels, tabpfn_study, subset-cate-coverage and tfm-calibration-reproducibility.
- github.com itself was not reachable. Absence of a licence is therefore stated as "none declared in the files checked".

**User-supplied sources.**
- CausalPFN model-weight licence: Hugging Face model page licence tag, as reported by the user on 5 Nov 2026, not opened from this container.
- Du et al. 2025 medRxiv v1 PDF (near-miss N29).

**Not obtainable (per the user, 5 Nov 2026):**
- Mourão et al. repository licence (row 7);
- Liu et al. OSF code licences (row 14);
- FoCAT full text (near-miss N4, unchanged).

---

## B. Changed cells

Each row gives the cell's old text exactly as in the brief, its replacement, and the supporting page and quotation. Where a cell keeps its tag, the new text gives the reason. Full notes, with sources and extra quotations, are in `brief7/notes/` in the session scratchpad.

| Row | Field | Old value (exact; Brief line) | New value | Page or section | Quotation (verbatim, <25 words) |
|---|---|---|---|---|---|
| 1 | Comparators and tuning | (L87) \| Comparators and tuning \| EconML T-, S-, X-, DA-, Forest DR-, Forest DML learners: **FLAML AutoML on propensity and outcome models, 900 s budget, 3-fold CV** (p.35 §D.5: "Time budget of 900 seconds, (ii) K-fold cross-validation with K = 3"); feasible nuisance-level criterion (FLAML default loss; the CATE stage is not selected on a CATE criterion). CATENets TARNet, DragonNet, RA-Net: **grid of 16 configurations** (p.35: "Number of layers ∈ {2, 3}"); selection criterion not stated (UNVERIFIED). GRF: internal `tune` option (p.35: "The GRF implementation includes an internal tune option"). **BART untuned** (p.35: "BART, on the other hand, offers no comparable hyperparameter-tuning"). IPW. An untuned table (Table 6, EconML notebook defaults) is also given. TabPFN (latest at the time) as a regression proxy, and TabPFN fine-tuned 48 h on the causal prior (p.9). \| | EconML T-, S-, X-, DA-, Forest DR-, Forest DML learners: **FLAML AutoML on propensity and outcome models, 900 s budget, 3-fold CV** (p.35 §D.5: "Time budget of 900 seconds, (ii) K-fold cross-validation with K = 3"); feasible nuisance-level criterion (FLAML default loss; the CATE stage is not selected on a CATE criterion). CATENets TARNet, DragonNet, RA-Net: **grid of 16 configurations** (p.35: "Number of layers ∈ {2, 3}"); the paper does not state the selection criterion, but the released benchmark code selects the configuration with the **lowest validation loss on a held-out split of the training data** (CATENets `fit_and_select_params`; default validation share 0.3), a feasible, factual-outcome criterion, not a CATE criterion (code, main branch, read 5 Nov 2026). GRF: internal `tune` option (p.35: "The GRF implementation includes an internal tune option"). **BART untuned** (p.35: "BART, on the other hand, offers no comparable hyperparameter-tuning"). IPW. An untuned table (Table 6, EconML notebook defaults) is also given. TabPFN (latest at the time) as a regression proxy, and TabPFN fine-tuned 48 h on the causal prior (p.9). | catenets.py L51-55; base.py L266-267; base.py L305-306 | `self.model.fit_and_select_params(` ... `param_grid=PARAM_GRID,` / `# find lowest loss and set params` / `best_idx = jnp.array(losses).argmin()` / `X, y, X_val, y_val, val_string = make_val_split(` / `X, y, val_split_prop=val_split_prop, seed=seed` |
| 1 | Code and licence (model weights) | (L92) \| Code and licence \| https://github.com/vdblm/CausalPFN; `pip install causalpfn`. LICENSE file (raw.githubusercontent, main) is titled "CausalPFN License Version 1.0, April 2025" with Apache-2.0-style terms; README states "licensed under the Apache-2.0 License". Code (`src/causalpfn/causal_estimator.py`, main branch, read 3 Nov 2026) reduces dimension when features exceed the model maximum: "the model will apply PCA to reduce the dimensionality" (code comment; implemented with TruncatedSVD). Model-weight licence: UNVERIFIED (Hugging Face not opened). \| | \| Code and licence \| https://github.com/vdblm/CausalPFN; `pip install causalpfn`. LICENSE file (raw.githubusercontent, main) is titled "CausalPFN License Version 1.0, April 2025" with Apache-2.0-style terms; README states "licensed under the Apache-2.0 License". Code (`src/causalpfn/causal_estimator.py`, main branch, read 3 Nov 2026) reduces dimension when features exceed the model maximum: "the model will apply PCA to reduce the dimensionality" (code comment; implemented with TruncatedSVD). Model weights: Apache-2.0 (Hugging Face model page licence tag, as reported by the user on 5 Nov 2026; not opened from this container). \| | user report (verbatim, typo as typed) | "causa pfn License: apache-2.0" |
| 3 | Comparators and tuning | (L125) \| Comparators and tuning \| TabPFN-based S-, T-, X-learner and DML (TabPFN at defaults; no tuning described). EconML S-, T-, X-learner with **FLAML for 60 s per base learner** (p.22: "HPO is performed using FLAML where we tune the each base-learner for 60 seconds"); TARNet and DragonNet via CATENets (tuning not stated, UNVERIFIED); Causal Forest DML "tuned using exhaustive search" (p.22; criterion not stated). DoWhy given the **true graph** (an oracle-informed comparator). Selection criteria: FLAML default nuisance loss (feasible); others not stated. \| | TabPFN-based S-, T-, X-learner and DML (TabPFN at defaults; no tuning described). EconML S-, T-, X-learner with **FLAML for 60 s per base learner** (p.22: "HPO is performed using FLAML where we tune the each base-learner for 60 seconds"); TARNet and DragonNet via CATENets (UNVERIFIED: tuning not reported by the authors; §D.3.2, p.22, says only "implemented using CATENets"); Causal Forest DML "tuned using exhaustive search" (p.22; criterion not stated). DoWhy given the **true graph** (an oracle-informed comparator). Selection criteria: FLAML default nuisance loss (feasible); others not stated. | p.22; p.22 | "balance; also implemented using CATENets." / "Hyperparameters are tuned using exhaustive search." |
| 3 | Code and licence | (L130) \| Code and licence \| https://github.com/jr2021/Do-PFN (p.6). No LICENSE, LICENSE.md or LICENSE.txt at raw.githubusercontent (main/master): **licence UNVERIFIED**. \| | https://github.com/jr2021/Do-PFN (p.6). **No licence declared**: no LICENSE, LICENSE.md, LICENSE.txt, LICENCE, LICENCE.md, COPYING or LICENSE.rst file and no pyproject.toml, setup.py or setup.cfg at raw.githubusercontent (main and master), and the README contains no licence statement (checked 5 Nov 2026). (github.com itself was not reachable, so a licence stated elsewhere in the repository cannot be excluded.) | probe log | `jr2021/Do-PFN [main]: LICENSE=404 LICENSE.md=404 LICENSE.txt=404 LICENCE=404 LICENCE.md=404 COPYING=404 LICENSE.rst=404 pyproject.toml=404 setup.py=404 setup.cfg=404 README.md=200` |
| 4 | Sample sizes, covariates | (L143) \| Sample sizes, covariates \| Training: "Each training datasets contain 1024 data samples. The feature dimensions are also different across the datasets, ranging from 10 to 100" (p.27 §E.7). ACIC 2016: "4802 individuals and 58 covariates" (p.32). Test-set sizes for the ten synthetic datasets: not stated (UNVERIFIED). \| | Training: "Each training datasets contain 1024 data samples. The feature dimensions are also different across the datasets, ranging from 10 to 100" (p.27 §E.7). ACIC 2016: "4802 individuals and 58 covariates" (p.32). Ten synthetic test datasets (not stated in the paper; from the released repository): **1,024 units and 10 covariates each**; the evaluation notebook uses the first 80% (819 units) as context and the remaining 20% (205 units) for PEHE. | CSV header (each of the 10 files, 1,024 data rows); notebook | `x0,x1,x2,x3,x4,x5,x6,x7,x8,x9,treatment,outcome,y0,y1,ite` / `- Uses 80% as the training data and 20% as the test data for one dataset.` and `ratio = 0.8` / `train_text_split = int(y.shape[0] * ratio)` |
| 4 | Comparators and tuning | (L144) \| Comparators and tuning \| S-, T-, X-, DR-, RA-learner and TARNet from CATENets; CausalPFN and Do-PFN released checkpoints (p.25 §D.3: "we follow the implementation from https://github. com/AliciaCurth/CATENets"). **No tuning procedure described for comparators (UNVERIFIED; appear to be library defaults).** \| | S-, T-, X-, DR-, RA-learner and TARNet from CATENets; CausalPFN and Do-PFN released checkpoints (p.25 §D.3: "we follow the implementation from https://github. com/AliciaCurth/CATENets"). **UNVERIFIED: no tuning procedure reported by the authors** (§D.3, p.25, gives implementation sources only; the repository README lists no baseline-tuning script); possibly library defaults. | p.25 | "For the standard CATE setting baselines, we follow the implementation from https://github. com/AliciaCurth/CATENets/tree/main" |
| 4 | Extra advantages to the foundation model | (L145) \| Extra advantages to the foundation model \| Whether the ten synthetic test datasets were generated from the same family as the training prior is not stated; Appendix E, headed as synthetic data generation for standard CATE estimation, describes the training prior (p.26–27) (UNVERIFIED leakage risk). \| | Whether the ten synthetic test datasets were generated from the same family as the training prior is not stated; Appendix E, headed as synthetic data generation for standard CATE estimation, describes the training prior (p.26–27). The released test files (10 × 1,024 units, 10 covariates) match the default size of the released training generator (`gen_standard_syn.py`: `num_samples: int = 1024, num_features: int = 10`) and share its column names, but carry an extra `ite` column that this generator does not write, so they were made by a script not found in the repository. Leakage risk remains UNVERIFIED. | gen_standard_syn.py L707; gen_standard_syn.py L689-695; test CSV header | `def generate_single_dataset(dataset_id: int, num_samples: int = 1024, num_features: int = 10, ` / `df['treatment'] = A` / `df['outcome'] = Y` / `df['y0'] = Y0` / `df['y1'] = Y1` (no `ite` column) / `x0,x1,x2,x3,x4,x5,x6,x7,x8,x9,treatment,outcome,y0,y1,ite` |
| 5 | Venue and version | (L156) \| Venue and version \| Preprint (arXiv v2, 27 Nov 2025). Peer-review status UNVERIFIED. \| | Preprint (arXiv v2, 27 Nov 2025). UNVERIFIED: no peer-reviewed version found (arXiv record has no journal reference; Crossref title search and web search found none, 5 Nov 2026). | arXiv API | `<id>http://arxiv.org/abs/2505.20003v2</id>` and `<updated>2025-11-27T04:39:49Z</updated>`; the entry has no journal_ref element (absence, not a quotation) |
| 5 | Code and licence | (L168) \| Code and licence \| https://github.com/qinglong-tian/tabpfn_study; no LICENSE file at raw (main/master): **licence UNVERIFIED**. \| | https://github.com/qinglong-tian/tabpfn_study; **Creative Commons Attribution-NonCommercial 4.0 (CC BY-NC 4.0)**, stated in the README §License (no separate LICENSE file at raw main/master). | README L278 | `This code is offered under the [Attribution-NonCommercial 4.0 International](https://creativecommons.org/licenses/by-nc/4.0/) license.` |
| 6 | Comparators and tuning | (L182) \| Comparators and tuning \| Meta-learners with TabPFNv2 and with HPO base learners, "Hyperparameter optimization is run for 60 seconds on an H100 per propensity and outcome model using FLAML" (p.9, footnote 5); "specialized tree- and deep-learning-based methods" (identity and tuning not given in text, UNVERIFIED). \| | Meta-learners with TabPFNv2 and with HPO base learners, "Hyperparameter optimization is run for 60 seconds on an H100 per propensity and outcome model using FLAML" (p.9, footnote 5); "specialized tree- and deep-learning-based methods" (UNVERIFIED: identities shown only in the Fig. 9 legend, p.10; the text cites only Wager and Athey [33]; their tuning is not reported). | p.9 | "outperforming specialized tree- and deep-learning-based methods [33]" |
| 7 | Extra advantages to the foundation model | (L202) \| Extra advantages to the foundation model \| None; TabPFN and CausalPFN at defaults. Whether CausalPFN's optional temperature calibration was enabled is not stated (UNVERIFIED). \| | None; TabPFN and CausalPFN at defaults. UNVERIFIED: whether CausalPFN's optional temperature calibration was enabled is not reported by the authors (the text never mentions temperature or calibration of CausalPFN intervals); the code repository could not be located (URL printed with spaces). | p.19 | "Our code and simulations are available at https://github.com/franciscomourao/PFNs Causal Inference." |
| 8 | Code and licence | (L225) \| Code and licence \| Not checked (UNVERIFIED). \| | https://github.com/Valentyn1997/freq-cons-pfns (p.2, footnote). **No licence declared**: no LICENSE-type or packaging file at raw.githubusercontent (main and master) and no licence statement in the README (checked 5 Nov 2026; github.com not reachable). | p.2; probe log | "Code is available at https://github.com/ Valentyn1997/freq-cons-pfns." / `Valentyn1997/freq-cons-pfns [main]: LICENSE=404 LICENSE.md=404 LICENSE.txt=404 LICENCE=404 LICENCE.md=404 COPYING=404 LICENSE.rst=404 pyproject.toml=404 setup.py=404 setup.cfg=404 README.md=200` |
| 9 | Code and licence | (L244) \| Code and licence \| https://github.com/gabeschulman-nyu/subset-cate-coverage (p.11); licence UNVERIFIED. \| | https://github.com/gabeschulman-nyu/subset-cate-coverage (p.11); **MIT** (LICENSE file read). | LICENSE L1; LICENSE L3 | `MIT License` / `Copyright (c) 2026 Gabe Schulman, Lucius E.J. Bynum, Yoav Wald` |
| 11 | Code and licence | (L282) \| Code and licence \| https://github.com/MLAI-Yonsei/CausalIDView (p.1); licence UNVERIFIED. \| | https://github.com/MLAI-Yonsei/CausalIDView (p.1). **No licence declared for the repository's own code**: no LICENSE-type or packaging file at raw.githubusercontent (main and master), and the README gives none (checked 5 Nov 2026). The README states that foundation-model weights are not redistributed and keep their upstream licences. | README L97-98 | `Foundation-model source trees and weights are not redistributed. Their upstream` / `licenses and execution environments differ, and TabPFN-v3.5 access is gated.` |
| 12 | Code and licence | (L301) \| Code and licence \| Not checked (UNVERIFIED). \| | https://github.com/ArikReuter/Graphs4CausalFoundationModels (p.2, footnote). **No licence declared**: no LICENSE-type or packaging file at raw.githubusercontent (main and master) and no licence statement in the README (checked 5 Nov 2026; github.com not reachable). | p.2; probe log | "The code for our natively causal prior, model training, and our experiments is available at https://github.com/ ArikReuter/Graphs4CausalFoundationModels." / `ArikReuter/Graphs4CausalFoundationModels [main]: LICENSE=404 LICENSE.md=404 LICENSE.txt=404 LICENCE=404 LICENCE.md=404 COPYING=404 LICENSE.rst=404 pyproject.toml=404 setup.py=404 setup.cfg=404 README.md=200` |
| 13 | Comparators and tuning | (L313) \| Comparators and tuning \| TabPFN-2.5 meta-learners; others not described in text (UNVERIFIED). \| | TabPFN-2.5 meta-learners. UNVERIFIED: any other methods appear only in Fig. 27 and are not named in the text (§3.5, p.21; App. E.1). | p.21 | "observe that all TabPFN-3 meta-learners improve over TabPFN-2.5, with the top two spots occupied by T and S-Learners (Figure 27)" |
| 14 | Model and version | (L324) \| Model and version \| TabPFN (version not stated, UNVERIFIED). \| | TabPFN (UNVERIFIED: version not reported by the authors; p.9 states only that TabPFN "was implemented in Python"). | p.9 | "predictive models were developed in R, while the pretrained model TabPFN was implemented in Python." |
| 16 | Code and licence | (L364) \| Code and licence \| Code doi:10.5281/zenodo.23737378 (arXiv comment); licence UNVERIFIED. \| | Code: https://github.com/ebrahimkhaled/tfm-calibration-reproducibility, **MIT** (p.25, Code availability; LICENSE file read), archived on Zenodo doi:10.5281/zenodo.23737378. Per-replicate predictions and test results deposited at doi:10.5281/zenodo.23737416 under CC BY 4.0 (p.25, Data availability). | p.25; p.25; LICENSE L1 | "is available in a public GitHub repository (https://github.com/ebrahimkhaled/tfm-calibration-reproducibility) under the MIT licence, archived on Zenodo" / "deposited on Zenodo under a CC BY 4.0 licence (doi:10.5281/zenodo.23737416)" / `MIT License` |

**Sources for the changed cells.**

- Row 1: https://raw.githubusercontent.com/vdblm/CausalPFN/main/benchmarks/baselines/catenets.py (main branch, fetched 5 Nov 2026), lines 13-18 and 50-56; saved `brief7/texts/causalpfn_code_benchmarks_baselines_catenets.py.txt`
- Row 1: https://raw.githubusercontent.com/AliciaCurth/CATENets/main/catenets/models/jax/base.py (main, fetched 5 Nov 2026), lines 213, 248-257, 266-269, 286, 305-307; saved `brief7/texts/catenets_code_models_jax_base.py.txt`
- Row 1: https://raw.githubusercontent.com/AliciaCurth/CATENets/main/catenets/models/constants.py line 30; saved `brief7/texts/catenets_code_models_constants.py.txt`
- Row 1: Paper (for the old, unchanged parts): arXiv 2506.07918v2 p.35; `brief7/texts/b1_causalpfn_v2.pg.txt` line 2025
- Row 1: Which notebook runs the HPO arms: https://raw.githubusercontent.com/vdblm/CausalPFN/main/REPRODUCE.md and notebooks/causal_effect_full.ipynb cell 9 (`"TarNet (HPO)": TarNetBaseline(hpo=True)`); REPRODUCE saved `brief7/texts/causalpfn_REPRODUCE.md.txt`
- Row 1: user report `brief7/texts/user_causalpfn_weights_licence_userreport.txt` (page https://huggingface.co/vdblm/causalpfn, opened by the user, 5 Nov 2026). Not independently verified.
- Row 3: arXiv 2506.06039v3 §D.3.2 p.22; `brief7/texts/b1_dopfn.pg.txt` lines 1195-1203
- Row 3: Repository README (no baseline scripts listed): `brief7/texts/jr2021_Do-PFN_README.md.txt`
- Row 3: `brief7/texts/licence_probe_log.txt` (raw.githubusercontent.com HTTP status per file, run 2026-11-05T09:10Z)
- Row 3: `brief7/texts/jr2021_Do-PFN_README.md.txt` (README, main; `grep -i licen` gives 0 hits)
- Row 4: https://raw.githubusercontent.com/yccm/CausalFM/main/DATA_standard/standard_cate_TEST/cate_test_dataset_{1..10}.csv (fetched 5 Nov 2026; _0 and _11 return 404); row and column counts in `brief7/texts/causalfm_repo_testsets.txt`
- Row 4: https://raw.githubusercontent.com/yccm/CausalFM/main/evaluation/notebook/test_standard_cate.ipynb; saved `brief7/texts/causalfm_code_test_standard_cate.ipynb.txt` (JSON lines 39, 54-55, 93-94)
- Row 4: arXiv 2506.10914v3 §D.3 p.25; `brief7/texts/b1_causalfm.pg.txt` line 1371
- Row 4: `brief7/texts/causalfm_README.md.txt` (training and evaluation scripts listed; none for baselines)
- Row 4: https://raw.githubusercontent.com/yccm/CausalFM/main/DATA_standard/gen_standard_syn.py (fetched 5 Nov 2026) lines 681-695 and 707; saved `brief7/texts/causalfm_code_gen_standard_syn.py.txt`
- Row 4: test CSVs as in the row 4 sample-size note; `brief7/texts/causalfm_repo_testsets.txt`
- Row 5: arXiv API record, fetched 5 Nov 2026; saved `brief7/texts/arxiv_api_2609.03003_2505.20003_2506.07918.xml`
- Row 5: Crossref query `TabPFN One Model to Rule Them All`; saved `brief7/texts/crossref_query_zhang_tabpfn.json` (top 5 results unrelated)
- Row 5: https://raw.githubusercontent.com/qinglong-tian/tabpfn_study/main/README.md (fetched 5 Nov 2026) lines 276-278; saved `brief7/texts/qinglong-tian_tabpfn_study_README.md.txt`
- Row 5: `brief7/texts/licence_probe_log.txt`
- Row 6: arXiv 2511.08667v2 p.9-10; `brief7/texts/b1_tabpfn25.pg.txt` lines 599-600, 624-625
- Row 7: arXiv 2603.15928v2; `brief7/texts/b1_mourao.pg.txt` (grep -c -i 'temperature|calibrat' = 0); p.19 code statement line 726
- Row 8: arXiv 2603.12037v3 p.2 footnote; `brief7/texts/b1_melnychuk.pg.txt` line 127 (two-column interleaved); non-layout text `brief7/texts/b1_melnychuk.raw.txt` line 254
- Row 8: `brief7/texts/Valentyn1997_freq-cons-pfns_README.md.txt`
- Row 9: https://raw.githubusercontent.com/gabeschulman-nyu/subset-cate-coverage/main/LICENSE (fetched 5 Nov 2026); saved `brief7/texts/gabeschulman-nyu_subset-cate-coverage_LICENSE.txt`
- Row 11: https://raw.githubusercontent.com/MLAI-Yonsei/CausalIDView/main/README.md lines 95-99; saved `brief7/texts/MLAI-Yonsei_CausalIDView_README.md.txt`
- Row 12: arXiv 2602.14972v3 p.2 footnote; `brief7/texts/b1_reuter_partial.pg.txt` line 112 (two-column interleaved); non-layout text `brief7/texts/b1_reuter_partial.raw.txt` line 146
- Row 12: `brief7/texts/ArikReuter_Graphs4CausalFoundationModels_README.md.txt`
- Row 13: arXiv 2605.13986v2 §3.5 p.21; `brief7/texts/b1_tabpfn3.pg.txt` lines 1406-1407
- Row 14: arXiv 2604.23465v1 p.9; `brief7/texts/b1_liu_ibd.pg.txt` line 282
- Row 16: arXiv 2610.39065v1 p.25 (Code and Data availability); `brief7/texts/b1_ebrahim_calib.pg.txt` lines 1333-1336, 1350-1353
- Row 16: https://raw.githubusercontent.com/ebrahimkhaled/tfm-calibration-reproducibility/main/LICENSE (fetched 5 Nov 2026); saved `brief7/texts/ebrahimkhaled_tfm-calibration-reproducibility_LICENSE.txt`

## C. Tags that remain, with reasons

- **Row 3, Comparators and tuning:** TARNet/DragonNet tuning not reported by the authors (§D.3.2, p.22).
- **Row 4, Comparators and tuning:** no tuning procedure reported by the authors (§D.3, p.25); the repository has no baseline-tuning script.
- **Row 4, Extra advantages:** leakage risk. The test-set generating script is not in the repository, so in-family test data cannot be confirmed.
- **Row 5, Venue:** no peer-reviewed version found (arXiv, Crossref and web search on 5 Nov 2026).
- **Row 6, Comparators:** method identities shown only in Fig. 9; tuning not reported.
- **Row 7, Extra advantages:** whether CausalPFN temperature calibration was used is not reported; the repository could not be located.
- **Row 7, Code and licence:** repository licence not obtainable (user, 5 Nov 2026). Proposed cell wording: "licence UNVERIFIED: repository URL printed with spaces could not be resolved, and the licence could not be obtained (5 Nov 2026)".
- **Row 13, Comparators:** other methods only in Fig. 27.
- **Row 14, Model and version:** TabPFN version not reported by the authors.
- **Row 14, Code and licence:** OSF licences not obtainable (user, 5 Nov 2026). Proposed cell wording: "Code on OSF (osf.io/xj9pr, osf.io/DCJM6); licence UNVERIFIED: OSF not reachable from here and not obtainable (5 Nov 2026)".
- **Caveats (not tags):**
  - Rows 3, 8, 11 and 12: "no licence declared" is based on the root files and READMEs reachable at raw.githubusercontent.com. github.com was not browsable.
  - Row 1: the CATENets selection rule is from today's main branch, not a tagged release.
- **Row 15 (skipped):** all its tags, and the dependent §4.1 (L413) and §4.2 (L416) statements, await the separate check.

## D. Changes to the synthesis and answer sections that follow

Line 387 (§3 Established 1) and line 148 (Row 4) are given in section E. Each item gives the old text exactly, the new text, and the reason.

### S1-1. §3 Contested 1 (L393): depends on Row 4 'Extra advantages' (brief1_row4_extra_advantages.md)

Old (Brief1.md line 393, exact):

```
1. Whether CausalPFN's benchmark advantage reflects generality or prior–benchmark alignment: Reuter et al. attribute it to CausalPFN's prior "closely mimicking the RealCause data-generating process" (Row 12). Do-PFN and CausalFM evaluations also used test data from families close to their priors (Rows 3, 4).
```

New:

```
1. Whether CausalPFN's benchmark advantage reflects generality or prior–benchmark alignment: Reuter et al. attribute it to CausalPFN's prior "closely mimicking the RealCause data-generating process" (Row 12). Do-PFN's synthetic case studies reuse its prior's parameter distributions (Row 3); for CausalFM, the family of the synthetic test sets is not documented: the released test files match the training generator's default size but were produced by a script not in the repository (Row 4, UNVERIFIED).
```

Why: The old sentence stated as fact that CausalFM's tests came from families close to its prior, while the Row 4 cell had this as UNVERIFIED; the repository check confirms only the size match.

### S1-2. §4.4 tuned comparators (L424): depends on Row 1 'Comparators and tuning' (brief1_row1_comparators_and_tuning.md)

Old (Brief1.md line 424, exact):

```
- Tuned comparators used **feasible, nuisance-level** criteria with fixed budgets: FLAML 900 s, 3-fold CV (Rows 1, 10; R² and ROC-AUC in Row 10); FLAML 60 s per model (Rows 3, 6); FLAML 5-fold CV (Row 5). None selected the final CATE model with a CATE-targeted criterion (for example an R-loss or DR pseudo-outcome loss), and none used oracle selection.
```

New:

```
- Tuned comparators used **feasible** criteria with fixed budgets: nuisance-model losses with FLAML 900 s, 3-fold CV (Rows 1, 10; R² and ROC-AUC in Row 10); FLAML 60 s per model (Rows 3, 6); FLAML 5-fold CV (Row 5); and, for the CATENets networks in Row 1, the lowest validation loss over a 16-setting grid on a held-out 30% of the training data (from the released code). None selected the final CATE model with a CATE-targeted criterion (for example an R-loss or DR pseudo-outcome loss), and none used oracle selection.
```

Why: Adds the CATENets selection rule now settled from code; the conclusion (no CATE-targeted, no oracle selection) is unchanged.

### S1-3. §4.4 untuned comparators (L425): depends on Rows 3 and 4 'Comparators and tuning' (brief1_row3_…, brief1_row4_…)

Old (Brief1.md line 425, exact):

```
- Untuned or weakly tuned comparators: BART untuned (Row 1); XGBoost default "to limit computational burden" and misspecified logistic regression (Row 7); all arms at defaults (Row 11); CATENets defaults in CausalFM (Row 4, UNVERIFIED); Do-PFN's neural baselines (Row 3, UNVERIFIED). ACIC 2017 baselines were taken from challenge submissions (Row 5).
```

New:

```
- Untuned or weakly tuned comparators: BART untuned (Row 1); XGBoost default "to limit computational burden" and misspecified logistic regression (Row 7); all arms at defaults (Row 11). Tuning not reported by the authors: CausalFM's CATENets comparators (Row 4; possibly library defaults) and Do-PFN's TARNet and DragonNet (Row 3). ACIC 2017 baselines were taken from challenge submissions (Row 5).
```

Why: The two UNVERIFIED tags now state their reason (not reported by the authors).

### S1-4. §3 Missing 4 (L401): consistency with S1-2

Old (Brief1.md line 401, exact):

```
4. No study gives comparators equal, CATE-targeted tuning; all tuned arms used nuisance-level, feasible criteria with short budgets, and some arms were untuned (§4.4).
```

New:

```
4. No study gives comparators equal, CATE-targeted tuning; all tuned arms used feasible criteria (nuisance-model losses, or a factual validation loss for the CATENets networks in Row 1) with short budgets, and some arms were untuned (§4.4).
```

Why: 'Nuisance-level' does not describe the CATENets validation-loss selection.

### S1-5 (optional). §3 Established 3 (L389): depends on Row 7 'Extra advantages' (brief1_row7_extra_advantages.md, tag kept)

Old (Brief1.md line 389, exact):

```
3. Interval calibration is the main documented weakness of the direct models. CausalPFN credible intervals are overconfident out of prior (Row 1), under-cover the ATE in binary-outcome clinical simulations (54–68% at n = 1,000; Row 7), and lose coverage for group averages because unit-level errors are correlated (Row 9). PFN priors concentrate observed confounding near zero, which can prevent frequentist consistency for the ATE (Row 8).
```

New:

```
3. Interval calibration is the main documented weakness of the direct models. CausalPFN credible intervals are overconfident out of prior (Row 1), under-cover the ATE in binary-outcome clinical simulations (54–68% at n = 1,000; Row 7; whether CausalPFN's optional temperature calibration was used there is not reported), and lose coverage for group averages because unit-level errors are correlated (Row 9). PFN priors concentrate observed confounding near zero, which can prevent frequentist consistency for the ATE (Row 8).
```

Why: The coverage figure could depend on an unreported setting; flagging it keeps the claim traceable.

### No knock-on (checked)

- Licence cells (Rows 3, 5, 8, 9, 11, 12, 16): the synthesis and answers cite licences only for TabPFN weights (Rows 2, 6; L406). No change.
- Row 4 sample sizes: no synthesis line uses CausalFM test sizes.
- Row 5 peer-review status, Row 6 and Row 13 figure-only comparators, Row 14 TabPFN version: Established 2 already calls Rows 6 and 13 "vendor claims"; §4.5 cites Row 14 for ICI only. No change.
- Row 15 (skipped) dependents L413 and L416 are left to the separate check.


### S1-7 (optional). §4.1 EHR answer (L413): name the CPRD near-miss

Old (Brief1.md line 413, exact):

```
**No evidence for CATE estimation by pre-trained in-context models on EHR or claims data.** Closest items: Row 7 builds plasmode-style scenarios from a trial dataset and a tumour-bank cohort (ATE, binary, ≤1,000 patients, ≤8 binarised confounders); Row 14 applies TabPFN as an outcome model in a prospective multicentre research cohort (613 children, 29 predictors), validated only against a propensity-matched estimate; Row 15 uses a registry-trained TabPFN risk model to stratify an RCT (abstract only). Row 11 uses three RCTs (ACTG 175, Pennsylvania, Illinois) for null-effect tests. CaML (near-miss N3) uses "large-scale medical claims", but it is meta-trained inside that claims database to predict effects of unseen drugs, not an in-context model applied to a new dataset. No CPRD study was found.
```

New:

```
**No evidence for CATE estimation by pre-trained in-context models on EHR or claims data.** Closest items: Row 7 builds plasmode-style scenarios from a trial dataset and a tumour-bank cohort (ATE, binary, ≤1,000 patients, ≤8 binarised confounders); Row 14 applies TabPFN as an outcome model in a prospective multicentre research cohort (613 children, 29 predictors), validated only against a propensity-matched estimate; Row 15 uses a registry-trained TabPFN risk model to stratify an RCT (abstract only). Row 11 uses three RCTs (ACTG 175, Pennsylvania, Illinois) for null-effect tests. CaML (near-miss N3) uses "large-scale medical claims", but it is meta-trained inside that claims database to predict effects of unseen drugs, not an in-context model applied to a new dataset. No CPRD study using a pre-trained in-context model was found; the one CPRD causal-ML study screened (N29, a GOLD plasmode study of DML) uses LASSO nuisance models only.
```

Why: Makes explicit that the CPRD DML study was checked in full and uses no TFM.

## E. Independence correction (row 10 replication of CausalPFN)

### Facts used (all from p.1 author blocks; arXiv API agrees)

- Stith C, Rahmani H, Cresswell JC. *Causal Foundation Models*. arXiv:2609.03003v1 (2 Sep 2026; only version on 5 Nov 2026). p.1: Stith "Layer 6 AI, Toronto, Canada"; Rahmani "TD Bank Group, Toronto, Canada"; Cresswell "Layer 6 AI, Toronto, Canada". Text: `brief7/texts/b1_stith_cfm.txt` lines 1-10.
- Balazadeh V, Kamkari H, Thomas V, Li B, Ma J, Cresswell JC, Krishnan RG. *CausalPFN*. arXiv:2506.07918v2. p.1 affiliations "1 University of Toronto 2 Vector Institute 3 Layer 6 AI"; Kamkari, Thomas, Ma and Cresswell carry affiliation 3. Text: `brief7/texts/b1_causalpfn_v2.txt` lines 1-10.
- Shared author: **Jesse C. Cresswell**. Shared lab: **Layer 6 AI** (two of three Stith authors; four of seven CausalPFN authors).
- Stith et al. p.20: "We note that our CausalPFN results independently replicate the values reported by Balazadeh et al. (2025)". The paper states no link to the CausalPFN authorship next to this claim.
- Do-PFN (arXiv 2506.06039v3, p.1): Robertson J, Reuter A, Guo S, Hollmann N, Hutter F, Schölkopf B. Reuter et al. 2026 (arXiv 2602.14972v3, p.1): Reuter A, Dhir A, Diaconu C, Robertson J, Ossen O, Hutter F, Weller A, van der Wilk M, Schölkopf B. Shared: **Reuter, Robertson, Hutter, Schölkopf**. Texts: `brief7/texts/b1_dopfn.pg.txt`, `brief7/texts/b1_reuter_partial.pg.txt` (p.1).
- CausalPFN's authors include none of the six Do-PFN authors (author lists above).

Wording rule followed: state who the shared author is and which lab; no statement about motives.

### A. Required by Brief 7 item 3 (Brief 1)

#### A1. Brief 1 §3 Synthesis, Established 1 (L387)

Old (Brief1.md line 387, exact):

```
1. On standard semi-synthetic back-door benchmarks (IHDP, ACIC 2016, RealCause Lalonde), the released CausalPFN reaches CATE error comparable with or better than tuned meta-learners without any per-dataset tuning, and an independent replication reproduced its numbers (Rows 1, 10). Its average CATE rank is best in its own paper (2.30 vs 3.57) but second to a FLAML-tuned T-learner in the replication (1.75 vs 1.40), and it is not best on ACIC 2016 (Row 1: 0.92 vs X-learner 0.60) nor on Lalonde-PSID against a tuned T-learner (Row 10).
```

New:

```
1. On standard semi-synthetic back-door benchmarks (IHDP, ACIC 2016, RealCause Lalonde), the released CausalPFN reaches CATE error comparable with or better than tuned meta-learners without any per-dataset tuning, and a replication by Stith, Rahmani and Cresswell reproduced its numbers (Rows 1, 10). That replication is not independent of CausalPFN: Cresswell is a CausalPFN co-author, and Stith and Cresswell work at Layer 6 AI, the affiliation of four of the seven CausalPFN authors (Row 10). Its average CATE rank is best in its own paper (2.30 vs 3.57) but second to a FLAML-tuned T-learner in the replication (1.75 vs 1.40), and it is not best on ACIC 2016 (Row 1: 0.92 vs X-learner 0.60) nor on Lalonde-PSID against a tuned T-learner (Row 10).
```

Why: Brief 7 item 3: the synthesis called the replication independent.

#### A2. Brief 1 Row 10, Main result (L261)

Old (Brief1.md line 261, exact):

```
| Main result | PEHE ×10³ (p.20 Table 3): CPS CausalPFN 8.97 vs T-learner 9.04; **PSID T-learner 13.65 vs CausalPFN 14.00**; average PEHE rank T-learner 1.40 vs CausalPFN 1.75; Do-PFN 11.96/20.20; CausalFM 12.34/22.27. "our CausalPFN results independently replicate the values reported by Balazadeh et al. (2025)" (p.20). |
```

New:

```
| Main result | PEHE ×10³ (p.20 Table 3): CPS CausalPFN 8.97 vs T-learner 9.04; **PSID T-learner 13.65 vs CausalPFN 14.00**; average PEHE rank T-learner 1.40 vs CausalPFN 1.75; Do-PFN 11.96/20.20; CausalFM 12.34/22.27. The authors write that "our CausalPFN results independently replicate the values reported by Balazadeh et al. (2025)" (p.20). The replication is not independent of CausalPFN: Cresswell is a CausalPFN co-author, and Stith and Cresswell are at Layer 6 AI, as are four CausalPFN authors (p.1 of both papers). |
```

Why: Keeps the authors' verbatim quotation, attributes the word 'independently' to them, and states the shared author and lab.

#### A3. Brief 1 Row 10, Venue and version (L251)

Old (Brief1.md line 251, exact):

```
| Venue and version | Preprint (arXiv v1, Sep 2026). Authors at Layer 6 AI; Cresswell is a CausalPFN co-author (Row 1): not independent of CausalPFN. |
```

New:

```
| Venue and version | Preprint (arXiv v1, 2 Sep 2026). Stith and Cresswell at Layer 6 AI, Rahmani at TD Bank Group (p.1). Cresswell is a CausalPFN co-author (Row 1), and four of the seven CausalPFN authors list Layer 6 AI: not independent of CausalPFN. |
```

Why: Corrects 'Authors at Layer 6 AI' (Rahmani is at TD Bank Group) and adds the shared lab; the date is from the arXiv record.

#### A4. Brief 1 Row 4 (CausalFM), Failure modes (L148)

Old (Brief1.md line 148, exact):

```
| Failure modes | ACIC 2016 underperformance (above). Using the wrong identification prior raises PEHE (p.34 Table 9: IV data 0.422 correct vs 0.489 back-door). Authors: "The current evaluation is limited to synthetic and semi-synthetic data" (p.10). In external benchmarks CausalFM shrinks ATE towards zero (Row 10: ATE relative error 0.94 on Lalonde CPS). Binary outcomes, time-to-event, EHR: not evaluated. |
```

New:

```
| Failure modes | ACIC 2016 underperformance (above). Using the wrong identification prior raises PEHE (p.34 Table 9: IV data 0.422 correct vs 0.489 back-door). Authors: "The current evaluation is limited to synthetic and semi-synthetic data" (p.10). In a benchmark by authors who include CausalPFN co-author Cresswell (Row 10), CausalFM shrinks ATE towards zero (ATE relative error 0.94 on Lalonde CPS). Binary outcomes, time-to-event, EHR: not evaluated. |
```

Why: 'External benchmarks' implied a neutral evaluator; Row 10 is by authors outside CausalFM but including a CausalPFN co-author.


### B. Beyond what Brief 7 asked (same kind of error; for the coordinator to accept or drop)

#### B1. Brief 1 Row 3 (Do-PFN), Main result (L128)

**Goes beyond Brief 7 item 3.**

Old (Brief1.md line 128, exact):

```
| Main result | Synthetic: "Do-PFN significantly outperforms meta-learners (Künzel et al., 2019), a causal forest double machine learning (DML) approach" (p.8). RealCause: "strong performance among competitive baselines on three out of four RealCause datasets" (p.10). Numbers: figure only (Figs 3, 5). Independent numbers in Rows 1, 4, 10, 11, 12: e.g. IHDP PEHE 6.07 vs CausalPFN 0.58 (Row 1, p.40 Table 8). |
```

New:

```
| Main result | Synthetic: "Do-PFN significantly outperforms meta-learners (Künzel et al., 2019), a causal forest double machine learning (DML) approach" (p.8). RealCause: "strong performance among competitive baselines on three out of four RealCause datasets" (p.10). Numbers: figure only (Figs 3, 5). Numbers from other papers in Rows 1, 4, 10, 11 and 12: Row 1 is the CausalPFN paper; Row 10's authors include CausalPFN co-author Cresswell; Row 12 shares four authors with Do-PFN (Reuter, Robertson, Hutter, Schölkopf). E.g. IHDP PEHE 6.07 vs CausalPFN 0.58 (Row 1, p.40 Table 8). |
```

Why: 'Independent numbers' included Row 12, which shares four authors with Do-PFN, and Rows 1 and 10, which come from the CausalPFN group or include a CausalPFN co-author.


### C. Checked, no change needed (Brief 1)

- L390 (§3 Established 4), L419 (§4.3), L424 and L427 (§4.4): cite Row 10 without any claim of independence.
- §2b capability table (L366–380): Row 10 not cited.

## F. Near-miss updates

| Row | Field | Old value (exact; Brief line) | New value | Page or section | Quotation (verbatim, <25 words) |
|---|---|---|---|---|---|
| N29 | Near-miss N29, reason for exclusion | (L466) \| N29 \| Du et al. 2025, *Double Machine Learning for Causal Inference in High-Dimensional EHR* (medRxiv) \| https://doi.org/10.1101/2025.07.21.25331944 \| EHR plasmode DML study, but Crossref abstract mentions no TFM; full text not reachable (medRxiv blocked). \| | \| N29 \| Du M, Guo Y, Li X, Catala M, Pareto-Alhambra D 2025, *Double Machine Learning for Causal Inference in High-Dimensional Electronic Health Records* (medRxiv preprint v1, 22 Jul 2025; not peer reviewed) \| https://doi.org/10.1101/2025.07.21.25331944 \| Plasmode simulation on CPRD GOLD of an offset-based DML estimator for a log-odds ATE; nuisance models are cross-validated LASSO logistic regressions only. **No tabular foundation model or other pretrained model is used** (full text: 0 hits for "TabPFN", "foundation", "transformer", "pretrain"); ATE only, not CATE. \| | PDF p.5; PDF p.15; PDF p.6 | "The plasmode simulation was based on data from the Clinical Practice Research Datalink (CPRD) GOLD database" / "while we employed Lasso regression for nuisance model estimation, we did not evaluate alternative machine learning algorithms" / "The causal effects estimand we estimated for this study is the average treatment effect (ATE)" |

Source: user PDF `brief7/user_pdfs/du2025_medrxiv.pdf`, medRxiv preprint v1 (posted 22 Jul 2025, doi:10.1101/2025.07.21.25331944), not peer reviewed. Text `brief7/texts/user_du2025_medrxiv.txt`.

Author list as printed (p.1): 'Mike Du1, Yuchen Guo1, Xintong Li1, Marti Catala1, Daniel Pareto-Alhambra12'. Surnames as printed (p.1) match Crossref: Du, Guo, Li, Catala, Pareto-Alhambra. The only 'neural network' hit is a reference title (p.20). Directly relevant to Brief 1's application B (CPRD), but not a TFM study.

- **N4 (FoCAT):** unchanged. The full text could not be obtained (user, 5 Nov 2026).

## Quote audit (run 5 Nov 2026)

Quotations were extracted from the quotation column, the new values and the synthesis 'New' blocks. Each was matched against the session texts after normalising whitespace, hyphenation, soft hyphens and the publisher's download watermark.

- Matched exactly: **60** (56 in `brief7/texts/`; 4 in texts saved for Briefs 1–6, quoted in cells carried over from Brief1.md).
- Quotations of Brief1.md's own wording (old text carried into new cells): 0.
- Matched only in order across layout breaks; **manual check** done by eye in the layout text: 0.
- Not found: **0**.
- Quotation-column entries of 25 words or more: 0.
