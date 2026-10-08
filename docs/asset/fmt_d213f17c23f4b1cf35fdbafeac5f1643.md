
## 扩展对数组的使用

### 在 ARRAY 语句中创建变量

到为止，你已经学习了在 `ARRAY` 语句中引用现有变量的方法。你还可以通过省略语句中的数组元素在 `ARRAY` 语句中创建变量。如果你不引用现有变量，SAS 会为你创建新变量并为它们分配默认名称。这些

# 扩展你的数组用法 493

默认名称是数组名，后跟从 1 到数组维度的连续数字。

创建新变量的 `ARRAY` 语句通用形式为：
`ARRAY array-name[dimension];`

其中

- `array-name` 指定数组名称。
- `dimension` 描述数组元素的数量和排列。

接下来，假设你想计算健身班中每个成员每周的体重增加或减少，如下所示：

SAS 数据集 Hrd Convert

| Name | Weight1 | Weight2 | Weight3 | Weight4 | Weight5 | Weight6 |
|---|---|---|---|---|---|---|
| Alicia | 153.4 | 151.9 | 151.7 | 148.6 | 145.5 | 145.9 |
| Betsy | 116.0 | 116.0 | 114.0 | 111.1 | 109.8 | 108.2 |
| Brenda | 151.2 | 149.0 | 147.7 | 146.4 | 145.1 | 143.7 |
| Carl | 149.0 | 146.8 | 145.5 | 144.2 | 142.9 | 141.5 |
| Carmela | 140.2 | 137.8 | 136.5 | 135.4 | 134.0 | 128.3 |

你想创建变量来计算这些差异。为了执行计算，你首先将变量 `Weight1` 到 `Weight6` 分组为一个数组。

```
data hr.diff;

set hr.convert;

array(6) weight1-weight6;
```

接下来，你想创建变量来存储这六个记录变量之间的差异。可以使用不带元素的 `ARRAY` 语句来创建新变量 `WgtDiff1` 到 `WgtDiff5`。

```
data hr.diff;

set hr.convert;

array(6) weight1-weight6;

array(5) wgtDiff1-wgtDiff5;
```

SAS 数据集 Hrd Convert

| Name | Weight1 | Weight2 | Weight3 | Weight4 | Weight5 | Weight6 |
|---|---|---|---|---|---|---|
| Alicia | 153.4 <-> 151.9 | <-> 151.7 <-> 148.6 <-> 145.5 <-> 145.9 |
| Betsy | 116.0 | 116.0 | 114.0 | 111.1 | 109.8 | 108.2 |
| Brenda | 151.2 | 149.0 | 147.7 | 146.4 | 145.1 | 143.7 |
| Carl | 149.0 | 146.8 | 145.5 | 144.2 | 142.9 | 141.5 |
| Carmela | 140.2 | 137.8 | 136.5 | 135.4 | 134.0 | 128.3 |

记住，在 `ARRAY` 语句中创建变量时，只要指定了数组中有多少个元素，就不需要指定数组元素。

```
array WgtDiff(5);
```

### 默认变量名

默认变量名通过拼接数组名和数字 1, 2, 3 等直到数组维度来创建。

```
array WgtDiff[5];

...

WgtDiff1 WgtDiff2 WgtDiff3 WgtDiff4 WgtDiff5
```

> 如果你愿意，可以指定单个变量名。要指定变量名，请将每个名称作为数组元素列出。以下 `ARRAY` 语句创建了数值变量 `Oct12`、`Oct19`、`Oct26`、`Nov02` 和 `Nov09`。

```
array WgtDiff[5] Oct12 Oct19 Oct26 Nov02 Nov09;

array WgtDiff[5];

...

Oct12 Oct19 Oct26 Nov02 Nov09
```

### 字符型变量数组

要创建一个字符型变量数组，在数组维度后添加一个美元符号 `$`。
`array firstName[5] $;`

默认情况下，在 `ARRAY` 语句中创建的所有字符型变量长度都为 8。你可以通过在美元符号后指定长度来分配自己的长度。
`array firstName[5] $ 24;`

你指定的长度会自动分配给 `ARRAY` 语句创建的所有变量。

在 DATA 步编译期间，此 `ARRAY` 语句创建的变量被添加到程序数据向量中并存储在生成的数据集中。

```
data hrd.diff;

set hrd.convert;

array wt(6) Weight1-Weight6;

array WgtDiff[5];
```

### 扩展你的数组用法

程序数据向量

| N | Name | Weight1 | Weight2 | Weight3 | Weight4 | Weight5 | Weight6 |
|---|---|---|---|---|---|---|---|
| WgtDiff1 | WgtDiff2 | WgtDiff3 | WgtDiff4 | WgtDiff5 | | | |
| |---|---|---|---|---|---|---|---|

