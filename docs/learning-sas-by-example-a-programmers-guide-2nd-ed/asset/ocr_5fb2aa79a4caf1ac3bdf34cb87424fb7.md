# 414 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 24.1: Listing of Data Set Clinic

| ID | VisitDate | Dx | HR | SBP | DBP |
|---|---|---|---|---||
| 101 | 10/21/2005 | GI Problems | 68 | 120 | 80 |
| 101 | 02/25/2006 | Cold | 68 | 122 | 84 |
| 255 | 09/01/2005 | Routine Visit | 76 | 188 | 100 |
| 255 | 12/18/2005 | Routine Visit | 74 | 180 | 95 |
| 255 | 02/01/2006 | Heart Problems | 79 | 210 | 110 |
| 255 | 04/01/2006 | Heart Problems | 72 | 180 | 88 |
| 303 | 10/10/2006 | Routine Visit | 72 | 138 | 84 |
| 409 | 09/01/2005 | Injury | 88 | 142 | 92 |
| 409 | 10/02/2005 | Routine Visit | 72 | 136 | 90 |
| 409 | 12/15/2006 | Routine Visit | 68 | 130 | 84 |
| 712 | 04/06/2006 | Infection | 58 | 118 | 70 |
| 712 | 04/15/2006 | Infection | 56 | 118 | 72 |

Variables in this data set are ID (ID), visit date (VisitDate), diagnosis (Dx), heart rate (HR), systolic blood pressure (SBP), diastolic blood pressure (DBP). Notice that some patients have several visits, but one patient, Number 303, has a single visit.

One of the important tasks when dealing with data sets is to identify when you are processing the first or last observation for each patient (or the variable you want to use to identify a group). Program 24.1 shows how to do this:

Program 24.1: Creating FIRST and LAST. Variables

```
proc sort data=Learn.Clinic out=Clinic;
  by ID VisitDate;
run;
data Last;
  set clinic;
  by ID;
  put ID=VisitDate First.ID= Last.ID=
  if last;
run;
```

The key to this program is the BY statement following the SET statement. In this example, the data set was also sorted by VisitDate within each ID so that the first observation for each ID would correspond to the first visit date and the last observation for each ID would correspond to the last visit date.