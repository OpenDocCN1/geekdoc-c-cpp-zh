
## 第 27 章：引入 Perl 正则表达式 461

# 程序 27.6：重写程序 27.5 以演示一个由强迫症程序员编写程序

title "使用正则表达式检查社会安全号码";
title2 "结合 PRXPARSE 和 PRXMATCH 函数";

```sas
data _null_;
  file print;
  input SS $11;

  retain Return_Code;
  if n = 1 then
    Return_Code = prxparse("/\d\d-\d\d-\d\d\d\d/");

  if not prxmatch(Return_Code, SS) then
    put "Error for SS Number " SS;
datalines;
123-45-6789
123456789
123-ab-9876
999-888-7777
;
```

由于你只执行一次 `PRXPARSE` 函数，因此你需要一个 `RETAIN` 语句，以便变量 `Return_Code` 在 DATA 步的下一次迭代中不会被设置为缺失（Missing）。

希望你会发现，当你需要验证模式而不是字符的精确匹配时，正则表达式是极其な。你可以使用 Google 搜索几乎任何术语或短语的正则表达式。请注意，某些结果可能是错误的或过于复杂的。作者推荐的一个网站是 www.stackoverflow.com。

## 27.7 习题

奇数题的解答位于书末尾。所有题目的解答均供教授参考。如果你是教授，请访问书籍的配套网站 support.sas.com/cody，获取如何获得所有题目解答的信息。

- 1. 你有一份车牌号列表，想要提取任何不符合“三个大写字母后跟三个数字”格式的数字部分。请使用此数字列表测试你的程序：
**注意：** SASMAN 是我的德克萨斯州车牌号，SASJEDI 属于我的朋友 Mark Jordan。

ABC123
SASMAN
SASJEDI
345XYZ
1ow987
WWW999

- 2. 使用程序 27.3 中的电话号码，但假设你希望号码格式为 ddd.ddd.dddd，其中 d 是任何数字。请注意，点（.）在正则表达式中是一个特殊字符。它是代表任何字符的通配符。因此，在编写表达式时，必须在点之前加一个反斜杠。

- 3. 结合 PRXPARSE 和 PRXMATCH 重复习题 2。

## 奇数题解答

此 SAS 文件包含《实例学习 SAS：程序员指南》（Learning SAS by Example: A Programmer’s Guide）书中所有奇数题的解答。

你需要修改任何 `libname` 和 `infile` 语句，使其指向你计算机上相应的文件夹。转换文件中所有 `libname` 和 `infile` 语句的最简单方法是找到字符串：

```
c:\books\learning
```

并将其替换为你存放 SAS 数据集和文本文件的文件夹。如果你将 SAS 数据集和文本文件存储在不同的地方，你需要分别搜索 `libname` 和 `infile`。

```sas
libname learn 'c:\books\learning';
options fmt=(learn);
```

## 第 2 章解答

- 1-1;
/* 无效的变量名为：
Wt-Kg (包含连字符)
76Trombones (以连字符开头)
/

- 1-3;
/* 变量数量为 5
观测值数量为 10
/

- 1-5;
/* 数值的默认长度为 8 */ /

## 第 2 章解答

- 2-1;

```sas
Program name: stocks.sas in c:\books\learning
Purpose: 读取股票价格的原始数据并
计算值
Programmer: Ron Cody
Date: 2006年6月23日
```

```sas
*a;
data portfolio;
  infile 'c:\books\learning\stocks.txt';
  input Symbol $ Price Number;
  Value = Number*Price;
```

```sas
title "Listing of Portfolio"
proc print data=portfolio noobs;
run;
```

![](img/e9e15d853989558188e1c83b0ae655b0_468_0.png)

## 464 实例学习 SAS：程序员指南，第二版

```sas
*b;
title "Means and Sums of Portfolio Variables";
proc means data=portfolio n mean sum maxdec=0;
var Price Number;

```sas
run;
```

*2-3;
/*
EMF = 1.45*V + (R/E)*v**3 - 125;
*/
```

```sas
*2-5;
/*需要 $ Gender*/
data XYZ;
  infile 'c:\books\learning\XYZ.txt';
  input Gender $ X Y Z;
  Sum = X + y + Z;
datalines;
Male 1 2 3
Female 4 5 6
Male 7 8 9
run;
```

## 第 3 章解答

```sas
*3-1;
*= c;
data scores;
  infile 'c:\books\learning\scores.txt';
  input Gender : $;
  English
  History
  Math
  Science;
  Average = (English + History + Math + Science) / 4;
run;
```

```sas
title "Listing of SCORES";
proc print data=scores noobobs;
run;
```

```sas
*3-3;
data company;
  infile 'c:\books\learning\company.txt' dsd dlm='$';
  input LastName $ EmpNo $ Salary;
  format Salary dollar10.; /*可选语句 */
run;
```

```sas
title "Listing of COMPANY";
proc print data=company noobobs;
run;
```

```sas
*3-5
testdata;
data;
  input X Y;
  Z = 100 + 50*X + 2*X**2 - 25*Y + Y**2;
datalines;
1 2
3 5
5 9
9 11
```

```sas
title "Listing of TESTDATA";
proc print data=testdata noobs;
run;
```

```sas
*3-7;
data scores;
  infile 'c:\books\learning\scores.txt';
  input Gender : $;
  English
  History

Math
  Science;
  Average = (English + History + Math + Science) / 4;
run;
```

```sas
title "Listing of SCORES";
proc print data=scores noobobs;
run;
```

```sas
*2-5;
data XYZ;
  infile 'c:\books\learning\XYZ.txt';
  input Gender $ X Y Z;
  Sum = X + y + Z;
datalines;
Male 1 2 3
Female 4 5 6
Male 7 8 9
run;
```
