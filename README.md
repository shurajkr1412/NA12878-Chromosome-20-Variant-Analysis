# NA12878 Chromosome 20 Variant Analysis

**A Galaxy-Based Bioinformatics Research Project | Germline Variant Calling, Functional Annotation and Transcript-Aware Interpretation**

## Project Overview

This project documents my hands-on bioinformatics analysis of publicly available whole-genome sequencing (WGS) data from the **NA12878 (HG001) reference individual**.

The analysis focuses on a selected region of chromosome 20 using the human reference genome GRCh38/hg38. It explores how genomic variants are identified, filtered, annotated and interpreted using commonly used next-generation sequencing (NGS) bioinformatics tools.

The main case study investigates a single-nucleotide variant (SNV), **chr20:1118382 A>G (rs73071626)**, and examines why an automated HIGH-impact annotation does not necessarily establish a damaging effect on a protein-coding gene.

This project demonstrates practical experience with sequencing data analysis, genomic databases, variant interpretation and reproducible scientific documentation.

> **Project scope:** This is an educational, single-variant research case study. It is not a complete chromosome-wide pathogenicity analysis or a clinical diagnostic report.

---

## Research Objectives

The objectives of this project were to:

1. Explore the processing and analysis of publicly available human whole-genome sequencing data.
2. Review sequence quality control, read alignment and BAM processing using Galaxy.
3. Examine germline variant calling using GATK HaplotypeCaller.
4. Investigate variant filtering and data extraction using bcftools and SnpSift.
5. Identify predicted functional consequences using SnpEff.
6. Examine population allele frequencies using gnomAD.
7. Investigate transcript biotypes and genomic annotations using Ensembl.
8. Review read-level evidence using the Integrative Genomics Viewer (IGV).
9. Document findings, limitations and biological interpretation in a research report.

---

## Tools and Technologies

| Tool / Database | Application |
|---|---|
| Galaxy Europe | Web-based bioinformatics analysis platform |
| FastQC | Sequencing quality assessment |
| BWA-MEM | Short-read alignment |
| SAMtools | BAM processing and alignment statistics |
| GATK HaplotypeCaller | Germline variant calling |
| bcftools | Variant filtering, querying and extraction |
| SnpSift | Variant filtering and annotation field extraction |
| SnpEff | Functional consequence annotation |
| IGV | Visualization of aligned sequencing reads |
| gnomAD | Population allele frequency and annotation |
| Ensembl | Transcript structure and biotype analysis |
| dbSNP | Variant identification and genomic cross-referencing |
| ClinVar | Investigation of clinical variant records |

**Reference genome:** GRCh38/hg38

**Sample:** NA12878 (HG001)

---

## Bioinformatics Workflow

The analysis followed the general NGS processing and variant interpretation workflow:

1. Public NA12878 paired-end sequencing reads
2. Sequence quality assessment using FastQC
3. Read alignment using BWA-MEM
4. BAM sorting, processing and duplicate marking
5. Read-group assignment and alignment statistics
6. Germline variant calling using GATK HaplotypeCaller
7. Variant selection and filtering using bcftools and SnpSift
8. Functional annotation using SnpEff
9. Selection and examination of chr20:1118382 A>G
10. Population and transcript-level interpretation using gnomAD and Ensembl
11. Read visualization using IGV
12. Scientific documentation and reporting

The annotated VCF header documents **GATK HaplotypeCaller 4.6.2.0, bcftools 1.24 and SnpEff 5.4c**.

The repository preserves the selected variant and supporting results rather than all intermediate files and parameters. Therefore, it should not be interpreted as a fully executable reconstruction of the complete upstream workflow.

For additional technical details, see [METHODS.md](METHODS.md).

---

## Selected Variant

The detailed investigation focused on the following single-nucleotide variant:

| Parameter | Result |
|---|---|
| Sample | NA12878 |
| Genome assembly | GRCh38 / hg38 |
| Chromosome | chr20 |
| Position | 1,118,382 |
| Reference allele | A |
| Alternate allele | G |
| dbSNP identifier | rs73071626 |
| Genotype | 0/1 (heterozygous) |
| Read depth (DP) | 12 |
| Allelic depth (AD) | 3,9 |
| Genotype quality (GQ) | 65 |
| Variant quality (QUAL) | 298.64 |
| Mapping quality (INFO/MQ) | 60 |
| VCF FILTER | . (not explicitly PASS) |

The genotype indicates that NA12878 is heterozygous at the selected position.

The allele depths indicate three reads supporting the reference allele (A) and nine reads supporting the alternate allele (G).

The alternate allele represents 75% of the genotype-supporting reads at this position. Given the modest depth, this imbalance should be interpreted cautiously.

The VCF INFO allele frequency of 0.5 is derived from the single-sample callset and should not be confused with population allele frequency.

---

