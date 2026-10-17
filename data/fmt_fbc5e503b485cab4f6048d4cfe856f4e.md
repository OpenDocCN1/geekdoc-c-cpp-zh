
# 转换 HR 数据：完整程序

`PROC PRINT` Output

| EmpID | Pay | Bonus | Phone | HireDate |
|---|---|---|---|--|
| 1036 | 52000 | 5200 | (303) 393-0956 | 04/13/2008 |
| 11048 | 32000 | 3200 | (919) 770-8292 | 08/25/2010 |
| 11052 | 49000 | 4900 | (301) 449-5239 | 06/08/2009 |

### 练习

如果你自上一次练习以来重新启动了 SAS 会话，请打开并提交数据文件夹中的 `libname.sas` 程序。

## Level 1

### 10. 使用 PUT 和 INPUT 函数

数据集 `orion.shipped` 包含了 2007 年运往 Orion Star 某零售网店的产品的详细信息。

部分 `orion.shipped`

| Product_ID | Ship_Date | Quantity | Price |
|---|---|---|--|
| 24080200021 | 05JAN2011 | 2 | $42.45 |
| 24080200035 | 04JAN2011 | 6 | $12.15 |
| 24020112225 | 04JAN2011 | 2 | $77.65 |
| 21020500002 | 09JAN2011 | 3 | $5.70 |

`PROC CONTENTS` Output for `orion.shipped`

| Variable | Type | Len | Format |
|---|---|---|---|
| 1 | Product_ID | Num | 8 | |
| 2 | Ship_Date | Num | 8 | DATE9. |
| 3 | Quantity | Num | 8 | |
| 4 | Price | Char | 7 | |

## 5.5 转换变量类型 5-77

Orion Star 的一名分析师编写了一个 SAS 程序来计算出货物品的总价格，并创建一个包含发货日的注释。遗憾的是，该 SAS 程序得出了意之外的结果。

a. 打开并提交程序 `p205e10.sas`。

b. 查看意外的结果。

部分 `PROC PRINT` Output（共 148 条观测值）

| Product_ID | Ship_Date | Quantity | Price | Comment | Total |
|---|---|---|---|---|---|
| 24080200021 | 05JAN2011 | 2 | $42.45 | Shipped on 18632 | . |
| 24080200035 | 04JAN2011 | 6 | $12.15 | Shipped on 18631 | . |
| 24020100225 | 04JAN2011 | 2 | $77.85 | Shipped on 18631 | . |
| 21020500002 | 09JAN2011 | 3 | $5.70 | Shipped on 18638 | . |

c. 修改程序以获得预期的结果。

部分 `PROC PRINT` Output

| Product_ID | Ship_Date | Quantity | Price | Comment | Total |
|---|---|---|---|---|---|
| 24080200021 | 05JAN2011 | 2 | $42.45 | Shipped on 01/05/2011 | $84.90 |
| 24080200035 | 04JAN2011 | 6 | $12.15 | Shipped on 01/04/2011 | $72.90 |
| 24020100225 | 04JAN2011 | 2 | $77.85 | Shipped on 01/04/2011 | $155.70 |
| 21020500002 | 09JAN2011 | 3 | $5.70 | Shipped on 01/09/2011 | $17.10 |

- 查看 `orion.ship` 的 `PROC CONTENTS` 输出。
- 注意到 `Ship_Date` 是数值型，并分配了永久的 `DATE9.` 格式。它需要使用 `MMDDYY10` 格式转换为字符值。
- 注意到 `Price` 是字符型。它需要使用 `COMMA7.` 或 `DOLLAR*` 转换为数值。
- 使用函数转换 `Ship_Date` 和 `Price` 的值以获得所需的结果。

## Level 2

### 11. 更改变量的数据类型

数据集 `orion_newhire` 包含了新员工的信息。

`orion_newhire` 的部分 `PROC CONTENTS` 输出

| ID | Telephone | Birthday |
|---|---|---|
| 120-012-40-4928 | 5467883 | 05DEC1972 |
| 120-012-83-3816 | 6688321 | 03MAY1969 |
| 120-341-44-0781 | 9418123 | 23NOV1976 |
| 120-423-01-7721 | 7839191 | 28JUN1971 |

按创建顺序排列的变量

