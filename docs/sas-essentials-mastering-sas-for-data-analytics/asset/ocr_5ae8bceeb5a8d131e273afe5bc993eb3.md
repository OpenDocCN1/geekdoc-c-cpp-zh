# 32 CHAPTER 2: GETTING DATA INTO SAS®

One way to tell if a variable in a SAS data set listing (PROC PRINT) is character or numeric is this: Character data are listed left justified in a cell and numeric data are listed right justified in a cell.

# 2.5.4 Reading Data Using Formatted Input

Another technique for reading data from specific columns is formatted input. This technique allows you to specify information about how SAS will interpret data as they are read into the program. SAS uses the inform to specify an input format specification that tells SAS how to read data (A FORMAT specification tells SAS how to output data into a report. This is discussed in the section “Using FORMATS for Output” in this chapter.) Using inform is helpful when you are reading data that might be in an otherwise hard-to-read format, such as date and dollar values. The syntax for formatted input is as follows:

```
DATA MYDATA;
INPUT @col variable1 format. @col variable2 format. ;
```

where @col is a pointer that tells SAS which column to start reading the information about a particular variable. Here is a specific example:

```
DATA MYDATA;
INPUT @1 SBP 3. @4 DBP 3. @7 GENDER $1. @8 WT 3. @12 OWE COMMA9;
```

In this example, note that the information for each variable contains three components. Thus, for the first variable, the information is the following:

# @1 SBP 3.

![](bbox=[0.188, 0.558, 0.812, 0.652])

+   1. **The pointer** (@ sign) tells SAS to read data for this variable beginning in the indicated column (in this case column 1).
2. **The variable name** (SBP) tells SAS that the name of this first variable is SBP.
3. **The inform** (3 .) tells SAS that data at this location in each row are numbers containing three digits and containing no decimal places.

Here is a brief description of how typical inform (input format) specifications are named:

| Inform Type | Syntax |
|---|---|
| Character | $FORMATNAME.w, |
| Numeric | FORMATNAMEw.d |
| Date and Time | FORMATNAME.w. |