
# Partial PROC PRINT Output (34 Total Observations)

Employees Earning at Least $60000

| Obs | Employee_ID | Gender | Salary | Birth_Date | Employee_Hire_Date | Employee_Term_Date | Marital_Status | Dependents |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 120101 | | 63040 | 18AUG1980 | 01JUL1970 | | S | |
| 2 | 120102 | | 108255 | 11AUG1973 | 01JUN1993 | | O | 2 |
| 3 | 120103 | | 87975 | 22JAN1953 | 01JAN1978 | | M | 1 |
| 99 | 120259 | | 433800 | 25JAN1968 | 01SEP1993 | | M | 1 |
| 100 | 120260 | F | 207885 | 02DEC1968 | 01NOV1988 | | M | 2 |

- b. Modify the previous solution to display employees who can earn at least $10000. Verify your results.

# PROC PRINT Output (9 Total Observations)

Employees Earning at Least $100000

| Obs | Employee_ID | Gender | Salary | Birth_Date | Employee_Hire_Date | Employee_Term_Date | Marital_Status | Dependents |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 120101 | | 63040 | 18AUG1980 | 01JUL1970 | | S | |
| 2 | 120102 | | 108255 | 11AUG1973 | 01JUN1993 | | O | 2 |
| 99 | 120259 | | 433800 | 25JAN1968 | 01SEP1993 | | M | 1 |
| 100 | 120260 | F | 207885 | 02DEC1968 | 01NOV1988 | | M | 2 |
| 101 | 120261 | | 243190 | 21FEB1973 | 01AUG1991 | | O | 1 |

# 11.4 Solutions

# Solutions to Exercises

- 1. Modifying an Inner Join

```
proc sql;
select d.Product_ID, Product_Name, Start_Date, End_Date, Discount
from orion.discount as d, orion.product_dim as p
where d.Product_ID=p.Product_ID and Discount >=6;
quit;
```

- 2. Coding proc SQL Inner Join

```
title 'Detail Information for Ordered Products and Quantities';
proc sql;
select Order_ID, o.Product_ID, Product_Name, Quantity
from orion.order_fact as o, orion.product_dim as p
where o.Product_ID=p.Product_ID;
quit;
title;
```

Alternate Solution

```
title 'Detail Information for Ordered Products and Quantities';
proc sql;
select Order_ID, o.Product_ID, Product_Name, Quantity
from orion.order_fact as o
INNER JOIN
orion.product_dim as p
on o.Product_ID=p.Product_ID;
quit;
title;
```

# 3. Comparing PROC SQL Inner Joins and Outer Joins

```
proc sql;
create table work.matches as
select EmployeeName, City, Order_Date
from orion.Order_fact as o
INNER JOIN
orion.Employee_addresses as a
on a.Employee_ID=o.Employee_ID
order by Order_Date;
quit;
```

title 'Matches from the Order and Address Tables';
proc print data=work.matches;
run;
title;

```
proc sql;
create table work.allorders as
select EmployeeName, City, Order_Date
from orion.Order_fact as o
LEFT JOIN
orion.Employee_addresses as a
on a.Employee_ID=o.Employee_ID
order by Order_Date;
quit;
```

title 'Order Dates, with Employee Information when Available';
proc print data=work.allorders;
run;
title;
```

# 4. Replacing a Hardcoded Value with a Macro Variable

```
%let location=DE;
title "Customers in &location";
proc print data=orion.customer;
var customer_id customer_name gender;
where country="&location";
run;
```

```
%let location=ZA;
title "Customers in &location";
proc print data=orion.customer;
var customer_id customer_name gender;
where country="&location";
run;
```

# 5. Creating and Using a Macro Variable

```
%let minSal=60000;
title "Employees Earning at Least $\&minSal";
proc print data=orion.employee_payroll;
where salary >= &minSal;
run;
```

let minSal=100000;
title "Employees Earning at Least $\&minSal";
proc print data=orion.employee_payroll;
where salary >= &minSal;
run;
```

# Solutions to Student Activities (Polls/Quizzes)

# 11.02 Short Answer Poll – Correct Answer

Modify the SELECT statement to display only the Employee_ID, Job_Title, and Salary columns.

```
libname orion "SAS-data-library";
proc sql;
select employee_id, job_title, salary
from orion.sales_mgmt;
quit;
```

