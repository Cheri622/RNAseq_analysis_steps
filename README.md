# RNAseq_analysis_steps
Workflow as:
![image](https://github.com/Cheri622/RNAseq_analysis_steps/assets/95024780/cbb6f3de-13a1-4550-b14b-749bd2ecd1b8)

## Instruction with reference and download links
1).Raw RNA-sequencing data is usually deposited in the Gene Expression Omnibus (GEO), at https://www.ncbi.nlm.nih.gov/geo/.  
SRA Run Selector -> Gallus gallus; RNA-Seq as: SRR6169229  

In order to download the SRA files onto your machine, we use the NCBI’s SRA toolkit
(https://erilu.github.io/python-fastq-downloader/#finding-raw-sequencing-data-in-geo)  
$sudo apt install sra-toolkit  

2).Aligning and counting reads  
We will align our FASTQ files to the mouse reference genome using the RNA-seq alignment tool STAR.   
(https://github.com/erilu/dendritic-cell-bulk-rnaseq)  
STAR     
The basic options to generate genome indices are as follows:    
--runThreadN NumberOfThreads  
--runMode genomeGenerate  
--genomeDir /path/to/genomeDir (index file output directory)  
--genomeFastaFiles /path/to/genome/fasta1 /path/to/genome/fasta2 ...  
--sjdbGTFfile /path/to/annotations.gtf  

generate genome index file first :  
$./STAR_2.7.11b/Linux_x86_64_static/STAR   
--runThreadN NumberOfThreads  
--runMode genomeGenerate  
--genomeFastaFiles ./genome/*.fa  
--sjdbGTFfile ./genome/annotations.gtf  
--genomeDir ./genome/index  
--genomeSAindexNbases 10  

QC  
$samtools flagstat ./bam/Aligned.sortedByCoord.out.bam    

3).Counting using featureCounts  
download Subread package from http://subread.sourceforge.net.  
unzip subread-1.x.x.tar.gz    
$cd ./subread-2.0.6-source/src  
$make -f Makefile.Linux    

$./subread-2.0.6-source/bin/featureCounts \  
-p -t exon -g gene_id \  
-a ./genome/annotations.gtf  \    
-o ./counts/featurecounts.exon.txt ./bam/*.bam  

4).Analyzing RNA-seq data with DESeq2 in Python   
https://github.com/owkin/PyDESeq2    
DESeq2 docs:    
https://www.bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html  

5).GSEAPY: Gene Set Enrichment Analysis (GSEA) in Python  
GSEAPY Example :  
https://gseapy.readthedocs.io/en/latest/gseapy_example.html#Over-representation-analysis-by-Enrichr-web-services  
