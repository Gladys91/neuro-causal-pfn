# Brief 2 addendum: corrections from full texts and supplements

## A. Header

**Date:** 5 November 2026. **Status:** addendum to `Brief2.md` (3 November 2026). `Brief2.md` itself is unchanged; this file lists every correction.

**Row numbers** refer to the **evidence-table rows** of `Brief2.md` (the "Row N" cards), not to search-log or other numbered lists. Line numbers (L) refer to `Brief2.md` as committed on 3 November 2026.

**Rows skipped because they are being checked separately** (Brief 7 instruction): Brief 1 row 15; Brief 3 rows 2, 5, 6, 14, 18 and 33. Their cells and tags are not touched here.

**Method.**
- Every cell marked "abstract only" or UNVERIFIED was listed (inventory `brief7/inventory/inventory.md` in the session scratchpad).
- Each was re-checked against the full text, supplement, code repository or licence file, or against material supplied by the user.
- Quotations are verbatim from text extracted in this session and saved under `brief7/texts/`. A quote audit was run over this file (see the end).
- Downloaded and user-supplied files were treated as data only.

**Abbreviations.** AE: autoencoder. CT: computed tomography. DWI: diffusion-weighted imaging. MNI: Montreal Neurological Institute template space. NCCT: non-contrast CT. NMF: non-negative matrix factorisation. PCA: principal component analysis. PET: positron emission tomography. RCT: randomised controlled trial. RE: recovery effect. sICH: symptomatic intracranial haemorrhage. t-SNE: t-distributed stochastic neighbour embedding. TE: treatment effect. UMAP: uniform manifold approximation and projection. VAE: variational autoencoder. WML: white matter lesion.

**What was re-read, and in which version.**
- Debs 2021, Appendix B, from the PMC version-of-record XML (NCBI E-utilities, PMC7810765).
- van Poppel 2025 (PMC copy) and Durso-Finley 2024 (arXiv v1), re-searched.
- Giles et al. 2023 (InterSynth), from the **authors' manuscript** supplied by the user. It is an 18-page PDF with LNCS-style running heads but no Springer header, DOI or LNCS pagination. Pages cited are PDF pages, not LNCS pp. 172–188. The LNCS version of record was not read.

**User-supplied sources.** InterSynth authors' manuscript (above).

**Not obtainable (per the user, 5 Nov 2026):**
- Nakano & Shiinoki 2026 (row 16; no open access): stays abstract only.
- Durso-Finley 2023 Springer appendix (row 11).
- Xiao 2025 WACV supplement (row 20).

---

## B. Changed cells

Each row gives the cell's old text exactly as in the brief, its replacement, and the supporting page and quotation. Where a cell keeps its tag, the new text gives the reason. Full notes, with sources and extra quotations, are in `brief7/notes/` in the session scratchpad.

