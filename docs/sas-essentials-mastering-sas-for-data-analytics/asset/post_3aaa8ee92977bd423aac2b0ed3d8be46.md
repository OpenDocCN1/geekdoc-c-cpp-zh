
it is ready to be called when the code sees the %DISCLAIM statement at the end of
the program.
2. Submit the code and observe the output given in Table 7.11. It contains the disclaimer
from the macro routine. This illustrates that you can keep certain macros in files,
include them in any program you want to use them in, and call them at locations in
your program where you want the macro to run.

| TABLE 7.11 Output Syncing GSLIDE Results |
| The MEANS Procedure |
| Analysis Variable : AGE |
| GENDER | N | Obs | N | Mean | Std Dev | Minimum | Maximum |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| FEMALE | 9 | 9 | 40.8888889 | 14.2954927 | 24.0000000 | 72.0000000 |
| M | 9 | 9 | 38.7777777 | 15.1226467 | 18.0000000 | 64.0000000 |

Data provided by ACME Company may be delayed as
specified by financial exchanges or our data providers.
@ACME does not verify any data and declares any obligation-
to do so.

## 7.4.6 Using The SAS Macro %DO Loop

The SAS %DO loop statement is similar to the previously discussed DO loop, but in this
macro version (note the percentage sign before the DO), you are able to define increment
macro variables that take on dynamic values. The %DO loop statement must appear inside
a SAS macro routine, but unlike the standard DO loop, it does not have to appear within a
DATA step. A simplified syntax is as follows:
%DO macrovariable=start %TO stop %BY increment;
SAS statements
%END;

Note that one of the big differences in this %DO loop is the variable being incremented,
called macrovariable here. That, this is like a macro variable created in a %LET
statement, but you have the ability to make it increment over a selected range in the loop.
For example, the following %DO loop iterates from the variable I (which we refer to as &I,
macro variable) to 5 and assigns the name of a DATA file based on the value of &I.

```
%do i=1 to 5;
data gppi;
set mysaslib.somedata;
where status=&i;
run;
%end;
```

The code GPPI resolves to the data set names GP1, GP2, GP3, and so on within the
loop as I increments from 1 to 5.

## HANDS-ON EXAMPLE

This example illustrates how to use a %DO loop in a SAS macro.

- 1. Open the program file DMACRO4.SAS. This routine contains a macro named GROUPS that creates data sets from the SOMEDATA set based on the value of the variable STATUS. Submit this code and examine the log. Verify that five data sets GP1, GP2, GP3, GP4, and GP5 were created.

```
%MACRO GROUPS (COUNT);
%DO I=1 TO &COUNT;
DATA GP&\I;
SET SASHLIB.SOMEDATA;
WHERE STATUS=\&I;
END;
%MEND;
GUPS(COUNT=5);
TITLE "LISTING FOR STATUS=1";
PROC PRINT DATA=GP1;RUN;
TITLE "LISTING FOR STATUS=2";
PROC PRINT DATA=GP2;RUN;
```

Note that the call to the macro program %GROUPS(COUNT=5) sends the macro variable COUNT the value 5, which was used in the %DO loop at the &TO value. The data sets are created by concatenating GP with the increment &I and they are GP1, GP2, and so on. The PROC PRINT statements list the contents of the first two data sets created. Submit this code and observe the results in Table 7.12.

## TABLE 7.12 Output Showing Results of %DO Loop

| Obs | ID | GP | AGE | TIME1 | TIME2 | TIME3 | TIME4 | STATUS | SEX | GENDER |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 343 | B | 11 | 19.0 | 25.2 | 27.7 | 25.1 | | 1 | Male |
| 2 | 410 | B | 13 | 22.2 | 30.4 | 32.1 | 35.2 | | 0 | Female |
| 3 | 307 | C | 11 | 22.6 | 30.1 | 34.4 | 35.2 | 1 | Female |

## Listing for STATUS=1

| Obs | ID | GP | AGE | TIME1 | TIME2 | TIME3 | TIME4 | STATUS | SEX | GENDER |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 187 | A | 11 | 22.5 | 29.3 | 32.6 | 33.7 | | 2 | Female |
| 2 | 162 | B | 7 | 20.9 | 28.9 | 29.7 | 25.9 | | 2 | Male |
| 3 | 198 | B | 12 | 23.4 | 29.2 | 30.4 | 35.1 | | 2 | Female |
| 4 | 282 | B | 13 | 21.3 | 28.7 | 32.3 | 30.3 | | 2 | Female |
| 5 | 575 | B | 8 | 21.2 | 25.7 | 28.9 | 31.6 | | 2 | Female |
| 6 | 589 | B | 7 | 22.0 | 25.5 | 28.2 | 30.9 | | 2 | Female |
| 7 | 593 | B | 11 | 18.9 | 23.1 | 27.7 | 25.6 | | 2 | Male |

## 2. Change the macro call to

%GROUPS (5)

Resubmit and see that the call still works. As long as there is no ambiguity in the call, you do not have to include a specific assignment such as COUNT=5.

## 7.4.7 Using CALL SYMPUT to Create a Macro Variable

The SAS SYMPUT routine assigns a value to a macro variable within a DATA step. The call does not have to be within a macro routine, although it can be. The syntax of the call is as follows:

```
CALL SYMPUT('macrovariablename', value);
```

The macrovariablename is the name you want to assign a value (similar to how the $LET assigns a value). However, in this case, the value in the routine can be an expression, and the name itself can be created using SAS text operators. This is illustrated in the following example:

## HAND-ON EXAMPLE

This example illustrates how to use MACRO05.SAS.

- 1. Open the program file MACRO05.SAS. The data set CARS contains two variables CITYMG and HYPMG. This macro allows you to specify which version of MPG to use in a procedure. Submit this code and examine the log. Verify that five data sets GP1, GP2, GP3, GP4, and GP5 were created.

```
%MACRO GROUPS (COUNT);
%DO I=1 TO &COUNT;
DATA GP&\I;
SET SASHLIB.SOMEDATA;
WHERE STATUS=\&I;
END;
%MEND;
GUPS(COUNT=5);
TITLE "LISTING FOR STATUS=1";
PROC PRINT DATA=GP1;RUN;
TITLE "LISTING FOR STATUS=2";
PROC PRINT DATA=GP2;RUN;
```
(Note: The OCR text seems to have repetitions/disruptions in the later pages, I have cleaned them based on the logical flow provided in the source.)
