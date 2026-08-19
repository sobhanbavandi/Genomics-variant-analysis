# Clinical Summary

**Privacy note:** This is a de-identified teaching case (no name, no exact
date/location of birth). No identifying information beyond a laboratory
sample code is included anywhere in this repository. See the "Data
Privacy" section of the main README before making this repository public.

## Original clinical note (Persian, as provided)

 خانواده با ازدواج خویشاوند (پدر مبتلا، پسرعموی مادربزرگ می باشد و
 مادربزرگ و پدربزرگ ها نیز ازدواج خویشاوندی داشتند) دارای یک فرزند پسر
 مبتلا بدون سابقه خانوادگی با تظاهرات بالینی تاخیر تکاملی شدید، تشنج،
 بیماری قلبی، میکروسفالی ثانویه، عدم تکلم و راه رفتن میباشند. مبتلا در
 زمان معاینه ۲۰ ساله دارای دور سر ۴۷ سانتیمتر (SD ۵.۴۵-)، قد ۱۳۴
 سانتیمتر (SD ۵.۹۲-) و وزن ۵۰ کیلوگرم (SD ۲.۲۵-) و در بدو تولد دور سر
 ۳۵ سانتیمتر (SD ۰.۴۰-) بود. این خانواده دارای یک پسر و دختر سالم نیز
 هستند.

## English translation

The family reports consanguinity across multiple generations (the father is
related to the paternal grandmother's family; the grandparents were also
consanguineous). They have one affected son, with no other family history of
the same condition, presenting with severe developmental delay, seizures,
heart disease, secondary (postnatal) microcephaly, absence of speech, and
inability to walk. At the time of examination the proband was 20 years old,
with a head circumference of 47 cm (SD -5.45), height of 134 cm (SD -5.92),
and weight of 50 kg (SD -2.25). Head circumference at birth was 35 cm
(SD -0.40) — essentially within normal range. The family also has one
unaffected son and one unaffected daughter.

## Structured phenotype summary

| Feature | Detail |
|---|---|
| Proband | Male, age 20 at examination |
| Family history | Consanguineous pedigree (multi-generational); only child affected; 1 unaffected brother, 1 unaffected sister |
| Suspected inheritance | Autosomal recessive (favored strongly by the consanguinity + single-affected-child pattern) |
| Developmental delay | Severe, global |
| Seizures | Present |
| Cardiac | Congenital/structural heart disease (no further detail provided in the note) |
| Head circumference | Birth: 35 cm (SD -0.40, ~normal) &rarr; Age 20: 47 cm (SD -5.45) &mdash; **postnatal/secondary microcephaly**, i.e. growth deceleration after a normal start |
| Height | 134 cm (SD -5.92) &mdash; severe short stature |
| Weight | 50 kg (SD -2.25) |
| Speech | Absent (non-verbal) |
| Gait | Absent (non-ambulatory) |

## Candidate HPO-style terms

For an assignment that expects Human Phenotype Ontology (HPO) terms, start
from these and confirm the exact codes at [hpo.jax.org](https://hpo.jax.org/)
(codes are not reproduced here to avoid citing a possibly outdated ID):

- Global developmental delay
- Seizure
- Congenital heart defect
- Postnatal microcephaly / progressive microcephaly
- Absent speech
- Gait disturbance / inability to walk
- Short stature
- Consanguineous parents

## Why this phenotype matters for variant filtering

Two details in this note directly shape the bioinformatics strategy used in
this repository:

1. **Multi-generation consanguinity + a single affected child + no other
   family history** is the classic signature of an **autosomal recessive**
   condition transmitted through a shared ancestral haplotype. This justifies
   prioritizing **homozygous** genotypes in the proband (see
   `scripts/filter_variants.py`).
2. **"Secondary" / postnatal microcephaly** (normal at birth, well below
   average by adulthood) is a specific, informative sign — it points toward
   a *progressive/neurodegenerative* process rather than a purely congenital
   brain malformation, and it is explicitly described as a feature of
   several genes discussed in `results/prioritized_candidates.md`.
