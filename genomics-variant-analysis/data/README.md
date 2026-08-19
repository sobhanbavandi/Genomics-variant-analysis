# data/

Place the original ANNOVAR multianno file here to re-run the pipeline:

    data/3-SNPs-INDELs_annovar_vcf_hg19_multianno.xlsx

This file is intentionally **not** committed to the repository:

- It is ~248 MB — over GitHub's 100 MB per-file limit (would need Git LFS).
- It contains patient-level genomic data; see "Data & Privacy" in the main README.

Then run the default strict filter (MAF ≤0.1%):

    python3 scripts/filter_variants.py data/3-SNPs-INDELs_annovar_vcf_hg19_multianno.xlsx

For the broader exploratory ≤1% pass used during initial review:

    python3 scripts/filter_variants.py data/3-SNPs-INDELs_annovar_vcf_hg19_multianno.xlsx results/candidates_homozygous_rare_coding_broad_1pct.csv --maf-threshold 0.01
