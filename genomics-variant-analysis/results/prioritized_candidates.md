# Prioritized Candidates — Manual Curation

`candidates_homozygous_rare_coding.csv` contains **51 variants** that survive
the stricter automated funnel (PASS quality &rarr; exonic/ANNOVAR-annotated
splicing &rarr; protein-altering &rarr; MAF ≤0.1% in each checked population
database or absent &rarr; homozygous in the proband). The original 67-variant
MAF ≤1% exploratory set is retained as
`candidates_homozygous_rare_coding_broad_1pct.csv`. Automated tiering in that file (column `Tier`)
is purely computational — loss-of-function or InterVar/ClinVar-flagged
variants are Tier 1, missense variants with strong in-silico support are
Tier 2, everything else is Tier 3.

**This file adds the step an automated pipeline cannot do on its own:
matching each candidate gene against the patient's actual phenotype**
(severe developmental delay, seizures, congenital heart disease, secondary/
postnatal microcephaly, absent speech, non-ambulatory, consanguinity — see
`../clinical/clinical_summary.md`). Genes were looked up against OMIM /
GeneReviews / recent peer-reviewed literature; sources are listed under each
entry and consolidated in **References** at the bottom.

None of this constitutes a diagnosis. It is a prioritized reading list for
the manual curation step that every real variant-filtering pipeline needs —
exactly the step this assignment is designed to teach.

---

## Tier A — strongest combined evidence

### 1. `SLC6A6` — chr3:14,444,330, splice-site deletion
`chr3:14,444,330 T>−` in the ANNOVAR input. The project annotation places
this variant at a canonical splice-site position in the *SLC6A6* transcript;
the exact HGVS intronic coordinate should be re-verified against the current
transcript before clinical reporting. The repository therefore avoids
presenting transcript-specific donor/acceptor numbering as definitive.

