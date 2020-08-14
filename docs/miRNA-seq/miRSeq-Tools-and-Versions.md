## Reference Genomes
|Name|Species|Common name|Annotation Version|
|----|-------|-----------|------------------|
|hg38|_Homo sapiens_|Human|Genome Reference Consortium Human Build 38|
|mm10|_Mus musculus_|House mouse|Genome Reference Consortium Mouse Build 38

## Software
### Quality control and pre-processing
|Package/Tool|Version|Usage|Reference|
|------------|-------|-----|---------|
|FastQC|0.11.5|Preliminary quality control on FASTQ reads before and after adapter trimming|[1](#ref1)|
|Cutadapt|1.18|Adapter sequence trimming|[2](#ref2)|
|Kraken|1.1|Assesses microbial contamination|[3](#ref3)|
|KronaTools|2.7|Visualizes results from Kraken|[4](#ref4)
|FastQ Screen|0.9.3|Assesses sequence contamination|[5](#ref5)|
|MultiQC|1.4|QC report aggregation and generation|[6](#ref6)|
|FASTX-Toolkit|0.0.14|FASTA and FASTQ conversion kit|[7](#ref7)|

### Alignment and differential expression
|Package/Tool|Version|Usage|Reference|
|------------|-------|-----|---------|
|miRDeep2|2.0.0.8|Backbone for miRSeq alignment and quantification. Dependencies include `Bowtie1`, `ViennaRNA`, `RandFold`, and `Perl`|[8](#ref8), [9](#ref9), [10](#ref10), [11](#ref11), [12](#ref12)|
|edgeR|3.28.1|Normalization and differential miR expression analysis|[13](#ref13), [14](#ref14)|
|R|3.6.1|Programming language used to run edgeR|[15](#ref15)|

#### References
<a name=ref1><sup>1</sup></a> Andrews, S. 2018. "FastQC: A quality control tool for high throughput sequence data." http://www.bioinformatics.babraham.ac.uk/projects/fastqc/. Version 0.11.5

<a name=ref2><sup>2</sup></a> Martin, M. 2011. "Cutadapt removes adapter sequences from high-throughput sequencing reads." _EMBnet.journal_ 17(1): 10-12. [doi: 10.14806/ej.17.1.200](https://doi.org/10.14806/ej.17.1.200)

<a name=ref3><sup>3</sup></a> Wood and Salzberg. 2014. "Kraken: ultrafast metagenomic sequence classification using exact alignments." _Genome Biol._ 15: R46. [doi: 10.1186/gb-2014-15-3-r46](https://doi.org/10.1186/gb-2014-15-3-r46)

<a name=ref4><sup>4</sup></a> Ondov, Bergman, and Phillippy. 2011. "Interactive metagenomic visualization in a Web browser." _BMC Bioinformatics_ 12: 385. [doi: 10.1186/1471-2105-12-385](https://doi.org/10.1186/1471-2105-12-385)

<a name=ref5><sup>5</sup></a> Wingett and Andrews. 2018. "FastQ Screen: A tool for multi-genome mapping and quality control." _F1000Res._ 7: 1338. [doi: 10.12688/f1000research.15931.2](https://doi.org/10.12688/f1000research.15931.2)

<a name=ref6><sup>6</sup></a> Ewels, Magnusson, _et al._ 2016. "MultiQC: Summarize analysis results for multiple tools and samples in a single report." _Bioinformatics_ 32(19): 3047-3048. [doi: 10.1093/bioinformatics/btw354](https://doi.org/10.1093/bioinformatics/btw354)

<a name=ref7><sup>7</sup></a> Gordon, A. 2010. "FASTX-Toolkit: FASTQ/A short-reads pre-processing tools." http://hannonlab.cshl.edu/fastx_toolkit/index.html

<a name=ref8><sup>8</sup></a> Friedlander, Mackowiak, _et al._ 2012. "miRDeep2 accurately identifies known and hundreds of novel microRNA genes in seven animal clades." _Nucleic Acids Res._ 40(1): 37-52. [doi: 10.1093/nar/gkr688](https://doi.org/10.1093/nar/gkr688)

<a name=ref9><sup>9</sup></a> Langmead, Trapnell, _et al._ 2009. "Ultrafast and memory-efficient alignment of short DNA sequences to the human genome." _Genome Biol._ 10: R25.  [doi: 10.1186/gb-2009-10-3-r25](https://doi.org/10.1186/gb-2009-10-3-r25)

<a name=ref10><sup>10</sup></a> Lorenz, Bernhart, _et al._ 2011. "ViennaRNA Package 2.0." _Algorithms Mol Biol._ 6: 26. [doi: 10.1186/1748-7188-6-26](https://doi.org/10.1186/1748-7188-6-26)

<a name=ref11><sup>11</sup></a> Bonnet, Wuyts, _et al._ 2004. "Evidence that microRNA precursors, unlike other non-coding RNAs, have lower folding free energies than random sequences." _Bioinformatics_ 20(17): 2911-2917. [doi: 10.1093/bioinformatics/bth374](https://doi.org/10.1093/bioinformatics/bth374)

<a name=ref12><sup>12</sup></a> "perl - The Perl 5 language interpreter." 2017. https://www.perl.org. Version 5.24.3.

<a name=ref13><sup>13</sup></a> Robinson, McCarthy, and Smyth. 2010. "edgeR: a Bioconductor package for differential expression analysis of digital gene expression data. _Bioinformatics_ 26: 139-140. [doi: 10.1093/bioinformatics/btp616](https://doi.org/10.1093/bioinformatics/btp616)

<a name=ref14><sup>14</sup></a> McCarthy, Chen, and Smyth. 2012. "Differential expression analysis of multifactor RNA-Seq experiments with respect to biological variation." _Nucleic Acids Res._ 40(10): 4288-4297. [doi: 10.1093/nar/gks042](https://doi.org/10.1093/nar/gks042)

<a name=ref15><sup>15</sup></a> "The R Project for Statistical Computing." https://www.r-project.org/. [Version 3.6.1](https://cran.r-project.org/src/base/R-3/R-3.6.1.tar.gz), released 2019-07-05.
