
# Chapter 2: Introduction to the DS2 Language 13

System methods execute automatically and do not accept parameters. You must explicitly define at least one of these methods in your data or thread program or the program will not execute. You do not write explicit code for one or more system method blocks, the DS2 compiler will create an empty version of the missing system method for you at compile time. An empty method contains only the appropriate METHOD statement by an END statement.

## 2.2.5.1 The INIT Method

The INIT method executes once and only once, immediately upon commencement of program execution. It provides a standard place to execute program initialization routines. The following DATA step and DS2 data programs produce the same results, but the DS2 data program does not require any conditional logic:

DATA step:

```
data _null;
if _n=1 then do;
put 'Execution is beginning';
end;
```

DS2 data program:

```
proc ds2;
data _null;
method init();
put 'Execution is beginning';
end;
endata;
run;
quit;
```

## 2.2.5.2 The RUN Method

The RUN method emulates the performance of a traditional SAS DATA step. It begins operation as soon as the INIT method has completed execution and acts as a data-driven loop. The RUN method iterates once for every row (observation) in the input data set. The RUN method is the only method that includes an implicit output at the END statement. The DATA step and DS2 data program produce the results:

```
data new_data;
if _n=1 then do;
put 'Execution is beginning';
end;
set crs.one_day;
run;
```

```
proc ds2;
data new_data;
method init();
put 'Execution is beginning';
end;
method run();
set crs.one_day;
end;
enddata;
run;
quit;
```

## 2.2.5.3 The TERM Method

The TERM method executes once, and only once, immediately after the RUN method completes execution and before the data or thread program terminates execution. It provides an appropriate place to execute program finalization code. This DATA step and DS2 data program would produce the same results, but the DATA step requires the use of the END= statement option, the associated automatic variable, and a conditional logic decision to accomplish the DS2 data program without requiring any additional resources or code:

```
data new_data;
if _n=1 then do
  put 'Execution is beginning';
end;
set crs.one_day end=last;
if last=1 then do
  put 'Execution is ending';
end;
```

```
proc ds2;
data null;
method init();
  put 'Execution is beginning';
end;
method run();
  set crs.one_day;
end;
method term();
  put 'Execution is ending';
end;
enddata;
run;
quit;
```

## 2.2.6 User-Defined Methods

In DS2, you can easily define and use your own reusable code blocks. These code blocks are called user-defined methods, and they can accept parameter values either by reference or by value. When all parameters are passed into a method by value, the values are available inside the method for use in calculations, and the method can return a single value to the calling process—like a Base SAS function. This data program uses a user-defined method to convert temperatures from Celsius to Fahrenheit.

```
proc ds2;
/* No output DATA set. Results returned as a report (like SQL) */
data;
  dcl double DegC DegF;
  /* Method returns a value */
method c2f(double Tc) returns double;
/* Celsius to Fahrenheit */
return ((Tc*9)/5+32);
end;
method init();
  do DegC=0 to 30 by 15;
  DegF=c2f(DegC);
  output;
end;
enddata;
run;
quit;
```

Figure 2.2: Output of Temperature Conversion

| DegC | DegF |
|---|---|
| 0 | 32 |
| 15 | 59 |
| 30 | 86 |

One or more parameters are passed by reference, the values are available inside the method for use in calculations, and those values can be modified by the method at the call site, like a Base SAS call routine. In DS2, parameters passed by reference are called IN_OUT parameters. A method that has IN_OUT parameters cannot return a value, but can modify several of its IN_OUT parameters during execution.

This data program uses a user-defined method to convert temperatures from Fahrenheit to Celsius, but passes the temperature parameter by reference:

```
proc ds2;
data;
  dcl double Tc;
  /* Method modifies a value at the call site */
method f2c(in_out double T);
  /* Fahrenheit to Celsius (Rounded) */
  T=round((T-32)*5/9);
end;
method init();
  do Tf0=0 to 212 by 100;
    Tc=Tf;
    f2c(Tc);
    output;
  end;
end;
enddata;
run;
quit;
```

# 14 Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

Figure 2.3: Output of Temperature Conversion

| Tf | Tc |
|---|---|
| 0 | -18 |
| 100 | 38 |
| 200 | 93 |

When calling this type of method, you must supply a variable name for IN_OUT parameters; otherwise, it will result in this message in the SAS log:

```
ERROR: Compilation error.
ERROR: In call of f2c: argument must be modifiable.
```
(Note: The OCR text for the table and log above was reconstructed based on the fragmented context.)

# Chapter 2: Introduction to the DS2 Language 15

## 2.2.7 Variable Identifiers and Scope

In DS2, all objects, variables, and code blocks must have identifiers (names). Within the DS2 program, an identifier's scope is either global or local, Figure 2.4 shows a DS2 program with both global and local scope.

```
proc ds2;
data null;
dcl varchar(6) var1 var2;
retain var2='Global
method init();
dcl varchar(5) var1;
put var1='Local';
put var2=Global;
end;
method run();
put var1=Global;
put var2=Global;
end;
method term();
put var1=Global;
put var2=Global;
end;
endata;
run;
quit;
```

Figure 2.4: DS2 Program Variable Scope

![Figure 2.4](img/ef05c3db88dda150abd07414dd206df_33_0.png)
Legend:
- Global Scope
- Local Scope

If the program illustrated in Figure 2.4 is executed, the following results are produced in the SAS log:

INIT method var1=Local
INIT var2=Global
RUN var1=Global
RUN var2=Global
TERM var1=Global
TERM var2=Global

Variable identifiers are also in scope if the variable is undeclared or introduced to the program via a statement. In DS2, an undeclared variable is created whenever a variable is first referenced in a program statement other than a SET or DECLARE statement, such as an assignment statement. The use of undeclared variables in DS2 is discouraged; doing so will produce warnings in the log. Although this might at first seem strange to a SAS data programmer, if you ever executed a long-running SAS program only to be greeted by the dreaded NOTE: Variable var is uninitialized in the SAS log, you will understand the benefit. Generally, that means you've misspelled a variable name somewhere in your code, and the processing time for that run of the step has been wasted.

You can control DS2 behavior for undeclared variables with the system option DS2COND or SCOND=option in the PROC DS2 statement. The default is WARNING, but NONE, NOTE, and ERROR are all valid values. When writing, prototyping, or coding, I prefer to have this option to ERROR, so that DS2 programs containing undeclared variables will fail to compile, will not execute, and will produce this message in the SAS log:

```
ERROR: Compilation error.
ERROR: Line nn: No DECLARE for referenced variable var; creating as a global variable of type double.
```
