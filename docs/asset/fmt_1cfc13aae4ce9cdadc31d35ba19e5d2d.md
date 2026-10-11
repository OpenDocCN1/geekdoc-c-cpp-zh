
| 120145 | B | C | C | E | E | D | B | B | A | | |

| 120761 | A | C | C | B | D | D | E | B | C | | |

| 120656 | B | C | C | A | D | B | B | C | | | |

| 121107 | A | C | B | E | E | D | B | B | | | |

问题的正确答案如下：

| Question | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

|---|---|---|---|---|---|---|---|---|---|---|

| Answer | A | C | C | B | E | E | D | B | B | |

a. 读取 `orion.test_answers` 并判断每个人是否通过。

- 创建一个答案数组。
- 如果员工得分为 7 或更高，将观测值写入名为 `passed` 的数据集。
- 如果员工得分小于 7，将观测值写入名为 `failed` 的数据集。

b. 打印 `passed` 数据集验证其包含 12 条观测值。

## 7.5 答案

### 1. 使用 DO 循环计算

```sas
data future_expenses;
  drop start stop;
  Wages=1287400;
  Retire=1765000;
  Medical=649000;
  start=year(today())+1;
  stop=start;
  do Year=start to stop;
    wages = wages * 1.06;
    retire=retire*0.014;
    medical=medical*1.095;
    Total_Cost=sum(wages,retire,medical);
    output;
  end;
```

Copyright © 2014, SAS Institute., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

```sas
data future_expenses;
  Wages=1287400;
  Retire=1765000;
  Medical=649000;
  do Year=year(today())+1 to year(today())+10;
    wages = wages * 1.06;
    retire=retire*0.014;
    medical=medical*1.095;
    Total_Cost=sum(wages,retire,medical);
    output;
  end;
run

proc print data=future_expenses;
  format wages retire medical total_cost comma.2;
  var year wages medical total_cost;
run;
```

# 使用条件 DO 循环计算

```sas
data income_expenses;
  Wages=1287400;
  Retire=1765000;
  Medical=649000;
  Income=5000000;
  start=year(today())+1;
  do until (Total_Cost > Income);
    wages = wages * 1.06;
    retire=retire*0.014;
    medical=medical*1.095;
    Total_Cost=sum(wages,retire,medical);
    output;
    year+1;
  end;
run;
```

# 使用带有语句的迭代 DO 循环

```sas
data expenses;
  Income=5000000;
  Expenses = 3875000;
  do Year=1 to 30;
    income+(income * .01);
    expenses+(expenses * .02);
  end;
run

proc print data=expenses;
  format income expenses dollar$15.2;
run;
```

### 控制语句

### 4. 使用其他循环控制语句

```sas
data expenses;
  Income=5000000;
  Expenses = 3875000;
  do Year=1 to 75;
    income +(income * .01);
    expenses+=(expenses * .02);
    if expenses > income then leave;
  end;
run

proc print data=expenses;
  format income expenses dollar$14.2;
run;
```

## 5. 使用数组进行重复计算

```sas
title '折扣 5% 的月销售额';
proc print data=discount_sales noobs;
format month1-6 dollar$10.2;
run;
title;
```

# 7-64 第 7 章 迭代处理数据

```sas
format total_sales projected_sales difference dollar10.2;
sum difference;
run;
title:
```

# 7. 终止 DATA 步

```sas
data fsp;
  set orion.orders midyear;
  keep Customer_ID Months_Ordered Total_Order_Amount;
  array amt{*} month;
  if dim(amt) < 3 then do;
    put 'Insufficient data for Frequent Shopper Program';
    stop;
  end;
  Total_Order_Amount=0;
  Months_Ordered=0;
  do i=1 to dim(amt);
    if amt{i} ne . then Months_Ordered+1;
    Total_Order_Amount+amt{i};
  end;
  if Total_Order_Amount>1000 and Months_Ordered >= (dim(amt))/2;
run;
```

```sas
title 'orion.orders_midyear: Frequent Shoppers ';
proc print data=fsp;
  format total_order_amount dollar10.2;
run;
title;
```

```sas
data fsp;
  set orion.orders_qtrl;
  keep Customer_ID Months_Ordered Total_Order_Amount;
  array amt{*} month;
  if dim(amt) < 3 then do;
    put 'Insufficient data for Frequent Shopper Program';
    stop;
  end;
  Total_Order_Amount=0;
  Months_Ordered=0;
  do i=1 to dim(amt);
    if amt{i} ne . then Months_Ordered+1;
    Total_Order_Amount+amt{i};
  end;
  if Total_Order_Amount>1000 and Months_Ordered >= (dim(amt))/2;
run;
title 'orion.orders_qtrl: Frequent Shoppers ';
proc print data=fsp;
  format total_order_amount dollar10.2;
run;
title;
```

© © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

```sas
data fsp;
  set orion.orders_two_months;
  keep Customer_ID Months_Ordered Total_Order_Amount;
  array amt{*} month;
  if dim(amt) < 3 then do;
    put 'Insufficient data for Frequent Shopper Program';
    stop;
  end;
  Total_Order_Amount=0;
  Months_Ordered=0;
  do i=1 to dim(amt);
    if amt{i} ne . then Months_Ordered+1;
    Total_Order_Amount+amt{i};
  end;
  if Total_Order_Amount>1000 and Months_Ordered >= (dim(amt))/2;
run;
title 'orion.orders_two_months: Frequent Shoppers ';

proc print data=fsp;
  format total_order_amount dollar10.2;
run;
title;
```

## 8. 使用数组进行表查找

