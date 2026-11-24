# Methods

## Scope

Single-variant case study in NA12878: GRCh38 **chr20:1,118,382 A>G**. This document summarizes steps supported by the examined Galaxy VCF header and analysis notes; undocumented upstream quality-control and preprocessing steps are not assumed.

## Genome reference and variant calling

- Reference genome: **GRCh38 / hg38**.
- Variant-calling tool recorded in the VCF header: **GATK HaplotypeCaller 4.6.2.0**.
- SNP selection recorded in the header: **bcftools 1.24** (`view --types snps`).
- Consequence annotation recorded in the header: **SnpEff 5.4c** using the `hg38` database.
- Sample reported by the VCF: **NA12878**.

## Target variant review

The annotated VCF was examined for the exact site `chr20:1118382`. The VCF fields CHROM, POS, REF, ALT, QUAL, FILTER, INFO, FORMAT and NA12878 were reviewed. The `ANN` entries were parsed separately for transcript ID, gene, biotype, effect and impact. The allele balance was computed from genotype `AD=3,9` (9/12 = 75% alternate among genotype-supporting reads).

## Database cross-references

- **dbSNP:** checked the variant identity `rs73071626` and GRCh38 coordinate.
- **gnomAD:** examined population frequency, variant consequences and in-silico splicing predictions.
- **Ensembl:** checked biotypes for three ENST transcripts implicated by the displayed splice-donor annotations.
- **ClinVar:** an exact-variant search at the time of analysis returned no matching entry.
- **IGV:** read visualization had been reviewed; no orthogonal laboratory verification or splice assay was performed.

## Interpretation rules

SnpEff impact categories are **predicted consequences**, not clinical classifications. The VCF's pseudogene splice-donor annotation and PSMF1's protein-coding intronic annotations are reported separately. The ENST lncRNA IDs are not assumed to be identical to the RefSeq pseudogene `NR_136535.1`.

## Reproducibility caveat

The repository documents the observed annotated site and VCF header provenance. It does **not** contain complete input alignments, reference files, Galaxy workflow export or all tool parameters required for exact reproduction.
