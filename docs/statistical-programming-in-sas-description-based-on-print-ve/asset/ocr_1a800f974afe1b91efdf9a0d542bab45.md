In this %do loop, three macro variables are defined: npts_lo, npts_hi, and npts_by. These references are resolved and noted in the first lines starting with SYMBOLGEN:

```
SYMBOLGEN: Macro variable NPTS_LO resolves to 5
SYMBOLGEN: Macro variable NPTS_HI resolves to 25
SYMBOLGEN: Macro variable NPTS_BY resolves to 5
```

# Display 10.14 SAS log output produced by the SYMBOLGEN option

```
88 options symbolgen nomprint nomlogic;
89 %trap_area Z(LOW=0,HIGH=1.96,npts_lo=5,npts_hi=25,npts_by=5,
display_graph=TRUE)
SYMBOLGEN: Macro variable NPTS_LO resolves to 5
SYMBOLGEN: Macro variable NPTS_HI resolves to 25
SYMBOLGEN: Macro variable NPTS_BY resolves to 5
SYMBOLGEN: Macro variable FOUT resolves to
C:\Users\baileraj.IT\Desktop\est3.out
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable LOW resolves to 0
SYMBOLGEN: Macro variable HIGH resolves to 1.96
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable NPTS resolves to 5
SYMBOLGEN: Macro variable LOW resolves to 0
SYMBOLGEN: Macro variable HIGH resolves to 1.96
SYMBOLGEN: Macro variable NPTS resolves to 5

NOTE: The file "C:\Users\baileraj.IT\Desktop\est3.out" is:
Filename=C:\Users\baileraj.IT\Desktop\est3.out,
RECFM=V,LRECL=256,File Size (bytes)=284,
Last Modified=31Oct2009:11:38:46,
Create Time=31Oct2009:11:38:36

NOTE: 1 record was written to the file
"C:\Users\baileraj.IT\Desktop\est3.out".
The minimum record length was 54.
The maximum record length was 54.
NOTE: The data set WORK.TRAPPER has 1 observations and 17 variables.
NOTE: DATA statement used (Total process time):
real time 3.56 seconds
cpu time 0.06 seconds

SYMBOLGEN: Macro variable ODS_ON resolves to FALSE
SYMBOLGEN: Macro variable PRINT_EST resolves to FALSE
SYMBOLGEN: Macro variable NPTS resolves to 5
```