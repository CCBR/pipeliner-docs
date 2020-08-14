## Phase 1 of the ChIP-seq pipeline
Successful completion of Phase 1 of the ChIPseq tutorial demo data will create the following file/folder structure:

### Rawdata files

Symlinks to the raw fastq files:

```bash
<working_dir>
│ 
│ 
├── CTCF_ChIP_macrophage_p20_1.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/chipseq//SRR3081748_1.fastq.gz
├── CTCF_ChIP_macrophage_p20_2.R1.fastq.gz -> /data/CCBR_Pipeliner/testdata/chipseq//SRR3081749_1.fastq.gz
├── ...
├── ...
```

### Sequencing quality and contamination assessments:

#### FastQC

`rawfastqc` and `fastqc` folders contains sequencing quality assessment results using [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) for raw and preprocess fastq files. Each file has a *.zip* archive and a *.html* report. These results are also summarized across samples in the *multiqc_report.html* file.

```bash
<working_dir>
│ 
│
├── rawfastQC
│   ├── CTCF_ChIP_macrophage_p20_1.R1_fastqc.html
│   ├── CTCF_ChIP_macrophage_p20_1.R1_fastqc.zip
│   ├── ...
│   ├── ...
├── fastQC
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_fastqc.html
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_fastqc.zip
│   ├── ...
│   ├── ...
```

#### FastQScreen

