
`PROC FREQ` 输出

| Period | Frequency |
|---|---|
| Qtr1 | 110 |
| Qtr2 | 98 |
| Qtr3 | 107 |
| Qtr4 | 102 |

# 旋转后的 SAS 数据集绘图

`PROC GCHART` 输出

| Sum of Employee Contributions | |
|---|---|
| Qtr2 | Qtr1 |
| $1,440 | $1,510 |
| Qtr3 | Qtr4 |

### 练习题

如果你自上次练习以来重启了 SAS 会话，请打开并提交位于数据文件夹中的 `libname.sas` 程序。

## 第 1

### 1. 旋转数据集

数据集 `orion.orders_midyear` 包含每个客户的观测值，其中包含该客户上半年每月订单的总零售价值。

`orion.orders_midyear` 部分列出（共 24 条观测值）

| Obs | Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|---|
| 1 | 5 | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 2 | 10 | 188.10 | 414.00 | 2876.9 | 3164.59 | 2373.44 | 169.29 |
| 3 | 11 | 78.20 | | | | | 70.38 |
| 4 | 12 | 135.60 | | 117.6 | 129.36 | 97.02 | 122.04 |
| 5 | 18 | | | | 29.4 | 32.34 | 24.26 |

- a. 旋转 `orion.orders_midyear` 以创建一个输出数据集 `sixmonths`，其中包含每个客户每月一个观测值。
- 数据集应包含 `Customer_ID`、`Month` 和 `Sales`。
- 如果每月总额缺失，则不输出该观测值。

b. 打印新数据集。验证结果。

部分 `PROC PRINT` 输出（共 88 条观测值）

| Obs | Customer_ID | Month | Sales |
|---|---|---|---|
| 1 | 5 | 1 | 213.10 |
| 2 | 5 | 3 | 478.00 |
| 3 | 5 | 4 | 525.80 |
| 4 | 5 | 5 | 394.35 |
| 5 | 5 | 6 | 191.79 |

## 第 2

### 2. 旋转数据集并使用查找表

数据集 `orion.travel_expense` 包含每个员工出差的观测值，并在 `Trip_ID`、`Employee_ID` 以及多达五项费用 `Exp1-Exp5`。下表显示了每项费用的类型：

| Exp1 | Airfare |
|---|---|
| Exp2 | Hotel |
| Exp3 | Meals |
| Exp4 | Transportation |
| Exp5 | Miscellaneous |

`orion.travel_expense` 部分（共 10 条观测值）

| Obs | Trip_ID | ID | Exp1 | Exp2 | Exp3 | Exp4 | Exp5 |
|---|---|---|---|---|---|---|---|
| 1 | 1044-1 | 121044 | 345.97 | 568.54 | 235.00 | 320.00 | |
| 2 | 0145-1 | 120145 | 256.00 | 675.90 | 343.25 | 125.00 | 67.50 |
| 3 | 0656-1 | 120656 | 312.26 | | 236.98 | 325.00 | 45.00 |
| 4 | 1119-1 | 121119 | 597.80 | 780.99 | 345.87 | 195.00 | 50.75 |
| 5 | 0812-1 | 120812 | 345.24 | 865.12 | | | |

- a. 旋转 `orion.travel_expense` 以创建一个名为 `travel` 的输出数据集，其中包含每个客户一个观测值。
- 数据集应包含 `Trip_ID`、`Employee_ID`、`Expense_Type` 和 `Amount`。
- 使用数组处理每个客户的五项费用，并将结果存储为查找表。
- b. 打印新数据集。为 `Amount` 化美元符号、逗号和两位小数。将你的结果与下方进行对比。

`PROC PRINT` 输出（共 44 条观测值）

| Obs | Trip_ID | Expense_Type | Amount |
|---|---|---|---|
| 1 | 1044-1 | Airline | 345.97 |
| 2 | 1044-1 | Hotel | 568.54 |
| 3 | 1044-1 | Meals | 235.00 |
| 4 | 1044-1 | Transportation | 320.00 |
| 5 | 0145-1 | Airline | 256.00 |
| 6 | 0145-1 | Hotel | 675.90 |
| 7 | 0145-1 | Meals | 343.25 |
| 8 | 0145-1 | Transportation | 125.00 |
| 9 | 0145-1 | Miscellaneous | 67.50 |
| 10 | 0656-1 | Airline | 312.26 |

### 挑战

## 3. 旋转数据集

数据集 `orion.order_summary` 包含每个客户的每月订单信息，多个观测值。

