---
editor_options: 
  markdown: 
    wrap: 72
---

# Homework 3

Jake Perez

# Data input/output

The `tidyverse` package can be used to read a csv file to perform data
analysis within R. The code below reads a data file
(`iron_raw_data.csv`) that contains some data related to analysis of
iron content in sediment layers of a lake system.

``` r
library(tidyverse)
```

``` r
my_data <- read_csv('iron_raw_data.csv')
```

    Rows: 50 Columns: 3
    -- Column specification --------------------------------------------------------
    Delimiter: ","
    chr (1): color
    dbl (2): depth, sample_mass

    i Use `spec()` to retrieve the full column specification for this data.
    i Specify the column types or set `show_col_types = FALSE` to quiet this message.

# Investigating the properties of data frames

We can look at the properties of the data frame object that was created
by using various functions. Below are examples of using `str()` and
`summary()`. The `str()` function specifies the dimensions of the data
frame, the different column vectors with headers, and the data type of
each column.

``` r
str(my_data)
```

    spec_tbl_df [50 x 3] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
     $ depth      : num [1:50] 1 1.5 2 2.6 3.2 4 6.1 6.8 6.9 7.4 ...
     $ color      : chr [1:50] "Black" "Green" "Black" "White" ...
     $ sample_mass: num [1:50] 0.0032 0.0038 0.0048 0.0051 0.0046 0.0043 0.004 0.0025 0.0067 0.0036 ...
     - attr(*, "spec")=
      .. cols(
      ..   depth = col_double(),
      ..   color = col_character(),
      ..   sample_mass = col_double()
      .. )
     - attr(*, "problems")=<externalptr> 

The `summary()` function gives statistical information for the different
column vectors. For the numeric columns, it provides statistical data
like mean and median values. Character columns return the number of
values.

``` r
summary(my_data)
```

         depth          color            sample_mass      
     Min.   : 1.00   Length:50          Min.   :0.002100  
     1st Qu.: 7.40   Class :character   1st Qu.:0.003600  
     Median :18.15   Mode  :character   Median :0.004800  
     Mean   :26.22                      Mean   :0.005782  
     3rd Qu.:32.33                      3rd Qu.:0.007675  
     Max.   :95.50                      Max.   :0.015000  

While statistical data is valuable for numeric data, the `str()`
function is more valuable because it verifies what values were read from
the csv file into the data frame object while the `summary()` function
does not provide enough information to check that your file reading was
effective.

# Manipulating data frames

We can create a new column in the data frame by using `cbind()`. Here we
created a new vector that is an arithmetic manipulation of another
column. This example shows a scaling of the depth of the core data that
is an estimation of the true depth of the layers within the lake
sediments.

``` r
depth <- my_data$depth
scaled_depth <- 2.43142*(depth - 2.6) + 17
my_data <- cbind(my_data, scaled_depth)
print(my_data)
```

       depth      color sample_mass scaled_depth
    1    1.0      Black      0.0032     13.10973
    2    1.5      Green      0.0038     14.32544
    3    2.0      Black      0.0048     15.54115
    4    2.6      White      0.0051     17.00000
    5    3.2       Grey      0.0046     18.45885
    6    4.0      Black      0.0043     20.40399
    7    6.1      Green      0.0040     25.50997
    8    6.8      Black      0.0025     27.21196
    9    6.9      White      0.0067     27.45511
    10   7.4       Grey      0.0036     28.67082
    11  14.6      Black      0.0041     46.17704
    12  15.3      Green      0.0108     47.87903
    13  16.0      Black      0.0065     49.58103
    14  16.8       Grey      0.0110     51.52616
    15  17.7      Black      0.0081     53.71444
    16  18.6      Green      0.0150     55.90272
    17  19.0      Green      0.0098     56.87529
    18  20.5      Black      0.0086     60.52242
    19  21.1       Grey      0.0094     61.98127
    20  25.8      White      0.0089     73.40894
    21  25.0      Black      0.0103     71.46381
    22  27.5      Black      0.0042     77.54236
    23  28.4      Green      0.0077     79.73064
    24  30.9      Black      0.0132     85.80919
    25  32.8       Grey      0.0082     90.42888
    26  12.7      Black      0.0041     41.55734
    27  12.9       Grey      0.0102     42.04363
    28   3.8      Green      0.0022     19.91770
    29   4.0      Black      0.0055     20.40399
    30   7.2      Black      0.0051     28.18453
    31   7.4       Grey      0.0064     28.67082
    32  16.6      Green      0.0058     51.03988
    33  16.7      Black      0.0031     51.28302
    34  29.3      Green      0.0027     81.91891
    35  29.6       Grey      0.0024     82.64834
    36  12.1      Black      0.0047     40.09849
    37  12.4       Grey      0.0076     40.82792
    38  51.0      Green      0.0054    134.68073
    39  51.3      Black      0.0032    135.41015
    40  25.5 Light Grey      0.0058     72.67952
    41  36.1      Green      0.0024     98.45257
    42  36.3      Black      0.0047     98.93885
    43  62.8      Black      0.0033    163.37148
    44  63.0       Grey      0.0021    163.85777
    45  45.2      Black      0.0028    120.57849
    46  45.6      Green      0.0032    121.55106
    47  83.5      Green      0.0036    213.70188
    48  83.6      Black      0.0048    213.94502
    49  95.3      Green      0.0039    242.39263
    50  95.5      Black      0.0057    242.87892

