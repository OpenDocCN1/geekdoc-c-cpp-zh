# PROGRAMMING IN R

functions take file paths as arguments and otherwise assume that the named file or files reside in the current working directory. In this regard, the R functions getwd and setwd determine and reset, the location of the current working directory are described in Appendix B.

The operations performed by file.create, file.remove and file.copy can also be obtained with the Unix commands, rm and cp in Appendix A. The primary difference is that the further functions can be called directly inside an R session when the latter commands require use of the system function from Appendix B to pass a command to a shell.

Let us begin by discussing the import of data into R. For the moment, assume that the data of interest resides in a text file fileName in the pathToFile and the information in the file is formatted as a rectangular array with columns representing variables and the rows corresponding to observations. Then, the simplest option is to proceed via the command

```
A <- read.table(file = "pathToFile/fileName")
```

This reads fileName as a data frame and the assignment operator <- places the result in data frame object. The data is presumed to be white-space delimited. If this is not the case, another delimiter can be specified using the sep argument for read.table. For example,

Once A has been imported into R, it may be edited in a spreadsheet-type environment via the command edit(A).

To illustrate a few of the features of read.table consider the group1.txt file shown below.

```
$ cat group1.txt
25 26 30 38
35 34 29 25
31 24 28 39
27 20 25 29
31 22 28 34
35 29 20 40
```

This rectangular array, or portions of it, can be imported directly via read.table.

```
A <- read.table("group1.txt")
A
V1 V2 V3 V4
1 25 26 30 38
2 35 34 29 25
3 31 24 28 39
4 27 20 25 29
5 31 22 28 34
6 35 29 20 40
```

By setting the nrows argument of read.table to 3 only the first three rows are imported as in

```
A <- read.table("group1.txt", nrows = 3)
A
V1 V2 V3 V4
1 25 26 30 38
2 35 34 29 25
3 31 24 28 39
```