stat\_binscatter
================
Maximilian Eber
26/09/2017

A useful summary tool for large datasets is the binscatter. It can be interpreted as an empirical approximation of the conditional expectation function *E*\[*y*|*x*\]. This is particularly useful when dealing with large datasets.

The difference to `stat_bin` is that the bins are not of equal width but of equal size. Keeping the number of observations (roughly) constant across bins helps identify areas of high density in the data. Therefore, this avoids overinterpreting thinly populated cells with noisy means.

``` r
library(ggplot2)
source("stat_binscatter.R")
```

Examples
--------

``` r
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point(alpha = .1) +
  stat_binscatter(color = "red")
```

![](readme_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-1-1.png)

You can add approximate standard errors by changing the geom to `pointrange`:

``` r
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point(alpha = .1) + 
  stat_binscatter(color = "red", geom = "pointrange")
```

![](readme_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-2-1.png)

Binscattering works well on large datasets where a scatterplot be confusing (and take a long time to plot):

``` r
ggplot(diamonds, aes(x = carat, y = price, color = cut)) + 
  stat_binscatter(bins = 20, geom = "pointrange") +
  stat_binscatter(bins = 20, geom = "line")
```

![](readme_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-3-1.png)