`orion.order_summary` 部分（共 101 条观测值）

| Customer_ID | Month | Sale_Amt |
|---|---|---|
| 5 | 1 | 213.10 |
| 5 | 3 | 478.0 |
| 5 | 4 | 525.80 |
| 5 | 5 | 394.35 |
| 5 | 6 | 191.79 |
| 10 | 1 | 188.10 |
| 10 | 2 | 414.0 |
| 10 | 3 | 2876.9 |
| 10 | 4 | 3164.59 |
| 10 | 5 | 2373.44 |
| 10 | 6 | 169.29 |
| 11 | 1 | 78.20 |
| 11 | 6 | 70.38 |
| 12 | 1 | 135.60 |
| 12 | 3 | 117.6 |
| 12 | 4 | 129.36 |
| 12 | 5 | 97.02 |
| 12 | 6 | 122.04 |
| 18 | 5 | 29.4 |
| 18 | 6 | 32.34 |
| 18 | 7 | 24.26 |

- a. 旋转 `orion.order_summary` 以创建一个名为 `customer_orders` 的数据集，其中包含每个客户一个观测值。
- 在 `DATA` 步中使用数组。
- 数据集应包含 `Customer_ID` 和从 `Month1` 到 `Month12`。
- b. 打印新数据集。验证结果。

部分 `PROC PRINT` 输出（共 37 条观测值）

| Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 | Month7 | ... | Month11 | Month12 |
|---|---|---|---|---|---|---|---|---|---|
| 5 | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 | | | | |
| 10 | 188.10 | 414.0 | 2876.9 | 3164.59 | 2373.44 | 169.29 | | | | |
| 11 | 78.20 | | | | | 70.38 | | | | |
| 12 | 135.60 | | 117.6 | 129.36 | 97.02 | 122.04 | | | | |
| 18 | | | | 29.4 | 32.34 | 24.26 | | | | |

# 8.2 答案

练习题的答案

- 1. 旋转数据集

```sas
data sixmonths;

  set orion.orders_midyear;

  keep id month sales;

  array months{6} month1-month6;

  do Month=1 to 6;

    if months{Month} ne . then do;

      Sales=months{Month};

      output;

    end;

  end;

run;
```

```sas
proc print data=sixmonths;

run;
```

- 2. 旋转数据集并使用查找表

```sas
data travel;

  set orion.travel_expense;

  keep employee id trip_id Expense_Type amount;

  array exp{5} exp1-exp5;

  array descr{5} $ ('Airfare', 'Hotel', 'Meals', 'Transportation', 'Miscellaneous');

  do i=1 to 5;

    if exp{i} ne . then do;

      Expense_Type=descr{i};

      Amount=exp{i};

      output;

    end;

  end;

run;
```

```sas
proc print data=travel;

format Amount dollar.2.;

run;
```

```sas
data customer_orders;

  set orion.order_summary;

  retain Month1-Month12;

  array Month{12};

  by Customer_ID;

  if first.Customer_ID then call missing(of Month*);

  Month{Order_ID}=Sale_Amt;

  if last.Customer_ID;

  drop Order_ID Sale_Amt;

run;

options ls=120;

proc print data=customer_orders noobs;

run;
```

## 9.1 使用数据处理技术进行匹配合并（Match-Merging）

### 目标
- 复习 SAS 数据集的匹配合并。
- 展示在匹配合并中使用数据处理技术的示例。
- 展示针对以下特殊情况执行匹配合并的技术：
  - 缺少单个共同变量的三个或多个 SAS 数据集
  - 为了获得正确的合并结果而需要更改变量名。

### 匹配合并（复习）
匹配合并（Match merging）根据一个或多个共同变量的值，将一个或多个 SAS 数据集的观测值合并到一个新数据集的单个观测值中。

![](img/d3bde6e6ab06b1fc622215d982111742_376_0.png)

### 9.01 多选题调查

关于匹配合并，哪种陈述是正确的？

- a. `MERGE` 语句必须引用永久数据集。
- b. `BY` 语句中的变量只能存在于一个数据集中。
- c. `MERGE` 语句只能指定两个数据集。
- d. 当你使用带有 `BY` 语句的 `MERGE` 语句时，数据必须按照 `BY` 变量进行排序或索引。

### 匹配合并（复习）

部分 SAS 日志

```
729 proc sort data=or.order_fact
730     out=work.order_fact;
731     by Customer_ID;
732     where year(Order_Date)=2007;
733 run;
```

