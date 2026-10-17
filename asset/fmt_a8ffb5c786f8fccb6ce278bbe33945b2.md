
默认情况下，通过赋值语句创建的变量在每次 DATA 步迭代开始时都会被初始化为缺失值。

```sas
data mnthtot;
set orion.aprsales;
Mth2Dte=Mth2Dte+SaleAmt;
run;
```

### 创建累加变量

保留 `Mth2Dte` 的值并设置初始值。

```sas
data mnthtot;
  set orion.aprsales;
  retain Mth2Dte 0;
  Mth2Dte=Mth2Dte+SaleAmt;
run;
```

`RETAIN` 变量名 `<初始值>`...

如果你不提供初始值，`Mth2Dte` 的所有值都将为缺失（missing）。

### RETAIN 语句：详情

`RETAIN` 语句

- 在 DATA 步的迭代过程中，保留变量在 PDV 中的值
- 在 DATA 步的第一次迭代之前，将被保留的变量初始化为缺失或指定的变量
- 是一个仅在编译时执行的语句。

> `RETAIN` 语句对通过 `SET`、`MERGE` 或 `UPDATE` 语句读取的变量没有影响。从 SAS 数据集读取的变量会被自动保留。

### 编译：创建累加变量

```sas
data mntthot;
set orion.aprsales;
retain Mth2Dte 0;
Mth2Dte=Mth2Dte+SaleAmt;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_85_0.png)

### 执行：创建累加变量

| SaleDate | SaleAmt |
|---|---|
| 18718 | 498.49 |
| 18719 | 946.50 |
| 18720 | 994.97 |
| 18721 | 564.59 |
| 18722 | 783.01 |

```sas
data mntthot;
set orion.aprsales;
retain Mth2Dte 0;
Mth2Dte=Mth2Dte+SaleAmt;
run;
```

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| . | . | 0 输入数据集必须按 `SaleDate` 排序才能产生正确结果。

### 执行：创建累加变量

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | 0 |

### 执行：创建累加变量

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | | (img/d3bde6e6ab06b1fc622215d982111742_86_0.png)

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | 498.49 |

### 执行：创建累加变量

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

```sas
Implicit OUTPUT;
Implicit RETURN;
```

PDV

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | 498.49 | 将观测值写入 `mnthtot`

### 执行：创建累加变量

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

```sas
Mth2Dte is not initialized.
```

PDV

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | 498.49 |

## 3.1 创建累加总计变量

### 执行：创建累加变量

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

| PDV | SaleDate | SaleAmt | Mth2Dte |
|---|---|---|---|
| 18719 | 946.50 | 498.49 |

### 执行：创建累加变量

| SaleDate | SaleAmt | mnthtot; |
|---|---|---|
| 18718 | 498.49 | |
| 18719 | 946.50 | |
| 18720 | 994.97 | |
| 18721 | 564.59 | |
| 18722 | 783.01 | |

| PDV | SaleDate | SaleAmt | Mth2Dte |
|---|---|---|---|
| 18719 | 946.50 | 1444.99 |

### 执行：创建累加变量

| SaleDate | SaleAmt |
|---|---|
| 18718 | 498.49 |
| 18719 | 946.50 |
| 18720 | 994.97 |
| 18721 | 564.59 |
| 18722 | 783.01 |

```sas
data mnthtot;
set orion.aprsales;
retain Mth2Dte 0;
Mth2Dte=Mth2Dte+SaleAmt;
run;
```
> 隐式 OUTPUT:隐式 RETURN;

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18719 | 946.50 | 1444.99 | 将观测值写入 `mnthtot`

### 执行：创建累加变量

| SaleDate | SaleAmt |
|---|---|
| 18718 | 498.49 |
| 18719 | 946.50 |
| 18720 | 994.97 |
| 18721 | 564.59 |
| 18722 | 783.01 |

```sas
Mth2Dte is not reinitialized. Mth2Dte 未被重新初始化。
```

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18719 | 946.50 | 1444.99 |

### 执行：创建累加变量

| SaleDate | SaleAmt |
|---|---|
| 18718 | 498.49 |
| 18719 | 946.50 |
| 18720 | 994.97 |
| 18721 | 564.59 |
| 18722 | 783.01 |

```sas
data mnthtot;
set orion.aprsales;
retain Mth2Dte;
Mth2Dte=Mth2Dte+SaleAmt;
run;
```

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 18719 | 946.50 | 1444.99 |

### 创建累加变量

```sas
proc print data=mnthtot noobs;
format SaleDate date;
run;
```

部分 PROC 输出

| SaleDate | Amt | Mth2Dte |
|---|---|---|
| 01APR2011 | 498.49 | 498.49 |
| 02APR2011 | 946.50 | 1444.99 |
| 03APR2011 | 994.97 | 2439.96 |
| 04APR2011 | 564.59 | 3004.55 |
| 05APR2011 | 783.01 | 3787.56 |

## 3-12 第 3 章 数据汇总

### 调查设置

如果 `SaleAmt` 有缺失值会发生什么？

打开并提交 `p203a02` 并查看输出。

部分 `orion.Aprsales`

img/d3bde6e6ab06b1fc622215d982111742_91_0.png)

## 3.02 选择

`SaleAmt` 的缺失值对 `Mth2Dte` 有什么影响？

- a 缺失值被忽略；`Mth2Dte` 值不受影响。
- b 缺失值导致 DATA 步停止处理。
- c 缺失值导致后续的 `Mth2Dte` 值被设为缺失。

## 3.1 创建累加总计变量

### 不理想的输出：缺失值

| SaleDate | Amt | Mth2Dte |
|---|---|---|
| 01APR2011 | 498.44 | 498.47 |
| 02APR2011 | | . |
| 03APR2011 | 994.97 | . |
| 04APR2011 | 564.59 | . |
| 05APR2011 | 783.01 | . |

img/d3bde6e6ab06b1fc622215d982111742_92_0.png)

### SUM 函数

`RETAIN` 语句配合赋值语句中的 `SUM` 函数可以创建 `Mth2Dte`。

```sas
data mnthtot;
set orion.aprsales;
retain Mth2Dte 0;
Mth2Dte=sum(Mth2Dte, SaleAmt);
run;
```

> `SUM` 函数忽略值。

## 3-14 第 3 章 数据汇总

# Sum 语句

使用 `sum` 语句创建 `Mth2Dte`。

```sas
data mnthtot2;
set orion.aprsales;
Mth2Dte+=SaleAmt;
run;
```

> `sum` 语句初始化为零并并每个观测值的 `SaleAmt` 自动增加。

# Sum 语句

```sas
proc print data=mnthtot noobs;
run;
```

部分 PROC 输出

| SaleDate | SaleAmt | Mth2Dte |
|---|---|---|
| 01APR2011 | 498.49 | 498.49 |
| 02APR2011 | 946.50 | 1444.99 |
| 03APR2011 | 994.97 | 2439.96 |
| 04APR2011 | 564.59 | 3004.55 |
| 05APR2011 | 783.01 | 3787.56 |

## 3.1 创建累加变量

# 1. 创建累加总计

数据集 `orion.order_fact` 包含一组订单，按 `Order_Date` 排序。`DATA` 步使用 `WHERE` 语句仅读取指定日期范围内的观测值：

- 修改程序以创建一个累加总计 `Sales2Dte`，用于显示到目前的销售额。
- 同时创建一个累加变量 `Num_Orders`，表示每个观测值计一个订单。

```sas
where '01Nov2008'd <= Order_Date <= '14Dec2008'd;
```

部分 PROC PRINT 输出

| Obs | Order_ID | Date | Total_Retail_Price | Sales2Dte | Num Orders |
|---|---|---|---|---|---|
| 1 | 123403037 | 01NOV2008 | $53.70 | $53.70 | 1 |
| 2 | 123409222 | 10NOV2008 | $7.20 | $60.90 | 2 |
| 3 | 123413379 | 17NOV2008 | $328.30 | $389.20 | 3 |
| 4 | 123418633 | 25NOV2008 | $200.10 | $589.30 | 4 |
| 10 | 1234031319 | 1DEC2008 | $105.60 | $1,664.20 | 10 |

## 第3章 数据汇总

`orion.order_fact` 的部分列出（共计 617 条观测值，12 个变量）

| Order_ID | Order_Type | Order_Date | Quantity |
| --- | --- | --- | --- |
| 1230058123 | 1 | 11JAN2007 | 1 |
| 1230080101 | 2 | 15JAN2007 | 1 |
| 1230106863 | 2 | 20JAN2007 | 1 |
| 1230147441 | 1 | 28JAN2007 | 2 |
| 1230315085 | 1 | 27FEB2007 | 3 |

- Orion Star 公司希望通过创建来自零售（retail）、目录（catalog）和互联网（Internet）的项目总数来分析 2009 年的数据。
- * `Order_Type` 的值表示销售类型是零售（=1）、目录（=2）还是互联网（=3）。
- 创建名为 `work.ytotals` 的数据集，其中包含上所述的 `TotalRetail`、`TotalCatalog` 和 `TotalInternet` 的累积总计。

> `Quantity` 变量包含每个订单的项目数量。

- * 为了在这一步中测试你的程序，请仅读取满足 `WHERE` 语句的前 10 条观测值。
- 记住只处理 `Order_Date` 发生在 2009 年的行。
- 通过打印 a 部分的结果继续测试你的程序。打印所有变量，并验证程序正在计算累计总和的值。

### PROC PRINT 输出

| Obs | Customer_ID | Employee_ID | Street_ID | Date | Order_ID | Type | Product_ID |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 195 | 120150 | 160010663 | 02JAN2009 | 02JAN2009 | 123443760 | 1 | 23010600028 |
| 2 | 36 | 9999999 | 926012823 | 14JAN2009 | 14JAN2009 | 1234534069 | 3 | 24800100026 |
| 3 | 183 | 120121 | 160010760 | 12JAN2009 | 12JAN2009 | 1234537441 | 1 | 24010200001 |
| 4 | 16 | 9999999 | 3940150865 | 14JAN2009 | 14JAN2009 | 1234538390 | 2 | 22020200035 |
| 10 | | 120179 | 1600107680 | 31JAN2009 | 31JAN2009 | 1234727966 | 1 | 24070400004 |
| | TotalRetail_Price | CostPrice_Per_Unit | Total Retail | Total Catalog | Total Internet |
| --- | --- | --- | --- | --- | --- |
| 1 | $193.40 | $48.45 | 2 | 0 | 0 |
| 2 | $525.20 | $58.55 | 2 | 0 | 4 |
| 3 | $16.00 | $6.35 | 3 | 0 | 4 |
| 4 | $115.50 | $48.50 | 3 | 1 | 4 |
| 10 | $13.20 | $5.95 | 2 | 0 | 6 |

当 a 和 b 部分的结果正确时，执行以下操作：

- 修改程序以读取满足 `WHERE` 语句的所有观测值。生成的报告包含 90 条观测值。
- 仅保留 `Order_Date`、`Order_ID`、`TotalRetail` 和 `TotalInternet` 变量。
- 使用适当标题打印你的结果。

## 3.1 创建累计变量

数据集 `orion.order_fact`（617 条观测值，12 个变量）包含按 `Order_Date` 排序的跨年订单组。

| Order_ID | Date | TotalRetail_Price |
| --- | --- | --- |
| 1230058123 | 11JAN2007 | $16.50 |
| 1230080101 | 15JAN2007 | $247.50 |
| 1230106863 | 20JAN2007 | $28.30 |
| 1230147441 | 28JAN2007 | $32.00 |
| 1230315085 | 27FEB2007 | $63.60 |

Orion Star 希望生成以下显示 2011 年所有订单的报告：累计总计在每月开始时重置为零。记住只处理 `Order_Date` 发生在 2011 年的行。PROC PRINT 输出（2011 年每月累计总计）
