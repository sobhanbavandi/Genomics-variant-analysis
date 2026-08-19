# Genomics Variant Analysis — Consanguineous Case (SNPs/INDELs, ANNOVAR hg19)

**Author:** Sobhan Bavandi  
**Project type:** Bioinformatics coursework / research variant-prioritization project  

This repository documents a reproducible workflow for prioritizing candidate causal variants
from a single-sample ANNOVAR-annotated VCF (SNPs + indels, hg19), for a
patient from a consanguineous family with severe developmental delay,
seizures, congenital heart disease, secondary microcephaly, absent speech,
and absent gait. See `clinical/clinical_summary.md` for the full phenotype.

## Repository structure

```
genomics-variant-analysis/
├── README.md                      <- you are here
├── requirements.txt
├── clinical/
│   └── clinical_summary.md        <- phenotype, translated + structured
├── scripts/
│   └── filter_variants.py         <- the full, reproducible pipeline
├── results/
│   ├── candidates_homozygous_rare_coding.csv   <- 51 strict candidates (MAF ≤0.1%)
│   ├── candidates_homozygous_rare_coding_broad_1pct.csv <- 67 broader-pass candidates (MAF ≤1%)
│   └── prioritized_candidates.md               <- curated top picks + evidence
└── data/
    └── README.md                  <- where to put the raw xlsx to re-run
```

## Input data

`3-SNPs-INDELs_annovar_vcf_hg19_multianno.xlsx` — a `table_annovar.pl`
output (129 columns): RefSeq gene/functional annotation, cytoBand, ~25
in-silico deleteriousness predictors (SIFT, PolyPhen2, CADD, etc.),
population-frequency panels (1000 Genomes, ExAC, ESP6500, Kaviar, HRC),
ClinVar fields, an automated InterVar/ACMG classification, and the original
VCF fields (including the sample's genotype) appended at the end.
**This file is ~248 MB and is not included in this repository** — see
`data/README.md` and "Data & Privacy" below.

## Methodology

A standard rare-disease variant-filtering funnel, run over all 393,209
variant rows in one pass (`scripts/filter_variants.py`). The default rarity
threshold is **≤0.1% (0.001)**. A broader **≤1% exploratory pass** is retained
for comparison in `results/candidates_homozygous_rare_coding_broad_1pct.csv`.

| Step | Filter | Rationale | Rows remaining |
|---|---|---|---|
| 0 | — | Total SNPs + indels in the VCF | 393,209 |
| 1 | Standard chromosomes (1–22, X, Y, M) | Excludes unplaced/decoy contigs, which are unreliable for gene annotation | 385,780 |
| 2 | VCF `FILTER == PASS` | Removes low-confidence calls | 331,591 |
| 3 | Exonic or ANNOVAR-annotated splicing | A variant has to be able to alter coding sequence or a reported splice region | 22,460 |
| 4 | Not synonymous | Synonymous SNVs don't change the amino acid sequence | 10,716 |
| 5 | Rare/absent in 1000G, ExAC, ESP6500, Kaviar, HRC (≤0.1%) | Conservative rarity threshold; missing values are treated as absent in the legacy annotation | see run output |
| 6 | **Homozygous-ALT** in the proband | Consanguinity makes homozygous candidates a useful first-pass enrichment, but this does not exclude compound heterozygosity | **51** |

Step 6 is the case-specific step, explained in more depth (with its main
blind spot) under **Limitations** below.

The packaged strict output contains 51 survivors. The original 67-variant ≤1% exploratory set is retained separately for transparency. The step-by-step counts printed by the script are the authoritative counts for a fresh run against the original workbook. The strict survivors were then split into three transparent, *computational*
priority tiers (loss-of-function or already-flagged pathogenic; strong
in-silico missense; everything else), and separately reviewed **gene by
gene against the actual clinical phenotype** using OMIM/GeneReviews and
recent literature — see `results/prioritized_candidates.md` for the full,
cited discussion. In short:

- **`SEPSECS`** — the strongest single-gene phenotypic match (Pontocerebellar
  Hypoplasia type 2D: postnatal microcephaly + severe DD + seizures), but a
  variant with weak in-silico deleteriousness scores.
- **`SLC6A6`** — a canonical splice-site variant in the taurine-transporter
  gene, which causes an AR syndrome of cardiomyopathy + retinal
  degeneration, first described in a consanguineous family — best
  explanation for the cardiac finding.
- **`CLN5`** — a plausible match for the seizure/regression component
  (neuronal ceroid lipofuscinosis).
- **`DNAH11`** — an automatically "Likely pathogenic" stop-gain in a PCD
  gene; can explain congenital heart disease via a laterality defect, but
  not the neurodevelopmental features.
- **`EXOSC5`** — retained only in the broader exploratory set because its population frequency exceeds the strict ≤0.1% threshold.
- **`ZNF486` / `ZNF626`** — flagged and then *deprioritized*: they sit in a
  notoriously hard-to-map zinc-finger gene cluster and are not private
  variants — a useful cautionary example, kept in the results table rather
  than deleted.

## How to reproduce

```bash
pip install -r requirements.txt
python3 scripts/filter_variants.py /path/to/your_multianno.xlsx results/candidates_homozygous_rare_coding.csv
```

Runtime: this file is unusually large (a 1.8 GB uncompressed worksheet), so
the script streams it row-by-row rather than loading it into memory; expect
roughly 4–5 minutes on a single CPU core.

## Limitations

- **Single-sample analysis.** No parental sequencing was available, so
  phasing was not possible. Homozygosity is a strong signal in a
  consanguineous pedigree but **cannot rule out compound heterozygosity**
  (two different rare variants, one per parental allele, in the same gene).
  Re-running the "rare" heterozygous variants and grouping by gene is a
  reasonable next step if trio data ever becomes available.
- **Non-coding and deep-intronic variants were not evaluated.** The filter
  is restricted to exonic/splice-site regions; a causal regulatory or deep
  intronic variant would be missed entirely.
- **The bundled frequency/ClinVar databases are an older ANNOVAR snapshot**
  (1000 Genomes 2015, no gnomAD, ClinVar as of the annotation date). Before
  finalizing any candidate, re-check its current population frequency
  (gnomAD) and current ClinVar classification directly.
- **Automated ACMG/InterVar calls are not a diagnosis.** "Likely
  pathogenic" from an automated tool (as for `DNAH11` here) still needs
  human review of segregation and phenotype fit; conversely, "Uncertain
  significance" (as for `SEPSECS` and `CLN5` here) does not rule a variant
  out, especially for private, novel changes in strong candidate genes.

## Data & Privacy

This repository is built for a coursework exercise, but the underlying
files describe a real clinical presentation and (in the original xlsx) raw
genomic coordinates and a lab sample ID. Before making this repository
**public** on GitHub:

- Confirm with your instructor whether patient-level genomic/clinical data
  may be shared publicly at all, even de-identified.
- If in doubt, keep the repository **private** and only share it with the
  instructor/grader (GitHub supports private repos and adding a
  collaborator by username/email).
- Do **not** commit the original 248 MB `.xlsx` file (see `data/README.md`)
  — it is excluded via `.gitignore`, and GitHub rejects files over 100 MB
  by default in any case.

## References

See the fully cited discussion in `results/prioritized_candidates.md`.
