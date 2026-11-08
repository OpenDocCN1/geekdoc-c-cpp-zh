It is likely that you will have a number of functions stored in several data sets. To make all of these functions available each of the data sets must be listed on the CMPLIB= system option.

Here two data sets are listed. All the functions in all the packets in both of these data sets will be available for use. The exception will be for multiple functions with the same name. Unlike most library searches, the search order across multiple function libraries is from right to left. In the example shown here functions in WORK.MYFUNCNS will be found first. The packet is not named in the CMPLIB option; consequently, if the same function name is used in two different packets within the same data set, it will be harder to anticipate which will be used. I would recommend that function names be unique within data set.

```
options cmplib=(advprt.functions.work.myfuncs);
```

# 15.2.3 Interaction with the Macro Language

Functions and routines created using PROC FCMP are typically called from within a DATA step; however, they may also be called from within the macro language by using the macro function %SYSFUNC and the macro statement %SYSCALL.

It is also possible to call or execute a macro from within the function or routine by using the RUN_MACRO function. The following rather silly example demonstrates some of the issues when calling a macro from within a function or routine.

```
proc fcmp outlib=advprt.functions.utilities;
subroutine prnt(dsn$, kvar $, cvar $);
  rc=run_macro('printit',dsn, kvar, cvar);
endsub;
run;
%macro printit();
  %let dsn = %sysfunc(dequote(&dsn));
  %let kvar = %sysfunc(dequote(&kvar));
  %let cvar = %sysfunc(dequote(&cvar));
  title2 "&dsn";
  proc print data=advprt.&dsn;
    %if &kvar ne %then id &kvar;
    %if &cvar ne %then var &cvar;
  run;
%mend printit;

options cmplib=(advprt.functions);
title1 '15.2.3 Macro Language Interface';
data _null_;
  set advprt.dsncontrol;
  call printit(dsn, keyvars, critvars);
  put 'Print ' dsn keyvars critvars;
run;
proc print data=advprt.dsncontrol;
run;
```

+   1. The SUBROUTINE statement declares this as the routine’s definition. Like with the FUNCTION statement the routine is named. Character argument names are followed by a $.
+   2. The first argument of the RUN_MACRO function is the name of the macro to be called. The remaining arguments are the parameters for that macro.
+   3. The positional macro parameters are not named on the %MACRO statement. The parameter names will flow from the RUN_MACRO function on through to the macro %PRINTIT.
+   4. The values of the macro parameters arrive quoted. Since we need them to be unquoted in the application shown here, the DEQUOTE function is called.
+   5. TITLE2 will be displayed when the PROC PRINT executes. Although the TITLE1 statement will have been executed, within the domain available to the compiled routine its definition is not available, and will, therefore, remain undefined.
+   6. The PROC PRINT within the macro %PRINTIT is constructed using the macro parameters.
+   7. The function library is specified.