| # | Variable Type Len |
|---|---|---|
| 1 ID | Char | 15 |
| 2 Telephone | Num | 8 |
| 3 Birthday | Char | 9 |

Copyright ©2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

## 5-78 第 5 章 数据转换

- a. 从 `orion.US_newhire` 创建一个新的数据集。
- 将新数据集命名为 `US_converted`。
- 移除 `ID` 中的连字符。
- 将 `ID` 转换为数值。
- 将 `Telephone` 转换为字符，并在第三和第四位数字之间插入连字符。
- 将 `Birthday` 转换为 SAS 日期。
- b. 使用适当标题打印 `US_converted` 集，并使用 `PROC CONTENTS` 检查类型。

部分 `US_converted`（共 14 条观测值）

| ID | Telephone | Birthday |
|---|---|---|
| 120-012-40-4928 | 5467883 | 05DEC1972 |
| 120-012-83-3816 | 6688321 | 03MAY1969 |
| 120-341-44-0781 | 9418123 | 23NOV1976 |
| 120-423-01-7721 | 7839191 | 28JUN1971 |

部分 `CONTENTS` 输出

| Variable | Type | Len |
|---|---|---|
| 1 ID | Char | 15 |
| 2 Telephone | Num | 8 |
| 3 Birthday | Char | 9 |

## 5-82 第 5 章 数据转换

```sas
title 'Charity Contributions for each Employee';
proc print data=work.split noobs;
var Employee_ID Charity;
run;
title;
```

### 7. 在输入缓冲区使用字符函数
```sas
data work.supplier;
length Supplier_ID $ 5 Supplier Name $ 30 Country $ 2;
infile 'supplier.dat';
input Supplier_ID $
Country=scan(INFILE, -1, ' ');
StartCol=find(INFILE, ' ');
EndCol=length(INFILE)-3;
/* 在第一个和最后一个空格之间的所有内容都是
供应商名称。 */
Supplier_Name=substr(INFILE,StartCol+1,EndCol-StartCol);
/* 知道最后一个空格的位置后，
也可以使用 SUBSTR 创建 Country。 */
drop StartCol EndCol;
run;
title 'Supplier Information';
proc print data=work.supplier noobs;
run;
title;
```

### 8. 计算统计数据与四舍五入
```sas
data work.stats;
set orion.orders midyear;
MonthAvg=round(mean(of month1-month6));
MonthMax=max(of month1-month6);
MonthSum=sum(of month1-month6);
run;
title '客户下订单月份的统计';
proc print data=work.stats noobs;
var Customer_ID MonthAvg Max MonthSum;
run;
title;
```

### 9. 计算缺失值、中位数和最大值的统计数据
```sas
data work.customers;
set orion.orders midyear;
if n(of month1-month6) >= 5;
/* 替代方案：if nmiss(of month1-month6) <= 1; */
Month Median=median(of month1-month6);
Month Highest=largest(1,of month1-month6);
Month_2ndHighest=largest(2,of month1-month6);
run;
```

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

```sas
title 'Month Statistics on Frequent Customers';
proc print data=work.freqcustomers noobs;
run;
title;
```

```sas
data shipping_notes;
set orion.shipped;
length Comment $ 21;
Comment=cat('Shipped on ',put(Ship_Date,mmddyy10.0));
Total=Quantity * input(Price,comma7);
run;
proc print data=shipping_notes noobs;
format Total dollar7.2;
run;
```

## 11. 更改变量的数据类型

```sas
data US_converted (drop=cid nTelephone cBirthday);
set orion.US newhire
(rename=(ID=CID nTelephone=Telephone Birthday=cBirthday));
ID=input(compress(CID,'-'),15.);
length Telephone $ 8;
Telephone=cat(substr(put(nTelephone,7.),1,3),
-'substr(put(nTelephone,7.),4));
Birthday =input(cBirthday,date9.);
run;
```

```sas
title 'US New Hires'
proc print data=US_converted noobs;
run;
title;
```

```sas
proc contents data=US_converted varnum;
run;
```

## 学生活动解答（调查/测验）

### 5.02 简答调查 – 正确答案

使用 SAS 变量列表和 `SUM` 函数将 `Year1`、`Year2`、`Year3` 和 `Year4` 的值相加，完成 `Total` 的赋值语句。

