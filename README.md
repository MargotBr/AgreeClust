
<!-- README.md is generated from README.Rmd. Please edit that file -->

# agreeclust <img src='man/figures/hex-agreeclust-white.png' align="right" height="139" />

The website presenting the package is:
<https://margotbr.github.io/agreeclust/>

The `{agreeclust}` package considers a latent class regression modeling
framework for highlighting the structure of disagreement among panels of
raters involved in an inquiry. On the contrary to popular approaches,
the present method considers the ratings data provided by all raters
when studying the structure of disagreement among the panel. More
precisely, the structure of disagreement is captured through the
profiles of residuals of a no-latent class regression model adjusted on
the entire set of binary ratings, and can be visualized by using
exploratory data analysis tools. The disagreement between two raters is
then quantify in a concise way through the Euclidean distance between
their respective profiles of residuals, this disagreement index being
used as a basis to construct a dendrogram representing the structure of
disagreement among the panel. The proper number of disagreed clusters
among the panel of raters is then chosen by implementing a sequential
strategy to test the significance of each \(K\)-clusters structure of
disagreement.

## Installation

You can install the package from [GitHub](https://github.com/) with:

``` r
if(!requireNamespace("remotes")){install.packages("remotes")}
remotes::install_github("MargotBr/agreeclust", build_vignettes = TRUE) # create vignettes
```

You can install the development version with:

``` r
if(!requireNamespace("remotes")){install.packages("remotes")}
remotes::install_github("MargotBr/agreeclust", ref = "dev", build_vignettes = TRUE) # create vignettes
```

## Package functionalities

To get an overview of the functionalities of the package, you can read
the
vignettes:

``` r
vignette(topic = "a- Global overview of the statistical methodology", package = "agreeclust")
vignette(topic = "b- Using the proper format of data", package = "agreeclust")
vignette(topic = "c- Use of the package with binary ratings", package = "agreeclust")
```

Or access the website presenting the package:
<https://margotbr.github.io/agreeclust/>

## Usage

``` r
library(agreeclust)
data(binary_data_for_example)
res_pedag <- get_agreeclust_bin(dta = binary_data_for_example,
                                id_info_rater = 9 : nrow(binary_data_for_example),
                                type_info_rater = c(rep("cat", 2), "cont"),
                                id_info_stim = 21 : ncol(binary_data_for_example),
                                type_info_stim = c(rep("cont", 4), "cat"),
                                )
res_pedag
```

    #> ** Results for the agreement-based clustering **
    #> 
    #> The analysis was performed on 20 raters who assessed 8 stimuli
    #> The results are available in the following objects:
    #> 
    #>   name                 
    #> 1 "$call"              
    #> 2 "$profiles.residuals"
    #> 3 "$mat.disag"         
    #> 4 "$pval.dendro"       
    #> 5 "$nb.clust.found"    
    #> 6 "$partition"         
    #> 7 "$res.plot.segment"  
    #> 8 "$res.pca"           
    #> 9 "$charact.clust"     
    #>   description                                                                    
    #> 1 "arguments used in the AgreeClust function"                                    
    #> 2 "matrix of profiles of deviance residuals"                                     
    #> 3 "disagreement matrix"                                                          
    #> 4 "p-values in the dendrogram"                                                   
    #> 5 "number of clusters of raters found"                                           
    #> 6 "partition of raters found (consolidated or not)"                              
    #> 7 "graphical results of the clustering (not needed)"                             
    #> 8 "PCA results of the multidimensional analysis of the structure of disagreement"
    #> 9 "description of the clusters of raters"

``` r
# Visualisation of the clustering process
plot_agreeclust(res_pedag, choice = "seg")
```

<img src="man/figures/README-unnamed-chunk-7-1.png" width="600" style="display: block; margin: auto;" />

``` r
# Visualisation of the multidimensional structure of disagreement
plot_agreeclust(res_pedag, choice = "mul")
```

<img src="man/figures/README-unnamed-chunk-8-1.png" width="600" style="display: block; margin: auto;" />

``` r
# Interactive version
plot_agreeclust(res_pedag, choice = "mul", interact = TRUE)
```
