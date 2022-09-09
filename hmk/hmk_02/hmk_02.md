# Hmk 2

## Basics of base R

### Packages in R

The following block is a demonstration of loading the tidyverse package while also using chunk options to suppress the messages that R produces.

``` r
library(tidyverse)
```

We can look at the packages loaded in R using the search() function.

``` r
search()
```

     [1] ".GlobalEnv"        "package:forcats"   "package:stringr"  
     [4] "package:dplyr"     "package:purrr"     "package:readr"    
     [7] "package:tidyr"     "package:tibble"    "package:ggplot2"  
    [10] "package:tidyverse" "tools:quarto"      "package:stats"    
    [13] "package:graphics"  "package:grDevices" "package:utils"    
    [16] "package:datasets"  "package:methods"   "Autoloads"        
    [19] "package:base"     

The packages forcats, stringr, dplyr, purrr, readr, tidyr, tibble, ggplot2, and tidyverse are all loaded when library(tidyverse) was executed in the block above. The packages stats, graphics, grDevices, utils, datasets, methods, and base are packages that are loaded "when R is invoked". Essentially, these are the default packages in R.

### Assigning, Displaying, and Removing Variables

This block demonstrates the assignment of numeric values to two objects, a and b. We can then use logical operators to determine which object is greater.

``` r
a <- 21/10
b <- 20/9

#Is a less than b?
a < b
```

    [1] TRUE

``` r
#Is a greater than b?
a > b
```

    [1] FALSE

``` r
#Is a equal to b?
a == b
```

    [1] FALSE

We can use ls() to display the variables currently in the workspace.

``` r
ls()
```

    [1] "a" "b"

We can use rm() to remove variables from the workspace.

``` r
rm(list=ls())
ls()
```

    character(0)
