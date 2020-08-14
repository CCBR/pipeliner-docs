## Inputs
### Initial input files
These files are generated during the `Initialize Directory` and are linked from the rawdata directory.

```
<WorkingDirectory>
│
│
├── Control_1_miRNA_S1.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/mirseq/fastq/Control_1_miRNA_S1.R1.fastq.gz
├── Control_2_miRNA_S2.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/mirseq/fastq/Control_2_miRNA_S2.R1.fastq.gz
├── ...
├── ...
├── TreatmentB_3_miRNA_S11.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/mirseq/fastq/TreatmentB_3_miRNA_S11.R1.fastq.gz
├── TreatmentB_4_miRNA_S12.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/mirseq/fastq/TreatmentB_4_miRNA_S12.R1.fastq.gz
```

### Input tab files 
These are the tab-delimited files created by the user to indicate groups and contrasts

```
<WorkingDirectory>
│
│
├── groups.tab
├── contrasts.tab
```

## Quality Control

### Pre-trim FastQC
These files are available in the `rawQC` directory and are produced by the first round of FastQC, performed on the reads before adapter trimming.

```
<WorkingDirectory>
│
│
├── rawQC
│   ├── Control_1_miRNA_S1.R1_fastqc.html
│   ├── Control_1_miRNA_S1.R1_fastqc.zip
│   ├── Control_2_miRNA_S2.R1_fastqc.html
│   ├── Control_2_miRNA_S2.R1_fastqc.zip
│   ├── ...
│   ├── TreatmentB_3_miRNA_S11.R1_fastqc.html
│   ├── TreatmentB_3_miRNA_S11.R1_fastqc.zip
│   ├── TreatmentB_4_miRNA_S12.R1_fastqc.html
│   └── TreatmentB_4_miRNA_S12.R1_fastqc.zip
├── ...
```

### Adapter trimmed reads
These files are produced by Cutadapt by trimming the adapter sequences from the read sequences.

```
<WorkingDirectory>
│
│
├── trim
│   ├── Control_1_miRNA_S1.R1.trim.fastq.gz
│   ├── Control_2_miRNA_S2.R1.trim.fastq.gz
│   ├── ...
│   ├── TreatmentB_3_miRNA_S11.R1.trim.fastq.gz
│   └── TreatmentB_4_miRNA_S12.R1.trim.fastq.gz
├── ...
```

### Kraken
Kraken is a tool for evaluating the degree of contamination in the individual samples and produces html reports for each sample.

```
<WorkingDirectory>
│
│
├── kraken
│   ├── Control_1_miRNA_S1.trim.fastq.kraken_bacteria.krona.html
│   ├── Control_1_miRNA_S1.trim.fastq.kraken_bacteria.taxa.txt
│   ├── Control_2_miRNA_S2.trim.fastq.kraken_bacteria.krona.html
│   ├── Control_2_miRNA_S2.trim.fastq.kraken_bacteria.taxa.txt
│   ├── ...
│   ├── TreatmentB_4_miRNA_S12.trim.fastq.kraken_bacteria.krona.html
│   └── TreatmentB_4_miRNA_S12.trim.fastq.kraken_bacteria.taxa.txt
├── ...
```

### Post-trim FastQC
FastQC is also performed after adapter trimming to evaluate the quality of the reads without appended adapter sequences. It also includes two files containing the read length statistics. These results are available in the QC directory.

```
<WorkingDirectory>
│
│
├── QC
│   ├── Control_1_miRNA_S1.R1.trim_fastqc.html
│   ├── Control_1_miRNA_S1.R1.trim_fastqc.zip
│   ├── Control_2_miRNA_S2.R1.trim_fastqc.html
│   ├── ...
│   ├── readlength.err
│   ├── readlength.txt
│   ├── ...
│   ├── TreatmentB_3_miRNA_S11.R1.trim_fastqc.html
│   ├── TreatmentB_3_miRNA_S11.R1.trim_fastqc.zip
│   ├── TreatmentB_4_miRNA_S12.R1.trim_fastqc.html
│   └── TreatmentB_4_miRNA_S12.R1.trim_fastqc.zip
├── ...
```
### FastQ Screen
FastQ Screen is run twice, with different configuration files. The results for the first run are stored in the `FQscreen` directory and perform a preliminary mapping to identify likely species from which the reads were obtained. The second run is stored in the `FQscreen2` directory and aligns the reads to ribosomal and UniVec sequences.

