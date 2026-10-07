# Chapter 2: Introduction to the DS2 Language 13

System methods execute automatically and do not accept parameters. You must explicitly define at least one of these methods in your data or thread program or the program will not execute. You do not write explicit code for one or more system method blocks, the DS2 compiler will create an empty version of the missing system method for you at compile time. An empty method contains only the appropriate METHOD statement by an END statement.

# 2.2.5.1 The INIT Method

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

# 2.2.5.2 The RUN Method

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
```