
# DO WHILE Statement

![](img/d3bde6e6ab06b1fc622215d982111742_299_0.png)

# 7.04 Short Answer Poll

How can you generate the same result with a DO WHILE statement?

```sas
data invest;
  do until (Capital>1000000);
    Year+1;
    Capital+5000;
    Capital+(Capital*.045);
  end;
run;
proc print data=invest noobs;
  format capital dollar14.2;
run;
```

do while (capital <= 1000000);
```

# Using DO WHILE with an Iterative DO Loop

Determine the value of the account again. Stop the loop if 30 years is reached or more than $250,000 is accumulated.

```sas
data invest;
  do Year=1 to 30 while (Capital<=250000);
    Capital+=5000;
    Capital+(Capital* .045);
  end;
run;
proc print data=invest noobs;
  format capital dollar14.2;
run;
```

PROC PRINT Output
<BY index-variable=start> WHILE | UNTIL

| Year | Capital |
| :--- | :--- |
| 28 | $264,966.67 |

# Using DO UNTIL with an Iterative DO Loop

Determine the value of the account again, but this time use a DO UNTIL statement.

```sas
data invest;
  do Year=1 to 30 until (Capital>250000);
    Capital+=5000;
    Capital+(Capital* .045);
  end;
run;
proc print data=invest noobs;
  format capital dollar14.2;
run;
```

In a DO UNTIL loop, the condition is checked *before* the index variable is incremented.

PROC PRINT Output

| Year | Capital |
| :--- | :--- |
| 27 | $264,966.67 |

# Business Scenario

Create one observation per year for five years, and show the earnings if you invest $5,000 per year with 4.5 percent annual interest compounded quarterly.

| Year | Capital |
| :--- | :--- |
| 1 | 5225.00 |
| 2 | 10699.95 |
| 3 | 16415.32 |
| 4 | 22395.39 |
| 5 | 28649.15 |

![](img/d3bde6e6ab06b1fc622215d982111742_301_0.png)

# Nested DO Loops

```sas
DO index-variable-1=start TO stop <BY increment>;
  DO index-variable-2=start TO stop <BY increment>;
    <additional SAS statements>
  END;
END;
```

```sas
data invest (drop=Quarter);
  Year=1 to 5;
  do Quarter=1 to 4;
    Capital=Capital+(Capital*(.045/4));
  end;
  output;
end;
run;
```

# 7.05 Short Answer Poll

How can you generate one observation for each quarterly amount?

```sas
data invest (drop=Quarter);
  do Year=1 to 5;
    Capital+5000;
    do Quarter=1 to 4;
      Capital+(Capital*(.045/4));
    end;
  output;
end;
run;

proc print data=invest noobs;
run;
```

# Business Scenario

Compare the final results of $5,000 a year for five years in three different banks that compound interest quarterly. Assume that each bank has a fixed interest rate, stored in the orion.banks data set.

Listing of orion.banks

| Name | Rate |
| :--- | :--- |
| Carolina Bank and Trust | 0.0318 |
| State Savings Bank | 0.0321 |
| National Savings and Trust | 0.0328 |

![](img/d3bde6e6ab06b1fc622215d982111742_302_0.png)

# Using Nested DO Loops with a SET Statement

```sas
data invest (drop=Quarter Year);
  set orion.banks;
  Capital=0;
  do Year=1 to 5;
    Capital+5000;
    do Quarter=1 to 4;
      Capital+Capital*(Rate/4);
    end;
  end;
```

There are three observations in orion.banks. Therefore, there are three iterations of the DATA step. Capital must be set to zero on each iteration of the DATA step.

# Execution: Nested DO Loops

```sas
data invest (drop=Quarter Year);
  set orion.banks;
  Capital=0;
  do Year=1 to 5;
    Capital+5000;
    do Quarter=1 to 4;
      Capital+Capital*(Rate/4);
    end;
  end;
```

| Name | Rate | N |
| :--- | :--- | :--- |
| Carolina Bank and Trust | 0.0318 | 1 |

# Execution: Nested DO Loops

```sas
data invest (drop=Quarter Year);
  set orion.banks;
  Capital=0;
  do Year=1 to 5;
    Capital+5000;
    do Quarter=1 to 4;
      Capital+(Capital*(Rate/4));
  end;
