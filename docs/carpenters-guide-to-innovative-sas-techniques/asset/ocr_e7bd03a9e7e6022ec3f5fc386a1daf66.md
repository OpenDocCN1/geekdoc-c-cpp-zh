```
```sas
%macro errrpt(dsn=, keyvars=subject); ❶
%local i;
data null ; ❷
  set advrpt.fldchk(where=(upcase(dsn)=upcase("&dsn")));
  fldcnt+1;
  cnt = left(put(fldcnt,6.));
  call symputx('errd',cnt, 'l');
  call symputx('ervar',var,'l');
  call symputx('errtxt',chktext,'l');
  call symputx('errtype',chktype,'l');
  call symputx('errtxt',chktext,'l');
  call symputx('chkcnt',cnt,'l');
run;
data errrpt&dsn ❸
     (keep=dsn
           &keyvars
           ervar erval errtxt errating);
  length dsn     $25
         ervar   $15
         erval   $25
         errtxt  $25
         erratng 8;
  set advrpt.&dsn;

%do i = 1 %to &chkcnt; ❹
  /* Write as many error checks as are needed; */
  if ❺
  /* Determine the error expression; */
  %if %upcase(&errtype&i) = NOTMISS %then ❻
     missing(&ervar&i); ❼
  %else %if %upcase(&errtype&i) = LIST %then
     &ervar&i not in(&errtxt&i); ❼
  %else %if %upcase(&errtype&i) = DATEFMT %then
     input(&ervar&i,&errtxt&i) eq .; ❼
  %else %if %upcase(&errtype&i) = MAXIMUM %then
     &ervar&i gt &errtxt&i; ❼
  then do; ❸
    dsn = "&dsn";
    ervar = "&ervar&i";
    erval = &ervar&i;
    errtxt = "&errtxt&i";
    erratng= &erratng&i;
    output errrpt&dsn;
  end;
  %end;
run;

title2 "Data Errors for the &dsn data set";
proc print data=errrpt&dsn;
run;
%mend errrpt;
```
```

+   ❶ The %ERRRPT macro is passed the name of the data set to be checked and the key variables for that data set.
+   
+   ❷ A DATA _NULL_ step is used to read the error metadata appropriate for the data set to be checked.
+   
+   ❸ A data set containing the data errors is defined. Here it is written to the WORK directory and its name includes the name of the data set being checked.
+   
+   ❹ A macro %DO loop is used to cycle across the checks that have been requested in the metadata for this data set.
+   
+   ❺ The expression used to detect the data error will be written for the DATA step IF statement by a macro %IF and will be based on the metadata.

The IF statement terminates with a THEN DO/END at ❸.

❻ A %IF statement is used to determine the type of error comparison that is to be written.

❼ The error condition specified in the metadata is written.