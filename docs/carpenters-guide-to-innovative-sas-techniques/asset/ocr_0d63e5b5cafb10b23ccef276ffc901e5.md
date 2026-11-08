# ### 13.10.3 Using the MINDELIMITER= Option

By default the IN operator expects the list of values to be space separated; however, it is possible to use the MINDELIMITER= option to specify an alternate delimiter for the list. Like the MINOPERATOR option, the MINDELIMITER= option can be specified at the system option level or at the macro level, and again my recommendation is to always apply it on the %MACRO statement and not at the system level. Here the MINDELIMITER= option has been added to the %MACRO statement ❶ to allow a comma separated list ❷ of values.

```
```sas
%macro testIN(dsn=demog) /minoperator
    mindelimiter=','; ❶
  %if %upcase(&dsn) in (AE,CONMED,DEMOG) ❷ %then %do;
    %put &dsn count %obscnt(advrpt,&dsn);
  %end;
%mend testin;
%testin(dsn=demog)
```
```

By enclosing the list in parentheses and by using the IN mnemonic, as was done here, the macro expression more closely mimics the syntax used with the DATA step's IN operator.

# ### 13.10.4 Compilation vs. Execution for these Options

When using the system option versions of MINOPERATOR and MINDELIMITER=, it is important to understand the difference between compilation and execution of the macro. If you intend to use these options on the %MACRO statement (as I have suggested), rather than as system options, then the issues discussed below will not affect you, as the values declared on the %MACRO statement will override the system options during both compilation and execution.

# #### The MINDELIMITER= System Option

The value of the MINDELIMITER= option is set when the macro is compiled. Subsequent changes to this option will not affect the execution of the macro.

```
```sas
options minoperator mindelimiter=','; ❶
%macro testIN(dsn=demog);
  %if %upcase(&dsn) in (AE,CONMED,DEMOG) %then %do;
    %put &dsn count %obscnt(advrpt,&dsn);
  %end;
  %else %PUT &DSN not on the list;
%mend testin;
* change in mindelimiter does not break the macro;
options minoperator mindelimiter=' '; ❷
%testin(dsn=conmed)
```
```

+   - ❻ The MINDELIMITER= option has been set prior to the compilation of the macro %TESTIN.
+   - ❼ Prior to execution, the value of the MINDELIMITER= option has been changed to a blank.

Although the value of the MINDELIMITER= option has been changed ❼, the %TESTIN macro will still operate correctly. This means that before you compile a macro that depends on the MINDELIMITER= system option, you must either know the current value of the option or explicitly set this system option prior to compiling the macro. You do not, however, need to know the current setting when executing the macro.