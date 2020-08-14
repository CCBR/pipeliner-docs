## Reference Genomes
|Name|Species|Common name|Annotation Version|
|----|-------|-----------|------------------|
|GRCh38|_Homo sapiens_|Human|Genome Reference Consortium Human Build 38|
|mm10|_Mus musculus_|House mouse|Genome Reference Consortium Mouse Build 38

## Software
### Data processing
|Package name|Version|Usage|Reference|
|------------|-------|-----|-----------|
|R|3.6.1|Primary framework and programming language for data processing|[1](#ref1)|
|Seurat|3.1.4|Primary program for processing single cell data|[2](#ref2), [3](#ref3)|
|Routliers|0.0.0.3|R package for identifying outliers via median absolute deviation|[4](#ref4), [5](#ref5), [6](#ref6)|
|SCTransform|Included in Seurat v3.1.4|Used for normalization. This replaces the ScaleData/Normalization from previous versions of Seurat|[7](#ref7)|
|URD|1.1.0|Used to calculate optimal number of principal components through the Marchenko-Pastur law|[8](#ref8)|
|UMAP|0.4.6|2D and 3D dimensionality reduction projection for visualizing cells and relative similarity|[9](#ref9), [10](#ref10)|
|SingleR|1.0.5|Cell type annotation based on correlation to cell types within curated databases|[11](#ref11), [12](#ref12)|
|DoubletFinder|2.0.2|Algorithm to determine likely doublets based on cell distribution and cell type similarity|[13](#ref13), [14](#ref14)|

### Visualization
|Package name|Version|Usage|Reference|
|------------|-------|-----|-----------|
|ggplot2|3.3.0|Basis for a majority of the visualization, including violin distribution plots and UMAP plots|[15](#ref15)|
|Rmarkdown|2.1|Report writing in html and pdf formats|[16](#ref16), [17](#ref17)|
|VennDiagram|1.6.20|Generate Venn diagrams|[18](#ref18)|
|cluster|2.1.0|Analyze clustering similarity for optimization via silhouette plots|[19](#ref19)|

## References

<a name=ref1><sup>1</sup></a> "The R Project for Statistical Computing." https://www.r-project.org/. [Version 3.6.1](https://cran.r-project.org/src/base/R-3/R-3.6.1.tar.gz), released 2019-07-05.

<a name=ref2><sup>2</sup></a> Stuart, Butler, _et al._, 2019. "Comprehensive Integration of Single-Cell Data." _Cell_ 177 (7): 1888-1902.e21. [doi: 10.1016/j.cell.2019.05.031](https://doi.org/10.1016/j.cell.2019.05.031)

<a name=ref3><sup>3</sup></a> Butler, Hoffman, _et al._, 2018. "Integrating single-cell transcriptomic data across different conditions, technologies, and species." _Nat. Biotechnol._ 36: 411-420. [doi: 10.1038/nbt.4096](https://doi.org/10.1038/nbt.4096)

<a name=ref4><sup>4</sup></a> Leys, Ley, _et al._, 2013. "Detecting outliers: Do not use standard deviation around the mean, use absolute deviation around the median." _J. Exp. Soc. Psychol._ 49(4): 764-766. [doi: 10.1016/j.jesp.2013.03.013](https://doi.org/10.1016/j.jesp.2013.03.013)

<a name=ref5><sup>5</sup></a> Leys, Klein, _et al._, 2018. "Detecting multivariate outliers: Use a robust variant of the Mahalanobis distance." _J. Exp. Soc. Psychol._ 74: 150-156. [doi: 10.1016/j.jesp.2017.09.011](https://doi.org/10.1016/j.jesp.2017.09.011)

<a name=ref6><sup>6</sup></a> Delecre and Klein. 2019. "Routliers: Robust Outliers Detection." https://CRAN.R-project.org/package=Routliers.

<a name=ref7><sup>7</sup></a> Hafemeister and Satija. 2019. "Normalization and variance stabilization of single-cell RNA-seq data using regularized negative binomial regression." _Genome Biol._ 20: 296. [doi: 10.1186/s13059-019-1874-1](https://doi.org/10.1186/s13059-019-1874-1)

<a name=ref8><sup>8</sup></a> Farrell, Wang, _et al._ 2018. "Single-cell reconstruction of developmental trajectories during zebrafish embryogenesis." _Science_ 360: 979. [doi: 10.1126/science.aar3131](https://doi.org/10.1126/science.aar3131)

<a name=ref9><sup>9</sup></a> McInnes, L. "UMAP." https://github.com/lmcinnes/umap.

<a name=ref10><sup>10</sup></a> McInnes and Healy. 2018. "UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction." _ArXiv e-prints_. [1802.03426](https://arxiv.org/pdf/1802.03426.pdf).

<a name=ref11><sup>11</sup></a> Aran, Looney, _et al._ 2019. "Reference-based analysis of lung single-cell sequencing reveals a transitional profibrotic macrophage." _Nat. Immunol._ 20: 163-172. [doi: 10.1038/s41590-018-0276-y](https://doi.org/10.1038/s41590-018-0276-y).

<a name=ref12><sup>12</sup></a> Aran, Lun, _et al._ "Reference-Based Single-Cell RNA-Seq Annotation." https://bioconductor.org/packages/release/bioc/html/SingleR.html. [doi: 10.18129/B9.bioc.SingleR](https://doi.org10.18129/B9.bioc.SingleR)

<a name=ref13><sup>13</sup></a> McGinnis, Murrow, and Gartner. 2019. "DoubletFinder: Doublet Detection in Single-Cell RNA Sequencing Data Using Artificial Nearest Neighbors." _Cell Systems_ 8(4): 329-337.e4. [doi: 10.1016/j.cels.2019.03.003](https://doi.org/10.1016/j.cels.2019.03.003)

<a name=ref14><sup>14</sup></a> McGinnis, C. "DoubletFinder." https://github.com/chris-mcginnis-ucsf/DoubletFinder.

<a name=ref15><sup>15</sup></a> Wickham, H. 2016. _ggplot2: Elegant graphics for data analysis_. Springer-Verlag New York. ISBN 978-3-319-24277-4, https://ggplot2.tidyverse.org. 

<a name=ref16><sup>16</sup></a> Allaire, Xie, _et al._ 2019. _rmarkdown: Dynamic documents for R._ R package version 2.1, https://github.com/rstudio/rmarkdown.

<a name=ref17><sup>17</sup></a> Xie, Allaire, and Grolemund. 2018. _R Markdown: The Definitive Guide._ Chapman and Hall/CRC, Boca Raton, FL, USA. ISBN 9781138359338, https://bookdown.org/yihui/rmarkdown.

<a name=ref18><sup>18</sup></a> Chen and Boutros. 2018. _VennDiagram: Generate high-resolution Venn and Euler plots._ R package version 1.6.20, https://cran.r-project.org/web/packages/VennDiagram

<a name=ref19><sup>19</sup></a> Maechler, Rouseeuw, _et al._ 2019. _cluster: Cluster Analysis Basics and Extensions._ R package version 2.1.0, https://cran.r-project.org/web/packages/cluster/
