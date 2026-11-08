To use these option(s) place them in parentheses immediately following the name of the data set to which they are to be applied. While data set options can be used virtually anytime the data set is named, some of the options are situation dependent, which means that you will have to understand what an option does before applying it. For instance, options that control how a data set is to be read would not be used on a DATA statement.

In the following example the KEEP data set option is applied to the data set being used by PROC SORT.

```
```sas
proc sort data=advrpt.demog(keep= lname fname ssn)
          out=namesonly;
by lname fname;
run;
```
```

Regardless of how many variables are in ADVRPT.DEMOG the SORT procedure will only have to deal with the three variables named in the KEEP= option. For a SORT procedure this can substantially speed up the processing.

Data set options apply only to the data set to which they are associated. Here all the variables

```
```sas
data yr6_7;
  set year2006
      year2007(keep=subject visit labdt);
run;
```
```

```
```sas
data yr6_7;
  set year:(keep=subject visit labdt);
run;
```
```

from YEAR2006 will be included. Only the variables from YEAR2007 will be limited by the KEEP= data set option.

This is not the case when a data set list abbreviation is used. Only these three variables will be read from the incoming data sets (WORK.YEARxxxxxx). The

variable list applies to each incoming data set; consequently, an error is generated if a variable is not present on one or more of the incoming data sets.

For a number of the data set options, similar functionality can be obtained through the use of DATA step statements or through the use of system options. System options are the most general (they would apply to all data sets); DATA step statements will only apply to data sets within that DATA step, and data set options are the most specific as they apply only to a specific data set.

# MORE INFORMATION

Additional information on the use of data set options with PROC SORT can be found in Section 4.2. The INDSNAME= option, along with the IN= data set options, are discussed in Section 3.8.2.