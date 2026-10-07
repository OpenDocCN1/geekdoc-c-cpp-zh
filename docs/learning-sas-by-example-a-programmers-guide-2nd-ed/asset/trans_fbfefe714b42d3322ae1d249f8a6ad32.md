

# 第 475 页奇数练习题解答

```sas
merge learn.inventory learn.purchase;
run;

title "Listing of TRY1";
proc print data=try1;
run;

options mergenoby=warn;
data try2;
merge learn.inventory learn.purchase;
run;

title "Listing of TRY2";
proc print data=try2;
run;

options mergenoby=error;
data try3;
merge learn.inventory learn.purchase;
run;

title "Listing of TRY3";
proc print data=try3;
run;
```

*10-13*
/* 将数值型标识符转换为字符型值的解决方案 */
proc sort data=learn.demographic_ID out=demographic_ID
by ID;
run;

data survey2;
set learn.survey2 (rename=(ID = NumID));
ID = put(NumID, z3.);
drop NumID;
run;

proc sort data=survey2;
by ID;
run;

data combine;
merge demographic_ID survey2;
by ID;
run;

title "Listing of COMBINE"
proc print data=combine noobs;
run;

/* 将字符型标识符转换为数值型值的解决方案 */
data demographic_ID;
set learn.demographic_ID(rename=(ID = CharID));
ID = input(CharID,z3.);
drop CharID;
run;

proc sort data=demographic_ID;
run;

proc sort data=learn.survey2 out=survey2;
by ID;
run;

data combine;
merge demographic_ID
survey2;
by ID;
run;

title "Listing of COMBINE";
proc print data=combine noobs;
run;
```

# 第 11 章解答

```sas
*11-1;
data health;
set learn.health;
BMI = (Weight/2.2) / (Height*.0254)**2;
BMIRound = round(BMI);
BMIRound2 = round(BMI,.1);
BMIGroup = round(BMI,5);
BMITunc = int (BMI);

title "Listing of HEALTH";
proc print data=health noobs;
run;

*11-3;
data miss_blood;
set learn.blood;
if (WBC) then call missing(Gender,RBC, Chol);

title "Listing of MISS_BLOOD";
proc print data=miss_blood noobs;
run;

*11-5;
data psychscore;
set learn.psych;
if n(of Score-5) ge 3 then
ScoreAve = mean(largest(1,of Score-5),
largest(2,of Score-5),
largest(3,of Score-5));
if n(of Ques-10) ge 7 then
QuesAve = mean(of Ques-10);
Composit = ScoreAve + 10*QuesAve;
keep ID ScoreAve QuesAve Composit;

title "Listing of PSYCHSCORE";
proc print data=psychscore noobs;
run;

*11-7;
data _null_;
x = 10; y = 20; z = -30;
AbsZ = abs(z);
ExpX = round(exp(x),.001);
Circumference = round(2*constant('pi')*y,.001);
put _all_;
run;

*11-9;
data fake;
do Subj = 1 to 100;
  if rand('uniform') le .4 then Gender = 'Female';
  else Gender = 'Male';
  Age = 9 + ceil(rand('uniform')*51);
  output;
end;
run;
title "Frequencies";
proc freq freq data=fake;
tables Gender / nocum;
run;
title "First 10 Observations of FAKE";
proc print data=fake(obs=10);
run;

*11-11;
data convert;
set learn.char_num(rename=
(Age = Char_Age
Weight = Char_Weight
SS = Num_SS));
Age = input(Char_Age,8);
Weight = input(Char_Weight,8);
SS = put(Num_SS,ssn1);
Zip = put(Num_Zip,z5);
drop Char_:Num_;
run;
title "Listing of CONVERT";
proc print data=convert noobs;
run;

*11-13;
data smooth;
set learn.stocks;
Price1 = lag(Price);
Price2 = lag2(Price);
Average = mean(Price, Price1, Price2);
run;
title "Plot of Price and Moving Average";
proc sgplot data=smooth;
series x=Date y=Price;
series x=Date y=Average;
run;
```

# 478 页《SAS 实例教程：程序员指南》，第二版

# 第 12 章解答

```sas
*12-1;
* 测试存储长度的一种方法是使用 LENGTH 函数，
 * 它返回存储长度，可以与返回字符字符串长度的 LENGTH 函数
 *（不计算末尾空格）进行比较；
data storage;
length A 5 B 4;
Name = 'Goldstein';
andB = A || B;
Cat = cats(A,B);
if Name = 'Smith' then Match = 'No';
else Match = 'Yes';
Substring = substr(Name,5,2);
L_A = length(A);
L_B = length(B);
L_Name = length(Name);
L_AandB = length(andB);
L_Cat = length(Cat);
L_Match = length(Match);
L_Substring = length(Substring);

title "Lengths of Character Variables";
proc print data=storage noobs;
var L_:;

| 变量 | 长度 |
| :--- | :--- |
| A | 5 |
| B | 4 |
| Name | 9 |
| AandB | 8 |
| Cat | 20 |
| Match | 2 |
| Substring | 9 |

*12-3;
data names_and_more;
set learn.names_and_more;
Name = compbl(Name);
Phone = compress(Phone,'kd');
run;
title "Listing of NAMES_AND_MORE";
proc print data=names_and_more noobs;

*12-5;
data convert_ID;
set learn.dem_ID(rename=(ID = CharID));
ID = input(CharID,z3.);
drop CharID;
run;

proc sort data=demographic_ID;
run;

proc sort data=learn.survey2 out=survey2;
by ID;
run;

data combine;

 demographic_ID
survey2;
by ID;
run;

title "Listing of COMBINE";
proc print data=combine noobs;
run;
```

