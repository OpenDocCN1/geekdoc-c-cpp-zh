
One important feature to note here, though, is that it is difficult to distinguish between files and folders. Files will typically have an extension, and folders won't; however, WISE-P2L is a file that happens to have no extension and looks nothing different from any of the listed folders.

You can also find files interactively from R. The file.choose command opens your filesystem directly from the R prompt—just as any program does when you want to open something. Then, you can navigate to the folder of interest, and after you select your file (see Figure 8-3), only a character string is returned.

```
R> file.choose()
[1] "/Users/tdavies/myfiledata.txt"
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_185_0.png)

Figure 8-3: My local file navigator opened as the result of a call to file.choose. When the file of interest is opened, the R command returns the full path to file as a character string.

This command is particularly useful, as it returns the character string of the directory in the format that requires for a command such as read.table. So, calling the following line and selecting myfiledata.txt, as in Figure 8-3, will produce an identical result to the explicit use of the file in file, shown earlier:

If your file has been successfully loaded, it will be returned to the R prompt without issuing any error messages. You can check this with a call to myfiledata, which would return the data frame. When importing data into data frames, keep in mind the difference between character string observations and factor observations. No factor attribute information is stored in the plain-text file, read.table will convert non-numeric values into factors by default. Here, you want to keep some of your data saved as strings, so set stringsAsFactors=FALSE, which prevents R from treating all non-numeric elements as factors. This way, person, sex, and funny are all stored as character strings.

You can overwrite sex and funny with factor versions of themselves if you use them as that data type.

```
R mydatafilesex <- as.factor(mydatafilesex)
R mydatafile$funny <- factor(x=mydatafile$funny,levels=c("Low","Med","High"))
```

## 8.2.2 Spreadsheet Workbooks

Next, let's examine some ubiquitous spreadsheet software file formats. The standard file format for Microsoft Excel is .xls or .xlsx. In general, these files are not directly compatible with R. There are some competent package functions that attempt to bridge this gap—see, gdata by Barnes et al. (2014) or xtConnect by Mirai Solutions (2014)—but it's generally preferable to first export the spreadsheet to table format as CSV. Consider the hypothetical data from Exercise 7.1 (b), which has been stored in an Excel file spreadsheet.xlsx, shown in Figure 8-4.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_186_0.png)

Figure 8-4: A spreadsheet file of the data from Exercise 7.1 (b)

To read this spreadsheet with R, you should first convert it to table format. In Excel, File → Save As... provides a wealth of options. Save the spreadsheet as a comma-separated file, called spreadsheet.csv. R has a shortcut version of read.table, read.csv, for these files.

```
R spread <- read.csv(file="/Users/tdavies/spreadsheet.csv", header=FALSE,stringsAsFactors=TRUE)
```

```
R spread n1 V2 V3
1 55 161
2 85 185
3 75 174
4 42 154
5 93 188
6 63 178
7 58 170
8 75 167
9 89 181
10 67 178
```

Here, the file argument specifies the desired file, which has no header, header=FALSE. You set stringsAsFactors=TRUE because you want to treat the variable (the only non-numeric variable) as a factor. There are no missing values, so you don't need to specify na (though if there were, this argument is used in the same way as earlier), and by definition, .csv files are comma-delimited, read.csv correctly implements the desired data frame, spread, can then be printed in your R console.

As you can see, reading tabular data into R is straightforward—you just need to be aware of how the data is headed and how missing entries are identified. The simple table format is natural and common for data sets to be stored, but if you need to read a file with a more complicated structure, R and its packages make available more sophisticated functions. See for example, the documentation for scan and readLines which provide advanced control over how to parse a file. You can also find documentation on read.table and read.csv by accessing read.table from the prompt.

## 8.2.3 Web-Based Files

With an Internet connection, R can read files from a website with the same read.table command. The rules concerning headers, delimiters, and missing values remain in place; you just have to specify the URL address of the file instead of a local folder. As an example, you'll use the online repository of data sets available by the journal of Statistics Education (JSE) through the American Statistical Association at http://www.stat.org/publications/jse/jse_data_archive.html. One of the first files linked to the top of this page is the table-format data 4cd.txt (http://www.stat.org/publications/jse/v9n2/4cd.txt), which contains data on the characteristics of 308 diamonds from an analysis by Chu (2001) based on an advertisement in a Singaporean newspaper. Figure-8 shows the data you can look at the document (4cd.txt) and the accompanying article linked from the JSE site for details on what is recorded in this table. Note that of the five columns, the first and fifth are numeric, and the others would be represented by factors. The delimiter is whitespace, there's no header, and there are no missing values (so you don't have to specify a value to represent them).

![](img/b2cfc85cbb129f60fe595a2bae074fe4_188_0.png)

With this in mind, you can create a data frame directly from the R prompt with the following lines:

```
dia.url <- "http://amstat.org/publications/jse/v9n2/4data.txt"
diamonds <- read.table(dia.url)
```

Note that you haven't supplied any extra values to this call to read.table because the defaults work fine. Because there's no header in the table, you can leave the default header value FALSE. The default value for sep is " ", meaning whitespace (not to be confused with a space character), which is exactly what this table uses. The default value for stringsAsFactors is TRUE, which is what you want for your character columns. Following the import, you can supply names (based on the information in the documentation) to each column as:

```
names(diamonds) <- c("Carat","Color","Clarity","Cert","Price")
diamonds <- diamonds[1:5]
```

| Carat Color Clarity Cert Price |
|---|---|---|---|---|
| 1 | 0.30 | D | VS2 GIA 1302 |
| 2 | 0.30 | E | VS1 GIA 1510 |
| 3 | 0.30 | G | VVS1 GIA 1510 |
| 4 | 0.30 | G | VS1 GIA 1260 |
| 5 | 0.31 | D | VS1 GIA 1641 |

Viewing the first five records shows that the data frame is displayed as you intended.

## 8.2.4 Other File Formats

There are other file formats besides .txt or .csv files that can be read into R, such as the data format .dat. These files can also be imported using read.table, though they may contain extra information at the top that must be skipped using the optional skip argument. The skip argument asks for the number of lines at the top of the file that should be ignored before R begins the import.

As mentioned in Section 8.2.2, there are also contributed packages that can cope with other statistical software files; however, if there are multiple worksheets within a file it can complicate things. The R package foreign (R Core Team, 2015), available provides support for reading data files used by statistical programs such as Stata, SAS, Minitab, and SPSS.

Other contributed packages on CRAN can help your various database management systems (DBMSs). For example, the RJDBC package (Ripley and Laplace, 2023) lets you query Access databases and return the results as a data frame. Other interfaces include the packages MySQL (James and deRoy, 2012) and RSQLite (Urbanek, 2023).

## 8.3 Writing Out Data Files and Plots

Writing out files from data frame objects with R is just as easy as reading in. R's vector-oriented behavior is a fast and convenient way to record data sets, restructuring it, and writing back to file.

### 8.3.1 Data Sets

The function for writing table-format files to your computer is write.table. You supply a data frame object as x, and this function writes its contents to a new file with a specified name, delimiter, and value string. For example, the following line takes the mytable object from Section 8.2 and writes it to a file:

```
write.table(x=myDatafile,file="Users/tdavies/somefile.txt",sep="@",na="??",quote=FALSE,row.names=FALSE)
```

You provide file with the folder location, ending in the filename you want for your new data file. called somefile.txt in the specified folder location, delimited by & and with missing values denoted with ?? (because you are actually creating a new file, file.choose command doesn't tend to be used here). Since myfile has variable names, these are automatically written to the file as a header. The optional logical argument quote determines whether to encapsulate each non-numeric entry in double quotes (if you explicitly need them in your file formatting requirements of other software); no quotes by setting the argument to FALSE. Another optional logical argument, row.names, asks whether to include the row names of mymyfile (in this example, this would just be the numbers 1 to 6), which you also omit with FALSE.

Like read.csv, write.csv is a shortcut version of the write table function designed specifically for .csv.
