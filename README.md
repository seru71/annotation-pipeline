## Pipeline

Variant annotation pipeline using annovar, and a toolbox of variant-table manipulation scripts.

### annotation_pipeline.py

-------------------------------
--------- To be updated -------
-------------------------------


The script for annotating variants with location (gene, exon, intron), effect on protein (synonymous, nonsynonymous, stopgain), 
and various pathogenicity scores (OMIM, PolyPhen, CADD). 


*   Running the script

    You can run the script using `python ~/bin/pipeline_multisample.py`.
    A list of possible options will be presented. The only required option is `--pipeline_settings`,
    which accepts a config file with paths to input bam files, resources (e.g. reference genome, database, capture regions), 
    and right versions of software. See an exemplary file for all required options 
    in ~/tools/ExomeSeqGenotypingPipeline/pipeline_settings.cfg 
  
    If you want to follow progress of the script, use the verbose option (`-vvvvv`).
    In order to use multithreading, use the `-j` option (`-j 12`).

*   Outputs

    The script will create one or more directories in the current folder, named after
    the bam file prefix (`xxx.bam` will create directory `xxx`).

    After finishing a few files will be in that directory, including the cleaned up 
    bam file (`xxx.gatk.bam`), a .gvcf file, some quality control files (e.g. coverage statistics),
    and the vcf file with variants restricted to the exome.

    In the directory where the script is run, additional files will be created with the
    multisample results (`multisample.gatk.vcf` for the multisample snp and indels,
    and `multisample.gatk.analysisReady.exome.vcf` for the variants restricted to the exome bed-file).

*   Typical usage

    For running the genotyping analysis using 12 cpus (half of astrakan).

	mkdir ~/results/new_project
	cd ~/results/new_project
	cp ~/tools/ExomeSeqGenotypigPipeline/pipeline_settings.cfg .
	vi pipeline_settings.cfg  ## insert correct paths to the bam files, ref genome, executables, etc.
	pipeline_multisample.py -s pipeline_settings.cfg -t split_snps -vvvvv -j 12





