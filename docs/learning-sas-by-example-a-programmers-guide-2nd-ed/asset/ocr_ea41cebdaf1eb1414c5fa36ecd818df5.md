# 390 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 22.13: Listing of Data Set Control (with OTHER Added)

| Unformatted_ICD | ICD10 |
|--- |--- |
| 020 | Plague |
| 410 | Myocardial infarction |
| 500 | Not Found |
| 493 | Asthma |

Both the unformatted and formatted values of the ICD data are shown so that it is clear that the code of 500 now shows Not Found.

# 22.8 Updating and Maintaining Your Formats

Suppose you want to add some ICD-10 codes to your $ICDFmt. The easiest way to accomplish this is to first use the CNTLOUT option of PROC FORMAT to create a data set containing all the formatting information. You can then use this data set in a DATA step to add new codes or modify existing ones.

As an example, suppose you want to add two new ICD-10 codes to your $ICDFMT format, 427.5 (bronchitis) and 466 (cardiac arrest). The following program does the trick:

Program 22.13: Updating an Existing Format Using the CNTLOUT= Data Set Option

```
proc format cntnout=Control_Out;
    select $ICDFMT;
run;

data New_Control;
    length Label = $21;
    set Control_Out end=Last;
    output;

    if Last then do;
        Hlo = ' ';
        Start = '427.5';
        End = Start;
        Label = 'Cardiac Arrest';
        output;
        Start = '466';
        End = Start;
        Label = 'Bronchitis';
        output;
    end;

run;

proc format cntlin=New_Control;
    select $ICDFMT;
run;
```