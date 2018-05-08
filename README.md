# BIOC-3301
Datasets for this year's Soil collection data were uploaded to High performance Cluster Cirrus and processed according to the bash scripts 2018_02_smb. The standard output from these scripts is saved in 8 and Baron, respectively.

The files contain several lines of codes starting with #, which are instructions for the HPC job queue. Such as how long the job will run on how many cores, how much RAM and storage is required.

The data for 2017 had both reads joined, prior to de-multiplexing.

After picking OTUs with the Greengenes reference the BIOM-formated tables were merged with the command in merge_otu_tables.sh. This was repeated later with the SILVA reference database.

