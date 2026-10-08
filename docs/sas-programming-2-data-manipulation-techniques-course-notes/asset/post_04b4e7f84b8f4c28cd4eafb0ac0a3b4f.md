
# Controlling Variable Output

The task is to drop Street_ID and Country from usa, drop Street_ID, Country, and State from australia, and keep all variables in other.

| ID | Employee_Name | Street_Name | City | State | Postal_Code |
|---|---|---|---|---|--|
| 120104 | Abbott, Roy | 627 | Edwards Mill Rd | FL | 39150 |
| 120769 | Akincluir, Tameka | 5 | Donkey Road | Philadelphia | PA | 19143 |
| 120868 | Cairns, Riley | 50 | California Ct | San Diego | CA | 92101 |

| ID | Employee_Name | Street_Name | City | Postal_Code |
|---|---|---|---|--|
| 120145 | Aliazetti, Sandy | 90 | Bingley Street | Melbourne | 2001 |
| 120508 | Durant, Kevin | 24 | Street Road | Sydney | 2118 |
| 120699 | Baker, Gabriela | 106 | Torak Road | |

| ID | Employee_Name | Street_ID | Street_Name | City | State | Postal_Code | Country |
|---|---|---|---|---|---|---|--|
| 120318 | Danielle, Scott | 80012167 | Sunderland | Philadelphia | 19150 | us |
| 120697 | Jonathan, Mary | 80012189 | 4623 | Philadelphia | PA | 19152 | us |
| 120747 | Farthing, Zelia | 80012756 | 789 | San Diego | CA | 92118 | us |

# DROP= Option in an Output Data Set

```
SAS-data-set(DROP=variable-1 <variable-2 ...variable-n>)
```

![](img/d3bde6e6ab06b1fc622215d982111742_59_0.png)

# Using the DROP= Data Set Option

```
data usa(drop=Street_ID Country)
australia(drop=Street_ID State Country)
other;
set orion.employee_addresses;
if Country='US' then output usa;
else if Country='AU' then
  output australia;
else output other;
run;
```

NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations
and 2 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations
and 6 variables.
NOTE: The data set WORK.OTHER has 8 observations
and 9 variables.

![](img/d3bde6e6ab06b1fc622215d982111742_60_0.png)

# KEEP= Option in an Output Data Set

```
SAS-data-set(KEEP=variable-1 <variable-2 ...variable-n>)
```

new1

| Y | Z |
|---|---|

old data new1(keep=y z)
new2(drop=x z)
new3;
set old;
...

PDV
| X | Y | Z |
|---|---|---|

| X | Y | Z |
|---|---|---|

new2

| X | Y | Z |
|---|---|---|

new3

| X | Y | Z |
|---|---|---|

![](img/d3bde6e6ab06b1fc622215d982111742_60_1.png)

2-34 Chapter 2 Controlling Input and Output

# Using the DROP= and KEEP= Options

The DROP= and KEEP= options can both be used
in a SAS program.

```
data usa (keep=Employee_Name City State)
      australia (drop=Street_ID State)
      other;
      set orion.employee_addresses;
      if Country='US' then output usa;
      else if Country='AU' then output australia;
      else output other;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_61_0.png)

In many cases, you have a choice between using a DROP= or KEEP= data set (or DROP
or KEEP= statements). Often the data option or statement minimizes the amount of typing
is selected.

# 2.06 Short Answer Poll

The data set orion.employee_addresses contains nine
variables. How many variables are in the usa, australia,
and other data sets?

```
data usa (keep=Employee_Name City Country)
      australia (drop=Street_ID State Country)
      other;
      set orion.employee_addresses;
      if Country='US' then output usa;
      else if Country='AU' then output australia;
      else output other;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_61_1.png)

Copyright © 2014, SAS Inc., Cary, North Carolina. ALL RESERVED.

# 2.3 Selecting Variables and Observations

# Using DROP= in an Input Data Set

When a DROP= data option is used in an input set, the specified variables are not read into the PDV and therefore are not available for processing.

| old | data new1 new2; set old(drop=x); ... |
| X Y Z | | |
| new1 |
| Y Z | |
| PDV |
| Y Z | |
| new2 |
| Y Z | |

![](img/d3bde6e6ab06b1fc622215d98211742_62_0.png)

# Using KEEP= in an Input Data Set

When a KEEP= data set option is used used, only the specified variables are read into the PDV and therefore are available for processing.

| old | data new1 new2; set old(keep=y z); ... |
| X Y Z | | |
| new1 |
| Y Z | |
| PDV |
| Y Z | |
| new2 |
| Y Z | |

