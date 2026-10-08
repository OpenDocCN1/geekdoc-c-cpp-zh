

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

使用 SAS 变量列表和 SUM 函数将 Year1、Year2、Year3 和 Year4 的值相加，完成 Total 的赋值语句。

| PDV | | | | | |
|---|---|---|---|---|
| Year2 | Year1 | Year3 | Year4 | 销售额 |

| | Total=sum(of Year1-Year4); |
| | Total=sum(of Year2--Year4); |
| | Total=sum(of Year:); |

### 5.03 多选题调查 – 正确答案

哪个 SUBSTR 函数可以从 Item_Code 值的中间提取五个数字？

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
`Name = propcase(Name, ' *');`
```

PROPCASE 函数的第二个参数必须列出所有用作分隔符的字符。在这个例中，空格和 * 都需要列出。

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

运行修正后的程序后，shoes 数据集有八个观测值和五个变量。

### 5.06 简答调查 – 正确答案

| PDV | Phrase | 第二 |
| --- | --- |
| $ 28 | 200 |
| software, hardware | hardware |

![](img/d3bde6ab061fc622215d982111742259)

如如下所示，在分隔符列表中添加空格以提取 Phrase 的第二个单词。

```sas
Second=scan(Phrase, 2, ' ');
```

### 5.07 多选题调查 – 正确答案

哪个表达式可以正确从 Text 变量中提取 2007？

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

PDV 中 Pos3 和 Pos4 的值是多少？

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

给定相同的参数，INT 和 FLOOR 函数返回相同的结果吗？

- 是
- 否

### 5.10 多选题调查 – 正确答案

Ord1、Ord2 和 Ord3 包含三个订单的金额。以下哪个可以计算两个最大订单的总和？

- a. sum(max(Ord1,Ord2))
- b. sum(Ord1)-min(Ord3)
- c. max(Ord1,Ord2)+max(Ord2,Ord3)
- d. 都不是。

### 5.11 简答调查 – 正确答案

在 DATA 步中填充缺失的表达式。该表达式应通过 SharePrice 乘以 MyShares 来计算 TotalValue。

```sas
data Input;
SharePrice=$130.25;
MyShares=125;
TotalValue=...;
run;
```

