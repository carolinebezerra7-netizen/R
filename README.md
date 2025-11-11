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






