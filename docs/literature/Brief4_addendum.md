# Brief 4 addendum: corrections from code

## A. Header

**Date:** 5 November 2026. **Status:** addendum to `Brief4.md` (3 November 2026). `Brief4.md` itself is unchanged; this file lists every correction.

**Row numbers** refer to the **evidence-table rows** of `Brief4.md` (the "Row N" cards), not to search-log or other numbered lists. Line numbers (L) refer to `Brief4.md` as committed on 3 November 2026.

**Rows skipped because they are being checked separately** (Brief 7 instruction): Brief 1 row 15; Brief 3 rows 2, 5, 6, 14, 18 and 33. Their cells and tags are not touched here.

**Method.**
- Every cell marked "abstract only" or UNVERIFIED was listed (inventory `brief7/inventory/inventory.md` in the session scratchpad).
- Each was re-checked against the full text, supplement, code repository or licence file, or against material supplied by the user.
- Quotations are verbatim from text extracted in this session and saved under `brief7/texts/`. A quote audit was run over this file (see the end).
- Downloaded and user-supplied files were treated as data only.

**Abbreviations.** CEPO: conditional expected potential outcome. CFM: causal foundation model. PFN: prior-data fitted network. SCM: structural causal model.

**What was re-read, and in which version.**
- CausalPFN arXiv v2 and the repository's `REPRODUCE.md` (main branch, 5 Nov 2026).
- Do-PFN arXiv v3 and its prior code (`priors/doscm.py`, `priors/playground_scm/scm.py`, `prior_data_example.py`; main branch, 5 Nov 2026).
- CausalFM repository test files and generator (main branch), for a knock-on to row 3.

**User-supplied sources:** none for Brief 4. **Not obtainable:** FoCAT full text (near-miss N4, unchanged).

---

## B. Changed cells

Each row gives the cell's old text exactly as in the brief, its replacement, and the supporting page and quotation. Where a cell keeps its tag, the new text gives the reason. Full notes, with sources and extra quotations, are in `brief7/notes/` in the session scratchpad.

| Row | Field | Old value (exact; Brief line) | New value | Page or section | Quotation (verbatim, <25 words) |
|---|---|---|---|---|---|
| 1 | Outcome types | (L77) - **Outcome types:** Continuous CEPO columns plus zero-mean noise (p.32: "we sample ϵt from a Gaussian"). No binary-outcome generator is described in the sections read (code not opened: **UNVERIFIED** whether binary base-table columns can be selected as CEPOs). Binary outcomes appear only in evaluation (p.8: "The outcome is whether a website visit occurred within two weeks (binary)."). | Continuous CEPO columns plus zero-mean noise (p.32: "we sample ϵt from a Gaussian"). No binary-outcome generator is described (p.31–32). UNVERIFIED whether binary base-table columns can be selected as CEPOs: not reported in the paper, and the repository's reproducibility guide (REPRODUCE.md) covers evaluation only, with no prior or training code. Binary outcomes appear only in evaluation (p.8: "The outcome is whether a website visit occurred within two weeks (binary)."). | REPRODUCE.md L3; p.32 | `While the README was a simple showcase of the package, this is an in-depth step-by-step guide to reproduce the results in the paper.` / "For our training, we sample ϵt from a Gaussian with" |
| 1 | Training scale | (L79) - **Training scale:** p.33: "The full model has approximately 20M parameters and is trained in two stages": a predictive phase (context up to 16K) then a causal phase (context 2,048). Number of prior datasets: not found in the sections read (**UNVERIFIED**). | p.33: "The full model has approximately 20M parameters and is trained in two stages": a predictive phase (context up to 16K) then a causal phase (context 2,048). Number of prior datasets: UNVERIFIED, not reported by the authors (only training time is given, p.33). | p.33 | "trained for at most one week for the initial phase, and two days on an H100 for the second phase." |
| 2 | Outcome types | (L89) - **Outcome types:** Continuous outcome; binary treatment (p.3: "performing an intervention do(t) for a binary variable T"). How T is binarised in the prior: not described in the sections read (**UNVERIFIED**). | Continuous outcome; binary treatment (p.3: "performing an intervention do(t) for a binary variable T"). How T is binarised in the prior is not described in the paper; in the released code, the simulated treatment node is split at a per-dataset threshold, either a random interior value (`extreme` strategy) or the mean (`mean` strategy), and values below and above it are set to two treatment levels; with `zero_one_treatment` these are recoded to 0/1 by comparison with the mean (code, main branch, read 5 Nov 2026). Which strategy trained the released checkpoints is not stated (UNVERIFIED). | doscm.py L99-100; scm.py L112-113; scm.py L117-118 | `# sample observational dataset and binarize the treatment` / `endo_obs, exo_obs = self.scm.get_next_sample(binarize=True, graph=scm_graph)` / `if self.binary_strategy == 'extreme':` / `t_thresh = np.random.choice(treatment[b][not_min_max])  # the threshold cannot be the min or max value of the treatment` / `elif self.binary_strategy == 'mean':` / `t_thresh = (treatment[b][not_min_max]).mean()` |

