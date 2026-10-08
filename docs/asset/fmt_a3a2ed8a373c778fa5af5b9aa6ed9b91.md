
| x1 | x2 | x3 | x4 |
| x5 | x6 | x7 | x8 |
| x9 | x10 | x11 | x12 |

当你定义二维数组时，数组元素按照在 `ARRAY` 语句中列出的顺序分组。例如，数组元素 `x1` 到 `x4` 可以视为表格的第一行。

```
array new[3,4] x1 x2 x3 x4 x5 x6 x7 x8 x9 x10 x11 x12;
```

| x1 | x2 | x3 | x4 |
| x5 | x6 | x7 | x8 |
| x9 | x10 | x11 | x12 |

元素 `x5` 到 `x8` 变成第二行，依此类推。

# 引用二维数组元素

多维数组通常配合嵌套循环使用。下一个示例使用一维数组、二维数组和嵌套 `DO` 循环来重组变量。

你公司的销售数据按月存储在 `Monthly` 数据集中。你的任务是生成一个季度销售数据集而不是月销售数据集。

| 变量 | 类型 |
|---|---|
| Year | num |
| Month1 | num |
| Month2 | num |
| Month3 | num |
| Month4 | num |
| Month5 | num |
| Month6 | num |
| Month7 | num |
| Month8 | num |
| Month9 | num |
| Month10 | num |
| Month11 | num |
| Month12 | num |

定义数组 `m(4,3)` 将变量 `Month1` 到 `Month12` 分为四组，每组三个月。

| Month1 | Month2 | Month3 |
| Month4 | Month5 | Month6 |
| Month7 | Month8 | Month9 |
| Month10 | Month11 | Month12 |

```
data finance.quarters;

set finance.monthly;

array(4,3) month1-12;
```

定义数组 `Qtr[4]` 创建数值变量 `Qtr1`, `Qtr2`, `Qtr3`, `Qtr4`，它们将用于存储每个季度的销售额。

```
data finance.quarters;

set finance.monthly;

array(4,3) month1-12;

array Qtr[4];
```

使用嵌套 `DO` 循环来引用 `Qtr1` 到 `Qtr4` 的值。变量 `Month1` 到 `Month12` 以及变量 `i` 和 `j` 用于循环处理；`DROP` 选项将它们从 `Finance.Quarters` 数据集中排除。

```
data finance.quarters(drop=i j);

set finance.monthly;

array(4,3) month1-12;

array Qtr[4];
```

# 使用数组处理变量

```
do i=1 to 4;

qtr(i)=0;

do j=1 to 3;

qtr(i)+m(i,j);

end;

run;
```

`Qtr` 数组中的每个元素代表 `m` 数组中一行的和。`Qtr` 数组中的元素数量应该匹配 `m` 数组的第一个维度（即 `m` 数组的行数）。第一个 `DO` 循环为 `Qtr` 数组的每个元素执行一次。

赋值语句 `qtr(i)=0` 在第一个 `DO` 循环的每次迭代后将 `qtr(i)` 的值设置为零。如果没有赋值语句，由于循环内 `qtr(i)+m[i,j]` 求和，`Q1`、`Q2`、`Q3` 和 `Q4` 的值将在 `DATA` 步的迭代中累积。

```
data finance.quarters(drop=i j);

set finance.monthly;

array m(4,3) month1-12;

array Qtr[4];

do i=1 to 4;

qtr(i)=0;

do j=1 to 3;

qtr(i)+m(i,j);

end;

run;
```

第二个 `DO` 循环执行的次数与 `m` 数组的第二个维度相同（即 `m` 数组每行的列数）。

## 504 第15章 使用数组处理变量

```sas
array m[4,3] month1-month12;

array Qtr(4);

do i=1 to 4;

  qtr(i)=0;

  do j=1 to 3;

    qtr(i)=qtr(i)+m[i,j];

  enddo;
```

程序数据向量 (Program Data Vector)

| N | Year | Month1 | Month2 | Month3 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1999 | 23000 | 21500 | 24600 | 44500 | | | | 1 | 2 |

嵌套 `DO` 循环继续执行，直到索引变量 `j` 超过停止值。当嵌套 `DO` 循环执行完毕时，第一季度的总销售额 `Qtr1` 已经计算完毕。

