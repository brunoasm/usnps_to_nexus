# unlinked_snps_to_nexus.py
A simple script that converts unlinked_snps files produced by [pyRAD](https://github.com/dereneaton/pyrad) to a NEXUS file suitable for SNAPP.

The input file is simply a phylip-formatted alignment in which heterozygous individuals are coded by ambiguities, missing data by N and gaps by -.


## Usage
To show help: 
```bash
python unlinked_snps_to_nexus.py -h
```
To create a nexus file: 
```bash
python unlinked_snps_to_nexus input_file
```
To create a nexus file and add populations to sample names: 
```bash
python unlinked_snps_to_nexus input_file -p pop_file.csv
```

To create a nexus file, add populations to sample names and filter loci that are not present in all populations: 
```bash
python unlinked_snps_to_nexus input_file -f -p pop_file.csv
```

### Parameters
* Required: path to input alignment, usually a \*.unlinked_snps file generated by pyRAD
* Optional: 
  * **-p** path to \*.csv file containing population assignments. This file must contain a column named 'sample', with sample names as in the input file, and another named 'population', with population names. All samples in the input file must be in the population table. Other columns in this table are ignored.
In the NEXUS file produced, population will be appended to sample name, separated by underline. In BEAUTi, this can be used to quickly set populations by using button **GUESS**.
  * **-f** remove sites not present in all populations.

## Output
The program outputs a nexus file to the directory in which it is called, with same base name as input file. Sample names will contain populations if a population file is provided.

If any alignment column has more than 2 alleles, a warning is given and this column is ommited from output. The same happens for monomorphic sites.

The most frequent allele in a column is coded as 0, the other allele as 2 and heterozygotes as 1. Ns and -s are converted to ? in the output.

## Required Python libraries.
These libraries need to be installed to use this script:
* [Pandas] (http://pandas.pydata.org)
* [Biopython] (http://biopython.org)

The script was tested using Python 2.7.11. It seems there might be some incompatibilities with Python 3.