**Sources for the changed cells.**

- Row 1: arXiv 2506.07918v2 p.32; `brief7/texts/b1_causalpfn_v2.pg.txt` line 1858
- Row 1: https://raw.githubusercontent.com/vdblm/CausalPFN/main/REPRODUCE.md (fetched 5 Nov 2026); saved `brief7/texts/causalpfn_REPRODUCE.md.txt`
- Row 1: arXiv 2506.07918v2 §D.2 p.33; `brief7/texts/b1_causalpfn_v2.pg.txt` line 1907
- Row 2: https://raw.githubusercontent.com/jr2021/Do-PFN/main/priors/playground_scm/scm.py (fetched 5 Nov 2026) lines 99-143; saved `brief7/texts/dopfn_code_priors_playground_scm_scm.py.txt`
- Row 2: https://raw.githubusercontent.com/jr2021/Do-PFN/main/priors/doscm.py lines 99-100, 134-136; saved `brief7/texts/dopfn_code_priors_doscm.py.txt`
- Row 2: https://raw.githubusercontent.com/jr2021/Do-PFN/main/prior_data_example.py line 12; saved `brief7/texts/dopfn_code_prior_data_example.py.txt`

## C. Tags that remain, with reasons

- **Row 1, Outcome types:** whether binary base-table columns can become CEPOs. Not reported, and no prior-generation code is referenced in the repository's reproducibility guide.
- **Row 1, Training scale:** number of prior datasets not reported by the authors.
- **Row 2, Outcome types (residual):** which binarisation strategy (`extreme` or `mean`) trained the released checkpoints is not stated.
- **Row 3, Held out? (knock-on in §D):** whether CausalFM's synthetic test sets share the prior's family is UNVERIFIED.

## D. Changes to the synthesis and answer sections that follow

### S4-1. Row 3 (CausalFM) 'Held out?' cell (L106): depends on the Brief 1 Row 4 repository check (brief1_row4_extra_advantages.md)

Old (Brief4.md line 106, exact):

```
- **Held out?** Not stated. The synthetic test sets use the prior's generator (p.9: "We benchmark our model on ten synthetic datasets generated under diverse mechanisms, with implementation details in Appendix D."), so synthetic results are in-family **(my reading)**. Jobs and ACIC 2016 outcome generators are external to the prior.
```

New:

```
- **Held out?** Not stated. The paper says the synthetic test sets were "generated under diverse mechanisms" (p.9: "We benchmark our model on ten synthetic datasets generated under diverse mechanisms, with implementation details in Appendix D."). The released test files (10 × 1,024 units, 10 covariates) match the default size of the released training generator but carry an extra `ite` column that this generator does not write, so the generating script is not in the repository; whether synthetic results are in-family is UNVERIFIED (likely, my reading). Jobs and ACIC 2016 outcome generators are external to the prior.
```

Why: The old cell asserted that the test sets 'use the prior's generator'; the repository shows only a size match.

Source: `brief7/texts/causalfm_repo_testsets.txt`; `brief7/texts/causalfm_code_gen_standard_syn.py.txt` L681–695, L707.

### S4-2. §5 leakage table, L2 (L411)

Old (Brief4.md line 411, exact):

```
| L2 | **Effect-function families shared** between prior and benchmark (for example the evaluation's severity/location/network effect processes reused in the prior) | Do-PFN synthetic case studies reuse prior parameter laws (row 2); CausalFM synthetic tests use the prior generator (row 3) | Define evaluation effect families first and freeze them. Exclude them, or parameter ranges of them, from the prior. Report in-family and held-out-family results separately, as CausalPFN did for polynomial/sinusoid families (row 1). |
```

New:

```
| L2 | **Effect-function families shared** between prior and benchmark (for example the evaluation's severity/location/network effect processes reused in the prior) | Do-PFN synthetic case studies reuse prior parameter laws (row 2); CausalFM synthetic test files match its training generator's default size, but their generating script is not released (row 3; in-family use UNVERIFIED) | Define evaluation effect families first and freeze them. Exclude them, or parameter ranges of them, from the prior. Report in-family and held-out-family results separately, as CausalPFN did for polynomial/sinusoid families (row 1). |
```

Why: Consistent with S4-1.

### S4-3 (optional). §4.1 A5 Allocation (L377): depends on Row 2 'Outcome types' (brief4_row2_outcome_types.md)

Old (Brief4.md line 377, exact):