```sas
data finance.quarters(drop=i j);

set finance.monthly;

array m(4,3) month1-month12;

array Qtr(4);

do i=1 to 4;

  qtr(i)=0;

  do j=1 to 3;

    qtr(i)=qtr(i)+m[i,j];

  enddo;
```

程序数据向量 (Program Data Vector)

| N | Year | Month1 | Month2 | Month3 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1999 | 23000 | 21500 | 24600 | 69100 | | | | 1 | 4 |

外部 `DO` 循环将 `i` 增加到 2，该过程继续对数组 `m` 的元素 `Month4` 到 `Month6` 进行处理。

```sas
data finance.quarters(drop=i j);

set finance.monthly;

array m(4,3) month1-month12;

array Qtr(4);

do i=1 to 4;

  qtr(i)=0;

  do j=1 to 3;

    qtr(i)=qtr(i)+m[i,j];

  enddo;
```

程序数据向量 (Program Data Vector)

| N | Month2 | Month3 | Month4 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 21500 | 24600 | 23300 | 69100 | 23300 | | | 2 | 1 |

## 额外功能

当外部 `DO` 循环执行完成后，到达 `DATA` 步的末尾，第一个观测值被写入 `Finance.Quarters` 数据集中。

```sas
data finance.quarters(drop= j);

set finance.monthly;

  array m(4,3) month1-month12;

  array Qtr(4);

do i=1 to 4;

    i=5 (loop ends)

    qtr(i)=0;

    j=1 to 3;

    qtr(i)=m{i,j};

  end;

run;
```

程序数据向量 (Program Data Vector)

| | Month2 | Month3 | Month4 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 21500 | 24600 | 23300 | 69100 | 64400 | 69200 | 71800 | 5 | 4 |

你目前所看到的代表了 `DATA` 步的第一次迭代。`Finance.Monthly` 数据集中的观测值以相同的方式处理。以下是生成的数据集的一部分，包含了按季度分组的销售额。

`SAS` 数据集 `Finance Quarters`（部分列出）

| Year | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 1989 | 69100 | 64400 | 69200 | 71800 |
| 1990 | 73100 | 72000 | 83200 | 82800 |
| 1991 | 73400 | 81800 | 85200 | 87800 |

## 额外功能

你已经看到了数组的多种用法，包括创建变量、执行重复计算以及执行表查找。你还可以使用数组来旋转（转置）`SAS` 数据集。

当你旋转 `SAS` 数据集时，你将变量转换为观测值或将观测值转换为变量。例如，假设你想旋转 `Finance.Funddrive` 数据集，为每个输入观测值创建四个输出观测值。

## 第15章 • 使用数组处理变量

| LastName | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| ADAMS | 18 | 18 | 20 | 20 |
| ALEXANDE | 15 | 18 | 15 | 10 |
| APPLE | 25 | 25 | 25 | 25 |
| ARTHURTHUR | 10 | 25 | 20 | 30 |
| AVERY | 15 | 15 | 15 | 15 |
| BAREFOOT | 20 | 20 | 20 | 20 |
| BAUCOM | 25 | 20 | 5 | 30 |
| BLAIR | 10 | 10 | 5 | 10 |
| BLALOCK | 5 | 10 | 10 | 15 |
| BOSTIC | 20 | 25 | 30 | 25 |
| BRADLEY | 12 | 16 | 14 | 18 |
| BRADY | 20 | 20 | 20 | 20 |
| BROWN | 18 | 18 | 18 | 18 |
| BRYANT | 16 | 18 | 20 | 18 |
| BURNETTE | 10 | 10 | 10 | 10 |
| CHEUNG | 30 | 30 | 30 | 30 |
| LEHMAN | 20 | 20 | 20 | 20 |
| VALADEZ | 14 | 18 | 25 | |

以下程序旋转数据集并列出新数据集的前16个观测值。

```sas
data work.rotate(drop=qtr);

set finance.funddrive;

array contrib(4) qtr1-qtr4;

do qtr=1 to 4;

  Amount=contrib(qtr);

  output;

end;

run;

proc print data=rotate(obs=16);

run;
```

## 总结

