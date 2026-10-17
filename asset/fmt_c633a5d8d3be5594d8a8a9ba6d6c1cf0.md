
`FILENAME` `'filename'`;

`DATA` `data-set`;

  `INFILE` `file-specification` `MISSO`;

  `INPUT` `id-variable` `@`;

  `counter-variable`=0;

  `DO` `WHILE` (`expression`);

    `counter-variable`+1;

    `OUTPUT`;

    `INPUT` `repeating-variable` `@`;

`END`;

```

## 示例程序

### 重复数据块
```sas

`LIBNAME` `'weather'`;

`FILENAME` `'tempdata'`;

`DATA` `data.perm.april`;

`INFILE` `tempdata`;

`INPUT` `Date` : `@@`;

```

### ID 字段后跟随相同数量的重复字段
```sas

`LIBNAME` `'sales'`;

`FILENAME` `'sales97'`;

`DATA` `data.perm.97`;

`INFILE` `data97`;

`INPUT` `ID` `$` `@`;

`DO` 1 `to` 4;

  `INPUT` `Sales` : `@`;

  `OUTPUT`;

`END`;

```

### ID 字段后跟随不同数量的重复字段
```sas

`LIBNAME` `'sales'`;

`FILENAME` `'sales97'`;

`DATA` `data.perm.97`;

`INFILE` `data97` `MISSO`;

`INPUT` `ID` `$` `@`;

`quarter`=0;

`DO` `WHILE` (`sales` `ne` `.`);

  `quarter`+1;

  `OUTPUT`;

`END`;

```

## 注意事项
- 双重尾随符号 (`@@`) 在 `DATA` 步的多次迭代中保持记录，直到到达记录末尾。
- 单个尾随符号 (`@`) 在控制返回 `DATA` 步顶部时释放记录。
- 使用 `END` 语句完成 `DO` 循环和 `DO WHILE` 循环。

## 测验
为每个问题选择最佳答案。

1. 关于双重尾随符号 (`@@`) 的哪项描述是正确的？
   a. 它允许下一个 `INPUT` 语句在 `DATA` 步的多次迭代中读取当前记录。
   b. 它必须是 `INPUT` 语句中的最后一个项。
   c. 当输入指针移过记录末尾时，它会被释放。
   d. 以上所有。

2. 被单个尾随符号 (`@`) 保持的记录会在会自动释放：
   a. 输入指针移过记录末尾时。
   b. `DATA` 步的下次迭代开始时。
   c. 另一个 `INPUT` 语句执行观测值时。

3. 哪一个 SAS 程序为每个数据块创建一个单独的观测值？

图 2.45 原始数据文件
| | | | | | |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | 20 | 30 | 40 |
| 1001 | apple | banana | cherry | guava |
| 1005 | kiwi | papaya | | |
| 1007 | pineapple | raspberry | strawberry | | |

   a. `data.perm.produce`;
   `infile` `fruit`;
   `input` `Item` `$` : `$10.`;
   b. `data.perm.produce`;
   `infile` `fruit`;
   `input` `Item` `$` : `$10.` `@`;
   c. `data.perm.produce`;
   `infile` `fruit`;
   `input` `Item` `$` : `$10.` `@@`;
   d. `data.perm.produce`;
   `infile` `fruit` `@@`;
   `input` `Item` `$` : `$10.`;

4. 哪一个 SAS 程序读取 ID 的值并为每个 Quantity 的值保持记录，从而每条记录创建三个观测值？

## 从单条记录创建多个观测值

图 20.46 原始数据文件
| | | | | | |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | 20 | 30 | |
| 2101 | 208 | 19047 | 22890 | |
| 2102 | 1775 | 20214 | 22654 | |
| 2103 | 1763 | 22927 | 21862 | |

   a. `data work.sales`;
   `infile unitsold`;
   `input ID $`;
   `DO week=1 to 3`;
     `input Quantity : ,`;
     `OUTPUT`;
   `END`;
   `RUN`;
   b. `data work.sales`;
   `infile unitsold`;
   `input ID $ @ @`;
   `DO week=1 to 3`;
     `input Quantity : ,`;
     `OUTPUT`;
   `END`;
   `RUN`;
   c. `data work.sales`;
   `infile unitsold`;
   `input ID $ @`;
   `DO week=1 to 3`;
     `input Quantity : ,`;
     `OUTPUT`;
   `END`;
   `RUN`;
   d. `data work.sales`;
   `infile unitsold`;
   `input ID $ @`;
   `DO week=1 to 3`;
     `input Quantity : ,.`;
     `OUTPUT`;
   `END`;
   `RUN`;

5. 哪一个 SAS 语句在名为 `ranges` 的索引变量值范围于 1 到 50 且增量为 5 时重复执行几个语句？
   a. `do count=1 to 50 by 5`;
   b. `do while count=1 to 50 by 5`;
   c. `do count=1 to 50 + 5`;
   d. `do while (count=1 to 50 + 5)`;

6. 下面哪个选项在 `DATA` 步中使用时，会在读取完每个 Activity 值后将一个观测值写入数据集？
   a. `do choice=1 to 3`;
     `input Activity : $10. @`;
     `OUTPUT`;
   `END`;
   b. `do choice=1 to 3`;
     `input Activity : $10. @`;
     `OUTPUT`;
   c. `do choice=1 to 3`;
     `input Activity : $10. @`;
   `OUTPUT`;

7. a 和 b 都是。

8. 哪一个 SAS 语句在 `Cholesterol` 的值大于 200 时重复执行几个语句？
   a. `do cholesterol > 200`;
   b. `do cholesterol gt 200`;
   c. `do while (cholesterol > 200)`;
   d. `do while cholesterol > 200`;

9. 下面哪个选项是 `sum` 语句的示例？
   a. `totalpay=1`;
   b. `totalpay+1`;
   c. `totalpay. 1`;

10. 哪一个程序从下面的原始文件创建 `Perm.store` 数据集？

图 20.47 原始数据文件
| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | 20 | 30 | |
| 1001 | 63 | 80 | 75 | 27 |
| 1002 | 112 | 45 | 98 | 10 |
| 1003 | 85 | 26 | 33 | |

# 原始数据文件

```

