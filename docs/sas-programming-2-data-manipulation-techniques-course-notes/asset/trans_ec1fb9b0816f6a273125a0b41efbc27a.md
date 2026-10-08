

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

# 学生活动答案（投票/测验）

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

部分 orion.donations.

## 7.09 简答题投票 – 正确答案

在纸上写一个 ARRAY 语句，定义一个名为 Country 的临时表，包含三个元素，长度为两个字符。将元素初始化为 AU, NZ 和 US。参考下面的语法。

```sas
array Country{3} $ 2 temporary_ ('AU','NZ','US');
```

