238 Learning SAS by Example: A Programmer's Guide, Second Edition

# Program 15.1: Listing of Medical Using PROC PRINT

```
title "Listing of Data Set Medical from PROC PRINT";nproc print data=Learn.Medical;
id Patno;
run;
```

This program produces the following list:

Figure 15.1: Output from Program 15.1

| Patno | Clinic | VisitDate | Weight | HR | DX | Comment |
|---|---|---|---|---|---||}{
| 001 | Mayo Clinic | 10/21/2006 | 120 | 78 | 7 | Patient has a persistent cough for 3 weeks |
| 003 | HMC | 09/01/2006 | 166 | 58 | 8 | Patient placed on beta-blockers on 7/1/2006 |
| 002 | Mayo Clinic | 10/01/2006 | 210 | 68 | 9 | Patient has been on antibiotics for 10 days |
| 004 | HMC | 11/01/2006 | 288 | 88 | 9 | Patient advised to lose some weight |
| 007 | Mayo Clinic | 05/01/2006 | 180 | 54 | 7 | This patient is always under high stress |
| 050 | HMC | 07/06/2006 | 199 | 60 | 12 | Refer this patient to mental health for evaluation |

# 15.2 Using PROC REPORT

Here is a report, using the same data set, produced by PROC REPORT:

# Program 15.2: Using PROC REPORT (All Defaults)

```
title "Using the REPORT Procedure;";
proc report data=Learn.Medical;
run;
```

Here is the output:

Figure 15.2: Output from Program 15.2

| Patno | Clinic | VisitDate | Weight | Heart Rate | DX | Comment |
|---|---|---|---|---|---||}{
| 001 | Mayo Clinic | 10/21/2006 | 120 | 78 | 7 | Patient has a persistent cough for 3 weeks |
| 003 | HMC | 09/01/2006 | 166 | 58 | 8 | Patient placed on beta-blockers on 7/1/2006 |
| 002 | Mayo Clinic | 10/01/2006 | 210 | 68 | 9 | Patient has been on antibiotics for 10 days |
| 004 | HMC | 11/01/2006 | 288 | 88 | 9 | Patient advised to lose some weight |
| 007 | Mayo Clinic | 05/01/2006 | 180 | 54 | 7 | This patient is always under high stress |
| 050 | HMC | 07/06/2006 | 199 | 60 | 12 | Refer this patient to mental health for evaluation |