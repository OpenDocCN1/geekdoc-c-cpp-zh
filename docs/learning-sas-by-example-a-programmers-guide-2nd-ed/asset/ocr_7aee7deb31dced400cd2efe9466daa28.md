# Chapter 26: Introducing the Structured Query Language 439

Here is the output that resulted from this program:

Figure 26.2: Output from Program 26.1

| Subj | Height | Weight |
|---|---|--|
| 001 | 68 | 155 |
| 003 | 74 | 250 |

If you want to select all the variables from a data set, you can use an asterisk (*), like this:

Program 26.2: Using an Asterisk to Select all the Variables in a Data Set

```
proc sql;
select *
from Learn.Health
where Height gt 65;
quit;
```

If you want the result of the query to be stored in a SAS data set, include a CREATE TABLE statement, like this:

Program 26.3: Using PROC SQL to Create a SAS Data Set

```
proc sql;
create table Height65 as
select *
from Learn.Health
where Height gt 65;
quit;
```

# 26.3 Joining Two Tables (Merge)

Two Tables (used in the last example) and Demographic, are used to demonstrate various ways to perform joins using PROC SQL. Here are listings of these two tables:

Figure 26.3: Listing of Tables Health and Demographic

| Subj | Height | Weight | Subj | DOB | Gender | Name |
|---|---|---|---|---|---|-|
| 001 | 68 | 155 | 001 | 10/15/1960 | M | Friedman |
| 003 | 74 | 250 | 002 | 08/01/1955 | M | Stern |
| 004 | 63 | 110 | 003 | 12/25/1988 | F | McGoldrick |
| 005 | 60 | 95 | 005 | 05/28/1949 | F | Chien |