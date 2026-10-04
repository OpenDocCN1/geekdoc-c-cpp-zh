Note that the first line is the header, the values are delimited with a single space, and missing values are denoted with an asterisk (*). Also, that each new record is required to start on a new line. Suppose you've handed this plain-text file for data analysis in R. The ready-to-use command read.table imports table-format files, producing a data frame object, as follows:

```
R mydatafile <- read.table(file="/Users/tdavies/mydatafile.txt", header=TRUE,sep=" ",na.strings="*", stringsAsFactors=FALSE)

R mydatafile
person age sex few.mon
1 Peter NA M High 504
2 Lois 40 F <NA> 480
3 Meg 17 F Low 204
4 Chris 14 M Med 168
5 Stevie 1 M High NA
6 Brian NA M Med NA
```

In a call to read.table, file takes a string with the filename and folder location (using forward slashes), header is a logical value telling R whether file has a header (TRUE in this case), sep takes a character string representing the delimiter (a single space, " "), na.strings requests the characters used to denote missing values ("*" in this case).

If you're reading multiple files and don't want to type the entire folder location each time, it's possible to first set your working directory viasetwd (Section 1.2.3) and then simply use the filename and its extension as the character string supplied to the file argument. However, both approaches require you to know exactly where your file is located when you're working at the R prompt. Fortunately, R possesses useful tools that should forget your file's precise location. You can view the output of the contents of any folder by using list.files. The following example betrays the mess of my local directory.

```
R list.files("/Users/tdavies")
[1] "bands-SCHIST1l200.txt" "Desktop"
[4] "Documents" "Downloads"
[7] "Dropbox" "Exercise2-20Data.txt" "Google Drive"
[10] "icloud" "Library" "log.txt"
[13] "Movies" "Music" "mydata.txt"
[16] "OneDrive" "peritonitis.sav" "peritonitis.txt"
[19] "Personal94144" "Pictures" "Public"
[22] "Research" "Rintro.txt" "Rprofile.txt"
[25] "Rstartup.R" "spreadsheet.csv" "spreadsheet.xlsx"
[28] "TakeHome_template.txt" "WISE-P2L" "WISE-P2S.txt"
[31] "WISE-SCHIST1l200.txt"
```