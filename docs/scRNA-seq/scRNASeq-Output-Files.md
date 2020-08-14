## Input Files

### Initial input files
The initial input files are obtained from the raw data directory during the `Initialize Directory` step.

```
<WorkingDirectory>
│ 
│
├── ...
├── sample1_NR.h5 -> /data/CCBR_Pipeliner/testdata/scrnaseq/h5/sample1_NR.h5
├── sample1_R.h5 -> /data/CCBR_Pipeliner/testdata/scrnaseq/h5/sample1_R.h5
├── sample2_NR.h5 -> /data/CCBR_Pipeliner/testdata/scrnaseq/h5/sample2_NR.h5
├── sample2_R.h5 -> /data/CCBR_Pipeliner/testdata/scrnaseq/h5/sample2_R.h5
├── ...
```

### Input tab files
These are the tab-delimited files created by the user to indicate groups and contrasts.

```
<WorkingDirectory>
│ 
│
├── contrasts.tab
├── ...
├── groups.tab
├── ...
```

## Single Sample Quality Control

### Filtered Sample Outputs
For each sample, an RDS file containing a Seurat object is exported for both pre- and post-doublet removal. Flag files are also exported to indicate progress to the Snakemake pipeline.

```
├── filtered
│   ├── sample1_NR_doublets.rds
│   ├── sample1_NR.rds
│   ├── sample1_R_doublets.rds
│   ├── sample1_R.rds
│   ├── ...
├── flags
│   ├── sample1_NR.txt
│   ├── ...
```

### Quality control reports
The QC run for each sample produces a number of image outputs that indicate the quality of the sample and show how many cells were removed for each justification (e.g. low number of unique genes). These images and statistics are compiled into a single html report for each sample.

```
├── QC
│   ├── QC_Report_sample1_NR.html
│   ├── ...
│   ├── sample1_NR
│   │   └── images
│   │       ├── cellAnnotUMAP_BP_encode_sample1_NR.pdf
│   │       ├── ...
│   │       ├── cellAnnotVln_BP_encode_sample1_NR.pdf
│   │       ├── ...
│   │       ├── cellCycle_sample1_NR.pdf
│   │       ├── cellsRemovedVenn_sample1_NR.png
│   │       ├── ...
│   │       ├── clusterResolution_0.4_sample1_NR.pdf
│   │       ├── clusterResolution_0.6_sample1_NR.pdf
│   │       ├── ...
│   │       ├── doublets_sample1_NR.pdf
│   │       ├── filterStats_sample1_NR.png
│   │       ├── mitoPct_postFilter_sample1_NR.pdf
│   │       ├── mitoPct_preFilter_sample1_NR.pdf
│   │       ├── ...
│   │       ├── silhouetteResolution_0.4_sample1_NR.pdf
│   │       ├── ...
│   ├── sample1_R
│   │   └── images
│   │       ├── ...
│   ├── ...
```

## Multisample Outputs
After QC is performed on the individual samples, the samples are combined both with and without batch correction. Seurat has named the process of combining samples as "merging" and the process of batch correction as integration. For each contrast, a merged and integrated object is created. 

```
├── integration
│   ├── merged
│   │   └── R-NR
│   │       └── R-NR.rds
│   └── seurat_batch_corrected
│       └── R-NR
│           └── R-NR.rds
```
## Differential Expression
Coming soon

## Miscellaneous Pipeliner Outputs

```
<WorkingDirectory>
│ 
│ 
├── cluster.json
├── ...
├── HPC_usage_table.txt
├── ...
├── logfiles
│   └── blank
├── pairs
├── pipeline_ctrl.sh
├── ...
├── Reports
│   ├── ...
├── Rplots.pdf
├── run.json
├── samples
├── Scripts
│   ├── ...
├── slurmfiles
│   ├── blank
│   ├── ...
├── Snakefile
└── submit_slurm.sh
```