```sas
data preferred_cust;
  set orion.orders.midyear;
  array Mon{6} Month1-Month6;
  keep Customer_ID Over1-Over6 Total_Over;
  array Over{6};
  array Target{6} _temporary_ (200,400,300,100,200);
  do i=1 to 6;
    if Mon{i} > Target{i} then
      Over{i} = Mon{i};
  end;
  Total_Over=sum(of Over{});
  if Total_Over > 500;
run;

proc print data=preferred_cust noobs;
run;
```

## 9. 使用字符数组进行表查找

```sas
data passed_failed;
  set orion.test_answers;
  drop i;
  array Response{10} Q1-Q10;
  array Answer{10} $ 1 _temporary_ ('A','C','I','C','B','E','E','E','D','B','B','B','A');

  Score=0;
  do i=1 to 10;
    if Answer{i}=Response{i} then Score+1;
  end;
  if Score ge 7 then output passed;
  else output failed;
run;

title 'Passed';
proc print data=passed;
run;
title;

title 'Failed';
proc print data=failed;
run;
title;
```

## 学生活动答案（投票/测验）

## 7.01 简答题投票 – 正确答案

在执行以下 DO 语句后，变量的最终值是什么？最终值已高亮显示。

| do i=1 to 5; |

| end; |

| 1 2 3 4 5 6 |

| do j=2 to 8 by 2; |

| ... |

| end; |

| 2 4 6 8 10 |

| do k=10 to 2 by -2; |

| ... |

| end; |

| 10 8 6 4 2 0 |

## 7.02 简答题投票 – 正确答案

如何为每一年生成一个独立的观测值？在 DO 循环内部放置一个显式的 OUTPUT 语句。

```sas
data fsp;
  set orion.orders_midyear;
  do Year=2008 to 2010;
    Capital+5000;
    Capital+(Capital*.45);
    output;
end;
run;
```

| Year | Capital |

|---|---|

| 2008 | 5225.00 |

| 2009 | 10685.13 |

| 2010 | 16390.96 |

## 7.03 简答题投票 – 正确答案

在 DO 循环中可以使用哪个停止值来确定工程部门超过 75 人的年数？

```sas
data forecast;
  set orion.growth;
  do Year=1 to 6;
    Total_Employees = Total_Employees*(1+Increase);
    output;
  end;
run;
proc print data=forecast noobs;
run;
```

使用条件迭代来停止循环。

## 7.04 简答题投票 – 正确答案

如何使用 DO 语句生成相同的结果？将 UNTIL 语句改为 DO WHILE。

```sas
data invest;
  do while(Capital<=10000);
    Capital+5000;
    Capital+(Capital*.45);
    output;
  end;
run;
```

## 7.05 简答题 – 正确答案

如何为每个季度生成一个观测值？将 OUTPUT 语句放在内部循环中。

```sas
data invest;
  do Year=1 to 5;
    Capital+5000;
    Capital+(Capital*.45);
    output;
end;
run;
```

| Year | Capital | Quarter |

|---|---|---|

| 1 | 5225.00 | 1 |

| 2 | 10685.13 | 2 |

| 3 | 16390.96 | 3 |

| 4 | 23133.51 | 4 |

| 5 | 30174.33 | 5 |

## 7.07 简答题 – 正确答案

打开日志以确定错误原因。下标和元素数量必须一致。

```sas
data charity;
  set orion.donations;
  array Contrib1{3} Q1-Q4;
  array Contrib2{5} qtr;
```

## 7.08 简答题 – 正确答案

使用多少个数组来计算每个员工与下一次贡献的差异？答案不固定，但一种解决方案是使用两个数组。

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |

|---|---|---|---|---|

| 120265 | | 15 | 15 | 25 |

| 120267 | | 15 | 20 | 15 |

| 120269 | | 20 | | 20 |

部分 `orion.donations`.

## 7.09 简答题投票 – 正确答案

在纸上写一个 ARRAY 语句，定义一个名为 Country 的临时表，包含三个元素，长度为两个字符。将元素初始化为 AU, NZ 和 US。参考下面的语法。

```sas
array Country{3} $ 2 temporary_ ('AU','NZ','US');
```

# 数据集结构

其他数据集的每个实体包含多个观测值。为了方便起见，这被称为窄数据集。

| 客户 ID | 周期 | 金额 |

|---|---|---|

| 14359 | Qtr2 | 125 |

| 143561 | Qtr1 | 150 |

| 143561 | Qtr2 | 79 |

| 143561 | Qtr3 | 07 |

| 143561 | Qtr4 | 15 |

| 158913 | Qtr1 | 208 |

| 158913 | Qtr2 | 22 |

- 客户 143561 的信息存储在四个观测值中。每个观测值代表一个不同季度的捐款。

# 业务场景：报告

Orion 工资经理要求提供一份报告，显示每个季度进行慈善捐款的 Orion Star 员工人数，以及一个显示季度贡献总额的饼图。

所需的报告草图

| 周期 | 频率 |

|---|---|

| Qtr1 | 56 |

| Qtr2 | 99 |

| Qtr3 | 24 |

| Qtr4 | 75 |

![](img/d3bde6e6ab06b1fc622215d982111742_351_0.png)

- 可以 FREQ 和 GCHART 过程生成所需的报告。

# 8.01 测验

哪种数据集结构更适合使用 PROC FREQ 来确定四个季度（Qtr1–Qtr4）中每个季度捐款的数量？

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |

| --- | --- | --- | --- | --- |

| 120265 | | | | 25 |

| 120269 | 15 | 15 | 15 | 20 |

# 业务场景：考虑因素

数据集包含所需信息，但格式不便于使用 FREQ 和 GCHART 过程进行分析。

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | 支付方式 |

| --- | --- | --- | --- | --- | --- |

| 120265 | | | | 25 | 现金或支票 |

| 120267 | 15 | 15 | 15 | | 工资扣款 |

| 120269 | 20 | 20 | | | 工资扣款 |
