

# 468 实例实例 SAS 学习：程序员指南，第二版

```sas
21-40 = '2'
41-60 = '3'
61-80 = '4'
81-high = '5';
nrun;
```

## 第6 章答案

```sas
*6-1;
/*
文件 --> 导入数据
选择 Excel 并选择 Drugtest.xls。
*/

*6-3;
*修改此 libname 语句;
libname maxit 'c:\books\learning\soccer.xls'
title="使用引擎读取数据";
proc print data=readit.soccer$ noobs;
run;
```

## 第7 章答案

```sas
*7-1;
data school;
input Age Quiz : $1 Midterm Final;
if Age = 12 then Grade = 6;
else if Age = 13 then Grade = 9;
if Quiz = 'A' then QuizGrade = 95;
if Quiz = 'B' then QuizGrade = 85;
else if Quiz = 'C' then QuizGrade = 75;
else if Quiz = 'D' then QuizGrade = 70;
else if Quiz = 'P' then QuizGrade = 65;
FinalGrade = .2*QuizGrade + .3*Midterm + .5*Final;
datalines;
12 A 92 95
12 B 88 88
13 C 70 75
13 A 92 93
12 F 55 62
13 B 88 82;
;
```

```sas
title "SCHOOL 列表";
proc print data=school noobs;
run;
```

```sas
*7-3;
title "从 SALES 中筛选员工";
proc print data=learn.sales;
where EmpID = '9888' or EmpID = '0177';
run;
```

```sas
proc print data=learn.sales;
where EmpID in ('9888' '0177');
run;
```

```sas
*7-5;
data blood;
set learn.blood;
```

```sas
length CholGroup = $6;
select;
when (missing(Chol)) CholGroup = ' ';
when (Chol le 110) CholGroup = 'Low';
when (Chol le 140) CholGroup = 'Medium';
otherwise CholGroup = 'High';
end;
run;

title "BLOOD 列表";
proc print data=blood noobs;
run;

*7-7;
``````sas
title "从 BICYCLES 中筛选观测值";
proc print data=learn.bicycles noobs;
where Model="Road Bike" and UnitCost gt 2500
or Model="Hybrid" and UnitCost gt 660;
*注：不需要括号，因为 AND 操作是先执行的。你可以包含
run;
```

```

## 第8 章答案

```sas
*8-1;
data vitals;
input ID : $3.
Age
Pulse
SBP
DBP;
label SBP = "收缩压"
DBP = "舒张压";
datal;
001 23 68 120 80
002 55 72 188 96
003 78 82 200 100
004 18 58 116 70
005 43 52 120 82
006 37 74 150 98
007 82 140 100
;

***注：此程序假设 Pulse 或 SBP 没有缺失值；
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

# 470 实例实例 SAS 学习：程序员指南，第二版

```sas
title "NEWVITALS 列表";
proc print data=newvitals noobs;
run;

*8-3;
data test;
  input Score-Score3;
  Subj + 1;
datalines;
90 88 92
75 76 88
88 82 91
72 68 70
;

title "TEST 列表";
proc print data=test noobs;
run;

*8-5;
data logs;
do N = 1 to 20;
  LogN = log(N);
  output;
end;
run;

title "LOGS 列表";
proc print data=logs noobs;
run;

*8-7;
data plotit;
do x = 0 to 10 by .1;
  y = 3*x*2 - 5*x + 10;
  output;
end;
run;

title "问题 7";
proc sgplot data=plotit;
  series x=x y=y;
run;

*8-9;
data temperatures;
do Day = 'Mon','Tue','Wed','Thu','Fri','Sat','Sun';
  input Temp @;
  output;
end;
datalines;
70 72 74 76 77 78 85;
;

title "TEMPERATURE 列表";
proc print data=temperatures noobs;
run;

*8-11;
data temperature;
  length City $7;
do City = 'Dallas', 'Houston';
do Hour = 1 to 24;
  input Temp @;
  output;
end;
datalines;
80 81 82 83 84 84 87 88 89 90 91 93 93 95 96 97 95 92 90 86 84 80 78 76 74;
;

title "Dallas 和 Houston 的温度";
proc print data=temperature;
run;

*8-13;
data money;
do Year = 1 to 99 until (Amount ge 300);
  Amount = 1000;
  do Quarter = 1 to 4;
    Amount = Amount*(25/4);
    output;
  end;
end;

title "MONEY 列表";
proc print data=money;
run;

## 第9 章答案

```sas
*9-1;
data dates;
input @1 Subj $3 mmy;
@4 Visit;
Age = ydiff(DOB,Visit);
format DOB Visit;
datalines;
01/10/1950
01/11/1950
02/02/1955
03/15/2005
05/09/2006
12/25/2006;
;

