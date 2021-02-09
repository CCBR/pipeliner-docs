# Output from the whole genome and exome pipelines
The output files and their locations are broken down here per pipeline type.  All file locations are relative to the working directory specified for the Pipeliner run.

## Initial QC
The `Intial QC` pipeline is the first step for both exome and genome workflows.  It implements alignment and pre-processing according to best practices for GATK 3.6.

Here's a table of the most important output files from this pipeline. 

<table>
    <thead>
        <tr>
            <th>Pipeline</th>
            <th>Output Type</th>
            <th>Tool(s)</th>
            <th>File Location</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>Initial QC</td>
        </tr>
        <tr>
            <td>Original fastqs (symlinked)</td>
            <td>--</td>
            <td>[sample].R[1,2].fastq.gz</td>
        </tr>
        <tr>
            <td>Recalibrated (BQSR) BAMs</td>
            <td>GATK 3.6</td>
            <td>[sample].recal.bam</td>
        </tr>
        <tr>
            <td>QC Report</td>
            <td>multiqc, qualimap, fastqc, fastq_screen</td>
            <td>multiqc_report.html</td>
        </tr>
    </tbody>
</table>

## Germline
This pipeline is essentially the GATK Best Practices with a few alterations detailed below. Briefly, joint SNP and INDEL variant detection is conducted across all samples included in a pipeline run using the GATK Haplotypcaller under default settings. This produces the 'combined.vcf' call file. This file is subsequently filtered at two levels of stringency based on several GATK annotations:

1. A strict set of criteria (QD < 2.0, FS > 60.0, MQ < 40.0, MQRankSum < -12.5, ReadPosRankSum < -8.0 for SNPs; QD < 2.0, FS > 200.0, ReadPosRankSum < -20.0 for INDELs) generates the 'combined.strictFilter.vcf'. This call set is highly stringent, maximizing the true positive rate at the expense of an elevated false negative rate. This call set is really only intended for more general population genetic scale analyses (e.g., burden tests, admixture, linkage/pedigree based analysis, etc.) where false positives can be significantly confounding.
2. A relaxed set of criteria (QD < 2.0, FS > 60.0 for SNPs; QD < 2.0, FS > 200.0 for INDELs) generates the 'combined.relaxedFilter.vcf' file. This call set is an attempt to optimize the balance between false positive and false negative, and is generally suitable for all discovery applications. Unless you have strong justification otherwise, the 'combined.relaxedFilter.vcf' file should be used for all downstream analyses.

In addition, we provide structural variants called using Manta v1.2.0 and Svaba. We also provide copy number calling using Freec and Sequenza, as well as Canvas for WGS data.  Finally, a basic analyses of sample relatedness and ancestry (e.g., % European, African, etc.) is also performed and displayed as a network tree.

