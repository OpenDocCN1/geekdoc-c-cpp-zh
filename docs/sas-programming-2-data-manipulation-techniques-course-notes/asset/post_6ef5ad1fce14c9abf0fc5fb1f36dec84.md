
## 3.3 Solutions 3-41

```sas
title 'Customers Spending $100 or more in Retail Sales';
proc print data=work.discount1 noobs;
format TotSales dollar11.2;
run;
title;
```

## 7 Identifying Extreme Values in Each Group of Data

```sas
proc sort data=orion.customer_dim out=work.customers;
  by Customer_Type;
run;

data work.agecheck;
  set work.customers;
  by Customer_ID;
  retain oldest youngest o_ID y_ID;
  if first.Customer_Type=1 then do
    oldest=Customer BirthDate;
    youngest=Customer BirthDate;
    o_ID=Customer_ID;
    y_ID=Customer_ID;
  end;
  if Customer BirthDate < oldest then do
    o_ID=Customer_ID;
    oldest=Customer BirthDate;
  end;
  else if Customer BirthDate > youngest then do
    y_ID=Customer_ID;
    youngest=Customer BirthDate;
  end;
  if last.Customer_Type=1 then do
    age=(youngest-oldest)/365.25;
    output;
  end;
  keep Customer_Type oldest youngest o_ID y_ID ageange;
```

```sas
title 'Oldest and youngest Customers of each Customer Type';
proc print data=work.agecheck noobs;
format youngest date9. ageange 5.1;
ntitle;
```

### Alternate Solution

```sas
proc sort data=orion.customer_dim out=work.customers;
  by Customer_Type Customer_BirthDate;
run;

data work.agecheck;
  set work.customers;
  by Customer_Type;
  /* Could indent instead use: by Customer_Type Customer_BirthDate;
     In this DATA step, either BY statement works. */
  retain oldest youngest o_ID y_ID;
  if first.Customer_Type=1 then do
    o_ID=Customer_ID;
    oldest=Customer_BirthDate;
  end;
  /* Having sorted also on Customer_BirthDate, we know the first
     customer in each BY group will be the oldest (have the
     smallest SAS date value for a Birthday). */
  if last.Customer_Type=1 then do
    y_ID=Customer_ID;
    youngest=Customer_BirthDate;
    agerange=(youngest-oldest)/365.25;
    output;
  end;
  /* Similar story: last in each BY group will be the youngest. */
  keep Customer_Type oldest youngest o_ID y_ID agarange;
run;

title 'Oldest and Youngest Customers of each Customer Type';
proc print data=work.agecheck noobs;
format oldest youngest date9. agarange 5.1;
run;
title;
```

## Solutions to Student Activities (Polls/Quizzes)

### 3.01 Short Answer Poll – Correct Answer

Open and submit the program in p203a1. Does this create the correct values for MthDte?

```sas
data mnthDte;
  set orion.apales;
  MthDte=MthDte+SaleAmt;
run;
```

Partial orion.apales:

| SaleDate | Sale Amt | MthDte |
|---|---|---|
| 01APR2011 | 49.49 | 49.49 |
| 02APR2011 | 96.50 | 145.99 |
| 03APR2011 | 94.97 | 240.96 |
| 04APR2011 | 56.59 | 297.55 |

No, the program creates MthDte with missing values.

### 3.02 Multiple Choice Poll – Correct Answer

What effect did the missing value for SaleAmt have on MthDte?

- a. The missing value is ignored, MthDte values are not affected.
- b. The missing value causes the DATA step to stop.
- c. The missing value causes the subsequent values for MthDte to be set to missing.

### 3.03 Short Answer Poll – Correct Answer

What are the values for First.Dept and Last.Dept when the DATA step is processing the observation by the arrow?

| Dept | Salary |
|---|---|
| ADMIN | 20000 |
| ADMIN | 10000 |
| ADMIN | 50000 |
| ENGINR | 25000 |
| FINANC | 10000 |
| FINANC | 12000 |

First.Dept and Last.Dept are both 1. This happens when a group consists of a single observation.

### 3.04 Multiple Answer Poll – Correct Answer

What must happen in the DATA step to summarize data by groups? (Circle all that apply.)

- b. Set the accumulating variable to zero at the start of each BY group.
(Note: Choice a does not apply because sorting is done with PROC SORT, not in the DATA step.)

