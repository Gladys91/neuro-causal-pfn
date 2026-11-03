# Brief 3: Treatment effects in electronic health records

**Date:** 3 November 2026
**Question:** How are heterogeneous treatment effects estimated, tuned and validated in electronic health records (EHR) and claims data, especially for second-line type 2 diabetes (T2D) drugs, and what is used when the true effect is unknown?
**Scope covered:**
- estimation of the conditional average treatment effect (CATE) in EHR and claims, with UK data first: the Clinical Practice Research Datalink (CPRD) and the Exeter precision-medicine programme
- second-line T2D drug classes: sodium-glucose cotransporter-2 inhibitors (SGLT2i), dipeptidyl peptidase-4 inhibitors (DPP-4i), glucagon-like peptide-1 receptor agonists (GLP-1 RA), sulfonylureas (SU) and thiazolidinediones (TZD)
- validation when the true effect is unknown
- estimator and hyperparameter selection under confounding
- high-dimensional code covariates
- tabular foundation models applied to EHR

Each paper has its own card in section 2, giving every field the brief asks for.

### Assumptions (how ambiguities in the brief were resolved)
1. **Venkatasubramaniam et al. 2023** is "Comparison of causal forest and regression-based approaches to evaluate treatment effect heterogeneity: an application for type 2 diabetes precision medicine", BMC Med Inform Decis Mak 23:110, doi:10.1186/s12911-023-02207-2 (PubMed identifier, PMID, 37328784). It matches the brief: SGLT2i versus DPP-4i, CPRD. Note that the models were *developed in randomised trial data* and only *validated* in CPRD.
2. **Wendling et al. 2018** is "Comparing methods for estimation of heterogeneous treatment effects using observational data from health care databases", Stat Med 37(23):3309–3324, doi:10.1002/sim.7820 (PMID 29862536). It is the only Wendling 2018 paper in Statistics in Medicine on this topic.
3. **The Exeter precision-medicine work.** I took the MASTERMIND/Exeter outputs on these drug classes:
   - the SGLT2i–DPP-4i treatment-selection model (Dennis 2022, Lancet Digital Health, doi:10.1016/S2589-7500(22)00174-1)
   - its external validation by ethnicity (Güdemann 2026, Lancet Regional Health Europe, doi:10.1016/j.lanepe.2025.101547)
   - the SGLT2i–GLP-1 RA Bayesian causal forest model (Cardoso 2024, Diabetologia, doi:10.1007/s00125-024-06099-3)
   - the five-drug-class model (Dennis 2025, Lancet, doi:10.1016/S0140-6736(24)02617-5)
   - the TriMaster crossover-trial comparison (Güdemann 2026, Diabetes Care, doi:10.2337/dc26-0118)
   - the risk-based SGLT2i benefit models for heart failure (Young 2026, Diabetes Care, doi:10.2337/dc25-2973) and kidney protection (Jansz 2026, Diabetologia, doi:10.1007/s00125-025-06577-2).
4. **Franklin et al. 2014** is "Plasmode simulation for the evaluation of pharmacoepidemiologic methods in complex healthcare databases", Comput Stat Data Anal 72:219–226, doi:10.1016/j.csda.2013.10.018 (PMID 24587587).
5. **Shaw et al. 2025** is arXiv:2504.11740v1, "A cautionary note for plasmode simulation studies in the setting of causal inference" (April 2025). It was published as Stat Med 2026, doi:10.1002/sim.70676. Its central argument is an induced violation of positivity, which matches the brief.
6. **Mahajan et al. 2024** is "Empirical Analysis of Model Selection for Heterogeneous Causal Effect Estimation", ICLR 2024 (arXiv:2211.01939v3). **Doutreligne and Varoquaux 2025** is "How to select predictive models for decision-making or causal inference", GigaScience 14:giaf016, doi:10.1093/gigascience/giaf016 (arXiv:2302.00370). **Bach et al. 2024** is "Hyperparameter Tuning for Causal Inference with Double Machine Learning: A Simulation Study", CLeaR 2024, PMLR 236 (arXiv:2402.04674).
7. **Wyss et al. 2018** is "Using Super Learner Prediction Modeling to Improve High-dimensional Propensity Score Estimation", Epidemiology 29(1):96–106, doi:10.1097/EDE.0000000000000762.
   - **Caution:** arXiv:1703.02236 is often linked to this topic but is a *different* paper (Ju, …, Wyss, Schneeweiss, van der Laan; J Appl Stat 2019). It is included separately as row 19.
8. **Wyss et al. 2024 is ambiguous.** No 2024 Wyss paper on *learned representations* was found (PubMed author search, Crossref author search and two WebSearch queries; see the search log).
   - I took "Wyss 2024" as "Targeted learning with an undersmoothed LASSO propensity score model for large-scale covariate adjustment in health-care database studies", Am J Epidemiol 193(11):1632–1640, doi:10.1093/aje/kwae023. This is the 2024 Wyss first-author paper on high-dimensional propensity scores with machine learning.
   - I cover "learned representations" with Wyss's 2022 overview (row 20), which discusses neural feature generation from codes, and I list the representation-learning papers as near-misses.
   - If the coordinator meant a different paper, row 21 should be replaced.
9. "Tabular foundation models applied to EHR": I found no paper that uses a tabular foundation model to estimate treatment effects in EHR or claims data. The closest is row 33 (TabPFN trained on a hospital stroke registry and applied to a randomised trial). See the answer in section 5.

### Access limitations
- **Wiley (onlinelibrary.wiley.com) and Elsevier (linkinghub) were blocked**, so these were read as *abstract only*: Wendling 2018, Dennis 2022, Dennis 2025, the Güdemann 2026 TriMaster paper, Wyss 2018, Wyss 2024, Wang 2024, Wang 2025 (Am J Epidemiol), Mori 2026 and Kurmann 2026.
- **The medRxiv preprints of the Exeter papers could not be opened:** www.medrxiv.org returned a Cloudflare 403.
- **pmc.ncbi.nlm.nih.gov served a reCAPTCHA page after the first request**, so PMC full texts were taken from the NCBI E-utilities XML (efetch db=pmc). That works for open-access and author-manuscript articles. For others it returns only the abstract.
- **Page numbers.** PMC texts carry no page numbers, so quotes from them are located by *section heading* (§). Quotes from arXiv PDFs give the PDF page (p.).
- **Supplementary material was not opened for any paper.** Several tuning details sit in supplements and are marked UNVERIFIED.
- **Databases not queried directly:**
  - Google Scholar cannot be queried automatically.
  - OpenReview and the proceedings of NeurIPS, ICML, ICLR, AISTATS, CLeaR and UAI were searched only through arXiv and WebSearch. One exception: the PMLR v236 listing was opened to confirm Bach 2024.
  - Semantic Scholar was used for forward citation chasing of two seeds, after retries on 429 errors.

---

## 1. Search log

All searches were run on 3 November 2026. Date window 2019 to November 2026 (seeds older than 2019 accepted). "Screened" means title or abstract read. "Included" counts new inclusions, not duplicates.

| # | Source | Exact query / action | Hits | Screened | Included (new) |
|---|---|---|---|---|---|
| 1 | PubMed (E-utilities) | `Venkatasubramaniam[au] AND (SGLT2 OR DPP-4 OR causal forest)` | 1 | 1 | 1 (row 1) |
| 2 | PubMed | `Wendling T[au] AND heterogeneous treatment effects` | 1 | 1 | 1 (row 14) |
| 3 | PubMed | `Franklin JM[au] AND plasmode` | 8 | 8 | 2 (rows 23, 18) |
| 4 | PubMed | `plasmode positivity Shaw` | 0 | 0 | 0 |
| 5 | PubMed | `plasmode AND positivity` | 5 | 5 | 0 |
| 6 | PubMed | `Shaw[au] AND plasmode` | 4 | 4 | 1 (row 24, published version identified) |
| 7 | PubMed | `Wyss R[au] AND (high-dimensional propensity OR representation OR machine learning) AND 2022:2026[dp]` | 17 | 17 | 5 (rows 15, 16, 17, 20, 22) |
| 8 | PubMed | `Dennis JM[au] AND (SGLT2 OR DPP4 OR treatment selection OR precision)` | 37 | 37 | 7 (rows 2, 3, 4, 6, 7, 8 and row 1 duplicate) |
| 9 | PubMed | `Wyss R[au] AND 2024[dp]` | 14 | 14 | 1 (row 21) |
| 10 | PubMed | `(autoencoder OR representation learning OR embedding) AND (high-dimensional propensity score OR proxy confounder) AND 2019:2026[dp]` | 19 | 19 | 0 (near-misses N1–N3) |
| 11 | PubMed | `Dennis JM[au] AND 2022:2026[dp] AND (heterogeneous OR heterogeneity OR validation OR calibration)` | 19 | 19 | 1 (row 5) |
| 12 | Crossref API | author query "Richard Wyss", 2023-06 to 2025-06, 60 rows | 60 | 60 | 0 |
| 13 | WebSearch | `Wyss 2024 learned representations high-dimensional proxy confounding claims data autoencoder propensity score` | 10 | 10 | 0 |
| 14 | WebSearch | `Wyss Schneeweiss 2024 "representation" pharmacoepidemiology machine learning confounding healthcare database embeddings` | 10 | 10 | 0 |
| 15 | arXiv API | `au:Doutreligne` | 5 | 5 | 2 (rows 30, 32) |
| 16 | arXiv API | `au:Mahajan AND ti:"model selection"` | 1 | 1 | 1 (row 29) |
| 17 | arXiv API | `au:Bach AND ti:"double machine learning"` | 3 | 3 | 1 (row 31) |
| 18 | arXiv API | `all:plasmode` (max 30) | 18 | 18 | 3 (rows 24, 25, 26) |
| 19 | arXiv API | `au:Wyss AND (all:propensity OR all:confounding)` | 4 | 4 | 2 (rows 19, 22) |
| 20 | arXiv API | `ti:"iterative causal forest"` | 0 | 0 | 0 |
| 21 | Crossref API | titles of Dennis 2022, Dennis 2025, TriMaster, Wendling, O'Neill (to find preprints) | 5 queries × 6 | 30 | 0 (only a medRxiv DOI was found, and it is blocked) |
| 22 | PubMed | `("causal forest" OR "heterogeneous treatment effect*" OR "conditional average treatment effect" OR "individualized treatment effect*") AND (diabetes) AND (SGLT2 OR "sodium-glucose" OR GLP-1 OR DPP-4 OR sulfonylurea* OR thiazolidinedione*) AND 2019:2026[dp]` | 27 | 27 | 4 (rows 9, 11, 12, 13) |
| 23 | PubMed | `Weberpals J[au] AND (autoencoder OR "deep learning") AND propensity` | 1 | 1 | 0 (N1) |
| 24 | PubMed | `(TabPFN OR "tabular foundation model*" OR "prior-data fitted network*") AND (electronic health record* OR EHR OR claims OR clinical)` | 116 | 30 (first page) | 0 |
| 25 | PubMed | `(TabPFN OR "tabular foundation model") AND (treatment effect OR causal OR propensity)` | 34 | 20 | 1 (row 33) |
| 26 | arXiv API | `all:TabPFN AND (all:"treatment effect" OR all:causal) AND (all:"health records" OR all:EHR OR all:claims OR all:clinical)` | 3 | 3 | 0 (N9) |
| 27 | arXiv API | `all:"foundation model" AND all:"electronic health records" AND all:"treatment effect"` | 2 | 2 | 0 |
| 28 | PubMed | `"rank-weighted average treatment effect"[tiab] OR "targeting operator characteristic"[tiab] OR "Qini"[tiab]` | 24 | 24 | 1 (row 27) |
| 29 | PubMed | `"c-for-benefit"[tiab] AND (observational OR "electronic health" OR claims OR registry OR "real-world")[tiab]`: **query returned an error; not rerun** | n/a | n/a | n/a |
| 30 | arXiv API | `all:"rank-weighted average treatment effect"` | 1 | 1 | 0 (same as row 27) |
| 31 | PubMed | HTE terms[tiab] AND (`CPRD` OR `Clinical Practice Research Datalink` OR `UK Biobank` OR `SAIL` OR `THIN` OR `QResearch`)[tiab] | 11 | 11 | 1 (row 10) |
| 32 | Semantic Scholar | forward citations of doi:10.1186/s12911-023-02207-2 (first 100) | 100 | ~40 relevant titles | 1 (row 28) |
| 33 | Semantic Scholar | forward citations of doi:10.1002/sim.7820 (first 100) | 100 | 100 | 0 new (row 30 duplicate; N5–N8 near-misses) |
| 34 | WebSearch | `Doutreligne Varoquaux "How to select predictive models for decision-making or causal inference" GigaScience 2025` | 10 | 10 | 0 (confirmed the published version of row 30) |
| 35 | Backward chasing | reference sections read in Wyss 2022 (plasmode, negative controls), Shaw 2025 (plasmode designs) and Karim 2026b (Shaw, Franklin, Schreck) | n/a | ~15 references | 0 new (cited works seen through citing text only) |

