```
length CholGroup = $6;
select;
when (missing(Chol)) CholGroup = ' ';
when (Chol le 110) CholGroup = 'Low';
when (Chol le 140) CholGroup = 'Medium';
otherwise CholGroup = 'High';
run;
```

title "Listing of BLOOD";
proc print data=blood noobs;
run;

*7-7;
title "Selected Observations from BIBYCLES";
proc print data=learn.bicycles noobs;
where Model eg=Road Bike and UnitCost gt 2500
Model eg="Hybrid" and UnitCost gt 660;
*Note: parentheses are not needed since that the AND
operation is performed before. You may include
run;

# Chapter 8 Solutions

```
*8-1;
data vitals;
input ID : $3.
Age
Pulse
SBP
DBP;
label SBP = "Systolic Blood Pressure"
DBP = "Diastolic Blood Pressure";
datal;
001 23 68 120 80
002 55 72 188 96
003 78 82 200 100
004 18 58 116 70
005 43 52 120 82
006 37 74 150 98
007 82 140 100
;

***Note: this program assumes there are no
missing values for Pulse or SBP;
data newvisits;
set vitals;
if Age lt 50 and not missing(Age) then do;
if Pulse lt 70 then PulseGroup = 'Low';
else PulseGroup = 'High';
if SBP lt 140 then SBPGroup = 'Low';
else SBPGroup = 'High';
end;
if Age ge 50 then do;
if Pulse lt 74 then PulseGroup = 'Low';
else PulseGroup = 'High';
if SBP lt 140 then SBPGroup = 'Low';
else SBPGroup = 'High';
end;
run;
```