```
<WorkingDirectory>
│
│
├── FQscreen
│   ├── Control_1_miRNA_S1.R1.trim_screen.html
│   ├── Control_1_miRNA_S1.R1.trim_screen.png
│   ├── Control_1_miRNA_S1.R1.trim_screen.txt
│   ├── Control_2_miRNA_S2.R1.trim_screen.html
│   ├── Control_2_miRNA_S2.R1.trim_screen.png
│   ├── Control_2_miRNA_S2.R1.trim_screen.txt
│   ├── ...
│   ├── TreatmentB_4_miRNA_S12.R1.trim_screen.html
│   ├── TreatmentB_4_miRNA_S12.R1.trim_screen.png
│   └── TreatmentB_4_miRNA_S12.R1.trim_screen.txt
├── FQscreen2
│   ├── Control_1_miRNA_S1.R1.trim_screen.html
│   ├── Control_1_miRNA_S1.R1.trim_screen.png
│   ├── Control_1_miRNA_S1.R1.trim_screen.txt
│   ├── ...
│   ├── TreatmentB_4_miRNA_S12.R1.trim_screen.html
│   ├── TreatmentB_4_miRNA_S12.R1.trim_screen.png
│   └── TreatmentB_4_miRNA_S12.R1.trim_screen.txt
├── ...
```

### MultiQC Report
The MultiQC report, which compiles all the results of the different QC programs into a single html report, is in the Reports directory.

```
<WorkingDirectory>
│
│
├── Reports
│   ├── ...
│   ├── multiqc_data
│   │   ├── multiqc_data.json
│   │   ├── multiqc_fastqc.txt
│   │   ├── multiqc_fastq_screen.txt
│   │   ├── multiqc_general_stats.txt
│   │   ├── multiqc.log
│   │   └── multiqc_sources.txt
│   ├── multiqc_report.html
│   ├── ...
│   └── ...
├── ...

```
 
## miRDeep2 Outputs

