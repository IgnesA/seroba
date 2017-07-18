# SeroBA
SeroBA is a k-mer based Pipeline to identify the Serotype from Illumina NGS reads for given references. You can use SeroBA to download references from (https://github.com/phe-bioinformatics/PneumoCaT) to do identify the capsular type of Streptococcus pneumoniae.
## Usage
```
usage: seroba  getPneumocat out_dir

Downloads PneumoCat and build an tsv formatted meta data file out of it

positional arguments:
  out_dir      directory to store the PneumoCats capsular type variant (CTV) database


usage: seroba createDBs  <database dir> <meta data tsv>

Creates a Database for kmc and ariba

positional arguments:
    out_dir     output directory for kmc and ariba Database
    kmer_size   kmer_size zou want to use for kmc , recommended = 71

    usage: seroba runSerotyping [options]  <databases directory> <read1> <read2> <prefix>

    identify serotype of your input data

    positional arguments:
      databases          path to database directory
      read1              forward read file
      read2              backward read file
      prefix             unique prefix

    optional arguments:
      -h, --help         show this help message and exit

    Other options:
      --noclean NOCLEAN  Do not clean up intermediate files (assemblies, ariba
                         report)


Summaries the output in one tsv file

usage: seroba summary  <output folder>

positional arguments:
  output folder   directory where the output directories from seroba runSerotyping are stored


```   

## Output
In the folder 'prefix' you will find a pred.tsv including your predicted serotype
as well as en file called detailed_serogroup_info.txt including information about
snps, genes, and alleles that are found in your reads.
After the use of "seroba summary" a tsv file called summary.tsv is created that
consists of two columns (sample Id , serotype).

## Database
You can use the CTV von PneumoCat by using seroba  getPneumocat. It is also
possible so add new serotypes by adding the references sequence to the
"references.fasta" file in the database folder. Out of  the information provided
 by this database a TSV file is created while using seroba createDBs. You can
 easily put in additional genetic information for any of these serotypes in the
 given format.

## Installation

### Debian Testing/Ubuntu 16.04 (Xenial)

SeroBA has the following dependencies, which need to be installed:
  * [Python3][python] version >= 3.3.2
  * [KMC][kmc] version >= 3.0
  * [KMC_tools][kmc_tools] version >= 3.0
  * [MUMmer][mummer] version >= 3.1

If this dependencies are installed, you can download the latest release from this github repository,or clone the repository.
Then run the tests:

    python3 setup.py test

If the tests all pass, install:

    python3 setup.py install

# Linux/OSX/Windows/Cloud
## Docker
Install [Docker](https://www.docker.com/).  We have a docker container which gets automatically built from the latest version of SeroBA. To install it:

```
docker pull sangerpathogens/seroba
```
To use it you would use a command such as this (substituting in your directories), where your files are assumed to be stored in /home/ubuntu/data:
```
docker run --rm -it -v /home/ubuntu/data:/data sangerpathogens/seroba seroba runSerotyping seroba/database /data/read_1.fastq.gz /data/read_2.fastq.gz  /data/output_folder
```    
