

# 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee Id Period Amount);
  set orion.employee_donations
  (drop=recipients paid_by);
  array contrib[4] qtr1-q4;
  do i=1 to 4;
    if contrib{i} ne . then do
      Period=cats("Qtr",i);
      Amount=contrib{i};
      output;
    end;
  end;
  run; 
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120267 | 15 | 15 | 15 | 15 | | | 15 |

| Employee_ID | Period | Amount |
|---|---|---|
| 120267 | Qtr4 | 25 |
| 120267 | Qtr1 | 15 |

# 输出：旋转后的数据集

```sas
proc print data=rotate;
run;
```

部分旋转后的 PROC PRINT 输出（共 417 条观测值）

| Obs | Employee_ID | Period | Amount |
|---|---|---|---|
| 1 | 120267 | Qtr4 | 25 |
| 2 | 120267 | Qtr1 | 15 |
| 3 | 120267 | Qtr2 | 15 |
| 4 | 120267 | Qtr3 | 15 |
| 5 | 120267 | Qtr4 | 15 |

# 分析旋转后的 SAS 数据集

```sas
proc freq data=rotate;
tables Period /nocum nopct;
run;
```

PROC FREQ 输出

| Period | Frequency |
|---|---|
| Qtr1 | 110 |
| Qtr2 | 98 |
| Qtr3 | 107 |
| Qtr4 | 102 |

# 旋转后的 SAS 数据集绘图

PROC GCHART 输出

| Sum of Employee Contributions | |
|---|---|
| Qtr2 | Qtr1 |
| $1,440 | $1,510 |
| Qtr3 | Qtr4 |

# 练习题

如果你自上次练习以来重启了 SAS 会话，请打开并提交位于数据文件夹中的 `libname.sas` 程序。

# 第 1 

# 1. 旋转数据集

数据集 `orion.orders_midyear` 包含每个客户的观测值，其中包含该客户上半年每月订单的总零售价值。

`orion.orders_midyear` 部分列出（共 24 条观测值）

| Obs | Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|---|
| 1 | 5 | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 2 | 10 | 188.10 | 414.00 | 2876.9 | 3164.59 | 2373.44 | 169.29 |
| 3 | 11 | 78.20 | | | | | 70.38 |
| 4 | 12 | 135.60 | | 117.6 | 129.36 | 97.02 | 122.04 |
| 5 | 18 | | | | 29.4 | 32.34 | 24.26 | |

- a. 旋转 `orion.orders_midyear` 以创建一个输出数据集 `sixmonths`，其中包含每个客户每月一个观测值。
- * 数据集应包含 `Customer_ID`、`Month` 和 `Sales`。
- 如果每月总额缺失，则不输出该观测值。

b. 打印新数据集。验证结果。

部分 PROC PRINT 输出（共 88 条观测值）

| Obs | Customer_ID | Month | Sales |
|---|---|---|---|
| 1 | 5 | 1 | 213.10 |
| 2 | 5 | 3 | 478.00 |
| 3 | 5 | 4 | 525.80 |
| 4 | 5 | 5 | 394.35 |
| 5 | 5 | 6 | 191.79 |

# 第 2 

# 2. 旋转数据集并使用查找表

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
| 5 | 0812-1 | 120812 | 345.24 | 865.12 | | | | |

- a. 旋转 `orion.travel_expense` 以创建一个名为 `travel` 的输出数据集，其中包含每个客户一个观测值。
- 数据集应包含 `Trip_ID`、`Employee_ID`、`Expense_Type` 和 `Amount`。
- 使用数组处理每个客户的五项费用，并将结果存储为查找表。
- b. 打印新数据集。为 `Amount` 化美元符号、逗号和两位小数。将你的结果与下方进行对比。

PROC PRINT 输出（共 44 条观测值）

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

# 挑战

# 3. 旋转数据集

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
- 在 DATA 步中使用数组。
- 数据集应包含 `Customer_ID` 和从 `Month1` 到 `Month12`。
- b. 打印新数据集。验证结果。

部分 PROC PRINT 输出（共 37 条观测值）

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

