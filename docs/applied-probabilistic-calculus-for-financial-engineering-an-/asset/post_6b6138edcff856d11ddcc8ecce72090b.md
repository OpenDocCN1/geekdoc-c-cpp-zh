
```
3 13 1 0
4 18 1 1
5 23 1 1
6 28 1 0
7 31 1 1
8 34 1 1
9 45 1 0
10 48 1 1
11 161 1 0
12 5 0 1
13 5 0 1
14 8 0 1
15 8 0 1
16 12 0 1
17 16 0 0
18 23 0 1
19 27 0 1
20 30 0 1
21 33 0 1
22 43 0 1
23 45 0 1
>
```

Later, in Section 6.3, this data set will be revisited and further processed for survival analysis.

## 4.4.1.2 Obtaining a Data Frame from a Text File

Data from various sources are often entered using many different software programs.

They may be transferred from one format to another through the ASCII file format.

For example, in Windows, a text file is the most common ASCII file, usually having a ".txt" extension. There are other files in ASCII format, including the ".R" command file.

Data from most software programs can be outputted or saved as an ASCII file. From Excel, a very common spreadsheet program, the data can be saved as ".csv" (comma separated values) format. This is an easy way to interface between Excel spreadsheet files and R. Open the Excel file and "save as" the csv format.

### Files with field separators

As an example, suppose the file "csv1.xls" is originally an Excel spreadsheet. After "save as" into csv format, the output file is called "csv1.csv", the contents of which is

```
"name","gender","age"
"A", "F", 20
"B", "M", 30
"C", "F", 40
```

The characters are enclosed in quotes and the delimiters (variable separators) are commas. Sometimes the file may not contain quotes, as in the file "csv2.csv".

```
name, gender, age
A, F, 20
B, M, 30
C, F, 40
```

For both files, the R command to read in the data set is the same.

```r
> a <- read.csv("csv1.csv", as.is=TRUE)
> a
  name gender age
1 A    F      20
2 B    M      30
3 C    F      40
```

The argument `as.is=TRUE` keeps all characters as they are, otherwise the characters would have been coerced into factors. The variable `name` should not be factored but `gender` should. The following command should, therefore, be entered

```r
> a$gender <- factor(a$gender)
```

Note that the object "a" has class data frame and that the names of the variables within the data frame "a" must be referenced using the dollar sign notation `$`. Otherwise, R will state that the object "gender" cannot be found.

For files with white space (spaces and tabs) as the separator, such as in the file "data1.txt", the command to use is `read.table()`:

```r
> a <- read.table("data1.txt", header=TRUE,
+                 as.is=TRUE)
```

### Files without field separators

Consider the file "data2.txt" which is in fixed field format without field separators.

```
name gender age
1 A F 20
2 B M 30
3 C F 40
```

To read in such a file, use the function `read.fwf()`:

- Skip the first line, which is the header.
- The width of each variable and the column names must be specified.

```r
> a <- read.fwf("data2.txt", skip=1, width=c(1,1,2),
+ col.names = c("name", "gender", "age"),
+ as.is=TRUE)
```

## 4.4.1.3 Data Entry and Analysis Using the Function data.entry()

