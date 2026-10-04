```
2 85 185  male
3 75 174  male
4 42 154  female
5 93 188  male
6 63 178  male
7 58 170  female
8 75 167  male
9 89 181  male
10 67 178 female
```

Here, the file argument again specifies the desired file, which has no header, so header=FALSE. You set stringsAsFactors=TRUE because you do want to treat the sex variable (the only non-numeric variable) as a factor. There are no missing values, so you don’t need to specify na.strings (though if there were, this argument is simply used in the same way as earlier), and by definition, .csv files are comma-delimited, which read.csv correctly implements by default, so you don’t need the sep argument. The resulting data frame, spread, can then be printed in your R console.

As you can see, reading tabular data into R is fairly straightforward—you just need to be aware of how the data file is headed and delimited and how missing entries are identified. The simple table format is a natural and common way for data sets to be stored, but if you need to read in a file with a more complicated structure, R and its contributed packages make available some more sophisticated functions. See, for example, the documentation for the scan and readLines functions, which provide advanced control over how to parse a file. You can also find documentation on read.table and read.csv by accessing ?read.table from the prompt.

# 8.2.3 Web-Based Files

With an Internet connection, R can read in files from a website with the same read.table command. All the same rules concerning headers, delimiters, and missing values remain in place; you just have to specify the URL address of the file instead of a local folder location.

As an example, you’ll use the online repository of data sets made available by the Journal of Statistics Education (JSE) through the American Statistical Association at http://www.amstat.org/publications/jse/jse_data_archive.htm.

One of the first files linked to at the top of this page is the table-format data set 4cdata.txt (http://www.amstat.org/publications/jse/v9n2/4cdata.txt), which contains data on the characteristics of 308 diamonds from an analysis by Chu (2001) based on an advertisement in a Singaporean newspaper. Figure 8-5 shows the data.

You can look at the documentation file (4c.txt) and the accompanying article linked from the JSE site for details on what is recorded in this table. Note that of the five columns, the first and fifth are numeric, and the others would be well represented by factors. The delimiter is blank whitespace, there’s no header, and there are no missing values (so you don’t have to specify a value used to represent them).