## Functional Annotation Using SnpEff

SnpEff was used to investigate the predicted functional consequences of the selected variant.

The annotated VCF contained the following transcript-level consequences:

| Gene | Transcript | Transcript type | Consequence | Impact |
|---|---|---|---|---|
| LOC105372493 | NR_136535.1 | Pseudogene | splice_donor_variant & intron_variant | HIGH |
| PSMF1 | NM_178578.3 | Protein-coding | intron_variant | MODIFIER |
| PSMF1 | NM_001323407.2 | Protein-coding | intron_variant | MODIFIER |

### Key Observation

**The HIGH-impact annotation was assigned to the pseudogene transcript NR_136535.1, not to the two protein-coding PSMF1 transcripts represented in the same VCF record.**

The protein-coding PSMF1 transcripts were annotated as intronic variants.

This finding illustrates why automated variant impact classifications should be interpreted at the transcript level rather than relying on the overall severity label alone.

Importantly, a predicted HIGH-impact annotation is not equivalent to a clinical pathogenic classification.

---

## Population Frequency Analysis Using gnomAD

The variant was examined using gnomAD v4.1.2 to investigate its distribution in population sequencing datasets.

| Parameter | Observed value |
|---|---|
| Overall allele frequency | 0.003978 |
| Total allele count | 746 |
| Total allele number | 187,520 |
| Number of homozygotes | 6 |
| SpliceAI score | 0.00 |

The reported overall allele frequency corresponds to approximately 0.3978%.

gnomAD also displayed a warning that the variant was covered in fewer than 50% of individuals in the exome dataset, indicating that some frequency estimates may be less reliable.

The reported SpliceAI score of 0.00 does not provide computational support for a splice-altering effect according to that predictor.

These findings were considered alongside the transcript annotations rather than being used independently to classify the variant as benign or pathogenic.

---

## Ensembl Transcript Investigation

To investigate the splice-donor annotations, three Ensembl transcripts were examined.

| Transcript | Biotype | Associated gene |
|---|---|---|
| ENST00000664648.2 | lncRNA | ENSG00000286787.4 |
| ENST00000620712.4 | lncRNA | ENSG00000286787.4 |
| ENST00000692211.2 | lncRNA | ENSG00000286787.4 |

All three transcripts were classified as **long non-coding RNA (lncRNA)**.

Ensembl describes their associated gene as a novel transcript antisense to PSMF1.

This observation emphasizes the importance of distinguishing non-protein-coding transcript consequences from effects on protein-coding genes.

The Ensembl transcript identifiers differ from the RefSeq pseudogene transcript identifier reported by SnpEff. Direct equivalence between these annotations was not established during this analysis.

---

## IGV Read-Level Visualization

The selected variant was examined using IGV with the NA12878 alignment data.

The visualization showed sequencing reads aligned across chr20:1118382 and reads supporting the alternate G allele.

Inspection of an individual supporting read showed:

| Parameter | Value |
|---|---|
| Genomic position | chr20:1118382 |
| Observed read base | G |
| Base quality | 35 |
| Mapping quality | 60 |
| Duplicate flag | No |

The IGV inspection provided additional read-level evidence for the alternate allele identified in the VCF.

However, visualization alone does not constitute independent experimental validation of the variant.

---

## Research Interpretation

The central finding of this project is that **a predicted HIGH-impact variant annotation does not automatically imply loss of protein function or clinical pathogenicity**.

In this case:

- SnpEff identified a HIGH-impact splice-donor consequence in a pseudogene transcript.
- The examined protein-coding PSMF1 transcripts received intronic annotations.
- Three additional Ensembl transcripts associated with splice-donor annotations were classified as lncRNAs.
- SpliceAI did not predict a splice-altering effect.
- gnomAD showed that the alternate allele occurs in population sequencing data.

Taken together, the findings support a cautious, transcript-aware interpretation of the selected variant.

**The available evidence does not establish that chr20:1118382 A>G disrupts PSMF1 protein function or causes disease.**

The biological and clinical significance of the variant remains undetermined.

---

## Repository Structure

```text
NA12878-Chromosome-20-Variant-Analysis/
│
├── README.md
├── METHODS.md
├── .gitignore
│
├── results/
│   ├── README.md
│   ├── variant_summary.tsv
│   ├── transcript_effects.tsv
│   └── selected_variant_vcf_excerpt.txt
│
├── figures/
│   ├── README.md
│   ├── figure1_galaxy_history.png
│   ├── figure2_selected_vcf_row.png
│   ├── figure3_gnomad_variant.png
│   ├── figure4a_ensembl_ENST00000664648.2.png
│   ├── figure4b_ensembl_ENST00000620712.4.png
│   ├── figure4c_ensembl_ENST00000692211.2.png
│   └── figure5_igv_locus.png
│
└── report/
    ├── README.md
    └── NA12878_Chr20_Research_Portfolio_Report.pdf
```

