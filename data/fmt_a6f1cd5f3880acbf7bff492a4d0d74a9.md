
`run;`

title "Listing of BLOODPRESSURE";

`proc print data=bloodpressure noobs;`

`run;`

*22-5;

`proc format;`

value `$convert`

0 - 65 = 'F'

66 - 75 = 'C'

76 - 85 = 'B'

86 - high = 'A'

other = ' ';

`run;`

data `lettergrades`;

infile `'c:\books\learning\numgrades.txt'`;

input `ID $ Lettergrade $convert. @@`;

`run;`

title "Listing of LETTERGRADES";

`proc print data=lettergrades noobs;`

`run;`

*22-7;

data `control`;

set `learn.dxcodes` (rename=(Dx = Start Description = Label));

retain6='$dxcodes' Type 'C';

`run;`

`proc format cntlin=control;`

select `$dxcodes`;

`run;`

*22-9;

`proc format;`

value `muggle`

'01jan1990'd - '31dec2004'd = 'Too Early'

'01jan2005'd - '31dec2005'd = [mmddy10]

'01jan2007'd - high = 'Too Late';

`run;`

title "Listing of GYM";

`proc print data=learn.gym noobs;`

format `Date muggle`;

`run;`

# 第 23 章答案

*23-1;

```
data long;
set learn.wide;
array X_array[5] X1-X5;
array Y_array[5] Y1-Y5;
do Time = 1 to 5;
X = X_array[Time];
Y = Y_array[Time];
output;
end;
keep Subj Time X Y;
run;
```

title "Listing of LONG";

`proc print data=long;`

`run;`

*23-3;

```
proc transpose data=learn.wide
out=long(rename=(coll=X)
drop=_name_name);
by Subj;
var X1-X5;
run;
```

title "Listing of LONG";

`proc print data=long;`

`run;`

# 第 24 章答案

*24-1;

```
proc sort data=learn.dailyprices out=dailyprices;
by Symbol Date;
run;

data lastprice;
set dailyprices;
by Symbol;
if last.Symbol;
run;
```

title "Listing of LASTPRICE";

`proc print data=lastprice noobs;`

`run;`

*24-3;

```
proc sort data=learn.dailyprices out=dailyprices;
by Symbol Date;
data count;
set dailyprices;
by Symbol;
if first.Symbol then N_Days = 0;
N_Days += 1;
if last.Symbol;
keep Symbol N_Days;
run;
```

title "Listing of COUNTIT";

`proc print data=count noobs;`

`run;`

*24-5;

```
proc sort data=learn.dailyprices out=dailyprices;
by Symbol Date;
run;

data first_last;
set dailyprices;
by Symbol;
retain FirstPrice;
if first Symbol and last.Symbol then delete;
if Symbol then FirstPrice = Price;
if last.Symbol then do;
  Diff = Price - FirstPrice;
  output;
end;
keep Symbol Price Diff;
```

title "Listing of FIRST_LAST";

`proc print data=first_last noobs;`

`run;`

*24.7;

```
proc sort data=learn.dailyprices out=dailyprices
by Symbol Date;
run;

data first_last;
set dailyprices;
by Symbol;
if first.Symbol and last.Symbol then delete;
Diff = dif(Price);
if not first.Symbol then output;
keep Symbol Price Diff;
```

title "Listing of FIRST_LAST";

`proc print data=first_last noobs;`

`run;`

# 第 25 章答案

*25-1;

title "Listing produced on &sysday, &sysdate9 at &systime";

`proc print data=learn.stocks(obs=5) noobs;`

`run;`

*25-3;

```
%macro print_n(dsn, /* data set name */
nobs /* * number of observations to list */
nobs /* * number of observations to list */);
ntitle "Listing of the first &nobs Observations from
"Data set &dsn";
proc print data=&dsn(obs=&nobs) noobs;
run;
%mend print_n;
%print_n(learn.bicycles, 4)
```

*25-5;

```
proc means data=learn.fitness noprint;
var TimeMile MaxPulse;
output out=summary;
data _null;
set summary;
call symput('GrandTime',TimeMile_mean);
call symput('GrandRest',RestPulse_mean);
call symput('GrandMax',MaxPulse_mean);
run;

data compute_percents;
set learn.fitness;
P_TimeMile = round(100*TimeMile/GrandTime);
P_RestPulse = round(100*RestPulse/GrandRest);
P_MaxPulse = round(100*MaxPulse/GrandMax);
run;
```

title "Fitness Stats as Percent";

`proc print data=compute_percents noobs;`

`run;`

# 第 26 章答案

*26-1;

ntitle "Observations from INVENTORY where Price > 20";

`proc sql;`

select *

from `learn.inventory`

where `Price > 20`;

quit;

*26-3;

`proc sql;`

create table `n_sales` as

select `Name`, `TotalSales`

from `learn.sales`

where `Region eq 'North'`;

quit;

*26-5;

`proc sql;`

create table `both` as

select `l.Subj` as `LeftSubj`,

`Height`,

`Weight`,

`r.Subj` as `RightSubj`,

`Salary`

from `learn.left` as `l` join `learn.right` as `r`

where `l.Subj = r.Subj`;

title "Listing of BOTH";

`proc print data=both noobs;`

`run;`