Backward chasing was not done systematically. Forward chasing was done only for the Venkatasubramaniam and Wendling seeds, because Semantic Scholar returned many 429 errors. In 2023–2026 the forward-citation list for Venkatasubramaniam contained many unrelated titles, which suggests mismatched records; these were ignored.

---

## 2. Evidence table (one card per paper)

Every card has all the brief's fields (paper; database; cohort size; treatments; outcome; covariates; estimators; tuning and selection procedure; validation approach; subgroups examined; main result), plus link, version and peer-review status. Quotes are verbatim. "§" gives the section heading in PMC texts and "p." the PDF page in arXiv texts.

### A. CATE in EHR and claims for second-line T2D drugs

#### Row 1. Venkatasubramaniam A, Mateen BA, Shields BM, Hattersley AT, Jones AG, Vollmer SJ, Dennis JM (2023). BMC Med Inform Decis Mak 23:110
- **Link / version:** https://doi.org/10.1186/s12911-023-02207-2. Version of record (VoR) via PMC10276367. Peer reviewed.
- **Database:**
  - Development: the CANTATA-D and CANTATA-D2 randomised controlled trials (RCTs), from the Yale University Open Data Access (YODA) Project.
  - Validation: CPRD GOLD (UK primary care) (§Routine clinical data: "Anonymized primary care electronic health records were extracted from UK Clinical Practice Research Datalink (CPRD) GOLD").
- **Cohort size:**
  - 1,428 trial participants.
  - 18,741 CPRD patients (§Abstract Methods: "external validation … evaluated in 18,741 patients in UK primary care").
  - The arm counts are inconsistent within the paper. Table 2 heads the SGLT2i column n = 11,682, but the Results text says "DPP4-i (n = 11,682), or SGLT2-i (n = 7,059)".
- **Treatments:** SGLT2i (canagliflozin in the trials; any SGLT2i in CPRD) versus DPP-4i (sitagliptin in the trials).
- **Outcome:** HbA1c (glycated haemoglobin) at 6 months, continuous.
- **Covariates:**
  - 11 predictors: baseline HbA1c, age, sex, estimated glomerular filtration rate (eGFR), alanine aminotransferase (ALT), body mass index (BMI), HDL and LDL cholesterol, triglycerides, albumin and bilirubin.
  - CPRD confounders added for the validation step: ethnicity, smoking, diabetes duration, comorbidities and prior non-adherence.
- **Estimators:**
  - Penalised linear regression with restricted cubic splines and drug-by-covariate interactions.
  - Causal forest from the R package grf (generalised random forests).
- **Tuning and selection:**
  - Regression: "optimal penalty factors, based on Akaike information criterion (AIC), were estimated separately for main effects, non-linear effects, and interaction terms" (§Model development in trial data: penalized regression). Lasso was compared and gave similar results.
  - Causal forest: "used default tuning parameters for growing the many tree structures" (§…: causal forest). The only sensitivity check was the number of trees (50 to 10,000).
- **Validation approach:** the authors state that the CATE "cannot be evaluated at the patient-level" (§Model evaluation in routine clinical data).
  - Calibration of observed against predicted differences by decile and by clinical cut-offs (≥10, 5–10, 3–5 and 0–3 mmol/mol).
  - Observed differences were estimated by regression adjusted for predictors and confounders, with sensitivity analyses using inverse probability of treatment weighting (IPTW) and inverse probability of censoring weighting (IPCW).
  - Patients receiving the therapy the model predicted as best (concordant) were contrasted with those who did not (discordant).
- **Subgroups examined:**
  - Strata of predicted benefit.
  - Ethnicity was **not** evaluated ("Ethnicity was not evaluated as a candidate predictor as trial participants were predominantly of White ethnicity", §Predictors).
  - People with eGFR < 45 were excluded. A sensitivity analysis restricted to second-line use only.
- **Main result (null or negative for machine learning):**
  - "calibration was good with penalized regression but sub-optimal with causal forest" (§Abstract Results).
  - The causal forest predicted that 99.7% of CPRD patients would do better on SGLT2i and found no DPP-4i-benefit stratum. Regression identified a stratum with ≥10 mmol/mol SGLT2i benefit (observed 11.0 mmol/mol, abstract).
  - Conclusion: researchers "must compare outputs with standard regression" (§Abstract Conclusions).
  - **Discrepancy:** for that stratum the abstract gives 3.7% of patients; Table 3 gives n = 1,173 and an observed difference of −10.7 (−13.0 to −8.4); the text gives 687 (3.7%).
  - Limitations stated by the authors: a single low-dimensional setting, and that "we cannot rule out unmeasured confounding" (§Discussion).

#### Row 2. Dennis JM et al. (2022). Lancet Digit Health 4(12):e873–e883. **Abstract only**
- **Link / version:** https://doi.org/10.1016/S2589-7500(22)00174-1. PubMed abstract (PMID 36427949). Peer reviewed. Full text UNVERIFIED (Elsevier blocked).
- **Database:** CPRD (UK primary care) plus a reanalysis of 14 trials.
- **Cohort size:**
  - CPRD n = 26,877 (10,253 SGLT2i and 16,624 DPP-4i).
  - Derivation n = 14,069. Independent CPRD validation n = 9,376.
  - Head-to-head trials n = 2,499.
