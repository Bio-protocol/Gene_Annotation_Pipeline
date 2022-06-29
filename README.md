[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)

# Data, Code and Workflows Guideline

To guide eBook authors having a better sense of the workflow layout, here we briefly introduce the specific purposes of the dir system. 


1. __cache__: Here, it stores intermediate datasets or results that are generated during the preprocessing steps.
2. __graphs__: The graphs/figures produced during the analysis.
3. __input__: Here, we store the raw input data. Data size > 100M is not allowed. We recommend using small sample data for the illustration purpose of the workflow. If you have files > 100M, please contact the chapter editor to find a solution. 
4. __lib__: The source code, functions, or algorithms used within the workflow.
5. __output__: The final output results of the workflow.
6. __workflow__: Step by step pipeline. It may contain some sub-directories. 
    - It is suggested to use __a numbering system__ and __keywords__ to indicate the order and the main purpose of the scripts, i.e., `1_fastq_quality_checking.py`, `2_cleaned_reads_alignment.py`.
    - To ensure reproducibility, please use the __relative path__ within the `workflow`.
7. __README__: In the readme file, please briefly describe the purpose of the repository, the installation, and the input data format. 
    - We recommend using a diagram to describe the workflow briefly.
    - Provide the installation details.
    - Show a small proportion of the input data unless the data file is in a well-known standard format, i.e., the `head` or `tail` of the input data.

## Overview of an example workflow: Fastq data quality checking

This is an example workflow to check the quality of the paired-end fastq files using `FastQC` software.

![](graphs/diagram.png)

## Installation

- __Running environment__: 
    - The workflow was constructed based on the __Linux system__ running the Oracle v1.6 to 1.8 java runtime environment (JREs).

- __Required software and versions__: 
    
1.	MAKER-P (Campbell et al., 2014; v3.1; http://www.yandell-lab.org/software/maker-p.html) 
2.	RepeatMasker (Tarailo-Graovac et al., 2009; v4.1.1; www.repeatmasker.org)
3.	Augustus (Stanke et al., 2006; v3.0; http://bioinf.uni-greifswald.de/augustus/)
4.	Fgenesh (Solovyev et al., 2006; v8.0.0a; http://www.softberry.com/berry.phtml)
5.	Snap (Korf, 2004; version 2013-11-29; https://github.com/KorfLab/SNAP)
6.	WUBLAST (Gish, W. (1996-2003); v2.0; ttp://blast.wustl.edu)
7.	InterProScan (Quevillon et al., 2005; v89.0; http://www.ebi.ac.uk/interpro/search/sequence-search).
8.	Exonerate (Slater GS and Birney E, 2005; https://www.ebi.ac.uk/about/vertebrate-genomics/software/exonerate)


## Input Data

The example data used here is the FASTA file.  

## Major steps

step 1. Set up each configure file, feed input data, evidence data to the .ctl file, and set parameter as needed.

step 2. Run script ‘run_maker.sh’ to annotate the genomes.

step 3. Use the following command to create the final merged gff file. The “-n” option would produce a gff file without genome sequences.

   gff3_merge -s -n -d genome.maker.output/genome_master_datastore_index.log>genome.noseq.gff

step 4. Generate AED plots.

   /programs/maker/AED_cdf_generator.pl -b 0.025 chr1.noseq.gff > AED_rnd3

   Plot the file AED_rnd3 in Excel or any plotting software. 

step 5. Load the gff file into IGV or JBrowse. Instructions for IGV and JBrowse can be found at:

   IGV: http://software.broadinstitute.org/software/igv/UserGuide

   JBrowse: https://biohpc.cornell.edu/lab/userguide.aspx?a=software&i=357#c

## Expected results

GFF3 file with gene structure information, and AED score

## License
It is a free and open source software, licensed under []() (choose a license from the suggested list:  [GPLv3](https://github.com/github/choosealicense.com/blob/gh-pages/_licenses/gpl-3.0.txt), [MIT](https://github.com/github/choosealicense.com/blob/gh-pages/LICENSE.md), or [CC BY 4.0](https://github.com/github/choosealicense.com/blob/gh-pages/_licenses/cc-by-4.0.txt)).
