
<!-- README.md is generated from README.Rmd. Please edit that file -->
<!-- badges: start -->

[![R-CMD-check](https://github.com/zabore/ppseq/workflows/R-CMD-check/badge.svg)](https://github.com/zabore/ppseq/actions)
[![Codecov test
coverage](https://codecov.io/gh/zabore/ppseq/branch/main/graph/badge.svg)](https://codecov.io/gh/zabore/ppseq?branch=main)
[![CRAN
status](https://www.r-pkg.org/badges/version/ppseq)](https://CRAN.R-project.org/package=ppseq)
[![Lifecycle:
stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)
<!-- badges: end -->

<br> <br>

## ppseq

The {ppseq} package provides functions to design clinical trials using
Bayesian sequential predictive probability monitoring. Functionality is
available to design
[one-arm](https://www.emilyzabor.com/ppseq/articles/one_sample_expansion.html)
or
[two-arm](https://www.emilyzabor.com/ppseq/articles/two_sample_randomized.html)
trials by searching over a grid of combinations of posterior and
predictive thresholds and identifying the optimal design according to
two criteria: accuracy and efficiency. Interactive plotting allows easy
comparison of the various design options and easy trial implementation
through decision rule plots.

## Installation

You can install the production version of ppseq from CRAN with:

``` r
install.packages("ppseq")
```

Or you can install the development version of ppseq from GitHub with:

``` r
remotes::install_github("zabore/ppseq")
```

## Basic usage

The primary function to search over a grid of combinations of posterior
and predictive thresholds for a certain trial design is
`calibrate_thresholds()`. This function is computationally intensive to
varying degrees depending on the number of looks and the number of
threshold combinations, and is best run on a server and/or with
parallelization.

``` r
set.seed(12345)
calthresh <-
  calibrate_thresholds(
    p_null = c(0.2, 0.2),
    p_alt = c(0.2, 0.5),
    n = cbind(seq(10, 50, 10), seq(10, 50, 10)),
    N = c(50, 50),
    pp_threshold = seq(0.9, 0.95, 0.01),
    ppp_threshold = seq(0.05, 0.2, 0.05),
    delta = 0
    )
```

The resulting design options can be interactively compared by passing
the results to `plot()` with the option `plotly = TRUE`:

``` r
plot(calthresh, plotly = TRUE)
```