![](img/d3bde6e6ab06b1fc622215d98211742_62_1.png)

# 2.07 Short Answer Poll

Open file orion.employee_addresses and submit it. The intent is to drop Country, Street_ID, and Employee_ID from every data set, and to drop State from australia. What is wrong with the program?

```
data australia (drop=State) other;
set orion.employee_addresses
(drop=Country Street_ID Employee_ID);
if Country='US' then output usa;
else if Country='AU' then output australia;
else output other;
```

# Improved Solution

Use a combination of the DROP= option and the DROP statement to achieve the desired results.

```
data australia (drop=State) other;
set orion.employee_addresses
(drop=Street_ID Employee_ID);
drop Country;
if Country='US' then output usa;
else if Country='AU' then output australia;
else output other;
```

| PDV | Country | Employee_Name | Postal_Code | State | Street_Name | Street_ID |
|---|---|---|---|---|---|---|
| | | | | | | |

If a DROP or KEEP statement is used in the same step as a data option, the statement is applied first. Attempting to drop and keep the same variable in a data set results in a warning.

# Check the SAS Log

NOTE: There were 424 observations read from the data set ORION.EMPLOYEE_ADDRESS.
NOTE: The data set WORK.USA has 311 observations
and 8 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations
and 8 variables.
NOTE: The data set WORK.OTHER has 8 observations
and 6 variables.

![](img/d3bde6e6ab06b1fc622215d982111742_64_0.png)

# Controlling Variable Input

| Input SAS data set | Raw data file |
|---|---|
| DROP= and KEEP= in an input data set | Affects contents of PDV |
| PDV | DROP and KEEP statements |
| DROP and KEEP= in an output data set | Output SAS data set |

The DROP= and KEEP= data set options can be used to exclude variables from processing in a PROC step.

```
proc print data=orion.employee_addresses (keep=Employee_Name City State Country);
run;
```

However, the DROP= and KEEP= data set options do not affect the order in which the variables are processed.

# Controlling Which Observations Are Read

By default, SAS processes every observation in a SAS data set, from the first observation to the last. The FIRSTOBS= and OBS= data set options can be used to control which observations are processed.

The FIRSTOBS= and OBS= options are with input data sets. You cannot use either option with output data sets.

# Using the OBS= Data Set Option

This OBS= data option causes the DATA step to processing after observation 100.

```
data australia;
  set orion.employee_addresses (obs=100);
  if Country='AU' then output;
run;
```

# Partial SAS Log

```
NOTE: There were 100 observations read from the data set ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.AUSTRALIA has 24 observations and
9 variables.
```

specifies a positive integer that is less than or equal to the number of observations in the data set, or zero.

# Using OBS= and FIRSTSTOBS= Data Set Options

The FIRSTSTOBS= and OBS= data set options cause the SET statement below to read 51 observations from orion.employee_addresses. Processing begins with observation 50 and ends after observation 100.

```
data australia;
  set orion.employee_addresses
  (firststobs=50 obs=100);
  if Country='AU' then output;
run;
```

# Check the SAS Log

Partial SAS Log

```
640 data australia;
641   set orion.employee_addresses(firststobs=50 obs=100);
642   if Country='AU' then output;
643 run;
```

NOTE: There were 51 observations read from the data set ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.AUSTRALIA has 13 observations and
9 variables.

# Controlling Which Records Are Read

The FIRSTOBS= OBS= options can be used in an INFILE statement when SAS reads from raw data files.

```
data employees;
infile "&path\emps.dat" firstobs=11 obs=15;
input @1 EmpID 8. @9 EmpName $40;
  @153 Country $2;

run;
proc print data=employees;
run;
```

The syntax is different. In an INFILE statement, the options are not enclosed in parentheses.

# Check the Output

Partial SAS Log

```
45 data employees;
46 infile "&path\emps.dat" firstobs=11 obs=15;
47 input @1 EmpID 8. @9 EmpName $40. @153 Country $2;
48 run;

NOTE: records were read from the infile 'emps.dat'.
NOTE: The data set WORK.EMPLOYEES has 5 observations and
3 variables.
```

# PROC PRINT Output

| Obs | EmpID | EmpName | Country |
|---|---|---|---|
| 1 | 120117 | Arizendi, Gilbert | US |
| 2 | 121062 | Armant, Debra | US |
| 3 | 121119 | Armogida, Bruce | US |
| 4 | 120812 | Arruza, Pauver | US |
| 5 | 120756 | Asta, Wendy | US |