### 3.05 Short Answer Poll – Correct Answer

What are the values for First.Proj and Last. variables when the DATA step is processing the observation by the arrow?

| Proj | Dept | First.Proj |
|---|---|---|
| A | ADMIN | 0 |
| A | ADMIN | First.Dept 0 |
| A | ADMIN | |
| B | ADMIN | |
| B | ENGINR | Last.Proj 1 |
| B | ENGINR | |
| C | ENGINR | |
| C | SALES | Last.Dept 1 |
| C | SALES | |

## Chapter 4 Reading Raw Files

- 4.1 Reading Raw Data Files with Formatted Input............................................... 4-3
- Exercises ................................................................................................................ 4-17
- 4.2 Controlling when a Record Loads ............................................................ 4-20
- Exercises ................................................................................................................ 4-41
- 4.3 Solutions ....................................................................................... 4-45
- Solutions to Exercises ....................................................... 4-45
- Solutions to Student Activities.................................................................. 4-47

## 4.1 Reading Raw Data Files with Formatted Input

Objectives
- Read raw data in fixed columns using formatted input.

![](img/d3bdee6ab06b1fc622215d98211742_126_0.png)

### Business Scenario

Management wants to analyze discount offer data. The data currently resides in a raw data file and needs to be converted to a SAS data set.

| type | Offer_dt | Item_gp | Discount |
|---|---|---|
| 1040 | 02DEC2011 | Outdoors | 0.15 |
| 2020 | 07OCT2011 | Golf | 0.07 |
| 1030 | 22SEP2011 | Shoes | 0.10 |

## 4.01 Multiple Choice Poll

For your work, how often do you need to read raw data files?

- a. all the time
- b. occasionally
- c. very rarely
- d. never

### Idea Exchange

The INPUT statement describes the arrangement of values in the input data record and assigns input values to the corresponding SAS variables.

What are the four styles of input?

![](img/d3bdee6ab06b1fc622215d98211742_127_0.png)

## Input Styles

Column input, formatted input, list input, and named input are all styles of writing INPUT statement specifications.

| Style | Use for Reading |
|---|---|
| Column input | Standard data in fixed columns |
| Formatted input | Standard and nonstandard data in fixed columns |
| List input | Standard and nonstandard data separated by blanks or other delimiter |
| Named input | Standard data that is preceded by the name and an equal sign (=) |

### Standard and Nonstandard Data (Review)

Standard data is data that SAS can read without any instruction.

- Character data is always standard.
- Some numeric values are standard and some are not.

| Standard Numeric Data | Nonstandard Data |
|---|---|
| 58 | |
| 67.23 -23 | (23) $67.23 |
| 5.67E5 00.99 | 5,823 01/12/2010 |
| 1.2E-2 | 12May2009 |

The following are the only acceptable characters in a standard numeric field:

0 1 2 3 4 5 6 7 8 9 . E e D d +

Leading or trailing blanks are also acceptable.

E, e, and D represent exponential notation in a standard numeric field. An alternate way of writing 30000, example, is 3E5.

Examples of nonstandard character data include preserving leading blanks in character values, hexadecimal characters, and values surrounded by quotation marks.

## 4.02 Short Answer Poll

Which style of INPUT statement specification should you choose to read the offers.dat raw data file?

| Partial offers.dat | | | |
|---|---|---|---|
| 1 | 1 | 2 | 2 |
| 1---5----0----5 |
| 104012/02/11 Outdoors | 15% |
| 202010/07/11 Golf | 7% |
| 103009/22/11 Shoes | 10% |
| 103009/22/11 Clothes | 10% |

### Reading Data Using Formatted Input

This SAS program uses formatted input to read the raw data file in offers.dat.

```sas
data work.discounts;
  infile "&path\offers.dat";
  input @1 Cust type 4;
  @5 Offer dt mmddyy8;
  @14 Item gp $8;
  @22 Discount percent3;
run;
  INPUT pointer-control variable informat...;
```

- * starting position
* variable
* informat

| Statement | Description |
|---|---|
| DATA output-SAS-data-set; | The DATA statement begins a DATA step and provides the name of the SAS data set being created. 
output-SAS-data-set can refer to a temporary or permanent data set. |
