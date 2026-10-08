
# Performing Repetitive Calculations

```sas
data charity;
set orion.employee_donations;
keep employee id qtr1-qtr4;
Qtr1=Qtr1*1.25;
Qtr2=Qtr2*1.25;
Qtr3=Qtr3*1.25;
Qtr4=Qtr4*1.25;
run;
proc print data=charity noobs;
run;
```

# Partial PROC PRINT Output

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 120267 | 18.75 | 18.75 | 18.75 | 31.25 |
| 120269 | 25.00 | 25.00 | 25.00 | 25.00 |
| 120270 | 25.00 | 12.50 | 6.25 | - |

![](img/d3bde6e6ab06b1fc622215d982111742_309_0.png)

# Performing Repetitive Calculations

The four calculations cannot be replaced by a single calculation inside a DO loop because they are not identical.

```sas
data charity;
set orion.employee_donations;
keep employee id qtr1-qtr4;
Qtr1=Qtr1*1.25;
Qtr2=Qtr2*1.25;
Qtr3=Qtr3*1.25;
Qtr4=Qtr4*1.25;
do i=1 to 4;
?
end;
run;
proc print data=charity noobs;
run;
```

A SAS array can be used to simplify this code.

# Use Arrays to Simplify Repetitive Calculations

An array provides an alternate way to access values in the PDV, which simplifies repetitive calculations.

```sas
data charity;
  set orion.employee_donations;
  keep employee qtr1-qtr4;
 Qtr1=qtr1*1.25;
 Qtr2=qtr2*1.25;
 Qtr3=qtr3*1.25;
 Qtr4=qtr4*1.25;
run;
proc print data=charity noobs;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_310_0.png)

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |

# What Is a SAS Array?

SAS array

- - is a temporary grouping of SAS variables that are arranged in a particular order
- is identified by an array name
- must contain all numeric or all character variables
- exists only for the duration of the current DATA step
- is **not** a variable.

# Why Use a SAS Array?

Create an array named Contrib and use it to access the four numeric variables, Qtr1 – Qtr4.

![](img/d3bde6e6ab06b1fc622215d982111742_311_0.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|

SAS arrays are different from arrays in many other programming languages. In SAS, an array is not a data structure. It is simply a convenient way of temporarily identifying a group of variables.

# Array Elements

Each value in an array is called an element.

![](img/d3bde6e6ab06b1fc622215d982111742_311_1.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| First element | Second element | Third element | Fourth element |

# Referencing Array Elements

Each element is identified by a subscript that represents its position in the array. When you use an array reference, the corresponding value is substituted for the reference.

![](img/d3bde6e6ab06b1fc622215d982111742_312_0.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| | Contrib{1} | Contrib{2} | Contrib{3} | Contrib{4} |

# Defining an Array

The ARRAY statement is a compile-time statement that defines the elements in an array.

```sas
ARRAY array-name {subscript} $< <length> <array-elements>;
array Contrib{4} Qtr1 Qtr2 Qtr3 Qtr4;
```

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| | Contrib{1} | Contrib{2} | Contrib{3} | Contrib{4} |

array-name specifies the name of the array.

{subscript} describes the number and arrangement of elements in the array using an asterisk, a number, numbers separated by commas (for multi-dimensional arrays), a range of numbers, or an expression. The subscript is enclosed in braces ({}). Brackets ([]) and parentheses () are also allowed.

$ indicates that the elements in the array are character elements. The dollar sign is not necessary if the elements in the array were previously defined as character elements.

length specifies the length of elements in the array that were not previously assigned a length.

array-elements names the elements that make up the array. Array elements can be listed in any order.

- - Array references cannot be used in compile-time statements such as LABEL, FORMAT, DROP, KEEP, or LENGTH statements.

If you use a function name as the name of the array, SAS treats parenthetical references that involve the name as array references, not function references, for the duration of the DATA step.

- - The four variables, Qtr1, Qtr2, Qtr3, and Qtr4, can now be referenced via the array name Contrib, with an appropriate subscript.

![](img/d3bde6e6ab06b1fc622215d982111742_313_0.png)

- - You can use special SAS name lists to reference variables that were previously defined in the same DATA step. The _CHARACTER_ variable list lists character values only. The _NUMERIC_ variable list lists numeric values.

Avoid using the _ALL_ special SAS name list to reference variables, because the elements in an array must be either character or all numeric values.

# Defining an Array

Variables that are elements of an array do not need the following:
* to have similar, related, or numbered names
* be stored sequentially
* to be adjacent

```sas
array Amt(*) Q1 Q2 ThrdQ Qtr4;
AMT
PDV
ID Q1 Total ThrdQ Q2 Qtr4
Amt{1} Amt{3} Amt{2} Amt{4}
```

# 7.07 Short Answer Poll

Open and submit p207a04. What is the cause of the error?

```sas
data charity (keep=Employee ID Qtr1-Qtr4);
set orion.employee_donations;
array Contrib(3) Qtr1-Qtr4;
array Contrib(5) qtr;
/* additional SAS statements */
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_314_0.png)