NOTE: 从数据集 `ORIG.ORDER_FACT` 读取了 128 个观测值。
NOTE: `WHERE(Order_Date)=2007`.
NOTE: 数据集 `WORK.ORDER_FACT` 具有 128 个观测值和 12 个变量。

```
734 data Custord;
735     merge orig.customer
736     work.order_fact;
737     by Customer_ID;
738 run;
```

NOTE: 从数据集 `ORIG.CUSTOMER` 读取了 77 个观测值。
NOTE: 从数据集 `WORK.ORDER_FACT` 读取了 128 个观测值。
NOTE: 数据集 `WORK.CUSTORD` 具有 168 个观测值和 22 个变量。

### 9.1 使用数据处理技术进行匹配合并

### 匹配合并（复习）

部分 `PROC PRINT` 输出

| Obs | Customer_Name | Gender | Quantity | Total_Retail_Price |
|---|---|---|---|---|
| 152 | Tommy Macdonald | M | 2 | $49.00 |
| 153 | Colin Bylter | M | | |
| 154 | Lena Kroll | F | | |
| 155 | Wilma Yeargan | - | | |
| 156 | Patrick Leach | M | 2 | $42.40 |
| 157 | Patrick Leach | - | 1 | $55.90 |
| 158 | Portia Reynoso | F | | |

![](img/d3bde6e6ab06b1fc622215d982111742_378_0.png)

![](img/d3bde6e6ab06b1fc622215d982111742_378_1.png)

如何只保留匹配的项？

### 匹配合并（复习）

此程序仅为匹配项写入观测值。`IN=` 数据集选项创建一个用于识别匹配项和非匹配项的变量。

```
data CustOrd;

  merge orion.customer(in=cust)
         work.order_fact(in=order);

  by Customer_ID;

  if cust=1 and order=1;

run;
```

> NOTE: 从数据集 `ORION.CUSTOMER` 读取了 77 个观测值。
NOTE: 从数据集 `ORDER_FACT` 读取了 128 个观测值。
NOTE: 数据集 `CUSTORD` 具有 128 个观测值和 22 个变量。

### 9.02 答调查

编写适当的 `IF` 语句创建一个创建一个包含非匹配项的数据集。

```
data combine;

  merge products(in=InProd) costs(in=InCost);

  by ID;

  if InProd = 0 or InCost = 0;

run;
```

| Products | ID | | ID | Cost | |
| --- | --- | --- | --- | --- | --- |
| XYZ Shoe | A123 | | B456 | 59.99 | |
| ABC Coat | B456 | | C789 | 35.75 | |

### 业务场景

营销经理需要三个 SAS 数据集来帮助她分析客户和订单。
输入数据集需要合并以创建输出。

- Customer * Order_fact

img/d3bde6e6ab06b1fc622215d982111742_379_0.png

### 业务场景

经理希望你创建以下 SAS 数据集：
- **noorders** – 包含未下单客户的姓名和出生日期
- **orders** – 详细记录订单，包括客户姓名、产品 ID、数量和价格
- **summary** – 包含每个客户下达的订单计数

### 数据处理技术

逐个添加这些技术，以展示如何构建和测试最终解决方案。

![](img/d3bde6e6ab06b1fc622215d982111742_380_0.png)

### OUTPUT 语句

在此程序中，`OUTPUT` 语句用于将有匹配订单的客户重定向到一个数据集，将没有订单的客户重定向到另一个数据集。

```
data orders noorders;

  merge orion.customer
  work.order_fact(in=order);

  by Customer_ID;

  if order=1 then output orders;
  else output noorders;

run;
```

部分 SAS 日志

> NOTE: 从数据集 `ORION.CUSTOMER` 读取了 77 个观测值。
NOTE: 从数据集 `WORK.ORDER_FACT` 读取了 128 个观测值。
NOTE: 数据集 `WORK.ORDERS` 具有 128 个观测值和 22 个变量。
NOTE: 数据集 `WORK.NOORDERS` 具有 35 个观测值和 22 个变量。

### DROP= 和 KEEP= 选项

你可以使用 `DROP=` 和 `KEEP=` 数据选项来决定哪些变量写入每个输出集。

```
data orders (keep=(Customer_Name ID Total_Retail_Price))
  noorders (keep=(Customer_Name Birth_Date));

  merge orion.customer
  work.order_fact(in=order);

  by Customer_ID;

  if order=1 then output orders;
  else output noorders;

run;
```
