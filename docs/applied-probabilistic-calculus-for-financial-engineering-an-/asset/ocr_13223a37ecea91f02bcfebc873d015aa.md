name gender age
1 A F 20
2 B M 30
3 C F 40

To read in such a file, use the function read.fwf():

+   - Skip the first line, which is the header.
+   - The width of each variable and the column names must be specified.

```
> a <- read.fwf("data2.txt", skip=1, width=c(1,1,2),
+ col.names = c("name", "gender", "age"),
+ as.is=TRUE)
```

# 4.4.1.3 Data Entry and Analysis Using the Function data.entry()

The previous section deals with creating data frames by reading in data created from programs outside R, such as Excel. It is also possible to enter data directly into R by using the function data.entry(). However, if the data size is large (say more than 15 columns and/or more than 25 rows), the chance of human error is high with the spreadsheet or text mode data entry. A software program specially designed for data entry, such as Epidata, is more appropriate. (http://www.epidata.dk)

# 4.4.1.4 Data Entry Using Several Available R Functions

The data set, in Table C, lists deaths among subjects who received a dose of tolbutamide or a placebo in the University Group Diabetes Program (1970), stratifying by age:

Table C**
Deaths Among Subjects Who Received Tolbutamide or a Placebo in the University Group Diabetes Program (1970)
Age < 55 Age ≥ 55 Combined
Tolbutamide Placebo Tolbutamide Placebo Tolbutamide Placebo
Deaths 8 5 22 16 30 21
Survivors 98 115 76 69 174 184
**Available at http://www.medepi.net/data/ugdp.txt

The R functions that can be used to import the data frame have been previously introduced in Sections 4.3.3–4.3.13 A convenient way to enter data at the command prompt is to use the R functions:

```
c(), matrix(), array(), apply(), list(), data.frame(), and odd.ratio(),
```