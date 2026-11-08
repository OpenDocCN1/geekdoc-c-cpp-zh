```
~~~sas
proc means data=advrpt.demog noprint;
  class sex;
  var ht wt;
  output out=stats
    n=
    mean=
    stderr= / autoname;
run;
~~~
```

Consider the following simple PROC MEANS step. We want to generalize the step to allow processing against any data set and any list of classification and analysis variables. We may also want to allow the user to choose whether or not the procedure will generate printed output. The bolded sections of code are those things that we will need to control using macro language elements. These are the items that will be dependent on run-time conditions.

```
~~~sas
proc means data=&dsn &print;
  class &classlst;
  var &varlst;
  output out=&outdsn
    n=
    mean=
    stderr= / autoname;
run;
~~~
```

These dependencies are then converted to macro language elements, in this case macro variables. The values of these macro variables can be supplied in a number of different ways. For the simple,

most straightforward case, the values can be supplied as parameters in a macro call.

The macro %MYMEANS uses keyword parameters to specify the macro parameters. In addition the macro also performs some logic checks.

```
~~~sas
%macro mymeans(dsn=advrpt.demog,
        classlst=sex,
        varlst=ht wt,
        outdsn=stats,
        print=noprint ❶);
proc means data=&dsn
%if &outdsn = %then print; ❷
%else &print; ❸
%if &classlst ne %then %do; class &classlst;%end; ❹
%if &varlst ne %then %do; var &varlst; %end; ❺
%if &outdsn ne %then %do; ❻
  output out=&outdsn n= mean= stderr= / autoname;
%end;
run;
%mend mymeans;
~~~
```

+   - ❶ By default no printed output will be written; however, if there is no summary data set specified ❷ printed output is automatically generated.
+   - ❷ The user can request both printed output and a summary data set by setting &PRINT to PRINT. The second semicolon closes the PROC statement.

❸ The CLASS and VAR statements are only written if one or more variables have been specified. The %DO blocks are not really needed here, but they eliminate the need to have a double semicolon, such as was used on the %ELSE ❸.

❹ When the name of a summary data set is provided the OUTPUT statement is written.

The following calls of the %MYMEANS macro demonstrate its flexibility.

This call to %MYMEANS will change the data set and analysis variables, use the default classification variable, and will produce no printed output.

```
~~~sas
%mymeans (dsn=sashelp.class, varlst=height weight)
~~~
```

```
~~~sas
%mymeans (outdsn=)
~~~
```

Here only printed output is generated using all the standard defaults for the macro.