# FILE INPUT AND OUTPUT

```
> mean(A, na.rm = TRUE)
Sample1 Sample2 Sample3 Sample4
27.80000 26.00000 26.66667 33.00000
```

The workhorse function that underlies abbreviated read.table is scan. This function provides great flexibility in reading input at the expense of generally having to manually reshape the data that it imports. To accomplish this scan is used with no arguments at which point data may be entered directly until the process is terminated by input of a blank line. As an illustration, a segment from an R session is shown where scan was used to place the integers from 1 to 10 in a numeric object.

```
> v <- scan()
1: 1
2: 2 3
4: 4 5 6 7
8: 8 9 10
Read 10 items
> v
[1] 1 2 3 4 5 6 7 8 9 10
```

More generally, an abbreviated prototype for scan

```
scan(file, what, n)
```

The file argument is the name of the file to be read with a path specification if it does not reside in the current working directory. The n argument determines the number of values to read from the file; the entire file will be read when this argument is not specified. The what argument indicates the type of data that will be read and defaults to double(0). The seemingly innocuous syntax for scan conveys more than it may seem and provides a key point to the power and flexibility of scan.

As noted in Section 2.7, the primitive data types in R include character, integer and logical as well as numeric as is also equivalent to double. These data types are also classes in R with constructors that are invoked through use of the class name. In particular, we see from

```
> integer(2)
[1] 0 0
> logical(1)
[1] FALSE
> numeric(3)
[1] 0 0 0
> character(2)
[1] " " ""
```

that one of these constructors with an integer n as its argument will produce a vector of length consisting of the default values for that data type. The special cases character(0), integer(0), logical(0) and numeric(0) (or double(0)) produce zero or "empty" objects of type character, integer, logical and numeric, respectively. Thus, we can understand the specification of what=double(0) in scan as a means of indicating that the data to be read will be of type numeric and, similarly, using the other options character(0), integer(0) or logical(0) will serve the same basic purpose.