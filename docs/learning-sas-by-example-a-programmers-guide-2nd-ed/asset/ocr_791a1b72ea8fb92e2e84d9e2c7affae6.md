# Chapter 18: Creating Tabular Reports

+   18.1 Introduction ................................................................................ 299

+   18.2 A Simple PROC TABULATE Table ............................................................ 300

+   18.3 Describing the Three PROC TABULATE Operators ................................................ 301

+   18.3.1 Concatenation......................................................................................... 301

+   18.3.2 Table Dimensions (Page, Row, and Column)................................................ 302

+   18.3.3 Nesting...................................................................................................... 302

+   18.4 Using the Keyword ALL ...................................................................... 303

+   18.5 Producing Descriptive Statistics ........................................................ 304

+   18.6 Combining CLASS and Analysis Variables in a Table ................................ 306

+   18.7 Customizing Your Table ....................................................................... 307

+   18.8 Demonstrating a More Complex Table....................................................... 309

+   18.9 Computing Row and Column Percentages ................................................... 310

+   18.10 Displaying Percentages in a Two-Dimensional Table ........................ 312

+   18.11 Computing Column Percentages ................................................... 313

+   18.12 Computing Percentages on Numeric Variables......................................... 314

+   18.13 Understanding How Missing Values Affect PROC TABULATE Output ...... 315

+   18.14 Problems ...................................................................................... 318

# 18.1 Introduction

PROC TABULATE is an underused, underappreciated procedure that can create a wide variety of tabular reports, displaying frequencies, percentages, and descriptive statistics (such as sums and means) broken down by one or more CLASS variables. There are several excellent books devoted to PROC TABULATE. I recommend E. Haworth's book, PROC TABULATE By Example (Cary, NC: SAS Institute Inc., 1999), for one of the best and most complete books on this topic.

This chapter introduces you to this procedure and, we hope, piques your interest.

To demonstrate many of the features of PROC TABULATE, we will use a data set called Blood that has information on types, genders, age groups, red and white blood cell counts, and cholesterol levels. A listing showing the first 10 observations of this data set follows: