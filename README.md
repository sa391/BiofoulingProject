# Biofouling of Solar Panels
## IBIEM 2020 Project

This document will provide a guide to the steps performed by this research group to analyze the microbiome of biofilms swabbed from solar panel glass.


# Computing Environment
To replicate this analysis, a Docker container can be downloaded from [Docker Hub](https://hub.docker.com/r/ibiem/docker_rstudio_ibiem2020) using the command `docker pull ibiem/docker_rstudio_ibiem2020:2020_v004` (using Docker) or `singularity pull docker://ibiem/docker_rstudio_ibiem2020:2020_v004` (using Singularity).

# Code
## Git Repository
You will need to clone the project's git repository.  The [repository](https://github.com/sa391/BiofoulingProject) is available to clone using: `git clone https://github.com/sa391/BiofoulingProject.git`.

## Run 
Run the Rmarkdown `AMKIBIEMProject.rmd` (in the Docker image described above) to automatically download the data, taxonomic references, and run the full analysis pipeline.  Further detail on each step performed in the analysis is described within the Rmarkdown file.  Multiple plots are produced by the pipeline to allow visual inspection of the results.

The final phyloseq file produced by this project is available for comparison or further analysis without need to rerun the pipeline.  See `Final_Phyloseq.rds`.

### Data
The data used in this analysis is composed of full-length 16S PacBio reads.  The pipeline described above performs an additional trimming step in order to facilitate comparison of full-length reads to the V4 region only.

The unaltered FASTQ and mapping files are available within the IBIEM 2020 container.  The filepath is:
`/data/project_data/biofouling_pacbio`

### Taxonomy References
This pipeline utilizes the Silva v132 16S rRNA database to assign taxonomy. To download the version of the database formatted for DADA2 `assignTaxonomy`, use the following URLs:

1. https://zenodo.org/record/1172783/files/silva_nr_v132_train_set.fa.gz
2. https://zenodo.org/record/1172783/files/silva_species_assignment_v132.fa.gz

For the final phyloseq object provided with this repository, reads left unassigned after referencing the Silva database were run against the NCBI BLAST blastn database.  If a match was identified, the taxonomy data was added to the phyloseq file.