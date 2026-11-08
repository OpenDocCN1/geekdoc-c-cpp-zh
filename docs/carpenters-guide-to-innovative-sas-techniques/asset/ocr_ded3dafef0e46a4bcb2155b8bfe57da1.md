With recent enhancements (especially in SAS 8 and SAS®9), a number of additional capabilities have been added to the MEANS and SUMMARY procedures, and even the ‘seasoned’ programmer may not have been exposed to them. This chapter covers some of the more useful of these capabilities. Because these two procedures have the same capabilities and have very few differences, most of the examples and text in this chapter will highlight only one of them. In each case either of the two procedures could be used.

Prior to SAS 6, MEANS and SUMMARY were distinct procedures with overlapping capabilities. Currently the same software is used behind the scenes regardless of which procedure the user calls; therefore, their capabilities are now the same. The only real differences between these procedures are seen in their defaults, and then primarily in the way each procedure creates printed tables. By default MEANS always creates a table to be printed. If you do not want a printed table you must explicitly turn it off (NOPRINT option). On the other hand, the SUMMARY procedure never creates a printed table unless it is specifically requested (PRINT option).

# **SEE ALSO**

Carpenter (2008) discusses these two procedures in more detail, including an introduction as well as additional options not covered in this book.

# 7.1  Using Multiple CLASS Statements and CLASS Statement Options

Although the following discussion concerning the use of multiple CLASS statements and CLASS statement options is within the context of the MEANS and SUMMARY procedures, it can be generalized to most procedures that use the CLASS statement.

```
```sas
class race sex edu;
```
```

The CLASS statement can be specified as a single statement or it can be broken up into a series of CLASS statements. The order of the CLASS statements determines the overall order of the classification variables.

```
```sas
class race sex;
class edu;
```
```

```
```sas
class race sex;
class edu / missing;
```
```

The CLASS statement now accepts options and for most procedures that accept the CLASS statement, a single class statement can be replaced by a series of CLASS statements. This allows you to control the application of CLASS statement options to specific classification variables. One or more options

are specified on a CLASS statement by preceding the option with a slash. While it is not necessary to have multiple CLASS statements just to apply CLASS statement options, multiple CLASS statements allow you to apply these options differentially. For instance when you use the MISSING option on the PROC statement, it is applied to all of the classification variables. By using multiple CLASS statements along with the MISSING option on the CLASS statement, you can choose which classification variables are to utilize the MISSING option.

CLASS statement options include:

# **ASCENDING/DESCENDING (Section 7.1.1)**

Analogous to the DESCENDING option in PROC SORT and other procedures, these options allow you to reverse the order of the displayed values.