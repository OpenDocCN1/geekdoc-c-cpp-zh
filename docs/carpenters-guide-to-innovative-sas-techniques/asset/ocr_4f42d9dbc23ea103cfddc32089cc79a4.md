Since there is no informat that will effectively combine the flexibility of the ANYDTDTM. informat with the ability to interpret the AM/PM, the following adjustment can be used. ❷

```
```sas
dt_plus= input(datetime,anydtdtm.) ❶
        +(43200 ❸
        *(^(index(upcase(datetime),'PM')❹)));
```
```

12.6 ANYDATE Informats  
Converting Mixed DATETIME Values

| Obs | datetime | dt_plus |
|---:|---|---|
| 1 | 10/13/2011:15:45:12 | 13OCT2011:15:45:12 |
| 2 | 2011-03-01T15:20:45 | 01MAR2011:15:20:45 |
| 3 | 9/13/2011 11:52:54 AM | 13SEP2011:11:52:54 |
| 4 | 9/13/2011 11:52:54 PM | 13SEP2011:23:52:54 |
| 5 | 10/09/2011 11:52:54 PM | 09NOV2011:23:52:54 |
| 6 | 11/09/12 11:52:54 AM | 13SEP2012:11:52:54 |
| 7 | 2011/09/12 11:52:54 PM | 12SEP2011:23:52:54 |

ANYDTDTM. informat is used to convert the datetime string. The INPUT function returns the datetime value in seconds. ❸ If a ‘PM’ is present we need to add 12 hours worth of seconds (43,200=12*60*60) to the datetime value. ❹ The INDEX function searches for an occurrence of ‘PM’ and the location is converted to a binary 0/1 value which is multiplied by the number of seconds to add.

# 12.7 Building Formats from Data Sets

The VALUE, INVALUE, and PICTURE statements are usually used to create a user-defined format or informat. As the number of value pairs becomes large, coding the statements becomes inconvenient (for me large can be less than a dozen). Fortunately you can also define formats and informats using a data set.

PROC FORMAT accepts a data set to control the definition of the format or informat. The procedure expects specific variables, and the observations of the data set are used to form the value pairs. As a minimum the data set used to control the formation of the format must contain the variables FMTNAME, START, and LABEL ❶. It may also contain over twenty other variables that can be used to define the format.

In this example the data set CNTLRFMT will be used create a character format ($CL_REG.) that will map the clinic number (CLINNUM) into a region (REGION).

```
```sas
data cntrlfmt (keep=fmtname start label)❶;
    set advrpt.clinicnames(rename=( clinum=start ❷
                                   region=label));
    retain fmtname '$cl_reg'; ❸
    run;
proc format cntlin=cntrlfmt; ❹
    run;
```
```

❶ You may keep variables that will not be used by PROC FORMAT. Extraneous variables will be ignored.

❷ The variable

START contains the data value that is to be mapped (left side of the value pair), while LABEL is the value that will appear as a result of the mapping.

❸ The character variable FMTNAME contains the name of the format that is to be created.

❹ The CNTLIN= option is used to specify the data set that contains the format definition.