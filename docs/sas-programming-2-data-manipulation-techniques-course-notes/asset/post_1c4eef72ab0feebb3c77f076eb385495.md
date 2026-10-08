
# 10.2 Solutions 10-23

3) Add another PROC FORMAT step with the CNTLIN= option to read the continentfmt data set and re-create the CONTINENT format. Use the FMTLIB option in this PROC FORMAT step to ensure that the new values are added to the CONTINENT format.

```
proc format library=orion.MyFmts cntlin=continentfmt
  fmtlib;
  select continent;
```

# 2. Creating Formats with Inclusive Ranges from SAS Data Set

a. Create a format from the orion.ages data set and store it permanently in the orion.MyFmts catalog. Use the appropriate option to view the values in the format.

```
data ages
  set orion.ages (rename=(First_Age=Start Last_Age=End
                               Description=Label));
  retain FmtName 'ages';

proc format library=orion.MyFmts fmtlib cntlin=ages;
  select ages;
```

b. Write a DATA step to create a data set sales that reads the Employee_ID and Birth_Date variables from the orion.sales data set. Create a new variable named Age that is the employee's age as the current date, and another new variable named Age_Cat that is the value of the variable Age using the AGE format.

```
data sales
  set orion.sales (keep=Employee_ID Birth_Date);
  Age_int=yrdiff(Birth_Date, today(), 'AGE');
  Age_Cat=put(Age, ages).
```

c. Print the first five observations of the sales data set to confirm that the new variables were created correctly.

```
proc print data=sales(obs=5);
  format Birth_Date date9.
  title 'Sales Data Set';
```

# 3. Creating Formats with Exclusive Ranges from a SAS Data Set

a. Create a named format ages_mod from the orion.ages_mod data set and store it permanently in the orion.MyFmts catalog. Use the appropriate option to view the values in the format.

```
data ages_mod;
set orion.ages_mod(rename=(First_Age=Start Last_Age=End
Description=Label));
retain fmtname 'ages_mod';
EEXCL='Y';
run;

proc format library=orion.MyFmts fmtlib cntlinn=ages_mod;
select ages_mod;
run;
```

b. Write a DATA step to create a data set sales that reads the Employee_ID and Birth_Date variables from the orion.sales data set. Create a new variable named Age that is the employee's age as the current date, and another new variable named Age_Cat that is the value of the variable Age using the AGES_MOD format.

```
options fmtsearch=(orion.MyFmts);
data sales:
  set orion.sales(keep=Employee_ID Birth_Date);
  Age=int(yrdif(Birth_Date, today(), 'AGE'));
  Age_Cat=put(Age, ages_mod.);
run;
```

c. Print the first five observations of the sales data set to confirm that the new variables were created correctly.

```
proc print data=sales(obs=5);
  format birth date date9;
title 'Sales Data Set'
run;
```

# Solutions to Student Activities (Polls/Quizzes)

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

1004 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

# 10-24 Chapter 10 Creating and Maintaining Permanent Formats

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

# 10-24 Chapter 10 Creating and Maintaining Permanent Formats

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

# 10-24 Chapter 10 Creating and Maintaining Permanent Formats

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

# 10-24 Chapter 10 Creating and Maintaining Permanent Formats

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

[content]
# 10.2 Solutions 10-23

3) Add another PROC FORMAT step with the CNTLIN= option to read the continentfmt data set and re-create the CONTINENT format. Use the FMTLIB option in this PROC FORMAT step to ensure that the new values are added to the CONTINENT format.

```
proc format library=orion.MyFmts cntlin=continentfmt
  fmtlib;
  select continent;
```

# 2. Creating Formats with Inclusive Ranges from SAS Data Set

a. Create a format from the orion.ages data set and store it permanently in the orion.MyFmts catalog. Use the appropriate option to view the values in the format.

```
data ages
  set orion.ages (rename=(First_Age=Start Last_Age=End
                               Description=Label));
  retain FmtName 'ages';

proc format library=orion.MyFmts fmtlib cntlin=ages;
  select ages;
```

b. Write a DATA step to create a data set sales that reads the Employee_ID and Birth_Date variables from the orion.sales data set. Create a new variable named Age that is the employee's age as the current date, and another new variable named Age_Cat that is the value of the variable Age using the AGE format.

```
data sales
  set orion.sales (keep=Employee_ID Birth_Date);
  Age_int=yrdiff(Birth_Date, today(), 'AGE');
  Age_Cat=put(Age, ages).
```

c. Print the first five observations of the sales data set to confirm that the new variables were created correctly.

```
proc print data=sales(obs=5);
  format Birth_Date date9.
  title 'Sales Data Set';
```

# 3. Creating Formats with Exclusive Ranges from a SAS Data Set

a. Create a named format ages_mod from the orion.ages_mod data set and store it permanently in the orion.MyFmts catalog. Use the appropriate option to view the values in the format.

```
data ages_mod;
set orion.ages_mod(rename=(First_Age=Start Last_Age=End
Description=Label));
retain fmtname 'ages_mod';
EEXCL='Y';
run;

proc format library=orion.MyFmts fmtlib cntlinn=ages_mod;
select ages_mod;
run;
```

b. Write a DATA step to create a data set sales that reads the Employee_ID and Birth_Date variables from the orion.sales data set. Create a new variable named Age that is the employee's age as the current date, and another new variable named Age_Cat that is the value of the variable Age using the AGES_MOD format.

```
options fmtsearch=(orion.MyFmts);
data sales:
  set orion.sales(keep=Employee_ID Birth_Date);
  Age=int(yrdif(Birth_Date, today(), 'AGE'));
  Age_Cat=put(Age, ages_mod.);
run;
```

c. Print the first five observations of the sales data set to confirm that the new variables were created correctly.

```
proc print data=sales(obs=5);
  format birth date date9;
title 'Sales Data Set'
run;
```

# Solutions to Student Activities (Polls/Quizzes)

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

# 10-24 Chapter 10 Creating and Maintaining Permanent Formats

# 10.01 Multiple Choice Poll – Correct Answer

Which program should be more efficient?

+   a. Program 1
b. Program 2
c. They should be equally efficient.

+   - The RETAIN statement assigns an initial value at compilation time.
- The RENAME= option renames the variables in the new data set at compilation time.

# Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step.

To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

# 10.02 Short Answer Poll – Correct Answer

Submit the program p210a01.
What error messages do you see in the SAS log?

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

# 10.03 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtlib;
```

# 10.04 Short Answer – Correct Answer

Replace the current statement with the following and resubmit p210a01. What is the result?

```
options fmtsearch=(orion.MyFmts);
```

