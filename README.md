# BIOC-3301
This repository contains batch scripts used to submit to Cirrus HPC for the analysis of Illumina MiSeq soil microbiome sequencing data using QIIME 1.9.1. The resulting data can be used to provide information on diversity and abundance of specific groups of phyla for both Greengenes and SILVA reference databases.

Datasets for this year's Soil collection data were uploaded to High performance Cluster Cirrus and processed according to the bash scripts shown for both reference databases, Greengenes and SILVA

The files contain several lines of codes starting with #, which are instructions for the HPC job queue. Such as how long the job will run on how many cores, how much RAM and storage is required.

The data for 2017-2018 had both reads joined, prior to de-multiplexing.

After picking OTUs with the Greengenes reference the BIOM-formatted tables were merged with the command in merge_otu_tables.sh. This was repeated later with the SILVA reference database.

QIIME Analysis Workflow

1) Validate mapping file - Remember to delete spaces in mapping file
2) Joining reads together - Set parameters for overlap
3) Splitting libraries and Demultiplexing using mapping file and joined reads
4) Making OTU table using slout sequence file and for Greengenes reference database) (Repeat for SILVA analysis with SILVA reference database)
5) Filter OTU table to remove the sample with the lowest counts
6) Use OTU table to do alpha/beta diversity analysis and filtered mapping file
7) Other statistical analysis and tests

The scripts should be carried out in the following order:
1. Joining Reads - Joins Read1 and Read2 sequencing data to create one file for use in subsequent analysis
2. Split libraries - Carries out barcode assignment and quality filtering of samples
3. Counting and Picking OTU - Used Closed Reference OTU picking method for both Greengenes and SILVA 128 release databases and  97% similarity to output a biom table for subsequent analyses
4. Core diversity analysis - Carries out core diversity analysis of the final biom table to output taxa summaries, alpha diversity and beta diversity metrics
5. Summarize Taxa - The summarize_taxa.py script provides summary information of the representation of taxonomic groups within each sample. It takes an OTU table that contains taxonomic information as input. The taxonomic level for which the summary information is provided is designated with the -L option. The meaning of this level will depend on the format of the taxon strings that are returned from the taxonomy assignment step. The taxonomy strings that are most useful are those that standardize the taxonomic level with the depth in the taxonomic strings. For instance, the Greengenes database uses the following levels: Level 1 = Kingdom (e.g. Bacteria), Level 2 = Phylum (e.g. Actinobacteria), Level 3 = Class (e.g. Actinobacteria), Level 4 = Order (e.g. Actinomycetales), Level 5 = Family (e.g. Streptomycetaceae), Level 6 = Genus (e.g. Streptomyces), Level 7 = Species (e.g. mirabilis).
6. Compare Taxa - This script compares two taxa summary files by computing the correlation coefficient between pairs of samples. This script is also useful for sorting and filling taxa summary files so that each sample has the same taxa listed in the same order (with missing taxa reporting an abundance of zero). The sorted and filled taxa summary files can then be passed to a script, such as plot_taxa_summary.py, to visually compare the differences using the same taxa colouring scheme.
7. Plot Taxa - This script automates the construction of pie, bar and area charts showing the breakdown of taxonomy by given levels. The script creates an html file for each chart type for easy visualization. It uses the taxonomy or category counts from summarize_taxa.py for combined samples by level.
8. Statistical Tests can then be carried out, for the purpose of Comparing the two reference databases, the stats tests were not required to run as a script as they did not require the mapping file. However, for hypotheses which compare the generated data to various categories in the mapping file such as pH, the compare_categories.py script could be used to analyse statistical significance of sample groupings using distance matrices.
