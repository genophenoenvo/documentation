# Documentation

We started with environmental data and phenotype and genotype data files from TERRA-REF.  

## Genomic Data

The documentation for the genomic data is [here](https://docs.terraref.org/experimental-design/experimental-design-genomics).
There are HapMap files and [VCF files](https://datacommons.cyverse.org/browse/iplant/home/shared/terraref/genomics/derived_data/bap/resequencing/danforth_center/version1/gvcf) available. The difference between VCF and HapMap files is explained [here](http://augustogarcia.me/statgen-esalq/Hapmap-and-VCF-formats-and-its-integration-with-onemap/). The HapMap file was [downloaded from Cyverse](https://datacommons.cyverse.org/browse/iplant/home/shared/terraref/genomics/derived_data/bap/resequencing/danforth_center/version1/hapmap). The initial decision to use HapMap instead of VCF was likely due to the convenience of already having one HapMap file. The VCF files need to be concatenated. The genotype data contain information on X cultivars.

The HapMap file and the phenotype [file](https://docs.google.com/spreadsheets/d/1wxPZUNe6-2DxEYNpklahUOScweRmuiV9Vc0ax6JWFLY/edit#gid=1382556769) was used with [Tassel](https://www.maizegenetics.net/tassel) to find the relevant SNPs (rows in the HapMap file) using GWAS. The result of the GWAS is [here](https://data.monarchinitiative.org/tassel5/). The hapmap-slim.vcf file contains only the SNPs that were found to be correlated to the phenotypes of interest by the GWAS.

The knowledge graphs at Monarch, Gramene, and Planteome were queried to find genes that impact the phenotypes of interest. The knowledge graphs were queried using ontology terms that mapped to the phenotypes [here](https://docs.google.com/spreadsheets/d/1VZRN38Sf4j57SBtkJQIX7zQV4sYXahw7eCaJqYNzC0c/edit#gid=2033025260) and additional related GO terms. The results of these queries are [here](https://docs.google.com/spreadsheets/d/1ugMisjghvSfa0W_TPhA-0_6C8A0X-gwOqPZbzqjJOrg/edit#gid=0). We used Gramene [biomart](http://ensembl.gramene.org/biomart/martview/892190680828bd6ce88eb424dda517cf) to find Sorghum orthologs for Arabidopsis genes that were identified as potentially relevant by Monarch. Additionally, we used the flowering time pathway for Arabidopsis in [WikiPathways](https://www.wikipathways.org/index.php/Pathway:WP2312) to identify more relevant genes. There is much less data for the other phenotypes. Instructions for using Gramene Biomart are [here](https://docs.google.com/presentation/d/1_nwQBiHmgFad7lwwlN_Hqq9WD_ukRSm-21NMX4YRyps/edit#slide=id.p).

The ML will use the complete file, the file filtered by GWAS, and the file filtered by the knowledge graph queries. We will compare the predictive power of each.

## Phenotype Data

The phenotype data was transformed into this [file](https://docs.google.com/spreadsheets/d/1wxPZUNe6-2DxEYNpklahUOScweRmuiV9Vc0ax6JWFLY/edit#gid=1382556769) for use in the ML model and this file for GWAS. Phenotypes were mapped to ontology terms  

Genes relevant for the phenotypes of interest were found using Gramene and are [here](https://docs.google.com/spreadsheets/d/1ugMisjghvSfa0W_TPhA-0_6C8A0X-gwOqPZbzqjJOrg/edit#gid=0).

Initial phenotypes for ML are:
* GDD to flowering
* GDD to flagleaf emergence
* End of season canopy height
* End of season above ground dry biomass

Initial environmental parameters are:
* Row and column position
* Soil - maybe

The weather parameters we have are below, but are from a nearby weather station, so are not different for each cultivar.
* Air temperature
* Relative humidity
* GDD
* Wind speed and direction
* Precipitation

# Outstanding Questions and Issues

Can we get the VCF files concatenated?

We need more data. What should we prioritize?

We need to filter the genotype data file based on the KG query.
