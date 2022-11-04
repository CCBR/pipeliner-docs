## Quality-control pipeline

### QC assessment tools

| Tool                     | Version | Notes                                                        |
| ------------------------ | ------- | ------------------------------------------------------------ |
| FastQC<sup>1</sup>       | 0.11.5  | Assess sequencing quality, run before and after adapter trimming |
| Kraken<sup>2</sup>       | 1.1     | Assess microbial taxonomic composition                       |
| KronaTools<sup>3</sup>   | 2.7     | Visualize kraken output                                      |
| FastQ Screen<sup>4</sup> | 0.9.3   | Assess contamination; additional dependencies: bowtie2/2.3.4, perl/5.24.3 |
| Preseq<sup>5</sup>       | 2.0.3   | Estimate library complexity                                  |
| NGSQC<sup>6</sup>        |         | Infers a set of global QC indicators to asses data quality          |
| MultiQC<sup>7</sup>      | 1.7     | Aggregate sample statistics and quality-control information across all samples |

### Data processing tools

| Tool                   | Version | Notes                                                        |
| ---------------------- | ------- | ------------------------------------------------------------ |
| Cutadapt<sup>8</sup>   | 1.18    | Remove adapter sequences and perform quality trimming        |
| BWA<sup>9</sup> mem    | 0.7.17  | Read alignment, first to identify reads aligning to blacklisted regions and later for the remainder of the genome |
| Picard<sup>10</sup>    | 2.17.11 | Run SamToFastq (for blacklist read removal) and MarkDuplicates (to remove PCR duplicates in PE data) |
| SAMtools<sup>11</sup>  | 1.6     | Remove reads with mapQ less than 6. Also run flagstat and idxstats to calculate alignment statistics. |
| MACS<sup>12</sup>      | 2.1.1   | Run filterdup on SE data (`--keep-dup=”auto”`) to remove PCR duplicates |
| Bedtools<sup>13</sup>  | 2.27.1  | Run intersect and bedtobam to convert .tag.Align.gz to .bam for use with Deeptools (specific to SE data) |
| ppqt<sup>14</sup>      | 2.0     | Also known as phantompeakqualtools, used to calculate estimated fragment length (used for bigwig and peak calling for SE data). Also produces QC metrics: NSC and RSC. |
| deepTools<sup>15</sup> | 3.0.1   | Used for bigwig creation and multiple QC metrics. Use bamcoverage to create RPGC-normalized data: `--binSize 25 --smoothLength 75 --normalizeUsing RPGC`. For PE data, add `--centerReads`. For Control SE, add `-e 200`. For ChIP SE, add `-e [estimated fragment length]`. For control subtraction (inputnorm), use bigwigCompare: `--binSize 25 --operation ‘subtract’`. Run multiBigWigSummary, plotCorrelation, plotPCA, plotFingerprint, computeMatrix, plotHeatmap, and plotProfile for QC plots. |


## Peak calling and differential binding pipeline

### Peak calling and differential peak calling tools

|           Tool                |      Version    |     Notes       |
| ----------------------------- | --------------- | --------------- | 
|       MACS<sup>16</sup>       |      2.1.1      |                 |
|      Sicer<sup>17</sup>       |       1.1       |                 |
|       GEM<sup>18</sup>        |       3.0       |                 |
|      MANorm<sup>19</sup>      |      1.1.4      |                 |
|     DiffBind<sup>20,21</sup>  |     2.10.0      |                 |

### Annotations, motifs, and QC assesment tools

|           Tool              |      Version    |     Notes       |
| --------------------------- | --------------- | --------------- | 
|      Uropa<sup>22</sup>     |      4.0.2      |                 |
|      Homer<sup>23</sup>     |      4.10.1     |                 |
|      IDR<sup>24</sup>       |      2.0.3      |                 |
|      Jaccard                |                 |                 |
|      FRiP                   |                 |                 |


## References

<sup>**1. FastQC:** Andrews, S. (2010). FastQC: a quality control tool for high throughput sequence data. [https://www.bioinformatics.babraham.ac.uk/projects/fastqc/](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)</sup>  
<sup>**2. Kraken:** Wood, D. E. and S. L. Salzberg (2014). "Kraken: ultrafast metagenomic sequence classification using exact alignments." Genome Biol 15(3): R46. [http://ccb.jhu.edu/software/kraken/](http://ccb.jhu.edu/software/kraken/)</sup>  
<sup>**3.  Krona:** Ondov, B. D., et al. (2011). "Interactive metagenomic visualization in a Web browser." BMC Bioinformatics 12(1): 385. [https://github.com/marbl/Krona/wiki](https://github.com/marbl/Krona/wiki)</sup>  
<sup>**4. FastQ Screen:** Wingett, S. and S. Andrews (2018). "FastQ Screen: A tool for multi-genome mapping and quality control." F1000Research 7(2): 1338. [https://www.bioinformatics.babraham.ac.uk/projects/fastq_screen/](https://www.bioinformatics.babraham.ac.uk/projects/fastq_screen/)</sup>  
<sup>**5. Preseq:** Daley, T. and A.D. Smith (2013). Predicting the molecular complexity of sequencing libraries. Nat Methods 10(4): 325-7. [http://smithlabresearch.org/software/preseq/](http://smithlabresearch.org/software/preseq/)</sup>  
<sup>**6. NGSQC:** Mendoza-Parra M., et al. (2013). A quality control system for profiles obtained by ChIP sequencing. Nucleic Acids Research 41(21,): e196.</sup>  
<sup>**7. MultiQC:** Ewels, P., et al. (2016). "MultiQC: summarize analysis results for multiple tools and samples in a single report." Bioinformatics 32(19): 3047-3048. [https://multiqc.info/docs/](https://multiqc.info/docs/)</sup>  
<sup>**8. Cutadapt:** Martin, M. (2011). "Cutadapt removes adapter sequences from high-throughput sequencing reads." EMBnet 17(1): 10-12. [https://cutadapt.readthedocs.io/en/stable/](https://cutadapt.readthedocs.io/en/stable/)</sup>  
<sup>**9. BWA:** Li H. and Durbin R. (2009) Fast and accurate short read alignment with Burrows-Wheeler Transform. Bioinformatics 25: 1754-60. [http://bio-bwa.sourceforge.net/bwa.shtml](http://bio-bwa.sourceforge.net/bwa.shtml)</sup>  
<sup>**10. Picard:** The Picard toolkit. [https://broadinstitute.github.io/picard/](https://broadinstitute.github.io/picard/)</sup>  
<sup>**11. SAMtools:** Li, H., et al. (2009). "The Sequence Alignment/Map format and SAMtools." Bioinformatics 25(16): 2078-2079. [http://www.htslib.org/doc/samtools.html](http://www.htslib.org/doc/samtools.html)</sup>  
<sup>**12. MACS:** Zhang, Y., et al. (2008). Model-based Analysis of ChIP-Seq (MACS). Genome Biol 9: R137. [https://github.com/macs3-project/MACS](https://github.com/macs3-project/MACS)</sup>  
<sup>**13. Bedtools:** Quinlan, A.R. (2014). BEDTools: The Swiss‐Army Tool for Genome Feature Analysis. Current Protocols in Bioinformatics, 47: 11.12.1-11.12.34. [https://bedtools.readthedocs.io/en/latest/index.html](https://bedtools.readthedocs.io/en/latest/index.html)</sup>  
<sup>**14. ppqt:** Landt S.G., et al. (2012). ChIP-seq guidelines and practices of the ENCODE and modENCODE consortia. Genome Res 22(9): 1813-31. [https://github.com/kundajelab/phantompeakqualtools](https://github.com/kundajelab/phantompeakqualtools)</sup>  
<sup>**15. deepTools:** Ramírez, F., et al. (2016). [deepTools2: A next Generation Web Server for Deep-Sequencing Data Analysis](http://nar.oxfordjournals.org/content/early/2016/04/12/nar.gkw257.abstract), Nucleic Acids Research, 44(W1), W160-W165.</sup>  
<sup>**16. MACS:** Zhang Y., et al. (2008). Model-based Analysis of ChIP-Seq (MACS). Genome Biol 9(9): R137</sup>    
<sup>**17. Sicer:** Xu S., et al. (2014). Spatial Clustering for Identification of ChIP-Enriched Regions (SICER) to Map Regions of Histone Methylation Patterns in Embryonic Stem Cells. Methods Mol Biol 1150: 97–111.</sup>    
<sup>**18. GEM:** Guo Y., Mahony S., and D. K. Gifford. (2012). High Resolution Genome Wide Binding Event Finding and Motif Discovery Reveals Transcription Factor Spatial Binding Constraints. PLoS Comput Biol 8(8): e1002638.</sup>    
<sup>**19. MANorm:** Shao, Z., et al. (2012). MAnorm: a robust model for quantitative comparison of ChIP-Seq data sets. Genome Biology 13: R16. https://manorm.readthedocs.io/en/latest/index.html </sup>    
<sup>**20. DiffBind:** Ross-Innes C.S., et al. (2012). Differential oestrogen receptor binding is associated with clinical outcome in breast cancer. Nature 481: 389–393.</sup>    
<sup>**21. DiffBind:** Stark R. and G. Brown. (2011). DiffBind: differential binding analysis of ChIP-Seq peak data. http://bioconductor.org/packages/release/bioc/vignettes/DiffBind/inst/doc/DiffBind.pdf.</sup>    
<sup>**22. Uropa:** Kondili M., et al. (2017). UROPA: a tool for Universal RObust Peak Annotation. Scientific Reports 7: 2593.</sup>    
<sup>**23. Homer:** Heinz S., et al. (2010). Simple combinations of lineage-determining transcription factors prime cis-regulatory elements required for macrophage and B cell identities. Mol Cell 38(4): 576–589.</sup>    
<sup>**24. IDR:** Li Q., et al. (2011). Measuring reproducibility of high-throughput experiments. Ann Appl Stat 5(3): 1752-1779.</sup>    