在引用数组元素时，注意不要混淆数组引用 `WgtDiff[1]` 到 `WgtDiff[5]`（注意大括号）与变量名 `WgtDiff1` 到 `WgtDiff5`。下方的程序数据向量显示了数组引用与对应变量名之间的关系。程序数据向量

| Name | Weight1 | Weight2 | Weight3 | Weight4 | Weight5 | Weight6 |
|---|---|---|---|---|---|---|
| WgtDiff(1) | WgtDiff(2) | WgtDiff(3) | WgtDiff(4) | WgtDiff(5) | | |
| |---|---|---|---|---|---|---|
| WgtDiff1 | WgtDiff2 | WgtDiff3 | WgtDiff4 | WgtDiff5 | | |

现在你可以使用 DO 循环来计算每个记录重量之间的差异。注意 `WgtDiff[i]` 的每个值都是通过从 `wt[i]` 减去 `wt[i+1]` 计算得。通过操作索引变量，你可以轻松地引用任何数组元素。

```
data hrd.diff;

  set hrd.convert;

  array wt[6] weight1-weight6;

  array wgtDiff[5];

  do i=1 to 5;

    wgtDiff[i]=wt[i+1]-wt[i];

  end;
```

生成的数据集部分所示。SAS 数据集 Hrd.Diff

| Name | WgtDiff1 | WgtDiff2 | WgtDiff3 | WgtDiff4 | WgtDiff5 |
|---|---|---|---|---|---|
| Alicia | -1.542 | -2.206 | -3.086 | -3.064 | 0.409 |
| Betsy | 0.000 | -1.914 | -2.868 | -1.327 | -1.542 |
| Brenda | -1.276 | -1.376 | -1.376 | -1.376 | | |

# 给数组分配初始值

有时在定义数组时，为数组元素分配初始值是有用的。

```
array goal(4) g1 g2 g3 g4 (initial values);
```

在 `ARRAY` 语句中分配值：

2. 为每个数组指定一个值。
`array goal(4) g1 g2 g3 g4 (9000 9300 9600 9900);`

3. 用逗号或空格分隔每个值。
`array goal(4) g1 g2 g3 g4 (9000 9300 9600 9900);`

4. 将初始值括在括号内。
`array goal(4) g1 g2 g3 g4 (9000 9300 9600 9900);`

5. 用引号包含每个值。
`array col[3]('red','green','blue');`

可以在不指定每个元素的情况下为数组分配初始值。以下语句变量 `Var1`、`Var2`、`Var3` 和 `Var4`，并为它们分配初始值 1、2、3 和 4：

```
array Var(4)(1 2 3 4);
```

在这个示例中，你的任务是将 `Finance.Qsales` 数据集中的实际销售额与每个销售代表年初的销售目标进行比较。销售记录在 `Finance.Qsales` 中。

### Finance.Qsales 描述

| Variable | Type | Length |
|---|---|---|
| SalesRep | char | 8 |
| Sales1 | num | 8 |
| Sales2 | num | 8 |
| Sales3 | num | 8 |
| Sales4 | num | 8 |

下方的 DATA 步读取 `Finance.Qsales` 数据集以创建 `Finance.Report` 数据集。`ARRAY` 语句创建一个数组来处理每季的销售数据。

```
finance.report;

set finance.qsales;

array sale(4) sales1-sales4;
```

要比较销售额与销售目标，必须为销售目标创建变量并赋值。

```
finance.report;

set finance.qsales;

array sale(4) sales1-sales4;

array Goal(4) (9000 9300 9600 9900);
```

第三个 `ARRAY` 语句创建变量 `Achieved1` 到 `Achieved4` 以存储实际销售额与销售目标的比较。

```
data finance.report;

set finance.qsales;

array sale(4) sales1-sales4;

array Goal(4) (9000 9300 9600 9900);

array Achieved(4);

do i=1 to 4;

  achieved(i)=100*sale(i)/goal(i);

end;

run;
```

执行四次 DO 循环以计算 `achieved` 数组每个元素的值（百分比）。

```
data finance.report;

set finance.qsales;

array sale(4) sales1-sales4;

array Goal(4) (9000 9300 9600 9900);

array Achieved(4);

do i=1 to 4;

achieved(i)=100*sale(i)/goal(i);

end;

run;
```

在提交此 DATA 步之前，可以通过在 DATA 语句中设置 `DROP` 选项从新数据中删除索引变量。

```
data finance.report(drop=1);

set finance.qsales;

array sale(4) sales1-sales4;

array Goal(4) (9000 9300 9600 9900);

array Achieved(4);

do i=1 to 4;

achieved(i)=100*sale(i)/goal(i);

end;

run;
```

这是一个简单的表查找程序示例。生成的数据集包含了从 `Finance.Qsales` 读取的变量，加上用 `ARRAY` 语句创建的变量。

### SAS 数据集 Finance Report