- **Treatments:** SGLT2i versus DPP-4i.
- **Outcome:** HbA1c at 6 months, adjusted for baseline. Secondary: weight change and discontinuation.
- **Covariates:** the final algorithm uses five features. Abstract: "baseline HbA1c, age, BMI, eGFR, and alanine aminotransferase were associated with differential HbA1c outcome".
- **Estimators:** UNVERIFIED (full text not read; from row 3's description, a regression-based model).
- **Tuning and selection:** UNVERIFIED.
- **Validation approach:** abstract: "validated in head-to-head trials (n=2499) and CPRD (independent validation; n=9376)".
- **Subgroups examined:** a subgroup of about 40% defined by predicted benefit; discontinuation by predicted-benefit group. eGFR < 45 excluded.
- **Main result:**
  - Abstract: "identified a subgroup, representing around four in ten CPRD patients, with a 5 mmol/mol or greater observed benefit with SGLT2 inhibitors in all validation cohorts".
  - Observed benefit in that subgroup: CPRD 8.8 mmol/mol; CANTATA-D/D2 5.8; BI1245.20 6.6.
  - The subgroup predicted to benefit more from DPP-4i was about twice as likely to discontinue SGLT2i (median 26.8% vs 14.8%).

#### Row 3. Güdemann LM et al. (2026). Lancet Reg Health Eur, "Validation of an algorithm for selection of SGLT2 and DPP4 inhibitor therapies … across major UK ethnicity groups"
- **Link / version:** https://doi.org/10.1016/j.lanepe.2025.101547. VoR via PMC12702077. Peer reviewed.
- **Database:** CPRD Aurum, 2013–2020. Described as "a near distinct set of individuals to our development set (CPRD Gold)" (§Research design and participants).
- **Cohort size:** 145,556 initiations (57,749 SGLT2i and 87,807 DPP-4i): White 114,287, Black 6,663, South Asian 20,969, Mixed/Other 3,637.
  - The "Research in context" box gives White as "n = 1,142,887", which is presumably a typo.
- **Treatments:** SGLT2i versus DPP-4i.
- **Outcome:** HbA1c at 6 months. Secondary: weight change and discontinuation within 6 months.
- **Covariates:** model predictors HbA1c, age, BMI, eGFR and ALT. The adjustment set adds the number of current and ever glucose-lowering drugs and the month of the HbA1c measurement.
- **Estimators:** the existing Dennis 2022 model with recalibration only. The CATE model was not refitted.
- **Tuning and selection:**
  - A closed testing procedure (log-likelihood tests, after Vergouwe) chose between the original model, recalibration-in-the-large, and intercept-plus-slope updating, separately for each ethnicity and drug class (§Step 1).
  - Outcome: "Model intercept recalibration (Model 2) was therefore performed to allow for greater DPP4i response for all ethnicity groups" (§A model update was required…).
- **Validation approach:**
  - Grouped calibration: within deciles of predicted difference, the mean prediction was compared with a regression-adjusted observed difference (§Step 2). Absolute calibration was reported as root mean square error (RMSE).
  - The authors acknowledge that the validation "is based on subgroup-level averages rather than individual patient-level differences" (§Discussion).
- **Subgroups examined:**
  - Ethnicity (White, Black, South Asian, Mixed/Other).
  - Deprivation (sensitivity), Mixed and Other separately, and 12-month outcome.
- **Main result:**
  - "For all ethnicity groups, predicted differential glycaemic treatment effects were well calibrated" (§Findings).
  - DPP-4i response was underpredicted: "White—1.6 mmol/mol; Black—3.0 mmol/mol; South Asian—2.6 mmol/mol; Mixed/Other—2.6 mmol/mol" (§Findings).
  - There was "minor miscalibration … in the South Asian ethnicity group" in the top decile (§Model predicted HbA1c differences…).
  - The reported Black-group interval "0.6 mmol/mol (95% CI 0.5–1.7)" does not contain its own point estimate in the way written. It is probably −0.5 and is reproduced as printed.

#### Row 4. Cardoso P et al. (2024). Diabetologia 67:822–836, "Phenotype-based targeted treatment of SGLT2 inhibitors and GLP-1 receptor agonists in type 2 diabetes"
- **Link / version:** https://doi.org/10.1007/s00125-024-06099-3. VoR via PMC10955037. Peer reviewed.
- **Database:**
  - CPRD Aurum (England), 2013–2020.
  - External validation in SCI-Diabetes (Tayside & Fife, Scotland).
  - Sex replication in the HARMONY trials and the PRIBA cohort.
- **Cohort size:** "46,394 people … 27,319 for model development, 19,075 for hold-out validation" plus "2252 people … from Scotland" (§Abstract Methods).
- **Treatments:** SGLT2i versus GLP-1 RA (semaglutide excluded).
- **Outcome:** HbA1c at 12 months.
  - Secondary: weight change, discontinuation within 6 months, and new-onset microvascular disease, major adverse cardiovascular events (MACE), heart failure and kidney events up to 5 years.
- **Covariates:** about 35 routine features, including age, duration, sex, ethnicity, deprivation, smoking, drug counts, HbA1c, BMI, eGFR, HDL, ALT, albumin, bilirubin, cholesterol, blood pressure, and microvascular and cardiovascular comorbidities (§Predictors).
- **Estimators:** Bayesian causal forest (BCF), an extension of Bayesian additive regression trees (BART), using the R packages bcf 2.0.1 and sparseBCF 1.0. A propensity score was estimated first.
- **Tuning and selection:**
  - "Variable selection, based on each variable's splitting probabilities, was deployed to develop a parsimonious final model" (§Treatment selection model development).
  - The propensity score did not meet the selection threshold.
  - BCF priors and hyperparameters are in the electronic supplementary material (ESM): UNVERIFIED (supplement not opened).
- **Validation approach:**
  - Grouped calibration: deciles of predicted CATE (quintiles in Scotland) were compared with subgroup average treatment effects (ATEs) from Bayesian regression adjustment, with propensity-score matching as a sensitivity analysis.
  - Rationale: "true CATE estimates are unobserved as a single individual receives only one therapy" (§Model validation).
- **Subgroups examined:**
  - Sex.
  - Ethnicity (South Asian, Black, Other, Mixed), with or without cardiovascular disease.
  - Distributions of baseline HbA1c, eGFR, age and BMI across benefit strata.
- **Main result:**
  - "Calibration was good in hold-back validation". The Scottish validation "identified clear differences in glycaemic outcomes" (§Abstract Results) but showed "modest calibration in middle quintiles" (§Model calibration).
  - Sex was a major modifier: women responded more to GLP-1 RA, replicated in HARMONY-7 at 4.4 mmol/mol (95% credible interval 2.2 to 6.3).
  - Mean CATE was 0.1 mmol/mol; 52% were predicted to do better on GLP-1 RA.
  - Heart failure and chronic kidney disease (CKD) hazard ratios favoured SGLT2i with "no clear evidence of a difference by subgroup" (§Effect of targeting therapy…).
  - The authors note the possibility of selection bias and that validation in randomised data "would further strengthen the evidence" (§Discussion).

#### Row 5. Dennis JM et al. (2025). Lancet 405:701–714, five-drug-class model. **Abstract only**
- **Link / version:** https://doi.org/10.1016/S0140-6736(24)02617-5. PubMed abstract (PMID 40020703). Peer reviewed. Full text UNVERIFIED.
- **Database:** CPRD Aurum 2004–2020, with hold-back validation by region and calendar period, plus individual-level data from three trials (TriMaster, NCT00622284, NCT01167881).
- **Cohort size:** development 100,107 initiations; total CPRD 212,166 initiations. Geographical validation had 12,373 matched pairs and temporal validation 4,841.
- **Treatments:** DPP-4i, GLP-1 RA, SGLT2i, SU and TZD.
- **Outcome:** HbA1c at 12 months.
  - Long-term (5-year): glycaemic failure, mortality, MACE or heart failure (MACE-HF), renal progression and microvascular complications.
- **Covariates:** nine features: "age, duration of diabetes, sex, and baseline HbA1c, BMI, estimated glomerular filtration rate, HDL cholesterol, total cholesterol, and alanine aminotransferase".
- **Estimators:** UNVERIFIED (abstract says only "five-drug class model").
- **Tuning and selection:** UNVERIFIED.
- **Validation approach:**
  - Matched (1:1) concordant versus discordant groups.
  - Pairwise calibration in CPRD and in three randomised trials.
  - Long-term outcomes by concordance (adjusted Cox models).
- **Subgroups examined:** model-concordant versus model-discordant groups. Others UNVERIFIED.
- **Main result:**
  - Concordant groups had a 12-month HbA1c benefit of 5.3 mmol/mol (geographical validation) and 5.0 mmol/mol (temporal validation).
  - Abstract: "Predicted HbA1c differences were well calibrated with observed HbA1c differences in the three clinical trials".
  - Glycaemic failure adjusted hazard ratio (aHR) 0.62.
  - Mortality aHR 0.95 (0.83–1.09), a null result.

#### Row 6. Güdemann LM et al. (2026). Diabetes Care, "To Cluster or Not to Cluster?" (TriMaster). **Abstract only**
- **Link / version:** https://doi.org/10.2337/dc26-0118. PubMed abstract (PMID 42312889). Peer reviewed. Full text UNVERIFIED.
- **Database:** the TriMaster three-way crossover RCT. Not EHR; it serves here as a within-person benchmark.
- **Cohort size:** 309 adults.
- **Treatments:** sitagliptin (DPP-4i), canagliflozin (SGLT2i) and pioglitazone (TZD), all three received by each participant.
- **Outcome:** HbA1c at 4 months and within-person differential response.
- **Covariates:** routine features, HOMA (homeostasis model assessment) and partitioned polygenic scores (PPS).
- **Estimators compared:**
  - clustering on routine features and HOMA
  - direct outcome prediction with the routine-features treatment-selection model (the EHR-derived model)
  - PPS
  - discriminative dimensionality reduction tree (DDRTree).
- **Tuning and selection:** none reported in the abstract (UNVERIFIED).
- **Validation approach:** association with observed within-person differential response in a crossover trial.
- **Subgroups examined:** data-driven clusters, including severe insulin-resistant diabetes.
- **Main result:**
  - "The routine-features model identified the most effective therapy with significant benefit across all drug comparisons, whereas clinical clusters showed benefit for only one cluster-drug comparison".
  - Allocation by model: 2.9 mmol/mol (2.0 to 3.8), against 1.7 mmol/mol for clusters.
  - "DDRTree was not associated with treatment response" (null).

#### Row 7. Young KG et al. (2026). Diabetes Care, SGLT2-inhibitor Absolute Benefit REsponse (SABRE) model for heart failure
- **Link / version:** https://doi.org/10.2337/dc25-2973. Author manuscript via PMC7619156. Peer reviewed.
- **Database:** CPRD Aurum linked to Hospital Episode Statistics (HES), Office for National Statistics (ONS) death data and the Index of Multiple Deprivation (IMD), 2013–2020.
- **Cohort size:** 57,368 SGLT2i and 111,673 DPP-4i/SU initiations, in people without atherosclerotic cardiovascular disease (ASCVD), heart failure (HF) or CKD.
- **Treatments:** SGLT2i versus pooled DPP-4i/SU.
- **Outcome:** new-onset HF, time to event, over 5 years.
- **Covariates:** QDiabetes-HF predictors (including ethnicity), deprivation, HbA1c, blood pressure, BMI, admissions, drug counts and year (§Weighting).
- **Estimators:**
  - Not a CATE learner: absolute benefit = QDiabetes-HF 5-year risk × the trial relative risk reduction (meta-analysis HR 0.63) (§Estimation and validation…).
  - Checked with overlap-weighted Cox models.
- **Tuning and selection:** none (fixed formula). Confounding control by overlap weighting with regression adjustment.
- **Validation approach:**
  - The relative effect was checked against the trial meta-analysis. The treatment-by-risk interaction was tested.
  - Predicted against "observed" benefit by decile. The "observed" benefit came from a Cox model with only a main treatment term: "incorporating a term for treatment (SGLT2i or DPP4i/SU). We then used the model to estimate 5-year heart failure risk with both" (§Estimation and validation…).
  - Because of that constant-HR model, this calibration cannot detect heterogeneity in relative effect.
- **Subgroups examined:**
  - Baseline HF risk (interaction p = 0.82).
  - Sex and ethnicity (sensitivity). "Hazard ratios in non-White ethnicity subgroups had wider confidence intervals" (§Results).
  - Insulin users and second-line users.
- **Main result:**
  - HR 0.70 (0.63–0.78), "concordant with the 37% lower risk from previous trial meta-analysis".
  - Predicted benefit ranged from <0.1% to 14.1% and was "well-calibrated with observed benefits" (§Absolute heart failure benefit predictions…).
  - The restricted SABRE strategy lowered the 1-year number needed to treat (NNT) to 131.

#### Row 8. Jansz TT et al. (2026). Diabetologia, "targeting SGLT2 inhibitor treatment for kidney protection"
- **Link / version:** https://doi.org/10.1007/s00125-025-06577-2. VoR via PMC12779664. Peer reviewed.
- **Database:** CPRD (UK primary care), 2013–2020.
- **Cohort size:** 53,096 SGLT2i and 88,404 DPP-4i/SU initiations. Population: eGFR ≥ 60 and urine albumin-to-creatinine ratio (uACR) < 30 mg/mmol, without HF or atherosclerotic disease.
- **Treatments:** SGLT2i versus DPP-4i/SU.
- **Outcome:** kidney disease progression over 3 years (≥50% eGFR decline, end-stage kidney disease or kidney death). Time to event.
- **Covariates:** full covariate set with multiple imputation (10 imputations).
- **Estimators:** predicted absolute risk reduction (pARR) = the CKD Prognosis Consortium (CKD-PC) risk score combined with the trial HR (0.62). Checked with doubly robust overlap-weighted Cox models.
- **Tuning and selection:** none (fixed formula). The CKD-PC score "did not require recalibration".
- **Validation approach:** HR checked against the trial meta-analysis. Calibration of pARR against overlap-weighted observed estimates.
- **Subgroups examined:**
  - Albuminuria (uACR < 3 vs 3–30 mg/mmol), with interaction p = 0.99.
  - Continuous CKD-PC risk (p = 0.71 non-linear).
  - eGFR ≥ 60 only.
- **Main result:**
  - HR 0.58 (0.48–0.69).
  - Calibration slope 1.10 (1.09–1.12).
  - Targeting by model would prevent "over 10% more events over 3 years (253 vs 228)" (§Abstract Results).
  - The authors' limitation: "treatment allocation was non-random … introducing potential for unmeasured confounding and indication bias" (§Limitations).

#### Row 9. O'Neill S et al. (2025). Diabetologia, "Comparative effectiveness of alternative second-line oral glucose-lowering therapies…"
- **Link / version:** https://doi.org/10.1007/s00125-025-06447-x. VoR via PMC12361298. Peer reviewed.
- **Database:** CPRD linked to hospital data (England), 2015–2021.
- **Cohort size:** 41,790.
- **Treatments:** SU, DPP-4i and SGLT2i added to metformin.
- **Outcome:** change in HbA1c over 1 year.
- **Covariates:** HbA1c, blood pressure, eGFR, BMI, sex, practice size, smoking, alcohol, co-prescriptions, hospitalisations, and 21 long-term conditions grouped as multiple long-term conditions (MLTC).
- **Estimators:** target trial emulation plus instrumental variable (IV) analysis.
  - Instrument: the clinical commissioning group's (CCG's) tendency to prescribe.
  - Method: two-stage residual inclusion (2SRI) with recycled predictions, giving individual-level effects aggregated to subgroups.
