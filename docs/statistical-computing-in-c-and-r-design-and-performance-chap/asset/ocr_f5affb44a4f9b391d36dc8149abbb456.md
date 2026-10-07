# 156 PROGRAMMING IN R

> 1:4
[1] 1 2 3 4

produced by the sequence operator : from Appendix B.
Instead of assigning names to the rows and columns of an array on input, they may be\specified in the text file that contains the data. For our running example, this might be
t form of the group2.txt file listed below.

```
$ cat group2.txt
"Sample1" "Sample2" "Sample3" "Sample4"
"Row1" 25 26 30 38
"Row2" 25 34 29 25
"Row3" 31 24 28 39
"Row4" 27 20 25 29
#missing data in next 2 rows
```

Here the variable/column names are specified in a header and each row is given its own
ame in the file. If, as is the case here, the header contains one fewer than the first
row, read.table automatically processes if the first column contains row names.
There are three other features that appear in the group2.txt file. First, there is a
comment inserted by the R comment symbol #, a blank line appears after
the comment. We will see that read.table includes both comments and entries.
Of somewhat more substance is the presence of missing values in group2.txt. Missing
data are a common occurrence that arise from errors, nonresponsive, etc. A language such
is R that provides data analysis tools have effective means of dealing with missing
observations. In this regard, R functions have an na.action or na.rm argument that
can be used to determine how missing values are treated.

The default string for the argument na.string is is NA. Other values may also
be specified through the argument na.string that can be given a vector of character values.
To read the group2.txt file one could use

```
> A <- read.table("group2.txt", na.string = c("n", "q", "NA"))
> A
```

| Sample1 Sample2 Sample3 Sample4 |
| Row1 25 26 30 38 |
| Row2 25 34 29 25 |
| Row3 31 24 28 39 |
| Row4 27 20 25 29 |
| Row5 31 NA 28 34 |
| Row6 NA NA 20 NA |

Notice that the comment and blank line were ignored and that the symbols for all missing
values translated to the R logical constant NA. Operations can now be performed on the
A data frame as usual the missing values are handled appropriately. For example,
a rote application of the mean function to its imported data products

```
> mean(A)
1 Sample2 Sample3 Sample4
NA NA 26.6667 NA
```

By setting the na.rm argument for mean to TRUE the missing values will be omitted
from the calculations resulting in the output