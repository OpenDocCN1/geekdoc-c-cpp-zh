The macro %DATAVAL reads the DSCONTROL metadata and then builds macro variable lists

```
```sas
%macro dataval;
%local i;
* Determine list of data sets to check;
data _null_; ❾
  set advrpt.dsncontrol;
  cnt = left(put(_n_,5.));
  call symputx('dsn'||cnt,dsn,'l');
  call symputx('keyvars'||cnt,keyvars,'l');
  call symputx('dsncntr',cnt,'l');
run;

%* Perform data validation checks on
%* each data set;
%do i = 1 %to &dsncntr;
  %if %sysfunc(notdigit(&keyvars&i)) %then %do;
    %errrpt(dsn=&&dsn&i, keyvars=&&keyvars&i)
  %end;
%mend dataval;
%dataval
```
```

of data set names and BY variables. Those macro variable lists are then used to call the %ERRRPT macro (shown above) for each data set.

❾ A DATA step is used to create the lists of macro variables. This type of list is generally easier to create using an SQL step.

❿ An iterative %DO loop is used to process across the list of data sets.

```
```sas
%macro dataval2;
* Determine list of data sets to check;
proc sql noprint;
  select dsn,keyvars
    into :dsn1-:dsn999,
         :keyvars1-:keyvars999
    from advrpt.dsncontrol;
  %let dsncntr=&sqlobs;
quit;

%* Perform data validation checks;
%* on each data set;
%do i = 1 %to &dsncntr;
  %errrpt(dsn=&&dsn&i, bylist=&&keyvars&i)
%end;
%mend dataval2;
```
```

In some instances you may want to store the validation formula itself in the metadata. Although technically this can be more challenging, the methodology is an expansion of the techniques shown above.

The DATA_NULL_ step in the %DATAVAL macro could have been replaced with a PROC SQL step. The end result is the same with the exception that we cannot as easily control the symbol

table for the derived macro variables.

The generation of the list of macro variables can be avoided altogether by using the CALL EXECUTE routine.