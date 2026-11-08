# The VALIDVARNAME=V6 Option

```
```sas
option validvarname=v6;
data a;
    abcdefghig= 5;
    run;
```
```

Useful when you are creating data sets that must conform to V6 naming conventions. While acceptable for all other values of VALIDVARNAME, the following DATA step fails when VALIDVARNAME=V6, because the variable name has more than 8 characters. This value of VALIDVARNAME= option may not be supported in future releases of SAS. In SAS 9.2 it has not been included in the documentation for the VALIDVARNAME option. Although the V6 value restricts the length of variable names it does not restrict the length of data set names, as was the case for SAS V6.

VALIDVARNAME= option may not be supported in future releases of SAS. In SAS 9.2 it has not been included in the documentation for the VALIDVARNAME option. Although the V6 value restricts the length of variable names it does not restrict the length of data set names, as was the case for SAS V6.

# The VALIDVARNAME=ANY Option

This setting permits variable names that may come from other sources, such as ORACLE or EXCEL, that do not use the same naming conventions as SAS. We access these non-standard variables through the use of named literals that are needed whenever the name contains non-standard characters. Once the data have been imported into SAS, it is generally recommended that these variables are renamed to conform to standard SAS naming conventions. When a data set contains variables defined using named literals, in order to include non-standard characters, VALIDVARNAME= must always be set to ANY before the data set can be used. Also, whenever you access any variable containing non-standard characters you must always use named literals to name the variable.

A named literal is enclosed in quotes and the quoted string is followed by the letter n.

```
```sas
options validvarnames=any;
proc print data=aexls;
  var subject 'ae-date'n 'ae#type'n;
  run;
```
```

Named literals are used just like any other variable name. Three variables are included in the VAR statement to the left.

The application of the use of VALIDVARNAMES=ANY can be shown using the EXCEL file E14_1_2AE.XLS. This spreadsheet has column headers that do not meet SAS naming standards.

|   | Subject | AE-date | AE#type |
|---|---:|---|---:|
| 2 | 201 | 24-Apr-06 | 1 |
| 3 | 202 | 15-May-06 | 2 |

PROC IMPORT can be used to convert this EXCEL table to a SAS data set. Since the GETNAMES=YES option is used, SAS will attempt to use the column headers as variable names. Without first specifying VALIDVARNAME=ANY, non-standard characters would be converted to underscores.

In this example it would not have a large impact; however, naming conflicts can arise. By using VALIDVARNAME=ANY, the names that the columns will be named in the SAS data set (WORK.AEXLS). A look at the properties of WORK.AEXLS shows that the non-standard names are being used by SAS.

```
```sas
option validvarname=any;
PROC IMPORT OUT= WORK.Aexls
    DATAFILE= "gpath\\data\\E14_1_2AE.xls"
    DBMS=EXCEL REPLACE;
    SHEET="Sheet1$";
    GETNAMES=YES;
    MIXED=NO;
    SCANTEXT=YES;
    USEDATE=YES;
    SCANTIME=YES;
RUN;
```
```

| Column Name | Type | Length |
|---|---|---:|
| Subject | Number | 8 |
| AE-date | Number | 8 |
| AE#type | Number | 8 |