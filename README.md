#27 April 2021
# ENM-Bovidae
#code for create ENM of wild Bovidae using package ENMTML (link: https://github.com/andrefaa/ENMTML) 
  #Bos gaurus, Bos javanicus, Bubalus arnee, Capricornis sumatraensis, Naemorhedus griseus
#ENMTML
# R version 4.0.2 
# install.packages("devtools")  
#install new version from GITHUB
if (!"devtools"%in%installed.packages()){install.packages("devtools")}  
devtools::install_github("andrefaa/ENMTML")  
remotes::install_github('jmarshallnz/ENMTML', ref='no_parallel')

#remove objects
rm(list = ls(all.names = T))
gc()

library(devtools)  
library(ENMTML) #"BIO","MAH","DOM","ENF","MXS","MXD","SVM","GLM","GAM","BRT","RDF", "MLK","GAU"
library(rstan)
library(raster)
library(plyr)
library(dplyr)


#create path
path<-"D:/enmtml" #Bovidae
setwd(path)
getwd()
dir()
d_ex <- file.path(getwd())
d_ex

#--------------------------
#1) Gaur (Bos gaurus)

#species occurrence data (species,x,y)
d_occ<- file.path(d_ex, 'gaur01252021.txt')

# bioclimatic variables for current conditions
d_env <- file.path(d_ex, 'envgaur')
dir(d_env) #bio1-19,+/-slope, elev,hpop_log,land_cgls2015,ndvi,waterG3W

ENMTML(pred_dir = d_env, 
       proj_dir = NULL, 
       result_dir = NULL, 
       occ_file = d_occ,
       sp = 'species', 
       x = 'x', 
       y = 'y', 
       min_occ = 10,
       thin_occ=c(method='CELLSIZE'),
       eval_occ = NULL, 
       colin_var=c(method ='PCA'), 
       imp_var = FALSE, 
       #add shapefile path for accessible area
       sp_accessible_area = c(method= 'MASK', 
          filepath='/Users/whorpien/OneDrive - Massey University/R/enmtml/accgaur/wwf_eco_gaur_dissolve17082020.shp'),
       pseudoabs_method = c(method= 'RND'),    
       pres_abs_ratio = 1, 
       part = c(method='BOOT', replicates='10', proportion='0.75'),
       save_part = FALSE, 
       save_final = TRUE,
       algorithm = c("BIO","GLM","GAM","SVM","RDF","MXD","MLK","GAU"),      #algorithyms for creating ensembles
       thr=c(type=c('LPT', 'MAX_TSS', 'MAX_KAPPA','JACCARD','SORENSEN')), 
       msdm = NULL,
       ensemble=c(method=c('MEAN','W_MEAN', 'PCA','SUP'), metric='TSS'), 
       extrapolation = FALSE, 
       cores = 2)
#==============================

#2) Banteng (Bos javanicus)

#species occurrence data (species,x,y)
d_occ<- file.path(d_ex, 'banteng_tot02122020.txt')

# bioclimatic variables for current conditions
d_env <- file.path(d_ex, 'env_banteng_is')
dir(d_env)

ENMTML(pred_dir = d_env, 
       proj_dir = NULL, 
       result_dir = NULL, 
       occ_file = d_occ,
       sp = 'species', 
       x = 'x', 
       y = 'y', 
       min_occ = 10,
       thin_occ=c(method='CELLSIZE'),
       eval_occ = NULL, 
       colin_var=c(method ='PCA'), 
       imp_var = FALSE, 
       sp_accessible_area = c(method= 'MASK', 
          filepath='D:/enmtml/acc_banteng/wwf_banteng_dissolve01102020.shp'),
       pseudoabs_method = c(method= 'RND'),    
       pres_abs_ratio = 1, 
       part = c(method='BOOT', replicates='10', proportion='0.75'),
       save_part = FALSE, 
       save_final = TRUE,
       algorithm = c("BIO","GLM","GAM","SVM","RDF","MXD","MLK","GAU"), 
       thr=c(type=c('LPT', 'MAX_TSS', 'MAX_KAPPA','JACCARD','SORENSEN')), 
       msdm = NULL,
       ensemble=c(method=c('MEAN','W_MEAN', 'PCA','SUP'), metric='TSS'),
       extrapolation = FALSE, 
       cores = 2)

