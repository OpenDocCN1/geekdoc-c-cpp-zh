# 472 Learning SAS by Example: A Programmer's Guide, Second Edition

```
02/23/05
03/15/15
05/09/06
;
options yearcutoff=1920;
/* Good idea to set yearcutoff back to
the default after you change it */
title "Listing of YEAR1910_2006";
proc print data=year1910_2006 noobs;
run;
```

```
*9-5;
data freq;
set learn.hosp(keep=AdminDate);
Day = weekday(AdminDate);
Month = month(AdminDate);
Year = year(AdminDate);
run;
```

```
proc format;
value days 1='Sun' 2='Mon' 3='Tue'
4='Wed' 5='Thu' 6='Fri'
7='Sat';
value months 1='Jan' 2='Feb' 3='Mar'
4='Apr' 5='May' 6='Jun'
7='Jul' 8='Aug' 9='Sep'
10='Oct' 11='Nov' 12='Dec';
run;
```

```
title "Frequencies for Hospital Admissions";
proc freq data=freq;
tables Day Month Year / nocum nopercent;
format Day. Month.;
run;
```

```
*9-7;
title "Admissions before July 15, 2002";
proc print data=learn.hosp;
where AdminDate = '15Jul2002' and
AdminDate is not missing;
run;
```

```
*9-9;
data dates;
input (Day) Month Year;
if missing(Day) then Date = mdy(Month,15,Year);
elelse Date = mdy(Month,Day,Year);
format Date mmddyy10.
datallines;
25 12 2005
5 2 2006
;
```

```
title "Listing of DATES";
proc print data=dates noobs;
run;
```

```
*9-11;
data intervals;
set learn.medical;
Quarters = intck('qtr','01Jan2006'd,VisitDate);
```