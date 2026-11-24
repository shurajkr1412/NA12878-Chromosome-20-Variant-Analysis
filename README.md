# NA12878 Chromosome 20 Variant Analysis

**Galaxy-based variant calling and transcript-aware interpretation of a selected SNV in NA12878**

> **Scope:** This is an educational case study of **one selected chromosome 20 variant**, not a complete chromosome-wide interpretation or a clinical diagnostic report.

## Project overview

This project follows the GRCh38/hg38 variant **chr20:1,118,382 A>G** (`rs73071626`) from its genotype in a Galaxy-processed VCF through SnpEff consequence annotation and cross-checks using gnomAD, Ensembl, dbSNP and ClinVar.

The main question is why SnpEff labels the variant `HIGH` and whether that label implies disruption of the protein-coding gene **PSMF1**.

## Key result

The variant was called **heterozygous** in NA12878 (`GT=0/1`; `DP=12`; `AD=3,9`; `GQ=65`). SnpEff's **HIGH** consequence is `splice_donor_variant&intron_variant` in **LOC105372493 / NR_136535.1**, which is marked as a **pseudogene** transcript in the VCF annotation. Two **PSMF1** protein-coding transcripts in the same record were annotated as **intronic (MODIFIER)**, not splice-donor variants.

Three additional splice-donor-associated Ensembl transcripts checked during the investigation were all classified as **lncRNA**. These use different transcript identifiers from the RefSeq pseudogene transcript, so direct transcript equivalence has **not** been established.

**Interpretation:** A `HIGH` consequence label in this record **does not by itself establish PSMF1 protein dysfunction or clinical pathogenicity**. The variant's functional significance remains undetermined.

## Variant summary

| Field | Observed result |
| --- | --- |
| Sample | NA12878 |
| Reference | GRCh38 / hg38 |
| Variant | `chr20:1118382 A>G` |
| dbSNP | [`rs73071626`](https://www.ncbi.nlm.nih.gov/snp/rs73071626) |
| Genotype | `0/1` (heterozygous) |
| Allelic depth | `3,9` (reference A, alternate G) |
| Depth | `12` |
| Genotype quality | `65` |
| Variant QUAL | `298.64` |
| Mapping quality (INFO/MQ) | `60` |
| FILTER | `.` (not an explicit `PASS`) |
| SnpEff HIGH transcript | `NR_136535.1` (`LOC105372493`, pseudogene) |
| SnpEff PSMF1 effects | Intronic on `NM_178578.3`, `NM_001323407.2` |
| gnomAD allele frequency | ~`0.003978` (as viewed during analysis) |
| gnomAD SpliceAI | `0.00` (as viewed during analysis) |
| ClinVar | Exact-variant search returned no match during the analysis; **not** a benign classification |

**Note:** VCF `INFO/AF=0.5` is the frequency calculated in this single-sample callset and **not** the population frequency reported by gnomAD.

## Methods at a glance

1. Review chromosome 20 NA12878 alignment and variant-calling output in Galaxy.
2. Confirm VCF provenance from its header: **GATK HaplotypeCaller 4.6.2.0**, **bcftools 1.24**, and **SnpEff 5.4c** with `hg38`.
3. Use `bcftools view` to retrieve the exact SnpEff-annotated site.
4. Inspect the genotype fields, INFO metrics and transcript-by-transcript `ANN` entries.
5. Compare variant identity and predicted transcript consequences using public databases and an IGV read visualization.

The available VCF header documents these tool versions, but this repository does **not** claim to reconstruct every upstream processing and quality-control step. For detail, see [METHODS.md](METHODS.md).

## Repository contents

```text
NA12878-Chromosome-20-Variant-Analysis/
├── README.md
├── METHODS.md
├── results/
│   ├── variant_summary.tsv
│   ├── transcript_effects.tsv
│   └── selected_variant_vcf_excerpt.txt
├── figures/
│   └── README.md
└── report/
    └── NA12878_Chr20_Variant_Analysis_Report.docx
```

The `figures/` folder currently contains instructions only. Add screenshots from your actual analysis with clear captions; no figures have been fabricated for this repository.

## Limitations

- A single selected variant is examined; no chromosome-wide pathogenicity analysis is claimed.
- Sample depth is modest (`DP=12`), with 3 reference and 9 alternate-supporting reads.
- The VCF `FILTER` field contains `.` rather than an explicit `PASS`.
- Annotation resources use different transcript sets/versions; cross-database transcript identity was not proven.
- A negative exact ClinVar search is not evidence of benignity, and no functional splice assay was performed.
- Population and prediction values reflect the database pages examined during the analysis and may differ in later releases.

## References

- [Galaxy](https://usegalaxy.eu/)
- [GATK HaplotypeCaller](https://gatk.broadinstitute.org/hc/en-us/articles/54698694431131-HaplotypeCaller)
- [bcftools manual](https://samtools.github.io/bcftools/bcftools-man.html)
- [SnpEff annotation format](https://pcingola.github.io/SnpEff/snpeff/inputoutput/)
- [gnomAD variant page](https://gnomad.broadinstitute.org/variant/20-1118382-A-G?dataset=gnomad_r4)
- [dbSNP rs73071626](https://www.ncbi.nlm.nih.gov/snp/rs73071626)
- [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/)
- [Ensembl ENST00000664648](https://www.ensembl.org/feature-explorer/GCA_000001405.29/transcript:ENST00000664648)
- [Ensembl ENST00000620712](https://www.ensembl.org/feature-explorer/GCA_000001405.29/transcript:ENST00000620712)
- [Ensembl ENST00000692211](https://www.ensembl.org/feature-explorer/GCA_000001405.29/transcript:ENST00000692211)

## Data and use

NA12878 is a widely used reference sample; this repository includes only a **small, user-reviewed VCF excerpt and summary tables**, not FASTQ/BAM/CRAM data or a full VCF. Check provenance, dataset terms, and privacy before making any sequencing data public.

*Educational/research documentation only. Not for clinical diagnosis.*
