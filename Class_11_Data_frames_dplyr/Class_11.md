Class 11: Operations on data frames, dplyr
================
Tomasz Gaczorek & Wiesław Babik
2022-07-12

-   [Operations on data frames, part
    2](#operations-on-data-frames-part-2)
    -   [Subsetting data frames with logical
        expressions](#subsetting-data-frames-with-logical-expressions)
        -   [Exercise 1](#exercise-1)
        -   [Exercise 2](#exercise-2)
    -   [Adding new column or row](#adding-new-column-or-row)
        -   [Exercise 3](#exercise-3)
        -   [Exercise 4](#exercise-4)
        -   [Exercise 5](#exercise-5)
        -   [Exercise 6](#exercise-6)
    -   [Saving data frame](#saving-data-frame)
        -   [Exercise 7](#exercise-7)
-   [`dplyr` and `tidyverse`](#dplyr-and-tidyverse)
-   [Six `dplyr` verbs](#six-dplyr-verbs)
    -   [Exercise 8](#exercise-8)
    -   [Exercise 9](#exercise-9)
    -   [Filtering rows with `filter()`](#filtering-rows-with-filter)
        -   [`filter()` examples](#filter-examples)
        -   [Exercise 10](#exercise-10)
    -   [Ordering rows with `arrange()`](#ordering-rows-with-arrange)
        -   [`arrange()` example](#arrange-example)
        -   [Exercise 11](#exercise-11)
    -   [Picking, dropping and re-ordering columns with
        `select()`](#picking-dropping-and-re-ordering-columns-with-select)
        -   [`select()` examples](#select-examples)
        -   [Exercise 12](#exercise-12)
        -   [Exercise 13](#exercise-13)
    -   [Creating new variables as functions of the existing ones with
        `mutate()`](#creating-new-variables-as-functions-of-the-existing-ones-with-mutate)
        -   [`mutate` examples](#mutate-examples)
        -   [Exercise 14](#exercise-14)
    -   [Grouping cases by variable(s) with
        `group_by()`](#grouping-cases-by-variables-with-group_by)
        -   [`group_by()` examples](#group_by-examples)
        -   [Exercise 15](#exercise-15)
        -   [The pipe operator (`%>%`)](#the-pipe-operator-)
    -   [Summarising with `summarise()`](#summarising-with-summarise)

## Operations on data frames, part 2

### Subsetting data frames with logical expressions

The logic of subsetting vector with logical expressions can be easily
extended to data frames. Note, that if you want to obtain a logical
vector with one element for each row (i.e, to subset rows), you need to
specify which column you want to use. For instance, if you have data
frame `my_data` and you want to get all rows with the value of variable
`my_column` different from 5, you would use the following expression
`my_data[my_data$my_column !=5,]`. This expression will return all
columns (note blank after the comma)

#### Exercise 1

Using built-in dataset `CO2`, return observations for `Qn2` plant.

Expected result:

    ##    Plant   Type  Treatment conc uptake
    ## 8    Qn2 Quebec nonchilled   95   13.6
    ## 9    Qn2 Quebec nonchilled  175   27.3
    ## 10   Qn2 Quebec nonchilled  250   37.1
    ## 11   Qn2 Quebec nonchilled  350   41.8
    ## 12   Qn2 Quebec nonchilled  500   40.6
    ## 13   Qn2 Quebec nonchilled  675   41.4
    ## 14   Qn2 Quebec nonchilled 1000   44.3

------------------------------------------------------------------------

#### Exercise 2

Using built-in dataset `CO2`, return observation from Mississippi
chilled plant with an uptake higher than 0.02 mmol/m<sup>2</sup> x s.
**Tip** Check the description of the `CO2` dataset for the `uptake`
units.

Expected result:

    ##    Plant        Type Treatment conc uptake
    ## 69   Mc1 Mississippi   chilled  675   22.2
    ## 70   Mc1 Mississippi   chilled 1000   21.9

------------------------------------------------------------------------

### Adding new column or row

Adding **new column** is relatively **simple**. All you need to have is
a vector. However, remember three things:

-   the length of vector must equal the number of rows of the data frame
-   the order of values within a vector corresponds to the row numbers
-   the name of the vector will become the name of the added column

We are going to add a column with IDs of observations to the `my_data`
data frame created during Class 9.Note that column with IDs is often
necessary in statistical analysis. It is also inherent to the data in
[long format](https://www.theanalysisfactor.com/wide-and-long-data/)
which is strongly advised (see class 1 and next class).

#### Exercise 3

Create vector with ID numbers starting from 100. Use one of the
functions introduced previously to determine what should be the length
of the vector, considering the length of `my_data`. Name the vector
`ID`.  
Expected result:

    ##  [1] 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118
    ## [20] 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137
    ## [39] 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156
    ## [58] 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175
    ## [77] 176 177 178 179 180 181 182

------------------------------------------------------------------------

You can combine data frames with the use of `cbind()` function in the
following manner: `cbind(data_frame1, data_frame2)`. Note that a vector
can be considered a data frame with a single column.

#### Exercise 4

Place created IDs at the beginning (as first column) of `my_data`.
Overwrite `my_data` dataset.

------------------------------------------------------------------------

Adding **new row** is more **complicated** as you cannot create a vector
with different types of data. Firstly you need to create a new data
frame (similar to the old one) consisting of only new row (or rows). To
do this use `data.frame()` function in the following manner:
`data.frame(columnName1 = value1, columnName2 = value2,...)`.

#### Exercise 5

Create data frame with a single row and the following values:
`1,"Kr1","Krakow","unknown",1000,20`. Column names should correspond to
these of `my_data`. Name the newly created data frame `Added_rows`.

Expected result:

    ##   ID Plant   Type Treatment conc uptake
    ## 1  1   Kr1 Kraków   unknown 1000     20

------------------------------------------------------------------------

To create a data frame with multiple rows, replace the value for each
column with a vector.

To combine data frames by rows use `rbind()` function in the following
manner: `rbind(data_frame1, data_frame2)`

#### Exercise 6

Add the row created in Ex. 5 at the end of `my_data`. Overwrite
`my_data` data frame.

------------------------------------------------------------------------

### Saving data frame

To save your data frame into a text file use `write.table()` function.

#### Exercise 7

Save the modified `my_data` int a `.csv` file. Consult `write.table()`
manual to set the arguments. Include your surname in the file name.

------------------------------------------------------------------------

## `dplyr` and `tidyverse`

`dplyr` is a package from `tidyverse` ecosystem (a set of packages
sharing a common philosophy), which has been enjoying an enormous
popularity in recent years. Sometimes even one has an impression that
people equate R with `tidyverse`. The main purpose of `dplyr` is to
simplify work with data frames. In this course we first introduced base
R, because we are convinced that its understanding is critical for
efficient work in R. During this class you’ll learn how to use `dplyr`
and we’ll go through a real-life example of filtering and summarizing a
complex, “real”, data. For more info on `tidyverse` see
[webpage](https://www.tidyverse.org/) and [free
book](https://r4ds.had.co.nz/)

## Six `dplyr` verbs

We’ll illustrate the basic `dplyr` functions (verbs) using the built-in
`iris` dataset that contains measurements (in cm) of several flower
traits of several *Iris* species.

#### Exercise 8

Display structure and summary of `iris` dataset using `str()` and
`summary()`. Answer the following questions:

-   which traits were measured?
-   how many flowers were measured in total?
-   which *Iris* species were studied?
-   what were sample sizes of particular species?

Here’s a schematic view of a flower with the most important structures
labeled:

![flower](flower.png)

------------------------------------------------------------------------

All six functions work similarly:

1.  The first argument is always a data frame.
2.  Subsequent arguments describe what the function is supposed to do
    with the data frame. You can refer to the columns of the data frame
    without using quotation marks.
3.  The result is a data frame.

#### Exercise 9

Load `dplyr` package.

    ## 
    ## Dołączanie pakietu: 'dplyr'

    ## Następujące obiekty zostały zakryte z 'package:stats':
    ## 
    ##     filter, lag

    ## Następujące obiekty zostały zakryte z 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

------------------------------------------------------------------------

### Filtering rows with `filter()`

`filter()` returns rows that fulfill a logical condition. You can
combine any number of conditions.

#### `filter()` examples

Display data for *Iris setosa*

``` r
filter(iris, Species == "setosa")
```

    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1           5.1         3.5          1.4         0.2  setosa
    ## 2           4.9         3.0          1.4         0.2  setosa
    ## 3           4.7         3.2          1.3         0.2  setosa
    ## 4           4.6         3.1          1.5         0.2  setosa
    ## 5           5.0         3.6          1.4         0.2  setosa
    ## 6           5.4         3.9          1.7         0.4  setosa
    ## 7           4.6         3.4          1.4         0.3  setosa
    ## 8           5.0         3.4          1.5         0.2  setosa
    ## 9           4.4         2.9          1.4         0.2  setosa
    ## 10          4.9         3.1          1.5         0.1  setosa
    ## 11          5.4         3.7          1.5         0.2  setosa
    ## 12          4.8         3.4          1.6         0.2  setosa
    ## 13          4.8         3.0          1.4         0.1  setosa
    ## 14          4.3         3.0          1.1         0.1  setosa
    ## 15          5.8         4.0          1.2         0.2  setosa
    ## 16          5.7         4.4          1.5         0.4  setosa
    ## 17          5.4         3.9          1.3         0.4  setosa
    ## 18          5.1         3.5          1.4         0.3  setosa
    ## 19          5.7         3.8          1.7         0.3  setosa
    ## 20          5.1         3.8          1.5         0.3  setosa
    ## 21          5.4         3.4          1.7         0.2  setosa
    ## 22          5.1         3.7          1.5         0.4  setosa
    ## 23          4.6         3.6          1.0         0.2  setosa
    ## 24          5.1         3.3          1.7         0.5  setosa
    ## 25          4.8         3.4          1.9         0.2  setosa
    ## 26          5.0         3.0          1.6         0.2  setosa
    ## 27          5.0         3.4          1.6         0.4  setosa
    ## 28          5.2         3.5          1.5         0.2  setosa
    ## 29          5.2         3.4          1.4         0.2  setosa
    ## 30          4.7         3.2          1.6         0.2  setosa
    ## 31          4.8         3.1          1.6         0.2  setosa
    ## 32          5.4         3.4          1.5         0.4  setosa
    ## 33          5.2         4.1          1.5         0.1  setosa
    ## 34          5.5         4.2          1.4         0.2  setosa
    ## 35          4.9         3.1          1.5         0.2  setosa
    ## 36          5.0         3.2          1.2         0.2  setosa
    ## 37          5.5         3.5          1.3         0.2  setosa
    ## 38          4.9         3.6          1.4         0.1  setosa
    ## 39          4.4         3.0          1.3         0.2  setosa
    ## 40          5.1         3.4          1.5         0.2  setosa
    ## 41          5.0         3.5          1.3         0.3  setosa
    ## 42          4.5         2.3          1.3         0.3  setosa
    ## 43          4.4         3.2          1.3         0.2  setosa
    ## 44          5.0         3.5          1.6         0.6  setosa
    ## 45          5.1         3.8          1.9         0.4  setosa
    ## 46          4.8         3.0          1.4         0.3  setosa
    ## 47          5.1         3.8          1.6         0.2  setosa
    ## 48          4.6         3.2          1.4         0.2  setosa
    ## 49          5.3         3.7          1.5         0.2  setosa
    ## 50          5.0         3.3          1.4         0.2  setosa

**Note:**

-   we used double equal sign (`==`) to specify a comparison
-   the column name was not enclosed in quotation marks, while the value
    (species name, character string) was.

Display all observations for *Iris setosa* that have sepal length at
least 5.5 cm:

``` r
filter(iris, Species == "setosa", Sepal.Length >= 5.5)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.8         4.0          1.2         0.2  setosa
    ## 2          5.7         4.4          1.5         0.4  setosa
    ## 3          5.7         3.8          1.7         0.3  setosa
    ## 4          5.5         4.2          1.4         0.2  setosa
    ## 5          5.5         3.5          1.3         0.2  setosa

If both conditions are to be met, they can be separated by comma (`,`)
or by the AND sign (`&`):

``` r
filter(iris, Species == "setosa" & Sepal.Length >= 5.5)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.8         4.0          1.2         0.2  setosa
    ## 2          5.7         4.4          1.5         0.4  setosa
    ## 3          5.7         3.8          1.7         0.3  setosa
    ## 4          5.5         4.2          1.4         0.2  setosa
    ## 5          5.5         3.5          1.3         0.2  setosa

You can use alternatives and group conditions using parentheses. To
display all observations of *I. versicolor* and *I. virginica* that have
petal length at least 5 cm:

``` r
filter(iris, (Species == "versicolor" | Species == "virginica"), Petal.Length >=5)
```

or

``` r
filter(iris, (Species == "versicolor" | Species == "virginica") & Petal.Length >=5)
```

    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1           6.7         3.0          5.0         1.7 versicolor
    ## 2           6.0         2.7          5.1         1.6 versicolor
    ## 3           6.3         3.3          6.0         2.5  virginica
    ## 4           5.8         2.7          5.1         1.9  virginica
    ## 5           7.1         3.0          5.9         2.1  virginica
    ## 6           6.3         2.9          5.6         1.8  virginica
    ## 7           6.5         3.0          5.8         2.2  virginica
    ## 8           7.6         3.0          6.6         2.1  virginica
    ## 9           7.3         2.9          6.3         1.8  virginica
    ## 10          6.7         2.5          5.8         1.8  virginica
    ## 11          7.2         3.6          6.1         2.5  virginica
    ## 12          6.5         3.2          5.1         2.0  virginica
    ## 13          6.4         2.7          5.3         1.9  virginica
    ## 14          6.8         3.0          5.5         2.1  virginica
    ## 15          5.7         2.5          5.0         2.0  virginica
    ## 16          5.8         2.8          5.1         2.4  virginica
    ## 17          6.4         3.2          5.3         2.3  virginica
    ## 18          6.5         3.0          5.5         1.8  virginica
    ## 19          7.7         3.8          6.7         2.2  virginica
    ## 20          7.7         2.6          6.9         2.3  virginica
    ## 21          6.0         2.2          5.0         1.5  virginica
    ## 22          6.9         3.2          5.7         2.3  virginica
    ## 23          7.7         2.8          6.7         2.0  virginica
    ## 24          6.7         3.3          5.7         2.1  virginica
    ## 25          7.2         3.2          6.0         1.8  virginica
    ## 26          6.4         2.8          5.6         2.1  virginica
    ## 27          7.2         3.0          5.8         1.6  virginica
    ## 28          7.4         2.8          6.1         1.9  virginica
    ## 29          7.9         3.8          6.4         2.0  virginica
    ## 30          6.4         2.8          5.6         2.2  virginica
    ## 31          6.3         2.8          5.1         1.5  virginica
    ## 32          6.1         2.6          5.6         1.4  virginica
    ## 33          7.7         3.0          6.1         2.3  virginica
    ## 34          6.3         3.4          5.6         2.4  virginica
    ## 35          6.4         3.1          5.5         1.8  virginica
    ## 36          6.9         3.1          5.4         2.1  virginica
    ## 37          6.7         3.1          5.6         2.4  virginica
    ## 38          6.9         3.1          5.1         2.3  virginica
    ## 39          5.8         2.7          5.1         1.9  virginica
    ## 40          6.8         3.2          5.9         2.3  virginica
    ## 41          6.7         3.3          5.7         2.5  virginica
    ## 42          6.7         3.0          5.2         2.3  virginica
    ## 43          6.3         2.5          5.0         1.9  virginica
    ## 44          6.5         3.0          5.2         2.0  virginica
    ## 45          6.2         3.4          5.4         2.3  virginica
    ## 46          5.9         3.0          5.1         1.8  virginica

Note, that the following doesn’t work:

``` r
filter(iris, (Species == "versicolor" | "virginica"), Petal.Length >=5)
```

    ## Error in `filter()`:
    ## ! Problem while computing `..1 = (Species == "versicolor" |
    ##   "virginica")`.
    ## Caused by error in `Species == "versicolor" | "virginica"`:
    ## ! operacje są możliwe jedynie dla typów liczbowych, logicznych oraz zespolonych

#### Exercise 10

Select all observations, regardless of species, that have sepal length
smaller than 6 cm or petal length smaller than 5 cm, and sepal width
larger than 4 cm.

Expected result:

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.7         4.4          1.5         0.4  setosa
    ## 2          5.2         4.1          1.5         0.1  setosa
    ## 3          5.5         4.2          1.4         0.2  setosa

------------------------------------------------------------------------

### Ordering rows with `arrange()`

`arrange()`returns data frame sorted according to a column or a
combination of columns. If you provide more than one column, each
additional column will be used to break the ties. If you want to sort
according to a column in descending order, use `desc()`. Note, that
numbers stored as character are sorted differently than numbers stored
as numeric, and when sorting logical values `FALSE` (`0`) comes before
`TRUE` (`1`).

#### `arrange()` example

Sort the `iris` dataset according to species in alphabetical (ascending)
order and within the species from the longest to the shortest sepal

``` r
arrange(iris, Species, desc(Sepal.Length))
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            5.8         4.0          1.2         0.2     setosa
    ## 2            5.7         4.4          1.5         0.4     setosa
    ## 3            5.7         3.8          1.7         0.3     setosa
    ## 4            5.5         4.2          1.4         0.2     setosa
    ## 5            5.5         3.5          1.3         0.2     setosa
    ## 6            5.4         3.9          1.7         0.4     setosa
    ## 7            5.4         3.7          1.5         0.2     setosa
    ## 8            5.4         3.9          1.3         0.4     setosa
    ## 9            5.4         3.4          1.7         0.2     setosa
    ## 10           5.4         3.4          1.5         0.4     setosa
    ## 11           5.3         3.7          1.5         0.2     setosa
    ## 12           5.2         3.5          1.5         0.2     setosa
    ## 13           5.2         3.4          1.4         0.2     setosa
    ## 14           5.2         4.1          1.5         0.1     setosa
    ## 15           5.1         3.5          1.4         0.2     setosa
    ## 16           5.1         3.5          1.4         0.3     setosa
    ## 17           5.1         3.8          1.5         0.3     setosa
    ## 18           5.1         3.7          1.5         0.4     setosa
    ## 19           5.1         3.3          1.7         0.5     setosa
    ## 20           5.1         3.4          1.5         0.2     setosa
    ## 21           5.1         3.8          1.9         0.4     setosa
    ## 22           5.1         3.8          1.6         0.2     setosa
    ## 23           5.0         3.6          1.4         0.2     setosa
    ## 24           5.0         3.4          1.5         0.2     setosa
    ## 25           5.0         3.0          1.6         0.2     setosa
    ## 26           5.0         3.4          1.6         0.4     setosa
    ## 27           5.0         3.2          1.2         0.2     setosa
    ## 28           5.0         3.5          1.3         0.3     setosa
    ## 29           5.0         3.5          1.6         0.6     setosa
    ## 30           5.0         3.3          1.4         0.2     setosa
    ## 31           4.9         3.0          1.4         0.2     setosa
    ## 32           4.9         3.1          1.5         0.1     setosa
    ## 33           4.9         3.1          1.5         0.2     setosa
    ## 34           4.9         3.6          1.4         0.1     setosa
    ## 35           4.8         3.4          1.6         0.2     setosa
    ## 36           4.8         3.0          1.4         0.1     setosa
    ## 37           4.8         3.4          1.9         0.2     setosa
    ## 38           4.8         3.1          1.6         0.2     setosa
    ## 39           4.8         3.0          1.4         0.3     setosa
    ## 40           4.7         3.2          1.3         0.2     setosa
    ## 41           4.7         3.2          1.6         0.2     setosa
    ## 42           4.6         3.1          1.5         0.2     setosa
    ## 43           4.6         3.4          1.4         0.3     setosa
    ## 44           4.6         3.6          1.0         0.2     setosa
    ## 45           4.6         3.2          1.4         0.2     setosa
    ## 46           4.5         2.3          1.3         0.3     setosa
    ## 47           4.4         2.9          1.4         0.2     setosa
    ## 48           4.4         3.0          1.3         0.2     setosa
    ## 49           4.4         3.2          1.3         0.2     setosa
    ## 50           4.3         3.0          1.1         0.1     setosa
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.9         3.1          4.9         1.5 versicolor
    ## 53           6.8         2.8          4.8         1.4 versicolor
    ## 54           6.7         3.1          4.4         1.4 versicolor
    ## 55           6.7         3.0          5.0         1.7 versicolor
    ## 56           6.7         3.1          4.7         1.5 versicolor
    ## 57           6.6         2.9          4.6         1.3 versicolor
    ## 58           6.6         3.0          4.4         1.4 versicolor
    ## 59           6.5         2.8          4.6         1.5 versicolor
    ## 60           6.4         3.2          4.5         1.5 versicolor
    ## 61           6.4         2.9          4.3         1.3 versicolor
    ## 62           6.3         3.3          4.7         1.6 versicolor
    ## 63           6.3         2.5          4.9         1.5 versicolor
    ## 64           6.3         2.3          4.4         1.3 versicolor
    ## 65           6.2         2.2          4.5         1.5 versicolor
    ## 66           6.2         2.9          4.3         1.3 versicolor
    ## 67           6.1         2.9          4.7         1.4 versicolor
    ## 68           6.1         2.8          4.0         1.3 versicolor
    ## 69           6.1         2.8          4.7         1.2 versicolor
    ## 70           6.1         3.0          4.6         1.4 versicolor
    ## 71           6.0         2.2          4.0         1.0 versicolor
    ## 72           6.0         2.9          4.5         1.5 versicolor
    ## 73           6.0         2.7          5.1         1.6 versicolor
    ## 74           6.0         3.4          4.5         1.6 versicolor
    ## 75           5.9         3.0          4.2         1.5 versicolor
    ## 76           5.9         3.2          4.8         1.8 versicolor
    ## 77           5.8         2.7          4.1         1.0 versicolor
    ## 78           5.8         2.7          3.9         1.2 versicolor
    ## 79           5.8         2.6          4.0         1.2 versicolor
    ## 80           5.7         2.8          4.5         1.3 versicolor
    ## 81           5.7         2.6          3.5         1.0 versicolor
    ## 82           5.7         3.0          4.2         1.2 versicolor
    ## 83           5.7         2.9          4.2         1.3 versicolor
    ## 84           5.7         2.8          4.1         1.3 versicolor
    ## 85           5.6         2.9          3.6         1.3 versicolor
    ## 86           5.6         3.0          4.5         1.5 versicolor
    ## 87           5.6         2.5          3.9         1.1 versicolor
    ## 88           5.6         3.0          4.1         1.3 versicolor
    ## 89           5.6         2.7          4.2         1.3 versicolor
    ## 90           5.5         2.3          4.0         1.3 versicolor
    ## 91           5.5         2.4          3.8         1.1 versicolor
    ## 92           5.5         2.4          3.7         1.0 versicolor
    ## 93           5.5         2.5          4.0         1.3 versicolor
    ## 94           5.5         2.6          4.4         1.2 versicolor
    ## 95           5.4         3.0          4.5         1.5 versicolor
    ## 96           5.2         2.7          3.9         1.4 versicolor
    ## 97           5.1         2.5          3.0         1.1 versicolor
    ## 98           5.0         2.0          3.5         1.0 versicolor
    ## 99           5.0         2.3          3.3         1.0 versicolor
    ## 100          4.9         2.4          3.3         1.0 versicolor
    ## 101          7.9         3.8          6.4         2.0  virginica
    ## 102          7.7         3.8          6.7         2.2  virginica
    ## 103          7.7         2.6          6.9         2.3  virginica
    ## 104          7.7         2.8          6.7         2.0  virginica
    ## 105          7.7         3.0          6.1         2.3  virginica
    ## 106          7.6         3.0          6.6         2.1  virginica
    ## 107          7.4         2.8          6.1         1.9  virginica
    ## 108          7.3         2.9          6.3         1.8  virginica
    ## 109          7.2         3.6          6.1         2.5  virginica
    ## 110          7.2         3.2          6.0         1.8  virginica
    ## 111          7.2         3.0          5.8         1.6  virginica
    ## 112          7.1         3.0          5.9         2.1  virginica
    ## 113          6.9         3.2          5.7         2.3  virginica
    ## 114          6.9         3.1          5.4         2.1  virginica
    ## 115          6.9         3.1          5.1         2.3  virginica
    ## 116          6.8         3.0          5.5         2.1  virginica
    ## 117          6.8         3.2          5.9         2.3  virginica
    ## 118          6.7         2.5          5.8         1.8  virginica
    ## 119          6.7         3.3          5.7         2.1  virginica
    ## 120          6.7         3.1          5.6         2.4  virginica
    ## 121          6.7         3.3          5.7         2.5  virginica
    ## 122          6.7         3.0          5.2         2.3  virginica
    ## 123          6.5         3.0          5.8         2.2  virginica
    ## 124          6.5         3.2          5.1         2.0  virginica
    ## 125          6.5         3.0          5.5         1.8  virginica
    ## 126          6.5         3.0          5.2         2.0  virginica
    ## 127          6.4         2.7          5.3         1.9  virginica
    ## 128          6.4         3.2          5.3         2.3  virginica
    ## 129          6.4         2.8          5.6         2.1  virginica
    ## 130          6.4         2.8          5.6         2.2  virginica
    ## 131          6.4         3.1          5.5         1.8  virginica
    ## 132          6.3         3.3          6.0         2.5  virginica
    ## 133          6.3         2.9          5.6         1.8  virginica
    ## 134          6.3         2.7          4.9         1.8  virginica
    ## 135          6.3         2.8          5.1         1.5  virginica
    ## 136          6.3         3.4          5.6         2.4  virginica
    ## 137          6.3         2.5          5.0         1.9  virginica
    ## 138          6.2         2.8          4.8         1.8  virginica
    ## 139          6.2         3.4          5.4         2.3  virginica
    ## 140          6.1         3.0          4.9         1.8  virginica
    ## 141          6.1         2.6          5.6         1.4  virginica
    ## 142          6.0         2.2          5.0         1.5  virginica
    ## 143          6.0         3.0          4.8         1.8  virginica
    ## 144          5.9         3.0          5.1         1.8  virginica
    ## 145          5.8         2.7          5.1         1.9  virginica
    ## 146          5.8         2.8          5.1         2.4  virginica
    ## 147          5.8         2.7          5.1         1.9  virginica
    ## 148          5.7         2.5          5.0         2.0  virginica
    ## 149          5.6         2.8          4.9         2.0  virginica
    ## 150          4.9         2.5          4.5         1.7  virginica

------------------------------------------------------------------------

#### Exercise 11

Sort species in descending order, and observations within each species
according to the increasing petal length.

Expected result:

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            4.9         2.5          4.5         1.7  virginica
    ## 2            6.2         2.8          4.8         1.8  virginica
    ## 3            6.0         3.0          4.8         1.8  virginica
    ## 4            5.6         2.8          4.9         2.0  virginica
    ## 5            6.3         2.7          4.9         1.8  virginica
    ## 6            6.1         3.0          4.9         1.8  virginica
    ## 7            5.7         2.5          5.0         2.0  virginica
    ## 8            6.0         2.2          5.0         1.5  virginica
    ## 9            6.3         2.5          5.0         1.9  virginica
    ## 10           5.8         2.7          5.1         1.9  virginica
    ## 11           6.5         3.2          5.1         2.0  virginica
    ## 12           5.8         2.8          5.1         2.4  virginica
    ## 13           6.3         2.8          5.1         1.5  virginica
    ## 14           6.9         3.1          5.1         2.3  virginica
    ## 15           5.8         2.7          5.1         1.9  virginica
    ## 16           5.9         3.0          5.1         1.8  virginica
    ## 17           6.7         3.0          5.2         2.3  virginica
    ## 18           6.5         3.0          5.2         2.0  virginica
    ## 19           6.4         2.7          5.3         1.9  virginica
    ## 20           6.4         3.2          5.3         2.3  virginica
    ## 21           6.9         3.1          5.4         2.1  virginica
    ## 22           6.2         3.4          5.4         2.3  virginica
    ## 23           6.8         3.0          5.5         2.1  virginica
    ## 24           6.5         3.0          5.5         1.8  virginica
    ## 25           6.4         3.1          5.5         1.8  virginica
    ## 26           6.3         2.9          5.6         1.8  virginica
    ## 27           6.4         2.8          5.6         2.1  virginica
    ## 28           6.4         2.8          5.6         2.2  virginica
    ## 29           6.1         2.6          5.6         1.4  virginica
    ## 30           6.3         3.4          5.6         2.4  virginica
    ## 31           6.7         3.1          5.6         2.4  virginica
    ## 32           6.9         3.2          5.7         2.3  virginica
    ## 33           6.7         3.3          5.7         2.1  virginica
    ## 34           6.7         3.3          5.7         2.5  virginica
    ## 35           6.5         3.0          5.8         2.2  virginica
    ## 36           6.7         2.5          5.8         1.8  virginica
    ## 37           7.2         3.0          5.8         1.6  virginica
    ## 38           7.1         3.0          5.9         2.1  virginica
    ## 39           6.8         3.2          5.9         2.3  virginica
    ## 40           6.3         3.3          6.0         2.5  virginica
    ## 41           7.2         3.2          6.0         1.8  virginica
    ## 42           7.2         3.6          6.1         2.5  virginica
    ## 43           7.4         2.8          6.1         1.9  virginica
    ## 44           7.7         3.0          6.1         2.3  virginica
    ## 45           7.3         2.9          6.3         1.8  virginica
    ## 46           7.9         3.8          6.4         2.0  virginica
    ## 47           7.6         3.0          6.6         2.1  virginica
    ## 48           7.7         3.8          6.7         2.2  virginica
    ## 49           7.7         2.8          6.7         2.0  virginica
    ## 50           7.7         2.6          6.9         2.3  virginica
    ## 51           5.1         2.5          3.0         1.1 versicolor
    ## 52           4.9         2.4          3.3         1.0 versicolor
    ## 53           5.0         2.3          3.3         1.0 versicolor
    ## 54           5.0         2.0          3.5         1.0 versicolor
    ## 55           5.7         2.6          3.5         1.0 versicolor
    ## 56           5.6         2.9          3.6         1.3 versicolor
    ## 57           5.5         2.4          3.7         1.0 versicolor
    ## 58           5.5         2.4          3.8         1.1 versicolor
    ## 59           5.2         2.7          3.9         1.4 versicolor
    ## 60           5.6         2.5          3.9         1.1 versicolor
    ## 61           5.8         2.7          3.9         1.2 versicolor
    ## 62           5.5         2.3          4.0         1.3 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.8          4.0         1.3 versicolor
    ## 65           5.5         2.5          4.0         1.3 versicolor
    ## 66           5.8         2.6          4.0         1.2 versicolor
    ## 67           5.8         2.7          4.1         1.0 versicolor
    ## 68           5.6         3.0          4.1         1.3 versicolor
    ## 69           5.7         2.8          4.1         1.3 versicolor
    ## 70           5.9         3.0          4.2         1.5 versicolor
    ## 71           5.6         2.7          4.2         1.3 versicolor
    ## 72           5.7         3.0          4.2         1.2 versicolor
    ## 73           5.7         2.9          4.2         1.3 versicolor
    ## 74           6.4         2.9          4.3         1.3 versicolor
    ## 75           6.2         2.9          4.3         1.3 versicolor
    ## 76           6.7         3.1          4.4         1.4 versicolor
    ## 77           6.6         3.0          4.4         1.4 versicolor
    ## 78           6.3         2.3          4.4         1.3 versicolor
    ## 79           5.5         2.6          4.4         1.2 versicolor
    ## 80           6.4         3.2          4.5         1.5 versicolor
    ## 81           5.7         2.8          4.5         1.3 versicolor
    ## 82           5.6         3.0          4.5         1.5 versicolor
    ## 83           6.2         2.2          4.5         1.5 versicolor
    ## 84           6.0         2.9          4.5         1.5 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.5         2.8          4.6         1.5 versicolor
    ## 88           6.6         2.9          4.6         1.3 versicolor
    ## 89           6.1         3.0          4.6         1.4 versicolor
    ## 90           7.0         3.2          4.7         1.4 versicolor
    ## 91           6.3         3.3          4.7         1.6 versicolor
    ## 92           6.1         2.9          4.7         1.4 versicolor
    ## 93           6.1         2.8          4.7         1.2 versicolor
    ## 94           6.7         3.1          4.7         1.5 versicolor
    ## 95           5.9         3.2          4.8         1.8 versicolor
    ## 96           6.8         2.8          4.8         1.4 versicolor
    ## 97           6.9         3.1          4.9         1.5 versicolor
    ## 98           6.3         2.5          4.9         1.5 versicolor
    ## 99           6.7         3.0          5.0         1.7 versicolor
    ## 100          6.0         2.7          5.1         1.6 versicolor
    ## 101          4.6         3.6          1.0         0.2     setosa
    ## 102          4.3         3.0          1.1         0.1     setosa
    ## 103          5.8         4.0          1.2         0.2     setosa
    ## 104          5.0         3.2          1.2         0.2     setosa
    ## 105          4.7         3.2          1.3         0.2     setosa
    ## 106          5.4         3.9          1.3         0.4     setosa
    ## 107          5.5         3.5          1.3         0.2     setosa
    ## 108          4.4         3.0          1.3         0.2     setosa
    ## 109          5.0         3.5          1.3         0.3     setosa
    ## 110          4.5         2.3          1.3         0.3     setosa
    ## 111          4.4         3.2          1.3         0.2     setosa
    ## 112          5.1         3.5          1.4         0.2     setosa
    ## 113          4.9         3.0          1.4         0.2     setosa
    ## 114          5.0         3.6          1.4         0.2     setosa
    ## 115          4.6         3.4          1.4         0.3     setosa
    ## 116          4.4         2.9          1.4         0.2     setosa
    ## 117          4.8         3.0          1.4         0.1     setosa
    ## 118          5.1         3.5          1.4         0.3     setosa
    ## 119          5.2         3.4          1.4         0.2     setosa
    ## 120          5.5         4.2          1.4         0.2     setosa
    ## 121          4.9         3.6          1.4         0.1     setosa
    ## 122          4.8         3.0          1.4         0.3     setosa
    ## 123          4.6         3.2          1.4         0.2     setosa
    ## 124          5.0         3.3          1.4         0.2     setosa
    ## 125          4.6         3.1          1.5         0.2     setosa
    ## 126          5.0         3.4          1.5         0.2     setosa
    ## 127          4.9         3.1          1.5         0.1     setosa
    ## 128          5.4         3.7          1.5         0.2     setosa
    ## 129          5.7         4.4          1.5         0.4     setosa
    ## 130          5.1         3.8          1.5         0.3     setosa
    ## 131          5.1         3.7          1.5         0.4     setosa
    ## 132          5.2         3.5          1.5         0.2     setosa
    ## 133          5.4         3.4          1.5         0.4     setosa
    ## 134          5.2         4.1          1.5         0.1     setosa
    ## 135          4.9         3.1          1.5         0.2     setosa
    ## 136          5.1         3.4          1.5         0.2     setosa
    ## 137          5.3         3.7          1.5         0.2     setosa
    ## 138          4.8         3.4          1.6         0.2     setosa
    ## 139          5.0         3.0          1.6         0.2     setosa
    ## 140          5.0         3.4          1.6         0.4     setosa
    ## 141          4.7         3.2          1.6         0.2     setosa
    ## 142          4.8         3.1          1.6         0.2     setosa
    ## 143          5.0         3.5          1.6         0.6     setosa
    ## 144          5.1         3.8          1.6         0.2     setosa
    ## 145          5.4         3.9          1.7         0.4     setosa
    ## 146          5.7         3.8          1.7         0.3     setosa
    ## 147          5.4         3.4          1.7         0.2     setosa
    ## 148          5.1         3.3          1.7         0.5     setosa
    ## 149          4.8         3.4          1.9         0.2     setosa
    ## 150          5.1         3.8          1.9         0.4     setosa

------------------------------------------------------------------------

### Picking, dropping and re-ordering columns with `select()`

Select selects, drops or re-arranges columns of a data frame. Columns
can be referred to by name, position in the data frame or by an
expression.

> #### `select` helpers
>
> The following helper functions can be used to select columns that
> match a pattern:
>
> `starts_with()` selects columns that start with a string  
> `ends_with()` selects columns that end with a string  
> `contains()` selects columns that contain a string  
> `matches()` selects columns matching a regular expression
>
> There are also useful helpers that allow to select column on the basis
> of a character vector containing names. See `?select` for more
> details.

#### `select()` examples

Select `iris` columns 1, 2, 3 and 5:

``` r
select(iris, 1:3, 5)
```

    ##     Sepal.Length Sepal.Width Petal.Length    Species
    ## 1            5.1         3.5          1.4     setosa
    ## 2            4.9         3.0          1.4     setosa
    ## 3            4.7         3.2          1.3     setosa
    ## 4            4.6         3.1          1.5     setosa
    ## 5            5.0         3.6          1.4     setosa
    ## 6            5.4         3.9          1.7     setosa
    ## 7            4.6         3.4          1.4     setosa
    ## 8            5.0         3.4          1.5     setosa
    ## 9            4.4         2.9          1.4     setosa
    ## 10           4.9         3.1          1.5     setosa
    ## 11           5.4         3.7          1.5     setosa
    ## 12           4.8         3.4          1.6     setosa
    ## 13           4.8         3.0          1.4     setosa
    ## 14           4.3         3.0          1.1     setosa
    ## 15           5.8         4.0          1.2     setosa
    ## 16           5.7         4.4          1.5     setosa
    ## 17           5.4         3.9          1.3     setosa
    ## 18           5.1         3.5          1.4     setosa
    ## 19           5.7         3.8          1.7     setosa
    ## 20           5.1         3.8          1.5     setosa
    ## 21           5.4         3.4          1.7     setosa
    ## 22           5.1         3.7          1.5     setosa
    ## 23           4.6         3.6          1.0     setosa
    ## 24           5.1         3.3          1.7     setosa
    ## 25           4.8         3.4          1.9     setosa
    ## 26           5.0         3.0          1.6     setosa
    ## 27           5.0         3.4          1.6     setosa
    ## 28           5.2         3.5          1.5     setosa
    ## 29           5.2         3.4          1.4     setosa
    ## 30           4.7         3.2          1.6     setosa
    ## 31           4.8         3.1          1.6     setosa
    ## 32           5.4         3.4          1.5     setosa
    ## 33           5.2         4.1          1.5     setosa
    ## 34           5.5         4.2          1.4     setosa
    ## 35           4.9         3.1          1.5     setosa
    ## 36           5.0         3.2          1.2     setosa
    ## 37           5.5         3.5          1.3     setosa
    ## 38           4.9         3.6          1.4     setosa
    ## 39           4.4         3.0          1.3     setosa
    ## 40           5.1         3.4          1.5     setosa
    ## 41           5.0         3.5          1.3     setosa
    ## 42           4.5         2.3          1.3     setosa
    ## 43           4.4         3.2          1.3     setosa
    ## 44           5.0         3.5          1.6     setosa
    ## 45           5.1         3.8          1.9     setosa
    ## 46           4.8         3.0          1.4     setosa
    ## 47           5.1         3.8          1.6     setosa
    ## 48           4.6         3.2          1.4     setosa
    ## 49           5.3         3.7          1.5     setosa
    ## 50           5.0         3.3          1.4     setosa
    ## 51           7.0         3.2          4.7 versicolor
    ## 52           6.4         3.2          4.5 versicolor
    ## 53           6.9         3.1          4.9 versicolor
    ## 54           5.5         2.3          4.0 versicolor
    ## 55           6.5         2.8          4.6 versicolor
    ## 56           5.7         2.8          4.5 versicolor
    ## 57           6.3         3.3          4.7 versicolor
    ## 58           4.9         2.4          3.3 versicolor
    ## 59           6.6         2.9          4.6 versicolor
    ## 60           5.2         2.7          3.9 versicolor
    ## 61           5.0         2.0          3.5 versicolor
    ## 62           5.9         3.0          4.2 versicolor
    ## 63           6.0         2.2          4.0 versicolor
    ## 64           6.1         2.9          4.7 versicolor
    ## 65           5.6         2.9          3.6 versicolor
    ## 66           6.7         3.1          4.4 versicolor
    ## 67           5.6         3.0          4.5 versicolor
    ## 68           5.8         2.7          4.1 versicolor
    ## 69           6.2         2.2          4.5 versicolor
    ## 70           5.6         2.5          3.9 versicolor
    ## 71           5.9         3.2          4.8 versicolor
    ## 72           6.1         2.8          4.0 versicolor
    ## 73           6.3         2.5          4.9 versicolor
    ## 74           6.1         2.8          4.7 versicolor
    ## 75           6.4         2.9          4.3 versicolor
    ## 76           6.6         3.0          4.4 versicolor
    ## 77           6.8         2.8          4.8 versicolor
    ## 78           6.7         3.0          5.0 versicolor
    ## 79           6.0         2.9          4.5 versicolor
    ## 80           5.7         2.6          3.5 versicolor
    ## 81           5.5         2.4          3.8 versicolor
    ## 82           5.5         2.4          3.7 versicolor
    ## 83           5.8         2.7          3.9 versicolor
    ## 84           6.0         2.7          5.1 versicolor
    ## 85           5.4         3.0          4.5 versicolor
    ## 86           6.0         3.4          4.5 versicolor
    ## 87           6.7         3.1          4.7 versicolor
    ## 88           6.3         2.3          4.4 versicolor
    ## 89           5.6         3.0          4.1 versicolor
    ## 90           5.5         2.5          4.0 versicolor
    ## 91           5.5         2.6          4.4 versicolor
    ## 92           6.1         3.0          4.6 versicolor
    ## 93           5.8         2.6          4.0 versicolor
    ## 94           5.0         2.3          3.3 versicolor
    ## 95           5.6         2.7          4.2 versicolor
    ## 96           5.7         3.0          4.2 versicolor
    ## 97           5.7         2.9          4.2 versicolor
    ## 98           6.2         2.9          4.3 versicolor
    ## 99           5.1         2.5          3.0 versicolor
    ## 100          5.7         2.8          4.1 versicolor
    ## 101          6.3         3.3          6.0  virginica
    ## 102          5.8         2.7          5.1  virginica
    ## 103          7.1         3.0          5.9  virginica
    ## 104          6.3         2.9          5.6  virginica
    ## 105          6.5         3.0          5.8  virginica
    ## 106          7.6         3.0          6.6  virginica
    ## 107          4.9         2.5          4.5  virginica
    ## 108          7.3         2.9          6.3  virginica
    ## 109          6.7         2.5          5.8  virginica
    ## 110          7.2         3.6          6.1  virginica
    ## 111          6.5         3.2          5.1  virginica
    ## 112          6.4         2.7          5.3  virginica
    ## 113          6.8         3.0          5.5  virginica
    ## 114          5.7         2.5          5.0  virginica
    ## 115          5.8         2.8          5.1  virginica
    ## 116          6.4         3.2          5.3  virginica
    ## 117          6.5         3.0          5.5  virginica
    ## 118          7.7         3.8          6.7  virginica
    ## 119          7.7         2.6          6.9  virginica
    ## 120          6.0         2.2          5.0  virginica
    ## 121          6.9         3.2          5.7  virginica
    ## 122          5.6         2.8          4.9  virginica
    ## 123          7.7         2.8          6.7  virginica
    ## 124          6.3         2.7          4.9  virginica
    ## 125          6.7         3.3          5.7  virginica
    ## 126          7.2         3.2          6.0  virginica
    ## 127          6.2         2.8          4.8  virginica
    ## 128          6.1         3.0          4.9  virginica
    ## 129          6.4         2.8          5.6  virginica
    ## 130          7.2         3.0          5.8  virginica
    ## 131          7.4         2.8          6.1  virginica
    ## 132          7.9         3.8          6.4  virginica
    ## 133          6.4         2.8          5.6  virginica
    ## 134          6.3         2.8          5.1  virginica
    ## 135          6.1         2.6          5.6  virginica
    ## 136          7.7         3.0          6.1  virginica
    ## 137          6.3         3.4          5.6  virginica
    ## 138          6.4         3.1          5.5  virginica
    ## 139          6.0         3.0          4.8  virginica
    ## 140          6.9         3.1          5.4  virginica
    ## 141          6.7         3.1          5.6  virginica
    ## 142          6.9         3.1          5.1  virginica
    ## 143          5.8         2.7          5.1  virginica
    ## 144          6.8         3.2          5.9  virginica
    ## 145          6.7         3.3          5.7  virginica
    ## 146          6.7         3.0          5.2  virginica
    ## 147          6.3         2.5          5.0  virginica
    ## 148          6.5         3.0          5.2  virginica
    ## 149          6.2         3.4          5.4  virginica
    ## 150          5.9         3.0          5.1  virginica

or, just drop column 4:

``` r
select(iris, -4)
```

    ##     Sepal.Length Sepal.Width Petal.Length    Species
    ## 1            5.1         3.5          1.4     setosa
    ## 2            4.9         3.0          1.4     setosa
    ## 3            4.7         3.2          1.3     setosa
    ## 4            4.6         3.1          1.5     setosa
    ## 5            5.0         3.6          1.4     setosa
    ## 6            5.4         3.9          1.7     setosa
    ## 7            4.6         3.4          1.4     setosa
    ## 8            5.0         3.4          1.5     setosa
    ## 9            4.4         2.9          1.4     setosa
    ## 10           4.9         3.1          1.5     setosa
    ## 11           5.4         3.7          1.5     setosa
    ## 12           4.8         3.4          1.6     setosa
    ## 13           4.8         3.0          1.4     setosa
    ## 14           4.3         3.0          1.1     setosa
    ## 15           5.8         4.0          1.2     setosa
    ## 16           5.7         4.4          1.5     setosa
    ## 17           5.4         3.9          1.3     setosa
    ## 18           5.1         3.5          1.4     setosa
    ## 19           5.7         3.8          1.7     setosa
    ## 20           5.1         3.8          1.5     setosa
    ## 21           5.4         3.4          1.7     setosa
    ## 22           5.1         3.7          1.5     setosa
    ## 23           4.6         3.6          1.0     setosa
    ## 24           5.1         3.3          1.7     setosa
    ## 25           4.8         3.4          1.9     setosa
    ## 26           5.0         3.0          1.6     setosa
    ## 27           5.0         3.4          1.6     setosa
    ## 28           5.2         3.5          1.5     setosa
    ## 29           5.2         3.4          1.4     setosa
    ## 30           4.7         3.2          1.6     setosa
    ## 31           4.8         3.1          1.6     setosa
    ## 32           5.4         3.4          1.5     setosa
    ## 33           5.2         4.1          1.5     setosa
    ## 34           5.5         4.2          1.4     setosa
    ## 35           4.9         3.1          1.5     setosa
    ## 36           5.0         3.2          1.2     setosa
    ## 37           5.5         3.5          1.3     setosa
    ## 38           4.9         3.6          1.4     setosa
    ## 39           4.4         3.0          1.3     setosa
    ## 40           5.1         3.4          1.5     setosa
    ## 41           5.0         3.5          1.3     setosa
    ## 42           4.5         2.3          1.3     setosa
    ## 43           4.4         3.2          1.3     setosa
    ## 44           5.0         3.5          1.6     setosa
    ## 45           5.1         3.8          1.9     setosa
    ## 46           4.8         3.0          1.4     setosa
    ## 47           5.1         3.8          1.6     setosa
    ## 48           4.6         3.2          1.4     setosa
    ## 49           5.3         3.7          1.5     setosa
    ## 50           5.0         3.3          1.4     setosa
    ## 51           7.0         3.2          4.7 versicolor
    ## 52           6.4         3.2          4.5 versicolor
    ## 53           6.9         3.1          4.9 versicolor
    ## 54           5.5         2.3          4.0 versicolor
    ## 55           6.5         2.8          4.6 versicolor
    ## 56           5.7         2.8          4.5 versicolor
    ## 57           6.3         3.3          4.7 versicolor
    ## 58           4.9         2.4          3.3 versicolor
    ## 59           6.6         2.9          4.6 versicolor
    ## 60           5.2         2.7          3.9 versicolor
    ## 61           5.0         2.0          3.5 versicolor
    ## 62           5.9         3.0          4.2 versicolor
    ## 63           6.0         2.2          4.0 versicolor
    ## 64           6.1         2.9          4.7 versicolor
    ## 65           5.6         2.9          3.6 versicolor
    ## 66           6.7         3.1          4.4 versicolor
    ## 67           5.6         3.0          4.5 versicolor
    ## 68           5.8         2.7          4.1 versicolor
    ## 69           6.2         2.2          4.5 versicolor
    ## 70           5.6         2.5          3.9 versicolor
    ## 71           5.9         3.2          4.8 versicolor
    ## 72           6.1         2.8          4.0 versicolor
    ## 73           6.3         2.5          4.9 versicolor
    ## 74           6.1         2.8          4.7 versicolor
    ## 75           6.4         2.9          4.3 versicolor
    ## 76           6.6         3.0          4.4 versicolor
    ## 77           6.8         2.8          4.8 versicolor
    ## 78           6.7         3.0          5.0 versicolor
    ## 79           6.0         2.9          4.5 versicolor
    ## 80           5.7         2.6          3.5 versicolor
    ## 81           5.5         2.4          3.8 versicolor
    ## 82           5.5         2.4          3.7 versicolor
    ## 83           5.8         2.7          3.9 versicolor
    ## 84           6.0         2.7          5.1 versicolor
    ## 85           5.4         3.0          4.5 versicolor
    ## 86           6.0         3.4          4.5 versicolor
    ## 87           6.7         3.1          4.7 versicolor
    ## 88           6.3         2.3          4.4 versicolor
    ## 89           5.6         3.0          4.1 versicolor
    ## 90           5.5         2.5          4.0 versicolor
    ## 91           5.5         2.6          4.4 versicolor
    ## 92           6.1         3.0          4.6 versicolor
    ## 93           5.8         2.6          4.0 versicolor
    ## 94           5.0         2.3          3.3 versicolor
    ## 95           5.6         2.7          4.2 versicolor
    ## 96           5.7         3.0          4.2 versicolor
    ## 97           5.7         2.9          4.2 versicolor
    ## 98           6.2         2.9          4.3 versicolor
    ## 99           5.1         2.5          3.0 versicolor
    ## 100          5.7         2.8          4.1 versicolor
    ## 101          6.3         3.3          6.0  virginica
    ## 102          5.8         2.7          5.1  virginica
    ## 103          7.1         3.0          5.9  virginica
    ## 104          6.3         2.9          5.6  virginica
    ## 105          6.5         3.0          5.8  virginica
    ## 106          7.6         3.0          6.6  virginica
    ## 107          4.9         2.5          4.5  virginica
    ## 108          7.3         2.9          6.3  virginica
    ## 109          6.7         2.5          5.8  virginica
    ## 110          7.2         3.6          6.1  virginica
    ## 111          6.5         3.2          5.1  virginica
    ## 112          6.4         2.7          5.3  virginica
    ## 113          6.8         3.0          5.5  virginica
    ## 114          5.7         2.5          5.0  virginica
    ## 115          5.8         2.8          5.1  virginica
    ## 116          6.4         3.2          5.3  virginica
    ## 117          6.5         3.0          5.5  virginica
    ## 118          7.7         3.8          6.7  virginica
    ## 119          7.7         2.6          6.9  virginica
    ## 120          6.0         2.2          5.0  virginica
    ## 121          6.9         3.2          5.7  virginica
    ## 122          5.6         2.8          4.9  virginica
    ## 123          7.7         2.8          6.7  virginica
    ## 124          6.3         2.7          4.9  virginica
    ## 125          6.7         3.3          5.7  virginica
    ## 126          7.2         3.2          6.0  virginica
    ## 127          6.2         2.8          4.8  virginica
    ## 128          6.1         3.0          4.9  virginica
    ## 129          6.4         2.8          5.6  virginica
    ## 130          7.2         3.0          5.8  virginica
    ## 131          7.4         2.8          6.1  virginica
    ## 132          7.9         3.8          6.4  virginica
    ## 133          6.4         2.8          5.6  virginica
    ## 134          6.3         2.8          5.1  virginica
    ## 135          6.1         2.6          5.6  virginica
    ## 136          7.7         3.0          6.1  virginica
    ## 137          6.3         3.4          5.6  virginica
    ## 138          6.4         3.1          5.5  virginica
    ## 139          6.0         3.0          4.8  virginica
    ## 140          6.9         3.1          5.4  virginica
    ## 141          6.7         3.1          5.6  virginica
    ## 142          6.9         3.1          5.1  virginica
    ## 143          5.8         2.7          5.1  virginica
    ## 144          6.8         3.2          5.9  virginica
    ## 145          6.7         3.3          5.7  virginica
    ## 146          6.7         3.0          5.2  virginica
    ## 147          6.3         2.5          5.0  virginica
    ## 148          6.5         3.0          5.2  virginica
    ## 149          6.2         3.4          5.4  virginica
    ## 150          5.9         3.0          5.1  virginica

Select species name and petal measurements:

``` r
select(iris, Species, starts_with("Petal"))
```

    ##        Species Petal.Length Petal.Width
    ## 1       setosa          1.4         0.2
    ## 2       setosa          1.4         0.2
    ## 3       setosa          1.3         0.2
    ## 4       setosa          1.5         0.2
    ## 5       setosa          1.4         0.2
    ## 6       setosa          1.7         0.4
    ## 7       setosa          1.4         0.3
    ## 8       setosa          1.5         0.2
    ## 9       setosa          1.4         0.2
    ## 10      setosa          1.5         0.1
    ## 11      setosa          1.5         0.2
    ## 12      setosa          1.6         0.2
    ## 13      setosa          1.4         0.1
    ## 14      setosa          1.1         0.1
    ## 15      setosa          1.2         0.2
    ## 16      setosa          1.5         0.4
    ## 17      setosa          1.3         0.4
    ## 18      setosa          1.4         0.3
    ## 19      setosa          1.7         0.3
    ## 20      setosa          1.5         0.3
    ## 21      setosa          1.7         0.2
    ## 22      setosa          1.5         0.4
    ## 23      setosa          1.0         0.2
    ## 24      setosa          1.7         0.5
    ## 25      setosa          1.9         0.2
    ## 26      setosa          1.6         0.2
    ## 27      setosa          1.6         0.4
    ## 28      setosa          1.5         0.2
    ## 29      setosa          1.4         0.2
    ## 30      setosa          1.6         0.2
    ## 31      setosa          1.6         0.2
    ## 32      setosa          1.5         0.4
    ## 33      setosa          1.5         0.1
    ## 34      setosa          1.4         0.2
    ## 35      setosa          1.5         0.2
    ## 36      setosa          1.2         0.2
    ## 37      setosa          1.3         0.2
    ## 38      setosa          1.4         0.1
    ## 39      setosa          1.3         0.2
    ## 40      setosa          1.5         0.2
    ## 41      setosa          1.3         0.3
    ## 42      setosa          1.3         0.3
    ## 43      setosa          1.3         0.2
    ## 44      setosa          1.6         0.6
    ## 45      setosa          1.9         0.4
    ## 46      setosa          1.4         0.3
    ## 47      setosa          1.6         0.2
    ## 48      setosa          1.4         0.2
    ## 49      setosa          1.5         0.2
    ## 50      setosa          1.4         0.2
    ## 51  versicolor          4.7         1.4
    ## 52  versicolor          4.5         1.5
    ## 53  versicolor          4.9         1.5
    ## 54  versicolor          4.0         1.3
    ## 55  versicolor          4.6         1.5
    ## 56  versicolor          4.5         1.3
    ## 57  versicolor          4.7         1.6
    ## 58  versicolor          3.3         1.0
    ## 59  versicolor          4.6         1.3
    ## 60  versicolor          3.9         1.4
    ## 61  versicolor          3.5         1.0
    ## 62  versicolor          4.2         1.5
    ## 63  versicolor          4.0         1.0
    ## 64  versicolor          4.7         1.4
    ## 65  versicolor          3.6         1.3
    ## 66  versicolor          4.4         1.4
    ## 67  versicolor          4.5         1.5
    ## 68  versicolor          4.1         1.0
    ## 69  versicolor          4.5         1.5
    ## 70  versicolor          3.9         1.1
    ## 71  versicolor          4.8         1.8
    ## 72  versicolor          4.0         1.3
    ## 73  versicolor          4.9         1.5
    ## 74  versicolor          4.7         1.2
    ## 75  versicolor          4.3         1.3
    ## 76  versicolor          4.4         1.4
    ## 77  versicolor          4.8         1.4
    ## 78  versicolor          5.0         1.7
    ## 79  versicolor          4.5         1.5
    ## 80  versicolor          3.5         1.0
    ## 81  versicolor          3.8         1.1
    ## 82  versicolor          3.7         1.0
    ## 83  versicolor          3.9         1.2
    ## 84  versicolor          5.1         1.6
    ## 85  versicolor          4.5         1.5
    ## 86  versicolor          4.5         1.6
    ## 87  versicolor          4.7         1.5
    ## 88  versicolor          4.4         1.3
    ## 89  versicolor          4.1         1.3
    ## 90  versicolor          4.0         1.3
    ## 91  versicolor          4.4         1.2
    ## 92  versicolor          4.6         1.4
    ## 93  versicolor          4.0         1.2
    ## 94  versicolor          3.3         1.0
    ## 95  versicolor          4.2         1.3
    ## 96  versicolor          4.2         1.2
    ## 97  versicolor          4.2         1.3
    ## 98  versicolor          4.3         1.3
    ## 99  versicolor          3.0         1.1
    ## 100 versicolor          4.1         1.3
    ## 101  virginica          6.0         2.5
    ## 102  virginica          5.1         1.9
    ## 103  virginica          5.9         2.1
    ## 104  virginica          5.6         1.8
    ## 105  virginica          5.8         2.2
    ## 106  virginica          6.6         2.1
    ## 107  virginica          4.5         1.7
    ## 108  virginica          6.3         1.8
    ## 109  virginica          5.8         1.8
    ## 110  virginica          6.1         2.5
    ## 111  virginica          5.1         2.0
    ## 112  virginica          5.3         1.9
    ## 113  virginica          5.5         2.1
    ## 114  virginica          5.0         2.0
    ## 115  virginica          5.1         2.4
    ## 116  virginica          5.3         2.3
    ## 117  virginica          5.5         1.8
    ## 118  virginica          6.7         2.2
    ## 119  virginica          6.9         2.3
    ## 120  virginica          5.0         1.5
    ## 121  virginica          5.7         2.3
    ## 122  virginica          4.9         2.0
    ## 123  virginica          6.7         2.0
    ## 124  virginica          4.9         1.8
    ## 125  virginica          5.7         2.1
    ## 126  virginica          6.0         1.8
    ## 127  virginica          4.8         1.8
    ## 128  virginica          4.9         1.8
    ## 129  virginica          5.6         2.1
    ## 130  virginica          5.8         1.6
    ## 131  virginica          6.1         1.9
    ## 132  virginica          6.4         2.0
    ## 133  virginica          5.6         2.2
    ## 134  virginica          5.1         1.5
    ## 135  virginica          5.6         1.4
    ## 136  virginica          6.1         2.3
    ## 137  virginica          5.6         2.4
    ## 138  virginica          5.5         1.8
    ## 139  virginica          4.8         1.8
    ## 140  virginica          5.4         2.1
    ## 141  virginica          5.6         2.4
    ## 142  virginica          5.1         2.3
    ## 143  virginica          5.1         1.9
    ## 144  virginica          5.9         2.3
    ## 145  virginica          5.7         2.5
    ## 146  virginica          5.2         2.3
    ## 147  virginica          5.0         1.9
    ## 148  virginica          5.2         2.0
    ## 149  virginica          5.4         2.3
    ## 150  virginica          5.1         1.8

The example above shows that `select()` can be used to reorder
variables. A useful trick to move a single column (here `Species`) to
the beginning of the data frame:

``` r
select(iris, Species, everything())
```

    ##        Species Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## 1       setosa          5.1         3.5          1.4         0.2
    ## 2       setosa          4.9         3.0          1.4         0.2
    ## 3       setosa          4.7         3.2          1.3         0.2
    ## 4       setosa          4.6         3.1          1.5         0.2
    ## 5       setosa          5.0         3.6          1.4         0.2
    ## 6       setosa          5.4         3.9          1.7         0.4
    ## 7       setosa          4.6         3.4          1.4         0.3
    ## 8       setosa          5.0         3.4          1.5         0.2
    ## 9       setosa          4.4         2.9          1.4         0.2
    ## 10      setosa          4.9         3.1          1.5         0.1
    ## 11      setosa          5.4         3.7          1.5         0.2
    ## 12      setosa          4.8         3.4          1.6         0.2
    ## 13      setosa          4.8         3.0          1.4         0.1
    ## 14      setosa          4.3         3.0          1.1         0.1
    ## 15      setosa          5.8         4.0          1.2         0.2
    ## 16      setosa          5.7         4.4          1.5         0.4
    ## 17      setosa          5.4         3.9          1.3         0.4
    ## 18      setosa          5.1         3.5          1.4         0.3
    ## 19      setosa          5.7         3.8          1.7         0.3
    ## 20      setosa          5.1         3.8          1.5         0.3
    ## 21      setosa          5.4         3.4          1.7         0.2
    ## 22      setosa          5.1         3.7          1.5         0.4
    ## 23      setosa          4.6         3.6          1.0         0.2
    ## 24      setosa          5.1         3.3          1.7         0.5
    ## 25      setosa          4.8         3.4          1.9         0.2
    ## 26      setosa          5.0         3.0          1.6         0.2
    ## 27      setosa          5.0         3.4          1.6         0.4
    ## 28      setosa          5.2         3.5          1.5         0.2
    ## 29      setosa          5.2         3.4          1.4         0.2
    ## 30      setosa          4.7         3.2          1.6         0.2
    ## 31      setosa          4.8         3.1          1.6         0.2
    ## 32      setosa          5.4         3.4          1.5         0.4
    ## 33      setosa          5.2         4.1          1.5         0.1
    ## 34      setosa          5.5         4.2          1.4         0.2
    ## 35      setosa          4.9         3.1          1.5         0.2
    ## 36      setosa          5.0         3.2          1.2         0.2
    ## 37      setosa          5.5         3.5          1.3         0.2
    ## 38      setosa          4.9         3.6          1.4         0.1
    ## 39      setosa          4.4         3.0          1.3         0.2
    ## 40      setosa          5.1         3.4          1.5         0.2
    ## 41      setosa          5.0         3.5          1.3         0.3
    ## 42      setosa          4.5         2.3          1.3         0.3
    ## 43      setosa          4.4         3.2          1.3         0.2
    ## 44      setosa          5.0         3.5          1.6         0.6
    ## 45      setosa          5.1         3.8          1.9         0.4
    ## 46      setosa          4.8         3.0          1.4         0.3
    ## 47      setosa          5.1         3.8          1.6         0.2
    ## 48      setosa          4.6         3.2          1.4         0.2
    ## 49      setosa          5.3         3.7          1.5         0.2
    ## 50      setosa          5.0         3.3          1.4         0.2
    ## 51  versicolor          7.0         3.2          4.7         1.4
    ## 52  versicolor          6.4         3.2          4.5         1.5
    ## 53  versicolor          6.9         3.1          4.9         1.5
    ## 54  versicolor          5.5         2.3          4.0         1.3
    ## 55  versicolor          6.5         2.8          4.6         1.5
    ## 56  versicolor          5.7         2.8          4.5         1.3
    ## 57  versicolor          6.3         3.3          4.7         1.6
    ## 58  versicolor          4.9         2.4          3.3         1.0
    ## 59  versicolor          6.6         2.9          4.6         1.3
    ## 60  versicolor          5.2         2.7          3.9         1.4
    ## 61  versicolor          5.0         2.0          3.5         1.0
    ## 62  versicolor          5.9         3.0          4.2         1.5
    ## 63  versicolor          6.0         2.2          4.0         1.0
    ## 64  versicolor          6.1         2.9          4.7         1.4
    ## 65  versicolor          5.6         2.9          3.6         1.3
    ## 66  versicolor          6.7         3.1          4.4         1.4
    ## 67  versicolor          5.6         3.0          4.5         1.5
    ## 68  versicolor          5.8         2.7          4.1         1.0
    ## 69  versicolor          6.2         2.2          4.5         1.5
    ## 70  versicolor          5.6         2.5          3.9         1.1
    ## 71  versicolor          5.9         3.2          4.8         1.8
    ## 72  versicolor          6.1         2.8          4.0         1.3
    ## 73  versicolor          6.3         2.5          4.9         1.5
    ## 74  versicolor          6.1         2.8          4.7         1.2
    ## 75  versicolor          6.4         2.9          4.3         1.3
    ## 76  versicolor          6.6         3.0          4.4         1.4
    ## 77  versicolor          6.8         2.8          4.8         1.4
    ## 78  versicolor          6.7         3.0          5.0         1.7
    ## 79  versicolor          6.0         2.9          4.5         1.5
    ## 80  versicolor          5.7         2.6          3.5         1.0
    ## 81  versicolor          5.5         2.4          3.8         1.1
    ## 82  versicolor          5.5         2.4          3.7         1.0
    ## 83  versicolor          5.8         2.7          3.9         1.2
    ## 84  versicolor          6.0         2.7          5.1         1.6
    ## 85  versicolor          5.4         3.0          4.5         1.5
    ## 86  versicolor          6.0         3.4          4.5         1.6
    ## 87  versicolor          6.7         3.1          4.7         1.5
    ## 88  versicolor          6.3         2.3          4.4         1.3
    ## 89  versicolor          5.6         3.0          4.1         1.3
    ## 90  versicolor          5.5         2.5          4.0         1.3
    ## 91  versicolor          5.5         2.6          4.4         1.2
    ## 92  versicolor          6.1         3.0          4.6         1.4
    ## 93  versicolor          5.8         2.6          4.0         1.2
    ## 94  versicolor          5.0         2.3          3.3         1.0
    ## 95  versicolor          5.6         2.7          4.2         1.3
    ## 96  versicolor          5.7         3.0          4.2         1.2
    ## 97  versicolor          5.7         2.9          4.2         1.3
    ## 98  versicolor          6.2         2.9          4.3         1.3
    ## 99  versicolor          5.1         2.5          3.0         1.1
    ## 100 versicolor          5.7         2.8          4.1         1.3
    ## 101  virginica          6.3         3.3          6.0         2.5
    ## 102  virginica          5.8         2.7          5.1         1.9
    ## 103  virginica          7.1         3.0          5.9         2.1
    ## 104  virginica          6.3         2.9          5.6         1.8
    ## 105  virginica          6.5         3.0          5.8         2.2
    ## 106  virginica          7.6         3.0          6.6         2.1
    ## 107  virginica          4.9         2.5          4.5         1.7
    ## 108  virginica          7.3         2.9          6.3         1.8
    ## 109  virginica          6.7         2.5          5.8         1.8
    ## 110  virginica          7.2         3.6          6.1         2.5
    ## 111  virginica          6.5         3.2          5.1         2.0
    ## 112  virginica          6.4         2.7          5.3         1.9
    ## 113  virginica          6.8         3.0          5.5         2.1
    ## 114  virginica          5.7         2.5          5.0         2.0
    ## 115  virginica          5.8         2.8          5.1         2.4
    ## 116  virginica          6.4         3.2          5.3         2.3
    ## 117  virginica          6.5         3.0          5.5         1.8
    ## 118  virginica          7.7         3.8          6.7         2.2
    ## 119  virginica          7.7         2.6          6.9         2.3
    ## 120  virginica          6.0         2.2          5.0         1.5
    ## 121  virginica          6.9         3.2          5.7         2.3
    ## 122  virginica          5.6         2.8          4.9         2.0
    ## 123  virginica          7.7         2.8          6.7         2.0
    ## 124  virginica          6.3         2.7          4.9         1.8
    ## 125  virginica          6.7         3.3          5.7         2.1
    ## 126  virginica          7.2         3.2          6.0         1.8
    ## 127  virginica          6.2         2.8          4.8         1.8
    ## 128  virginica          6.1         3.0          4.9         1.8
    ## 129  virginica          6.4         2.8          5.6         2.1
    ## 130  virginica          7.2         3.0          5.8         1.6
    ## 131  virginica          7.4         2.8          6.1         1.9
    ## 132  virginica          7.9         3.8          6.4         2.0
    ## 133  virginica          6.4         2.8          5.6         2.2
    ## 134  virginica          6.3         2.8          5.1         1.5
    ## 135  virginica          6.1         2.6          5.6         1.4
    ## 136  virginica          7.7         3.0          6.1         2.3
    ## 137  virginica          6.3         3.4          5.6         2.4
    ## 138  virginica          6.4         3.1          5.5         1.8
    ## 139  virginica          6.0         3.0          4.8         1.8
    ## 140  virginica          6.9         3.1          5.4         2.1
    ## 141  virginica          6.7         3.1          5.6         2.4
    ## 142  virginica          6.9         3.1          5.1         2.3
    ## 143  virginica          5.8         2.7          5.1         1.9
    ## 144  virginica          6.8         3.2          5.9         2.3
    ## 145  virginica          6.7         3.3          5.7         2.5
    ## 146  virginica          6.7         3.0          5.2         2.3
    ## 147  virginica          6.3         2.5          5.0         1.9
    ## 148  virginica          6.5         3.0          5.2         2.0
    ## 149  virginica          6.2         3.4          5.4         2.3
    ## 150  virginica          5.9         3.0          5.1         1.8

#### Exercise 12

Select width measurements and species from `iris`, at the same time
relocating species to the beginning of the data frame.

Expected result:

    ##        Species Sepal.Width Petal.Width
    ## 1       setosa         3.5         0.2
    ## 2       setosa         3.0         0.2
    ## 3       setosa         3.2         0.2
    ## 4       setosa         3.1         0.2
    ## 5       setosa         3.6         0.2
    ## 6       setosa         3.9         0.4
    ## 7       setosa         3.4         0.3
    ## 8       setosa         3.4         0.2
    ## 9       setosa         2.9         0.2
    ## 10      setosa         3.1         0.1
    ## 11      setosa         3.7         0.2
    ## 12      setosa         3.4         0.2
    ## 13      setosa         3.0         0.1
    ## 14      setosa         3.0         0.1
    ## 15      setosa         4.0         0.2
    ## 16      setosa         4.4         0.4
    ## 17      setosa         3.9         0.4
    ## 18      setosa         3.5         0.3
    ## 19      setosa         3.8         0.3
    ## 20      setosa         3.8         0.3
    ## 21      setosa         3.4         0.2
    ## 22      setosa         3.7         0.4
    ## 23      setosa         3.6         0.2
    ## 24      setosa         3.3         0.5
    ## 25      setosa         3.4         0.2
    ## 26      setosa         3.0         0.2
    ## 27      setosa         3.4         0.4
    ## 28      setosa         3.5         0.2
    ## 29      setosa         3.4         0.2
    ## 30      setosa         3.2         0.2
    ## 31      setosa         3.1         0.2
    ## 32      setosa         3.4         0.4
    ## 33      setosa         4.1         0.1
    ## 34      setosa         4.2         0.2
    ## 35      setosa         3.1         0.2
    ## 36      setosa         3.2         0.2
    ## 37      setosa         3.5         0.2
    ## 38      setosa         3.6         0.1
    ## 39      setosa         3.0         0.2
    ## 40      setosa         3.4         0.2
    ## 41      setosa         3.5         0.3
    ## 42      setosa         2.3         0.3
    ## 43      setosa         3.2         0.2
    ## 44      setosa         3.5         0.6
    ## 45      setosa         3.8         0.4
    ## 46      setosa         3.0         0.3
    ## 47      setosa         3.8         0.2
    ## 48      setosa         3.2         0.2
    ## 49      setosa         3.7         0.2
    ## 50      setosa         3.3         0.2
    ## 51  versicolor         3.2         1.4
    ## 52  versicolor         3.2         1.5
    ## 53  versicolor         3.1         1.5
    ## 54  versicolor         2.3         1.3
    ## 55  versicolor         2.8         1.5
    ## 56  versicolor         2.8         1.3
    ## 57  versicolor         3.3         1.6
    ## 58  versicolor         2.4         1.0
    ## 59  versicolor         2.9         1.3
    ## 60  versicolor         2.7         1.4
    ## 61  versicolor         2.0         1.0
    ## 62  versicolor         3.0         1.5
    ## 63  versicolor         2.2         1.0
    ## 64  versicolor         2.9         1.4
    ## 65  versicolor         2.9         1.3
    ## 66  versicolor         3.1         1.4
    ## 67  versicolor         3.0         1.5
    ## 68  versicolor         2.7         1.0
    ## 69  versicolor         2.2         1.5
    ## 70  versicolor         2.5         1.1
    ## 71  versicolor         3.2         1.8
    ## 72  versicolor         2.8         1.3
    ## 73  versicolor         2.5         1.5
    ## 74  versicolor         2.8         1.2
    ## 75  versicolor         2.9         1.3
    ## 76  versicolor         3.0         1.4
    ## 77  versicolor         2.8         1.4
    ## 78  versicolor         3.0         1.7
    ## 79  versicolor         2.9         1.5
    ## 80  versicolor         2.6         1.0
    ## 81  versicolor         2.4         1.1
    ## 82  versicolor         2.4         1.0
    ## 83  versicolor         2.7         1.2
    ## 84  versicolor         2.7         1.6
    ## 85  versicolor         3.0         1.5
    ## 86  versicolor         3.4         1.6
    ## 87  versicolor         3.1         1.5
    ## 88  versicolor         2.3         1.3
    ## 89  versicolor         3.0         1.3
    ## 90  versicolor         2.5         1.3
    ## 91  versicolor         2.6         1.2
    ## 92  versicolor         3.0         1.4
    ## 93  versicolor         2.6         1.2
    ## 94  versicolor         2.3         1.0
    ## 95  versicolor         2.7         1.3
    ## 96  versicolor         3.0         1.2
    ## 97  versicolor         2.9         1.3
    ## 98  versicolor         2.9         1.3
    ## 99  versicolor         2.5         1.1
    ## 100 versicolor         2.8         1.3
    ## 101  virginica         3.3         2.5
    ## 102  virginica         2.7         1.9
    ## 103  virginica         3.0         2.1
    ## 104  virginica         2.9         1.8
    ## 105  virginica         3.0         2.2
    ## 106  virginica         3.0         2.1
    ## 107  virginica         2.5         1.7
    ## 108  virginica         2.9         1.8
    ## 109  virginica         2.5         1.8
    ## 110  virginica         3.6         2.5
    ## 111  virginica         3.2         2.0
    ## 112  virginica         2.7         1.9
    ## 113  virginica         3.0         2.1
    ## 114  virginica         2.5         2.0
    ## 115  virginica         2.8         2.4
    ## 116  virginica         3.2         2.3
    ## 117  virginica         3.0         1.8
    ## 118  virginica         3.8         2.2
    ## 119  virginica         2.6         2.3
    ## 120  virginica         2.2         1.5
    ## 121  virginica         3.2         2.3
    ## 122  virginica         2.8         2.0
    ## 123  virginica         2.8         2.0
    ## 124  virginica         2.7         1.8
    ## 125  virginica         3.3         2.1
    ## 126  virginica         3.2         1.8
    ## 127  virginica         2.8         1.8
    ## 128  virginica         3.0         1.8
    ## 129  virginica         2.8         2.1
    ## 130  virginica         3.0         1.6
    ## 131  virginica         2.8         1.9
    ## 132  virginica         3.8         2.0
    ## 133  virginica         2.8         2.2
    ## 134  virginica         2.8         1.5
    ## 135  virginica         2.6         1.4
    ## 136  virginica         3.0         2.3
    ## 137  virginica         3.4         2.4
    ## 138  virginica         3.1         1.8
    ## 139  virginica         3.0         1.8
    ## 140  virginica         3.1         2.1
    ## 141  virginica         3.1         2.4
    ## 142  virginica         3.1         2.3
    ## 143  virginica         2.7         1.9
    ## 144  virginica         3.2         2.3
    ## 145  virginica         3.3         2.5
    ## 146  virginica         3.0         2.3
    ## 147  virginica         2.5         1.9
    ## 148  virginica         3.0         2.0
    ## 149  virginica         3.4         2.3
    ## 150  virginica         3.0         1.8

------------------------------------------------------------------------

#### Exercise 13

Drop petal measurements from `iris` data frame.

Expected result:

    ##     Sepal.Length Sepal.Width    Species
    ## 1            5.1         3.5     setosa
    ## 2            4.9         3.0     setosa
    ## 3            4.7         3.2     setosa
    ## 4            4.6         3.1     setosa
    ## 5            5.0         3.6     setosa
    ## 6            5.4         3.9     setosa
    ## 7            4.6         3.4     setosa
    ## 8            5.0         3.4     setosa
    ## 9            4.4         2.9     setosa
    ## 10           4.9         3.1     setosa
    ## 11           5.4         3.7     setosa
    ## 12           4.8         3.4     setosa
    ## 13           4.8         3.0     setosa
    ## 14           4.3         3.0     setosa
    ## 15           5.8         4.0     setosa
    ## 16           5.7         4.4     setosa
    ## 17           5.4         3.9     setosa
    ## 18           5.1         3.5     setosa
    ## 19           5.7         3.8     setosa
    ## 20           5.1         3.8     setosa
    ## 21           5.4         3.4     setosa
    ## 22           5.1         3.7     setosa
    ## 23           4.6         3.6     setosa
    ## 24           5.1         3.3     setosa
    ## 25           4.8         3.4     setosa
    ## 26           5.0         3.0     setosa
    ## 27           5.0         3.4     setosa
    ## 28           5.2         3.5     setosa
    ## 29           5.2         3.4     setosa
    ## 30           4.7         3.2     setosa
    ## 31           4.8         3.1     setosa
    ## 32           5.4         3.4     setosa
    ## 33           5.2         4.1     setosa
    ## 34           5.5         4.2     setosa
    ## 35           4.9         3.1     setosa
    ## 36           5.0         3.2     setosa
    ## 37           5.5         3.5     setosa
    ## 38           4.9         3.6     setosa
    ## 39           4.4         3.0     setosa
    ## 40           5.1         3.4     setosa
    ## 41           5.0         3.5     setosa
    ## 42           4.5         2.3     setosa
    ## 43           4.4         3.2     setosa
    ## 44           5.0         3.5     setosa
    ## 45           5.1         3.8     setosa
    ## 46           4.8         3.0     setosa
    ## 47           5.1         3.8     setosa
    ## 48           4.6         3.2     setosa
    ## 49           5.3         3.7     setosa
    ## 50           5.0         3.3     setosa
    ## 51           7.0         3.2 versicolor
    ## 52           6.4         3.2 versicolor
    ## 53           6.9         3.1 versicolor
    ## 54           5.5         2.3 versicolor
    ## 55           6.5         2.8 versicolor
    ## 56           5.7         2.8 versicolor
    ## 57           6.3         3.3 versicolor
    ## 58           4.9         2.4 versicolor
    ## 59           6.6         2.9 versicolor
    ## 60           5.2         2.7 versicolor
    ## 61           5.0         2.0 versicolor
    ## 62           5.9         3.0 versicolor
    ## 63           6.0         2.2 versicolor
    ## 64           6.1         2.9 versicolor
    ## 65           5.6         2.9 versicolor
    ## 66           6.7         3.1 versicolor
    ## 67           5.6         3.0 versicolor
    ## 68           5.8         2.7 versicolor
    ## 69           6.2         2.2 versicolor
    ## 70           5.6         2.5 versicolor
    ## 71           5.9         3.2 versicolor
    ## 72           6.1         2.8 versicolor
    ## 73           6.3         2.5 versicolor
    ## 74           6.1         2.8 versicolor
    ## 75           6.4         2.9 versicolor
    ## 76           6.6         3.0 versicolor
    ## 77           6.8         2.8 versicolor
    ## 78           6.7         3.0 versicolor
    ## 79           6.0         2.9 versicolor
    ## 80           5.7         2.6 versicolor
    ## 81           5.5         2.4 versicolor
    ## 82           5.5         2.4 versicolor
    ## 83           5.8         2.7 versicolor
    ## 84           6.0         2.7 versicolor
    ## 85           5.4         3.0 versicolor
    ## 86           6.0         3.4 versicolor
    ## 87           6.7         3.1 versicolor
    ## 88           6.3         2.3 versicolor
    ## 89           5.6         3.0 versicolor
    ## 90           5.5         2.5 versicolor
    ## 91           5.5         2.6 versicolor
    ## 92           6.1         3.0 versicolor
    ## 93           5.8         2.6 versicolor
    ## 94           5.0         2.3 versicolor
    ## 95           5.6         2.7 versicolor
    ## 96           5.7         3.0 versicolor
    ## 97           5.7         2.9 versicolor
    ## 98           6.2         2.9 versicolor
    ## 99           5.1         2.5 versicolor
    ## 100          5.7         2.8 versicolor
    ## 101          6.3         3.3  virginica
    ## 102          5.8         2.7  virginica
    ## 103          7.1         3.0  virginica
    ## 104          6.3         2.9  virginica
    ## 105          6.5         3.0  virginica
    ## 106          7.6         3.0  virginica
    ## 107          4.9         2.5  virginica
    ## 108          7.3         2.9  virginica
    ## 109          6.7         2.5  virginica
    ## 110          7.2         3.6  virginica
    ## 111          6.5         3.2  virginica
    ## 112          6.4         2.7  virginica
    ## 113          6.8         3.0  virginica
    ## 114          5.7         2.5  virginica
    ## 115          5.8         2.8  virginica
    ## 116          6.4         3.2  virginica
    ## 117          6.5         3.0  virginica
    ## 118          7.7         3.8  virginica
    ## 119          7.7         2.6  virginica
    ## 120          6.0         2.2  virginica
    ## 121          6.9         3.2  virginica
    ## 122          5.6         2.8  virginica
    ## 123          7.7         2.8  virginica
    ## 124          6.3         2.7  virginica
    ## 125          6.7         3.3  virginica
    ## 126          7.2         3.2  virginica
    ## 127          6.2         2.8  virginica
    ## 128          6.1         3.0  virginica
    ## 129          6.4         2.8  virginica
    ## 130          7.2         3.0  virginica
    ## 131          7.4         2.8  virginica
    ## 132          7.9         3.8  virginica
    ## 133          6.4         2.8  virginica
    ## 134          6.3         2.8  virginica
    ## 135          6.1         2.6  virginica
    ## 136          7.7         3.0  virginica
    ## 137          6.3         3.4  virginica
    ## 138          6.4         3.1  virginica
    ## 139          6.0         3.0  virginica
    ## 140          6.9         3.1  virginica
    ## 141          6.7         3.1  virginica
    ## 142          6.9         3.1  virginica
    ## 143          5.8         2.7  virginica
    ## 144          6.8         3.2  virginica
    ## 145          6.7         3.3  virginica
    ## 146          6.7         3.0  virginica
    ## 147          6.3         2.5  virginica
    ## 148          6.5         3.0  virginica
    ## 149          6.2         3.4  virginica
    ## 150          5.9         3.0  virginica

------------------------------------------------------------------------

### Creating new variables as functions of the existing ones with `mutate()`

`mutate()` adds a new column at the end of the data frame. The value of
this column can be a single element vector provided by the user or,
usually more usefully, a formula that uses values of other variables.
Once you create the new column, you can immediately use it in the same
`mutate()` call.

#### `mutate` examples

Add to `iris`a new variable called `One` with the value `1` and the data
type character for all observations.

``` r
mutate(iris, One = "1")
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species One
    ## 1            5.1         3.5          1.4         0.2     setosa   1
    ## 2            4.9         3.0          1.4         0.2     setosa   1
    ## 3            4.7         3.2          1.3         0.2     setosa   1
    ## 4            4.6         3.1          1.5         0.2     setosa   1
    ## 5            5.0         3.6          1.4         0.2     setosa   1
    ## 6            5.4         3.9          1.7         0.4     setosa   1
    ## 7            4.6         3.4          1.4         0.3     setosa   1
    ## 8            5.0         3.4          1.5         0.2     setosa   1
    ## 9            4.4         2.9          1.4         0.2     setosa   1
    ## 10           4.9         3.1          1.5         0.1     setosa   1
    ## 11           5.4         3.7          1.5         0.2     setosa   1
    ## 12           4.8         3.4          1.6         0.2     setosa   1
    ## 13           4.8         3.0          1.4         0.1     setosa   1
    ## 14           4.3         3.0          1.1         0.1     setosa   1
    ## 15           5.8         4.0          1.2         0.2     setosa   1
    ## 16           5.7         4.4          1.5         0.4     setosa   1
    ## 17           5.4         3.9          1.3         0.4     setosa   1
    ## 18           5.1         3.5          1.4         0.3     setosa   1
    ## 19           5.7         3.8          1.7         0.3     setosa   1
    ## 20           5.1         3.8          1.5         0.3     setosa   1
    ## 21           5.4         3.4          1.7         0.2     setosa   1
    ## 22           5.1         3.7          1.5         0.4     setosa   1
    ## 23           4.6         3.6          1.0         0.2     setosa   1
    ## 24           5.1         3.3          1.7         0.5     setosa   1
    ## 25           4.8         3.4          1.9         0.2     setosa   1
    ## 26           5.0         3.0          1.6         0.2     setosa   1
    ## 27           5.0         3.4          1.6         0.4     setosa   1
    ## 28           5.2         3.5          1.5         0.2     setosa   1
    ## 29           5.2         3.4          1.4         0.2     setosa   1
    ## 30           4.7         3.2          1.6         0.2     setosa   1
    ## 31           4.8         3.1          1.6         0.2     setosa   1
    ## 32           5.4         3.4          1.5         0.4     setosa   1
    ## 33           5.2         4.1          1.5         0.1     setosa   1
    ## 34           5.5         4.2          1.4         0.2     setosa   1
    ## 35           4.9         3.1          1.5         0.2     setosa   1
    ## 36           5.0         3.2          1.2         0.2     setosa   1
    ## 37           5.5         3.5          1.3         0.2     setosa   1
    ## 38           4.9         3.6          1.4         0.1     setosa   1
    ## 39           4.4         3.0          1.3         0.2     setosa   1
    ## 40           5.1         3.4          1.5         0.2     setosa   1
    ## 41           5.0         3.5          1.3         0.3     setosa   1
    ## 42           4.5         2.3          1.3         0.3     setosa   1
    ## 43           4.4         3.2          1.3         0.2     setosa   1
    ## 44           5.0         3.5          1.6         0.6     setosa   1
    ## 45           5.1         3.8          1.9         0.4     setosa   1
    ## 46           4.8         3.0          1.4         0.3     setosa   1
    ## 47           5.1         3.8          1.6         0.2     setosa   1
    ## 48           4.6         3.2          1.4         0.2     setosa   1
    ## 49           5.3         3.7          1.5         0.2     setosa   1
    ## 50           5.0         3.3          1.4         0.2     setosa   1
    ## 51           7.0         3.2          4.7         1.4 versicolor   1
    ## 52           6.4         3.2          4.5         1.5 versicolor   1
    ## 53           6.9         3.1          4.9         1.5 versicolor   1
    ## 54           5.5         2.3          4.0         1.3 versicolor   1
    ## 55           6.5         2.8          4.6         1.5 versicolor   1
    ## 56           5.7         2.8          4.5         1.3 versicolor   1
    ## 57           6.3         3.3          4.7         1.6 versicolor   1
    ## 58           4.9         2.4          3.3         1.0 versicolor   1
    ## 59           6.6         2.9          4.6         1.3 versicolor   1
    ## 60           5.2         2.7          3.9         1.4 versicolor   1
    ## 61           5.0         2.0          3.5         1.0 versicolor   1
    ## 62           5.9         3.0          4.2         1.5 versicolor   1
    ## 63           6.0         2.2          4.0         1.0 versicolor   1
    ## 64           6.1         2.9          4.7         1.4 versicolor   1
    ## 65           5.6         2.9          3.6         1.3 versicolor   1
    ## 66           6.7         3.1          4.4         1.4 versicolor   1
    ## 67           5.6         3.0          4.5         1.5 versicolor   1
    ## 68           5.8         2.7          4.1         1.0 versicolor   1
    ## 69           6.2         2.2          4.5         1.5 versicolor   1
    ## 70           5.6         2.5          3.9         1.1 versicolor   1
    ## 71           5.9         3.2          4.8         1.8 versicolor   1
    ## 72           6.1         2.8          4.0         1.3 versicolor   1
    ## 73           6.3         2.5          4.9         1.5 versicolor   1
    ## 74           6.1         2.8          4.7         1.2 versicolor   1
    ## 75           6.4         2.9          4.3         1.3 versicolor   1
    ## 76           6.6         3.0          4.4         1.4 versicolor   1
    ## 77           6.8         2.8          4.8         1.4 versicolor   1
    ## 78           6.7         3.0          5.0         1.7 versicolor   1
    ## 79           6.0         2.9          4.5         1.5 versicolor   1
    ## 80           5.7         2.6          3.5         1.0 versicolor   1
    ## 81           5.5         2.4          3.8         1.1 versicolor   1
    ## 82           5.5         2.4          3.7         1.0 versicolor   1
    ## 83           5.8         2.7          3.9         1.2 versicolor   1
    ## 84           6.0         2.7          5.1         1.6 versicolor   1
    ## 85           5.4         3.0          4.5         1.5 versicolor   1
    ## 86           6.0         3.4          4.5         1.6 versicolor   1
    ## 87           6.7         3.1          4.7         1.5 versicolor   1
    ## 88           6.3         2.3          4.4         1.3 versicolor   1
    ## 89           5.6         3.0          4.1         1.3 versicolor   1
    ## 90           5.5         2.5          4.0         1.3 versicolor   1
    ## 91           5.5         2.6          4.4         1.2 versicolor   1
    ## 92           6.1         3.0          4.6         1.4 versicolor   1
    ## 93           5.8         2.6          4.0         1.2 versicolor   1
    ## 94           5.0         2.3          3.3         1.0 versicolor   1
    ## 95           5.6         2.7          4.2         1.3 versicolor   1
    ## 96           5.7         3.0          4.2         1.2 versicolor   1
    ## 97           5.7         2.9          4.2         1.3 versicolor   1
    ## 98           6.2         2.9          4.3         1.3 versicolor   1
    ## 99           5.1         2.5          3.0         1.1 versicolor   1
    ## 100          5.7         2.8          4.1         1.3 versicolor   1
    ## 101          6.3         3.3          6.0         2.5  virginica   1
    ## 102          5.8         2.7          5.1         1.9  virginica   1
    ## 103          7.1         3.0          5.9         2.1  virginica   1
    ## 104          6.3         2.9          5.6         1.8  virginica   1
    ## 105          6.5         3.0          5.8         2.2  virginica   1
    ## 106          7.6         3.0          6.6         2.1  virginica   1
    ## 107          4.9         2.5          4.5         1.7  virginica   1
    ## 108          7.3         2.9          6.3         1.8  virginica   1
    ## 109          6.7         2.5          5.8         1.8  virginica   1
    ## 110          7.2         3.6          6.1         2.5  virginica   1
    ## 111          6.5         3.2          5.1         2.0  virginica   1
    ## 112          6.4         2.7          5.3         1.9  virginica   1
    ## 113          6.8         3.0          5.5         2.1  virginica   1
    ## 114          5.7         2.5          5.0         2.0  virginica   1
    ## 115          5.8         2.8          5.1         2.4  virginica   1
    ## 116          6.4         3.2          5.3         2.3  virginica   1
    ## 117          6.5         3.0          5.5         1.8  virginica   1
    ## 118          7.7         3.8          6.7         2.2  virginica   1
    ## 119          7.7         2.6          6.9         2.3  virginica   1
    ## 120          6.0         2.2          5.0         1.5  virginica   1
    ## 121          6.9         3.2          5.7         2.3  virginica   1
    ## 122          5.6         2.8          4.9         2.0  virginica   1
    ## 123          7.7         2.8          6.7         2.0  virginica   1
    ## 124          6.3         2.7          4.9         1.8  virginica   1
    ## 125          6.7         3.3          5.7         2.1  virginica   1
    ## 126          7.2         3.2          6.0         1.8  virginica   1
    ## 127          6.2         2.8          4.8         1.8  virginica   1
    ## 128          6.1         3.0          4.9         1.8  virginica   1
    ## 129          6.4         2.8          5.6         2.1  virginica   1
    ## 130          7.2         3.0          5.8         1.6  virginica   1
    ## 131          7.4         2.8          6.1         1.9  virginica   1
    ## 132          7.9         3.8          6.4         2.0  virginica   1
    ## 133          6.4         2.8          5.6         2.2  virginica   1
    ## 134          6.3         2.8          5.1         1.5  virginica   1
    ## 135          6.1         2.6          5.6         1.4  virginica   1
    ## 136          7.7         3.0          6.1         2.3  virginica   1
    ## 137          6.3         3.4          5.6         2.4  virginica   1
    ## 138          6.4         3.1          5.5         1.8  virginica   1
    ## 139          6.0         3.0          4.8         1.8  virginica   1
    ## 140          6.9         3.1          5.4         2.1  virginica   1
    ## 141          6.7         3.1          5.6         2.4  virginica   1
    ## 142          6.9         3.1          5.1         2.3  virginica   1
    ## 143          5.8         2.7          5.1         1.9  virginica   1
    ## 144          6.8         3.2          5.9         2.3  virginica   1
    ## 145          6.7         3.3          5.7         2.5  virginica   1
    ## 146          6.7         3.0          5.2         2.3  virginica   1
    ## 147          6.3         2.5          5.0         1.9  virginica   1
    ## 148          6.5         3.0          5.2         2.0  virginica   1
    ## 149          6.2         3.4          5.4         2.3  virginica   1
    ## 150          5.9         3.0          5.1         1.8  virginica   1

Create new variable named `Petal.Ratio`, the value of which will be the
ratio of petal length to petal width:

``` r
mutate(iris, Petal.Ratio = Petal.Length/Petal.Width)
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species Petal.Ratio
    ## 1            5.1         3.5          1.4         0.2     setosa    7.000000
    ## 2            4.9         3.0          1.4         0.2     setosa    7.000000
    ## 3            4.7         3.2          1.3         0.2     setosa    6.500000
    ## 4            4.6         3.1          1.5         0.2     setosa    7.500000
    ## 5            5.0         3.6          1.4         0.2     setosa    7.000000
    ## 6            5.4         3.9          1.7         0.4     setosa    4.250000
    ## 7            4.6         3.4          1.4         0.3     setosa    4.666667
    ## 8            5.0         3.4          1.5         0.2     setosa    7.500000
    ## 9            4.4         2.9          1.4         0.2     setosa    7.000000
    ## 10           4.9         3.1          1.5         0.1     setosa   15.000000
    ## 11           5.4         3.7          1.5         0.2     setosa    7.500000
    ## 12           4.8         3.4          1.6         0.2     setosa    8.000000
    ## 13           4.8         3.0          1.4         0.1     setosa   14.000000
    ## 14           4.3         3.0          1.1         0.1     setosa   11.000000
    ## 15           5.8         4.0          1.2         0.2     setosa    6.000000
    ## 16           5.7         4.4          1.5         0.4     setosa    3.750000
    ## 17           5.4         3.9          1.3         0.4     setosa    3.250000
    ## 18           5.1         3.5          1.4         0.3     setosa    4.666667
    ## 19           5.7         3.8          1.7         0.3     setosa    5.666667
    ## 20           5.1         3.8          1.5         0.3     setosa    5.000000
    ## 21           5.4         3.4          1.7         0.2     setosa    8.500000
    ## 22           5.1         3.7          1.5         0.4     setosa    3.750000
    ## 23           4.6         3.6          1.0         0.2     setosa    5.000000
    ## 24           5.1         3.3          1.7         0.5     setosa    3.400000
    ## 25           4.8         3.4          1.9         0.2     setosa    9.500000
    ## 26           5.0         3.0          1.6         0.2     setosa    8.000000
    ## 27           5.0         3.4          1.6         0.4     setosa    4.000000
    ## 28           5.2         3.5          1.5         0.2     setosa    7.500000
    ## 29           5.2         3.4          1.4         0.2     setosa    7.000000
    ## 30           4.7         3.2          1.6         0.2     setosa    8.000000
    ## 31           4.8         3.1          1.6         0.2     setosa    8.000000
    ## 32           5.4         3.4          1.5         0.4     setosa    3.750000
    ## 33           5.2         4.1          1.5         0.1     setosa   15.000000
    ## 34           5.5         4.2          1.4         0.2     setosa    7.000000
    ## 35           4.9         3.1          1.5         0.2     setosa    7.500000
    ## 36           5.0         3.2          1.2         0.2     setosa    6.000000
    ## 37           5.5         3.5          1.3         0.2     setosa    6.500000
    ## 38           4.9         3.6          1.4         0.1     setosa   14.000000
    ## 39           4.4         3.0          1.3         0.2     setosa    6.500000
    ## 40           5.1         3.4          1.5         0.2     setosa    7.500000
    ## 41           5.0         3.5          1.3         0.3     setosa    4.333333
    ## 42           4.5         2.3          1.3         0.3     setosa    4.333333
    ## 43           4.4         3.2          1.3         0.2     setosa    6.500000
    ## 44           5.0         3.5          1.6         0.6     setosa    2.666667
    ## 45           5.1         3.8          1.9         0.4     setosa    4.750000
    ## 46           4.8         3.0          1.4         0.3     setosa    4.666667
    ## 47           5.1         3.8          1.6         0.2     setosa    8.000000
    ## 48           4.6         3.2          1.4         0.2     setosa    7.000000
    ## 49           5.3         3.7          1.5         0.2     setosa    7.500000
    ## 50           5.0         3.3          1.4         0.2     setosa    7.000000
    ## 51           7.0         3.2          4.7         1.4 versicolor    3.357143
    ## 52           6.4         3.2          4.5         1.5 versicolor    3.000000
    ## 53           6.9         3.1          4.9         1.5 versicolor    3.266667
    ## 54           5.5         2.3          4.0         1.3 versicolor    3.076923
    ## 55           6.5         2.8          4.6         1.5 versicolor    3.066667
    ## 56           5.7         2.8          4.5         1.3 versicolor    3.461538
    ## 57           6.3         3.3          4.7         1.6 versicolor    2.937500
    ## 58           4.9         2.4          3.3         1.0 versicolor    3.300000
    ## 59           6.6         2.9          4.6         1.3 versicolor    3.538462
    ## 60           5.2         2.7          3.9         1.4 versicolor    2.785714
    ## 61           5.0         2.0          3.5         1.0 versicolor    3.500000
    ## 62           5.9         3.0          4.2         1.5 versicolor    2.800000
    ## 63           6.0         2.2          4.0         1.0 versicolor    4.000000
    ## 64           6.1         2.9          4.7         1.4 versicolor    3.357143
    ## 65           5.6         2.9          3.6         1.3 versicolor    2.769231
    ## 66           6.7         3.1          4.4         1.4 versicolor    3.142857
    ## 67           5.6         3.0          4.5         1.5 versicolor    3.000000
    ## 68           5.8         2.7          4.1         1.0 versicolor    4.100000
    ## 69           6.2         2.2          4.5         1.5 versicolor    3.000000
    ## 70           5.6         2.5          3.9         1.1 versicolor    3.545455
    ## 71           5.9         3.2          4.8         1.8 versicolor    2.666667
    ## 72           6.1         2.8          4.0         1.3 versicolor    3.076923
    ## 73           6.3         2.5          4.9         1.5 versicolor    3.266667
    ## 74           6.1         2.8          4.7         1.2 versicolor    3.916667
    ## 75           6.4         2.9          4.3         1.3 versicolor    3.307692
    ## 76           6.6         3.0          4.4         1.4 versicolor    3.142857
    ## 77           6.8         2.8          4.8         1.4 versicolor    3.428571
    ## 78           6.7         3.0          5.0         1.7 versicolor    2.941176
    ## 79           6.0         2.9          4.5         1.5 versicolor    3.000000
    ## 80           5.7         2.6          3.5         1.0 versicolor    3.500000
    ## 81           5.5         2.4          3.8         1.1 versicolor    3.454545
    ## 82           5.5         2.4          3.7         1.0 versicolor    3.700000
    ## 83           5.8         2.7          3.9         1.2 versicolor    3.250000
    ## 84           6.0         2.7          5.1         1.6 versicolor    3.187500
    ## 85           5.4         3.0          4.5         1.5 versicolor    3.000000
    ## 86           6.0         3.4          4.5         1.6 versicolor    2.812500
    ## 87           6.7         3.1          4.7         1.5 versicolor    3.133333
    ## 88           6.3         2.3          4.4         1.3 versicolor    3.384615
    ## 89           5.6         3.0          4.1         1.3 versicolor    3.153846
    ## 90           5.5         2.5          4.0         1.3 versicolor    3.076923
    ## 91           5.5         2.6          4.4         1.2 versicolor    3.666667
    ## 92           6.1         3.0          4.6         1.4 versicolor    3.285714
    ## 93           5.8         2.6          4.0         1.2 versicolor    3.333333
    ## 94           5.0         2.3          3.3         1.0 versicolor    3.300000
    ## 95           5.6         2.7          4.2         1.3 versicolor    3.230769
    ## 96           5.7         3.0          4.2         1.2 versicolor    3.500000
    ## 97           5.7         2.9          4.2         1.3 versicolor    3.230769
    ## 98           6.2         2.9          4.3         1.3 versicolor    3.307692
    ## 99           5.1         2.5          3.0         1.1 versicolor    2.727273
    ## 100          5.7         2.8          4.1         1.3 versicolor    3.153846
    ## 101          6.3         3.3          6.0         2.5  virginica    2.400000
    ## 102          5.8         2.7          5.1         1.9  virginica    2.684211
    ## 103          7.1         3.0          5.9         2.1  virginica    2.809524
    ## 104          6.3         2.9          5.6         1.8  virginica    3.111111
    ## 105          6.5         3.0          5.8         2.2  virginica    2.636364
    ## 106          7.6         3.0          6.6         2.1  virginica    3.142857
    ## 107          4.9         2.5          4.5         1.7  virginica    2.647059
    ## 108          7.3         2.9          6.3         1.8  virginica    3.500000
    ## 109          6.7         2.5          5.8         1.8  virginica    3.222222
    ## 110          7.2         3.6          6.1         2.5  virginica    2.440000
    ## 111          6.5         3.2          5.1         2.0  virginica    2.550000
    ## 112          6.4         2.7          5.3         1.9  virginica    2.789474
    ## 113          6.8         3.0          5.5         2.1  virginica    2.619048
    ## 114          5.7         2.5          5.0         2.0  virginica    2.500000
    ## 115          5.8         2.8          5.1         2.4  virginica    2.125000
    ## 116          6.4         3.2          5.3         2.3  virginica    2.304348
    ## 117          6.5         3.0          5.5         1.8  virginica    3.055556
    ## 118          7.7         3.8          6.7         2.2  virginica    3.045455
    ## 119          7.7         2.6          6.9         2.3  virginica    3.000000
    ## 120          6.0         2.2          5.0         1.5  virginica    3.333333
    ## 121          6.9         3.2          5.7         2.3  virginica    2.478261
    ## 122          5.6         2.8          4.9         2.0  virginica    2.450000
    ## 123          7.7         2.8          6.7         2.0  virginica    3.350000
    ## 124          6.3         2.7          4.9         1.8  virginica    2.722222
    ## 125          6.7         3.3          5.7         2.1  virginica    2.714286
    ## 126          7.2         3.2          6.0         1.8  virginica    3.333333
    ## 127          6.2         2.8          4.8         1.8  virginica    2.666667
    ## 128          6.1         3.0          4.9         1.8  virginica    2.722222
    ## 129          6.4         2.8          5.6         2.1  virginica    2.666667
    ## 130          7.2         3.0          5.8         1.6  virginica    3.625000
    ## 131          7.4         2.8          6.1         1.9  virginica    3.210526
    ## 132          7.9         3.8          6.4         2.0  virginica    3.200000
    ## 133          6.4         2.8          5.6         2.2  virginica    2.545455
    ## 134          6.3         2.8          5.1         1.5  virginica    3.400000
    ## 135          6.1         2.6          5.6         1.4  virginica    4.000000
    ## 136          7.7         3.0          6.1         2.3  virginica    2.652174
    ## 137          6.3         3.4          5.6         2.4  virginica    2.333333
    ## 138          6.4         3.1          5.5         1.8  virginica    3.055556
    ## 139          6.0         3.0          4.8         1.8  virginica    2.666667
    ## 140          6.9         3.1          5.4         2.1  virginica    2.571429
    ## 141          6.7         3.1          5.6         2.4  virginica    2.333333
    ## 142          6.9         3.1          5.1         2.3  virginica    2.217391
    ## 143          5.8         2.7          5.1         1.9  virginica    2.684211
    ## 144          6.8         3.2          5.9         2.3  virginica    2.565217
    ## 145          6.7         3.3          5.7         2.5  virginica    2.280000
    ## 146          6.7         3.0          5.2         2.3  virginica    2.260870
    ## 147          6.3         2.5          5.0         1.9  virginica    2.631579
    ## 148          6.5         3.0          5.2         2.0  virginica    2.600000
    ## 149          6.2         3.4          5.4         2.3  virginica    2.347826
    ## 150          5.9         3.0          5.1         1.8  virginica    2.833333

#### Exercise 14

Create, using a single `mutate()` call, two new variables:
Petal.Length.Squared, Sepal.Length.Squared, containing the squared
length of petal and sepal, respectively.

Expected result:

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            5.1         3.5          1.4         0.2     setosa
    ## 2            4.9         3.0          1.4         0.2     setosa
    ## 3            4.7         3.2          1.3         0.2     setosa
    ## 4            4.6         3.1          1.5         0.2     setosa
    ## 5            5.0         3.6          1.4         0.2     setosa
    ## 6            5.4         3.9          1.7         0.4     setosa
    ## 7            4.6         3.4          1.4         0.3     setosa
    ## 8            5.0         3.4          1.5         0.2     setosa
    ## 9            4.4         2.9          1.4         0.2     setosa
    ## 10           4.9         3.1          1.5         0.1     setosa
    ## 11           5.4         3.7          1.5         0.2     setosa
    ## 12           4.8         3.4          1.6         0.2     setosa
    ## 13           4.8         3.0          1.4         0.1     setosa
    ## 14           4.3         3.0          1.1         0.1     setosa
    ## 15           5.8         4.0          1.2         0.2     setosa
    ## 16           5.7         4.4          1.5         0.4     setosa
    ## 17           5.4         3.9          1.3         0.4     setosa
    ## 18           5.1         3.5          1.4         0.3     setosa
    ## 19           5.7         3.8          1.7         0.3     setosa
    ## 20           5.1         3.8          1.5         0.3     setosa
    ## 21           5.4         3.4          1.7         0.2     setosa
    ## 22           5.1         3.7          1.5         0.4     setosa
    ## 23           4.6         3.6          1.0         0.2     setosa
    ## 24           5.1         3.3          1.7         0.5     setosa
    ## 25           4.8         3.4          1.9         0.2     setosa
    ## 26           5.0         3.0          1.6         0.2     setosa
    ## 27           5.0         3.4          1.6         0.4     setosa
    ## 28           5.2         3.5          1.5         0.2     setosa
    ## 29           5.2         3.4          1.4         0.2     setosa
    ## 30           4.7         3.2          1.6         0.2     setosa
    ## 31           4.8         3.1          1.6         0.2     setosa
    ## 32           5.4         3.4          1.5         0.4     setosa
    ## 33           5.2         4.1          1.5         0.1     setosa
    ## 34           5.5         4.2          1.4         0.2     setosa
    ## 35           4.9         3.1          1.5         0.2     setosa
    ## 36           5.0         3.2          1.2         0.2     setosa
    ## 37           5.5         3.5          1.3         0.2     setosa
    ## 38           4.9         3.6          1.4         0.1     setosa
    ## 39           4.4         3.0          1.3         0.2     setosa
    ## 40           5.1         3.4          1.5         0.2     setosa
    ## 41           5.0         3.5          1.3         0.3     setosa
    ## 42           4.5         2.3          1.3         0.3     setosa
    ## 43           4.4         3.2          1.3         0.2     setosa
    ## 44           5.0         3.5          1.6         0.6     setosa
    ## 45           5.1         3.8          1.9         0.4     setosa
    ## 46           4.8         3.0          1.4         0.3     setosa
    ## 47           5.1         3.8          1.6         0.2     setosa
    ## 48           4.6         3.2          1.4         0.2     setosa
    ## 49           5.3         3.7          1.5         0.2     setosa
    ## 50           5.0         3.3          1.4         0.2     setosa
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.4         3.2          4.5         1.5 versicolor
    ## 53           6.9         3.1          4.9         1.5 versicolor
    ## 54           5.5         2.3          4.0         1.3 versicolor
    ## 55           6.5         2.8          4.6         1.5 versicolor
    ## 56           5.7         2.8          4.5         1.3 versicolor
    ## 57           6.3         3.3          4.7         1.6 versicolor
    ## 58           4.9         2.4          3.3         1.0 versicolor
    ## 59           6.6         2.9          4.6         1.3 versicolor
    ## 60           5.2         2.7          3.9         1.4 versicolor
    ## 61           5.0         2.0          3.5         1.0 versicolor
    ## 62           5.9         3.0          4.2         1.5 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.9          4.7         1.4 versicolor
    ## 65           5.6         2.9          3.6         1.3 versicolor
    ## 66           6.7         3.1          4.4         1.4 versicolor
    ## 67           5.6         3.0          4.5         1.5 versicolor
    ## 68           5.8         2.7          4.1         1.0 versicolor
    ## 69           6.2         2.2          4.5         1.5 versicolor
    ## 70           5.6         2.5          3.9         1.1 versicolor
    ## 71           5.9         3.2          4.8         1.8 versicolor
    ## 72           6.1         2.8          4.0         1.3 versicolor
    ## 73           6.3         2.5          4.9         1.5 versicolor
    ## 74           6.1         2.8          4.7         1.2 versicolor
    ## 75           6.4         2.9          4.3         1.3 versicolor
    ## 76           6.6         3.0          4.4         1.4 versicolor
    ## 77           6.8         2.8          4.8         1.4 versicolor
    ## 78           6.7         3.0          5.0         1.7 versicolor
    ## 79           6.0         2.9          4.5         1.5 versicolor
    ## 80           5.7         2.6          3.5         1.0 versicolor
    ## 81           5.5         2.4          3.8         1.1 versicolor
    ## 82           5.5         2.4          3.7         1.0 versicolor
    ## 83           5.8         2.7          3.9         1.2 versicolor
    ## 84           6.0         2.7          5.1         1.6 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.7         3.1          4.7         1.5 versicolor
    ## 88           6.3         2.3          4.4         1.3 versicolor
    ## 89           5.6         3.0          4.1         1.3 versicolor
    ## 90           5.5         2.5          4.0         1.3 versicolor
    ## 91           5.5         2.6          4.4         1.2 versicolor
    ## 92           6.1         3.0          4.6         1.4 versicolor
    ## 93           5.8         2.6          4.0         1.2 versicolor
    ## 94           5.0         2.3          3.3         1.0 versicolor
    ## 95           5.6         2.7          4.2         1.3 versicolor
    ## 96           5.7         3.0          4.2         1.2 versicolor
    ## 97           5.7         2.9          4.2         1.3 versicolor
    ## 98           6.2         2.9          4.3         1.3 versicolor
    ## 99           5.1         2.5          3.0         1.1 versicolor
    ## 100          5.7         2.8          4.1         1.3 versicolor
    ## 101          6.3         3.3          6.0         2.5  virginica
    ## 102          5.8         2.7          5.1         1.9  virginica
    ## 103          7.1         3.0          5.9         2.1  virginica
    ## 104          6.3         2.9          5.6         1.8  virginica
    ## 105          6.5         3.0          5.8         2.2  virginica
    ## 106          7.6         3.0          6.6         2.1  virginica
    ## 107          4.9         2.5          4.5         1.7  virginica
    ## 108          7.3         2.9          6.3         1.8  virginica
    ## 109          6.7         2.5          5.8         1.8  virginica
    ## 110          7.2         3.6          6.1         2.5  virginica
    ## 111          6.5         3.2          5.1         2.0  virginica
    ## 112          6.4         2.7          5.3         1.9  virginica
    ## 113          6.8         3.0          5.5         2.1  virginica
    ## 114          5.7         2.5          5.0         2.0  virginica
    ## 115          5.8         2.8          5.1         2.4  virginica
    ## 116          6.4         3.2          5.3         2.3  virginica
    ## 117          6.5         3.0          5.5         1.8  virginica
    ## 118          7.7         3.8          6.7         2.2  virginica
    ## 119          7.7         2.6          6.9         2.3  virginica
    ## 120          6.0         2.2          5.0         1.5  virginica
    ## 121          6.9         3.2          5.7         2.3  virginica
    ## 122          5.6         2.8          4.9         2.0  virginica
    ## 123          7.7         2.8          6.7         2.0  virginica
    ## 124          6.3         2.7          4.9         1.8  virginica
    ## 125          6.7         3.3          5.7         2.1  virginica
    ## 126          7.2         3.2          6.0         1.8  virginica
    ## 127          6.2         2.8          4.8         1.8  virginica
    ## 128          6.1         3.0          4.9         1.8  virginica
    ## 129          6.4         2.8          5.6         2.1  virginica
    ## 130          7.2         3.0          5.8         1.6  virginica
    ## 131          7.4         2.8          6.1         1.9  virginica
    ## 132          7.9         3.8          6.4         2.0  virginica
    ## 133          6.4         2.8          5.6         2.2  virginica
    ## 134          6.3         2.8          5.1         1.5  virginica
    ## 135          6.1         2.6          5.6         1.4  virginica
    ## 136          7.7         3.0          6.1         2.3  virginica
    ## 137          6.3         3.4          5.6         2.4  virginica
    ## 138          6.4         3.1          5.5         1.8  virginica
    ## 139          6.0         3.0          4.8         1.8  virginica
    ## 140          6.9         3.1          5.4         2.1  virginica
    ## 141          6.7         3.1          5.6         2.4  virginica
    ## 142          6.9         3.1          5.1         2.3  virginica
    ## 143          5.8         2.7          5.1         1.9  virginica
    ## 144          6.8         3.2          5.9         2.3  virginica
    ## 145          6.7         3.3          5.7         2.5  virginica
    ## 146          6.7         3.0          5.2         2.3  virginica
    ## 147          6.3         2.5          5.0         1.9  virginica
    ## 148          6.5         3.0          5.2         2.0  virginica
    ## 149          6.2         3.4          5.4         2.3  virginica
    ## 150          5.9         3.0          5.1         1.8  virginica
    ##     Petal.Length.Squared Sepal.Length.Squared
    ## 1                   1.96                26.01
    ## 2                   1.96                24.01
    ## 3                   1.69                22.09
    ## 4                   2.25                21.16
    ## 5                   1.96                25.00
    ## 6                   2.89                29.16
    ## 7                   1.96                21.16
    ## 8                   2.25                25.00
    ## 9                   1.96                19.36
    ## 10                  2.25                24.01
    ## 11                  2.25                29.16
    ## 12                  2.56                23.04
    ## 13                  1.96                23.04
    ## 14                  1.21                18.49
    ## 15                  1.44                33.64
    ## 16                  2.25                32.49
    ## 17                  1.69                29.16
    ## 18                  1.96                26.01
    ## 19                  2.89                32.49
    ## 20                  2.25                26.01
    ## 21                  2.89                29.16
    ## 22                  2.25                26.01
    ## 23                  1.00                21.16
    ## 24                  2.89                26.01
    ## 25                  3.61                23.04
    ## 26                  2.56                25.00
    ## 27                  2.56                25.00
    ## 28                  2.25                27.04
    ## 29                  1.96                27.04
    ## 30                  2.56                22.09
    ## 31                  2.56                23.04
    ## 32                  2.25                29.16
    ## 33                  2.25                27.04
    ## 34                  1.96                30.25
    ## 35                  2.25                24.01
    ## 36                  1.44                25.00
    ## 37                  1.69                30.25
    ## 38                  1.96                24.01
    ## 39                  1.69                19.36
    ## 40                  2.25                26.01
    ## 41                  1.69                25.00
    ## 42                  1.69                20.25
    ## 43                  1.69                19.36
    ## 44                  2.56                25.00
    ## 45                  3.61                26.01
    ## 46                  1.96                23.04
    ## 47                  2.56                26.01
    ## 48                  1.96                21.16
    ## 49                  2.25                28.09
    ## 50                  1.96                25.00
    ## 51                 22.09                49.00
    ## 52                 20.25                40.96
    ## 53                 24.01                47.61
    ## 54                 16.00                30.25
    ## 55                 21.16                42.25
    ## 56                 20.25                32.49
    ## 57                 22.09                39.69
    ## 58                 10.89                24.01
    ## 59                 21.16                43.56
    ## 60                 15.21                27.04
    ## 61                 12.25                25.00
    ## 62                 17.64                34.81
    ## 63                 16.00                36.00
    ## 64                 22.09                37.21
    ## 65                 12.96                31.36
    ## 66                 19.36                44.89
    ## 67                 20.25                31.36
    ## 68                 16.81                33.64
    ## 69                 20.25                38.44
    ## 70                 15.21                31.36
    ## 71                 23.04                34.81
    ## 72                 16.00                37.21
    ## 73                 24.01                39.69
    ## 74                 22.09                37.21
    ## 75                 18.49                40.96
    ## 76                 19.36                43.56
    ## 77                 23.04                46.24
    ## 78                 25.00                44.89
    ## 79                 20.25                36.00
    ## 80                 12.25                32.49
    ## 81                 14.44                30.25
    ## 82                 13.69                30.25
    ## 83                 15.21                33.64
    ## 84                 26.01                36.00
    ## 85                 20.25                29.16
    ## 86                 20.25                36.00
    ## 87                 22.09                44.89
    ## 88                 19.36                39.69
    ## 89                 16.81                31.36
    ## 90                 16.00                30.25
    ## 91                 19.36                30.25
    ## 92                 21.16                37.21
    ## 93                 16.00                33.64
    ## 94                 10.89                25.00
    ## 95                 17.64                31.36
    ## 96                 17.64                32.49
    ## 97                 17.64                32.49
    ## 98                 18.49                38.44
    ## 99                  9.00                26.01
    ## 100                16.81                32.49
    ## 101                36.00                39.69
    ## 102                26.01                33.64
    ## 103                34.81                50.41
    ## 104                31.36                39.69
    ## 105                33.64                42.25
    ## 106                43.56                57.76
    ## 107                20.25                24.01
    ## 108                39.69                53.29
    ## 109                33.64                44.89
    ## 110                37.21                51.84
    ## 111                26.01                42.25
    ## 112                28.09                40.96
    ## 113                30.25                46.24
    ## 114                25.00                32.49
    ## 115                26.01                33.64
    ## 116                28.09                40.96
    ## 117                30.25                42.25
    ## 118                44.89                59.29
    ## 119                47.61                59.29
    ## 120                25.00                36.00
    ## 121                32.49                47.61
    ## 122                24.01                31.36
    ## 123                44.89                59.29
    ## 124                24.01                39.69
    ## 125                32.49                44.89
    ## 126                36.00                51.84
    ## 127                23.04                38.44
    ## 128                24.01                37.21
    ## 129                31.36                40.96
    ## 130                33.64                51.84
    ## 131                37.21                54.76
    ## 132                40.96                62.41
    ## 133                31.36                40.96
    ## 134                26.01                39.69
    ## 135                31.36                37.21
    ## 136                37.21                59.29
    ## 137                31.36                39.69
    ## 138                30.25                40.96
    ## 139                23.04                36.00
    ## 140                29.16                47.61
    ## 141                31.36                44.89
    ## 142                26.01                47.61
    ## 143                26.01                33.64
    ## 144                34.81                46.24
    ## 145                32.49                44.89
    ## 146                27.04                44.89
    ## 147                25.00                39.69
    ## 148                27.04                42.25
    ## 149                29.16                38.44
    ## 150                26.01                34.81

------------------------------------------------------------------------

### Grouping cases by variable(s) with `group_by()`

You could (rightly) consider some of the preceding examples and
exercises boring, so let’s move to something more exciting. `group_by()`
creates a **grouped data frame**, that is a data frame which rows are
assigned to various groups based on the value of one or more grouping
variables. The data frame itself is not changed, but the way operations
on the data frame are performed is. For example, if you use a function,
such as `mean()` with `mutate()`, the mean of the group to which a row
belongs will be used for this row.

#### `group_by()` examples

Group `iris` by species

``` r
group_by(iris, Species)
```

When you execute the command above, you’ll see that the object is not
anymore `data.frame`, but now it’s called `tibble` and you’ll find
information about grouping added, though no information in the table was
altered:

    ## # A tibble: 150 x 5
    ## # Groups:   Species [3]
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##           <dbl>       <dbl>        <dbl>       <dbl> <fct>  
    ##  1          5.1         3.5          1.4         0.2 setosa 
    ##  2          4.9         3            1.4         0.2 setosa 
    ##  3          4.7         3.2          1.3         0.2 setosa 
    ##  4          4.6         3.1          1.5         0.2 setosa 
    ##  5          5           3.6          1.4         0.2 setosa 
    ##  6          5.4         3.9          1.7         0.4 setosa 
    ##  7          4.6         3.4          1.4         0.3 setosa 
    ##  8          5           3.4          1.5         0.2 setosa 
    ##  9          4.4         2.9          1.4         0.2 setosa 
    ## 10          4.9         3.1          1.5         0.1 setosa 
    ## # ... with 140 more rows

#### Exercise 15

Group `iris` by species, assign the grouped dataset to variable, and use
mutate to add column `Mean.Sepal.Length`, which would contain the mean
value of sepal length. Are all values in this column identical? Why?

------------------------------------------------------------------------

#### The pipe operator (`%>%`)

Usually, when you want to use several functions in sequence, you
repeatedly assign the result to a variable, which is fine, but a bit
inconvenient:

``` r
a <- select(iris, Species, starts_with("Sepal"))
a <- mutate(a, Sepal.Ratio = Sepal.Length/Sepal.Width)
head(a)
```

    ##   Species Sepal.Length Sepal.Width Sepal.Ratio
    ## 1  setosa          5.1         3.5    1.457143
    ## 2  setosa          4.9         3.0    1.633333
    ## 3  setosa          4.7         3.2    1.468750
    ## 4  setosa          4.6         3.1    1.483871
    ## 5  setosa          5.0         3.6    1.388889
    ## 6  setosa          5.4         3.9    1.384615

Here’s where the **pipe** `%>%` comes handy. Although the symbol used is
different, its behaviour is similar to the pipe operator `|` of the
Linux shell. In conjunction with `dplyr` verbs it allows creating
pipelines without the need of assigning intermediate results to
variables. Note, that when a `dplyr` function is used following `%>%`,
you don’t specify the data frame the function operates on - because the
data frame is passed by `%>%`!

So, instead of the code above you can use:

``` r
a <- select(iris, Species, starts_with("Sepal")) %>% mutate(Sepal.Ratio = Sepal.Length/Sepal.Width)
head(a)
```

    ##   Species Sepal.Length Sepal.Width Sepal.Ratio
    ## 1  setosa          5.1         3.5    1.457143
    ## 2  setosa          4.9         3.0    1.633333
    ## 3  setosa          4.7         3.2    1.468750
    ## 4  setosa          4.6         3.1    1.483871
    ## 5  setosa          5.0         3.6    1.388889
    ## 6  setosa          5.4         3.9    1.384615

or

``` r
a <- iris %>% select(Species, starts_with("Sepal")) %>% mutate(Sepal.Ratio = Sepal.Length/Sepal.Width)
head(a)
```

    ##   Species Sepal.Length Sepal.Width Sepal.Ratio
    ## 1  setosa          5.1         3.5    1.457143
    ## 2  setosa          4.9         3.0    1.633333
    ## 3  setosa          4.7         3.2    1.468750
    ## 4  setosa          4.6         3.1    1.483871
    ## 5  setosa          5.0         3.6    1.388889
    ## 6  setosa          5.4         3.9    1.384615

Using `%>%` not only eliminates the need for intermediate variables, but
also makes code more **readable**. In this case, you first take `iris`,
then select some columns and then add a column based on the values of
the existing columns. The way your code is written reflects the sequence
of steps.

Before we move on, we’ll show a useful technique that allows, for
example, easy standardization. Our task is to standardize the values of
sepal length by subtracting each from the species mean and dividing the
result by the species standard deviation (this is called
Z-standardization). Here’s the code:

``` r
iris %>% select(Species, Sepal.Length) %>%  group_by(Species) %>%
  mutate(sp.Mean = mean(Sepal.Length),
         sp.SD = sd(Sepal.Length),
         Zstand.Sepal.Length = (Sepal.Length - sp.Mean)/sp.SD)
```

    ## # A tibble: 150 x 5
    ## # Groups:   Species [3]
    ##    Species Sepal.Length sp.Mean sp.SD Zstand.Sepal.Length
    ##    <fct>          <dbl>   <dbl> <dbl>               <dbl>
    ##  1 setosa           5.1    5.01 0.352              0.267 
    ##  2 setosa           4.9    5.01 0.352             -0.301 
    ##  3 setosa           4.7    5.01 0.352             -0.868 
    ##  4 setosa           4.6    5.01 0.352             -1.15  
    ##  5 setosa           5      5.01 0.352             -0.0170
    ##  6 setosa           5.4    5.01 0.352              1.12  
    ##  7 setosa           4.6    5.01 0.352             -1.15  
    ##  8 setosa           5      5.01 0.352             -0.0170
    ##  9 setosa           4.4    5.01 0.352             -1.72  
    ## 10 setosa           4.9    5.01 0.352             -0.301 
    ## # ... with 140 more rows

we could use `select()` again to drop the intermediate variables we no
longer need:

``` r
iris %>% select(Species, Sepal.Length) %>%  group_by(Species) %>%
  mutate(sp.Mean = mean(Sepal.Length),
         sp.SD = sd(Sepal.Length),
         Zstand.Sepal.Length = (Sepal.Length - sp.Mean)/sp.SD) %>% select(-c(sp.Mean, sp.SD))
```

    ## # A tibble: 150 x 3
    ## # Groups:   Species [3]
    ##    Species Sepal.Length Zstand.Sepal.Length
    ##    <fct>          <dbl>               <dbl>
    ##  1 setosa           5.1              0.267 
    ##  2 setosa           4.9             -0.301 
    ##  3 setosa           4.7             -0.868 
    ##  4 setosa           4.6             -1.15  
    ##  5 setosa           5               -0.0170
    ##  6 setosa           5.4              1.12  
    ##  7 setosa           4.6             -1.15  
    ##  8 setosa           5               -0.0170
    ##  9 setosa           4.4             -1.72  
    ## 10 setosa           4.9             -0.301 
    ## # ... with 140 more rows

Note, that the columns to drop were passed as a vector of column names
not enclosed in quotation marks (quotation marks are allowed, but not
necessary).

### Summarising with `summarise()`

When used on a data frame that is not grouped `summarise` just applies a
function to a column and returns a small data frame containing the
result:

``` r
summarise(iris, mean.Sepal.Length = mean(Sepal.Length))
```

    ##   mean.Sepal.Length
    ## 1          5.843333

This may be useful, but rather not terribly so.

Things change when you use summarise with a grouped data frame. Then,
writing very little code you can get lots of useful results:

``` r
iris %>% select (Species, Petal.Length) %>% group_by(Species) %>% 
  summarise(min.Petal.Length = min(Petal.Length),
            mean.Petal.Length = mean(Petal.Length), 
            max.Petal.Length = max(Petal.Length))
```

    ## # A tibble: 3 x 4
    ##   Species    min.Petal.Length mean.Petal.Length max.Petal.Length
    ##   <fct>                 <dbl>             <dbl>            <dbl>
    ## 1 setosa                  1                1.46              1.9
    ## 2 versicolor              3                4.26              5.1
    ## 3 virginica               4.5              5.55              6.9