1----+10----+----20

P 1095

C 01-08-89  $45.0

C 01-17-89  $37.5

P 1096

C 01-09-89  $156.5

P 1097

C 01-02-89  $109.0

P 1099

C 01-03-89  $45.0

C 01-05-89  $45.0

P 1201

C 01-05-89  $37.0

C 01-10-89  $45.0

```

你可以通过为每个详细记录创建一个观测值，并保留头记录中的患者 ID，从层次化文件中构建 SAS 数据集。

## SAS 数据集

| 观测 | ID | 日期 | 金额 |
|---|---|---|---|
| 1 | 1095 | 01/08/89 | $45.00 |
| 2 | 1095 | 01/17/89 | $37.50 |
| 3 | 1096 | 01/09/89 | $156.50 |
| 4 | 1097 | 01/02/89 | $109.00 |
| 5 | 1099 | 01/03/89 | $45.00 |
| 6 | 1099 | 01/05/89 | $45.00 |
| 7 | 1201 | 01/05/89 | $37.00 |
| 8 | 1201 | 01/10/89 | $45.00 |

你也可以通过为每个头记录创建一个观测值，并将详细记录中的信息合并为汇总变量，从层次化文件中构建 SAS 数据集。

## SAS 数据集

| 观测 | ID | 总计 |
|---|---|---|
| 1 | 1095 | $82.50 |
| 2 | 1096 | $156.50 |
| 3 | 1097 | $109.00 |
| 4 | 1099 | $90.00 |
| 5 | 1201 | $82.00 |

在本章中，你将学习如何从层次化文件中读取数据，并创建一个包含每个详细记录对应一个观测值或每个头记录对应一个观测值的 SAS 数据集。

# 为每个详细记录创建一个观测值 649

# 目标

在本章中，你将学习到：

- 保留变量的值
- 条件地执行 SAS 语句
- 确定何时正在处理最后一个观测值
- 条件地执行多个 SAS 语句。

你还可以回顾如何：

- 使用 `linehold` 指定符来保留当前记录
- 显式地将观测值写入数据集。

# 为每个详细记录创建一个观测值

## 概述

为了实现每个详细记录创建一个观测值，有必要区分头记录和详细记录。拥有一个标识记录类型的字段会让此任务变得更容易。

在下面显示的部分数据文件 `Census` 中，`H` 表示包含街道地址的头记录，`P` 表示包含在该地址居住人员信息的详细记录。

```

Raw Data File

|-----+----10----+-------|

H 321 S. MAIN ST

nP MARY E 21 F

PWILLIAM M 23 M

PUSAN K 3 F

H 324 S. MAIN ST

P THOMAS H 79 M

PWALTER S 46 M

PALICE A 42 F

MARYANN A 20 F

JOHN S 16 M

H 325A S. MAIN ST

```

让我们看看如何创建一个包含每个居住在特定地址的人员对应观测值的数据集。

# 第 21 章 • 读取层次化文件

## SAS 数据集

| 观测 | 地址 | 姓名 | 房龄 | 性别 |
|---|---|---|---|---|
| 1 | 321 S. MAIN ST | MARY E | 21 | F |
| 2 | 321 S. MAIN ST | WILLIAM M | 23 | M |
| 3 | 321 S. MAIN ST | SUSAN K | 3 | F |
| 4 | 324 S. MAIN ST | THOMAS H | 79 | M |
| 5 | 324 S. MAIN ST | WALTER S | 46 | M |
| 6 | 324 S. MAIN ST | ALICE A | 42 | F |
| 7 | 324 S. MAIN ST | MARYANN A | 20 | F |
| 8 | 324 S. MAIN ST | JOHN S | 16 | M |

# 654 第 21 章 • 读取分级文件

```

