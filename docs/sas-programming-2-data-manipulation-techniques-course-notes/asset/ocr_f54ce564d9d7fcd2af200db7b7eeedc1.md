# Program Naming Conventions

In this course, you retrieve and save SAS programs using the structure below.

+   1 course ID
2 chapter #
3 type
na=activity
d=demo
e=exercise
s=solution
4 item #
5 place-holder

![](bbox=[0.305, 0.175, 0.568, 0.303])

Programming 2, Chapter 4, Demo 1

# Locating Data Files

In this course, macro variable references are used to give a more flexible approach for locating files.

Examples:

```
%let path=s:\workshop;
```

```
infile "&path\sales.csv";
```

```
infile "&path\payroll.dat";
```