- **Tuning and selection:** "Variables for each model and the choice of effect modifiers were selected by LASSO regression" (§Statistical analysis). Post-double-selection used adaptive LASSO.
- **Validation approach:**
  - IV checks: "Cragg–Donald F statistics were 1515 for DPP4i and 1413 for SGLT2i" and covariate balance across the instrument.
  - "We did not validate the treatment effect estimates in external data" (§Discussion).
- **Subgroups examined:** age (18–49, 50–69, ≥70), baseline HbA1c, MLTC and 64 profiles. Kidney function was not examined: only 6.7% had eGFR < 60 (§Discussion).
- **Main result:**
  - SGLT2i versus SU: −5.74 mmol/mol in ages 18–49, compared with −2.68 in ages ≥70.
  - Effects were similar across HbA1c and MLTC subgroups.

#### Row 10. Lugo-Palacios DG et al. (2025). Health Econ 34(1):85–104, "Going beyond randomised controlled trials to assess treatment effect heterogeneity across target populations"
- **Link / version:** https://doi.org/10.1002/hec.4903. VoR via PMC11631826. Peer reviewed.
- **Database:** CPRD (England), 2011–2015 (the PERMIT study).
- **Cohort size:** target population 13,240; RCT-eligible 6,497; RCT-ineligible 6,743.
- **Treatments:** DPP-4i versus SU, second line after metformin.
- **Outcome:** change in HbA1c over 1 year.
- **Covariates:** age, sex, ethnicity, HbA1c, eGFR, BMI, systolic blood pressure (SBP) and others, with interactions chosen by rigorous LASSO.
- **Estimators:** local instrumental variable (LIV) analysis, with the CCG tendency to prescribe as instrument. It gives person-level effects that are aggregated to CATEs. The alternative analysis used IPTW with regression adjustment (IPTW-RA), which assumes no unmeasured confounding.
- **Tuning and selection:** "we applied the rigorous Least Absolute Shrinkage and Selection Operator (LASSO) regression algorithm for the first and second stage models". The generalised linear model (GLM) family and link were chosen by RMSE (§Statistical analysis).
- **Validation approach:**
  - Benchmark against an RCT (Nauck 2007) in the RCT-eligible subset, using a binary agreement metric (point estimate inside the RCT 95% CI).
  - CATEs were then compared across eligible and ineligible subpopulations.
- **Subgroups examined:** age, ethnicity (White, South Asian, Black/mixed/other), baseline HbA1c and BMI.
- **Main result:**
  - The ATE agreed with the RCT. For HbA1c ≥ 88 the difference was −5.3 (−12.8 to 2.2) in favour of DPP-4i.
  - **Key negative finding about trial benchmarking:** "The alternative analysis assuming no unobserved confounding provided estimates of ATEs that were in the opposite direction to those from the LIV, but for the 'RCT-eligible' population still met the criteria for 'estimate agreement'" (§Results).

#### Row 11. Chen HY et al. (2026). Diabetes Obes Metab, "Heterogeneity of Treatment Effects Across Nine Glucose-Lowering Drug Classes" (LEGEND-T2DM extension)
- **Link / version:** https://doi.org/10.1111/dom.70918. Author manuscript via PMC13310412 (medRxiv version 10.64898/2026.01.06.26343548 not opened). Peer reviewed.
- **Database:** six databases in the Observational Medical Outcomes Partnership (OMOP) common data model from the Observational Health Data Sciences and Informatics (OHDSI) network: US claims and EHR, and Japan.
- **Cohort size:** 743,691 initiators.
- **Treatments:** nine drug classes (36 pairwise comparisons), including SGLT2i, GLP-1 RA, DPP-4i, SU and TZD.
- **Outcome:** 11 outcomes (time to event, hazard ratios).
- **Covariates:** large-scale propensity score models, "often more than 10,000" covariates (§Statistical Analysis).
- **Estimators:**
  - Subgroup hazard ratios after propensity-score matching, empirically calibrated with 20 negative-control outcomes.
  - The difference in log hazard ratios across subgroups was meta-analysed with random effects.
- **Tuning and selection:**
  - Cross-validated L1-regularised logistic regression for the propensity score.
  - Diagnostics gating:
    - minimum detectable relative risk (MDRR) < 4
    - preference-score equipoise > 25%
    - maximum standardised mean difference (SMD) < 0.15
    - expected absolute systematic error (EASE) < 0.25.
- **Validation approach:** negative-control calibration and the diagnostic thresholds; results unblinded only after diagnostics passed.
- **Subgroups examined:** sex, age, renal impairment, obesity, hyperlipidaemia, hypertension, poor control, diabetic ketoacidosis, retinopathy and metabolic dysfunction-associated steatotic liver disease (MASLD).
- **Main result (null):**
  - "None of the signals demonstrated statistical significance after multiple testing correction" (§Results, abstract).
  - Only 516 of 5,148 planned comparisons passed diagnostics.
  - Renal impairment: "relative homogeneity rather than clear heterogeneity" (§Renal Impairment).

#### Row 12. Tang H et al. (2024). Alzheimers Dement, "Heterogeneous treatment effects of sodium-glucose cotransporter 2 inhibitors on risk of dementia in people with type 2 diabetes: A population-based cohort study"
- **Link / version:** https://doi.org/10.1002/alz.14048. VoR via PMC11350016. Peer reviewed.
- **Database:** OneFlorida+ (EHR linked to claims; US).
- **Cohort size:** 35,458.
- **Treatments:** SGLT2i versus SU.
- **Outcome:** all-cause dementia (risk difference over about 3.2 years).
- **Covariates:** all baseline covariates; HbA1c multiply imputed.
- **Estimators:** doubly robust learner (LinearDRLearner from EconML), followed by a single decision tree on the estimated effects (leaf size ≥ 500).
- **Tuning and selection:**
  - Logistic propensity model and LASSO outcome model.
  - "Cross-validated models based on mean squared error (MSE) were used to select the optimal hyperparameters" (§Statistical analyses).
- **Validation approach:**
  - "we used MSE to evaluate the performance of the model with a 5-fold cross-validation for internal validation and the testing set for external validation" (§Statistical analyses).
  - The "external" validation is a random 30% split, and MSE does not measure CATE error.
- **Subgroups examined:** Hispanic ethnicity and CKD defined four subgroups.
- **Main result:**
  - Risk difference −2.5% (−3.0 to −2.1).
  - Subgroup risk differences ranged from −4.3% to −0.9% (−1.9 to 0.2).

#### Row 13. Mori Y et al. (2026). Eur J Prev Cardiol, causal forest and target trial emulation. **Abstract only**
- **Link / version:** https://doi.org/10.1093/eurjpc/zwaf539. PMC12771345 (body not available through E-utilities). Peer reviewed. Full text UNVERIFIED.
- **Database:** Japanese nationwide insurer database (working age), 2015–2023.
- **Cohort size:** 150,830.
- **Treatments:** SGLT2i versus DPP-4i.
- **Outcome:** a composite of death, myocardial infarction (MI), stroke or HF over 3 years.
- **Covariates:** UNVERIFIED.
- **Estimators:** causal forest.
- **Tuning and selection:** UNVERIFIED.
- **Validation approach:** correlation of predicted benefit with a cardiovascular disease (CVD) risk score (r = 0.287). Other validation UNVERIFIED.
- **Subgroups examined:** CVD-risk strata. 91.0% of the low-risk group were predicted to benefit.
- **Main result:** "estimated benefit correlating weakly with CVD risk score (r = 0.287, P < 0.001)".

#### Row 14. Wendling T, Jung K, Callahan A, Schuler A, Shah NH, Gallego B (2018). Stat Med 37:3309–3324. **Abstract only**
- **Link / version:** https://doi.org/10.1002/sim.7820. PubMed abstract (PMID 29862536). Peer reviewed. Full text UNVERIFIED (Wiley blocked; no arXiv or PMC version found).
- **Database:** "4 published observational studies that used records from 2 major health care databases in the United States".
- **Cohort size:** UNVERIFIED.
- **Treatments:** binary treatments from the four source studies (UNVERIFIED).
- **Outcome:** binary outcome. Estimand: conditional risk difference.
- **Covariates:** real covariates and real treatment assignment.
- **Estimators:** BART, causal forests, causal boosting and causal multivariate adaptive regression splines (MARS).
- **Tuning and selection:** UNVERIFIED.
- **Validation approach:** plasmode-style. "real covariate and treatment assignment data are used and only outcomes are simulated based on nonparametric models of the real outcomes".
  - Note: resampling real treatment is the "Sample Treatment" design that row 24 criticises.
- **Subgroups examined:** UNVERIFIED.
- **Main result:** "Bayesian additive regression trees and causal boosting consistently provide low bias in conditional risk difference estimates".

### B. High-dimensional code covariates (hdPS with machine learning; learned representations)

#### Row 15. Wang T, Pate V, Wyss R, Buse JB, Kosorok MR, Stürmer T (2024). Am J Epidemiol 194(7):2085–97, high-dimensional iterative causal forest (hdiCF). **Abstract only**
- **Link / version:** https://doi.org/10.1093/aje/kwae322. Abstract via PubMed and PMC12234226. Peer reviewed. Full text UNVERIFIED.
- **Database:** 20% random sample of fee-for-service Medicare.
- **Cohort size:** UNVERIFIED.
- **Treatments:** SGLT2i versus GLP-1 RA.
- **Outcome:** hospitalised HF.
- **Covariates:** "high-dimensional feature identification by International Classification of Diseases, Current Procedural Terminology, and Anatomical Therapeutic Chemical codes" (ICD, CPT and ATC), turned into ordinal frequency variables.
- **Estimators:** hdPS-style feature generation, propensity-score trimming, then an iterative causal forest (iCF).
- **Tuning and selection:** UNVERIFIED. See row 17 for the published hdiCF settings.
- **Validation approach:** consistency with prior clinical evidence.
- **Subgroups examined:** data-driven subgroups.
- **Main result:** "HdiCF findings were consistent with studies suggesting SGLT2i to be more beneficial for patients with pre-existing heart failure or chronic kidney disease".

#### Row 16. Wang T et al. (2025). Am J Epidemiol, "A novel high dimensional approach to assess heterogeneous treatment effect in claims data". **Abstract only**
- **Link / version:** https://doi.org/10.1093/aje/kwaf127. Abstract via PMC12527247. Peer reviewed.
- **Database:** 20% Medicare sample, 2015–2019.
- **Cohort size:** 8,075 SGLT2i and 7,313 GLP-1 RA.
- **Treatments:** SGLT2i versus GLP-1 RA.
- **Outcome:** hospitalised HF over 2 years (adjusted risk difference, aRD).
- **Covariates:** top 200 prevalent codes in each dimension. One ordinal variable per code was compared against standard hdPS (up to three binary variables per code).
- **Estimators:** iCF, with CATEs from IPTW.
- **Tuning and selection:** UNVERIFIED.
- **Validation approach:** alignment with prior clinical evidence and sensitivity analyses.
- **Subgroups examined:**
  - With the new coding: ≥2 loop-diuretic prescriptions.
  - With hdPS coding: CKD.
- **Main result:**
  - Overall aRD −0.4% (−1.1 to 0.2), a null result.
  - The new coding found the loop-diuretic subgroup (−2.6%). hdPS coding found the CKD subgroup (−1.7%, CI crosses 0).
  - "our high-dimensional approach more accurately identified expected subgroups".
  - This judgement rests on agreement with prior evidence, not on a known truth.

#### Row 17. Wang T et al. (2025). Pharmacoepidemiol Drug Saf, "Glucagon-like Peptide-1 Receptor Agonists in Asthma Exacerbations: An Application of High-Dimensional Iterative Causal Forest to Identify Subgroups"
- **Link / version:** https://doi.org/10.1002/pds.70192. Author manuscript via PMC12831167. Peer reviewed.
- **Database:** MarketScan claims, 2016–2020.
- **Cohort size:** 4,878 GLP-1 RA and 3,806 SU (8,684 total).
- **Treatments:** GLP-1 RA versus SU. Sensitivity analysis: GLP-1 RA versus SGLT2i.
- **Outcome:** asthma exacerbation within 6 months.
- **Covariates:** 599 high-dimensional variables from ICD-10, CPT/HCPCS and ATC codes, plus age and sex.
- **Estimators:** hdiCF to find subgroups, then IPTW risk differences with predefined covariates.
- **Tuning and selection:**
  - 200 codes per dimension, 1% prevalence cut-off.
  - Top 5% of variables by importance.
  - 1,000 trees per depth, 100 iterations, 5-fold cross-validation.
  - The subgroup decision was chosen by "the smallest prediction error (0.025) for the transformed outcome model" (§CATE).
  - "cross-fitting was not used for computation efficiency" (§Statistical Analysis). This is a compute-driven choice that weakens honesty of inference.
- **Validation approach:**
  - Negative-control outcome (skin and soft-tissue infection).
  - Bias analysis for unmeasured confounding.
  - An alternative algorithm (aVirtualTwin).
  - Cross-validation stability.
- **Subgroups examined:** number of systemic steroid prescriptions (0, 1, ≥2).
- **Main result:**
  - ≥2 prescriptions: aRD −3.8% (−5.3, −2.2).
  - In the GLP-1 RA versus SGLT2i cohort, hdiCF "identified four unstable subgroups (stability=0.2, few events) with neutral effects" (§Sensitivity analyses). This is a failure result.

#### Row 18. Wyss R, Schneeweiss S, van der Laan M, Lendle SD, Ju C, Franklin JM (2018). Epidemiology 29(1):96–106. **Abstract only**
- **Link / version:** https://doi.org/10.1097/EDE.0000000000000762. PubMed abstract (PMID 28991001). Peer reviewed. Full text UNVERIFIED.
- **Database:** "plasmode simulations based on empirical data" (source databases UNVERIFIED).
- **Cohort size:** UNVERIFIED.
- **Treatments:** UNVERIFIED.
- **Outcome:** UNVERIFIED.
- **Covariates:** hdPS-generated variables.
- **Estimators:** hdPS combined with Super Learner (SL), scalable collaborative targeted maximum likelihood estimation (C-TMLE), and penalised regression.
- **Tuning and selection:** the number of hdPS variables chosen data-adaptively, by SL, C-TMLE or penalisation.
- **Validation approach:** plasmode simulation; bias and mean squared error (MSE) of the effect estimates.
- **Subgroups examined:** none (ATE).
- **Main result:**
  - "the high-dimensional propensity score can be sensitive to the number of variables included for adjustment and that severe overfitting of the propensity score model can negatively impact the properties of effect estimates".
  - hdPS combined with SL was the most consistent strategy.

#### Row 19. Ju C, Combs M, Lendle SD, Franklin JM, Wyss R, Schneeweiss S, van der Laan MJ (2019). J Appl Stat 46(12):2216–2236
- **Link / version:** https://arxiv.org/abs/1703.02236v2 (read). Published as doi:10.1080/02664763.2019.1582614 (PMC7444746, not compared). Preprint version read; the published version is peer reviewed.
- **Database:** three US claims datasets: a novel oral anticoagulant (NOAC) study, a non-steroidal anti-inflammatory drug (NSAID) study (Medicare and Pennsylvania), and a Vytorin study (United Healthcare).
- **Cohort size:** NOAC 18,447 ("60 pre-defined baseline covariates and 23,531 unique claims codes", p.3). NSAID 49,653. Vytorin 148,327.
- **Treatments:** the treatment of each study (for example COX-2 inhibitor versus non-selective NSAID).
- **Outcome:** treatment assignment (propensity-score prediction only).
- **Covariates:** predefined covariates plus hdPS-generated code variables.
- **Estimators:** SL library (parametric and non-parametric) with or without hdPS.
- **Tuning and selection:** SL cross-validation over the library.
  - hdPS screening was **not** cross-validated: "the computation is too expensive for this procedure, so there is an additional risk of overfitting" (p.19). This is a compute-driven choice that weakens the science.
- **Validation approach:** negative log-likelihood and area under the curve (AUC) for propensity-score prediction. **No evaluation of effect estimates.**
- **Subgroups examined:** none.
- **Main result:** "the best individual algorithm, in terms of predictive performance, varied across datasets" (p.1). SL combined with hdPS was the most consistent.

#### Row 20. Wyss R, Yanover C, El-Hay T, Bennett D, Platt RW, Zullo AR et al. (2022). Pharmacoepidemiol Drug Saf 31(9):932–943. Overview
- **Link / version:** https://doi.org/10.1002/pds.5500. VoR via PMC9541861. Peer reviewed (review).
- **Database:** not applicable (overview of administrative healthcare databases).
- **Cohort size:** not applicable.
- **Treatments:** not applicable.
- **Outcome:** not applicable.
- **Covariates:** feature generation from codes.
  - "The hdPS has become the most widely used tool to generate features based on observed coding patterns".
  - Learned representations: "The use of neural networks for extracting confounder information by modeling complex coding patterns is promising but examples are limited" (§Generating features…).
- **Estimators:** reviewed: regularised regression, hdPS with SL, scalable C-TMLE, doubly robust machine learning.
- **Tuning and selection:** reviewed (covariate prioritisation and selection).
- **Validation approach (reviewed):** plasmode, Wasserstein generative adversarial networks (WGAN) synthetic data, negative and positive controls, and quantitative bias analysis.
  - Caveat: synthetic validation "could still be biased towards favoring causal inference methods that mimic the modeling choices made when generating the synthetic datasets" (§Parametric bootstrap ('Plasmode') simulation).
- **Subgroups examined:** none.
- **Main result:** "relatively little has been written on best practices for feature generation and diagnostic assessment" (§Results, abstract).

#### Row 21. Wyss R et al. (2024). Am J Epidemiol 193(11):1632–1640, "Targeted learning with an undersmoothed LASSO propensity score model…". **Abstract only**
- **Link / version:** https://doi.org/10.1093/aje/kwae023. PubMed abstract (PMID 38517025). Peer reviewed. Full text UNVERIFIED.
- **Database:** simulations (data source UNVERIFIED).
- **Cohort size:** UNVERIFIED.
- **Treatments:** UNVERIFIED.
- **Outcome:** UNVERIFIED.
- **Covariates:** large-scale covariate sets.
- **Estimators:** LASSO propensity score (PS) inside singly and doubly robust estimators, with collaborative targeted learning.
- **Tuning and selection:** "collaborative-controlled targeted learning to data-adaptively select the degree of undersmoothing".
- **Validation approach:** simulation (bias).
- **Subgroups examined:** none (ATE).
- **Main result:**
  - Collaborative learning "can data-adaptively select the degree of undersmoothing to reduce bias".
  - "the use of cross-fitting was important for avoiding nonoverlap in covariate distributions".

