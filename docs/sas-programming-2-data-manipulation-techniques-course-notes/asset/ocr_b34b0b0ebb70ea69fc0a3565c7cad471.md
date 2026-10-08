# BY-Group Processing

The BY statement in the DATA step enables
SAS to process data in groups.

```
proc sort data=orion.specialsals
  out=salsort;
  by Dept;
run;
ndata deptals (keep=Dept DeptSal)
  set salsort;
  by Dept;
  <additional SAS statements>
run;
```

Step 1:
Sort by
Dept.

Step 2:
Process
by Dept
groups.

First.BY-variable
Last.BY-variable

A BY statement in a DATA step creates two temporary
variables for each variable listed in the BY statement.

When a BY statement is used with a SET statement, the data must be sorted by the BY variable
or have an index based on the BY variable(s).

The SORT procedure

+   - orders SAS data set observations by the values of one or more character or numeric variables
- replaces the original data set or creates a new data set
- produces only an output data set.

# First. / Last. Values: First DATA Step Iteration

| Dept | Salary | First.Dept |
|---|---|-|
| ADMIN | 20000 | 1 |
| ADMIN | 100000 | |
| ADMIN | 50000 | |
| ENGINR | 25000 | |
| ENGINR | 20000 | |
| ENGINR | 23000 | |
| ENGINR | 27000 | |
| FINANC | 10000 | |
| FINANC | 12000 | |

> Last.Dept
How can SAS determine the value for Last.Dept?