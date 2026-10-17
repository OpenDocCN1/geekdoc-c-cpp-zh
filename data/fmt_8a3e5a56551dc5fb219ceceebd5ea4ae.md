
你有一个名为 `Sales` 的 SAS 数据集，其中包含有关销售的信息：员工姓名（`Name`）和 ID（`ID`）、销售区域（`region`）、销售对象公司名称、零件号、数量（`Quantity`）、物品单价（`UnitCost`）以及销售总额（`Quantity` 乘以 `UnitCost`）。程序 14.1 显示了带有所有默认值的 `PROC PRINT`：

220 实例化学习 SAS：程序员指南，第二版

### 程序 14.1：使用所有默认值的 PROC PRINT

```
title "Listing of Data Set Sales"
proc print data=Learn.Sales;
run;
```

你将获得类似于图 14.1 所示的列表：

### 图 14.1：程序 14.1 的部分输出

#### 数据集列表

| Obs | EmpID | Name | Region | Customer | Item | Quantity | UnitCost | TotalSales |

|---|---|---|---|---|---|---|---|---||

| 1 | 1843 | George Smith | North | Barco Corporation | 144L | 50 | 8.99 | 449.5 |

| 2 | 1843 | George Smith | South | Cost Cutter's | 122 | 100 | 5.99 | 599.0 |

| 3 | 1843 | George Smith | North | Minimart Inc. | 188S | 3 | 5199.0 | 15597.0 |

| 4 | 1843 | George Smith | North | Barco Corporation | 908X | 1 | 5129.00 | 5129.0 |

| 5 | 1843 | George Smith | South | Ely Corp. | 122L | 10 | 29.95 | 299.5 |

| 6 | 0177 | Glenda Johnson | East | Food Unlimited | 188X | 100 | 6.99 | 699.0 |

| 7 | 0177 | Glenda Johnson | East | Shop and Drop | 144L | 100 | 8.99 | 899.0 |

| 8 | 1843 | George Smith | South | Cost Cutter's | 855W | 1 | 9109.0 | 9109.0 |

| 9 | 9888 | Sharon Lewis | West | Cost Cutter's | 122 | 50 | 5.99 | 299.5 |

### 14.3 更改列表的外观

你可以使用 `VAR` 语句来控制列表中显示哪些变量以及这些变量的顺序。在 `VAR` 之后放置你想看到的变量。该顺序控制了列表中显示的变量。

### 程序 14.2：控制列表中显示的变量

```
title "Listing of Sales"
proc print data=Learn.Sales;
var Customer TotalSales;
run;
```

如果你运行程序 14.2 中的代码，你将获得：

232

### 图 14.2：程序 14.2 的输出

#### 销售列表

| Obs | EmpID | Customer | TotalSales |

|---|---|---|---|

| 1 | 1843 | Barco Corporation | 449.5 |

| 2 | 1843 | Cost Cutter's | 599.0 |

| 3 | 1843 | Minimart Inc. | 15597.0 |

| 4 | 1843 | Barco Corporation | 5129.0 |

| 5 | 1843 | Ely Corp. | 299.5 |

| 6 | 0177 | Food Unlimited | 699.0 |

| 7 | 0177 | Shop and Drop | 899.0 |

| 8 | 1843 | Cost Cutter's | 9109.0 |

| 9 | 9888 | Cost Cutter's | 299.5 |

你的下一步是省略 `Obs` 列并用员工替换它。使用 `ID` 语句来实现：

### 程序 14.3：使用 ID 语句省略列

```
title "Listing of Sales"
proc print data=Learn.Sales;
id EmpID;
var Customer TotalSales;
run;
```

注意列表发生了变化。

### 图 14.3：程序 14.3 的部分输出

#### 销售列表

| EmpID | Customer | TotalSales |

|---|---|---|

| 1 | 1843 | Barco Corporation | 449.5 |

| 2 | 1843 | Cost Cutter's | 599.0 |

| 3 | 1843 | Minimart Inc. | 15597.0 |

| 4 | 1843 | Barco Corporation | 5129.0 |

| 5 | 1843 | Ely Corp. | 299.5 |

| 6 | 0177 | Food Unlimited | 699.0 |

| 7 | 0177 | Shop and Drop | 899.0 |

| 8 | 1843 | Cost Cutter's | 9109.0 |

| 9 | 9888 | Cost Cutter's | 299.5 |

233

222 实例化学习 SAS：程序员指南，第二版

你放在 `ID` 语句中的变量（或变量）将替换 `Obs` 列并打印在列表的最左侧。注意在 `ID` 语句中放置变量时，不要在 `VAR` 语句中列出它。如果这样做了，它会出现两次。

