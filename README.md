# Latent-class Analysis of Parasitic Diagnostic Tests in the Philippines
This repository contains the code and figures generated by the Latent-Class Analysis (LCA) discussed in the paper *Reassessing The Use of Microscopy-Based Techniques*, by Vachel Gay V. Paller, Allen Jethro I. Alonte, Billy P. Divina, **Frederick T. A. Freeth**, Sheina Macy P. Manalo, Joaquin M. Prada, Martha Betson, and Vicente Y. Belizario Jr.

## Data
The files ```Data_Humans.csv``` and ```Data_Animals.csv``` contain the neccessary data used for the analysis. It contains the data for the status of a host. In the animals, ```1``` denotes the host being infected with a ```0``` implying undetectable levels of infection. In humans, raw fecal egg counts have been given.


## Algorithms and Supplementary Figures
The file ```LatentClassAnalysisFTAF.R``` contains the source code that implements the Markov Chain Monte Carlo analysis and produces the results. It also contains the JAGS models for the humans and animals to be run with the data.


## Informative Prior Calibration Data
Informative priors were used to ensure model convergence and minimal autocorrelation between samples. We least-squares fit the 25%, 50% and 75% quantiles of raw egg counts to the shape ```sh``` and rate ```rt``` parameters of a ```gamma``` distribution using R's ```optim()``` function in the ```stats``` package. This ```gamma``` distribution represents the infection intensity experienced by each host and is the parameter ```lambda``` in the JAGS model. The values of these quantiles were sourced from an independent unpublished study. In cases where suitable quantiles for the egg counts were not available, e.g. _S. Japonicum_ across all hosts, the shape and rate parameters for the ```gamma``` distribution were supplied as values predetermined from an unpublished, independent study. The table below summarises the parameters used for each host and diagnostic method.

| Species                  | Ascaris                          | Trichuris                              | Hookworm                             | Schistosomiasis                              |
|--------------------------|----------------------------------|----------------------------------------|--------------------------------------|----------------------------------------------|
| Humans                   | 25%: 0,<br>50%: 30.49,<br>75%: 0 | Same as in Cats<br>and Dogs            | Same as in Cats<br>and Dogs          | ```sh``` = 0.5775932<br>```rt``` = 0.07099037|
| Cats and Dogs            | Same as in Humans                | 25%: 0,<br>50%: 4.417,<br>75%: 1.250   | 25%: 1.75,<br>50%: 3.5,<br>75%: 5.25 | ```sh``` = 0.5775932<br>```rt``` = 0.07099037|
| Pigs                     | 25%: 0,<br>50%: 0.5,<br>75%: 1   | Same as in Water<br>Buffalo and Cattle | 25%: 3.75,<br>50%: 3.5,<br>75%: 5.25 | ```sh``` = 0.5775932<br>```rt``` = 0.07099037|
| Water Buffalo and Cattle | 25%: 0,<br>50%: 0.1892,<br>75%: 0| 25%: 0,<br>50%: 0.1351,<br>75%: 0      | 25%: 0,<br>50%: 1.216,<br>75%: 0     | ```sh``` = 0.5775932<br>```rt``` = 0.07099037|


## Main Results and Figures
- ```Analysis_Human.csv```, ```Analysis_Cats_and_Dogs.csv```, ```Analysis_Pigs.csv```, and ```Analysis_Water_Buffalo_and_Cattle.csv``` contain the diagnostic sensitivity, specificity and prevalence data for each parasite generated by the JAGS model. They will have not been uploaded to this repository, however, they can be reproduced locally by running ```LatentClassAnalysisFTAF.R``` as they are large .csv files.
 - ```Prevalence_Real_Sim_All_Hosts.svg``` is the plot of the simulated prevalence of each parasite compared with the prevalence recorded in the real-world data, with error bars highlighting the 95% confidence interval. Each host is arranged in a two-by-two grid with all diagnostics plotted together.
 - ```Sensitivity_Prevalence_All_Hosts.svg``` is the plot of the simulated sensitivites and prevalences of the JAGS model. Each host is arranged in a two-by-two grid, with all diagnostics plotted together. This has not been uploaded to this repository since it is a large file (~650 MB) however, it can be reproduced locally by running ```LatentClassAnalysisFTAF.R```.
 - ```Sensitivity_Prevalence_All_Hosts_Simplified.svg``` is the plot of the simulated sensitivites and prevalences of the JAGS model. Unlike the plots in the file ```Sensitivity_Prevalence_All_Hosts.svg```, the scatterpoints are replaced by error bars corresponding to the 95% confidence interval of the data, and the mean of the sensitivity and the mean of the prevalence is plotted point.
 - ```p1_p0_All_Hosts_Simplified.svg``` is the the Reciever Operating Characteristic (ROC) plot of the diagnostic sensitivity and 1 minus the diagnostic specificity. Like ```Sensitivity_Prevalence_All_Hosts_Simplified```, it plots each host for all parasites and diagnostics in a two-by-two grid. The mean of the diagnostic sensitivity and 1 minus the diagnostic specificity are plotted, with error bars corresponding to the 95% confidence interval for the data.

**Note:** When running the code generating the main figures ```Prevalence_Real_Sim_All_Hosts.svg```, ```Sensitivity_Prevalence_All_Hosts.svg```, ```Sensitivity_Prevalence_All_Hosts_Simplified.svg```, and ```p1_p0_All_Hosts_Simplified.svg```, please ensure the RStudio plotting window is very large and wide, especially on small screens such as a laptop.


## Supplementary Figures
These figures have not been included in the main publication. For each host and parasite, ```<Parasite>_<Host>_Supplementary.svg``` in ```/Supplementary_Figures/``` contains a histogram of the estimated probabilities of infection, a histogram of the estimated prevalence of the model, and frequency curves of the sensitivity and specificity of the diagnostics of the model each the parasite.

## Session Info
The R version and used packages are displayed below:
```
R version 4.2.2 (2022-10-31)
Platform: aarch64-apple-darwin20 (64-bit)
Running under: macOS Ventura 13.4

Matrix products: default
LAPACK: /Library/Frameworks/R.framework/Versions/4.2-arm64/Resources/lib/libRlapack.dylib

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

attached base packages:
[1] compiler  stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] rstudioapi_0.14   bayestestR_0.13.0 MCMCpack_1.6-3    MASS_7.3-58.1     ggplot2_3.4.0     cowplot_1.1.1    
[7] runjags_2.2.1-7   rjags_4-13        coda_0.19-4      

loaded via a namespace (and not attached):
 [1] cellranger_1.1.0   pillar_1.8.1       iterators_1.0.14   tools_4.2.2        viridisLite_0.4.1 
 [6] lifecycle_1.0.3    tibble_3.1.8       gtable_0.3.1       lattice_0.20-45    pkgconfig_2.0.3   
[11] rlang_1.0.6        foreach_1.5.2      igraph_1.3.5       Matrix_1.5-1       cli_3.6.0         
[16] parallel_4.2.2     SparseM_1.81       withr_2.5.0        dplyr_1.1.0        MatrixModels_0.5-1
[21] generics_0.1.3     vctrs_0.5.2        grid_4.2.2         tidyselect_1.2.0   glue_1.6.2        
[26] R6_2.5.1           fansi_1.0.4        survival_3.4-0     readxl_1.4.1       farver_2.1.1      
[31] magrittr_2.0.3     codetools_0.2-18   splines_4.2.2      scales_1.2.1       mcmc_0.9-7        
[36] datawizard_0.6.5   insight_0.19.0     colorspace_2.1-0   quantreg_5.94      utf8_1.2.2        
[41] munsell_0.5.0
```
