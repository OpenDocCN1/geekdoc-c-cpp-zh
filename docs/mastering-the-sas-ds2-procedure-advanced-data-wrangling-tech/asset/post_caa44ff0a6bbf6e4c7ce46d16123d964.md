
# 48 Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

Basically, the behavior of null and missing values in DS2 SAS mode are just as we would expect to traditional Base SAS processing.

## 3.3.4.3 PROC DS2 ANSI Mode

You invoke PROC DS2 in ANSI mode by including the ANSIMODE option in the PROC DS2 statement. In ANSI mode, expressions resolving to an unknown value produce ANSI null values as an intermediate result. Any numeric missing values are immediately converted to ANSI null values, so DOUBLE variables never contain SAS missing values in ANSI mode.

Here are the other pertinent rules for missing and null values while operating DS2 in ANSI mode:

- Numeric missing values are automatically converted to null when read from a SAS data set.
- SAS character variables read from SAS data sets are actually stored with space characters filling the entire length of the variable. In ANSI mode, these variables appear to be character strings padded entirely with blanks instead of ANSI null values, and even the SAS MISS function will not evaluate them as missing.
- Numeric null values are automatically converted to missing when passed to a Base SAS function as a parameter value.
- In comparisons a character value to a single blank, the blank is interpreted as an ANSI space character, not as null.

Executing program Ch3_3_3.43.sas demonstrates the handling of SAS missing and ANSI null values in PROC DS2 operating in ANSI mode.

SAS Log:

```
*** From SAS Data Set ***
*** DS2 Char Values - ANSI Mode ***
C is not = ' '
missing(C) is not true.
null(C) is not true.

*** DS2 DOUBLE Values - ANSI Mode ***
N is not = ''
missing(N) is true.
null(N) is true.

*** ANSI Mode Using ANSI Var and Decimal Variables ***
*** DS2 VARCHAR Values***
Var is not = ' '
missing(Var) is true.
null(Var) is true.

*** DS2 DECIMAL Values***
Dec is not = ' '
missing(Dec) is true.
null(Dec) is true.
```

Note that the VARCHAR and DECIMAL null values evaluate exactly the same as they did in SAS mode, but the CHAR and DOUBLE values behave differently.

## Chapter 3: DS2 Data Program Details 49

The CHAR value read in from the SAS set evaluates as '=', but now for a different reason: in ANSI mode ' ' indicates ANSI space character, and the CHAR value is indeed full of spaces. Note that neither the MISSING and NULL functions return FALSE for the CHAR value, which is interpreted as ANSI space filled instead of missing.

In ANSI mode, DOUBLE functions work the same as any other ANSI numeric. It evaluates as '.' because missing values are immediately replaced with ANSI null values when read into the PDV. For the same reason, the NULL function returns TRUE when presented with the DOUBLE value. The SAS MISSING function returns TRUE, but this is because the null value was automatically converted to missing when passed to the Base SAS null function.

## 3.4 Review of Key Concepts

- "Six Subtle Dissimilarities"
    - All executable statements must be part of a method code block
    - DS2 programs do not overwrite data by default.
    - All variables not introduced via the SET statement must be declared.
    - PUT statement cursor line pointers are not supported.
    - Keywords are reserved words.
    - DS2 uses ANSI SQL quoting standards:
        - Single quotation marks delimit text constants.
        - Double quotation marks delimit identifiers.
    - Use %TSLSIT to resolve macro variable values in literal text.
- DS2 “Missing” Features
    - Many “missing” features are not missing—they are just accomplished differently in DS2:
        - There is no WHERE statement, but the SET statement accepts SQL query result that might contain a WHERE clause.
        - There is no UPDATE or MODIFY statement, but this behavior can be emulated with an SQL query in a SET statement.
- Traditional SAS DATA steps read raw data, control the SAS environment, or execute arbitrary system commands are not supported in DS2.
- DS2 natively processes a wide variety of ANSI data types. Because of this, automatic data type conversions happen frequently. Whenever a DOUBLE value is involved in a numeric expression, all other values will be converted to DOUBLE for processing, and some precision might be lost if BIGINT or DECIMAL values are involved.
- DS2 provides functions for explicit conversion between ANSI TIMESTAMP, DATE, and TIME and SAS DATETIME, DATE, and TIME values.
- SAS missing values and ANSI null values are fundamentally different ways of expressing unknown data. DS2 has two modes, SAS mode and ANSI mode, that allow you to select the default processing paradigm. ANSI null and SAS missing values can be successfully processed together in the same program as long as the conversion behaviors are understood.

## Chapter 4: User-Defined Methods and Packages

4.1 Introduction ............................................................................................................ 51

4.2 Diving into User-Defined Methods ........................................................................ 52

4.2.1 Overview ............................................................................................................ 52

4.2.2 Designing a User-defined Method......................................................................... 52

4.3 User-Defined Packages ....................................................................................... 57

4.3.1 General Considerations ................................................................................... 57

4.3.2 User-Defined Package Specifics ................................................................ 57

4.3.3 Object-Oriented Programming with DS2 Packages...................................... 61

4.4 Review of Key Concepts ............................................................................ 68

## 4.1 Introduction

In this chapter, we will explore user-defined methods to create custom, reusable blocks. First, we will define methods in inline, and then we'll learn how to share, reuse. Specifically, we will cover these points:

- defining user-defined methods
- defining inline
- setting parameters
- returning a value versus modifying one at the call site
- using packages
- methods in DS2 programs
- compile-time versus execution-time
- using constructor arguments
- using global and local variables
- using dot notation
- object-oriented programming

## 4.2 Diving into User-Defined Methods

### 4.2.1 Overview

User-defined methods are named code blocks in DS2 that execute only when called. Methods that produce values can be designed in one of two ways: the method can either perform like Base SAS function, returning a single value to the calling process, or it can perform like Base SAS routine, modifying one or more values at the call site.

### 4.2.2 Designing a User-defined Method

Methods are a great tool for standardizing processes in your code. Let's take a simple interest calculation as an example. Here is how a bank could calculate the accumulated interest after one year:

```sas
Amount=SUM(Amount, Amount*Rate);
```

To calculate the amount over several years, it's possible to execute the formula in a DO loop:

```sas
do i=1 to Years;
Amount=SUM(Amount, Amount*Rate);
end;
```

### 4.2.2.1 Method Design Considerations

To create a method to perform interest calculations, we must first decide how to pass the calculated interest value back to our calling process. Because there is only one value involved, we choose to return a value or modify one of the method's parameters at the call site by defining an IN_OUT parameter. Each method has pros and cons. A method that returns a value is the most flexible when called. When parameters are passed by value (there are no IN_OUT parameters), each parameter value can be performed at execution time with constant, a variable reference, or an expression. A method that modifies the values of its parameters at the call site must pass in the values of the IN_OUT parameters by reference. When called, all IN_OUT parameter values must be returned using variable names.

### 4.2.2.2 The Interest Method - V1.0

Let's make version 1.0 of our method using an IN_OUT parameter to provide the initial amount invested and to hold the resulting total after the interest has been compounded.

```sas
proc ds2;
title 'Results for each bank - initial $5,000 deposit';ndata;
dcl double Total having format dollar10.2;
dcl int Duration;
keep total duration bank rate;
quit;
```