| Row | Field | Old value (exact; Brief line) | New value | Page or section | Quotation (verbatim, <25 words) |
|---|---|---|---|---|---|
| 2 | §2a overview row (Status, Modality, n, Source of the true effect) | (L141) \| 2 \| Giles 2023 InterSynth, [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13) \| peer-reviewed workshop \| UNVERIFIED \| UNVERIFIED \| UNVERIFIED \| | \| 2 \| Giles 2023 InterSynth, [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13) \| peer-reviewed workshop (authors' manuscript read) \| DWI lesion masks and disconnectomes, stroke \| 4,119 lesion masks (patients not reported) \| Simulated: lesion overlap with transcriptome- or receptor-defined subnetworks sets the optimal treatment; framework only, no results \| | PDF p.12 | "Here, 4119 ischaemic lesions masks are shown by the projection of their 50-component NMF embeddings" |
| 2 | Card header / version | (L207) **Row 2. Giles D, Gray R, Foulon C, Pombo G, Xu T, Ruffle JK, Jäger HR, Cardoso J, Ourselin S, Rees G, Jha A, Nachev P. *InterSynth: A Semi-Synthetic Framework for Benchmarking Prescriptive Inference from Observational Data*. LNCS, ML4MHD 2023, pp. 172–188.** [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13). Version read: metadata only (Crossref; Semantic Scholar). Peer-reviewed workshop proceedings. | **Row 2. Giles D, Gray R, Foulon C, Pombo G, Xu T, Ruffle JK, Jäger HR, Cardoso J, Ourselin S, Rees G, Jha A, Nachev P. *InterSynth: A Semi-Synthetic Framework for Benchmarking Prescriptive Inference from Observational Data*. LNCS, ML4MHD 2023, pp. 172–188.** [doi:10.1007/978-3-031-47679-2_13](https://doi.org/10.1007/978-3-031-47679-2_13). Version read: authors' manuscript (18-page PDF supplied by the user, without Springer pagination; pages cited are PDF pages). The version of record is peer-reviewed workshop proceedings and was not read. | PDF p.1; PDF p.14 | "InterSynth: a semi-synthetic framework for benchmarking prescriptive inference from observational data" / "InterSynth, and its documentation, will be made available upon publication for research use." |
| 2 | Confounding mechanism (for §4a; Brief 2 card has no separate field) | (L208) - **Modality, sample size, representation method, estimators, tuning, source of the true effect, performance measures, main result and stated limitations:** all UNVERIFIED, because neither the full text nor the abstract could be opened (see Access limitations). | - **Confounding:**<br>  - Observed: treatment probability ramps linearly, ρ = linspace(0.5 − b_obs, 0.5 + b_obs), along the axis joining the two subnetwork centroids, ordered by lesion-centroid position. For b_obs > 0.5 the extremes are assigned deterministically, which deliberately violates positivity (PDF p.7–8).<br>  - Unobserved: P(W = w*) = b_un_obs, an information leak from the true optimum, ranging from always wrong (0) through random (0.5) to always right (1) (PDF p.9).<br>  - b = 0 simulates an RCT (PDF p.14). | PDF p.8; PDF p.9 | "the ‘fixed’ assignments to treatment violate the assumption of positivity or overlap; this is not a limitation." / "assignment bias is modelled by an information ‘leak’ from each wi∗ variable." |
| 2 | Estimators | *Same cell as above (line 208)* | - **Estimators:** one-model (S-learner) and two-model (T-learner) outcome models with any scikit-learn-style classifier (`.fit()`, `.predict_proba()`), e.g. XGBoost; other prescriptive methods can be plugged in (PDF p.13). | PDF p.13 | "Standard inferential architectures comprising one- and two-model approaches [11] for this are implemented in InterSynth, compatible with any classifier" |
| 2 | Imaging modality | *Same cell as above (line 208)* | - **Imaging modality:** acute DWI. Ischaemic lesion masks were registered non-linearly to MNI space from the b0 and b1000 images, segmented with a U-Net transformer (taken from the seed preprint, ref. 18), and stored as binary 2 mm isotropic maps. Disconnectomes are an alternative input; any binary MNI-space lesion map can be used (PDF p.10–11). | PDF p.10; PDF p.10 | "registered non-linearly to MNI space using the b-value = 0 and b-value = 1000 images from each diffusion-weighted image" / "Lesions of any kind may be used in their place as long as they occupy the same stereotactic reference frame" |
| 2 | Main result | *Same cell as above (line 208)* | - **Main result:** a software framework description with **no reported performance results**. The "end-to-end" example shows the pipeline functions and one visualisation (Fig. 1: t-SNE of 50-component NMF embeddings of 4,119 masks); no estimator is evaluated numerically (PDF p.12–13). The results on this framework are in the seed (row 1). | PDF p.1; PDF p.12 | "We demonstrate end-to-end use of the platform with an example employing real neuroimaging data from patients with ischaemic stroke" / "An example of this InterSynth visualisation method is demonstrated in Figure 1." |
| 2 | Performance measures | *Same cell as above (line 208)* | - **Performance measures:** none specified. The manuscript says only that the true susceptibility w* is available "for quantifying the fidelity of inferential models" (PDF p.7). No metric is defined. | PDF p.7 | "is available for quantifying the fidelity of inferential models" |
| 2 | Representation method | *Same cell as above (line 208)* | - **Representation method:** a plug-in for any dimensionality reduction with `.fit()`/`.transform()`, tested with UMAP, t-SNE, PCA and NMF. Alternatives: raw masks or binarised disconnectomes; one-hot atlas categories by Dice overlap with arterial-territory atlases (Liu et al., four branch levels) or 21 lesion clusters (Bonkhoff et al.); standardised lesion volume; and lesion centroid coordinates. A tabular representation can be imported instead (PDF p.11–12). No VAE or autoencoder is described. | PDF p.11; PDF p.11 | "It has been tested with UMAP [32], and the Sci-Kit Learn [39] implementations of t-distributed stochastic neighbour embedding (t-SNE), principal component analysis (PCA)" / "a tabular representation of preprocessed data can alternatively be imported" |
| 2 | Sample size | *Same cell as above (line 208)* | - **Sample size:** 4,119 ischaemic lesion masks (Fig. 1 caption, PDF p.12). The number of patients and the per-trial sample sizes are not reported, and no simulation grid size is given. | PDF p.12 | "Here, 4119 ischaemic lesions masks are shown by the projection of their 50-component NMF embeddings" |
| 2 | Source of the true effect | *Same cell as above (line 208)* | - **Source of the true effect:** semi-synthetic.<br>  - Deficit: lesion overlap with each of 16 NeuroQuery functional networks above a threshold (e.g. 5%) defines enrolment (PDF p.5).<br>  - Susceptibility: each network is split into two subnetworks by Allen Brain Atlas transcriptomic clustering, or by the top two PET receptor classes. The lesion's overlap sets the true optimal treatment w* (PDF p.6–7).<br>  - Outcome: binary. Without noise, Y = 1 if and only if W = w*. Treatment effect TE = P(Y = 1 \| W = w*) and recovery effect RE, which sets Y = 1 for a random share regardless of treatment (PDF p.9–10).<br>  - Susceptibility is never given to the model under test (PDF p.7). | PDF p.7; PDF p.9; PDF p.9 | "Unobserved susceptibility to treatment can then be synthetically defined by each lesion’s intersection with the corresponding pair of subnetworks" / "In the absence of noise, assignment to the treatment to which an individual is susceptible (Wi = wi∗ ) produces the favourable outcome" / "the recovery effect, RE, is applied following TE to a random proportion across the whole training set, fixing (Yi = 1)" |
| 2 | Stated limitations | *Same cell as above (line 208)* | - **Stated limitations:** the approach "necessarily introduces a degree of domain specificity" (PDF p.14). The ground truths "may not replicate reality but plausibly enclose it" (PDF p.13). Positivity violations are modelled on purpose and are "not a limitation" (PDF p.8). | PDF p.14; PDF p.13 | "The approach necessarily introduces a degree of domain specificity" / "generating semi-synthetic ground truths that may not replicate reality but plausibly enclose it" |
| 2 | Tuning of estimators | *Same cell as above (line 208)* | - **Tuning of estimators:** not reported (UNVERIFIED: the manuscript describes no hyperparameter tuning). The only stated design is K-fold train:test splits that are kept throughout the pipeline, including the fitting of the representations (PDF p.13). | PDF p.13 | "allocates individuals to a series of K-fold cross-validation train:test splits respected throughout the entire pipeline" |
| 2 | Licence / code and data | (L209) - **Licence:** Semantic Scholar marks a green open-access PDF with licence "null". | - **Code, data and licence:** no code URL, data release or licence in this manuscript. The abstract says the platform is made "freely available", but the Conclusion says it "will be made available upon publication for research use" (PDF p.1, 14). The seed's public repository (row 1, CC BY-NC-SA 4.0) is not named here, and whether it contains the InterSynth package is UNVERIFIED (github.com not browsable). | PDF p.1; PDF p.14 | "We make our platform freely available to the scientific community." / "InterSynth, and its documentation, will be made available upon publication for research use." |
| 2 | §4a benchmark table, row 'Giles 2025 / InterSynth (1, 2)' | (L613) \| Giles 2025 / InterSynth (1, 2) \| DWI lesion masks and disconnectomes (MNI) \| 4,119 images, 2,830 patients. Per-network trials: 31–495 (masks), 297–3,078 (disconnectomes) \| Binary outcome. The deficit is lesion overlap ≥5% with one of 16 NeuroQuery networks. Responsiveness is set by overlap with receptor- or transcriptome-defined subnetworks. Treatment effect and recovery noise are added \| Observable: allocation ramp along the lesion-centroid axis (b_obs; deterministic above 0.5). Unobservable: allocation tied to the true optimal treatment (b_un_obs) \| Code, lesion masks and atlases on GitHub \| CC BY-NC-SA 4.0 (README and LICENCE file). InterSynth chapter: UNVERIFIED \| | \| Giles 2025 / InterSynth (1, 2) \| DWI lesion masks and disconnectomes (MNI) \| 4,119 images, 2,830 patients. Per-network trials: 31–495 (masks), 297–3,078 (disconnectomes) \| Binary outcome. The deficit is lesion overlap ≥5% with one of 16 NeuroQuery networks. Responsiveness is set by overlap with receptor- or transcriptome-defined subnetworks. Treatment effect and recovery noise are added \| Observable: allocation ramp along the lesion-centroid axis (b_obs; deterministic above 0.5). Unobservable: allocation tied to the true optimal treatment (b_un_obs) \| Code, lesion masks and atlases on GitHub \| CC BY-NC-SA 4.0 (README and LICENCE file; row 1). InterSynth manuscript (row 2): no code URL or licence; release promised "upon publication" \|<br><br>Proposed addition after the row (new wording, not a quotation): InterSynth (row 2) describes the same generator and confounding mechanisms, citing the seed preprint, and reports 4,119 lesion masks; the patient count and per-trial sizes in this row come from row 1 only. Row 2 adds UMAP/t-SNE plug-ins and atlas, volume and centroid representations, and reports no results. | PDF p.8; PDF p.14 | "If bobs > 0.5, a proportion of the lesions at the extremes of the ordered list" / "InterSynth, and its documentation, will be made available upon publication for research use." |
| 5 | Stated limitations | (L258) - **Stated limitations:** post-hoc design. The appendix was not opened, so the full limitations list is UNVERIFIED. | (§Discussion) Low incidence of sICH; selection bias from trial criteria and the requirement for baseline NCCT; post-hoc analysis with data-driven thresholds, so the aspirin effect modification is "hypothesis-generating rather than definitive"; the 11.35 mL WML threshold was statistically derived, with few patients above it; and limits of the parent MR CLEAN-MED trial (early termination, unblinded allocation, heparin in pressure bags not recorded, many transferred patients, deferred consent). NCCT is non-contrast CT. | §Discussion; §Discussion | "as this is a post-hoc analysis with data-driven thresholds, there’s an increased risk of Type I errors" / "Our study has several limitations." |
| 7 | Tuning of estimators | (L280) - **Tuning of estimators:** UNVERIFIED. The training configuration is in Appendix B, which was not opened. | (Appendix B) Each network's hyperparameters were "independently fine-tuned on a fixed search space"; the search space and the selection criterion are not reported. Final settings: weighted multi-class Dice loss (lesion class ×8), Adam (learning rate 1×10⁻⁴, decay 5×10⁻⁴), batch 12, dropout 0.5, L2 2×10⁻⁴, up to 500 epochs with early stopping on validation Dice; models evaluated by 5-fold cross-validation. Patients from the I-KNOW dataset were added to the training sets of the general and non-reperfused models only. | App. B; App. B; App. B | "each network’s hyperparameters were independently fine-tuned on a fixed search space" / "The best parameters were found to be the same in all tested architectures." / "patients from I-KNOW dataset were added in the training set of the general and the non-reperfused models" |
| 12 | Stated limitations | (L361) - **Stated limitations:** not extracted (UNVERIFIED). | No limitations section. §4 Conclusions (p.9) names only future work: other strategies to measure treatment response and uncertainty over trajectories, and clustering responder subgroups to find predictive image markers. | p.9 | "Future work will explore other strategies to measure treatment response and uncertainty estimation over trajectories." |

**Sources for the changed cells.**

- Row 2: user PDF `brief7/user_pdfs/giles2023_intersynth.pdf` (18 pp.), text `brief7/texts/user_giles2023_intersynth.txt`. **Authors' manuscript**: LNCS-style running heads, but no Springer header, copyright line, DOI or LNCS page numbers. Pages are PDF pages (form-feed count), not the LNCS pagination (pp. 172–188). Whether this is the submitted or the accepted manuscript is not stated. The code statement 'will be made available upon publication' suggests a pre-publication version (my reading). Content may differ from the LNCS version of record.
- Row 5: PMC12546164, NCBI efetch XML (version of record), §Discussion; `brief7/texts/b2_vanpoppel2025_PMC12546164.txt` line 120
- Row 7: PMC7810765, NCBI efetch XML (version of record), Appendix B 'Network training and parameters' (sec s0145), fetched 5 Nov 2026; saved `brief7/texts/debs2021_appendixB_PMC7810765.txt`
- Row 12: arXiv 2406.12807v1, §4 Conclusions, PDF p.8–9; `brief7/texts/b2_dursofinley2024_nsde_arxiv2406.12807v1.txt` lines 364-380 (form-feed count: p.9 from line 374)

## C. Tags that remain, with reasons

- **Row 2, Tuning of estimators:** not reported in the InterSynth manuscript.
- **Row 2 / §4a:** the LNCS version of record was not read. Whether row 1's public repository contains the InterSynth package is UNVERIFIED (github.com not browsable).
- **Row 7, Tuning:** search space and selection criterion not reported (Appendix B gives only the final settings).
- **Row 11, Tuning of estimators:** architecture appendix not in arXiv v4, and the Springer supplement is not obtainable (user, 5 Nov 2026). Proposed cell wording: "UNVERIFIED: in an appendix that is not in the arXiv PDF; the publisher's supplement could not be obtained".
- **Row 16 (Nakano & Shiinoki 2026):** remains **abstract only**; the full text is not open access and could not be obtained (user, 5 Nov 2026). Estimator detail and tuning stay UNVERIFIED for that reason.
- **Row 20, Tuning of estimators:** Supplement A.4 not in arXiv v2, and the WACV supplement is not obtainable (user, 5 Nov 2026).

## D. Changes to the synthesis and answer sections that follow

### S2-1. §3 tuning bullet (L580): depends on Row 7 'Tuning of estimators' (brief2_row7_tuning_of_estimators.md)

Old (Brief2.md line 580, exact):

```
   - Some report only fixed hyperparameters (rows 4, 8, 10, 21, 22).
```

New:

```
   - Some report only fixed hyperparameters (rows 4, 8, 10, 21, 22). Row 7 tuned each network on a fixed search space that is not reported, and added external (I-KNOW) training patients to the general and non-reperfused models only (Appendix B).
```

Why: Row 7 was previously unclassified (tuning UNVERIFIED). The unequal training data across its reperfusion-specific models bears on any comparison between them.

### S2-2 (optional). §3 imaging-marker subgroups (L572): depends on Row 5 'Stated limitations' (brief2_row5_stated_limitations.md)

Old (Brief2.md line 572, exact):

```
   - Conventional imaging-marker subgroup analyses of stroke trials were also null or mixed: perfusion–diffusion mismatch in LASTE (row 6), and WML volume in MR CLEAN-MED except for aspirin-related sICH (row 5).
```

New:

```
   - Conventional imaging-marker subgroup analyses of stroke trials were also null or mixed: perfusion–diffusion mismatch in LASTE (row 6), and WML volume in MR CLEAN-MED except for aspirin-related sICH, which the authors call hypothesis-generating because the analysis was post hoc with data-driven thresholds (row 5).
```

Why: The authors' own limitation qualifies the one positive finding.

### Cell knock-on outside the tagged fields (optional)

- Row 7, **Sample size** or **Estimators** (Brief2.md L275–279): add "(Appendix B) patients from the I-KNOW dataset were added to the training sets of the general and non-reperfused models only; training n per fold 89–91 (general), 59–60 (reperfused), 30–31 (non-reperfused); test n 17–19." Source: `brief7/texts/debs2021_appendixB_PMC7810765.txt`.

### No knock-on (checked)

- Row 12 limitations: no synthesis line cites Row 12's limitations. L584 cites Rows 7, 8, 12 for factual metrics only, which is unchanged.


### S2-3. Assumption 2, last bullet (L31): the 'InterSynth' word claim

Old (Brief2.md line 31, exact):

```
- Neither the Nature Communications version nor arXiv v1 or v4 of the seed contains the word "InterSynth" (text search of all three files found 0 hits). The link between the two papers rests on the shared authors and the shared design. The InterSynth paper itself could not be opened (see Access limitations).
```

New:

```
- Neither the Nature Communications version nor arXiv v1 or v4 of the seed contains the word "InterSynth" (text search of all three files found 0 hits), and none cites the InterSynth chapter. The link runs the other way: the InterSynth manuscript cites the seed preprint (arXiv 2301.10748, its ref. 18) for the functional parcellation, deficit threshold and lesion segmentation, and describes the same generator (row 2, PDF p.5–10).
```

Why: The claim of 0 hits is re-verified (also 0 hits for the DOI fragment and the ML4MHD volume title). The link no longer rests only on shared authors and design: InterSynth cites the seed preprint.

### S2-4. Access limitations, InterSynth bullet (L59–64)

Old (Brief2.md lines 59–64, exact):

```
- **InterSynth (row 2) could not be read.**
  - link.springer.com served a JavaScript challenge page.
  - The green open-access copy at discovery.ucl.ac.uk was refused by the proxy. WebFetch could not resolve that host.
  - icml.cc, OpenAlex, DBLP and Europe PMC were refused.
  - The Semantic Scholar record has its abstract elided by the publisher, and Crossref has no abstract.
  - Only the metadata (title, authors, venue, pages) is verified. The whole row is UNVERIFIED for content.
```

New:

```
- **InterSynth (row 2) was read from the authors' manuscript** supplied by the user (18 pp., no Springer pagination; PDF pages cited). The LNCS version of record could not be opened (link.springer.com served a JavaScript challenge; discovery.ucl.ac.uk was refused).
```

Why: Row 2 content is now verified from a full text, although not from the version of record.

### S2-5. §3 Established 1 (L557)

Old (Brief2.md line 557, exact):

```
   - InterSynth and Giles et al. 2025 are the only benchmarks found that simulate treatment effects from real stroke lesion anatomy with a known ground truth (rows 1, 2).
```

New:

```
   - InterSynth and Giles et al. 2025 are the only benchmarks found that simulate treatment effects from real stroke lesion anatomy with a known ground truth (rows 1, 2). InterSynth (row 2) describes the generator and its confounding mechanisms but reports no estimator results; all results come from the seed (row 1).
```

Why: Row 2 Main result: framework only.

### S2-6. §3 Missing 1 (L595)

Old (Brief2.md line 595, exact):

```
   - InterSynth lacks a tabular-covariate block and has binary outcomes only.
```

New:

```
   - InterSynth simulates no tabular clinical covariates (a tabular representation can replace the image embedding, row 2, PDF p.11), has binary outcomes only (PDF p.4), and its manuscript gives no code URL or licence (release promised "upon publication", PDF p.14).
```

Why: Refines the old claim with the manuscript's own statements. The 'public release of the generator' criterion (L587) is met only through row 1's repository, whose InterSynth contents are UNVERIFIED.

### No change

- §4b (L621–637): row 2 adds no decomposition of representation versus estimator error; the manuscript only says evaluation "should not decouple representational methods from the inferential architectures" (PDF p.14).
- Search log rows 2, 4, 6–9: keep as run on 3 Nov; the addendum can note the user-supplied manuscript.

## Quote audit (run 5 Nov 2026)

Quotations were extracted from the quotation column, the new values and the synthesis 'New' blocks. Each was matched against the session texts after normalising whitespace, hyphenation, soft hyphens and the publisher's download watermark.

- Matched exactly: **36** (36 in `brief7/texts/`; 0 in texts saved for Briefs 1–6, quoted in cells carried over from Brief2.md).
- Quotations of Brief2.md's own wording (old text carried into new cells): 0.
- Matched only in order across layout breaks; **manual check** done by eye in the layout text: 0.
- Not found: **0**.
- Quotation-column entries of 25 words or more: 0.
