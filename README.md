# BIOC-3301
Datasets for this year's Soil collection data were uploaded to High performance Cluster Cirrus and processed according to the bash scripts "3301 shown for both reference databases, Greengenes and SILVA

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
1. Joining Reads
2. Split libraries
3. Counting and Picking OTU
4 Core diversity analysis 
5. Summarize Taxa
6. Compare Taxa
7. Plot Taxa
8. Statistical Tests can then be carried out, for the purpose of Comparing the two reference databases, the stats test were not required to run as a script as they did not require the mapping file. However, for hypotheses which compare the gnerated data to various categories in the mapping file such as pH, the compare_categories.py script could be used to analyse statistical significance of sample groupings using distance matrices.
