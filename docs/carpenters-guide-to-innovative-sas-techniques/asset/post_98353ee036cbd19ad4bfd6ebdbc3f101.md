
| Operator | IF Statement Mnemonic | WHERE Statement Caveat for the Mnemonic | IF and WHERE Clause | Results |
|---|---|---|---|---|
| MIN | >< | Mnemonic is not supported in WHERE, although MIN is converted to >< in the LOG | where x=(y<>z);<br>if x=(y<>z); | WHERE → error<br>IF works as expected |
| MAX | <> | Mnemonic is interpreted as not equal in the WHERE | where x=(y<>z); | True when X=1 and Y not equal to Z or when X=0 and Y=Z |

## Potential Problem #2 – Negative Values

When the negative sign is used with the first value associated with these operators, the expressions are not interpreted the same in the WHERE and IF statements.

| Expression | Result |
|---|---|
| if -2 = (-5 min 2); | True – the minus sign is applied after the MIN operator, essentially the same as: if -2 = (-5 min 2); |
| where -2 = (-5 min 2); | False – the minus sign is applied before the MIN operator, comparison is the same as: where -2 = -5; |

## 2.2.6 Numeric Expressions and Boolean Transformations

It is sometimes necessary to transform numeric values to Boolean (0 or 1) values. There is no one function that does this, and indeed the exact transformation may be too situational for a specific function.

### True / False

Partly because of the way that SAS handles TRUE/FALSE, i.e., false is 0 or missing and all else is true, the missing values must also map to 0. The double negation (NOT) is used to perform the transformation:

```sas
x = ^^dob;
```

Since negation is a Boolean operator, it converts the original value to either a zero or a one.

### MORE INFORMATION

Double negation is used to convert a number to a binary 0/1 operator in an example in Section 12.6.2.

### Replace Missing with 0

For reporting purposes missing values can be replaced by a 0 using a simple assignment statement:

```sas
z = coalesce(dob,0);
```

The COALESCE function returns the first non-missing value. In this example if DOB is missing a 0 is returned. Prior to the inclusion of the COALESCE function, this same operation was sometimes accomplished using the SUM function.

```sas
y = sum(dob,0);
```

Be careful when working with dates as was done here. Remember that, although both are false, a date of missing and a date of 0 have different meanings.

These two expressions do not result in a Boolean value. If you want to convert all missing values to 0 and all other values to 1 (including 0) you can use the negation of the MISSING function:

```sas
mval=^missing(val);
```

In this expression MVAL will be 1 for all numbers except missing.

### Determine Positive or Negative Values

Because of missing values and the 0 value, we have four distinct possibilities when separating positive and negative values. The groups of positive and non-negative values are not necessarily the same. Fortunately we can build the Boolean flag for each of these four possibilities, with the use of the SIGN function, which returns -1 for values < 0, 0 for values=0, 1 for values>0, and missing for missing values.

```sas
data posneg;
  do v=-2 to 2;
    * if positive;
    pos = sign(v)=1;
    * Not positive;
    notpos = (sign(v) in(-1,0));
    * Negative;
    neg = ^sign(v)=-1;
    * Not negative;
    notneg = sign(v) in (0,1);
    output posneg;
  end;
run;
```

### 2.2.6 Boolean Conversions Positive or Negative?

| Obs | v | pos | notpos | neg | notneg |
| --- | --- | --- | --- | --- | --- |
| 1 | . | 0 | 0 | 0 | 0 |
| 2 | -2 | 0 | 1 | 0 | 0 |
| 3 | -1 | 0 | 1 | 0 | 0 |
| 4 | 0 | 0 | 1 | 1 | 1 |
| 5 | 1 | 1 | 0 | 1 | 1 |
| 6 | 2 | 1 | 0 | 1 | 1 |

### SEE ALSO

Several of the code examples in this section have been suggested by Howard Schreier in the sasCommunity.org article: [http://www.sascommunity.org/wiki/Numeric_transformations](http://www.sascommunity.org/wiki/Numeric_transformations).

## 2.3 Data Validation and Exception Reporting

Although we sometimes have the opportunity to work with data that has already been scrubbed clean, often a major portion of our work is the preparation and cleaning of the data. This is especially true for data that has been hand entered or for data that comes from a source without your high standards of excellence. In the biotech/pharmaceutical industries a great deal of time and careful attention to detail is spent on the validation of the data.

For large or complex data sets the manual/visual process of finding data errors is just not practical. We need some tools that will allow us to automate the validation process.

When reporting on errors in your data, you will need to be able to communicate the specific problem and precisely where it occurs. Generally this means that you will have to identify the specific row and column (observation and variable). To identify a particular row you need to know the values of all the variables that form the data set's primary key (the BY variables that identify the data down to the row level).

### SEE ALSO

Wright (2006), and the related papers by Nelson (2004a, 2004b), discusses an approach to the validation of SAS programs. Bahler (2001) provides a summary of a variety of data cleaning techniques. Ron Cody (2008b) has written an entire book on data cleaning techniques.

### 2.3.1 Date Validation

Since we will work with dates, we need to know how to detect and work with incomplete or inappropriate date values. There are several issues that we need to understand.

### Using Formats to Check Date Strings

Formats, whether they are user defined or provided by SAS, can be powerful tools when searching the data for values that are inappropriate, incomplete, missing, or out of range.

Dates can be particularly problematic for some types of data, such as survey response data. Often the dates are collected as character strings and then checked before conversion to a SAS date.

```sas
data visitdates;
   visit=1; v_date_ = '05/25/2004'; output;
   visit=2; v_date_ = '06/XX/2004'; output;
run;

proc print data=visitdates;
   where input(v_date_,mmddyy10.) = .;
run;
```

Collecting them as character strings is important so that we can record partial dates. In the second observation shown to the left, the date might be from the response: “My second visit was in June of 2004. I do not remember the exact day.”

### 2.3.1 Date Validation Using Formats

Date Errors

| Obs | visit | v_date |
|---|---|---|
| 2 | 2 | 06/XX/2004 |

The INPUT function in the WHERE statement attempts to convert the character string into a date. Invalid values will result in a missing value, which is selected by the WHERE.

```text
9    proc print data=visitdates;
10      where input(v_date_,mmddyy10.) eq .;
11   run;

ERROR: INPUT function reported 'ERROR: Invalid date value'
while processing WHERE clause.
```

When the INPUT function is used with the format MMDDYY, for an incorrectly structured value, as it is in the second observation, an error is issued in the LOG. This error message can be suppressed by using either the ?? format modifier (see Section 1.3.1) or the NOFMTERR system option.

The ?? format modifier suppresses format error messages and can be used with the INFORMAT in the INPUT function, and is more specific than the NOFMTERR system option as it can be applied to a specific informat. The subsetting IF statement in this step replaces the WHERE statement in the previous example, as the ?? informat modifier cannot be used in the WHERE statement.

```sas
data dateerrors;
   set visitdates;
   if input(v_date_,?? mmddyy10.) eq .;
run;
proc print data=dateerrors;
run;
```

Because we can suppress the error messages, we have more latitude in the use of formats to rebuild dates with missing components. As before, let’s assume that our incoming dates are received as character strings with either the day or month potentially coded as ‘XX’. This example shows the subject’s response to the question: “When did you stop smoking?” Very typically the patient is unable to remember the date let alone the day of the month. In this example we have decided to replace missing days with the 15th and if the month is missing with the year midpoint July 1. This code assumes that at least the year is present.
