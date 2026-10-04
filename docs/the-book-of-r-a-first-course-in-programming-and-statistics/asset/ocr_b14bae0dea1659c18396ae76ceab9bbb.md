the number of lines at the top of the file that should be ignored before R begins the import.

As mentioned in Section 8.2.2, there are also contributed packages that can cope with other statistical software files; however, if there are multiple worksheets within a file it can complicate things. The R package foreign (R Core Team, 2015), available from CRAN, provides support for reading data files used by statistical programs such as Stata, SAS, Minitab, and SPSS.

Other contributed packages on CRAN can help R handle files from various database management systems (DBMSs). For example, the RODBC package (Ripley and Lapsley, 2013) lets you query Microsoft Access databases and return the results as a data frame object. Other interfaces include the packages RMySQL (James and DebRoy, 2012) and RJDBC (Urbanek, 2013).

# 8.3 Writing Out Data Files and Plots

Writing out new files from data frame objects with R is just as easy as reading in files. R’s vector-oriented behavior is a fast and convenient way to recode data sets, so it’s perfect for reading in data, restructuring it, and writing it back out to a file.

# 8.3.1 Data Sets

The function for writing table-format files to your computer is write.table. You supply a data frame object as x, and this function writes its contents to a new file with a specified name, delimiter, and missing value string. For example, the following line takes the mydatafile object from Section 8.2 and writes it to a file:

```
R> write.table(x=mydatafile,file="/Users/tdavies/somenewfile.txt",
    sep="@",na="??",quote=FALSE,row.names=FALSE)
```

You provide file with the folder location, ending in the filename you want for your new data file. This command creates a new table-format file called somenewfile.txt in the specified folder location, delimited by @ and with missing values denoted with ?? (because you’re actually creating a new file, the file.choose command doesn’t tend to be used here). Since mydatafile has variable names, these are automatically written to the file as a header. The optional logical argument quote determines whether to encapsulate each non-numeric entry in double quotes (if you explicitly need them in your file for, say, formatting requirements of other software); request no quotes by setting the argument to FALSE. Another optional logical argument, row.names, asks whether to include the row names of mydatafile (in this example, this would just be the numbers 1 to 6), which you also omit with FALSE. The resulting file, shown in Figure 8-6, can be opened in a text editor.

Like read.csv, write.csv is a shortcut version of the write.table function designed specifically for .csv files.