# Using a DO Loop to Process an Array

```sas
data charity;
  set orion.employee_donations;
  keep ID Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

DO index-variable=1 TO number-of-elements-in-array

To reference an element, the index variable is often used as a subscript: array-name{index-variable}. To process particular elements of an array, specify these elements as the range of iterative DO statement. By default, SAS includes index-variable in the output set. Use a DROP or KEEP= set option to prevent the index variable from being written to the output set.

# First Iteration of the DO Loop

```sas
data charity;
  set orion.employee_donations;
  keep ID Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_315_0.png)

# Second Iteration of the DO Loop

```sas
data charity;
  set orion.employee_donations;
  keep ID Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_316_0.png)

# Third Iteration of the DO Loop

```sas
data charity;
  set orion.employee_donations;
  keep ID Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_316_1.png)

# Fourth Iteration of the DO Loop

```sas
data charity;
  set orion.employee_donations;
  keep ID Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
    when i=4
    Contrib{4}=Contrib{4}*1.25;
  end;
```

# Output: Using a Do Loop to Process Array

```sas
proc print data=charity noobs;
run;
```

Partial PROC PRINT Output

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 120267 | 18.75 | 18.75 | 18.75 | 31.25 |
| 120269 | 25.00 | 25.00 | 25.00 | 25.00 |
| 120270 | 25.00 | 12.50 | 6.25 | - |

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the folder.

# Level 1

# 5. Using Arrays for Repetitive Computations

Monthly customer order data for the first half of the year is stored in the data set orion.orders_midyear. Orion Star Sales manager is considering a 10% price decrease next year. The manager wants to see how such a discount would affect this year's income.

Partial orion.orders_midyear

| Obs | Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|---|
| 1 | | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 2 | 10 | 188.10 | 414.09 | 2876.9 | 3164.59 | 2373.44 | 169.29 |
| 3 | 11 | 78.20 | | | | 70.38 |
| 4 | 12 | | 135.60 | | 117.6 | 129.36 | 122.04 |
| 5 | 18 | | | | 29.4 | 32.34 | 24.26 |
| 6 | 24 | 93.00 | 265.80 | | | | 83.70 |
| 7 | 27 | 310.70 | 782.90 | | | | 279.63 |
| 8 | 31 | 1484.30 | 293.30 | | | | 1335.87 |
| 9 | 34 | 642.50 | | | 86.3 | 94.93 | 71.20 | 578.25 |
| 10 | 41 | | 134.00 | 119.20 | 313.0 | 344.30 | 258.23 | 120.60 |
| 11 | 45 | 443.88 | 216.20 | 40.2 | 44.22 | 33.17 | 399.49 |
| 12 | 49 | 24.80 | | | 111.72 | 122.89 | 92.17 | 115.94 |
| 18 | | | | | 27.93 | 30.72 | 23.04 | |

Partial PROC PRINT Output (24 Total Observations)

- a. Create a data set of discounts, to calculate the 5% discount.
- Create an array, Mon, to adjust Month1 through Month6.
- Use a DO loop to adjust each customer's monthly data. Apply the 5% discount.
- b. Print the resulting data set and verify your results.
- Add an appropriate title.
- Use the DOLLAR format for the monthly sales amounts.
