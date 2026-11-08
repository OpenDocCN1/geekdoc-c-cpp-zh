# ## Driving an Automated Process

Any data set or even any information arranged in rows and columns can be used as the driving information for automating a process. The SAS macro language is especially powerful when it comes to creating applications and programs that rely on external information to make decisions.

In this example that external information will be a data set created through the use of ODS and the OUTPUT destination. The example process shown here, one that we would like to execute many times, is a simple PROC PRINT, but in reality it could be any number of DATA and PROC steps. In this case we want to execute the %PROCESS macro once for every level of a classification variable (in this example the classification variable must be character). The control will be accomplished using a WHERE clause ❶ that will be constructed in the controlling macro (%DOPROCESS) ❷.

```
```
%macro process(dsn=,whr=);
    proc print data=&dsn;
        where &whr; ❶
    run;
%mend process;
```
```

The controlling macro, %DOPROCESS, uses PROC FREQ with the OUTPUT destination ❷ to form a data set containing one level for each distinct value of the classification variable (&CVAR).

```
```
%macro doprocess(dsn=, cvar=);
    ods output onewayfreqs=levels; ❷
    proc freq data=&dsn;
        table &cvar;
    run;
    data _null_;
        set levels; ❸
        whr = cats("&cvar=", &cvar, ""); ❹
        call execute('%nrstr(%process(dsn='||"&dsn"||',whr='||whr||'))'); ❺
    run;
%mend doprocess;

%doprocess(dsn=advrpt.demog, cvar=sex) ❻
```
```

+   - ❷ ODS OUTPUT and a PROC FREQ are used to create a data set (WORK.LEVELS) that will contain one row for each unique value of the classification variable (&CVAR).
+   - ❸ The data set created by the OUTPUT destination is read as input for the DATA _NULL_ step.
+   - ❹ The WHERE criteria is constructed and placed in the variable WHR, which will be added as text to the macro call ❺.

+   - ❺ CALL EXECUTE is used to build a series of calls to the macro %PROCESS; one for each level of the classification variable.
+   - ❻ The %DOPROCESS macro is called with the data set and classification variable of interest.

# ### MORE INFORMATION

In this example an SQL step could have also been used to create the data set WORK.LEVELS, but this is not always the case. PROC SQL is used to create a distinct list of values in the second example in Section 11.2.2.