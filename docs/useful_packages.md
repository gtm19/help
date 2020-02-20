Useful Packages
================

## R Packages

R comes bundled with so-called “base” packages, such as `tools::` and
`utils::`. However, there are heaps of packages which are so widely used
that they are considered *de facto* base packages.

As standard, most of my scripts start as follows:

``` r
library(tidyverse)
library(lubridate)
library(janitor)
library(readxl)
library(here)
```

If you want to install all of these packages, use the following code:

``` r
install.packages(
  c(
    "tidyverse",
    "lubridate",
    "janitor",
    "readxl",
    "here",
  )
)
```

### `tidyverse`

The [`tidyverse`](https://www.tidyverse.org/packages/) is a so-called
“meta-package”, which actually installs a handful of useful packages
such as `ggplot2`, `tidyr`, `readr`, and `dplyr`.

To highlight one, `dplyr` is used for wrangling data frames (which the
`tidyverse` calls “tibbles”). It can be used to filter rows, add
columns, and aggregate data frames:

#### Filtering

``` r
mtcars %>% 
  filter(cyl >= 8)
```

    ##    mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    ## 1 18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
    ## 2 14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
    ## 3 16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
    ## 4 17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
    ## 5 15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
    ## 6 10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
    ## 7 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
    ## 8 14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
    ## 9 15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
    ##  [ reached 'max' / getOption("max.print") -- omitted 5 rows ]

#### Adding Columns

``` r
mtcars %>% 
  mutate(wt_kg = wt * 1000)
```

    ##    mpg cyl  disp  hp drat    wt  qsec vs am gear carb wt_kg
    ## 1 21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4  2620
    ## 2 21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4  2875
    ## 3 22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1  2320
    ## 4 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1  3215
    ## 5 18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2  3440
    ## 6 18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1  3460
    ## 7 14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4  3570
    ## 8 24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2  3190
    ##  [ reached 'max' / getOption("max.print") -- omitted 24 rows ]

#### Summarising / Aggregating

``` r
mtcars %>% 
  group_by(cyl) %>% 
  summarise(mean_hp = mean(hp))
```

    ## # A tibble: 3 x 2
    ##     cyl mean_hp
    ##   <dbl>   <dbl>
    ## 1     4    82.6
    ## 2     6   122. 
    ## 3     8   209.

The [`dplyr` cheat sheet is very
useful](https://rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf).

### `lubridate`

This is a package with nice functions for working with dates. Some
notable ones are `day()`, `month()`, `year()`, which extract parts of
the date; as well as `dmy()` (and similar), which coerce text into a
date:

``` r
today <- Sys.Date()

year(today)
```

    ## [1] 2020

``` r
month(today)
```

    ## [1] 2

``` r
day(today)
```

    ## [1] 20

``` r
dmy("20 Feb 2020")
```

    ## [1] "2020-02-20"

### The Others

`janitor` provides some functions which tidy up data frames, `readxl` is
for working with spreadsheets, and `here` is a simple way to get full
file paths for local files.

If you want to learn more about them, either find them on GitHub and
consult their README files, or run (for example) the following code to
get a list of the vignettes associated with a package.

``` r
vignette(package = "janitor")
```

Then you can open a specific vignette as follows:

``` r
vignette("janitor")
```

### Learning

Probably the best place to learn more about the `tidyverse` and other
useful packages is by reading the book [R For Data
Science](https://r4ds.had.co.nz/), and by consulting the
[cheatsheets](https://rstudio.com/resources/cheatsheets/) on RStudio’s
website.