省略 `Obs` 列的另一种方法是使用带有 `NOOBS` 选项的 `PROC PRINT`。使用 `ID` 语句的优点是，如果有更多变量需要跨页显示，`ID` 变量将在每页开始显示。

### 14.4 更改值的显示方式

### 程序 14.4：在 PROC PRINT 中添加 FORMAT 语句

```
title "Listing of Sales"
proc print data=Learn.Sales;
  id EmpID;
  var Customer Quantity TotalSales;
  format TotalSales dollar10.2 comma7;
run;
```

注意 `Quantity` 和 `TotalSales` 列的变化。

### 图 14.4：程序 14.4 的部分列表

#### 列表

| EmpID | Customer | Quantity | TotalSales |

|---|---|---|---|---|

| 1 | 1843 | Barco Corporation | 50 | $449.50 |

| 2 | 1843 | Cost Cutter's | 100 | $599.00 |

| 3 | 1843 | Minimart Inc. | 3 | $15,597.00 |

| 4 | 1843 | Barco Corporation | 1 | $5,129.00 |

| 5 | 1843 | Ely Corp. | 10 | $299.50 |

| 6 | 0177 | Food Unlimited | 100 | $699.00 |

| 7 | 0177 | Shop and Drop | 100 | $899.00 |

| 8 | 1843 | Cost Cutter's | 1 | $9,109.00 |

| 9 | 9888 | Cost Cutter's | 50 | $299.50 |

### 14.5 控制列表中显示的的观测值

你也可以通过在过程中包含一个 `WHERE` 语句来控制哪些观测值出现在列表中。例如，假设你想让列表仅包含数量（`Quantity`）大于 400 的观测值。使用下面的技巧可以实现这一目标：

### 程序 14.5：控制在列表中显示的观测值（WHERE 语句）

```
title "Listing of Sales with Quantities Greater than 400";
proc print data=Learn.Sales;
where Quantity gt 400;
id EmPID;
var Customer Quantity TotalSales;
format TotalSales dollar10.2 Quantity comma7;
run;
```

图 14.5：程序 14.5 的输出

| EmpID | Customer | Quantity | TotalSales |

|---|---|---|---|

| 9888 | Pet's are Us | 1,000 | $1,990.00 |

| 0017 | Roger's Spirits | 500 | $19,995.00 |

假设你想查看两个员工（1843 和 0177）的销售情况。在 `WHERE` 语句中使用 `IN` 运算符是一种非常方便的方法，如程序 14.6 所示。

### 程序 14.6：在 WHERE 语句中使用 IN 运算符

```
title "Listing of Sales from Employees 1843 and 0177";
proc print data=Learn.Sales;
where EmPID in ('1843','0177');
id EmPID;
var Customer Quantity TotalSales;
format TotalSales dollar10.2 Quantity comma7;
run;
```

224 实例学习 SAS：程序员指南，第二版

你可以对数值值或字符值使用 `IN` 运算符。你还可以选择用空格或逗号分隔列表中的值。以下是程序 14.6 的输出：

图 14.6：程序 14.6 的输出

| Listing of Sales from Employees 1843 and 0177 | | | |

| EmpID | Customer | Quantity | TotalSales |

|---|---|---|---|

| 1843 | Barco Corporation | 50 | $449.50 |

| 1843 | Cost Cutter's | 100 | $599.00 |

| 1843 | Minimat Inc. | 3 | $15,597.00 |

| 1843 | Barco Corporation | 1 | $5,129.00 |

| 1843 | Ely Corp. | 10 | $299.50 |

| 0177 | Food Unlimited | 100 | $699.00 |

| 0177 | Shop and Drop | 100 | $899.00 |

| 1843 | Cost Cutter's | 1 | $9,109.00 |

| 0177 | Minimat Inc. | 5 | $52.00 |

| 0177 | Barco Corporation | 2 | $20,000.00 |

| 1843 | Minimat Inc. | 3 | $15,597.00 |

### 14.6 为你的列表添加标题和脚注

你可以通过添加额外的标题行以及为列表添加一个或多个脚注，让你的输出更有意义。`TITLE` 语句（其中 *n* 是 1 到 10 之间的数字）允许你指定多个标题行。注意 `TITLE1` 和 `TITLE2` 是等价的。`FOOTNOTE*n*` 允许你指定 1 到 10 个脚注，即出现在页面底部的行。请记住，一旦发布了 `TITLE` 或 `FOOTNOTE` 语句，标题或脚注就会出现在输出的每一页上，直到你更改或取消它们。

