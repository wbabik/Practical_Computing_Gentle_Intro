Class 9: Subsetting and working with dataframes
================
Tomasz Gaczorek & Wiesław Babik
2022-07-12

-   [Subsetting](#subsetting)
    -   [Exercise 1](#exercise-1)
    -   [Exercise 2](#exercise-2)
    -   [Exercise 3](#exercise-3)
    -   [Exercise 4](#exercise-4)
    -   [Exercise 5](#exercise-5)
    -   [Exercise 6](#exercise-6)
    -   [Exercise 7](#exercise-7)
    -   [Exercise 8](#exercise-8)
    -   [Exercise 9](#exercise-9)
    -   [Logical expressions](#logical-expressions)
        -   [Exercise 10](#exercise-10)
        -   [Exercise 11](#exercise-11)
        -   [Exercise 12](#exercise-12)
    -   [Comparisons](#comparisons)
        -   [Exercise 13](#exercise-13)
        -   [Exercise 14](#exercise-14)
        -   [Exercise 15](#exercise-15)
        -   [Exercise 16](#exercise-16)
    -   [Negation](#negation)
        -   [Exercise 17](#exercise-17)
        -   [Exercise 18](#exercise-18)
    -   [Logical operators](#logical-operators)
        -   [Exercise 19](#exercise-19)
        -   [Exercise 20](#exercise-20)
    -   [`which()` function](#which-function)
        -   [Exercise 21](#exercise-21)
        -   [Exercise 22](#exercise-22)
    -   [Subsetting with logical
        expressions](#subsetting-with-logical-expressions)
        -   [Exercise 23](#exercise-23)
-   [Operations on data frames, part
    1](#operations-on-data-frames-part-1)
    -   [Replacement](#replacement)
        -   [Exercise 24](#exercise-24)
    -   [Mathematical operations](#mathematical-operations)
        -   [Exercise 25](#exercise-25)
        -   [Exercise 26](#exercise-26)
    -   [Simple summaries](#simple-summaries)
        -   [Exercise 27](#exercise-27)
        -   [Exercise 28](#exercise-28)
    -   [Deleting rows containing missing
        data](#deleting-rows-containing-missing-data)
        -   [Exercise 29](#exercise-29)
        -   [Exercise 30](#exercise-30)

## Subsetting

Data frame can be subset with the use of coordinates (indexes) enclosed
within the square brackets. In case of data frames there are always two
coordinates: `[row_number, column_number]`. Note that vectors have only
a single coordinate, the position, so they are one-dimensional objects.
Data frames have two dimensions: rows and columns.

#### Exercise 1

Return the value from 49<sup>th</sup> row and 4<sup>th</sup> column of
`my_data` from the previous class (use your script/history to get this
variable).

Expected result:

    ## [1] 1000

------------------------------------------------------------------------

You can retrieve multiple values at the same time. To define a range of
coordinates, use colon to separate range limits:
`[row_number_1:row_number_2, column_number]`.

#### Exercise 2

Return first 5 rows of the last 3 columns of `my_data`. To check the
number of rows and columns use `str()`, which will give you also extra
info about the data frame, or `dim()` which will return just the number
of rows and columns

Expected result:

    ##    Treatment conc uptake
    ## 1 nonchilled   95   16.0
    ## 2 nonchilled  175   30.4
    ## 3 nonchilled  250   34.8
    ## 4 nonchilled  350   37.2
    ## 5 nonchilled  500   35.3

------------------------------------------------------------------------

If you want to get all rows or columns, it’s enough to put nothing
instead of the respective coordinate, e. g. `[, column_number]` will
return all rows for the column.

#### Exercise 3

Now, save the 5<sup>th</sup> column of `my_data` as variable
`my_column_5`. Call call the variable, so its content is displayed in
your console.

Expected result:

    ##  [1] 16.0 30.4 34.8 37.2 35.3 39.2 39.7 13.6 27.3 37.1 41.8 40.6 41.4 44.3 16.2
    ## [16] 32.4 40.3 42.1 42.9 43.9 45.5 14.2 24.1 30.3 34.6 32.5 35.4 38.7  9.3 27.3
    ## [31] 35.0 38.8 38.6 37.5 42.4 15.1 21.0 38.1 34.0 38.9 39.6 41.4 10.6 19.2 26.2
    ## [46] 30.0 30.9 32.4 35.5 12.0 22.0 30.6 31.8 32.4 31.1 31.5 11.3 19.4 25.8 27.9
    ## [61] 28.5 28.1 27.8 10.5 14.9 18.1 18.9 19.5 22.2 21.9  7.7 11.4 12.3 13.0 12.5
    ## [76] 13.7 14.4 10.6 18.0 17.9 17.9 17.9 18.9 19.9

------------------------------------------------------------------------

Note that the result is no longer a table. As we asked for just one
column, a series of numbers (vector) was returned. Let’s recall vector
subsetting.

#### Exercise 4

Return 3<sup>rd</sup>, 4<sup>th</sup> and 5<sup>th</sup> value from
`my_column_5`.

Expected result:

    ## [1] 34.8 37.2 35.3

------------------------------------------------------------------------

> #### Important
>
> Pulling one row from the data frame will not result in a vector. It’s
> because a row can contain elements of different types, which is not
> allowed for vectors.

Data frame can also be subset with the use of column (or row, if they
exist) names.

#### Exercise 5

Return the same column as in Ex. 3, but use column name instead of its
number. Don’t forget about quotation marks.

Another way of obtaining an entire column is to use dollar sign between
data frame and column names `dataframe_name$column_name`. Such
expression is automatically treated as vector, so it can be directly
subset to get a particular row:
`dataframe_name$column_name[row_number]`.

#### Exercise 6

Return values of rows 15<sup>th</sup> to 30<sup>th</sup> of `conc`
column from `my_data`. Use `$` sign.

Expected result:

    ##  [1]   95  175  250  350  500  675 1000   95  175  250  350  500  675 1000   95
    ## [16]  175

------------------------------------------------------------------------

If desired rows (or columns) do not follow each other and the range
option can’t be used, vector of coordinates should be provided.

#### Exercise 7

Create a vector of integers with values 3, 5, 7, 9 and 12 and save it to
a variable. Call it.

Expected result:

    ## [1]  3  5  7  9 12

------------------------------------------------------------------------

#### Exercise 8

Return rows of `my_data` `uptake` column corresponding to the numbers in
the vector created in the previous exercise.

Expected result:

    ## [1] 34.8 35.3 39.7 27.3 40.6

------------------------------------------------------------------------

You can also select everything except specified columns (or rows), i.
e., drop rows or columns. To do this, put minus (-) before an index or
vector of indexes.

#### Exercise 9

Return all columns of `my_data` except 5<sup>th</sup>.

Expected result:

    ##    Plant        Type  Treatment conc
    ## 1    Qn1      Quebec nonchilled   95
    ## 2    Qn1      Quebec nonchilled  175
    ## 3    Qn1      Quebec nonchilled  250
    ## 4    Qn1      Quebec nonchilled  350
    ## 5    Qn1      Quebec nonchilled  500
    ## 6    Qn1      Quebec nonchilled  675
    ## 7    Qn1      Quebec nonchilled 1000
    ## 8    Qn2      Quebec nonchilled   95
    ## 9    Qn2      Quebec nonchilled  175
    ## 10   Qn2      Quebec nonchilled  250
    ## 11   Qn2      Quebec nonchilled  350
    ## 12   Qn2      Quebec nonchilled  500
    ## 13   Qn2      Quebec nonchilled  675
    ## 14   Qn2      Quebec nonchilled 1000
    ## 15   Qn3      Quebec nonchilled   95
    ## 16   Qn3      Quebec nonchilled  175
    ## 17   Qn3      Quebec nonchilled  250
    ## 18   Qn3      Quebec nonchilled  350
    ## 19   Qn3      Quebec nonchilled  500
    ## 20   Qn3      Quebec nonchilled  675
    ## 21   Qn3      Quebec nonchilled 1000
    ## 22   Qc1      Quebec    chilled   95
    ## 23   Qc1      Quebec    chilled  175
    ## 24   Qc1      Quebec    chilled  250
    ## 25   Qc1      Quebec    chilled  350
    ## 26   Qc1      Quebec    chilled  500
    ## 27   Qc1      Quebec    chilled  675
    ## 28   Qc1      Quebec    chilled 1000
    ## 29   Qc2      Quebec    chilled   95
    ## 30   Qc2      Quebec    chilled  175
    ## 31   Qc2      Quebec    chilled  250
    ## 32   Qc2      Quebec    chilled  350
    ## 33   Qc2      Quebec    chilled  500
    ## 34   Qc2      Quebec    chilled  675
    ## 35   Qc2      Quebec    chilled 1000
    ## 36   Qc3      Quebec    chilled   95
    ## 37   Qc3      Quebec    chilled  175
    ## 38   Qc3      Quebec    chilled  250
    ## 39   Qc3      Quebec    chilled  350
    ## 40   Qc3      Quebec    chilled  500
    ## 41   Qc3      Quebec    chilled  675
    ## 42   Qc3      Quebec    chilled 1000
    ## 43   Mn1 Mississippi nonchilled   95
    ## 44   Mn1 Mississippi nonchilled  175
    ## 45   Mn1 Mississippi nonchilled  250
    ## 46   Mn1 Mississippi nonchilled  350
    ## 47   Mn1 Mississippi nonchilled  500
    ## 48   Mn1 Mississippi nonchilled  675
    ## 49   Mn1 Mississippi nonchilled 1000
    ## 50   Mn2 Mississippi nonchilled   95
    ## 51   Mn2 Mississippi nonchilled  175
    ## 52   Mn2 Mississippi nonchilled  250
    ## 53   Mn2 Mississippi nonchilled  350
    ## 54   Mn2 Mississippi nonchilled  500
    ## 55   Mn2 Mississippi nonchilled  675
    ## 56   Mn2 Mississippi nonchilled 1000
    ## 57   Mn3 Mississippi nonchilled   95
    ## 58   Mn3 Mississippi nonchilled  175
    ## 59   Mn3 Mississippi nonchilled  250
    ## 60   Mn3 Mississippi nonchilled  350
    ## 61   Mn3 Mississippi nonchilled  500
    ## 62   Mn3 Mississippi nonchilled  675
    ## 63   Mn3 Mississippi nonchilled 1000
    ## 64   Mc1 Mississippi    chilled   95
    ## 65   Mc1 Mississippi    chilled  175
    ## 66   Mc1 Mississippi    chilled  250
    ## 67   Mc1 Mississippi    chilled  350
    ## 68   Mc1 Mississippi    chilled  500
    ## 69   Mc1 Mississippi    chilled  675
    ## 70   Mc1 Mississippi    chilled 1000
    ## 71   Mc2 Mississippi    chilled   95
    ## 72   Mc2 Mississippi    chilled  175
    ## 73   Mc2 Mississippi    chilled  250
    ## 74   Mc2 Mississippi    chilled  350
    ## 75   Mc2 Mississippi    chilled  500
    ## 76   Mc2 Mississippi    chilled  675
    ## 77   Mc2 Mississippi    chilled 1000
    ## 78   Mc3 Mississippi    chilled   95
    ## 79   Mc3 Mississippi    chilled  175
    ## 80   Mc3 Mississippi    chilled  250
    ## 81   Mc3 Mississippi    chilled  350
    ## 82   Mc3 Mississippi    chilled  500
    ## 83   Mc3 Mississippi    chilled  675
    ## 84   Mc3 Mississippi    chilled 1000

------------------------------------------------------------------------

### Logical expressions

The simplest data type in R is **logical**, with only two values
allowed: `TRUE` and `FALSE`. It’s simple, but powerful and versatile, as
we’ll see in a moment. Logical values, as any other basic data type in R
can be combined into vectors.

#### Exercise 10

Create a logical vector named `my_logical` with 3 `TRUE` and 2 `FALSE`
values and call it. Note that `TRUE` and `FALSE` are internal R symbols
so you should not use quotation marks.

Expected result:

    ## [1]  TRUE  TRUE  TRUE FALSE FALSE

------------------------------------------------------------------------

> #### Logical values
>
> To save typing you can use `T` instead of `TRUE` and `F` instead of
> `FALSE`. Please make sure, however, that this doesn’t make your code
> leass readable. Formally, logical values correspond to `0` (`FALSE`)
> and `1` (`TRUE`) and behave accordingly in mathematical operations.

#### Exercise 11

Calculate the sum of `my_logical`

Expected result:

    ## [1] 3

------------------------------------------------------------------------

Logical vectors have one hugely important and useful characteristic:
they can be used for subsetting. To achieve this you need to provide a
logical vector with `TRUE` for the elements you want to keep and `FALSE`
for the elements you want to discard. The length of the logical vector
used for subsetting has to be equal to the number of elements (e.g.,
columns) in the object we want to subset.

#### Exercise 12

Save the first six rows of built-in `CO2` dataset to a variable. Then,
using a logical vector return its 1<sup>st</sup> and 5<sup>th</sup>
column.

Expected result:

    ##   Plant uptake
    ## 1   Qn1   16.0
    ## 2   Qn1   30.4
    ## 3   Qn1   34.8
    ## 4   Qn1   37.2
    ## 5   Qn1   35.3
    ## 6   Qn1   39.2

This works, but doesn’t seem to be really useful. To appreciate
subsetting with logical vectors, let’s move on!

------------------------------------------------------------------------

### Comparisons

We don’t usually create logical vectors manually. They are instead
created automatically as the result of various comparisons done by R.
The most common is checking for **equality**. The operator for equality
is the double equals sign (`==`).

#### Exercise 13

Check whether in R: 5 equals 5.00 and whether *π* equals 3.14.

Expected result:

    ## [1] TRUE

    ## [1] FALSE

------------------------------------------------------------------------

> #### Comparisons in R
>
> -   `==` equal
> -   `!=` not equal (different)
> -   `>` greater than
> -   `>=` greater than or equal to
> -   `<` less than
> -   `<=` less than or equal to

Note that when comparing two vectors with the symbols shown above, R
doesn’t consider the action as a single comparison. It rather compares
them element by element, recycling the shorter vector. The result is a
logical vector of length equal to the length of the longer vector. The
rule is the same as for mathematical operations on vectors.

#### Exercise 14

Manually create two vectors. The first with prime numbers and the second
with even numbers from the range \<2, 9\>. Check whether they are
equal. Then, modify the first vector to be the same length as the second
one but make sure the outcome of comparison doesn’t change.

Expected result:

    ## [1]  TRUE FALSE FALSE FALSE

------------------------------------------------------------------------

To check whether entire vectors are identical use `identical()`
function.

#### Exercise 15

Create two integer vectors from 1 to 10, name them differently and
compare them with `identical()` function. Then, change one element in
the first vector and repeat comparison.

Expected result:

    ## [1] TRUE

    ## [1] FALSE

------------------------------------------------------------------------

Another useful tool is `%in%` operator. It provides, for each element of
the first vector, information whether this element is present anywhere
in the second vector. Note that this action focuses on the first vector
only, so there is no recycling. The result is a logical vector of the
length equal to the that of the first vector.

#### Exercise 16

Create two character vectors, each consisting of a set of individual
characters. The first should contain your name and the second one a name
of another person from the group. Check how many letter your names have
in common.

------------------------------------------------------------------------

### Negation

The exclamation mark (`!`) works in R as the symbol of negation. Any
logical vector preceded by `!` will result in its reversal - `FALSE`
changed into `TRUE` and vice versa.

#### Exercise 17

Construct a vector of three `TRUE` values and return its negation.

Expected result:

    ## [1] FALSE FALSE FALSE

Typically, `!` is used to negate comparisons. Note that the idea is the
same as above: you negate a logical vector by negating the action that
produces it. Remember that negated comparison should be enclosed in
parentheses, e. g., `!(2 == 2)`.

#### Exercise 18

Create sequence of integers from the range \<1, 100\>, in which each
subsequent element is larger by 3 than the previous one. Then, create a
logical vector indicating which elements are larger than 50. Do not use
`>` sign.

Expected result:

    ##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [13] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
    ## [25]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE

### Logical operators

The real power of logical operation is provided by combining comparisons
(use parentheses for clarity). There are two basic logical operators:

-   `&` **AND** - condition is TRUE if both comparisons are TRUE
-   `|` **OR** - condition is TRUE if at least one comparison is TRUE

#### Exercise 19

For integer vector 1:10, create a logical vector indicating which
elements are smaller or larger than 5.

Expected result:

    ##  [1]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE

#### Exercise 20

For integer vector 1:10, create a logical vector indicating which
elements are divisible by both 2 and 3.

Expected result:

    ##  [1] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE

> #### `&`, `&&`, `|`, `||`
>
> R provides two versions of each AND (`&`, `&&`) and OR (`|`, `||`)
> operators. The difference between them is that `&&` and `||` when
> provided with vectors check only first elements. We won’t make much
> use of this distinction, but it’s good to remember that such things
> exist, as they are useful as you progress to more advanced use of R.
> For more discussion see
> [here](https://stackoverflow.com/questions/6558921/boolean-operators-and)

### `which()` function

Frequently, the question is not about logical vectors themselves but
rather about which elements of a vector fulfill a particular condition.
The answer is provided by `which()` function. It takes comparison as its
argument and returns a vector of indexes.

#### Exercise 21

Construct a vector with first 20 integers divisible by 3. Find positions
of its elements that are \>= 21?

Expected result:

    ##  [1]  7  8  9 10 11 12 13 14 15 16 17 18 19 20

------------------------------------------------------------------------

#### Exercise 22

Having indexes from the previous exercise, return the corresponding
values from the vector.

Expected result:

    ##  [1] 21 24 27 30 33 36 39 42 45 48 51 54 57 60

------------------------------------------------------------------------

### Subsetting with logical expressions

As explained above, subsetting can be done directly with logical vectors
(elements in positions corresponding to TRUE in another vector are
retained) or indexes generated by `which()` function. In practice, it is
even simpler. All you need to provide is a condition instead of a
coordinate, i.e., `vector[condition]` will return only the elements
fulfilling the condition. The logic behind is as follows:  
1. Condition generates a logical vector of the length equal to that of
the original vector (the one you want to subset); in this logical vector
`TRUE` is in positions of the original vector that fulfill the condition
and `FALSE` is in the remaining positions.  
2. Returned are only those elements of the original vector that
correspond to `TRUE` in the logical vector

#### Exercise 23

For integer vector 1:100, return elements larger than vector’s mean.

Expected result:

    ##  [1]  51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69
    ## [20]  70  71  72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88
    ## [39]  89  90  91  92  93  94  95  96  97  98  99 100

## Operations on data frames, part 1

### Replacement

Assign a particular value to a specific position in your your data frame
with the use of the assignment arrow `<-`. It works just as with
variable assignment: `data_frame[row_number,column_number] <- new_value`

#### Exercise 24

Replace 5<sup>th</sup> value in the column `Type` of `my_data` with the
label `"Unknown"`. Check whether this was indeed replaced.

------------------------------------------------------------------------

### Mathematical operations

You can use standard mathematical operators: `+`, `-`, `*` and `/`.
Remember, however, that mathematical operations make sense only for
**numeric** data types.

#### Exercise 25

The `conc` column of `my_data` gives CO2 concentration in ul/L,
recalculate concentration to ml/L and modify the column. Display the
modified column.

Expected result:

    ##  [1] 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500
    ## [13] 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250
    ## [25] 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095
    ## [37] 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675
    ## [49] 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350
    ## [61] 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000 0.095 0.175
    ## [73] 0.250 0.350 0.500 0.675 1.000 0.095 0.175 0.250 0.350 0.500 0.675 1.000

------------------------------------------------------------------------

Also, you can use simple summary functions from the previous class.

#### Exercise 26

Calculate the mean value of the `uptake` column.

Expected result:

    ## [1] 27.2131

------------------------------------------------------------------------

### Simple summaries

-   `nrow()` number of rows
-   `ncol()` number of columns
-   `summary()` descriptive statistics for each column

#### Exercise 27

Return the total number of cells within `my_data`.

Expected result:

    ## [1] 420

#### Exercise 28

Display summary of `my_data`. Note that the type of the info displayed
by `summary()` depends on the type of the data in a particular column.

Expected result:

    ##      Plant             Type         Treatment       conc           uptake     
    ##  Mc1    : 7   Mississippi:42   chilled   :42   Min.   :0.095   Min.   : 7.70  
    ##  Mc2    : 7   Quebec     :42   nonchilled:42   1st Qu.:0.175   1st Qu.:17.90  
    ##  Mc3    : 7                                    Median :0.350   Median :28.30  
    ##  Mn1    : 7                                    Mean   :0.435   Mean   :27.21  
    ##  Mn2    : 7                                    3rd Qu.:0.675   3rd Qu.:37.12  
    ##  Mn3    : 7                                    Max.   :1.000   Max.   :45.50  
    ##  (Other):42

Note that the type of the info displayed by `summary()` depends on the
type of the data in a particular column. Check what would change in
summary if you changed the type of the column `Type` to character.

### Deleting rows containing missing data

Missing data, as explained in the previous class, are represented as
`NA` (Not Available) in R. Many functions will raise an error every time
they encounter `NA` as their arguments or their parts. Many functions,
on the other hand, allow you to automatically discard `NA`. The default
behaviour of not ignoring `NA` is by design, as `NA`s actually carry
important information about your data.

#### Exercise 29

Choose one cell of `my_data` and replace its value with `NA`. Do not add
quotation marks as `NA` is an internal R symbol (just as *π*). Print the
entire row.

------------------------------------------------------------------------

Rows with missing data can be removed with `na.omit()` function. To save
changes, the result of `na.omit()` function must be assigned to
variable. In practice, as explained above, **deleting missing data must
be well justified and many functions have special arguments that inform
them how to deal with missing data, so you don’t have to remove them
from your data**.

> #### `is.na()`
>
> `is.na()` is a much used function that checks which elements of its
> argument are `NA`. It works with vectors including, of course, that of
> length one, as well as with data frames.

#### Exercise 30

Remove the row with missing data created in the previous exercise.
Replace `my_data` with such modified table. Remember that this action
cannot be undone.