| SalesRep | Sales1 | Sales2 | Sales3 | Sales4 | Goal1 | Goal2 |
|---|---|---|---|---|---|---|
| Britt | 8400 | 8800 | 9300 | 9800 | 9000 | 9300 |
| Fuchten | 9500 | 9300 | 9800 | 8900 | 9000 | 9300 |
| Goodyear | 9150 | 9200 | 9650 | 11000 | 9000 | 9300 |

| Goal4 | Achieved1 | Achieved2 | Achieved3 | Achieved4 |
|---|---|---|---|---|
| 9600 | 9900 | 93.333 | 94.624 | 96.875 |
| 9600 | 9900 | 105.556 | 100.000 | 102.083 |
| 9600 | 9900 | 101.667 | 98.925 | 100.521 |

# 临时数组元素

在 `ARRAY` 语句中分配了初始值的变量会自动保留。

变量 `Goal1` 到 `Goal4` 不应该存储在数据集中，因为它们仅用于计算 `Achieved1` 到 `Achieved4` 的值。下一个示例展示了如何创建临时数组元素。

要在不创建新变量的情况下为 DATA 步处理创建临时数组元素，请在数组名和维度之后指定 `_TEMPORARY_`。

```
data finance.report (drop-i);

set finance.qsales;

array sale(4) sales1-sales4;

array goal(4) _temporary_ (9000 9300 9600 9900);

array achieved(4);

do i=1 to 4;

achieved(i)=100*sale(i)/goal(i);

end;
```

临时数组元素不会出现在生成的数据集中。

### SAS 数据集财务报表

| 销售员 | Sales1 | Sales2 | Sales3 | Sales4 |
|---|---|---|---|---|
| Britt | 8400 | 8800 | 9300 | 9800 |
| Fruchten | 9500 | 9300 | 9800 | 8900 |
| Goodyear | 9150 | 9200 | 9650 | 11000 |

| Achieved1 | Achieved2 | Achieved3 | Achieved4 |
|---|---|---|---|
| 93.333 | 94.624 | 96.875 | 98.990 |
| 105.556 | 100.000 | 102.083 | 89.899 |
| 101.667 | 98.925 | 100.521 | 111.111 |

当数组仅用于执行计算时，临时数组元素非常有用。你可以通过临时数组元素提高性能。

# 理解多维数组

到此为止，你已经学习了如何将变量分组为一维数组。你还可以将变量分组为类似于表格的结构，称为多维数组。本节将教授如何定义和使用二维数组，这是多维数组的一种常见类型。

假设你想编写一个 DATA 步来比较测验的回答与正确答案。由于每个问题只有一个正确答案，这是一个简单的对一比较。

- Respl1 -> Answer1
- Respl2 -> Answer2
- Respl3 -> Answer3
- Respl4 -> Answer4

然而，如果每个问题有多个正确答案，你必须将每个回答与每个可能的正确答案进行比较，以确定是否存在匹配。

```
Resp1 -> Answer1 Answer2 Answer3

Resp2 -> Answer4 Answer5 Answer6

Resp3 -> Answer7 Answer8 Answer9

Resp4 -> Answer10 Answer11 Answer12
```

通过将变量分组为二维数组，你可以更容易地处理数据。就像你可以将一维数组视为单行变量一样，例如所示...

```
Answer1 Answer2 Answer3 Answer4 ... Answer9 Answer10 Answer11 Answer12

... 你也可以将二维数组看作多行变量。
```

```
Answer1 Answer2 Answer3

Answer4 Answer5 Answer6

Answer7 Answer8 Answer9

Answer10 Answer11 Answer12
```

### 定义多维数组

要定义多维数组，你需要指定每个维度中的元素数量，并用逗号分隔。此 `ARRAY` 语句定义了一个二维数组：

```
array new[3,4] x1-x12;
```

在二维数组中，两个维度可以被视为行和列的表格。

```
array new(r,c) x1-x12;
```

| | x1 | x2 | x3 | x4 |
|---|---|---|---|---|
| 行 | x5 | x6 | x7 | x8 |
| | x9 | x10 | x11 | x12 |

`ARRAY` 语句中的第一个维度指定行数。

```
array new(3,4) x1-12;
```

| | x1 | x2 | x3 | x4 |
|---|---|---|---|---|
| 行 | x5 | x6 | x7 | x8 |
| | x9 | x10 | x11 | x12 |

第二个维度指定列数。

```
array new(3,4) x1-12;
```

# 列

| x1 | x2 | x3 | x4 |
| x5 | x6 | x7 | x8 |
| x9 | x10 | x11 | x12 |

你可以通过指定两个维度来引用数组的任何元素。在示例中，通过指定数组 `new(2,3)` 对 `x7` 执行操作。你可以通过查找行 (2) 然后列 (3) 来定位表格中的数组元素。

```
array new[3,4] x1-12;

new(2,3)=x7;
```