title "DATES 列表";
proc print data=dates;
run;
```

```sas
*9-3;
options yearcutoff=1910;
data year910_2006;
  input @1 Date mmyy.;
  format Date;
datalines;
01/01/1911
02/23/1905
03/15/2015
05/09/2006
12/25/2006;
```

# 472 实例实例 SAS 学习：程序员指南，第二版

```sas
*9-5;
data freq;
set learn.hosp(keep=AdminDate);
Day = weekday(AdminDate);
Month = month(AdminDate);
Year = year(AdminDate);
run;

proc format;
value days 1='Sun' 2='Mon' 3='Tue'
4='Wed' 5='Thu' 6='Fri'
7='Sat';
value months 1='Jan' 2='Feb' 3='Mar'
4='Apr' 5='May' 6='Jun'
7='Jul' 8='Aug' 9='Sep'
10='Oct' 11='Nov' 12='Dec';
end;

title "医院入院频率";
proc freq data=freq;
tables Day Month / nocum nopercent;
format Day. Month.;
run;
```

```sas
*9-7;
title "2002年7月15日之前的入院";
proc print data=learn.hosp;
where AdminDate < '15JUL2002' and
AdminDate not missing;
run;
```

```sas
*9-9;
data dates;
input (Day) Month Year;
if missing(Day) then Date = mdy(Month,15,Year);
else Date = mdy(Month,Day,Year);
format Date mmddyy.
datal;
25 12 2005
5 2 2006;
;

title "DATES 列表";
proc print data=dates noobs;
run;
```

```sas
*9-11;
data intervals;
set learn.medical;
Quarters = intck('qtr','01JAN2006'd,VisitDate);
run;

title "INTERVALS 列表";
proc print data=intervals noobs;
run;
```

```sas
*9-13;
data return;
  set learn.medical(keep=Patno,VisitDate);
  Return = intnx('month',VisitDate,6,'sameday');
  format VisitDate worddate;
run;

title "患者复诊";
proc print data=return noobs;
run;
```

## 第10 章答案

```sas
*10-1;
data subset_a;
  set learn.blood;
  where Gender = 'Female' and BloodType='AB';
  Combined = .001*WBC + RBC;

title "SUBSET_A 列表";
proc print data=subset_a noobs;
run;
```

```sas
data subset_b;
  set learn.blood;
  Combined = .001*WBC + RBC;
  if Gender = 'Female' and BloodType='AB' and Combined ge 14;
run;

title "SUBSET_B 列表";
proc print data=subset_b noobs;
run;
```

```sas
*10-3;
data lowmale lowfemale;
  set learn.blood;
  where Chol < 100 and not missing(Chol);
  /* alternative statement
  where Chol < 100 and missing(Chol)
  */
  if Gender = 'Female' then output lowfemale;
  else if Gender = 'Male' then output lowmale;
run;

title "LOWMALE 列表";
proc print data=lowmale noobs;
run;
```

```sas
title "LOWFEMALE 列表";
proc print data=lowfemale noobs;
run;
```

```sas
*10-5;
title "INVENTORY 列表";
proc print data=learn.inventory noobs;
run;
```

```sas
title "NEWPRODUCTS 列表";
proc print data=learn.newproducts noobs;
run;
```

```sas
data updated;
  set learn.inventory learn.newproducts;
run;

proc sort data=updated;
  by Model;
run;

title "updated 列表";
proc print data=updated;
run;
```

```sas
*10-7;
proc means data=learn.gym noprint;
  var fee;
  output=Meanfee(drop=type__freq_)
    Mean = / automone;
run;
```

```sas
data percent;
  set learn.gym;
  if _n = 1 then set Meanfee;
  FeePercent = round(100*fee / Fee_Mean);
  drop Fee_Mean;
run;

title "PERCENT 列表";
proc print data=percent;
run;
```

```sas
*10-9;
proc sort data=learn.inventory out=inventory;
  by Model;
run;
```

```sas
proc sort data=learn.purchase out=purchase;
  by Model;
run;
```

```sas
data pur_price;
  merge inventory
    purchase(in=InPurchase);
  by Model;
  if InPurchase;
    TotalPrice = Quantity*Price;
    format TotalPrice dollar$8.2;
run;

title "PUR_PRICE 列表";
proc print data=pur_price noobs;
run;
```

```sas
*10-11;
options mergegenob=nowarn;
data try1;
```