```
| A5 | Allocation | Mixture of constant propensity (randomised trials) and linear and nonlinear logits (confounded). Use a positivity-degradation parameter ξ as in CausalPFN. Oversample strong *observed* confounding so that the prior's confounding distribution is not concentrated at zero. RCT share about one third (J). | 1 (D.1 mechanisms, ξ), 17 (PICB: Δ near 0 in existing priors) | E for mechanisms; weights J |
```

New:

```
| A5 | Allocation | Mixture of constant propensity (randomised trials) and linear and nonlinear logits (confounded). Use a positivity-degradation parameter ξ as in CausalPFN. Oversample strong *observed* confounding so that the prior's confounding distribution is not concentrated at zero. RCT share about one third (J). | 1 (D.1 mechanisms, ξ), 17 (PICB: Δ near 0 in existing priors) | E for mechanisms; weights J |  [Add to the rationale column (new wording): Do-PFN instead thresholds a simulated continuous treatment node at a random interior value or at its mean (row 2, released code), so its propensity is implicit and not controlled.]
```

Why: Contrast for the design choice; the 'implicit propensity' wording is my reading of the code and should be marked (I) as inference.

### No knock-on (checked)

- §3 Missing (L357), "No causal prior generates binary outcomes natively in a described way (rows 1–3 are continuous)": Row 1 binary-CEPO stays UNVERIFIED and Row 2's change concerns the treatment, not the outcome. No change.
- Row 1 training scale (number of prior datasets): no synthesis line uses it.
- L92 is drafted in `independence.md` (B2).

## E. Independence wording (equivalent of the Brief 1 correction)

Brief 7 asked for the Brief 1 correction only. This item corrects the same kind of wording in Brief 4. The CausalPFN authors include none of the six Do-PFN authors (author lists on p.1 of arXiv 2506.07918v2 and 2506.06039v3).

#### B2. Brief 4 Row 2 (Do-PFN), Ablation results (L92), last sentence only

**Goes beyond Brief 7 item 3 (Brief 4).**

Old (Brief4.md line 92, exact):

```
- **Ablation results:** (i) Effect size: p.24: "This result is likely explained by the high probability of low-ATE datasets in our prior", i.e., error rises for the largest-ATE datasets. (ii) Dataset size 5–2,000: CATE error falls with n (figure only). (iii) Noise: robust to Laplace, t, Gumbel and mixtures, but (p.9: "using a two-times larger variance of the Gaussian noise drastically hurts performance"). (iv) Mechanisms: (p.9: "testing on the pointwise average of the functions used during training does lead to a notable decrease in performance"). (v) Graph size (p.9: "For larger graphs out of its prior-distribution, we observe a significant reduction in Do-PFN-v1's performance"), recovered by v1.1 trained on larger graphs. (vi) Uncertainty: slightly under-confident when effects are identifiable (p.9: "slightly under-confident for theoretically identifiable case studies"). Independent head-to-head in CausalPFN's paper: Do-PFN PEHE 6.07 vs CausalPFN 0.58 on IHDP (CausalPFN Table 8, p.40).
```

New:

```
- **Ablation results:** (i) Effect size: p.24: "This result is likely explained by the high probability of low-ATE datasets in our prior", i.e., error rises for the largest-ATE datasets. (ii) Dataset size 5–2,000: CATE error falls with n (figure only). (iii) Noise: robust to Laplace, t, Gumbel and mixtures, but (p.9: "using a two-times larger variance of the Gaussian noise drastically hurts performance"). (iv) Mechanisms: (p.9: "testing on the pointwise average of the functions used during training does lead to a notable decrease in performance"). (v) Graph size (p.9: "For larger graphs out of its prior-distribution, we observe a significant reduction in Do-PFN-v1's performance"), recovered by v1.1 trained on larger graphs. (vi) Uncertainty: slightly under-confident when effects are identifiable (p.9: "slightly under-confident for theoretically identifiable case studies"). Head-to-head run by the CausalPFN authors, none of whom is a Do-PFN author, in the CausalPFN paper: Do-PFN PEHE 6.07 vs CausalPFN 0.58 on IHDP (CausalPFN Table 8, p.40).
```

Why: 'Independent' here means 'not by the Do-PFN authors'; the new wording says who ran it instead of calling it independent.


## F. Near-miss updates

- **N4 (FoCAT):** unchanged. The full text could not be obtained (user, 5 Nov 2026).

## Quote audit (run 5 Nov 2026)

Quotations were extracted from the quotation column, the new values and the synthesis 'New' blocks. Each was matched against the session texts after normalising whitespace, hyphenation, soft hyphens and the publisher's download watermark.

- Matched exactly: **20** (20 in `brief7/texts/`; 0 in texts saved for Briefs 1–6, quoted in cells carried over from Brief4.md).
- Quotations of Brief4.md's own wording (old text carried into new cells): 0.
- Matched only in order across layout breaks; **manual check** done by eye in the layout text: 0.
- Not found: **0**.
- Quotation-column entries of 25 words or more: 0.