| Employee ID | Employee Job Title | Annual Salary |
|---|---|---||
| 12143 | Senior Sales Manager | $95,090 |
| 12144 | Sales Manager | $83,505 |
| 12145 | Sales Manager | $84,290 |
| 12147 | Secretary II | $29,145 |

![](img/d3bdee6ab061fc62215d98211742_466.png)

# 11.03 Short Answer Poll – Correct Answer

No, the output contains more rows than expected.

```
/* SQL query to join two tables */
proc sql;
select sales_mgt.Employee_ID,
       Employee_Name,
       Job_Title;
from orion.sales_mgt,
     orion.employees_addresses;
NOTE: The execution of this query involves one or more Cartesian joins that cannot be optimized.
quit;
```

A Cartesian product was created. The result contains 1696 rows (42 * 44).

# 11.04 Short Answer Poll – Correct Answer

The orion.customer and country tables both have a column named Country. Add a WHERE clause to join the tables based on matching values of Country.

```
proc sql;
select Customer_ID, Customer_Name,
      Customer.Country, Country_Name
from orion.customer,
     orion.country
where customer.Country=country.Country;
quit;
```

# 11.05 Short Answer Poll – Correct Answer

Submit a PUT statement to display the values of automatic macro variables. What are the values of SYSVER and SYCP variables? Vary, but for many installations, the value of SYSVER is 9 and the value of SYCP is WIN.

# 11.06 Short Answer Poll – Correct Answer

Complete the rest of the table.

| Name | Value |
|---|---|
| year | 2007 |
| city | Dallas, TX |
| fname | Marie |
| name | Marie Hudson |
| total | 102 |

# 11.07 Short Answer Poll – Correct Answer

Examine the program below. What change(s) must be made to generate reports for 2008? Change the value assigned in %LET statement.

```
%let year=2008;
proc print data=orion.order_fact;
where order_date = &year;
title "Orders for &year";
run;
proc means data=orion.order_fact;
where order_date = &year;
class order_type;
var total_price;
title "Average Retail Prices for &year";
run;
by Order_Type;
```

# Chapter 12 Learning More

## 12.1 Introduction

### Objectives

- Identify the areas of support that SAS offers.
- Identify the next steps after the completion of this course.

### Customer Support

SAS provides a variety of resources to help customers.

![](img/d3bdee6ab061fc62215d98211742_472.png)

### Education

SAS Education provides comprehensive training, including:

- more than 200 course offerings
- world-class instructors
- multiple delivery methods
- worldwide training centers.

http://support.sas.com/training/

![](img/d3bdee6ab061fc62215d98211742_473.png)

### SAS Global Certification Program

SAS Education also provides

- globally recognized certifications
- preparation materials
- practice exams.

![](img/d3bdee6ab061fc62215d98211742_473.png)

http://support.sas.com/certify/

# Networking

Social media channels and user group organizations enable you to:

- interact with other SAS users and SAS staff
- learn new programming tips and tricks
- get exclusive discounts.

![](img/d3bdee6ab061fc62215d98211742_474.png)

For training-specific information:
http://support.sas.com/training/socialmedia

Icons are from top left to right, and then bottom left to right:
Twitter, RSS, Myspace, YouTube, Technorati, and SAS Community.

# SAS Books

SAS Books offers a complete selection of publications, including:

- eBooks
- CD-ROM
- hard-copy books
- books written by outside authors.

![](img/d3bdee6ab061fc62215d98211742_474.png)

http://support.sas.com/bookstore/
1-800-727-3228

# Beyond This Course

To grow your SAS skills, remember to activate the extended learning page for this course.

![](img/d3bdee6ab061fc62215d982111742_475.png)

Individual learning software is available.

# Next Steps

| To learn more about: | Enroll in this course: |
| --- | --- |
| How to use SQL to manipulate and merge data files | SAS SQL 1: Essentials |
| How to write SAS programs that are readable, dynamic, and easily maintained | SAS Macro Language 1: Essentials |
| DATA step programming techniques and comparing the efficiencies of different techniques | SAS Programming 3: Advanced Techniques and Efficiencies |
| Creating reports using the REPORT and TABULATE procedures, plus the Output Delivery System (ODS) | SAS Report Writing 1: Using Procedures and ODS |
| Performing statistical analysis using SAS/STAT software | Statistics 1: Introduction to ANOVA, Regression, and Logistic Regression |
| Preparing for the Base Certification Exam | SAS Certification Review: Base for SAS9 |