>------10------+

H 321 S. MAIN ST

NP MARY E 21 F

NP WILLIAM M 23 M

NP SUSAN K 3 F

H 324 S. MAIN ST

```

| 保留 (Retain) | 丢弃 (Drop) | 地址 | 姓名 | 年龄 | 性别 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 321 S. MAIN ST | | | | | |

第二次迭代开始，输入指针移动到下一个记录并读取一个新的类型值。IF-THEN 语句表示的条件不成立，因此不执行 THEN 关键字之后的语句。

```

>------10------+

H 321 S. MAIN ST

NP MARY E 21 F

NP WILLIAM M 23 M

NP SUSAN K 3 F

H 324 S. MAIN ST

```

| 保留 (Retain) | 丢弃 (Drop) | 地址 | 姓名 | 年龄 | 性别 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 321 S. MAIN ST | P | | | | |

现在，子集 IF 语句检查条件 `type='P'`。在这次迭代中，条件为真，因此最后的 `INPUT` 语句读取姓名、年龄和性别的值。

```

>------10------+

H 321 S. MAIN ST

NP MARY E 21 F

NP WILLIAM M 23 M

NP SUSAN K 3 F

H 324 S. MAIN ST

```

| 保留 (Retain) | 丢弃 (Drop) | 地址 | 姓名 | 年龄 | 性别 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 321 S. MAIN ST | P | MARY E | 21 | | |

然后，程序数据向量中的值被写入第一个观测值，控制返回到 `DATA` 步的顶部。注意，类型的值没有包含在内。

## 为每个详细记录创建一个观测值 655

![](img/d8531a787915cd75227275234ea33bae_667_0.png)

随着执行的继续，第三个和第四个记录产生了观测值。然而，注意第五个记录是一个头记录。在第五次迭代中，条件 'H' 为真，一个新的地址被读取到程序数据向量中，覆盖了之前的值。

![](img/d8531a787915cd75227275234ea33bae_667_1.png)

## 显示您的结果

当执行阶段完成后，您可以使用 `PRINT` 过程显示数据集。将显示前 10 个观测值。

第 21 章 • 读取分级文件

图 21.1 `PRINT` 过程输出

| 观测值 (Obs) | 地址 | 姓名 | 年龄 性别 |
| :--- | :--- | :--- | :--- |
| 1 | 321. MAIN ST | MARY E | 21 F |
| 2 | 321. MAIN ST | WILLIAM M | 23 M |
| 3 | 324. MAIN ST | SUSAN K | 3 F |
| 4 | 324. MAIN ST | THOMAS H | 79 M |
| 5 | 324. MAIN ST | WALTER S | 46 M |
| 6 | 324. MAIN ST | ALICE A | 42 F |
| 7 | 324. MAIN ST | MARYANN A | 20 F |
| 8 | 324. MAIN ST | JOHN S | 16 M |
| 9 | 325A. MAIN ST | JAMES L | 34 M |
| 10 | 325A. MAIN ST | LIZA A | 31 F |

## 为每个头记录创建一个观测值

## 概述

在在上一个示例中，您学习了如何为每个详细记录创建一个观测值。但假设您只想知道每个地址住着多少人。您可以创建一个数据集，读取每个记录，计算人数，并将此数字存储在摘要变量中。

在示例中，这个摘要变量 `Total` 是为每个地址计算的。正如您所见，为每个头记录创建一个观测值将大量信息压缩成了一个简洁的集合。

```

原始数据文件

+------+--10+----+--20

H 321 S. MAIN ST

P MARY E 21 F

WILLIAM M 23 M

P SUSAN K 3 F

H 324 S. MAIN ST

P THOMAS H 79 M

WALTER S 46 M

ALICE A 42 F

MARYANN A 20 F

JOHN S 16 M

H 325A. MAIN ST

PAMES L 34 M

PIZA A 31 F

H 325B S. MAIN ST

MARGO R 27 F

WILLIAM S 27 M

ROBERT W 1 M

```

## SAS 数据集：为每个头记录创建一个观测值 657

| 地址 | Total |
| :--- | :--- |
| 321 S. MAIN ST | 3 |
| 324 S. MAIN ST | 5 |
| 325A. MAIN ST | 2 |
| 325B S. MAIN ST | 3 |

当您编写 `DATA` 步来读取此文件时，您需要考虑执行若干任务。首先，在读取和汇总详细记录时，`Address` 的值必须保留。

```sas

data perm.people;

infile census;

retain Address;

```

```

---+------10------++

321 S. MAIN ST

MARY E 21 F

WILLIAM M 23 M

SUSAN K 3 F

```

接下来，必须读取类型的值，以确定当前记录是头记录还是详细记录。添加 `@` 来固定记录，以便另一个 `INPUT` 语句可以读取剩余的值。

```sas

data perm.people;

infile census;

retain Address;

input type $1. @;

```