#### Row 22. Wyss R, Hansen BB, Hahn G, van der Laan L, Lin KJ (2026). Stat Med, "Undersmoothed LASSO Models for Propensity Score Weighting and Synthetic Negative Control Exposures for Bias Detection"
- **Link / version:** https://arxiv.org/abs/2506.17760v3 (16 Dec 2025, read). Published Stat Med 2026, doi:10.1002/sim.70503 (PMC13055431, not opened). Preprint version read.
- **Database:** Monte Carlo simulations that mimic sparse, high-dimensional healthcare-database structure. No real cohort.
- **Cohort size:** varied (simulation).
- **Treatments:** binary exposure. The true effect was null by design.
- **Outcome:** binary outcome (rare).
- **Covariates:** sparse binary indicators (setup 1); non-linear continuous covariates (setup 2).
- **Estimators:** LASSO PS weighting.
- **Tuning and selection:** undersmoothing chosen by covariate-balance criteria, compared with cross-validation that minimises prediction error.
- **Validation approach:** synthetic negative-control exposures to detect bias. The authors use them for detection rather than selection to avoid "overfitting to the synthetic data" (p.11).
- **Subgroups examined:** none (ATE).
- **Main result:**
  - "undersmoothing the LASSO models using balance diagnostics resulted in less bias in estimated exposure effects when compared to tuning using cross-validation" (p.20).
  - Limitation: "the magnitude of bias within the synthetic negative control studies (synthetic bias) was smaller than the bias in the study population" (p.21).

### C. Validation without a known effect

#### Row 23. Franklin JM, Schneeweiss S, Polinski JM, Rassen JA (2014). Comput Stat Data Anal 72:219–226
- **Link / version:** https://doi.org/10.1016/j.csda.2013.10.018. Author manuscript via PMC3935334. Peer reviewed.
- **Database:** Medicare Parts A/B linked to Caremark prescription claims.
- **Cohort size:** 236,314 statin initiators. Simulated datasets: 500 × 100,000.
- **Treatments:** high- versus low-intensity statin.
- **Outcome:** MI or acute coronary syndrome (ACS) with revascularisation, within 180 days (time to event).
- **Covariates:** 61 outcome-model covariates. The full pool comprises all claims in the 180 days before initiation.
- **Estimators evaluated:** crude Cox model; age/sex/year-adjusted model; all-variables model; all-variables PS; exposure-based hdPS; bias-based hdPS.
- **Tuning and selection:** the outcome model used penalised splines (2 degrees of freedom) and ridge regression with penalty θ = 1, set by the authors (§3.1).
- **Validation approach:** plasmode.
  - Covariates **and exposure** are resampled together, and outcomes are simulated with a chosen true HR (1.0 or 1.5).
  - "resampling from the observed covariate and exposure data without modification" (§Abstract).
  - The true effect is constant (no heterogeneity).
- **Subgroups examined:** event rates by sex, prior MI or ACS, diabetes and rheumatoid arthritis (realism checks only).
- **Main result:**
  - hdPS reduced bias from the crude estimate by 88% (scenario 1) and 70% (scenario 2).
  - The all-variables PS was biased under a non-null HR because of non-collapsibility.
  - The authors' limitation: "conclusions … are limited to the specific data-generating scenarios explored" (§4 Discussion).

#### Row 24. Shaw PA, Gruber S, Williamson BD, Desai R, Shortreed SM, Krakauer C, Nelson JC, van der Laan MJ (2025 preprint; Stat Med 2026)
- **Link / version:** https://arxiv.org/abs/2504.11740v1 (read). Published https://doi.org/10.1002/sim.70676 (abstract compared via PMC13392349). The arXiv preprint was read; the published version is peer reviewed.
- **Database:** synthetic scenarios plus Kaiser Permanente Washington (KPWA) EHR.
- **Cohort size:** KPWA "50,337 individuals 13 years and older initiating antidepressant medication or psychotherapy" (p.13).
- **Treatments:** antidepressant medication versus psychotherapy. Synthetic binary treatment.
- **Outcome:** binary and continuous outcomes (point-treatment ATE).
- **Covariates:** KPWA EHR covariates, including the PHQ-9 (Patient Health Questionnaire-9) item 9 score and prior self-harm.
- **Estimators evaluated:**
  - IPTW
  - glmPS (PS-adjusted logistic regression, as the paper labels it)
  - glmCM (G-computation)
  - matching
  - TMLE (targeted maximum likelihood estimation).
- **Tuning and selection:** estimators were mostly correctly specified, to isolate the effect of the plasmode design.
- **Validation approach:** compares the "Sample Treatment" plasmode (as in Franklin 2014) with the "Generate Treatment" plasmode.
- **Subgroups examined:** none.
- **Main result:**
  - "the positivity assumption required for identifying a causal estimand … is violated under the Sample Treatment framework" (p.7).
  - Under that design, PS-based estimators look biased, with undercoverage, even at large n.
  - Recommendation: generate the treatment from a flexibly fitted PS: "We recommend avoiding simplistic parametric models for the DGM by flexible modeling or machine learning" (p.15).

#### Row 25. Karim ME (2026a). arXiv:2609.24053v1, "When bad adjustment looks good: what goes wrong in Plasmode 0.1.0 simulations"
- **Link / version:** https://arxiv.org/abs/2609.24053v1. Preprint, not peer reviewed.
- **Database:** a synthetic cohort and the SUPPORT/Right Heart Catheterisation (RHC) cohort (critical care, not EHR or claims).
- **Cohort size:** 200 null replicates per strategy (source n not checked).
- **Treatments:** RHC versus no RHC.
- **Outcome:** binary.
- **Covariates:** source-cohort covariates.
- **Estimators evaluated:** five estimators, correctly or deliberately incorrectly specified.
- **Tuning and selection:** not applicable.
- **Validation approach:** a software audit of the archived R package Plasmode 0.1.0, which uses the generate-treatment design.
- **Subgroups examined:** none.
- **Main result:**
  - "A sampled subject usually received another subject's exposure probability" (p.1).
  - "With the unmodified generator, all five appeared similarly unbiased" (p.1), including misspecified estimators. A faulty benchmark can make bad adjustment look good.

#### Row 26. Karim ME (2026b). arXiv:2609.26186v1, "A Plasmode Benchmark Can Refute but Cannot Certify"
- **Link / version:** https://arxiv.org/abs/2609.26186v1. Preprint, not peer reviewed. The PDF header date (10 Aug 2026) does not match the 2609 identifier.
- **Database:** theory, with the RHC cohort as a real-data example.
- **Cohort size:** not checked.
- **Treatments:** RHC.
- **Outcome:** binary (risk-difference ATE).
- **Covariates:** RHC covariates (fine-grained versus coarsened).
- **Estimators evaluated:** IPW, augmented inverse probability weighting (AIPW) and TMLE with flexible (super learner) or parametric nuisance models.
- **Tuning and selection:** cross-fitting compared with no cross-fitting.
- **Validation approach:** plasmode theory, separating regularity (overlap) from projection (the injected outcome model).
- **Subgroups examined:** none.
- **Main result:**
  - "Resampling the real treatment with fine-grained covariates destroys it, and the resulting coverage failure falls on flexible, machine-learning-based estimators", and "cross-fitting removes only part of it" (p.1).
  - The injected outcome model "can reverse estimator rankings even when overlap is intact" (p.1).
  - "A plasmode is a filter against estimators, not a warrant for them" (p.1).

#### Row 27. Yadlowsky S, Fleming S, Shah N, Brunskill E, Wager S (2025). J Am Stat Assoc, "Evaluating Treatment Prioritization Rules via Rank-Weighted Average Treatment Effects"
- **Link / version:** https://doi.org/10.1080/01621459.2024.2393466. Author manuscript via PMC12002561 (arXiv:2111.07966). Peer reviewed.
- **Database:** randomised trials (International Stroke Trial; SPRINT and ACCORD-BP), plus simulations. **No EHR application.**
- **Cohort size:** varies by application.
- **Treatments:** aspirin; intensive blood-pressure control.
- **Outcome:** binary and time to event.
- **Covariates:** trial baseline covariates.
- **Estimators:** metric only. It scores any prioritisation rule, CATE-based or risk-based.
- **Tuning and selection:** not applicable. Nuisance models are cross-fitted with random forests in the simulation.
- **Validation approach:** rank-weighted average treatment effect (RATE). This family includes the area under the targeting operator characteristic (AUTOC) and the Qini coefficient.
  - It is valid "in a wide variety of randomized and observational study settings" (§Abstract), and for observational data only under unconfoundedness with AIPW scores.
  - "We recommend using AIPW scores for estimating the RATE in both randomized trial and observational study settings" (§Choosing a RATE Metric and Score).
- **Subgroups examined:** prioritisation by CATE versus by risk.
- **Main result:** methodological. It provides inference (a central limit theorem) for RATE and Qini.

#### Row 28. Chen H et al. (2026). Am J Epidemiol, "Machine learning methods for estimating personalized treatment effects—insights on validity from two large trials"
- **Link / version:** https://doi.org/10.1093/aje/kwag065. VoR via PMC13437088. Peer reviewed.
- **Database:** two randomised trials (International Stroke Trial, IST; Chinese Acute Stroke Trial, CAST). Not EHR. Included because the paper tests the validation metrics themselves.
- **Cohort size:** IST 19,435; CAST 21,106 (20,614 after cleaning).
- **Treatments:** aspirin versus none.
- **Outcome:** death or dependency (binary).
- **Covariates:** 16 shared baseline covariates.
- **Estimators:** 17 causal machine-learning methods (meta-learners, tree-based and deep learning).
- **Tuning and selection:** not reported in the main text ("fine-tuning" mentioned). UNVERIFIED.
- **Validation approach:**
  - Internal splits (random and geographical) and cross-trial external validation.
  - c-for-benefit, model-based concordance for benefit (mbcb), calibration pseudo-R², and grouped ATE-versus-ITE plots (ITE: individual treatment effect).
- **Subgroups examined:** strata of predicted ITE (benefit or harm).
- **Main result (negative):**
  - "none of the ML methods consistently demonstrated reliable performance, neither internal nor external" (§Abstract).
  - Example: T-learner random forest c-for-benefit was 0.972 in training and 0.491 in test (Table 1).

### D. Estimator and hyperparameter selection under confounding

#### Row 29. Mahajan D, Mitliagkas I, Neal B, Syrgkanis V (2024). ICLR 2024
- **Link / version:** https://arxiv.org/abs/2211.01939v3 (camera-ready, "Published as a conference paper at ICLR 2024"). Peer reviewed.
- **Database:** semi-synthetic, **not EHR**:
  - 75 ACIC 2016 datasets (Atlantic Causal Inference Conference), whose covariates come from the Collaborative Perinatal Project
  - LaLonde PSID and CPS
  - Twins (RealCause).
- **Cohort size:** varies.
- **Treatments:** binary.
- **Outcome:** continuous or binary, with a known true CATE.
- **Covariates:** dataset-specific.
- **Estimators:** 415 CATE estimators (seven meta-learner types). 34 surrogate selection metrics.
- **Tuning and selection:**
  - Nuisance models of both estimators and metrics were tuned with AutoML (FLAML).
  - A two-level strategy was used: tune within each meta-learner class first, then select across classes.
