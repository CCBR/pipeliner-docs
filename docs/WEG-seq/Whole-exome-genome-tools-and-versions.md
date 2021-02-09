## Reference genomes
The Initial QC and variant calling pipelines support the following genomes:    
**Human** `hg19` `hg38`  
**Mouse** `mm10`

## Tools and versions

<table>
    <thead>
        <tr>
            <th>Analysis Category</th>
            <th>Software</th>
            <th>Version</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=5>Preprocessing</td>
        </tr>
        <tr>
            <td>Trimmomatic</td>
            <td>0.33</td>
            <td></td>
        </tr>
        <tr>
            <td>bwa aligner</td>
            <td>0.7.15</td>
            <td></td>
        </tr>
        <tr>
            <td>Picard</td>
            <td>2.1.1</td>
            <td></td>
        </tr>
        <tr>
            <td>Genome Analysis Toolkit (GATK)</td>
            <td>3.8-0</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=7>Somatic Variant Calling</td>
        </tr>
        <tr>
            <td>Mutect2</td>
            <td>GATK 3.8-0</td>
            <td></td>
        </tr>
        <tr>
            <td>Mutect</td>
            <td>1.1.7</td>
            <td></td>
        </tr>
        <tr>
            <td>VarDict</td>
            <td>1.4</td>
            <td></td>
        </tr>
        <tr>
            <td>Strelka</td>
            <td>2.9.0</td>
            <td>Tumor-Normal only</td>
        </tr>
        <tr>
            <td>vcf2maf</td>
            <td>1.6.16</td>
            <td></td>
        </tr>
        <tr>
            <td>MutSigCV</td>
            <td>1.41</td>
            <td>Run only if >10 tumor samples</td>
        </tr>
        <tr>
            <td rowspan=4>Germline Variant Calling</td>
        </tr>
        <tr>
            <td>HaplotypeCaller</td>
            <td>GATK 3.8-0</td>
            <td></td>
        </tr>
        <tr>
            <td>Admixture</td>
            <td>1.3.0</td>
            <td></td>
        </tr>
        <tr>
            <td>PLINK</td>
            <td>1.9.0</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=5>Copy Number Variants (CNV)</td>
        </tr>
        <tr>
            <td>Control-FREEC</td>
            <td>11.9</td>
            <td>Tumor-Normal only</td>
        </tr>
        <tr>
            <td>Sequenza-utils</td>
            <td>2.2.0</td>
            <td>Tumor-Normal only</td>
        </tr>
        <tr>
            <td>Sequenza R package</td>
            <td>3.0</td>
            <td>Tumor-Normal only</td>
        </tr>
        <tr>
            <td>Canvas</td>
            <td>1.3.8</td>
            <td>WGS only</td>
        </tr>
        <tr>
            <td rowspan=3>Structural Variants (SV)</td>
        </tr>
        <tr>
            <td>Manta</td>
            <td>1.3.0</td>
            <td></td>
        </tr>
        <tr>
            <td>SvABA</td>
            <td></td>
            <td>WGS only</td>
        </tr>
        <tr>
            <td rowspan=5>Quality Control and Reporting</td>
        </tr>
        <tr>
            <td>qualimap</td>
            <td>2.2.1</td>
            <td></td>
        </tr>
        <tr>
            <td>multiqc</td>
            <td>1.4</td>
            <td></td>
        </tr>
        <tr>
            <td>FastQC</td>
            <td>0.11.5</td>
            <td></td>
        </tr>
        <tr>
            <td>Fastq Screen</td>
            <td>0.9.3</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=4>General scripting</td>
        </tr>
        <tr>
            <td>R</td>
            <td>3.5</td>
            <td></td>
        </tr>
        <tr>
            <td>perl</td>
            <td>5.18.4</td>
            <td></td>
        </tr>
        <tr>
            <td>Python</td>
            <td>3.6</td>
            <td></td>
        </tr>
    </tbody>
</table>