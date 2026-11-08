❽ The error information is written to the error reporting data set. This THEN DO/END terminates the IF statement started at ❺.

The macro %ERRRPT is called once for each data set that is to have its data validated. The list of data sets used in the study, along with their key variables, can also be placed in metadata. For the study data being checked in this example, the metadata used to describe the study data sets can be found in ADVRPT.DSNCONTROL (see Section 13.5.1).

For the checks on the DEMOG data set the following DATA step is written by the %ERRRPT macro. Notice that only the two checks associated with this data set in the metadata have been included and that the appropriate variables have been used in the checks.

```
```sas
data errptdemog (keep=dsn subject errvar errval errtxt errrating);
length dsn $25 errvar $15 errval $25 errtxt $25 errrating 8;
set advrpt.democ;
if missing(subject) ❼ then do;
dsn = "demog";
errvar = "subject";
errval = subject;
errtxt = "";
errrating= 1;
output errptdemog;
end;
if RACE not in(('1','2','3','4','5','6')) ❼ then do;
dsn = "demog";
errvar = "RACE";
errval = RACE;
errtxt = "('1','2','3','4','5','6')";
errrating = 2;
output errptdemog;
end;
run;
```
```

The ERRRPTDEMOG data set will contain any detected errors (in this case a single error was found—a missing value for the variable RACE).

13.5.2 Metadata Driven Field Checks  
Data Errors for the demog data set

| Obs | dsn | errvar | errval | errtxt | errrating | subject |
|---:|---|---|---|---|---:|---:|
| 1 | demog | RACE |  | ('1','2','3','4','5','6') | 2 | 204 |