# # Date Lab

This assignment will focus on the use of functions and the passing of parameters. You are to construct a C program, date.c, which performs each of the following operations:

```
Converts a calendar date into a Julian date
Converts a Julian date into a calendar date.
Computes the number of days between any two calendar dates.
```

A calendar date is simply a date that contains a year, month, and day and a Julian date is an integer between 1 and 366, inclusive, which tells how many days have elapsed since the first of January in the current year (including the day for which the date is calculated). For example, calendar date 4/12/2008 is equivalent to Julian date 103, 2008.

Your program should contain a selection menu (hint: think do-while loop) that allows the user to choose one of the options. An illustration is given below:

```
DATE SELECTION MENU
1) Convert calendar date into Julian date
2) Convert Julian date into calendar date
3) Compute days between two calendar dates
4) Exit program
ENTER SELECTION (1 - 4):
```

Be sure your program contains separate functions for each of the required operations, passing parameters as necessary. Remember that no global variables are allowed in your program except for the file pointer. You should create at least the following functions for your program: