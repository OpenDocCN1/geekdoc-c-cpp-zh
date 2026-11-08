
Since there is no informat that will effectively combine the flexibility of the ANYDTDTM. informat with the ability to interpret the AM/PM, the following adjustment can be used. ❷

```sas
dt_plus = input(datetime, anydtdtm.) ❶
        + (43200 ❸
        * (index(upcase(datetime), 'PM') > 0) ❹);
```

## 12.6 ANYDTDTM Informats

### Converting Mixed DATETIME Values

| Obs | datetime | dt_plus |
|---:|---|---|
| 1 | 10/13/2011:15:45:12 | 13OCT2011:15:45:12 |
| 2 | 2011-03-01T15:20:45 | 01MAR2011:15:20:45 |
| 3 | 9/13/2011 11:52:54 AM | 13SEP2011:11:52:54 |
| 4 | 9/13/2011 11:52:54 PM | 13SEP2011:23:52:54 |
| 5 | 11/09/2011 11:52:54 PM | 09NOV2011:23:52:54 |
| 6 | 9/13/12 11:52:54 AM | 13SEP2012:11:52:54 |
| 7 | 2011/09/12 11:52:54 PM | 12SEP2011:23:52:54 |

ANYDTDTM. informat is used to convert the datetime string. The INPUT function returns the datetime value in seconds. If a ‘PM’ is present, we need to add 12 hours’ worth of seconds (43,200 = 12*60*60) to the datetime value. ❸ The INDEX function searches for an occurrence of ‘PM’ and the location is converted to a binary 0/1 value, which is multiplied by the number of seconds to add. ❹

## 12.7 Building Formats from Data Sets

The VALUE, INVALUE, and PICTURE statements are usually used to create a user-defined format or informat. As the number of value pairs becomes large, coding the statements becomes inconvenient (for me large can be less than a dozen). Fortunately you can also define formats and informats using a data set.

PROC FORMAT accepts a data set to control the definition of the format or informat. The procedure expects specific variables, and the observations of the data set are used to form the value pairs. As a minimum, the data set used to control the formation of the format must contain the variables FMTNAME, START, and LABEL ❶. It may also contain over twenty other variables that can be used to define the format.

In this example the data set CNTLRFMT will be used to create a character format ($CL_REG.) that will map the clinic number (CLINNUM) into a region (REGION).

```sas
data cntrlfmt (keep=fmtname start label) ❶;
    set advrpt.clinicalnames(rename=(clinnum=start ❷
                                     region=label));
    retain fmtname '$cl_reg'; ❸
run;
proc format cntlin=cntrlfmt; ❹
run;
```

❶ You may keep variables that will not be used by PROC FORMAT. Extraneous variables will be ignored.

❷ The variable START contains the data value that is to be mapped (left side of the value pair), while LABEL is the value that will appear as a result of the mapping.

❸ The character variable FMTNAME contains the name of the format that is to be created.

❹ The CNTLIN= option is used to specify the data set that contains the format definition.

The control data set may define more than one format definition; however, if it does, the data set must be sorted by format name (or at least grouped by format name). In the following example

```sas
data cntrlfmt(keep=fmtname start label);
   set advrpt.clinicalnames(rename=(clinnum=start));
   length fmtname $8 label $40;
   fmtname = '$cl_reg';
   label = region;
   output cntrlfmt;
   fmtname = '$cl_name';
   label = clinname;
   output cntrlfmt;
run;
proc sort data=cntrlfmt;
   by fmtname start;
run;
proc format cntlin=cntrlfmt;
run;
```

each incoming observation is used to build two formats ($CL_REG and $CL_NAME). Notice that the control data set has been sorted by the format name prior to passing it to the FORMAT procedure.

The list of potential variables in the control data set that can be utilized by PROC FORMAT is quite extensive, and while they are well documented, you can use PROC FORMAT and the CNTLOUT= option to surface the format definition by writing it to a data set. This will reveal the variable names that can be used in a format definition and can give you a good idea about their usage.

```sas
proc format cntlout=control(where=(fmtname='CL_NAME'));
run;
proc print data=control;
run;
```

| Obs | FMTNAME | START | END | LABEL | MIN | MAX | DEFAULT | LENGTH | FUZZ | PREFIX | FILL | TYPE | NOEDIT | SEXCL |
|---:|---|---|---|---|---:|---:|---:|---:|---:|---:|---:|---|---|---|
| 1 | CL_NAME | 011234 | 011234 | Boston National Medical | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 2 | CL_NAME | 014321 | 014321 | Vermont Treatment Center | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 3 | CL_NAME | 023910 | 023910 | New York Metro Medical Ctr | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 4 | CL_NAME | 024477 | 024477 | New York General Hospital | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 5 | CL_NAME | 026789 | 026789 | Geneva Memorial Hospital | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |

```sas
libname oldfmt 'c:\temp1';
libname newfmt 'c:\temp2';
libname allfmt (newfmt oldfmt);

proc format library=oldfmt;
  value yesno 1 = 'Yes'
              0 = 'No';
  value generation
    low - <1950 = 'Greatest'
    1950 - high = 'Boomer';
run;

proc format library=newfmt;
  value gender 1 = 'Female'
               0 = 'Male';
  value yesno 1 = 'No'
              0 = 'Yes';
run;

title1 '12.9.3 Display Format names';
proc catalog cat=allfmt.formats;
  contents;
quit;

options fmtsearch=(allfmt work);
```

- 1. Any references to the *libref* ALLFMT will point to both of the other two locations.
- 2. The YESNO. format appears in both format libraries. Notice that the two definitions are *not* the same.
- 3. PROC CATALOG is used here to show the locations of the formats. The column LEVEL refers to the library containing the catalog that contains the format.
- 4. Before any of the formats in the ALLFMT library can be used, the library must be included on the search path. Formats in ALLFMT will be found before any formats with the same name in the WORK library. Within ALLFMT, catalogs are searched from left to right. The version of the YESNO. format in the NEWFMT library will be used.

The output generated by the CATALOG procedure shows that the various formats can be found in the concatenated library ALLFMT. It also shows that the YESNO. format, which is defined in both the OLDFMT and NEWFMT catalogs, is being picked up from the first catalog in the list (NEWFMT – LEVEL=1).

### 12.9.3 Display Format names

| # | Name | Type | Level | Create Date | Modified Date | Description |
|---:|---|---|---:|---|---|---|
| 1 | GENDER | FORMAT | 1 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |
| 2 | GENERATION | FORMAT | 2 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |
| 3 | YESNO | FORMAT | 1 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |

![](img/4b16455363806a3241267bf9f49ba5d1_425_0.png)

## Chapter 13: Interfacing with the Macro Language

- 13.1 Avoiding Macro Variable Collisions—Make Your Macro Variables %Local 398
- 13.2 Using the SYMPUTX Routine 400
  - 13.2.1 Compared to CALL SYMPUT 401
  - 13.2.2 Using SYMPUTX to Save Values of Options 402
  - 13.2.3 Using SYMPUTX to Build a List of Macro Variables 402
- 13.3 Generalized Programs—Variations on a Theme 403
  - 13.3.1 Steps to the Generalization of a Program 403
  - 13.3.2 Levels of Generalization and Levels of Macro Language Understanding 405
- 13.4 Utilizing Macro Libraries 406
  - 13.4.1 Establishing an Autocall Library 406
  - 13.4.2 Tracing Autocall Macro Locations 408
  - 13.4.3 Using Stored Compiled Macro Libraries 408
  - 13.4.4 Macro Library Search Order 409
- 13.5 Metadata-Driven Programs 409
  - 13.5.1 Processing across Data Sets 409
  - 13.5.2 Controlling Data Validations 410
- 13.6 Hard Coding—Just Don’t Do It 415
- 13.7 Writing Macro Functions 417
- 13.8 Macro Information Sources 420
  - 13.8.1 Using SASHELP and Dictionary tables
  - 13.8.2 Retrieving System Options and Settings 422
  - 13.8.3 Accessing the Metadata of a SAS Data Set 424
