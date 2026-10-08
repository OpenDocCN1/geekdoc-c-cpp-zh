

# 7-42 第 7 章 迭代处理数据

**部分 orion.orders_midyear 数据**

| Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|
| 5 | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 10 | 188.10 | 414.09 | 2876.9 | 3164.59 | 2373.44 | 169.29 |
| 11 | 78.20 | | | | | 70.38 |
| 12 | 135.60 | | 117.6 | 129.36 | 97.02 | 122.04 |
| | | | 29.4 | 32.34 | | |

- 创建一个数据集 *special_offer*，包含第 1 到 3 月的 10% 折扣。
- 创建一个数组 *Mon*，用于访问 *Month1* 到 *Month3*。
- 使用 DO 循环调整每个客户的每月数据，包含 10% 的折扣（仅限 Month1 到 Month3）。
- 创建新变量：
- *Total_Sales* – 六个月内当前销售额的总和
- *Projected_Sales* – 六个月调整后销售额的总和（包括三个月的折扣后金额）
- *Difference* – *Total_Sales* 与 *Projected_Sales* 之间的差
- 仅保留新变量：

- b. 打印生成的数据集并验证你的结果。
- 隐藏会日期、页码和观测值列。
- 添加一个合适的标题。
- 使用 SUM 语句显示 **Difference** 变量的总和。
- 对所有变量使用 DOLLAR. 格式。

前三个月包含 10% 折扣的部分 PROC PRINT 输出

```
Total Sales
Total_Sales      Projected_Sales Difference
$1,803.04        $1,733.93      $69.11
$9,186.41        $8,838.50      $347.91
$148.58           $140.76        $7.82
$601.62           $576.30        $25.32
                               
$1,518.95        $1,467.02      $51.93
=================
$1,550.74
```

# 挑战

## 7. 终止 DATA 步骤
上半年的订单数据存储在 *orion.orders_midyear* 数据集中。该数据集每月更新，可能包含 1 到 12 个月的数据。

部分 **orion.orders_midyear 数据**

| Obs | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|
| 1 | 5 | 213.10 | 478.0 | 525.80 | 394.35 | 191.79 |
| 2 | 10 | 188.10 | 414.09 | 2876.9 | 3164.59 | 169.29 |
| 3 | 11 | 78.20 | | | | 70.38 |
| 4 | 12 | 135.60 | | 117.6 | 129.36 | 122.04 |
| 5 | 18 | | | 29.4 | 32.34 | 24.26 |

a. Orion Star 公司决定，如果客户至少有三个月的订单数据，则创建一个常客计划 (FSP)。若要获得该计划的邀请，客户必须在 50% 的月份内有订单，且自年初以来消费金额至少 $1000。例如：如果数据文件包含某客户 6 个月的订单，则客户必须在三个或更多月份内消费超过 $1000；如果数据文件只有 3 个月的订单，则客户必须在两个或更多月份内消费超过 $1000 才能获得常客计划。

- 打开数据集并验证其是否包含至少三个月的数据。
- 如果少于三个月，向 SAS 日志写入信息并立即停止 DATA 步骤。
- 如果数据集中至少有三个月的数据，创建一个数组 **Mon** 来访问 Month 变量，无论数据集中存在多少个变量。提示：考虑使用 SAS 变量来列出数组元素。
- 使用 DO 循环检查每个客户的数据，以确定该客户是否符合常客计划的条件。
- 创建一个新的数据集 **fsp**，包含每个符合条件的客户的观测值。
- 使用报告确定要删除或保留哪些变量。
- 提示：使用 SAS 文档研究 STOP 语句的使用。

b. 使用合适的标题和格式打印生成的数据集，并验证你的结果。部分 midyear: (11 个观测值) orion.orders_midyear: 常客

| Obs | Customer_ID | Total_Order_Amount | Months_Ordered |
|---|---|---|---|
| 1 | 5 | $1,803.04 | 5 |
| 2 | 10 | $9,186.41 | 6 |
| 3 | 27 | $1,373.23 | 3 |
| 4 | 31 | $1,113.47 | 3 |
| 5 | 34 | $1,473.18 | 5 |

c. 使用 **orion.orders_qtr1** 测试你的程序。PROC PRINT 输出 orion.orders_qtr1: 常客