<table>
    <thead>
        <tr>
            <th>Pipeline</th>
            <th>Output Type</th>
            <th>Tool(s)</th>
            <th>File Location</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=16>Germline</td>
        </tr>
        <tr>
            <td rowspan=7>SNVs</td>
        </tr>
        <tr>
            <td>Strict Filter</td>
            <td>exome.strictFilter.vcf</td>
        </tr>
        <tr>
            <td>Relaxed Filter</td>
            <td>exome.relaxedFilter.vcf</td>
        </tr>
        <tr>
            <td rowspan=4>Admixture and PLINK</td>
        </tr>
        <tr>
            <td>admixture_out/admixture_mqc.png</td>
        </tr>
        <tr>
            <td>admixture_out/admixture_table.tsv</td>
        </tr>
        <tr>
            <td>admixture_out/samples_and_knowns_filtered_recode*</td>
        </tr>
        <tr>
            <td rowspan=3>Structural Variants</td>
        </tr>
        <tr>
            <td>Manta</td>
            <td>manta_out/[pair]/results/variants/diploidSV.vcf.gz</td>
        </tr>
        <tr>
            <td>SvABA</td>
            <td>svaba_out/*</td>
        </tr>
        <tr>
            <td rowspan=2>Copy Number Variants</td>
        </tr>
        <tr>
            <td>Canvas (WGS only)</td>
            <td>canvas_out/*</td>
        </tr>
    </tbody>
</table>


## Tumor-Normal
This workflow calls somatic SNPs and INDELs using three variant detection algorithms. For each of these tools, variants are called in a paired tumor-normal fashion, with default settings. For each sample, the resulting VCF is fully annotated using VEP v92 and converted to a MAF file using the vcf2maf tool. Resulting MAF files are found in the onctotator_out directory within each caller's results directory (e.g., mutect2_out/oncotator_out/NORMAL+TUMOR.maf). Individual sample MAF files are then merged within the oncotator_out directory for each caller (e.g., mutect2_out/oncotator_out/mutect2_merged.maf), and MutSigCV is run for each caller separately (e.g., mutect2_out/mutsigCV_out/). In addition, within each caller's output directory, an oncoplot for the top 30 non-silent mutated genes and a general MAF summary are generated.

For Copy Number Variants (CNVs), two tools are employed in tandem.  First, Control-FREEC is run with default parameters.  This generates pileup files that can be used by Sequenza, primarily for jointly estimating contamination and ploidy. These value are used to run Freec a second time for improved performance.

Sample pairing must be provided as shown in the Quick Start guide. Individual germline samples samples can be used multiple times (e.g., for multiple tumors from the same patient), as long as one of the two samples in the pair is unique. You cannot run the exact pair in duplicate in the same run.

For Mutect2, we use a panel of normals (PON) developed from the ExAC (excluding TCGA) dataset, filtered for variants <0.001 in the general population, and also including and in-house set of blacklisted recurrent germline variants that are not found in any population databases.

Finally, germline analysis is also performed (see above for output details) with the Tumor-Normal pipeline.
 
 

<table>
    <thead>
        <tr>
            <th>Pipeline</th>
            <th>Output Type</th>
            <th>Tool(s)</th>
            <th>File Location</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=36>Somatic Tumor-Normal</td>
        </tr>
        <tr>
            <td rowspan=27>SNVs</td>
        </tr>
        <tr>
            <td>mutect VCF</td>
            <td>mutect_out/[pair].FINAL.vcf</td>
        </tr>
        <tr>
            <td rowspan=5>Mutect MAF and Summaries</td>
        </tr>
        <tr>
            <td>mutect_out/oncotator_out/final_filtered.maf</td>
        </tr>
        <tr>
            <td>mutect_out/oncotator_out/variants_fixed.maf</td>
        </tr>
        <tr>
            <td>mutect_out/oncotator_out/tcga_comparison.pdf</td>
        </tr>
        <tr>
            <td>mutect_out/oncotator_out/genes_by_VAF.pdf</td>
        </tr>
        <tr>
            <td rowspan=5>Mutect2 MAF and Summaries</td>
        </tr>
        <tr>
            <td>mutect2_out/oncotator_out/final_filtered.maf</td>
        </tr>
        <tr>
            <td>mutect2_out/oncotator_out/variants_fixed.maf</td>
        </tr>
        <tr>
            <td>mutect2_out/oncotator_out/tcga_comparison.pdf</td>
        </tr>
        <tr>
            <td>mutect2_out/oncotator_out/genes_by_VAF.pdf</td>
        </tr>
        <tr>
            <td rowspan=5>VarDict MAF and Summaries</td>
        </tr>
        <tr>
            <td>vardict_out/oncotator_out/final_filtered.maf</td>
        </tr>
        <tr>
            <td>vardict_out/oncotator_out/variants_fixed.maf</td>
        </tr>
        <tr>
            <td>vardict_out/oncotator_out/tcga_comparison.pdf</td>
        </tr>
        <tr>
            <td>vardict_out/oncotator_out/genes_by_VAF.pdf</td>
        </tr>
        <tr>
            <td rowspan=5>Strelka MAF and Summaries</td>
        </tr>
        <tr>
            <td>strelka_out/oncotator_out/final_filtered.maf</td>
        </tr>
        <tr>
            <td>strelka_out/oncotator_out/variants_fixed.maf</td>
        </tr>
        <tr>
            <td>strelka_out/oncotator_out/tcga_comparison.pdf</td>
        </tr>
        <tr>
            <td>strelka_out/oncotator_out/genes_by_VAF.pdf</td>
        </tr>
        <tr>
            <td rowspan=5>Merged Somatic Variants</td>
        </tr>
        <tr>
            <td>merged_somatic_variants/oncotator_out/final_filtered.maf</td>
        </tr>
        <tr>
            <td>merged_somatic_variants/oncotator_out/variants_fixed.maf</td>
        </tr>
        <tr>
            <td>merged_somatic_variants/oncotator_out/tcga_comparison.pdf</td>
        </tr>
        <tr>
            <td>merged_somatic_variants/oncotator_out/genes_by_VAF.pdf</td>
        </tr>
        <tr>
            <td rowspan=2>Structural Variants</td>
        </tr>
        <tr>
            <td>Manta</td>
            <td>manta_out/[pair]/results/variants/diploidSV.vcf.gz</td>
        </tr>
        <tr>
            <td rowspan=4>Copy Number Variants</td>
        </tr>
        <tr>
            <td>Control-FREEC (Pass 1)</td>
            <td>freec_out/pass1/[pair].recal.bam_CNVs.p.value.txt</td>
        </tr>
        <tr>
            <td>Control-FREEC (Pass 2)</td>
            <td>freec_out/pass2/[pair].recal.bam_CNVs.p.value.txt</td>
        </tr>
        <tr>
            <td>Sequenza</td>
            <td>sequenza_out/[tumor-sample]/*</td>
        </tr>
    </tbody>
</table>

## Tumor-Only
In general, the tumor-only pipeline is a stripped down version of the tumor-normal pipeline. We only run MuTect2, Mutect, and VarDict for somatic variant detection, with the same PON and filtering as described above for the tumor-normal pipeline.


