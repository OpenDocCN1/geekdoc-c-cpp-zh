# 13.8.2 Retrieving System Options and Settings

It is not unusual for a macro to need to adjust the value of a system option or setting during macro execution. If a macro changes system settings, such as options, during execution, these settings should be returned to their original values at the completion of the macro’s execution. This means that the original settings must be captured, saved, and restored.

The SASHELP views and DICTIONARY tables mentioned in Section 13.8.1 are one source of this type of information. Sources for SAS system option settings include:

+   - SASHELP.VOPTIONS
+   - SASHELP.VALLOPT
+   - SASHELP.VGOPT
+   - DICTIONARY.GOPTIONS
+   - DICTIONARY.OPTIONS
+   - GETOPTION function

The portion of the macro %SECURECODE shown here grabs the current settings for the system

```
```sas
%macro securecode;
data _null_;
  set sashelp.voption
      (where=(optnam in ('MPRINT','MLOGIC','SYMBOLGEN')));
  call symputx('hold'||left(optnam),optnam,'l');
run;
options nomprint nologic nosymb ogen;

/* secure code goes here*/

options &holdmprint &holdmlogic &holdsymb olgen;
%mend securecode;
```
```

options MPRINT, SYMBOLGEN, and MLOGIC, saves them in macro variables whose names start with HOLD, and then turns these options off so that the code used in the macro will not be revealed in the LOG. At the conclusion of the macro these three options are reset to their original values.

It is also possible to collect setting values through the use of functions. There are a great many functions that can be used to obtain this kind of information and it is essential for an advanced macro programmer to be well versed in which ones can be useful.

The documentation groups functions by category and some of these categories contain functions that are especially useful for obtaining information about system settings. These include:

+   - External files
+   - SAS File I/O
+   - Special