# RNAseq_analysis_steps
Workflow as:
![image](https://github.com/Cheri622/RNAseq_analysis_steps/assets/95024780/cbb6f3de-13a1-4550-b14b-749bd2ecd1b8)

## Instruction with reference links
1). Raw RNA-sequencing data is usually deposited in the Gene Expression Omnibus (GEO), at https://www.ncbi.nlm.nih.gov/geo/.

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
--sjdbOverhang ReadLength-1  

