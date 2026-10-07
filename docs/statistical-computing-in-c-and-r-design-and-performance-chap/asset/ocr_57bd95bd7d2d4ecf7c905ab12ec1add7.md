# 184 PROGRAMMING IN R

```
> drawData <- NULL
> for(i in 100)
+ drawData <- c(drawData, scan("guess5.txt", skip = 1, nlines = 10,
+ quiet(drawData))
+ length(drawData)
[1] 5000
```

Note the use of NULL to initialize the drawData array. Analogous results would be obtained using a class constructor for either the vector or matrix class with an empty argument: e.g., drawData <- vector(). Failure to initialize the concatenation operator would have caused an error the first time the loop used as its drawData argument would not exist.

The fact that guess5.txt contains a character and numeric data of unequal length precludes the use of read.table for importing the file. Our for loop formulation perhaps the most obvious (at least to a C/C++ programmer). Alternatively,

avoids explicit loop and instead, relies on the inherent features of R. To examine this approach, let us work out from the interior of the expression. As noted in Section 5.2, the readLines function brings in the content of a file as an array of character strings. Thus, the effect of

```
readLines("guess5.txt")
```

is to bring in a vector with 1100 rows corresponding to the 1100 (= 11 × 100) rows in the guess5.txt file. seq(1, 1090, 11) produces the integer collection {1, 11, ..., 1090} that corresponds to the rows of guess5.txt where the date and other numeric drawing information remains. Pending – to these indices removes them from the array created with readLines. So, at the completion of

```
readLines("guess5.txt")[-seq(1, 1090, 11)]
```

command, an array containing 10000 (= 1100–100) strings has created with each string containing the five integers by drawing for the guess5 data. The remainder of the import command uses strsplit, unlist and as integer exactly as in Section 5.2 to convert the strings to their integer format.

Another approach for reading the guess5.txt file‡ is

```
> drawData <- scan(readLines("guess5.txt")
+ -seq(1, 1090, 11)), what = integer(0))
Read 5000 items
```

The initial import of data via readLines is the same as before. The difference begins with the use of the textConnection function which enables an object creating character strings to be read by a function from a connection (as discussed in Section 5.2). In this case, the function that the connects is a scan. The application of textConnection makes the output of readlines appear to scan as a file of 5000 numbers which can be read in the usual way.

Now we have three ways to import guess5.txt information. Which one works the best? The system.time function from Section 5.4 provides one of comparison. Applying it to two different import schemes

> ‡ This is motivated by the strsplit approach. It was kindly suggested by one of this book's reviewers.