短程序列出了 Sales 数据并添加了几个标题和脚注行：

### 程序 14.7：为你的列表添加标题和脚注

```
title1 "The XYZ Company";
title3 "Sales Figures for Fiscal 2017";
title4 "Prepared by Roger";
title5 "----------------------"
footnote "All sales Figures are Confidential"

proc data=Learn;
  id EmpID;
  var Customer Quantity TotalSales;
  format TotalSales dollar10.2 Quantity comma7;
run;
```

首先我们显示列表，然后是解释：

图 14.7：程序 14.7 的部分输出 (img/6f22e781b7ad99a8ef00cc7e22e7e0236_0) 由于缺少 TITLE 语句，第一行和第三行标题之间有一个空行。如果你提交一个 `TITLEn` 语句，它将替换当前的 `TITLEn` 语句以及更高的 *n* 值。例如，你更改程序 14.7 中的 `TITLE3` 行：

```
title3 "New Sales Figures for 2017";
```

现在你提交不带任何之前标题行的 `PROC PRINT`，你的输出如下如下：

图 14.8：新标题 (img/6f22e781b7ad99a8ef00cc7e22e7e0236_1) 第 3 行被新文本替换，第 4 和第 5 行被删除。`FOOTNOTE` 语句的操作方式相同。要取消所有标题，使用以下代码：

```
title;
```

以类似的方式，使用以下代码取消所有脚注：

```
footnote;
```

### 14.7 更改列表顺序

如果你想按特定顺序查看列表，可以在 `PROC PRINT` 之前使用 `PROC SORT`。如果你想按 `TotalSales` 排序查看列表，可以使用以下程序：

### 程序 14.8：使用 PROC SORT 更改观测值顺序

```
proc sort data=Learn.Sales;
by TotalSales;
run;

title "Listing of Sales - Sorted by TotalSales";
proc print data=Learn.Sales;
id EmID;
var Customer Quantity TotalSales;
format TotalSales dollar10.2 Quantity comma7;
run;
```

你的列表现在按 `TotalSales` 从低到高排序。

图 14.9：程序 14.8 的输出

| EmpID | Customer | Quantity | TotalSales |

|---|---|---|---|

| 0177 | Minimart Inc. | 5 | $52.00 |

| 1843 | Ely Corp. | 10 | $299.50 |

| 9888 | Cost Cutter's | 50 | $299.50 |

| 1843 | Barco Corporation | 50 | $449.50 |

| 1843 | Cost Cutter's | 100 | $599.00 |

| 0177 | Food Unlimited | 100 | $699.00 |

| 0177 | Shop and Drop | 100 | $899.00 |

| 9888 | Pet's are Us | 1,000 | $1,990.00 |

| 0177 | Spirited Spirits | 100 | $1,995.00 |

| 1843 | Barco Corporation | 1 | $5,129.00 |

| 1843 | Cost Cutter's | 1 | $9,109.00 |

| 1843 | Minimart Inc. | 3 | $15,597.00 |

| 1843 | Minimart Inc. | 3 | $15,597.00 |

| 0177 | Roger's Spirits | 500 | $19,995.00 |

| 0177 | Barco Corporation | 2 | $20,000.00 |

若要从高到低查看列表，在变量名（`TotalSales`）之前加上 `DESCENDING` 关键字，如下：

### 程序 14.9：演示 PROC SORT 的 DESCENDING 选项

```
proc sort data=Learn.Sales;
by descending TotalSales;
run;
```

在程序 14.8 中，你用一个按 `TotalSales` 排序的数据集替换了原始 SAS 数据。在某些情况下，这是可以的。然而，如果你不想更改原始数据集，请在排序时添加 `OUT=` 来指定输出数据集。这在你执行排序时对数据进行子集划分时尤为重要。例如，下面的程序创建了按 `TotalSales` 降序排列的临时数据集（sets）：

### 程序 14.10：对永久数据集排序并创建临时输出数据集

```
proc sort data=Learn, out=Sales;
by descending TotalSales;
run;
```

注意，SAS 正在读取你的永久 SAS 数据集（`Sales`）并创建一个临时 SAS 数据（`Sales`）。只要它们位于不同的库，为它们使用相同的名称是可以的。

### 14.8 按多个变量排序

你可以按多个变量对数据排序。这被称为多级排序。例如，下面的 `PROC SORT` 语句按 ID 排序数据，并在每个 ID 内按销售总额降序排列：

### 程序 14.11：按多个变量排序
