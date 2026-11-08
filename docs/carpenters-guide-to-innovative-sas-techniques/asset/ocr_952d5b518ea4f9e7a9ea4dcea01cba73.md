+   ➐ The array index is calculated using the MOD function. This function is the key to rotating the values in and out of the stack. The newest value will always replace, and therefore remove, the oldest element in the stack. This is what makes this a FIFO stack.
+   
+   ➑ The value of POTASSIUM is loaded into the correct element in the stack.
+   
+   ➒ The average of the array elements (the values in the stack) is calculated.

Some coding alternatives can be found in example program E3_1_7b.sas.

# MORE INFORMATION

A multi-label format is used to calculate moving averages without building a stack in Section 12.3.2.

# 3.1.8  A Bit on the SUM Statement

As we have seen in the other subsections of Section 3.1, in the DATA step it is necessary to take deliberate steps if we intend to work across observations.

```
```sas
data totage;
    set sashelp.class;
    retain totage 0; ①
    totage = totage+age; ②
    run;
```
```

In this DATA step we want to keep an accumulator on AGE. ① The variable must first be retained and initialized to 0. ② Then for each observation the AGE is added to the total (TOTAGE).

The coding can be simplified by using the SUM statement. Since the SUM statement has an implied RETAIN statement and automatically initializes to 0, the RETAIN statement is not needed.

```
```sas
data totallage;
    set sashelp.class;
    totage+age; ③
    run;
```
```

Some programmers assume these two methods of accumulation are equivalent; however, that is not the case, and the difference is non-trivial. Effectively the SUM statement calls the SUM function, which ignores missing values. If AGE is missing, the accumulated total value for either ③ or ④ will not be affected; however, the total at ② will be set to missing and will be unable to do further accumulations.

```
```sas
data totage;
    set sashelp.class;
    retain totage 0;
    totage = sum(totage, age); ④
    run;
```
```

# MORE INFORMATION

The sasCommunity tip http://www.sascommunity.org/wiki/Tips:SUM_Statement_and_the_Implied_SUM_Function mentions the use of the implied SUM function.

# 3.2  Calculating a Person’s Age

The calculation of an individual’s age can be problematic. Dates are generally measured in terms of days (or seconds if a datetime value is used), so we have to convert the days to years. To some extent, how we calculate age will depend on how we intend to use the value. The society’s concept of age is different than the mathematical concept. Age in years is further complicated by the very definition of a year as one rotation of the earth around the sun. This period does not convert to an integer number of days, and it is therefore further complicated by leap years. Since