- **Validation approach:** normalised PEHE (precision in estimating heterogeneous effects) of the selected estimator.
- **Subgroups examined:** none.
- **Main result:**
  - "Doubly Robust and TMLE variants are globally dominating metrics" (p.7).
  - "plug-in metrics based on T-Learner are never dominated" (p.2).
  - The R-score did poorly: normalised PEHE 4.0 on ACIC 2016 versus 0.56 for DR T-score (Table 1, p.8).
  - The Qini DR score was poor under single-level selection.
  - The two-level strategy was better in about 28.7% of cases and never worse (p.8).

#### Row 30. Doutreligne M, Varoquaux G (2025). GigaScience 14:giaf016
- **Link / version:** https://doi.org/10.1093/gigascience/giaf016. VoR via PMC11927402. arXiv:2302.00370v2 was also read. Peer reviewed.
- **Database:** simulations (Caussim) plus three semi-simulated datasets with real covariates: ACIC 2016 (Collaborative Perinatal Project), ACIC 2018 (Linked Births and Infant Deaths Database, LBIDD) and Twins. **Not EHR or claims.**
- **Cohort size:** for example ACIC 2016 has 4,802 individuals (770 instances). Twins N = 11,984.
- **Treatments:** binary (synthetic).
- **Outcome:** synthetic.
- **Covariates:** real covariates.
- **Estimators:** candidate G-computation outcome models (a family of 18 gradient-boosting configurations for the semi-simulated data).
- **Tuning and selection:**
  - Risks compared: μ-risk (outcome MSE), inverse-propensity-weighted μ-risk, τ-risk variants, U-risk, and the R-risk.
  - Nuisances fitted with a stacked ridge plus boosting model.
- **Validation approach:** Kendall rank correlation with the oracle risk.
- **Subgroups examined:** levels of overlap (normalised total variation).
- **Main result:**
  - "the mean squared error, classically used to evaluate predictive modes, is worse" (§Results, abstract).
  - The R-risk "leads to the best performances". Nuisances are "best estimated with flexible estimators such as a super learner".
  - "Model selection is harder for low population overlap" (§heading). The best data split was 90/10.

#### Row 31. Bach P, Schacht O, Chernozhukov V, Klaassen S, Spindler M (2024). CLeaR 2024, PMLR 236
- **Link / version:** https://arxiv.org/abs/2402.04674v1 (read). PMLR version https://proceedings.mlr.press/v236/bach24a.html exists (not compared). Peer reviewed at CLeaR.
- **Database:** ACIC 2019 data challenge: "1600 data sets from 16 data generating processes … p = 200 covariates" (p.7). Plus a Belloni-style design. **Not EHR.**
- **Cohort size:** n = 1,000 or 2,000.
- **Treatments:** binary.
- **Outcome:** continuous.
- **Covariates:** 200.
- **Estimators:** double machine learning (DML), with the partially linear regression (PLR) and interactive regression (IRM) models. Learners: lasso, random forest, XGBoost, FLAML (AutoML) and stacking.
- **Tuning and selection:**
  - Tuning on the full sample, on folds, or on a split sample.
  - Learner selection by combined out-of-sample nuisance loss, by predictive error on the outcome Y, or by stacking.
- **Validation approach:** relative RMSE of the ATE against the known truth.
- **Subgroups examined:** none. CATE is explicitly left to future work: "extend the simulation framework to conditional average treatment effects (CATE)" (p.13).
- **Main result:**
  - "the use of default parameter estimators can lead to significant bias in the causal estimate" (p.13).
  - Choosing the learner with the lowest combined nuisance loss gave the best mean relative RMSE.
  - However, "the lowest nuisance prediction error did not always translate in the optimal ML configuration for DML" (p.13).

#### Row 32. Doutreligne M, Struja T, Abecassis J, Morgand C, Celi LA, Varoquaux G (2025). PLOS Digit Health 4(2):e0000721, "Step-by-step causal analysis of EHRs to ground decision-making"
- **Link / version:** https://doi.org/10.1371/journal.pdig.0000721. VoR via PMC11790099 (arXiv:2308.01605v4 is the preprint). Peer reviewed.
- **Database:** MIMIC-IV v2.2 (intensive care EHR, one US hospital).
- **Cohort size:** 18,121 (3,559 treated).
- **Treatments:** crystalloids plus albumin versus crystalloids alone.
- **Outcome:** 28-day mortality.
- **Covariates:** expert-selected confounders with several aggregations over time.
- **Estimators:** outcome regression, IPW, AIPW, double machine learning, and causal forest (S8 Fig). Nuisance models: random forests or ridge logistic regression.
- **Tuning and selection:** "We chose the hyperparameters with a random search procedure (S5 Appendix)" (§Outcome and treatment estimators). The estimator was chosen by agreement with RCT meta-analyses and methodological literature.
- **Validation approach:**
  - Benchmark against trials: the ATE was compared with pooled RCTs showing no effect.
  - "Vibration analysis" across design, confounder and estimator choices.
- **Subgroups examined:** age ≥ 60, sex, septic shock, and one further binary characteristic.
- **Main result:**
  - "a doubly robust estimator (AIPW) with random forests proved to be the most reliable estimator" (§Abstract).
  - Albumin appeared beneficial in age ≥ 60, males and septic shock.
  - The CATE step was trusted after the *ATE* matched trials: "Having validated the analytical pipeline, we can use it to inform decision-making" (§Step 5). No check targeted the heterogeneity itself.

### E. Tabular foundation models applied to EHR or registry data

#### Row 33. Kurmann C et al. (2026). Stroke, "Differential Effect of Endovascular Treatment in Medium or Distal Vessel Occlusion: A DISTAL Secondary Analysis". **Abstract only**
- **Link / version:** https://doi.org/10.1161/STROKEAHA.126.057558. PubMed abstract (PMID 42961033). Peer reviewed (online ahead of print). Full text UNVERIFIED.
- **Database:**
  - Development: the Bernese Stroke Registry (single hospital).
  - Application: the DISTAL RCT.
- **Cohort size:** development 257; DISTAL 539 (270 + 269).
- **Treatments:** endovascular treatment (EVT) plus best medical treatment versus best medical treatment alone.
- **Outcome:**
  - Model target: excellent early neurological outcome (EENO; National Institutes of Health Stroke Scale score 0–2 at 24 hours).
  - Trial outcome: shift in the modified Rankin Scale at 90 days.
- **Covariates:** UNVERIFIED.
- **Estimators:** "A Tabular Prior-Data Fitted Network (TabPFN) model was trained to predict EENO". It is a risk model used for risk-based heterogeneity analysis, **not** a CATE estimator.
- **Tuning and selection:** UNVERIFIED (version and settings not in the abstract).
- **Validation approach:** external AUC 0.73, and a treatment-by-predicted-risk interaction in the RCT.
- **Subgroups examined:** predicted EENO yes or no; admission NIHSS ≤ 4 versus > 4.
- **Main result:**
  - Interaction p = 0.012.
  - "A model using admission NIHSS alone showed comparable discrimination (area under the receiver operating characteristic curve 0.71)". A one-variable rule matched TabPFN.

---

## 3. Synthesis

**What is established.**

1. **The Exeter programme has built a consistent way to validate CATE without a counterfactual** (rows 1, 3, 4).
   - Patients are stratified by predicted CATE, a confounder-adjusted ATE is estimated within each stratum, and it is compared with the mean prediction.
   - This uses grouped calibration plus concordant-versus-discordant contrasts (rows 1 and 5).
   - It is applied across CPRD GOLD and Aurum, Scotland and ethnic groups.
   - It can detect failure. In row 1 it showed that a causal forest run with **default** tuning was under-dispersed and miscalibrated, while penalised regression with interactions calibrated well.
2. **Recalibration is cheap and often needed.** Row 3 needed intercept shifts of 1.6 to 3.0 mmol/mol for DPP-4i across ethnic groups, while the slopes held.
3. **Simple routine features carry most of the usable heterogeneity in HbA1c response.** The features are HbA1c, age, BMI, eGFR, ALT and sex (rows 2–5).
   - The one design that observes within-person differential response, the TriMaster crossover (row 6, abstract only), favoured direct outcome prediction over clusters. DDRTree was null.
   - For hard outcomes (HF and kidney), the Exeter group instead combines a validated risk score with a constant relative effect from trials (rows 7, 8).
   - Their own analyses found no heterogeneity on the relative scale: interaction p = 0.82 (row 7) and p = 0.99 / 0.71 (row 8). Large heterogeneity on the HR scale was also null in a multi-database analysis after correction for multiple testing (row 11).
4. **Plasmode design choices drive conclusions.**
   - Resampling the observed treatment, as in Franklin (row 23) and Wendling (row 14), induces positivity failure. That penalises PS-based estimators (row 24) and flexible machine-learning estimators (row 26).
   - Plasmodes favour estimators that match the injected outcome model (rows 20, 26).
   - Implementation bugs can make misspecified estimators look unbiased (row 25).
5. **Tuning matters.** Default learners bias DML (row 31), and tuning nuisance models with AutoML changes which selection metric wins (row 29). Cross-validation tuned for prediction is not optimal for PS weighting (rows 21, 22). hdPS is sensitive to the number of variables (row 18).

**What is contested.**

1. **Which selection risk to use.**
   - Row 30 recommends the R-risk.
   - Row 29 finds the R-score among the worst, with doubly robust and T-learner plug-in scores best.
   - The two differ in the candidate families compared (G-computation hyperparameters versus meta-learners) and in nuisance tuning.
   - Neither evaluated EHR or claims data.
2. **Whether CATE machine learning beats regression in routine data.**
   - Row 1 says no, for low-dimensional HbA1c data.
   - Row 14 (abstract) favours BART and causal boosting in plasmode tests.
   - Row 4 deploys BCF with good calibration.
   - Row 28 shows that 17 machine-learning methods fail to generalise even within large RCTs.
3. **Whether hdPS-style code features improve subgroup discovery** (rows 15–17).
   - The claims rest on agreement with prior clinical beliefs, not on a known truth.
   - hdiCF produced unstable subgroups in a second cohort (row 17).
   - Cross-fitting was skipped for compute reasons (row 17).

**What is missing.**

