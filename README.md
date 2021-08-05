# Documentation

In year 1, we started with environmental data and phenotype and genotype data files from TERRA-REF and later added data from KSU and Clemson. We developed ML/statistical models and a Bayesian Belief Network for making predictions. 

In year 2, we found an excellent cottonwood and corn data set. We are currently exploring those data sets to see if they are large enough to train a neural network. We starting collaborating with the Dogwood Genome Project to examine NPN data from the same dogwood clone and to sequence additional clones. We investigated the possibility of applying the sorghum-trained model on Sorghastrum, a wild relative of sorghum with data in NPN, but there were not enough data points. 

## Genomic Data
### Sorghum
The documentation for the genomic data is [here](https://docs.terraref.org/experimental-design/experimental-design-genomics).
There are HapMap files and [VCF files](https://datacommons.cyverse.org/browse/iplant/home/shared/terraref/genomics/derived_data/bap/resequencing/danforth_center/version1/gvcf) available. The difference between VCF and HapMap files is explained [here](http://augustogarcia.me/statgen-esalq/Hapmap-and-VCF-formats-and-its-integration-with-onemap/). The HapMap file was [downloaded from Cyverse](https://datacommons.cyverse.org/browse/iplant/home/shared/terraref/genomics/derived_data/bap/resequencing/danforth_center/version1/hapmap). The initial decision to use HapMap instead of VCF was likely due to the convenience of already having one HapMap file. The VCF files need to be concatenated. The genotype data contain information on X cultivars. 

The HapMap file and the phenotype [file](https://docs.google.com/spreadsheets/d/1wxPZUNe6-2DxEYNpklahUOScweRmuiV9Vc0ax6JWFLY/edit#gid=1382556769) was used with [Tassel](https://www.maizegenetics.net/tassel) to find the relevant SNPs (rows in the HapMap file) using GWAS. The result of the GWAS is [here](https://data.monarchinitiative.org/tassel5/). The hapmap-slim.vcf file contains only the SNPs that were found to be correlated to the phenotypes of interest by the GWAS. The results with the HapMap file did not contain any information about heterozygosity, so we decided to use the VCF files even though they had to be concatenated first.

The VCF files were concatenated and can be found [here](https://data.monarchinitiative.org/genophenoenvo/vcf/). These files were exported to Tassel for GWAS. The output can be found [here](https://data.monarchinitiative.org/genophenoenvo/tassel5/). The GWAS was used to filter the concatenated VCF file to the "Slim VCF" file that contains only the genes that the GWAS found to be useful for the phenotypes of interest. The Slim VCF was used to create a distance matrix for ML input. Unfortunately, this data did not improve the performance of the algorithms. We suspected that was because the cultivars were so closely related, that this distance matrix was not capturing useful genomic features. More information about this approach can be found [here](https://github.com/genophenoenvo/genomic_data/tree/master/GenomicApproachPrediction).

After this result, we decided to go back to the VCF files and explore creating a distance matrix based on information theory rather than genomics. Documentation for this work can be found [here](https://github.com/genophenoenvo/genomic_data/tree/master/FriendsOfEntropy) and [here](https://gist.github.com/TomConlin/6d38f8795add0230566456498164a63b). First, The VCF files were filtered to remove SNPs that were identical to the reference sorghum genome. The SNPs were filtered down by alternately filtered for the SNPs that are most informative and filtering out cultivars that don't have enough data. The filtering process produced a matrix of jaccard distances for the ML. This matrix worked better, but still not as well as we would like. Now we will remove all cultivars from the genomic data set that don't have data in the phenotype data set.

The knowledge graphs at Monarch, Gramene, and Planteome were queried to find genes that impact the phenotypes of interest. The knowledge graphs were queried using ontology terms that mapped to the phenotypes [here](https://docs.google.com/spreadsheets/d/1VZRN38Sf4j57SBtkJQIX7zQV4sYXahw7eCaJqYNzC0c/edit#gid=2033025260) and additional related GO terms. The results of these queries are [here](https://docs.google.com/spreadsheets/d/1ugMisjghvSfa0W_TPhA-0_6C8A0X-gwOqPZbzqjJOrg/edit#gid=0). We used Gramene [biomart](http://ensembl.gramene.org/biomart/martview/892190680828bd6ce88eb424dda517cf) to find Sorghum orthologs for Arabidopsis genes that were identified as potentially relevant by Monarch. Additionally, we used the flowering time pathway for Arabidopsis in [WikiPathways](https://www.wikipathways.org/index.php/Pathway:WP2312) to identify more relevant genes. There is much less data for the other phenotypes. Instructions for using Gramene Biomart are [here](https://docs.google.com/presentation/d/1_nwQBiHmgFad7lwwlN_Hqq9WD_ukRSm-21NMX4YRyps/edit#slide=id.p). When looking at the SNPs of interest using information theory, we looked to see if any of the genes are also present in the knowledge graph queries. there were very few - perhaps seven. We anticpate that the KG queries will become more relevant when we start examining more species.

After a discussion with Addie Thompson at MSU (in July 2021), we realized we took the wrong approach with the gene data. We will now repeat the gene data manipulations for the sorghum files with different parameters for the GWAS analysis. We will also convert the entirety of the VCF file into a matrix instead of relying on filtered data.
### Dogwood
The dogwood genome is available [here](https://genomevolution.org/coge/SearchResults.pl?s=Cornus%20florida&p=genome) for the appalachian spring cultivar. Our plan is to look at NPN data from the same cultivar (see this [project](https://www.usanpn.org/nn/cloned-dogwoods)) in different environments. We are collaborating with the Dogwood Genome Project to sequence additional dogwood cultivars with NPN data in the same environment for comparison.
### Black cottonwood
Populus trichocarpa has been the subject of research by the Dept of Energy, especially at the Oak Ridge National Laboratory, for decades. There is a large data set of phenotypes from sequenced trees collected over decades. We are collaborating with this research group to prepare these data for ML training. So far, it looks like we have data from about 1200 cultivars. The genomic and phenotype data are being processed.
### Corn
We have become aware of the large [Genomes2Fields](https://www.genomes2fields.org/) data set and are examining it to see if it is large enough to train a neural network.

## Phenotype Data
### Sorghum
The phenotype data was transformed into this [file](https://docs.google.com/spreadsheets/d/1wxPZUNe6-2DxEYNpklahUOScweRmuiV9Vc0ax6JWFLY/edit#gid=1382556769) for use in the ML model and this file for GWAS. Phenotypes were mapped to ontology terms. The phenotype data were obtained from TERRA-REF using the Traits R package. This includes the Arizona, KSU, and Clemson data. 

Genes relevant for the phenotypes of interest were found using Gramene and are [here](https://docs.google.com/spreadsheets/d/1ugMisjghvSfa0W_TPhA-0_6C8A0X-gwOqPZbzqjJOrg/edit#gid=0).

Phenotypes for ML are:
* GDD to flowering
* GDD to flagleaf emergence
* End of season canopy height
* End of season above ground dry biomass

The code used to prepare the phenotype data are currently being refactored to create a "story notebook" that contains the data, the code, and documentation.

## Environment Data
### Sorghum
Environmental parameters are:
* Row and column position
* Soil
* Air temperature
* Relative humidity
* GDD
* Wind speed and direction
* Precipitation

## Bayesian Belief Network
The documentation for the Bayesian Belief Network can be found in its repo.
https://github.com/genophenoenvo/phenophasebbn

## Machine Learning
The machine learning team used the phenotype, genomic, and environment data to train and test a model to predict flowering time, canopy height, and flag leaf emergence. This work is described [here](https://github.com/genophenoenvo/Machine-Learning).

# Knowledge Graph
A graph was created by combining the Gene Ontology, the Plant Trait Ontology, the Plant Ontology, NCBITaxon, and Planteome using the KG-Hub code. The Planteome data used included gene, ortholog, QTL, and germplasm data for Sorghum bicolor, Zea mays, Oryza sativa, Populus trichocarpa, and Arabidopsis thaliana. The code for constructing the graph is [here](https://github.com/diatomsRcool/eco-kg). The lastest version of the graph is [here](https://github.com/genophenoenvo/knowledge-graph).

# Outstanding Questions and Issues