# Working on columns

We can perform specific operations on an individual column of a data
frame by calling the data frame object and using `$` with the name of
the column.

``` r
mean(my_data$sample_mass)
```

    [1] 0.005782

# Accessing elements of data frames

Let's use this `cats` data frame example to explore different notations
that can be used to access different elements of a data frame.

``` r
cats <- data.frame(coat = c("calico", "black", "tabby"),
                   weight = c(2.1, 5.0, 3.2),
                   likes_string = c(1, 0, 1))
```

``` r
cats[1]
```

        coat
    1 calico
    2  black
    3  tabby

``` r
typeof(cats[1])
```

    [1] "list"

`cats[1]` returns a list that is consists of the values in the first
column of the `cats` data frame.

``` r
cats[[1]]
```

    [1] "calico" "black"  "tabby" 

``` r
typeof(cats[[1]])
```

    [1] "character"

`cats[[1]]` returns the values of the first column in the `cats` data
frame

``` r
cats$coat
```

    [1] "calico" "black"  "tabby" 

``` r
typeof(cats$coat)
```

    [1] "character"

`cats$coat` returns the values in the column that has the header `coat`
(in this case, it is also the first column).

``` r
cats[1, 1]
```

    [1] "calico"

``` r
typeof(cats[1, 1])
```

    [1] "character"

`cats[1, 1]` returns the first value of the first column in the `cats`
data frame.

``` r
cats[ ,1]
```

    [1] "calico" "black"  "tabby" 

``` r
typeof(cats[ ,1])
```

    [1] "character"

`cats[ ,1]` returns the values of the first column of the `cats` data
frame.

``` r
cats[1, ]
```

        coat weight likes_string
    1 calico    2.1            1

``` r
typeof(cats[1, ])
```

    [1] "list"

`cats[1, ]` returns a list object that is the first row of the `cats`
data frame.

# Optional challenge

Prompt:

"A data frame is an example of a list. I haven't discussed how to access
elements of lists, but it is covered
[here](https://swcarpentry.github.io/r-novice-gapminder/04-data-structures-part1/index.html#lists)).

Explain in what ways accessing elements of lists are like accessing
columns of data frames, and given that, how it shows that data frames
are a type of list."

Lists are a data type that can be an assembly of different data types.
You can have a list with elements that are numeric, characters, logical,
or complex. Lists can even include vectors of those data types. You can
access specific elements of that list by calling the specific index of
it (e.g. `list[[1]]`, `list[[2]]`) or by calling the value the data type
was assigned to.

For example, the list used in the link above:

``` r
another_list <- list(title = "Numbers", numbers = 1:10, data = TRUE)
another_list
```

    $title
    [1] "Numbers"

    $numbers
     [1]  1  2  3  4  5  6  7  8  9 10

    $data
    [1] TRUE

You can call the different elements by using the `$` notation:

``` r
another_list$title
```

    [1] "Numbers"

``` r
another_list$numbers
```

     [1]  1  2  3  4  5  6  7  8  9 10

These commands to access different elements are the same as accessing
elements in a data frame. A data frame is a specific type of list. A
data frame is a list of vectors that have to be of the same length.