| Name | Qtr | Amount |
|---|---|---|
| ADAMS | 1 | 18 |
| ADAMS | 2 | 18 |
| ADAMS | 3 | 20 |
| ADAMS | 4 | 20 |
| ALEXANDER | 1 | 15 |
| ALEXANDER | 2 | 18 |
| ALEXANDER | 3 | 15 |
| ALEXANDER | 4 | 10 |
| APPLE | 1 | 25 |
| APPLE | 2 | 25 |
| APPLE | 3 | 25 |
| APPLE | 4 | 25 |
| ARTHURTHUR | 1 | 10 |
| ARTHURTHUR | 2 | 25 |
| ARTHURTHUR | 3 | 20 |
| ARTHURTHUR | 4 | 30 |
| AVERY | 1 | 15 |
| AVERY | 2 | 15 |
| AVERY | 3 | 15 |
| AVERY | 4 | 15 |
| BAREFOOT | 1 | 20 |
| BAREFOOT | 2 | 20 |
| BAREFOOT | 3 | 20 |
| BAREFOOT | 4 | 20 |
| BAUCOM | 1 | 25 |
| BAUCOM | 2 | 20 |
| BAUCOM | 3 | 5 |
| BAUCOM | 4 | 30 |
| BLAIR | 1 | 10 |
| BLAIR | 2 | 10 |
| BLAIR | 3 | 5 |
| BLAIR | 4 | 10 |
| BLALOCK | 1 | 5 |
| BLALOCK | 2 | 10 |
| BLALOCK | 3 | 10 |
| BLALOCK | 4 | 15 |
| BOSTIC | 1 | 20 |
| BOSTIC | 2 | 25 |
| BOSTIC | 3 | 30 |
| BOSTIC | 4 | 25 |
| BRADLEY | 1 | 12 |
| BRADLEY | 2 | 16 |
| BRADLEY | 3 | 14 |
| BRADLEY | 4 | 18 |
| BRADY | 1 | 20 |
| BRADY | 2 | 20 |
| BRADY | 3 | 20 |
| BRADY | 4 | 20 |
| BROWN | 1 | 18 |
| BROWN | 2 | 18 |
| BROWN | 3 | 18 |
| BROWN | 4 | 18 |
| BRYANT | 1 | 16 |
| BRYANT | 2 | 18 |
| BRYANT | 3 | 20 |
| BRYANT | 4 | 18 |
| BURNETTE | 1 | 10 |
| BURNETTE | 2 | 10 |
| BURNETTE | 3 | 10 |
| BURNETTE | 4 | 10 |
| CHEUNG | 1 | 30 |
| CHEUNG | 2 | 30 |
| CHEUNG | 3 | 30 |
| CHEUNG | 4 | 30 |
| LEHMAN | 1 | 20 |
| LEHMAN | 2 | 20 |
| LEHMAN | 3 | 20 |
| LEHMAN | 4 | 20 |
| VALADEZ | 1 | 14 |

## 总结

### 数组的目的

嵌套 `DO` 循环继续执行，直到索引变量 `j` 超过停止值。当嵌套 `DO` 循环执行完毕时，第一季度的总销售额 `Qtr1` 已经计算完毕。

```sas
data finance.quarters(drop=i j);

set finance.monthly;

array m(4,3) month1-month12;

array Qtr(4);

do i=1 to 4;

  qtr(i)=0;

  do j=1 to 3;

    qtr(i)=qtr(i)+m[i,j];

  enddo;
```

程序数据向量 (Program Data Vector)

| N | Year | Month1 | Month2 | Month3 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1999 | 23000 | 21500 | 24600 | 69100 | | | | 1 | 4 |

外部 `DO` 循环将 `i` 增加到 2，该过程继续对数组 `m` 的元素 `Month4` 到 `Month6` 进行处理。

```sas
data finance.quarters(drop=i j);

set finance.monthly;

array m(4,3) month1-month12;

array Qtr(4);

do i=1 to 4;

  qtr(i)=0;

  do j=1 to 3;

    qtr(i)=qtr(i)+m[i,j];

  enddo;
```

程序数据向量 (Program Data Vector)

| N | Month2 | Month3 | Month4 | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | j |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 21500 | 24600 | 23300 | 69100 | 23300 | | | 2 | 1 |

## 额外功能

当外部 `DO` 循环执行完成后，到达 `DATA` 步的末尾，第一个观测值被写入 `Finance.Quarters` 数据集中。

```sas
data finance.quarters(drop= j);

set finance.monthly;

  array m(4,3) month1-month12;

  array Qtr(4);

do i=1 to 4;

    i=5 (loop ends)

    qtr(i)=0;

    j=1 to 3;

    qtr(i)=m{i,j};

  end;

run;
```
