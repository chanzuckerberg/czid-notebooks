## IDseq QC Report

**Purpose**: This jupyter notebook contains code required to generate and visualize several different IDseq QC metrics on a per-project level.

### Usage and Inputs

**1. Download the github repository containing this jupyter notebook**

This can be done using the command...

`git clone https://github.com/chanzuckerberg/idseq-notebooks.git` 

... or via manual download of the .zip file. You should then have a copy of the QCReport.ipynb jupyter notebook as well as a directory containing the reference files.

The reference files include the following:

- ERCC Reference File: "ERCC_analysis_conc.tsv" obtained from [here](https://github.com/chanzuckerberg/idseq-web/blob/master/app/lib/ercc_data.csv)
- Gene Biotype Reference File: "gene_biotype.csv" obtained by R script using ENSEMBL to HGNC conversion



**2. Ensure that jupyter is installed.** See install instrucutions [here](https://test-jupyter.readthedocs.io/en/latest/install.html).

Start a jupyter notebook by running `jupyter notebook` in the directory containing the "IDSeq QC Report.ipynb" file.


**3. Set up the data for QC metrics on a new project:** 

A. Create a new folder for the raw files in your project: /path/to/folder/PROJECT_NAME/

B. Navigate to IDseq to download the following files:
        
- microbe report files: from the project page select **Download -> Sample Reports**
- report.csv file containing the sample names and basic QC metrics: from the project page select **Download -> Sample Table**
            
C. IF you are interested in generating a gene counts matrix and/or evaluating ERCC counts, request download of host genecounts from IDseq

D. Unzip the downloaded folders and move them to the PROJECT_NAME/raw_data folder you created in **step A**.
        

**4. Set the filepaths for the user-configured inputs**
* `project_dir = '{/path/to/folder/PROJECT_NAME/}'`
* `report_dir = project_dir + '{name of directory containing IDseq report .csv files}'`
* `report_csv = project_dir + '{name of .csv file containing sample info and qc metrics}'`
* `genecounts_dir = project_dir + '{name of directory containing host gene counts}`
* `output_dir = project_dir + '{name of directory where results should be output}`

Note: IF you are not interested in generating a gene x sample table or evaluating ERCC counts, set the `genecounts_dir = None`

**5. Set the required user input values**

Default values are provided for the following variables (explained in the "Gather Necessary Files and User Input" section)
* `metadata_var`  :  which metadata field would you like to stratify across for QC metrics plots
* `var_of_interest`  :  when generating a combined matrix of taxons x samples, what variable should be used 
* `tax_level`  :  species or genus
* `NT_L_filter`  :  should the alignment length be filtered for taxonomic hits in NT?
* `NR_L_filter`  :  should the alignment length be filtered for taxonomic hits in NR?


### Outputs
* QC Plots shown in jupyter notebook
* Microbe matrix (taxa x samples) compiled from single-sample IDseq reports (downloaded from IDseq)
* Genecounts matrix (genes x samples) compiled from single-sample STAR reports 
* .pdf figures for each plot contained in the jupyter notebook
* Phyloseq R Library-compatible microbe counts, taxonomic tree, and metadata files for your project
* Microbiome metrics (alpha diversity) for each sample, computed via the skbio.diversity library