run;
```

| Name | Rate | N |
| :--- | :--- | :--- |
| State Savings Bank | 0.0321 | 2 |

# Execution: Nested DO Loops

```sas
data invest (drop=Quarter Year);
  set orion.banks;
  Capital=0;
  do Year=1 to 5;
    Capital+5000;
    do Quarter=1 to 4;
      Capital+(Capital*(Rate/4));
    end;
  end;
run;
```

| Name | Rate | N |
| :--- | :--- | :--- |
| National Savings and Trust | 0.0328 | 3 |

# Output: Nested DO Loops

```sas
proc print data=invest noobs;
run;
```

| Name | Rate | Capital |
| :--- | :--- | :--- |
| Carolina Bank and Trust | 0.0318 | 27519.69 |
| State Savings Bank | 0.0321 | 27544.79 |
| National Savings and Trust | 0.0328 | 27603.47 |

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the folder.

# Level 1

Performing Computations with DO Loops

The Payroll Department must project total employee costs (wages, retirement benefits, and medical benefits) through future years, based on assumed increases.

- Corporate income for last year is $50,000,000. Income is projected to increase at 1% per year.
- Modify the program p27 so that the DO loop stops when the year's total costs exceed the year's income.
- Print Year, Income, and Total_Cost and verify that total costs exceed income after 26 observations.

PROC PRINT Output

| Year | Income | Total_Cost |
| :--- | :--- | :--- |
| 1 | 2013 | 50,500,000.00 | 16,146,805.00 |
| 2 | 2014 | 51,005,000.00 | 17,058,159.57 |
| 3 | 2015 | 51,515,050.00 | 18,025,405.76 |
| 4 | 2016 | 52,030,200.50 | 19,052,105.42 |

# 7.2 Conditional DO Processing

| Year | Income | Total_Cost |
| :--- | :--- | :--- |
| 26 | 2038 | 64,762,815.75 | 67,973,189.29 |

The results above were generated on February 14, 2012. Your values for Year might differ.

# Level 2

# 3. Using an Iterative DO Statement with a Conditional Clause

Orion's income last year was $50,000,000 and expenses totaled $38,750,000. Income is projected to increase at 1% per year and expenses are expected to increase at 2% per year.

- a. Create a SAS data set named work.expenses that contains each's projected income and expenses.
- Use an iterative DO statement with a conditional clause.
- Stop the loop when expenses exceed income or after 30 years, whichever comes first.
- b. Print the results and format Income and Expenses with a dollar sign and two decimal places.

> Hint: Recall that an iterative DO statement with a conditional clause produces different results DO WHILE and DO UNTIL statements. The results below were generated using a DO UNTIL statement.

# PROC PRINT Output

| Obs | Income | Expenses | Year |
| :--- | :--- | :--- | :--- |
| 1 | $64,762,815.75 | $64,844,951.93 | 26 |

# Challenge

# 4. Using Other Loop Control Statements

- a. Use an iterative DO statement to calculate projected income and expenses for the next 75 years.
- Investigate SAS documentation for information about other loop statements such as CONTINUE and LEAVE.
- Include the appropriate loop control statement (CONTINUE/LEAVE) to stop the loop when expenses exceed income.
- b. Print the results and format the values of Income and Expenses with dollar signs and two decimal places.

> Hint: Recall that the DO WHILE and DO UNTIL statements might produce different results.

# PROC PRINT Output

| Obs | Income | Expenses | Year |
| :--- | :--- | :--- | :--- |
| 1 | $64,762,815.75 | $64,844,951.93 | 26 |

# 7.3 SAS Array Processing

# Objectives

- Explain the concepts of SAS arrays.
- Use SAS arrays to perform repetitive calculations.

# Array Processing

You can use arrays to simplify programs that do the following:

- perform repetitive calculations
- create many variables with the same attributes
- read data
- compare variables
- perform a table lookup

# 7.06 Short Answer Poll

Do you have experience with arrays in a programming language? If so, which languages?

# Business Scenario

The orion.employee_donations data set contains quarterly contribution data for each employee. Orion management is considering a 25% matching program. Calculate each employee's quarterly contribution, including the proposed company supplement.

Partial Listing of orion.employee_donations

| Employee | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
| :--- | :--- | :--- | :--- | :--- |
| 120265 | - | - | - | 25 |
| 120267 | 15 | 15 | 15 | 15 |
| 120269 | 20 | 20 | 20 | 20 |
| 120270 | 20 | 10 | 5 | - |
| 120271 | 20 | 20 | 20 | 20 |
| 120272 | 10 | 10 | 10 | 10 |