The previous section deals with creating data frames by reading in data created from programs outside R, such as Excel. It is also possible to enter data directly into R by using the function `data.entry()`. However, if the data size is large (say more than 15 columns and/or more than 25 rows), the chance of human error is high with the spreadsheet or text mode data entry. A software program specially designed for data entry, such as Epidata, is more appropriate. (http://www.epidata.dk)

## 4.4.1.4 Data Entry Using Several Available R Functions

The data set, in Table C, lists deaths among subjects who received a dose of tolbutamide or a placebo in the University Group Diabetes Program (1970), stratifying by age:

**Table C**  
Deaths Among Subjects Who Received Tolbutamide or a Placebo in the University Group Diabetes Program (1970)

| | Age < 55: Tolbutamide | Age < 55: Placebo | Age ≥ 55: Tolbutamide | Age ≥ 55: Placebo | Combined: Tolbutamide | Combined: Placebo |
|---|---|---|---|---|---|---|
| Deaths | 8 | 5 | 22 | 16 | 30 | 21 |
| Survivors | 98 | 115 | 76 | 69 | 174 | 184 |

Available at http://www.medepi.net/data/ugdp.txt

The R functions that can be used to import the data frame have been previously introduced in Sections 4.3.3–4.3.13. A convenient way to enter data at the command prompt is to use the R functions:

`c()`, `matrix()`, `array()`, `apply()`, `list()`, `data.frame()`, and `odds.ratio()`,

as shown by the following examples and using the data in Table C.

```r
> # Entering data for a vector
> vector1 <- c(8, 98, 5, 115) # Using data from Table C.
> vector1
[1] 8 98 5 115
> 
> vector2 <- c(22, 76, 16, 69); vector2 # Data from Table C.
[1] 22 76 16 69
>
```

```r
> # Entering data for a matrix
> matrix1 <- matrix(vector1, 2, 2)
> matrix1
     [,1] [,2]
[1,]    8    5
[2,]   98  115
> matrix2 <- matrix(vector2, 2, 2); matrix2
     [,1] [,2]
[1,]   22   16
[2,]   76   69
>
```

```r
> # Entering data for an array
> udata <- array(c(vector1, vector2), c(2, 2, 2))
> udata
, , 1
     [,1] [,2]
[1,]    8    5
[2,]   98  115
, , 2
     [,1] [,2]
[1,]   22   16
[2,]   76   69
> udata.tot <- apply(udata, c(1, 2), sum); udata.tot
     [,1] [,2]
[1,]   30   21
[2,]  174  184
>
```

```r
> # Entering a list
> x <- list(crude.data = udata.tot, stratified.data =
+ udata)
> x$crude.data
     [,1] [,2]
[1,]   30   21
[2,]  174  184
> x$stratified.data
, , 1
     [,1] [,2]
[1,]    8    5
[2,]   98  115
, , 2
     [,1] [,2]
[1,]   22   16
[2,]   76   69
>
```

```r
> # Entering a simple data frame
> subjectname <- c("Peter", "Paul", "Mary")
> subjectnumber <- 1:length(subjectname)
> age <- c(26, 27, 28) # These are their true ages,
> # respectively, in 1964!
> gender <- c("Male", "Male", "Female")
> data1 <- data.frame(subjectnumber, subjectname,
+ age, gender)
> data1
```

|  | subjectnumber | subjectname | age | gender |
|---|---|---|---|---|
| 1 | 1 | Peter | 26 | Male |
| 2 | 2 | Paul | 27 | Male |
| 3 | 3 | Mary | 28 | Female |

```r
> # Entering a simple function
> odds.ratio <- function(aa, bb, cc, dd) {aa*dd /
+ (bb*cc)}
> odds.ratio(30, 174, 21, 184) # Data from Table C.
[1] 1.510673
```

## 4.4.1.5 Data Entry and Analysis Using the Function scan()

The R function `scan()` is taken from the CRAN package base.

This function reads data into a vector or list from the console or file.

This function takes the following usage form:

```r
scan(file = "", what = double(), nmax = -1, n = -1,
    sep = "",
    quote = if(identical(sep, "\n")) "" else "'",
    dec = ".",
    skip = 0, nlines = 0, na.strings = "NA",
    flush = FALSE, fill = FALSE, strip.white = FALSE,
    quiet = FALSE, blank.lines.skip = TRUE, multi.line = TRUE,
    comment.char = "", allowEscapes = FALSE,
    fileEncoding = "", encoding = "unknown", text)
```

### Argument

`what` — The type of `what` gives the type of data to be read.

The supported types are logical, integer, numeric, complex, character, raw, and list. If `what` is a list, it is assumed that the lines of the data file are records each containing `length(what)` items (fields) and the list components should have elements that are one of the first six types listed or NULL.

The `what` argument describes the tokens that `scan()` should expect in the input file.

For a detailed description of this function, execute

```r
> ?scan
```

The methodology of applying `scan()` is similar to `c()`, as described in Section 4.4.1.4, except that it does not matter whether the numbers are entered on different lines; it will still be a vector.

- Use `scan()` when accessing data from a file that has an irregular or a complex structure.
- Use `scan()` to read individual tokens and use the argument `what` to describe the stream of tokens in the file.
- `scan()` converts tokens into data, and then assembles the data into records.
- Use `scan()` along with `readLines()`, especially when one attempts to read an unorthodox file format. Together, these two functions will likely result in a successful processing of the individual lines and tokens of the file!

The function `readLines()` reads lines from a file, and returns them to a list of character strings:

```r
> lines <- readLines("input.txt")
```

One may limit the number of lines to be read, per pass, by using the `n` parameter that gives the maximum number of lines to be read:

```r
> lines <- readLines("input.txt", n=5)
> # read 5 lines and stop
```