| PDV | | | | | |
|---|---|---|---|---|---|
| Year2 | Year1 | Year3 | Year4 | 销售额 |

| | Total=sum(of Year1-Year4); |
| | Total=sum(of Year2--Year4); |
| | Total=sum(of Year:); |

### 5.03 多选题调查 – 正确答案

哪个 `SUBSTR` 函数可以从 `Item_Code` 值的中间提取五个数字？

| PDV |
| Item_Code |
| --- |
| $ 20 |
| 978-1-59994-397-8 |

- a. substr(Item_Code,5,7)
- b. substr(Item_Code,5)
- c. substr(Item_Code,7,5)
- d. substr(Item_Code,'mid',5)

### 5.04 简答调查 – 正确答案

此 PDV 显示了 **Name:** 的当前值：

| Name |
| HEATH*BARR*LITTLE EQUIPMENT SALES |

写一个赋值语句，将 **Name** 转换为如下格式：

| Name |
| Heath*Barr*Little Equipment Sales |

```sas
Name = propcase(Name, ' *');
```

`PROPCASE` 函数的第二个参数必须列出所有用作分隔符的字符。在这个例中，空格和 * 都需要列出。

### 5.05 简答调查 – 正确答案

括号位置放置错误是函数中最常见的语法错误之一。

修正后的 `p205a01.sas`

```sas
data shoes;
  set orion.product_list;
  if substr(right(Product_Name),33,13) =
    'Running Shoes';
run;
```

![](img/d3bde6ab061fc622215d82111742258)

运行修正后的程序后，`shoes` 数据集有八个观测值和五个变量。

### 5.06 简答调查 – 正确答案

| PDV | Phrase | 第二 |
| --- | --- |
| $ 28 | 200 |
| software, hardware | hardware |

![](img/d3bde6ab061fc622215d982111742259)

如如下所示，在分隔符列表中添加空格以提取 `Phrase` 的第二个单词。

```sas
Second=scan(Phrase, 2, ' ');
```

### 5.07 多选题调查 – 正确答案

哪个表达式可以正确从 `Text` 变量中提取 2007？

```sas
data Scan;
Text="New Year's Day, January 2007";
run;
```

- a. scan(Text,1);
- b. scan(Text,6);
- c. scan(Text,6, ');
- d. 以上都是。

### 5.08 简答调查 – 正确答案

PDV 中 `Pos3` 和 `Pos4` 的值是多少？

```sas
data find;
Text='AUSTRALIA, DENMARK, US';
Pos1=find(Text,'A');
Pos2=find(Text,'D');
Pos3=find(Text,'U');
Pos4=find(Text,'I');
run;
```

| Pos1 | Pos2 | Pos3 | Pos4 |
|---|---|---|---|
| 8 | 2 | 8 | 0 |

### 5.09 调查 – 正确答案

给定相同的参数，`INT` 和 `FLOOR` 函数返回相同的结果吗？

- 是
- 否

### 5.10 多选题调查 – 正确答案

`Ord1`、`Ord2` 和 `Ord3` 包含三个订单的金额。以下哪个可以计算两个最大订单的总和？

- a. sum(max(Ord1,Ord2))
- b. sum(Ord1)-min(Ord3)
- c. max(Ord1,Ord2)+max(Ord2,Ord3)
- d. 都不是。

### 5.11 简答调查 – 正确答案

在 `DATA` 步中填充缺失的表达式。该表达式应通过 `SharePrice` 乘以 `MyShares` 来计算 `TotalValue`。

```sas
data Input;
SharePrice=$130.25;
MyShares=125;
TotalValue=...;
run;
```

# 逻辑错误

当程序语句遵循规则并执行，但结果不正确时，就会发生逻辑错误。
日志中不会写入任何备注，因此逻辑错误很难检测。

![](img/d3bde6e6ab06b1fc622215d982111742_267_0.png)

本节重点关注如何识别逻辑错误。

# 程序与部分输出

```sas
data us mailing;
set orion.mailing_list;
drop Address3;
length City $ 25 State $ 2 Zip $ 5;
if find(catx(' ', Name,catx(' ', 'US')),
scan(Name,2,','),
scan(Name,1,','));
City=scan(Address3,1,',');
State=scan(address3,2,',');
Zip=scan(Address3,3,',');
```