### Preliminary FASTA conversion
miRDeep2 operates on FASTA files, while the trimmed data is in FASTQ format. The files are converted to FASTA format using the FASTX-toolkit and compressed for storage [after they are utilized](#mirdeep2-mapper). The conversion is logged for the Snakemake program using file flags.

```
<WorkingDirectory>
│
│
├── fasta
│   ├── ...
│   ├── Control_1_miRNA_S1.trimfasta.done
│   ├── Control_2_miRNA_S2.trimfasta.done
│   ├── ...
│   ├── TreatmentB_3_miRNA_S11.trimfasta.done
│   ├── TreatmentB_4_miRNA_S12.trimfasta.done
│   └── ...
├── ...
```

### miRDeep2 Mapper
miRDeep2 performs a preliminary mapping prior to alignment to create a single collapsed FASTA file containing all the reads. This requires the creation of said FASTA file and a mapping config file containing sample abbreviations.  It then performs alignment with Bowtie 1 to the reference genome and the output is stored as `trimmed.arf` in the working directory. Since the raw FASTA files are no longer necessary, they are compressed into a `.tar.gz` file.

```
<WorkingDirectory>
│
│
├── ...
├── fasta
│   ├── collapsed_trim.fa
│   ├── ...
│   └── trim.tar.gz
├── ...
├── mirdeep_config.txt
├── ...
└── trimmed.arf
```

### miRDeep2: Annotated Reads Only
If the user has opted to <u>not</u> identify novel microRNAs, the collapsed FASTA file is aligned with Bowtie against the annotated precursor and mature microRNA sequences from miRBase, and the results are stored in a counts file in the directory `mirdeep2_out`. The final results, with the assigned sample names, are stored in `mirdeep2_results/annotated_counts.txt`.

```
<WorkingDirectory>
│
│
├── mirdeep2_out
│   ├── expression_<stamp>.html
│   ├── expression_analyses
│   │   └── expression_analyses_<stamp>
│   │       ├── bowtie_mature.out
│   │       ├── bowtie_reads.out
│   │       ├── collapsed_trim.fa.converted
│   │       ├── collapsed_trim.fa_mapped.arf
│   │       ├── collapsed_trim.fa_mapped.bwt
│   │       ├── expression_1594075822.html
│   │       ├── mature2hairpin
│   │       ├── mature.converted
│   │       ├── mature.fa_mapped.arf
│   │       ├── mature.fa_mapped.bwt
│   │       ├── miRBase.mrd
│   │       ├── miRNA_expressed.csv
│   │       ├── miRNA_not_expressed.csv
│   │       ├── miRNA_precursor.1.ebwt
│   │       ├── miRNA_precursor.2.ebwt
│   │       ├── miRNA_precursor.3.ebwt
│   │       ├── miRNA_precursor.4.ebwt
│   │       ├── miRNA_precursor.rev.1.ebwt
│   │       ├── miRNA_precursor.rev.2.ebwt
│   │       ├── precursor.converted
│   │       ├── read_occ
│   │       └── rna.ps
│   └── miRNAs_expressed_all_samples.txt
├── mirdeep2_results
│   └── annotated_counts.txt
├── ...
```

### miRDeep2: Novel miRNA Alignment
If the user has opted to have miRDeep2 identify novel miRNAs, several additional outputs are generated, including 
* Novel hairpin and mature FASTA references, which are stored in the `fasta` directory
* Alignments to the annotated miRBase reference in `mirdeep2_1p`
* Alignments to the novel reference sequences in `mirdeep2_2p`
* Counts for annotated and novel reference sequences in `mirdeep2_results`


```
<WorkingDirectory>
│
│
├── fasta
│   ├── collapsed_trim.fa
│   ├── ...
│   ├── novel_hairpin.fa
│   ├── novel_mature.fa
│   ├── ...
│   ├── TreatmentB_3_miRNA_S11.trimfasta.done
│   ├── TreatmentB_4_miRNA_S12.trimfasta.done
│   └── trim.tar.gz
├── mirdeep2_1p
│   ├── dir_prepare_signature1594151705
│   │   ├── mature_vs_precursors.arf
│   │   ├── mature_vs_precursors.bwt
│   │   ├── precursors.ebwt.1.ebwt
│   │   ├── precursors.ebwt.2.ebwt
│   │   ├── ...
│   │   ├── signature_unsorted.arf.tmp
│   │   └── signature_unsorted.arf.tmp2
│   ├── error_07_07_2020_t_15_43_26.log
│   ├── expression_07_07_2020_t_15_43_26.html
│   ├── expression_analyses
│   │   └── expression_analyses_07_07_2020_t_15_43_26
│   │       ├── bowtie_mature.out
│   │       ├── bowtie_reads.out
│   │       ├── collapsed_trim.fa.converted
│   │       ├── collapsed_trim.fa_mapped.arf
│   │       ├── ...
│   │       └── rna.ps
│   ├── mirna_results_07_07_2020_t_15_43_26
│   │   ├── known_mature_07_07_2020_t_15_43_26_score-50_to_na.bed
│   │   ├── known_mature_07_07_2020_t_15_43_26_score-50_to_na.fa
│   │   ├── ...
│   │   ├── novel_star_07_07_2020_t_15_43_26_score-50_to_na.bed
│   │   └── novel_star_07_07_2020_t_15_43_26_score-50_to_na.fa
│   ├── miRNAs_expressed_all_samples_1p.txt
│   ├── pdfs_07_07_2020_t_15_43_26
│   │   ├── chr10_23178.pdf
│   │   ├── chr10_23253.pdf
│   │   ├── ...
│   │   └── chrY_45431.pdf
│   ├── result_07_07_2020_t_15_43_26.bed
│   ├── result_07_07_2020_t_15_43_26.csv
│   └── result_07_07_2020_t_15_43_26.html
├── mirdeep2_2p
│   ├── expression_1594185150.html
│   ├── expression_analyses
│   │   └── expression_analyses_1594185150
│   │       ├── bowtie_mature.out
│   │       ├── bowtie_reads.out
│   │       ├── collapsed_trim.fa.converted
│   │       ├── collapsed_trim.fa_mapped.arf
│   │       ├── ...
│   │       ├── novel_mature.fa_mapped.bwt
│   │       ├── precursor.converted
│   │       ├── read_occ
│   │       └── rna.ps
│   ├── novel_miRNAs_expressed_all_samples_2p.txt
│   └── pdfs_1594185150
│       ├── chr10_23178.pdf
│       ├── chr10_23253.pdf
│       ├── ...
├── ...
├── mirdeep2_results
│   ├── annotatedCounts.txt
│   └── novelCounts.txt
```

## Differential expression
Coming soon!

## Miscellaneous outputs from the Pipeliner Snakemake
Many of these files are produced by Pipeliner in order to run the pipeline to completion or as background outputs.

```
<WorkingDirectory>
|
|
├── cluster.json
├── HPC_usage_table.txt
├── pairs
├── pipeline_ctrl.sh
├── Reports
│   └── ...
├── run.json
├── samples
├── Scripts
│   └── ...
├── slurmfiles
│   └── ...
├── Snakefile
└── submit_slurm.sh
```
