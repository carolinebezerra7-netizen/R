# R scripts for ecological niche modelling of *Pterodon* species in the Cerrado

This repository contains the R scripts used in the study:

**Modeling the potential distribution of species of the genus *Pterodon* (Fabaceae) in the Cerrado in climate change scenarios**, submitted to *Biota Neotropica*.

---
## Description

The scripts provided here reproduce the workflow used for ecological niche modelling (ENM) of *Pterodon* species under current and future climate scenarios.  
All analyses were performed in **R version 4.1.2**, using the **ENMTML** package (Andrade et al., 2020).

# Installing and running the ENMTML package
install.packages (“ENMTML”)
library (ENMTML)
require (ENMTML)
require (raster)

# Define working directory
getwd()
setwd("c:/users/carol/documents/modelagem/ENMTML_")
d_ex <- file.path(getwd())

# Create subfolders
dir.create(file.path(base_dir, "Ocorrencia"), showWarnings = FALSE)
dir.create(file.path(base_dir, "preditores"), showWarnings = FALSE)
dir.create(file.path(base_dir, "projection"), showWarnings = FALSE)

# Occurrence data
data ("oc")
data("oc")
occ_path <- file.path(base_dir, "Ocorrencia", "species.txt")
utils::write.table(oc, occ_path, sep = "\t", row.names = FALSE, quote = FALSE)

# --- Current predictors ---
data("pred")
pred_dir <- file.path(base_dir, "preditores")
raster::writeRaster(pred, filename = file.path(pred_dir, names(pred)),
                    bylayer = TRUE, format = "GTiff", overwrite = TRUE)

# --- Future projections ---
data("projection")
proj_dir <- file.path(base_dir, 'projection/')
proj_names <- names(projection)
proj_paths <- file.path(proj_dir, proj_names)
sapply(proj_paths, dir.create, showWarnings = FALSE)
for (i in seq_along(projection)) {
  this_proj <- projection[[i]]
  this_dir  <- proj_paths[i]
raster::writeRaster(projection$`ssp245_2041_2060`,file.path(d0[1], names(projection$`ssp245_2041_2060`)), bylayer=TRUE, format=“GTiff'”)
raster::writeRaster(projection$`ssp245_2061_2080`,file.path(d0[2], names(projection$`ssp245_2061_2080`)), bylayer=TRUE, format=“GTiff'”)                             
raster::writeRaster(projection$`ssp245_2081_2100`,file.path(d0[3], names(projection$`ssp245_2081_2100`)), bylayer=TRUE, format=“GTiff'”)
raster::writeRaster(projection$`ssp585_2041_2060`,file.path(d0[4], names(projection$`ssp585_2041_2060`)), bylayer=TRUE, format=“GTiff'”)
raster::writeRaster(projection$`ssp585_2061_2080`,file.path(d0[5], names(projection$`ssp585_2061_2080`)), bylayer=TRUE, format=“GTiff'”)                      
raster::writeRaster(projection$`ssp585_2081_2100`,file.path(d0[6], names(projection$`ssp585_2081_2100`)), bylayer=TRUE, format=“GTiff'”)

                
# --- Run ENMTML ---
ENMTML(pred_dir = d_preditores, proj_dir = d_fut, result_dir = NULL, occ_file = d_oc, sp = 'species', x = 'x', y = 'y', min_occ = 10, thin_occ = c(method='USER-DEFINED', distance='5'), eval_occ = NULL, colin_var = c(method='PCA'), imp_var = FALSE, sp_accessible_area = NULL, pseudoabs_method = c(method='GEO_ENV_KM_CONST', width='50'), pres_abs_ratio = 1, part=c(method= 'KFOLD', folds='5'), save_part = FALSE, save_final = TRUE, algorithm = c('BIO', 'DOM', 'MXS', 'SVM', 'RDF'), thr = c(type='MAX_TSS'), msdm = NULL, ensemble = c(method='PCA'), extrapolation = FALSE, cores = 1)


- `00_install_packages.R` — installs and loads all required R packages.  
- `01_run_ENMTML.R` — performs data preparation, climate projections, and model execution.

---

## Requirements

R (≥ 4.1.2)

Required packages:
```r
install.packages(c("ENMTML", "raster", "utils"))




## Data availability

Occurrence data: compiled from SpeciesLink and GBIF (as cited in the manuscript).

Environmental predictors: derived from WorldClim v2 and SoilGrids.

Future scenarios: CMIP6 datasets for SSP2-4.5 and SSP5-8.5, using ENMTML example projections.

## Repository link

GitHub: https://github.com/carolinebezerra7-netizen/R


## License

This repository is shared under the Creative Commons Attribution 4.0 International (CC-BY-4.0) license.
You are free to reuse or adapt the code with proper citation.


Andrade, A.F.A.D., Velazco, S.J.E., & De Marco Jr., P. (2020). ENMTML: An R package for a straightforward construction of complex ecological niche models. Environmental Modelling & Software, 125, 104615. https://doi.org/10.1016/j.envsoft.2019.104615

Title: R scripts for ecological niche modelling of Pterodon species in the Cerrado under climate change scenarios
Authors: Regivan Antonio de Saul; Samuel Freitas de Souza; Maria Teresa Gomes Lopes; Caroline de Souza Bezerra; Jennifer Souza Tomaz; Maria José Marques; Ananda Virginia de Aguiar; Francieli Alves Caldeira Saul; Alexandre Marques da Silva; Mario Luiz Teixeira de Moraes
Description: R scripts used for running the ENMTML modelling of Pterodon species under current and future climate scenarios (SSP2-4.5 and SSP5-8.5) for the manuscript submitted to Biota Neotropica.
Keywords: ENMTML, species distribution modelling, Cerrado, Pterodon, R script, climate change
License: CC-BY-4.0

---
















