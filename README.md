# LCA-Philippines-Diagnostics
This repository contains the code and figures generated by the Latent-Class Analysis (LCA) discussed in the paper *Reassessing The Use of Microscopy-Based Techniques*, by Vachel Gay V. Paller, Allen Jethro I. Alonte, Billy P. Divina, Frederick T. A. Freeth, Sheina Macy P. Manalo, Joaquin M. Prada, Martha Betson, and Vicente Y. Belizario Jr.

## Data:
```Comparison Data_Humans.xlsx``` and ```Comparison Data_Animals.xlsx``` contain the data used for the analysis. It contains binary data for the status of a host. In animals, 1 denotes the host being infected with a zero implying undetectable levels of infection. For humans, this is indexed as 2 and 1 respectively and is coerced to 1 and 0 in the R script.

## Algorithms and Supplementary Figures:
The file ```LatentClassAnalysisFTAF.R``` contains the source code that generates the results. It will automatically produce the figures and organise them by host and parasite. These figures are not included in the main publication. For each host, parasite and diagnostic:
 - ```<Parasite>_<Host>_Estimated_Probability_of_Infection.svg```: A histogram of how many hosts have a given probability of being 
 - ```<Parasite>_<Host>_Prevalence.svg```: A histogram of the prevalences across all the samples of the JAGS model.
 - ```<Parasite>_<Host>_Sensitivity.svg```: A density curve of the Sensitivties of each diagnostic.
 - ```<Parasite>_<Host>_Shape_Rate.svg```: Density curves of the shape (```sh```) and rate (```rt```) parameters of the JAGS model.
 - ```<Parasite>_<Host>_Specificity.svg```: A density curve of the specificities of each diagnostic.

Note: When running the code generating the figures ```Prevalence_Real_Sim_All_Hosts.svg``` and ```Sensitivity_Prevalence_All_Hosts.svg```, please ensure the plotting window is large.

## Main Results and Figures:
- ```analysisHuman.csv```, ```analysisCats_and_Dogs.csv```, ```analysisPigs.csv```, and ```analysisWater_Buffalo_and_Cattle.csv``` contain the diagnostic sensitivity data generated by each diagnostic for each parasite, along with the prevalence data for each parasite generated by the JAGS model for each host.
 - ```Prevalence_Real_Sim_All_Hosts.svg``` is the plot of the simulated prevalence of each parasite compared with the prevalence recorded in the real-world. Each host is arranged in a two-by-two grid with all diagnostics plotted together.
 - ```Sensitivity_Prevalence_All_Hosts.svg``` is the plot of the simulated sensitivites and prevalences of the JAGS model. Each host is arranged in a two-by-two grid, with all diagnostics plotted together.

## Session Info:
The R version and used packages are displayed below:
```
R version 4.2.1 (2022-06-23 ucrt)
Platform: x86_64-w64-mingw32/x64 (64-bit)
Running under: Windows 10 x64 (build 19045)

Matrix products: default

locale:
[1] LC_COLLATE=English_United Kingdom.utf8  LC_CTYPE=English_United Kingdom.utf8   
[3] LC_MONETARY=English_United Kingdom.utf8 LC_NUMERIC=C                           
[5] LC_TIME=English_United Kingdom.utf8    

attached base packages:
[1] compiler  stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
 [1] rstudioapi_0.14 MCMCpack_1.6-3  MASS_7.3-57     ggplot2_3.3.6  
 [5] runjags_2.2.1-7 Rmisc_1.5.1     plyr_1.8.7      lattice_0.20-45
 [9] rjags_4-13      coda_0.19-4    

loaded via a namespace (and not attached):
 [1] Rcpp_1.0.9         cellranger_1.1.0   pillar_1.8.1       tools_4.2.1       
 [5] lifecycle_1.0.1    tibble_3.1.8       gtable_0.3.1       viridisLite_0.4.1 
 [9] pkgconfig_2.0.3    rlang_1.0.5        Matrix_1.4-1       cli_3.3.0         
[13] DBI_1.1.3          parallel_4.2.1     SparseM_1.81       withr_2.5.0       
[17] dplyr_1.0.10       MatrixModels_0.5-0 generics_0.1.3     vctrs_0.4.1       
[21] grid_4.2.1         cowplot_1.1.1      tidyselect_1.1.2   glue_1.6.2        
[25] R6_2.5.1           fansi_1.0.3        survival_3.3-1     readxl_1.4.1      
[29] purrr_0.3.4        magrittr_2.0.3     splines_4.2.1      mcmc_0.9-7        
[33] scales_1.2.1       assertthat_0.2.1   colorspace_2.0-3   quantreg_5.94     
[37] utf8_1.2.2         munsell_0.5.0
```