1. **No study validated CATE estimates in UK EHR against a known effect.** No plasmode with heterogeneous effects was built on CPRD. Franklin's plasmode used a constant effect (row 23).
2. **No paper applied RATE or Qini to EHR or claims.** The RATE paper used trials (row 27).
3. **No selection-metric study used EHR or claims covariates** (rows 29–31). Bach covers ATE only.
4. **No paper used a tabular foundation model to estimate treatment effects in EHR or claims** (section 5).
5. **Grouped-calibration validation relies on the same no-unmeasured-confounding adjustment as the estimates themselves** (rows 3, 4).
   - In the SABRE design (row 7) the "observed" benefit came from a constant-HR model, so heterogeneity in relative effect could not be detected.
6. **Benchmarking ATEs against trials can certify the wrong answer.**
   - In row 10, IV and no-unmeasured-confounding estimates in *opposite directions* both "agreed" with the trial.
   - In row 32, an ATE match was taken as licence for CATE claims.
7. **Time-to-event CATE estimators in EHR were rare.** Most HF and kidney work used risk times a constant HR (rows 7, 8).
8. **Kidney function (eGFR) as an effect modifier of glycaemic response is under-examined.** eGFR < 45 was excluded in rows 1–3, and only 6.7% had eGFR < 60 in row 9.

**Answer to the brief's question: what is used when the true effect is unknown, and how good it is.**

| Method used | Where (rows) | Evidence on how good it is |
|---|---|---|
| Grouped calibration (deciles or clinical cut-offs, adjusted subgroup ATE versus mean predicted CATE) | 1, 3, 4, 5, 7, 8 | It detected a miscalibrated causal forest (row 1). It is only as unbiased as the confounding adjustment, and only at subgroup level (row 3 says so). No study has quantified its error against a known truth. |
| Concordant versus discordant comparison | 1, 5 | Supports clinical utility. Shares the confounding assumptions above. |
| Benchmarking against RCTs (develop in trials, test in EHR, or the reverse; ATE agreement) | 1, 2, 5, 6, 10, 32 | The strongest available. A within-person crossover (row 6) is the closest to individual truth. ATE agreement is weak: opposite-direction estimates both "agreed" (row 10). Trials exclude subgroups (row 10). |
| Negative-control outcomes or exposures, and empirical calibration | 11, 17, 22 | They detect residual bias. Synthetic negative controls under-estimated bias magnitude (row 22). They address ATE bias, not heterogeneity. |
| Plasmode simulation | 14, 18, 23–26 | Useful as a filter. It "can refute but cannot certify" (row 26). Results are sensitive to the treatment design (row 24), to the injected outcome model (rows 20, 26) and to software errors (row 25). |
| Surrogate risks for selection (R-risk, DR, T/X plug-ins, Qini) | 29, 30 | They work on semi-synthetic data with tuned nuisances, but disagree on the best risk. Not tested on EHR. |
| RATE, Qini and c-for-benefit | 27, 28, 29 | Formal inference exists (row 27). In RCTs, c-for-benefit exposed failure of machine-learning CATE models (row 28). Qini-based selection was poor in single-level selection (row 29). |

---

## 4. Excluded near-misses

| # | Citation | Link | Reason for exclusion |
|---|---|---|---|
| N1 | Weberpals J et al. (2021) Deep learning-based propensity scores… Epidemiology | https://doi.org/10.1097/EDE.0000000000001338 | Learned representation (autoencoder) for PS in real-world data. Only the PubMed record was seen (no PMC); not opened, so excluded under the "open everything" rule. A strong candidate to open next for "learned representations". |
| N2 | Venkatesan S et al. (2025) Dimensionality reduction techniques for improving propensity score specification… claims data. Pharmacoepidemiol Drug Saf | https://doi.org/10.1002/pds.70258 | Relevant to representations; Wiley blocked and no PMC version; not opened. |
| N3 | Ghosh S et al. (2021) Deep propensity network using a sparse autoencoder. J Am Med Inform Assoc | https://doi.org/10.1093/jamia/ocaa346 | Title-level only; ATE-focused representation learning; not opened in time. |
| N4 | Shen L et al. (2024) A Two-Step Framework for Validating Causal Effect Estimates. Pharmacoepidemiol Drug Saf | https://doi.org/10.1002/pds.5873 | Benchmarking against trials, but in cancer registry data and at ATE level. Abstract only (Wiley). |
| N5 | Brooks JM et al. (2024) Causal forest under essential heterogeneity. BMC Med Res Methodol | https://doi.org/10.1186/s12874-024-02187-5 | Opened (PMC10935905). A pure simulation not built on EHR or claims data. Notable null result: causal forest estimates were biased for untreated patients under essential heterogeneity. |
| N6 | Brooks JM et al. (2022) IV causal forest… BMC Med Res Methodol | https://doi.org/10.1186/s12874-022-01663-0 | Title and record only; not opened. |
| N7 | Post RAJ et al. (2024) Flexible ML estimation of CATE: a blessing and a curse. Epidemiology | https://doi.org/10.1097/EDE.0000000000001684 | Methods commentary or simulation; no PMC; not opened. |
| N8 | Lai Y et al. (2026) Statins and dementia, target trial emulation with causal machine learning (UK Biobank). Alzheimers Dement | https://doi.org/10.1002/alz.71178 | Opened (PMC12945722). Not a T2D drug. Validation and tuning not examined in depth (time). A candidate UK Biobank row. |
| N9 | Mourao F et al. (2026) PFNs for causal inference: a simulation study with real-world scenarios. arXiv:2603.15928v2 | https://arxiv.org/abs/2603.15928v2 | Opened. ATE only, with a trial and a breast-cancer cohort (n = 570; n = 2,260), not EHR or claims. Belongs to Brief 1. Finding: G-computation with TabPFN was "highly biased", and CausalPFN had poor coverage (p.1). |
| N10 | Ma Q et al. (2026) HFpEF phenotyping (MIMIC-IV), Front Pharmacol | https://doi.org/10.3389/fphar.2026.1838338 | TabPFN used only as a phenotype classifier, not for treatment effects (abstract opened). |
| N11 | Qian ET et al. (2026) Cefepime vs piperacillin-tazobactam ITE. Am J Respir Crit Care Med | https://doi.org/10.1093/ajrccm/aamag544 | Uses Qini, but in RCT data (ACORN), not EHR (abstract opened). |
| N12 | Afshar M et al. (2024) Buprenorphine vs naltrexone ITE. J Addict Med | https://doi.org/10.1097/ADM.0000000000001313 | Qini and c-for-benefit in RCT data, not EHR (abstract opened). |
| N13 | Jansz TT et al. (2026) GLP-1 RA kidney outcomes in SGLT2i users, CPRD target trial emulation. Lancet Prim Care | https://doi.org/10.1016/j.lanprc.2026.100139 | Opened (PMC13153036). An ATE comparative-effectiveness study; heterogeneity not the aim. |
| N14 | Kongmalai T et al. (2026) Heterogeneity in SGLT2i effect on CKD. Diabetol Metab Syndr | https://doi.org/10.1186/s13098-026-02249-2 | Full text downloaded (PMC13689252) but not analysed for lack of time. Relevant; a priority for a follow-up. |
| N15 | Keele L et al. (2026) Exploring HTE for GLP-1 RA in T2D. Am J Epidemiol; Xu Y et al. (2026) HTE of GLP-1 RA on kidney outcomes. Kidney Int | https://doi.org/10.1093/aje/kwag261 ; https://doi.org/10.1016/j.kint.2026.06.041 | Directly relevant titles, but no PMC version; not opened. Excluded under the open-everything rule. |
| N16 | Deng Y et al. (2025) Heterogeneity of CV effects of second-line therapies across moderate baseline risk. J Am Heart Assoc | https://doi.org/10.1161/JAHA.124.040217 | Title-level only; not opened (time). |
| N17 | Young KG et al. (2023) Systematic review of treatment effect heterogeneity for GLP-1 RA and SGLT2i. Commun Med | https://doi.org/10.1038/s43856-023-00359-w | A review of mainly trial-based heterogeneity; not opened. |
| N18 | Cardoso P et al. (2024) Dirichlet process mixture models to impute missing predictors in counterfactual prediction. BMC Med Inform Decis Mak | https://doi.org/10.1186/s12911-023-02400-3 | Missing-data method for Exeter models; title-level only; not opened. |
| N19 | Schreck N et al. (2024) Statistical plasmode simulations: potentials, challenges and recommendations. Stat Med (arXiv:2305.06028) | https://arxiv.org/abs/2305.06028 | General plasmode review; not opened (Shaw and Karim cover the causal-specific issues). |
| N20 | arXiv:2607.07065 (2026) Which regularized PS and doubly robust methods are best calibrated when exposures or outcomes are rare? | https://arxiv.org/abs/2607.07065 | Title-level only (ATE, plasmode); not opened. |

---

## 5. Brief-specific answers

**Is there evidence on tabular foundation models applied to EHR for treatment effects?**
- **None found.** The only clinical use found trains TabPFN as a *risk* model on a hospital registry (n = 257) and applies it to an RCT (row 33).
- In that study a one-variable rule (admission NIHSS) matched it.
- The one PFN causal study on real-world-based scenarios (N9) is ATE-only, uses non-EHR data, and reports bias for G-computation with TabPFN and poor CausalPFN coverage.

**Which tuning procedure was actually used in the core EHR papers?**

| Row | Tuning procedure |
|---|---|
| 1 | Regression penalties tuned by AIC. Causal forest **defaults**. |
| 3 | Closed-testing recalibration. |
| 4 | BCF variable selection by splitting probability; priors UNVERIFIED. |
| 7, 8 | None (fixed formulas). |
| 9, 10 | LASSO for variables and interactions. |
| 11 | Cross-validated L1 propensity score plus diagnostic thresholds. |
| 12 | Cross-validation on nuisance MSE. |
| 17 | hdiCF chosen by transformed-outcome prediction error, without cross-fitting. |
| 2, 5, 13, 14 | UNVERIFIED (abstract only). |

**Which subgroups were examined and what was found?**

| Subgroup | Rows | Finding |
|---|---|---|
| Ethnicity | 3, 4, 7, 10, 12 | Greater DPP-4i response in non-White groups. SGLT2i predictions held (row 3). Consistent GLP-1 RA/SGLT2i differences (row 4). Wide CIs for HF HRs (row 7). Hispanic ethnicity defined subgroups (row 12). |
| Sex | 4, 11 | Women respond more to GLP-1 RA, replicated in a trial (row 4). Nominal signals only (row 11). |
| Kidney function | 8, 11, 12 | No relative-effect modification by albuminuria (row 8). Homogeneity (row 11). CKD defined subgroups (row 12). Excluded or under-represented in rows 1–3 and 9. |
| BMI | 2, 4, 10 | Part of the selection models (rows 2, 4). Heterogeneity by BMI (row 10). |
| Age | 9, 10, 32 | Smaller SGLT2i HbA1c advantage in older people (row 9). |