---

## Supporting Figures

The following screenshots were captured during the actual investigation and uploaded to document the analysis.

### Figure 1 — Galaxy Analysis History

[View Galaxy Analysis History](figures/figure1_galaxy_history.png)

Shows the Galaxy environment and history of key analysis steps, including GATK HaplotypeCaller, bcftools, SnpSift and SnpEff.

### Figure 2 — Selected Variant VCF Record

[View Selected Variant](figures/figure2_selected_vcf_row.png)

Shows the selected VCF record at chr20:1118382, extracted from the SnpEff-annotated dataset using bcftools.

### Figure 3 — gnomAD Population Frequency

[View gnomAD Evidence](figures/figure3_gnomad_variant.png)

Documents the selected variant's population frequency and allele counts in gnomAD.

### Figure 4 — Ensembl Transcript Biotypes

The three screenshots document Ensembl transcript classifications:

- [ENST00000664648.2](figures/figure4a_ensembl_ENST00000664648.2.png)
- [ENST00000620712.4](figures/figure4b_ensembl_ENST00000620712.4.png)
- [ENST00000692211.2](figures/figure4c_ensembl_ENST00000692211.2.png)

These images support the transcript biotype comparison discussed in the interpretation.

### Figure 5 — IGV Locus Visualization

[View IGV Read Alignment](figures/figure5_igv_locus.png)

Shows read-level visualization of the selected chromosome 20 variant.

---

## Research Report and Supporting Files

The complete research report provides a detailed explanation of the methodology, selected variant, predicted functional consequences, population evidence, transcript comparison, limitations and conclusions.

**[Read the Full Research Report (PDF)](report/NA12878_Chr20_Research_Portfolio_Report.pdf)**

Additional project resources:

- [Detailed Methodology](METHODS.md)
- [Variant Summary](results/variant_summary.tsv)
- [Transcript Effects](results/transcript_effects.tsv)
- [Selected VCF Record](results/selected_variant_vcf_excerpt.txt)
- [Supporting Figures](figures/)

---

## Limitations

This project has several important limitations:

1. The detailed biological interpretation concerns one selected variant rather than all variants on chromosome 20.
2. The selected variant has modest read depth (DP = 12).
3. The VCF FILTER field contains a missing value (`.`) rather than an explicit PASS designation.
4. Transcript databases and annotation tools use different transcript sets and releases.
5. Predicted functional consequences do not independently establish pathogenicity.
6. gnomAD reported a low exome coverage warning for the selected variant.
7. The ClinVar exact-variant search reviewed during the investigation did not identify a matching entry; this is not evidence that the variant is benign.
8. No functional RNA-splicing assay or independent laboratory confirmation was performed.
9. The repository does not contain the complete raw datasets or all workflow configuration files necessary for exact computational reproduction.

These limitations are important when interpreting the findings and evaluating their biological relevance.

---

## Skills Demonstrated

Through this project, I gained practical experience in:

- NGS data analysis and bioinformatics workflow interpretation
- Human reference genome and genomic coordinate handling
- Sequencing quality control and alignment review
- BAM/VCF file interpretation
- Germline variant calling with GATK
- Variant selection, filtering and querying
- Functional annotation using SnpEff
- Transcript-aware genomic interpretation
- Population variant database investigation
- IGV read-level visualization
- Scientific reporting and research documentation
- GitHub-based organization and presentation of bioinformatics results

This project forms part of my bioinformatics portfolio and reflects my interest in genomic data analysis, computational biology and research-oriented problem solving.

---

## References and Resources

1. [Galaxy Europe](https://usegalaxy.eu/)
2. [GATK HaplotypeCaller](https://gatk.broadinstitute.org/hc/en-us/articles/54698694431131-HaplotypeCaller)
3. [SAMtools and bcftools](https://www.htslib.org/)
4. [SnpEff](https://pcingola.github.io/SnpEff/)
5. [gnomAD Browser](https://gnomad.broadinstitute.org/variant/20-1118382-A-G?dataset=gnomad_r4)
6. [Ensembl Genome Browser](https://www.ensembl.org/)
7. [dbSNP — rs73071626](https://www.ncbi.nlm.nih.gov/snp/rs73071626)
8. [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/)
9. [Integrative Genomics Viewer](https://igv.org/)

---

## Data Availability and Responsible Use

This project uses publicly available NA12878 reference sequencing data for educational and research purposes.

The repository contains a selected, reviewed VCF excerpt, summary tables, analysis screenshots and the scientific report. Complete FASTQ, BAM and other large sequencing datasets are not included.

The documentation is intended to demonstrate analytical methods and research interpretation rather than provide clinical findings.

**Disclaimer:** This project is intended for educational and research portfolio purposes only. It must not be used for medical diagnosis or clinical decision-making.