1 million reads from each sample are screened against the following database using [Fastqscreen](https://www.bioinformatics.babraham.ac.uk/projects/fastq_screen/):

* Human
* Mouse
* Bacteria
* Fungi
* Viruses
* [UniVec](https://www.ncbi.nlm.nih.gov/tools/vecscreen/univec/)
* Ribosomal sequences

The results are saved in the `FQscreen` and `FQscreen2` folders. You can expect 6 files per sample as shown the example below:

```bash
<working_dir>
│ 
│ 
├── FQscreen
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.html
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.png
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.txt
│   ├── ...
│   ├── ...
├── FQscreen2
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.html
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.png
│   ├── CTCF_ChIP_macrophage_p20_1.R1.trim_screen.txt
│   ├── ...
│   ├── ...
```

#### Kraken/Krona

[Kraken](https://ccb.jhu.edu/software/kraken/) provides a k-mer based approach which assigns each read to a bacterial reference in an "all known bacterial species" database. These are reported in the `*.taxa.txt` files per sample. These assignments can then be interactively visualized in a html file using [Krona](https://github.com/marbl/Krona/wiki).

```bash
<working_dir>
│ 
│ 
├── kraken
│   ├── CTCF_ChIP_macrophage_p20_1.trim.fastq.kraken_bacteria.krona.html
│   ├── CTCF_ChIP_macrophage_p20_1.trim.fastq.kraken_bacteria.taxa.txt
│   ├── ...
│   ├── ...
```

### ChIP quality and replicate concordance assessments

#### Deeptools outputs

deeptools` folder has the following set of files for each group (a group includes all replicates for that group including input samples):

* [fingerprint](https://deeptools.readthedocs.io/en/develop/content/tools/plotFingerprint.html?highlight=fingerprint#background) plot related files:
  * `fingerprint.metrics.Q5DD.tsv`: fingerprint plot stats
  * `fingerprint.Q5DD.pdf`: fingerprint plot with Q5DD data
  * `fingerprint.sorted.pdf`: fingerprint plot with unfiltered data
* [heatmap and profile](https://deeptools.readthedocs.io/en/develop/content/tools/plotHeatmap.html) plots focused on various genomic loci:
  * *metagene*: all genes in the genome normalized by gene length
  * *prot.metagene*: same as above but focused on protein-coding genes only
  * *TSS*: around transcription start sites of all genes
  * *prot.TSS*: same as above but focused on protein-coding genes only

```bash
<working_dir>
│ 
│ 
├── deeptools
│   ├── Macrophage_p20.fingerprint.metrics.Q5DD.tsv
│   ├── Macrophage_p20.fingerprint.Q5DD.pdf
│   ├── Macrophage_p20.fingerprint.sorted.pdf
│   ├── Macrophage_p20.metagene_heatmap.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.metagene_heatmap.sorted.RPGC.pdf
│   ├── Macrophage_p20.metagene_profile.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.metagene_profile.sorted.RPGC.pdf
│   ├── Macrophage_p20.prot.metagene_heatmap.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.prot.metagene_heatmap.sorted.RPGC.pdf
│   ├── Macrophage_p20.prot.metagene_profile.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.prot.metagene_profile.sorted.RPGC.pdf
│   ├── Macrophage_p20.prot.TSS_heatmap.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.prot.TSS_heatmap.sorted.RPGC.pdf
│   ├── Macrophage_p20.prot.TSS_profile.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.prot.TSS_profile.sorted.RPGC.pdf
│   ├── Macrophage_p20.TSS_heatmap.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.TSS_heatmap.sorted.RPGC.pdf
│   ├── Macrophage_p20.TSS_profile.Q5DD.RPGC.pdf
│   ├── Macrophage_p20.TSS_profile.sorted.RPGC.pdf
│   ├── ...
│   ├── ...
```

`deeptools` folder `sorted_fingerprint` subfolder with fingerprint stats for unfiltered bam files.

```bash
<working_dir>
│ 
│ 
├── deeptools
│   ├── sorted_fingerprint
│   │   ├── Macrophage_p20.fingerprint.metrics.sorted.tsv
│   │   ├── Macrophage_p3.fingerprint.metrics.sorted.tsv
│   │   └── MEF_p20.fingerprint.metrics.sorted.tsv
```

`deeptools` folder contains principle component analysis plots with all samples.

```bash
<working_dir>
│ 
│ 
├── deeptools
│   ├── pca.Q5DD.RPGC.pdf
│   ├── pca.sorted.RPGC.pdf
```

`deeptools` folder also contain spearman correlation plots (heatmaps and scatterplots) with all samples

```bash
<working_dir>
│ 
│ 
├── deeptools
│   ├── spearman_heatmap.Q5DD.RPGC_mqc.png
│   ├── spearman_heatmap.Q5DD.RPGC.pdf
│   ├── spearman_heatmap.sorted.RPGC.pdf
│   ├── spearman_scatterplot.Q5DD.RPGC.pdf
│   └── spearman_scatterplot.sorted.RPGC.pdf
```

#### ChIP-seq relevant QC

`QC` folder contains more ChIP-seq relevant qc metrics. For eg. 

* Preseq is used to assess library complexity. 
* NGSQC is used to compare ChIP quality between replicates/samples. These results are also summarized per group.

*QCTable.txt* neatly aggregrates all the QC metrics into a single tab-delimited file which can be easily read into Microsoft Excel.

```bash
<working_dir>
│ 
│
├── QC
│   ├── CTCF_ChIP_macrophage_p20_1.ccurve
│   ├── CTCF_ChIP_macrophage_p20_1.preseq.dat
│   ├── CTCF_ChIP_macrophage_p20_1.preseq.log
│   ├── ...
│   ├── ...
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.NGSQC_report.txt
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.NGSQC.txt
│   ├── ...
│   ├── ...
│   ├── Macrophage_p20.NGSQC.Q5DD.png
│   ├── ...
│   ├── ...
│   └── QCTable.txt
```

#### Multiqc report

Along with some other housekeeping files the `Reports` folder contains the `multiqc_report.html` which graphically aggregates all QC assestments into one report.

```bash
<working_dir>
│ 
│
├── Reports
│   ├── ...
│   ├── ...
│   ├── multiqc_data
│   │   ├── multiqc_bcbio_metrics.txt
│   │   ├── multiqc_chip-specific_qc_metrics.txt
│   │   ├── multiqc_data.json
│   │   ├── multiqc_fastqc.txt
│   │   ├── multiqc_fastq_screen.txt
│   │   ├── multiqc_general_stats.txt
│   │   ├── multiqc.log
│   │   ├── multiqc_samtools_flagstat.txt
│   │   ├── multiqc_samtools_idxstats.txt
│   │   ├── multiqc_sources.txt
│   │   ├── seqbuster_isomirs.txt
│   │   └── seqbuster_mirs.txt
│   ├── multiqc_report.html
│   ├── ...
│   ├── ...
```

### Alignment and Visualization files:

#### Bams

`bam` folder has following files for each sample:

 * `.bam`: binary version of the alignment file. There are 3 versions of alignment files:
   * `sorted.bam`: all alignments sorted by coordinates
   * `Q5.bam`: sorted alignments filtered to exclude alignments with MAPQ<5
   * `Q5DD.bam`: deduplicated version of the `Q5.bam` file
 * Each of the `.bam` files may also have the following secondary files:
   * `.bai`: index for the `.bam` file
   * `.flagstat`: file containing the alignment statistics
   * `.idxstat`: file containing number of reads aligning per chromosome
   * `.ppqt`: cross-correlation statistics
   * `.pdf`: cross-correlation plots
     * `.tagAlign.gz`: alignments in bed format for downstream peak calling by MACS2

```bash
<working_dir>
│ 
│ 
├── bam
│   ├── CTCF_ChIP_macrophage_p20_1.Q5.bam.bai
│   ├── CTCF_ChIP_macrophage_p20_1.Q5.bam.flagstat
│   ├── CTCF_ChIP_macrophage_p20_1.Q5.bam.idxstat
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.bam
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.bam.bai
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.bam.flagstat
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.bam.idxstat
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.pdf
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.ppqt
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.tagAlign.gz
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.bam
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.bam.bai
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.bam.flagstat
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.bam.idxstat
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.pdf
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.ppqt
│   ├── ...
│   ├── ...
```

#### Bigwigs

`.bigwig` folder contains alignments in [bigwig](https://genome.ucsc.edu/goldenpath/help/bigWig.html) format which is smaller than bam format and easy for quick visualizations using genome browsers like [IGV](https://software.broadinstitute.org/software/igv/). Each sample has 3 bigwig files:

* `.sorted.RPGC.bw`: created by normalizing the corresponding `.sorted.bam` file to 1X genome coverage
* `.Q5DD.RPGC.bw`: created by normalizing the corresponding `.Q5DD.bam` file to 1X genome coverage
* `.Q5DD.RPGC.inputnorm.bw`: created by subtracting the normalized input bigwig file from the normalized ChIP bigwig

```bash
<working_dir>
│ 
│ 
├── bigwig
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.RPGC.bw
│   ├── CTCF_ChIP_macrophage_p20_1.Q5DD.RPGC.inputnorm.bw
│   ├── CTCF_ChIP_macrophage_p20_1.sorted.RPGC.bw
│   ├── ...
│   ├── ...
```

### Other important files

Some of the other important files in the `working_dir` are:

* `cluster.json`: outlines the resources requested for each *Snakemake* rule
* `Snakefile`: contains all the *Snakemake* rules
* `HPC_usage_table.txt`: tabular report of how each *Snakemake* rule utilized the HPC cluster with details
* `run.json`: json file saving all GUI selections
* `peakcall.tab`: tab-delimited file defining which samples are ChIP and what are their corresponding input samples

```bash

<working_dir>
│ 
│ 
├── cluster.json
├── Snakefile
├── HPC_usage_table.txt
├── run.json
├── peakcall.tab
├── ...
├── ...
```

All other folder and files in the `working_dir` are for housekeeping and are required for successful execution of the CCBR_Pipeliner.

## Phase 2 of the ChIP-seq pipeline

Successful completion of Phase 2 of the ChIPseq tutorial demo data will create the following file/folder structure in addition to the files created in Phase 1:

### Peak calls:

#### GEM

`gem` folder has a subfolder for each sample, which should contain the files ending with `GEM_events.narrowPeak` which represent the peak calls from [GEM](https://www.encodeproject.org/software/gem/) in [narrowPeak](https://genome.ucsc.edu/FAQ/FAQformat.html#format12) format.

```bash
<working_dir>
│ 
│ 
├── gem
│   ├── CTCF_ChIP_macrophage_p20_1
│   │   ├── CTCF_ChIP_macrophage_p20_1.GEM_events.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p20_1.GEM_events.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1.GPS_events.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p20_1.GPS_events.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_outputs
│   │   │   ├── ...
│   │   │   ├── ...
│   ├── CTCF_ChIP_macrophage_p20_2
│   ├── ...
│   ├── ...
```

#### MACS2 for broad peaks

`macs2Broad` folder has a subfolder for each sample, which should contain the files ending with `.broadPeak` which represent the peak calls from [macs2](https://github.com/macs3-project/MACS) in [broadPeak](https://genome.ucsc.edu/FAQ/FAQformat.html#format13) format. The peaks are also available in Excel format.

```bash
<working_dir>
│ 
│ 
├── macsBroad
│   ├── CTCF_ChIP_macrophage_p20_1
│   │   ├── CTCF_ChIP_macrophage_p20_1_peaks.broadPeak
│   │   ├── CTCF_ChIP_macrophage_p20_1_peaks.gappedPeak
│   │   └── CTCF_ChIP_macrophage_p20_1_peaks.xls
│   ├── CTCF_ChIP_macrophage_p20_2
│   │   ├── CTCF_ChIP_macrophage_p20_2_peaks.broadPeak
│   │   ├── CTCF_ChIP_macrophage_p20_2_peaks.gappedPeak
│   │   └── CTCF_ChIP_macrophage_p20_2_peaks.xls
│   ├── CTCF_ChIP_macrophage_p3_1
│   │   ├── CTCF_ChIP_macrophage_p3_1_peaks.broadPeak
│   │   ├── CTCF_ChIP_macrophage_p3_1_peaks.gappedPeak
│   │   └── CTCF_ChIP_macrophage_p3_1_peaks.xls
│   ├── CTCF_ChIP_macrophage_p3_2
│   │   ├── CTCF_ChIP_macrophage_p3_2_peaks.broadPeak
│   │   ├── CTCF_ChIP_macrophage_p3_2_peaks.gappedPeak
│   │   └── CTCF_ChIP_macrophage_p3_2_peaks.xls
│   ├── CTCF_ChIP_MEF_p20_1
│   │   ├── CTCF_ChIP_MEF_p20_1_peaks.broadPeak
│   │   ├── CTCF_ChIP_MEF_p20_1_peaks.gappedPeak
│   │   └── CTCF_ChIP_MEF_p20_1_peaks.xls
│   └── CTCF_ChIP_MEF_p20_2
│       ├── CTCF_ChIP_MEF_p20_2_peaks.broadPeak
│       ├── CTCF_ChIP_MEF_p20_2_peaks.gappedPeak
│       └── CTCF_ChIP_MEF_p20_2_peaks.xls
```

#### MACS2 for narrow peaks

`macs2Narrow` folder has a subfolder for each sample, which should contain the files ending with `.narrowPeak` which represent the peak calls from [macs2](https://github.com/macs3-project/MACS) in [narrowPeak](https://genome.ucsc.edu/FAQ/FAQformat.html#format12) format. The peaks are also available in Excel format, along with peak summits in [bed](https://genome.ucsc.edu/FAQ/FAQformat.html#format1) format.

```bash
<working_dir>
│ 
│ 
├── macsNarrow
│   ├── CTCF_ChIP_macrophage_p20_1
│   │   ├── CTCF_ChIP_macrophage_p20_1_peaks.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p20_1_peaks.xls
│   │   └── CTCF_ChIP_macrophage_p20_1_summits.bed
│   ├── CTCF_ChIP_macrophage_p20_2
│   │   ├── CTCF_ChIP_macrophage_p20_2_peaks.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p20_2_peaks.xls
│   │   └── CTCF_ChIP_macrophage_p20_2_summits.bed
│   ├── CTCF_ChIP_macrophage_p3_1
│   │   ├── CTCF_ChIP_macrophage_p3_1_peaks.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p3_1_peaks.xls
│   │   └── CTCF_ChIP_macrophage_p3_1_summits.bed
│   ├── CTCF_ChIP_macrophage_p3_2
│   │   ├── CTCF_ChIP_macrophage_p3_2_peaks.narrowPeak
│   │   ├── CTCF_ChIP_macrophage_p3_2_peaks.xls
│   │   └── CTCF_ChIP_macrophage_p3_2_summits.bed
│   ├── CTCF_ChIP_MEF_p20_1
│   │   ├── CTCF_ChIP_MEF_p20_1_peaks.narrowPeak
│   │   ├── CTCF_ChIP_MEF_p20_1_peaks.xls
│   │   └── CTCF_ChIP_MEF_p20_1_summits.bed
│   └── CTCF_ChIP_MEF_p20_2
│       ├── CTCF_ChIP_MEF_p20_2_peaks.narrowPeak
│       ├── CTCF_ChIP_MEF_p20_2_peaks.xls
│       └── CTCF_ChIP_MEF_p20_2_summits.bed
```

#### Sicer

`sicer` folder has a subfolder for each sample which contains the peakcalls from [sicer](https://zanglab.github.io/SICER2/) in [bed](https://genome.ucsc.edu/FAQ/FAQformat.html#format1), [broadPeak](https://genome.ucsc.edu/FAQ/FAQformat.html#format13) and tabular formats.

```bash
├── sicer
│   ├── CTCF_ChIP_macrophage_p20_1
│   │   ├── CTCF_ChIP_macrophage_p20_1_broadpeaks.bed
│   │   ├── CTCF_ChIP_macrophage_p20_1_broadpeaks.txt
│   │   └── CTCF_ChIP_macrophage_p20_1_sicer.broadPeak
│   ├── CTCF_ChIP_macrophage_p20_2
│   │   ├── CTCF_ChIP_macrophage_p20_2_broadpeaks.bed
│   │   ├── CTCF_ChIP_macrophage_p20_2_broadpeaks.txt
│   │   └── CTCF_ChIP_macrophage_p20_2_sicer.broadPeak
│   ├── CTCF_ChIP_macrophage_p3_1
│   │   ├── CTCF_ChIP_macrophage_p3_1_broadpeaks.bed
│   │   ├── CTCF_ChIP_macrophage_p3_1_broadpeaks.txt
│   │   └── CTCF_ChIP_macrophage_p3_1_sicer.broadPeak
│   ├── CTCF_ChIP_macrophage_p3_2
│   │   ├── CTCF_ChIP_macrophage_p3_2_broadpeaks.bed
│   │   ├── CTCF_ChIP_macrophage_p3_2_broadpeaks.txt
│   │   └── CTCF_ChIP_macrophage_p3_2_sicer.broadPeak
│   ├── CTCF_ChIP_MEF_p20_1
│   │   ├── CTCF_ChIP_MEF_p20_1_broadpeaks.bed
│   │   ├── CTCF_ChIP_MEF_p20_1_broadpeaks.txt
│   │   └── CTCF_ChIP_MEF_p20_1_sicer.broadPeak
│   └── CTCF_ChIP_MEF_p20_2
│       ├── CTCF_ChIP_MEF_p20_2_broadpeaks.bed
│       ├── CTCF_ChIP_MEF_p20_2_broadpeaks.txt
│       └── CTCF_ChIP_MEF_p20_2_sicer.broadPeak
```

### Peaks-based QC

#### FRiP/Jaccard

[FRiP](https://www.encodeproject.org/data-standards/terms/) and [jaccard](https://bedtools.readthedocs.io/en/latest/content/tools/jaccard.html) barplots/scatterplots/table are saved in the `PeakQC` folder for each of the peak callers:

* gem
* macs
  * broad
  * narrow
* sicer

```bash
<working_dir>
│ 
│ 
├── PeakQC
│   ├── gem.FRiP_barplot.png
│   ├── gem.FRiP_scatterplot.png
│   ├── gem.FRiP_table.txt
│   ├── gem.jaccard_heatmap.pdf
│   ├── gem.jaccard_PCA.pdf
│   ├── gem_jaccard.txt
│   ├── macsBroad.FRiP_barplot.png
│   ├── macsBroad.FRiP_scatterplot.png
│   ├── macsBroad.FRiP_table.txt
│   ├── macsBroad.jaccard_heatmap.pdf
│   ├── macsBroad.jaccard_PCA.pdf
│   ├── macsBroad_jaccard.txt
│   ├── macsNarrow.FRiP_barplot.png
│   ├── macsNarrow.FRiP_scatterplot.png
│   ├── macsNarrow.FRiP_table.txt
│   ├── macsNarrow.jaccard_heatmap.pdf
│   ├── macsNarrow.jaccard_PCA.pdf
│   ├── macsNarrow_jaccard.txt
│   ├── sicer.FRiP_barplot.png
│   ├── sicer.FRiP_scatterplot.png
│   ├── sicer.FRiP_table.txt
│   ├── sicer.jaccard_heatmap.pdf
│   ├── sicer.jaccard_PCA.pdf
│   └── sicer_jaccard.txt
```

The above files allow you to make inter-sample comparison for a peak caller at a time. If you want to compare accross peak caller then you can you the following files in `PeakQC` folder.

```bash
<working_dir>
│ 
│ 
├── PeakQC
│   ├── jaccard_heatmap.pdf
│   ├── jaccard_PCA.pdf
│   └── jaccard.txt
```

#### Replicate concordance with IDR

`IDR` folder contains the outputs generated by comparing replicates peaks using [idr](https://www.encodeproject.org/software/idr/) for the following peak callers:

* sicer
* macs2
  * broad
  * narrow

Please note that IDR is not run for GEM.

```bash
<working_dir>
│ 
│ 
├── IDR
│   ├── macsBroad
│   │   ├── Macrophage_p20
│   │   │   ├── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt
│   │   │   └── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt.png
│   │   ├── Macrophage_p3
│   │   │   ├── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt
│   │   │   └── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt.png
│   │   └── MEF_p20
│   │       ├── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt
│   │       └── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt.png
│   ├── macsNarrow
│   │   ├── Macrophage_p20
│   │   │   ├── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt
│   │   │   └── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt.png
│   │   ├── Macrophage_p3
│   │   │   ├── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt
│   │   │   └── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt.png
│   │   └── MEF_p20
│   │       ├── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt
│   │       └── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt.png
│   └── sicer
│       ├── Macrophage_p20
│       │   ├── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt
│       │   └── CTCF_ChIP_macrophage_p20_1_vs_CTCF_ChIP_macrophage_p20_2.idrValue.txt.png
│       ├── Macrophage_p3
│       │   ├── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt
│       │   └── CTCF_ChIP_macrophage_p3_1_vs_CTCF_ChIP_macrophage_p3_2.idrValue.txt.png
│       └── MEF_p20
│           ├── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt
│           └── CTCF_ChIP_MEF_p20_1_vs_CTCF_ChIP_MEF_p20_2.idrValue.txt.png
```

#### MultiQC Report

Along with some other housekeeping files the `Reports` folder contains the `multiqc_report.html` which graphically aggregates all peak based QC assestments into one report. Also, the mulitqc report previously generated for the *initialQC* (phase1) of the pipeline is now located in the `multiqc_initialQC` subfolder as showed below: 

```bash
<working_dir>
│ 
│ 
├── Reports
│   ├── multiqc_data
│   │   ├── multiqc_bcbio_metrics.txt
│   │   ├── multiqc_chip-specific_qc_metrics.txt
│   │   ├── multiqc_data.json
│   │   ├── multiqc_fastqc.txt
│   │   ├── multiqc_fastq_screen.txt
│   │   ├── multiqc_general_stats.txt
│   │   ├── multiqc.log
│   │   ├── multiqc_samtools_flagstat.txt
│   │   ├── multiqc_samtools_idxstats.txt
│   │   ├── multiqc_sources.txt
│   │   ├── seqbuster_isomirs.txt
│   │   └── seqbuster_mirs.txt
│   ├── multiqc_initialQC
│   │   ├── multiqc_data
│   │   │   ├── multiqc_bcbio_metrics.txt
│   │   │   ├── multiqc_chip-specific_qc_metrics.txt
│   │   │   ├── multiqc_data.json
│   │   │   ├── multiqc_fastqc.txt
│   │   │   ├── multiqc_fastq_screen.txt
│   │   │   ├── multiqc_general_stats.txt
│   │   │   ├── multiqc.log
│   │   │   ├── multiqc_samtools_flagstat.txt
│   │   │   ├── multiqc_samtools_idxstats.txt
│   │   │   ├── multiqc_sources.txt
│   │   │   ├── seqbuster_isomirs.txt
│   │   │   └── seqbuster_mirs.txt
│   │   └── multiqc_report.html
│   ├── multiqc_report.html
```

### Peak annotations with UROPA

[UROPA](https://github.molgen.mpg.de/pages/loosolab/www/software/Uropa/) annotations are provided while prioritizing the following genomic features:

* all genes
* protein-coding genes
* transcription start sites of all genes
* transcription start sites of protein-coding genes

Files are saved for all four peak callers (gem/macs2Narrow/macs2Broad/sicer) in individual subfolders for all called peaks. Similarly the DiffBind results are also annotated with UROPA in the `DiffBind` folder if any contrasts are provided at the time of running phase2 of the pipeline.

```bash
<working_dir>
│ 
│ 
├── UROPA_annotations
│   ├── gem
│   │   ├── CTCF_ChIP_macrophage_p20_1.gem.genes.json
│   │   ├── CTCF_ChIP_macrophage_p20_1.gem.prot.json
│   │   ├── CTCF_ChIP_macrophage_p20_1.gem.TSSgenes.json
│   │   ├── CTCF_ChIP_macrophage_p20_1.gem.TSSprot.json
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_genes_allhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_genes_finalhits.bed
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_genes_finalhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_genes_summary.pdf
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_prot_allhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_prot_finalhits.bed
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_prot_finalhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_prot_summary.pdf
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSgenes_allhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSgenes_finalhits.bed
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSgenes_finalhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSgenes_summary.pdf
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSprot_allhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSprot_finalhits.bed
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSprot_finalhits.txt
│   │   ├── CTCF_ChIP_macrophage_p20_1_gem_uropa_TSSprot_summary.pdf
│   │   ├── ...
│   │   ├── ...
│   ├── macsNarrow
│   ├── macsBroad
│   ├── sicer
│   ├── DiffBind
```

### Motif analysis with HOMER

*de novo* and known motif enrichment is performed using [HOMER](http://homer.ucsd.edu/homer/) with the entire genome as background. The `HOMER_motifs` folder contains a subfolder for all four peak callers (gem/macsBroad/macsNarrow/sicer). Each of these subfolders further contain a subfolder per sample peak call as shown below:

```bash
<working_dir>
│ 
│ 
├── HOMER_motifs
│   ├── macsBroad
│   │   ├── CTCF_ChIP_macrophage_p20_1_macsBroad_GW
│   │   │   ├── homerMotifs.all.motifs
│   │   │   ├── homerMotifs.motifs10
│   │   │   ├── homerMotifs.motifs12
│   │   │   ├── homerMotifs.motifs8
│   │   │   ├── homerResults
│   │   │   ├── ...
│   │   │   ├── ...
│   │   │   ├── homerResults.html
│   │   │   ├── knownResults
│   │   │   ├── knownResults.html
│   │   │   ├── knownResults.txt
│   │   │   │   ├── ...
│   │   │   │   ├── ...
│   │   ├── CTCF_ChIP_macrophage_p20_2_macsBroad_GW
│   │   ├── CTCF_ChIP_macrophage_p3_1_macsBroad_GW   
│   │   ├── CTCF_ChIP_macrophage_p3_2_macsBroad_GW
│   │   ├── ...
│   │   ├── ...
│   ├── macsNarrow
│   │   ├── CTCF_ChIP_macrophage_p20_1_macsNarrow_GW
│   │   ├── CTCF_ChIP_macrophage_p20_2_macsNarrow_GW
│   │   ├── CTCF_ChIP_macrophage_p3_1_macsNarrow_GW   
│   │   ├── CTCF_ChIP_macrophage_p3_2_macsNarrow_GW
│   │   ├── ...
│   │   ├── ...
│   ├── sicer
│   │   ├── CTCF_ChIP_macrophage_p20_1_sicer_GW
│   │   ├── CTCF_ChIP_macrophage_p20_2_sicer_GW
│   │   ├── CTCF_ChIP_macrophage_p3_1_sicer_GW   
│   │   ├── CTCF_ChIP_macrophage_p3_2_sicer_GW
│   │   ├── ...
│   │   ├── ...
```

### DiffBind results (Optional)

[DiffBind](https://www.bioconductor.org/packages/release/bioc/html/DiffBind.html) is run for all contrast provided in the `contrast.tab` file using:

* DESeq2
* EdgeR

Each contrasts' results are saved in a separate subfolder along with a combined html report as shown below:

```bash
<working_dir>
│ 
│ 
├── DiffBind
│   ├── Macrophage_p3_vs_Macrophage_p20-gem
│   │   ├── DiffBind_pipeliner.Rmd
│   │   ├── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind_Deseq2.bed
│   │   ├── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind_Deseq2.txt
│   │   ├── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind_EdgeR.bed
│   │   ├── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind_EdgeR.txt
│   │   ├── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind.html
│   │   └── Macrophage_p3_vs_Macrophage_p20-gem_Diffbind_prep.csv
│   ├── Macrophage_p3_vs_Macrophage_p20-macsNarrow
│   │   ├── ...
│   │   ├── ...
│   ├── Macrophage_p3_vs_Macrophage_p20-macsBroad
│   │   ├── ...
│   │   ├── ...
│   ├── Macrophage_p3_vs_Macrophage_p20-sicer
│   │   ├── ...
│   │   ├── ...
│   ├── ...
│   ├── ...
```

### Other important files

Some of the other important files in the `working_dir` are:

* `contrast.tab`: if contrasts are supplied for running *DiffBind*, then they are saved in this tab-delimited file
* `HPC_usage_table.txt`: tabular report of how each *Snakemake* rule utilized the HPC cluster with details. The older version of this file from the phase1 execution is also retained by renaming it.

```bash
<working_dir>
│ 
│ 
├── ...
├── ...
├── contrast.tab
├── HPC_usage_table.txt
├── HPC_usage_table.txt.2020_06_22_05_14_24
├── ...
├── ...
```

All other folder and files in the `working_dir` are for housekeeping and are required for successful execution of the CCBR_Pipeliner.