#==============================
#3) Buffalo
#species occurrence data (species,x,y)
d_occ<- file.path(d_ex, 'buffalo_tot09112020.txt')

# bioclimatic variables for current conditions
d_env <- file.path(d_ex, 'env_buffalo_corr')
dir(d_env)

ENMTML(pred_dir = d_env, 
       proj_dir = NULL, 
       result_dir = NULL, 
       occ_file = d_occ,
       sp = 'species', 
       x = 'x', 
       y = 'y', 
       min_occ = 10,
       thin_occ=c(method='CELLSIZE'),
       eval_occ = NULL, 
       colin_var=c(method ='PCA'), 
       imp_var = FALSE, 
       sp_accessible_area = c(method= 'MASK', filepath='D:/enmtml/acc_buffalo/buffalo_wwfeco_iucn02112020-2.shp'),
       pseudoabs_method = c(method= 'RND'),    
       pres_abs_ratio = 1, 
       part = c(method='BOOT', replicates='10', proportion='0.75'),
       save_part = FALSE, 
       save_final = TRUE,
       algorithm = c("BIO","GLM","GAM","SVM","RDF","MXD","MLK","GAU"), 
       thr=c(type=c('LPT', 'MAX_TSS', 'MAX_KAPPA','JACCARD','SORENSEN')), 
       msdm = NULL,
       ensemble=c(method=c('MEAN','W_MEAN', 'PCA','SUP'), metric='TSS'),
       extrapolation = FALSE, 
       cores = 2)

#==============================
#4)mainland serow
#species occurrence data (species,x,y)
d_occ<- file.path(d_ex, 'serow_tot27102020_rmIndo.txt')

# bioclimatic variables for current conditions
d_env <- file.path(d_ex, 'env_thar')
dir(d_env)

ENMTML(pred_dir = d_env, 
       proj_dir = NULL, 
       result_dir = NULL, 
       occ_file = d_occ,
       sp = 'species', 
       x = 'x', 
       y = 'y', 
       min_occ = 10,
       thin_occ=c(method='CELLSIZE'),
       eval_occ = NULL, 
       colin_var=c(method ='PCA'), 
       imp_var = FALSE, 
       sp_accessible_area = c(method= 'MASK', filepath='D:/enmtml/acc_serowthar/serow_wwfeco_iucn03112020.shp'),
       pseudoabs_method = c(method= 'RND'),    
       pres_abs_ratio = 1, 
       part = c(method='BOOT', replicates='10', proportion='0.75'),
       save_part = FALSE, 
       save_final = TRUE,
       algorithm = c("BIO","GLM","GAM","SVM","RDF","MXD","MLK","GAU"), 
       thr=c(type=c('LPT', 'MAX_TSS', 'MAX_KAPPA','JACCARD','SORENSEN')), 
       msdm = NULL,
       ensemble=c(method=c('MEAN','W_MEAN', 'PCA','SUP'), metric='TSS'),
       extrapolation = FALSE, 
       cores = 2)
#===============================
#5) goral
#species occurrence data (species,x,y)
d_occ<- file.path(d_ex, 'goral_tot27102020.txt')

# bioclimatic variables for current conditions
d_env <- file.path(d_ex, 'env_goral')
dir(d_env)

ENMTML(pred_dir = d_env, 
       proj_dir = NULL, 
       result_dir = NULL, 
       occ_file = d_occ,
       sp = 'species', 
       x = 'x', 
       y = 'y', 
       min_occ = 10,
       thin_occ=c(method='CELLSIZE'),
       eval_occ = NULL, 
       colin_var=c(method ='PCA'), 
       imp_var = FALSE, 
       sp_accessible_area = c(method= 'MASK', filepath='D:/enmtml/acc_goral/goral_wwf_iucn09112020.shp'),
       pseudoabs_method = c(method= 'RND'),    
       pres_abs_ratio = 1, 
       part = c(method='BOOT', replicates='10', proportion='0.75'),
       save_part = FALSE, 
       save_final = TRUE,
       algorithm = c("BIO","GLM","GAM","SVM","RDF","MXD","MLK","GAU"), 
       thr=c(type=c('LPT', 'MAX_TSS', 'MAX_KAPPA','JACCARD','SORENSEN')), 
       msdm = NULL,
       ensemble=c(method=c('MEAN','W_MEAN', 'PCA','SUP'), metric='TSS'),
       extrapolation = FALSE, 
       cores = 2)
#===============================



