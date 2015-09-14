## Annotation pipeline

Variant annotation pipeline using ANNOVAR, and a toolbox of variant-table manipulation scripts.

Version: 0.1
Authors: Paweł Sztromwasser

### annotation_pipeline.py

The script for orchestrating simultanous VCF annotation using ANNOVAR. Annotats variants with location (gene, exon, intron), effect on protein (synonymous, nonsynonymous, stopgain), 
and various pathogenicity scores (OMIM, PolyPhen, CADD). 


*   Running the script

    If you run the script (./annotation_pipeline.py) a list of possible options will be presented. 
    The only required option is `--pipeline_settings`, which accepts a config file with paths to input VCF files and necessary resources (e.g. ANNOVAR paths, databases, etc). 
    See an exemplary file (pipeline_settings.cfg) for all possible options.  
  
  	To test the script before running it, append the `-n` option.
  	If you want to follow progress of the script, adjust verbosity level by adding or removing v's from (`-vvvv`).
    In order to use multithreading, use the `-j` option (`-j 12`).

*   Outputs

    The script will create annotated-with-annovar directory in the current folder.
  	Inside, there are lists of variants for every sample, filtered on multiple levels (1000 Genomes, inhouse db, coding etc).
  	In annotated-with-annovar/annotated-table, comma separated (.csv) tables of annotated variants are placed. 
	To convert csv files to tab-separated files, use the format_variant_table.sh script.

*   Typical usage

    For running the genotyping analysis using 12 cpus:

	mkdir ~/results/new_project
	cd ~/results/new_project
	git clone -depth 1 https://github.com/seru71/annotation-pipeline.git annotation-pipeline
	cp annotation-pipeline/pipeline_settings.cfg .
	vi pipeline_settings.cfg  	# insert correct paths to the bam files, ref genome, executables, etc.
	annotation-pipeline/annotation-pipeline.py -s pipeline_settings.cfg -t extract_recessive_disorder_candidates -vvv -j 12


### format_variant_table.sh

Formats the .csv annovar annotated table into a tab-delimited .tsv file.
Usage:
	TBD

### geneset_hits_in_variant_table.py

TBD

### variant_table_overlap.sh

TBD






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






