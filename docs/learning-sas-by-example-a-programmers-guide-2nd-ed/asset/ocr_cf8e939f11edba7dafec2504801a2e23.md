# 484 Learning SAS as Example: A Programmermer's Guide, Second Edition

```
*16-5;
proc format;
value rank 0-50 = 'Bottom Half'
51-74 = 'Third Quartile'
75-100 = 'Top Quarter';
run;
```

```
title "Statistics on the College Data Set";ntitle2 "Broken by School Size";nproc means data=learn.college
n
mean
maxdec=2;
class ClassRank;
var GPA;
format ClassRank.
run;
```

```
*16-7;
proc means data=learn.college noprint chartype;
class GenderSchoolSize;
var ClassRank GPA;
output out=summary
n=mean= median= min= max= / automeane;
run;
```

```
data grand(drop-GenderSchoolSize)
bygender(drop-SchoolSize)
bysize(drop-Gender)
cellndrop_freq;
set summary;
if _type_ = '00' then output grand;
elelse if _type_ = '10' then output bygender;
elelse if _type_ = '01' then output bysize;
elelse if _type_ = '11' then output cell;
run;
```

```
title "Listing of GRAND";nproc print data=grand noobs;
run;
```

```
title "Listing of BYGENDER"
proc print data=bygender noobs;
run;
```

```
title "Listing of BYSIZE"
proc print data=bysize noobs;
run;
```

```
title "Listing of CELL"
proc print data=cell noobs;
run;
```

# Chapter 17 Solutions

```
*17-1;
title "One-way Frequencies from BLOOD Data Set"
proc freq data=learn.blood;
tables Gender BloodType AgeGroup / nocumpercent;
```