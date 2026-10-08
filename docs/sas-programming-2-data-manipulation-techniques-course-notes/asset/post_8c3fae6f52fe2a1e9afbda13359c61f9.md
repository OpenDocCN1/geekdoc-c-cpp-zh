
# Using DO-END in a SELECT Group

Use DO and END statements to execute multiple statements when an expression is true.

```sas
data usa other;
  set orion.employee addresses;
  select (uppercase(country));
    when ('US') do;
      Benefits=1;
      output usa;
    end;
    when ('AU') do;
      Benefits=2;
      output australia;
    end;
    otherwise do;
      Benefits=0;
      output other;
    end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_53_0.png)

# Omitting the Select Expression

This version of the current example omits the SELECT expression.

```sas
data usa australia other;
  set orion.employee addresses;
  select;
    when (country='US') output usa;
    when (country='AU') output australia;
    otherwise output other;
  end;
```

```sas
SELECT;
  WHEN (expression-1)
    statement;
  ..<WHEN (expression-n)
    statement;
  <OVERWISE statement>
END;
```

See SAS documentation for more information about using SELECT groups.

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the data folder.

# 2.2 Writing to Multiple SAS Data Sets 2-27

## Level 1

## 4. Creating Multiple SAS Data Sets

The data set orion.employee_organization contains information about employee job titles, departments, and managers.

Partial orion.employee_organization (424 Total Observations)

| Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|--|
| 12101 | Director | Sales Management | 120261 |
| 120102 | Sales Manager | Sales Management | 120101 |
| 120103 | Sales Manager | Sales Management | 120101 |
| 120104 | Administration Manager | Administration | 120101 |
| 120105 | Secretary I | Administration | 120101 |

- a. Create a separate data set for each department.

Name the data sets work.admin, work.stock, and work.purchasing

Use conditional logic and explicit OUTPUT statements to write these data sets depending on whether the value of Department is Administration, Stock & Shipping, or Purchasing, respectively. Ignore all other Department values.

Hint: Be careful with capitalization and the spelling of the Department values.

- b. Print work.admin and verify your results. Add an appropriate title.

Partial work.admin (34 Total Observations)

| Obs | Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|---|--|
| 1 | 120104 | Administration Manager | Administration | 120101 |
| 2 | 120105 | Secretary I | Administration | 120101 |
| 3 | 120106 | Office Assistant II | Administration | 120104 |
| 4 | 120107 | Office Assistant III | Administration | 120104 |
| 5 | 120108 | Warehouse Assistant II | Administration | 120104 |

- c. Print work.stock and verify your results. Add an appropriate title.

Partial work.stock (26 Total Observations)

Stock and Shipping Employees

| Obs | Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|---|--|
| 1 | 120670 | Shipping Manager | Stock & Shipping | 120659 |
| 2 | 120671 | Shipping Agent III | Stock & Shipping | 120670 |
| 3 | 120672 | Shipping Manager | Stock & Shipping | 120659 |
| 4 | 120673 | Shipping Agent II | Stock & Shipping | 120672 |
| 5 | 120677 | Shipping Manager | Stock & Shipping | 120659 |

- d. Print work.purchasing and verify your results. Add an appropriate title.

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

2-28 Chapter 2 Controlling Input and Output

# Partial work.purchasing (18 Total Observations)

| Obs | Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|---|--|
| 1 | 120728 | Purchasing Agent II | Purchasing | 120735 |
| 2 | 120729 | Purchasing Agent I | Purchasing | 120735 |
| 3 | 120730 | Purchasing Agent I | Purchasing | 120735 |
| 4 | 120731 | Purchasing Agent II | Purchasing | 120735 |
| 5 | 120732 | Purchasing Agent III | Purchasing | 120736 |

## Level 2

- 5. Creating Multiple SAS Data Sets with Derived Values

The data set orion.orders contains information about in-store, catalog, and Internet orders as well as delivery dates.

Partial orion.orders (490 Total Observations)

| Order_ID | Type | Employee_ID | Customer_ID | Order_Date | Delivery_Date |
|---|---|---|---|---|---|
| 120058123 | 1 | 121039 | 63 | 11JAN2007 | 11JAN2007 |
| 120308011 | 2 | 999999 | 5 | 15JAN2007 | 15JAN2007 |
| 120306883 | 2 | 999999 | 45 | 20JAN2007 | 25JAN2007 |
| 120317441 | 1 | 120174 | 41 | 28JAN2007 | 28JAN2007 |
| 120315085 | 1 | 120134 | 183 | 27FEB2007 | 27FEB2007 |

- a. Orion wants to study catalog and Internet orders that were delivered quickly as well as those that went slowly.

- Create three data sets named work.fast, work.slow, and work.verslow.
- Write a WHERE statement to read only the observations with Order_Type equal 2 (catalog) or 3 (Internet).
- Create a variable ShipDays that is the number of days between when the order is placed and when the order is delivered.
- Handle the output:
- Output to work.fast when the value of ShipDays is less than 3.
- Output to work.slow when the value of ShipDays is 5 to 7.
- Output to work.verslow when the value of ShipDays is greater than 7.
- Do not output an observation when the value of ShipDays is 3 or 4.
- Drop the Employee_ID.
- There should be 80 observations in work.fast, 69 observations in work.slow, and 5 observations in work.verslow.

![](img/d3bde6e6ab06b1fc622215d982111742_55_0.png)

Of the 490 observations in orion.orders, only 230 are read due to the WHERE statement.

- b. Print your results from work.verslow with an appropriate title.

work.verslow

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

2-29 2.3 Selecting Variables and Observations

| Obs | Order_ID | Order_Type | Customer_ID | Order_Date | Delivery_Date | Ship Days |
|---|---|---|---|---|---|---|
| 1 | 123105521 | 2 | 16 | 27AUG2007 | 04SEP2007 | 8 |
| 2 | 123648375 | 2 | 70108 | 22JUL2009 | 02AUG2009 | 11 |
| 3 | 123965430 | 3 | 70165 | 08SEP2009 | 18SEP2009 | 10 |
| 4 | 1237165927 | 3 | 79 | 27SEP2009 | 08OCT2009 | 11 |
| 5 | 1241298131 | 2 | 2806 | 29JAN2011 | 08FEB2011 | 10 |

# Challenge

- 6. Using a SELECT Group

Write a solution to the previous exercise using SELECT logic instead of IF-THEN/ELSE logic. Refer to SAS documentation to explore the use of a compound expression in a SELECT statement. Print the data set work.veryslow.

# 2.3 Selecting Variables and Observations

## Objectives

- Control which variables are written to an output data set during a DATA step.
- Control which variables are read from an input data set during a DATA step.
- Control how many observations are processed from an input data set during a DATA or PROC step.

# Business Scenario

You have controlled the observations written to the three new data sets, and now you want to control the variables that are written to each.

orion.employee_addresses

![](img/d3bde6e6ab06b1fc622215d982111742_57_0.png)

# Controlling Variable Output (Review)

By default, SAS writes all variables from the input data set to every output data set.

orion.employee_addresses

![](img/d3bde6e6ab06b1fc622215d982111742_57_1.png)

# Controlling Variable Output (Review)

In the DATA step, the DROP and KEEP statements can be used to control which variables are written to output data sets. The statements can be used when reading from a SAS data set or from a raw data file.

```sas
data out1 out2;
set in;
drop x;

out1
Y Z
...
PDV
X Y Z

out2
Y Z
```