/* alternate code

`proc sql;`

create table `both` as

select `l.Subj` as `LeftSubj`,

`Height`,

`Weight`,

`r.Subj` as `RightSubj`,

`Salary`

from `learn.left` as `l` join `learn.right` as `r`

where `l.Subj = r.Subj`;

quit;

title "Listing of BOTH";

`proc print data=both noobs;`

`run;`

Part 3;

`proc sql;`

create table `both` as

select `l.Subj` as `LeftSubj`,

`Height`,

`Weight`,

`r.Subj` as `RightSubj`,

`Salary`

from `learn.left` as `l` join `learn.right` as `r`

where `l.Subj = r.Subj`;

quit;

title "Listing of LEFT";

`proc print data=both noobs;`

`run;`

Part 2;

`proc sql;`

create table `both` as

select `l.Subj` as `LeftSubj`,

`Height`,

`Weight`,

`r.Subj` as `RightSubj`,

`Salary`

from `learn.left` as `l` join `learn.right` as `r`

where `l.Subj = r.Subj`;

quit;

title "Listing of BOTH";

`proc print data=both noobs;`

`run;`

*26-7;

`proc sql;`

create table `third` as

select *

from `learn.first`;

quit;

title "Listing of THIRD";

`proc print data=third;`

`run;`

*26-9;

`proc sql;`

create table `percentages` as

select `Subject`,

`RBC`,

mean(`RBC`) as `MeanRBC`,

mean(`WBC`) as `MeanWBC`,

100*`RBC` as `Percent_RBC`,

100*`WBC` as `Percent_WBC`

from `learn.blood(obs=10)`;

quit;

title "Listing of PERCENTAGES";

`proc print data=percentages;`

`run;`

# 第 27 章答案

*27-1;

title "List of Non-standard Numbers";

file print;

input `Plate_No $10.`

if not match(`Plate_No`, "[A-Z]\d\d") then

put "Plate number does not conform";

*27-3;

title "List of Non-standard Numbers";

file print;

retain Return;

if `_n_ = 1` then `Return = match("[A-Z]\d\d.\d\d.\d\d/", Plate_No)`

put "Plate number does not conform";

# Index

- `ABS function` 167–168

- absolute column pointers 374

- `ACROSS variables` 254–255

- advanced `INPUT techniques` 359

- creating multiple observations 372–373

- handling missing values 360–361

- informat lists 373–374

- reading data conditionally 369–371

- reading data from multiple files using `FILENAME` 366

- reading external filenames from data files 366–367

- reading multiple lines of data 367–369

- reading portions of data 362–363

- trailing 373

- using relative pointers 374

- variable lists 373–376

- alignment list 133

- B Boolean logic 93

- bounds, array 210

- box plots

  - generating simple 347–348

  - generating with grouping variables 348–349

- breaks, report 248–251

- `BREAK statement` 248–251

- `BY SUBJECT statement` 142, 145–147, 151–152, 230–233, 263–264, 266, 269–270, 415

- C `CALL SORTN` 177–179

- `CARDS statement` 30

- `CATALOG procedure` 380

- `CAT function` 184–185

- `CATS function` 184–185, 399, 400, 459

- `CATX function` 184–185

- `CEIL function` 161–162, 172

- `CENTER option` 242

- character data, reading 382–384

- character functions

  - about 181

  - changing case of characters 182–183

  - data cleaning with NOT functions 193–194

  - dividing strings into words 196–197

  - extracting parts of strings 194–195

  - joining strings 184–185

  - performing matches 197–198

- D bar charts 337–340

# 498 索引

- 练习 201–204

- 从字符串中删除字符 183–184, 186–188

- 删除前导/尾空格 185–186

- 搜索字符类 192–193

- 搜索单个字符 190–191

- 替换字符串或单词 199–201

- 搜索字符 189–190

- 在字符串中搜索单词 191–192

- 字符值，确定长度 182

- 拼接 (concatenation)

  - 数据集 140

  - 拼接运算符 (`|| ||!!`) 184

- 条件处理

  - 关于 87

  - 布尔逻辑 93–94

  - ELSE If 语句 87–90

  - IF 语句 87–90

  - 多个 OR 运算符 94–95

  - NOT 运算符 93–94

  - AND 运算符 93–94

  - IN 运算符 91–92

- `CHART 过程` 337–340

- 图表和图形

  - 关于 337

  - 在图中添加置信限限 342–343

  - 在图中添加回归线 337–340

  - 创建条形

  - 使用分组变量创建箱线 348–349

  - 创建直方图 346–347

  - 创建散点图 341–342

  - 创建简单箱 347–348

  - 创建平滑曲线 345–346

  - 创建时间序列图 343–344

  - 显示响应变量的统计数据 340–341

  - 重叠 339–350

- OR 运算符 93–94

  - 练习 96–97

  - IF 语句子集 90–91

  - 使用 SELECT 进行逻辑测试 92–93

  - WHERE 运算符 96

  - WHERE 语句 95

- 置信限限，添加到图中 342–343

- `CONSTANT 函数` 168

- 计算 168

  - 日期 125–126

  - `CONTENTS 过程` 45–48, 51, 64–66, 75, 80, 83, 126–127, 143–341

  - `CONTINUE 语句` 116–117, 405

  - CSV 文件，读取由分隔符分隔的数据值 27–28

- 大括号 `{{}}` 206

- 自定义报告

- `CHARTYPE 过程` 272–273, 274, 276

- `CLASS 语句` 60, 264–266, 275–300, 301, 306–307, 316, 396–397

  见报告

- CLI 选项 342–343

# data

- CLM 选项 342–343

- CNTL–option, FORMAT 过程 386–390, 387–388, 392
