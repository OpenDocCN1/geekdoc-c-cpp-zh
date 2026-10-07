# 2. Change the macro call to

%GROUPS (5)

Resubmit and see that the call still works. As long as there is no ambiguity in the call, you do not have to include a specific assignment such as COUNT=5.

# 7.4.7 Using CALL SYMPUT to Create a Macro Variable

The SAS SYMPUT routine assigns a value to a macro variable within a DATA step. The call does not have to be within a macro routine, although it can be. The syntax of the call is as follows:

```
CALL SYMPUT('macrovariablename', value);
```

The macrovariablename is the name you want to assign a value (similar to how the $LET assigns a value). However, in this case, the value in the routine can be an expression, and the name itself can be created using SAS text operators. This is illustrated in the following example:

# HAND-ON EXAMPLE

This example illustrates how to use MACRO05.SAS.

+   1. Open the program file MACRO05.SAS. The data set CARS contains two variables CITYMG and HYPMG. This macro allows you to specify which version of MPG to use in a procedure (PROC MEANS in this case). Submit this code and observe the output. The DATA NULL statement is used to allow you to do procedures that must take place in a DATA step, but you do not want to save any data values to a SAS data set.

```
%MACRO CARINFO (WHICHPLACE);
DATA _NULL;
CALL SYMPUT('TIMEVAR', CATT(&WHICHPLACE.','MPG')));
RUN;
TITLE "THE VALUE OF THE MACRO VARIABLE TIMEVAR IS &TIMEVAR";nPROC MEANS MAXDEC=2 DATA=MYSASLIB.CARS;
VAR &TIMEVAR;
RUN;
%MEND CARINFO;
%CARINFO(WHICHPLACE=CITY);
```

(continued)