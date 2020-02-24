# documentation

We started with phenotype and genotype data files from TERRA-REF. These files were accessed directly from TERRA-REF using code found here for the trait data and here for the geneotype data.

The phenotype data was transformed into this [file](https://docs.google.com/spreadsheets/d/1wxPZUNe6-2DxEYNpklahUOScweRmuiV9Vc0ax6JWFLY/edit#gid=1382556769) for use in the ML model and this file for GWAS. Phenotypes were mapped to ontology terms [here](https://docs.google.com/spreadsheets/d/1VZRN38Sf4j57SBtkJQIX7zQV4sYXahw7eCaJqYNzC0c/edit#gid=2033025260). 

The genotype data is in VCF and HapMap files. Genes relevant for the phenotypes of interest were found using Gramene and are [here](https://docs.google.com/spreadsheets/d/1ugMisjghvSfa0W_TPhA-0_6C8A0X-gwOqPZbzqjJOrg/edit#gid=0).

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

The genotype data contain information on X cultivars.
