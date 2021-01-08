Star Wars Characters Analysis Using ggplot2
================
Your Name
2021-01-08

Use this chunk to set any global options. `echo=TRUE` means we’ll see
all the code chunks unless we specify otherwise.

To use `ggplot2` functions, we always have to first load the
`tidyverse`:

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.4     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

For help with `ggplot2`, see
[ggplot2.tidyverse.org](http://ggplot2.tidyverse.org/) and the `ggplot2`
Cheatsheet
[here](https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf)

This document will introduce elements of the grammar of graphics using
`ggplot2`.

## Introduction to the Starwars Data Frame

The data set `starwars` is a built-in data set that’s available after
loading the `tidyverse` family of packages as we did above. Let’s take a
look at it:

``` r
starwars
```

    ## # A tibble: 87 x 14
    ##    name  height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>  <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke…    172    77 blond      fair       blue            19   male  mascu…
    ##  2 C-3PO    167    75 <NA>       gold       yellow         112   none  mascu…
    ##  3 R2-D2     96    32 <NA>       white, bl… red             33   none  mascu…
    ##  4 Dart…    202   136 none       white      yellow          41.9 male  mascu…
    ##  5 Leia…    150    49 brown      light      brown           19   fema… femin…
    ##  6 Owen…    178   120 brown, gr… light      blue            52   male  mascu…
    ##  7 Beru…    165    75 brown      light      blue            47   fema… femin…
    ##  8 R5-D4     97    32 <NA>       white, red red             NA   none  mascu…
    ##  9 Bigg…    183    84 black      light      brown           24   male  mascu…
    ## 10 Obi-…    182    77 auburn, w… fair       blue-gray       57   male  mascu…
    ## # … with 77 more rows, and 5 more variables: homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

Questions:

  - How many rows?
  - How many columns?
  - What do the rows represent?  
  - What do the columns represent?

### Getting a Feel for the Data Set

The `glimpse` commands also help give us a feel for the basic
characteristics of the data. This command essentially transposes the
print command so that the rows are the data columns, showing as much of
the data as possible in a small area.

``` r
glimpse(starwars)
```

    ## Rows: 87
    ## Columns: 14
    ## $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia O…
    ## $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, …
    ## $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77…
    ## $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", …
    ## $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", …
    ## $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue"…
    ## $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0,…
    ## $ sex        <chr> "male", "none", "none", "male", "female", "male", "female"…
    ## $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femin…
    ## $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "…
    ## $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Hum…
    ## $ films      <list> [<"The Empire Strikes Back", "Revenge of the Sith", "Retu…
    ## $ vehicles   <list> [<"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "I…
    ## $ starships  <list> [<"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1…

Fortunately, most built-in R functions have help documentation to give
more details. We typically run this at the command line. I’ve set
`eval=FALSE` so that this command doesn’t run if you knit the document.

``` r
?starwars
```

## Using ggplot2 to explore the data

### Simple scatterplot using geom\_point()

``` r
ggplot(data = starwars, mapping = aes(x = height, y = mass)) +
  geom_point()
```

    ## Warning: Removed 28 rows containing missing values (geom_point).

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

Question: Which is the unusual character? How did you figure it out?

For reporting, we’d prefer to get rid of that warning message:

``` r
ggplot(data = starwars, mapping = aes(x = height, y = mass)) +
  geom_point()
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

As an aside, you can start learning about chunk options to control the
size and aspect ratio of your plots:

``` r
ggplot(data = starwars, mapping = aes(x = height, y = mass)) +
  geom_point()
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

Graphs are not complete without labeling. That comes in another layer of
the grammar of graphics, the thematic elements (more about that later).
Here’s an example:

``` r
ggplot(data = starwars) +
  geom_point(mapping = aes(x = height, y = mass)) +
  labs(title = "Scatterplot of Weight (y) vs. Height (x) of Starwars characters",
       x = "Height (cm)", y = "Weight (kg)")            
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

**Note**: Labels are just text and do not need to use the original
variable names. Lots more options of labels are available.

### Getting started with aesthetic mapping

Aesthetic mapping involves using aesthetic features of the graph (shape,
color, etc.) to represent information about a variable. Here are some
examples to get you started.

#### Use gender to color the points

``` r
ggplot(data = starwars) + 
  geom_point(mapping = aes(x = height, y = mass, color = gender))
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

#### Use size of the point to represent year of birth

``` r
ggplot(data = starwars) + 
  geom_point(mapping = aes(x = height, y = mass, color = gender, size = birth_year))
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

#### Use shape to represent gender and color to represent year of birth

``` r
ggplot(data = starwars) + 
  geom_point(mapping = aes(x = height, y = mass, color = birth_year, shape = gender))
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

#### Aesthetics WITHOUT mapping

Set the size of all points to have size 3mm:

``` r
ggplot(data = starwars) +
  geom_point(mapping = aes(x = height, y = mass, color = gender), size = 3)
```

![](star_wars_analysis_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

**Note**: In such as case, we generally need to set the aesthetic
**outside** the `aes()` function. Details of this will get clarified as
we go forward.
