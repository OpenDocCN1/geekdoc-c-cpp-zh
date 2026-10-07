```
DATA RECOVERY;
INPUT LNAME $ RECTIME;
DATALINES;
JONES 3.1
SMITH 3.6
HARRIS 4.2
MCCULLEY 2.1
BROWN 2.8
CURTIS 3.8
JOHNSTON 1.8

RUN;
PROC PRINT DATA=RECOVERY;
Title 'Exercise 1.2 - Your Name';
RUN;
PROC MEANS DATA=RECOVERY;
RUN;
```

Include your name in the TITLE line. Observe the results in the Results Viewer. (You may optionally print, save, or e-mail the output as directed by your instructor. These instructions will be assumed from this point on and will not be included in future exercises.)