

Sequenza: Copy Number Estimation from Tumor Genome Sequencing Data
==================================================================

About
-----

__This is a modified version of Sequenza that allows the use of any reference genome used__. For more info on the original work, please visit their repo [here](https://bitbucket.org/sequenzatools/sequenza). The main difference with the original repo is that this version of Sequenza is that it relies on a genome-agnostic fork of the package copynumber (see [here](Irrationone/copynumber)). By adding the new argument implemented by this package, we can use custom cytoband files instead of predefined genomes. Please, check the aforementioned repo for more information.

An example of the cytoband file (findable in UCSC) can be accessed [here](data/mm39.cytoband.txt).

Getting started
---------------

### Minimum requirements

-   Software: R, Python, SAMtools, tabix
-   Operating system: Linux, OS X, Windows
-   Memory: Minimum 4 GB of RAM. Recommended >8 GB.
-   Disk space: 1.5 GB for sample (depending on sequencing depth)
-   R version: 3.2.0
-   Python version: 2.7, 3.4, 3.5, 3.6 (or PyPy)

### Installation

The R package can be installed by:

``` r
devtools::install_github("pbousquets/copynumber")
devtools::install_github("pbousquets/sequenza")
```


Running sequenza
----------------

### Sequenza analysis (in R)

``` r
library(sequenza)
```

In the package is provided a small *seqz* file

``` r
data.file <-  system.file("data", "example.seqz.txt.gz", package = "sequenza")
data.file
```

    ## [1] "/usr/local/lib/R/3.4/site-library/sequenza/data/example.seqz.txt.gz"

The main interface consists of 3 functions:

-   sequenza.extract: process seqz data, normalization and segmentation

``` r
test <- sequenza.extract(data.file, verbose = FALSE, cytoband_file="hg19.cytoband.txt")
```

-   sequenza.fit: run grid-search approach to estimate cellularity and ploidy

``` r
CP <- sequenza.fit(test)
```

-   sequenza.results: write files and plots using suggested or selected solution

``` r
sequenza.results(sequenza.extract = test,
    cp.table = CP, sample.id = "Test",
    out.dir="TEST")
```