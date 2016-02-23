# `quandongr`: visualising and reporting data from bacterial genomes

## Short description

`quandongr` is a companion `R` package to the `nullarbor` pipeline by
Torsten Seemann (find out about `nullarbor` [here](https://github.com/tseemann/nullarbor)).

`quandongr` has three main goals:

  1. Expose `nullarbor` output to `R` users to explore
  2. Make available a number of routine analyses to the user to explore 
  the `nullarbor` output in `R`. In particular, `quandongr` will help
  users plot phylogenetic trees along with metadata
  3. Automate the generation of standard `HTML` or `PDF` reports that
  capture essential information

## Etymology

`nullarbor` is named after the [Australian desert](https://github.com/tseemann/nullarbor#etymology).
Because one of the main goals of `quandongr` is to **grow** beautiful and tasty
trees from `nullarbor`, we decided to name this package after the [*quandong*](https://en.wikipedia.org/wiki/Santalum_acuminatum),
or bush peach, a native fruit tree of the nullarbor desert.

## Installation

### Step 1. Get `R`

`quandongr` is an `R` package. To start off, you should have `R` (download from [here](https://www.r-project.org/))
installed, and to make things really easy, I also suggest installing `RStudio` (download from [here](https://www.rstudio.com/))
to work with `R`.

### Step 2. Get `devtools`

`quandongr` can be easily installed using [`devtools`](https://github.com/hadley/devtools).

If you don't have have `devtools` installed:

    install.packages(devtools)
    
### Step 3. Get `quandongr`

    library(devtools)
    devtools::install_github("andersgs/quandongr")
  
## Using `quandongr`

`quandongr` follows Hadley Wickham's [style guide](http://adv-r.had.co.nz/Style.html) 
where functions are named after verbs. Because the theme of `nullarbor` and 
`quandongr` is growing trees, the verbs used in `quandongr` have an **agricultural**
theme.

`quandongr` has three verbs:

### 1. `till()`

Tilling is the process of preparing the land for planting. Here, `till()` takes
the folder path to the output of `nullarbor`, and returns an object containing
all the information in the reports. 

    my_report <- quandongr::till('/path/to/my/nullarbor/')

### 2. `plant()`

Once the land is tilled, it is time to plant. The function `plant()` creates
a *report* template, which will include only summary information 
(e.g., number of isolates, predominant species, etc.).

To take full advantage of `quandongr`, we have to add `seeds`. If you are
familiar with the `ggplot2` package, `seeds` act like `geoms`, adding 
information to the report (in the agricultural alegory thus far, we wish to 
plant a diversity of seeds to get a variety of report fruits).
like `geom`, you can add `seeds` to build up a report:

    quandongr::plant() + 
      seed_mlst() +
      seed_abricate() +
      seed_core_snps()

### 3. `harvest()`

Once you till, and plant, you harvest the fruits of your labour. The function
`harvest` will produce a report that you can share:

    quandongr::harvest()
    
### 4. Putting it all together

In the process of automating, you can first play with the code in `R` to 
identify the report you would like to produce (e.g., say a bug specific report).
You can then generate a small script to add to your pipeline in order to 
produce the report in a consistent and automated way:

    library(quandongr)
    library(magrittr)

    quandongr::till() %>%
        quandongr::plant() +
            seed_mlst() +
            seed_abricate() +
            seed_core_snps() %>%
          quandongr::harvest()

So, one can chain along the three verbs to produce a report.

## Creating your own seeds

Part of the `quandongr` philosophy is that the user might want to create 
their own analyses. So, we are making it easy for you to make up your own
custom `seeds`. These should consist of an `R` script that takes 
the data object produced by `till` to make a figure or table of interest.

The development of your own `seed` can happen natually by first loading a
`nullarbor` output into `R` using `till()`, and experimenting with 
different visualisation options. Once you are happy with a code, save it
into the `seed bank` with a file name `seed_myseed.R`, where `myseed`
can be anything. 

Examples TBA.