| Obs | Customer_ID | Total_Order_Amount | Months_Ordered |
|---|---|---|---|
| 1 | 10 | $3,479.09 | 3 |
| 2 | 27 | $1,093.60 | 2 |
| 3 | 31 | $1,777.60 | 2 |
| 4 | 17 | $1,849.90 | 3 |
| 5 | 28 | $1,506.90 | 3 |

d. 使用 orion.orders_two_months 测试你的程序。部分 Shopper Program SAS 日志

```
Insufficient data for Shopper Program
NOTE: 从 ORION.ORDERS_MONTHS 读取了 0 个观测值。
NOTE: 数据集 WORK.FSP 有 0 个观测值和 3 个变量。
NOTE: 使用了 data 语句 (Total time):
title 'orion.orders_two_months: Frequent Shoppers ';
proc print data=fsp;
format total_order_amount dollar10.;
```
数据集 中没有观测值。

## 7.4 使用 SAS 数组

### 将数组作为函数使用
以下程序将数组传递给 SUM 函数。

```sas
data test;
  set orion.employee_donations;
  array val{4} Qtr1-Qtr4;
  Tot1=sum(of val*);
  Tot2=sum(of val*);
run;
proc print data=test;
  var Employee_ID Tot1 Tot2;
run;
```

部分 PROC PRINT 输出

| Obs | Employee_ID | Tot1 | Tot2 |
|---|---|---|---|
| 1 | 12065 | 25 | 25 |
| 2 | 12067 | 60 | 60 |
| 3 | 12069 | 80 | 80 |

![](img/d3bde6eab06b1fc622215d98211742_322_0.png)

### DIM 函数
DIM 函数返回数组元素。此值通常用作 DO 循环的停止值。

```sas
data charity;
  set orion.employee_donations;
  keep Employee_ID Qtr1-Qtr4;
  array Contrib{*} qtr;
  do i=1 to dim(Contrib);
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```
> DIM(array_name)

![](img/d3bde6eab06b1fc622215d98211742_322_1.png)

HBOUND 函数返回数组的上边界。LBOUND 函数返回数组的下边界。以下 DO 循环处理数组中的每个元素：

```sas
do i=lbound(items) to hbound(items);
  *process items{i};
end;
```

在大多数数组中，下标从 1 到 n，其中 n 是数组元素的数量。值 1 是方便的下边界。你不需要指定下边界。当数组维度起点不是 1 时，指定两个边界是有用的。例如，以下 ARRAY 定义了一个下标从 5 到 14 的 10 个元素的数组：

```sas
array items{5:14} n5-n14;
```

### 使用数组创建数值变量
ARRAY 语句可以在程序数据向量（PDV）中创建新变量。

```sas
array Pct{4} Pct1-Pct4;
```

如果 Pct1 和 Pct4 不存在于 PDV 中，则会被创建。此语句产生相同的结果：

```sas
array Pct{4};
```

PDV:

| Pct1 | Pct2 | Pct3 | Pct4 |
|---|---|---|---|
| N 8 | N 8 | N 8 | N 8 |

### 使用数组创建字符变量
定义一个名为 Month 的数组以创建长度为 10 的字符变量。

```sas
array Month{6} $ 10;
```

PDV:

| Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|
| $ 10 | $ 10 | $ 10 | $ 10 | $ 10 | $ 10 |

### 场景
使用 orion.employee_donations 作为输入，计算每个季度贡献占员工总贡献的百分比。创建四个新变量来存储这些百分比。

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 12065 | | | 25 | |
| 12067 | 15 | 15 | 15 | |

![](img/d3bde6eab06b1fc622215d98211742_324_0.png)

| Employee_ID | Percent1 | Percent2 | Percent3 | Percent4 |
|---|---|---|---|---|
| 12065 | | | | 100% |
| 12067 | 25% | 25% | 25% | |

### 使用数组创建变量

```sas
data percent(drop=i);
  set orion.employee_donations;
  array Contrib(4) Cary Qtr1-Qtr4;
  array Percent(4);
  Total=sum(of contrib*);
  do i=1 to 4;
    percent{i}=contrib{i}/total;
  end;
run;
```

