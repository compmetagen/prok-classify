# prok-classify
The directory contains the workflow metashot/prok-classify, a software for assigning objective taxonomic classifications to bacterial and archaeal genomes. The workflow is updated to use [GTDB-Tk](https://github.com/Ecogenomics/GTDBTk) 2.4.0 (latest version as of 2024) and the last release of the Genome Database Taxonomy GTDB (Release 220). 

- [MetaShot Home](https://metashot.github.io/)

## Main features (UPDATED)

- Input: prokaryotic genomes in FASTA format;
- Taxonomic classification using
  [GTDB-TK](https://github.com/Ecogenomics/GTDBTk) version 2.4.0 (**requires
  GTDB reference R220**);
- Filter genomes by domain (Bacteria and Achaea).

## Quick start

1. Install Docker (or Singulariry) and Nextflow (see
   [Dependences](https://metashot.github.io/#dependencies));
1. Download and extract/unzip the GTDB-TK reference data (see
   https://ecogenomics.github.io/GTDBTk/installing/index.html#gtdb-tk-reference-data):
   
   ```bash
   wget https://data.gtdb.ecogenomic.org/releases/release220/220.0/auxillary_files/gtdbtk_package/full_package/gtdbtk_r220_data.tar.gz
   tar -xvzf gtdbtk_r220_data.tar.gz
   ```
1. Start running the analysis:

   ```bash
   nextflow run compmetagen/prok-classify \
     --genomes "data/*.fa" \
     --gtdbtk_db ./release220 \
     --outdir results
   ```

## Parameters
See the file [`nextflow.config`](nextflow.config) for the complete list of
parameters.

## Output
The files and directories listed below will be created in the `results` directory
after the pipeline has finished.

### Main outputs
- `bacteria_summary.tsv`: the GTDB-Tk summary for bacterial genomes
  ([documentation](https://ecogenomics.github.io/GTDBTk/files/summary.tsv.html));
- `archaea_summary.tsv`: the GTDB-Tk summary for archaeal genomes
  ([documentation](https://ecogenomics.github.io/GTDBTk/files/summary.tsv.html));
- `bacteria_genomes`: genomes classified as bacteria by GTDB-Tk;
- `archaea_genomes`: genomes classified as archaea by GTDB-Tk.

### Secondary outputs
- `gtdbtk`: main GTDB-Tk output files
  ([documentation](https://ecogenomics.github.io/GTDBTk/files/index.html)).

## System requirements
Please refer to [System
requirements](https://metashot.github.io/#system-requirements) for the complete
list of system requirements options.[GTDB-Tk](https://github.com/Ecogenomics/GTDBTk) and the Genome Database
Taxonomy GTDB.

- [MetaShot Home](https://metashot.github.io/)