- **Gene–disease link:** *SLC6A6* encodes the taurine transporter (TauT).
  Biallelic loss-of-function variants cause an autosomal recessive disorder
  combining **retinal degeneration and cardiomyopathy** (HTRDC, OMIM
  #145350), first reported in a consanguineous Pakistani family and since
  reported in additional consanguineous families; taurine supplementation
  reversed the cardiomyopathy in treated patients (Ansar et al. 2020,
  *Hum Mol Genet*; European Journal of Human Genetics 2020 follow-up).
- **Phenotype match:** direct match to the **cardiac** component of this
  case, and the gene was specifically discovered in a **consanguineous**
  pedigree — mechanistically consistent with this family structure.
  Retinal degeneration is not mentioned in the clinical note, but a
  fundoscopic exam may simply not have been documented for a non-verbal
  patient.
- **Variant-level evidence:** disrupts a canonical splice donor site
  (mechanistically a strong loss-of-function candidate, comparable in
  severity to a stop-gain); catalogued in dbSNP (rs67559364); very low
  frequency where observed (HRC ~0.012%), absent from the other four
  panels in this (older) annotation.
- **Recommended follow-up:** echocardiogram findings if available,
  ophthalmologic exam, plasma/urine taurine level, and re-checking this
  exact variant in a current ClinVar/gnomAD lookup.

### 2. `SEPSECS` — chr4:25,161,949, c.C43T, p.Pro15Ser
`NM_016955:exon1:c.C43T:p.P15S`

- **Gene–disease link:** *SEPSECS* is the single most specific match in this
  candidate list. Biallelic *SEPSECS* variants cause **Pontocerebellar
  Hypoplasia type 2D** (PCH2D, OMIM #613811), described in OMIM as an
  autosomal recessive disorder with **progressive microcephaly**,
  **postnatal-onset** cerebral/cerebellar atrophy, **profound intellectual
  disability**, spasticity, and **variable seizures**. A 2022 case-series
  review (23 patients) reported microcephaly in 10/11 and intellectual
  disability in 10/11 of early-onset cases, and noted a late-onset subgroup
  with mean age at report of 21.8 ± 9.4 years — strikingly close to this
  proband's age of 20.
- **Phenotype match:** this is the only gene on the list that plausibly
  explains **secondary/postnatal microcephaly + severe DD + seizures**
  together as a single, well-described AR syndrome.
- **Variant-level evidence — the important caveat:** this specific
  substitution has **weak in-silico support** in this annotation
  (SIFT = tolerated, PolyPhen2 = benign, CADD = 11.66, well under common
  pathogenicity thresholds of ~20). It is absent from all five population
  databases (fully novel/private), which is consistent with — but not proof
  of — pathogenicity.
- **Recommended follow-up:** this is the textbook case for **not trusting
  in-silico scores alone**. Check cross-species conservation at this exact
  residue, check whether position 15 sits inside a mitochondrial-targeting
  or signal sequence (which some predictors handle poorly), consider
  whether the change could disrupt a nearby splice element despite being
  annotated as missense, and search HGMD/ClinVar/PubMed directly for
  "SEPSECS p.P15S" or "SEPSECS c.43C>T."

### 3. `CLN5` — chr13:77,566,340, c.C254T, p.Ala85Val
`NM_006493:exon1:c.C254T:p.A85V`

- **Gene–disease link:** *CLN5* biallelic variants cause a form of
  **neuronal ceroid lipofuscinosis** (CLN5 disease / late-infantile variant
  NCL, OMIM #256731), a progressive neurodegenerative lysosomal storage
  disorder. Case reports describe an initial period of comparatively normal
  function followed by **progressive loss of walking, speech, and cognitive
  function, together with seizures** — closely matching this proband's
  "severe developmental delay, seizures, no speech, no gait" description if
  interpreted as an acquired/regressive course rather than a static
  congenital picture. Notably, a 2020 case report describes a different
  homozygous *CLN5* missense variant that — like this one — was classified
  only as a **variant of uncertain significance** by automated ACMG
  criteria despite being the patient's molecular diagnosis, illustrating how
  common that outcome is for private NCL missense alleles.
- **Variant-level evidence:** absent from all five population databases
  (novel); mixed in-silico support (SIFT = tolerated, PolyPhen2(HDIV) =
  probably/possibly damaging, CADD = 24.2 — moderate-to-high).
- **What doesn't fit:** the cardiac finding is not a typical feature of
  CLN5 disease, and NCLs classically include progressive **visual failure**,
  which is not mentioned (again, possibly unassessed).
- **Recommended follow-up:** check for any documented visual/retinal
  findings, disease course/regression timeline from the family, and search
  ClinVar/HGMD for this exact substitution.

---

## Tier B — plausible, weaker support

### 4. `EXOSC5` — broader-pass candidate, chr19:41,892,573, c.C673T, p.Arg225Trp
- **Gene–disease link:** `EXOSC5` is a subunit of the RNA exosome complex.
  Other exosome subunits — *EXOSC3*, *EXOSC8*, *EXOSC9* — are established
  causes of **Pontocerebellar Hypoplasia type 1 (PCH1)**, which combines
  severe developmental delay, microcephaly, and spinal motor-neuron
  degeneration; functional work (zebrafish knockdown) shows *EXOSC5* loss
  also produces a small-head phenotype, and *EXOSC5* has been described in
  the literature as an emerging RNA-exosome disease gene, but with
  substantially less clinical case data behind it than *EXOSC3/8/9*.
- **Variant-level evidence:** strong in-silico support (SIFT = deleterious,
  PolyPhen2 = damaging, CADD = 35), but the variant is **not fully novel** —
  present at low frequency (~0.02–0.24% depending on the panel) with an
  existing dbSNP entry (rs35219501). These frequencies exceed the strict 0.1%
  threshold, so this candidate is retained only as a **broader-pass
  exploratory finding**, not as part of the final strict 51-variant set.
- **What doesn't fit well:** classic PCH1 (via EXOSC3/8/9) usually involves
  spinal motor-neuron degeneration and death in infancy; a 20-year survival
  is atypical for the classic presentation, though the phenotypic spectrum
  for exosome-related disease is still being defined.

### 5. `DNAH11` — chr7:21,646,271, c.C3772T, p.Gln1258Ter (stop-gain)
- **Gene–disease link:** *DNAH11* is an established, well-replicated cause
  of **Primary Ciliary Dyskinesia** (PCD / CILD7, autosomal recessive),
  characterized by chronic oto-sino-pulmonary disease and, in a meaningful
  subset of patients, **situs abnormalities and congenital heart disease**
  through disrupted left-right body-axis determination (heterotaxy is
  reported in roughly 12% of PCD cases in the literature).
- **Automated flag:** InterVar's automated ACMG classifier already calls
  this variant **"Likely pathogenic"** — a null (stop-gain) variant in an
  established recessive disease gene is a strong automatic signal (ACMG
  PVS1-type evidence).
- **What doesn't fit:** PCD does not cause developmental delay, seizures,
  or microcephaly. This variant may explain the cardiac component alone (if
  there is a laterality defect — situs inversus/dextrocardia), or it may be
  an unrelated incidental homozygous null variant. Both are common,
  realistic outcomes when filtering a consanguineous genome — not every
  homozygous LoF hit is the diagnosis.
- **Recommended follow-up:** check imaging specifically for situs
  inversus/dextrocardia, and check for a history of chronic respiratory or
  sinus disease.

---

## Deprioritized — cautionary examples, not dropped from the data

### `ZNF486` (stop-gain) and `ZNF626` (frameshift deletion) — broader-pass findings
These variants are retained only in the ≤1% exploratory set. Both sit in the **19p12 clustered zinc-finger gene region**, a segmentally
duplicated, difficult-to-map part of the genome that is well known for
generating false-positive or population-tolerated loss-of-function calls.
`ZNF486` in particular is **not private** — it carries a known dbSNP ID
(rs184976796) and is observed at ~0.3–0.6% across independent panels here,
i.e. a common polymorphism, not a private familial allele. Neither gene has
an established OMIM disease association matching this phenotype. **This
pair is a good in-class example of why "rare + LoF + homozygous" still
needs a plausibility check** — repetitive, paralogous genomic regions
generate exactly this kind of misleading hit.

### `NEK10` (stop-gain)
Essentially private (frequency ~6.5×10⁻⁶ in one panel, absent elsewhere),
which computationally looks compelling — but there is no established OMIM
disease association matching this phenotype in current literature.
Deprioritized for lack of phenotype fit, not for lack of rarity.

---

## Suggested one-line ranking (for a report or slide)

| Rank | Gene | Variant | Explains |
|---|---|---|---|
| 1 | *SEPSECS* | p.P15S (missense, weak in-silico) | DD + seizures + secondary microcephaly (best single-gene OMIM match) |
| 2 | *SLC6A6* | canonical splice donor | Cardiac disease (± unassessed retinal findings) |
| 3 | *CLN5* | p.A85V (missense) | DD + seizures + regression |
| 4 | *DNAH11* | p.Q1258X (stop-gain) | Cardiac disease only, if laterality defect confirmed |
| 5 | *NEK10* | p.R643X (stop-gain) | rare LoF candidate, but no matching established phenotype |

The current strict shortlist is therefore better treated as a set of candidates rather than a single molecular diagnosis. A genuinely satisfying answer may require **two genes** (one neuro, one
cardiac) rather than one — not unusual in a consanguineous pedigree, where
more than one region of the genome can be autozygous at once.

---

## References

1. Ben-Zeev B, et al. — OMIM #613811, Pontocerebellar Hypoplasia, Type 2D. https://omim.org/entry/613811
2. Agamy O, et al. (2010). *SEPSECS* and PCH2D. Summarized in OMIM #613811 and GeneReviews-style literature.
3. Case-series review of 23 PCH2D patients (early- vs. late-onset). PubMed: https://pubmed.ncbi.nlm.nih.gov/36085396/
4. "Case Report: A Relatively Mild Phenotype Produced by Novel Mutations in the SEPSECS Gene." https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8826681/
5. "CLN5, a novel gene... Finnish variant late infantile neuronal ceroid lipofuscinosis." PubMed: https://pubmed.ncbi.nlm.nih.gov/9662406/
6. "Functional Analysis of a Novel CLN5 Mutation..." https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7492598/
7. Eggens VRC, et al. EXOSC3 Pontocerebellar Hypoplasia — GeneReviews. https://www.ncbi.nlm.nih.gov/books/NBK236968/
8. "Homozygous EXOSC3... founder mutation..." (includes EXOSC5 zebrafish functional data). ResearchGate: https://www.researchgate.net/publication/251877433
9. Ansar M, et al. (2020). Biallelic *SLC6A6* variants, hypotaurinemic retinal degeneration and cardiomyopathy. *Hum Mol Genet.* https://academic.oup.com/hmg/article/29/4/618/5691205
10. Taurine treatment follow-up. *Eur J Hum Genet* (2020). https://www.nature.com/articles/s41431-020-0671-3
11. OMIM #186854 — *SLC6A6*. https://www.omim.org/entry/186854
12. Schultz R, et al. (2020). Two novel *DNAH11* mutations in PCD (CILD7). *BMC Med Genet.* https://bmcmedgenet.biomedcentral.com/articles/10.1186/s12881-020-01171-2
13. Carrier-frequency study noting heterotaxy/congenital heart disease in PCD. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4367086/

*(All entries above are paraphrased from the cited sources; consult the
original articles for exact wording, patient counts, and statistics before
citing them in your own submitted report.)*
