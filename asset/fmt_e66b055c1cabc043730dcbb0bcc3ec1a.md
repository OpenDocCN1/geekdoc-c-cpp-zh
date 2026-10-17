
- 包含特殊字符的值，例如百分号 (`%`)、美元符号 (`$`) 和逗号 (`,`)
- 日期和时间值
- 分数、整数二进制、实数二进制和十六进制形式的数据。

`filefref Empdata` 引用的外部文件包含某小型计算机制造商技术写作部门的人员信息。字段包含每个员工的姓、名、职位和年薪。

原始数据文件 `Empdata`

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |
| LARSON | AMY | 113 | 32,696.78 |
| MOORE | MARY | 112 | 29,845.89 |
| POWELL | JASON | 103 | 35,099.50 |
| RILEY | JUDY | 111 | 25,309.00 |
| RYAN | NEAL | 112 | 28,180.00 |
| WILSON | HENRY | 113 | 31,875.46 |
| WOODS | CHIP | 105 | 17,098.71 |

注意 `Salary` 的值包含逗号。因此，`Salary` 的值被认为是非标准数值值。

# 选择输入样式

非标准数据值需要一种比列输入更灵活的输入样式。

你可以使用格式化输入（formatted input），它结合了列输入的特征与读取标准和非标准数据的能力。

![](img/d8531a787915cd75227275234ea33bae_529_0.png)

每当你遇到组织成固定字段的原始数据时，你可以使用

- 列输入仅读取标准数据
- 格式化输入同时读取标准和非标准数据。

# 使用格式化输入

## 格式化输入的通用形式

格式化输入是在固定字段中读取标准和非标准数据的一种非常强大的方法。

使用格式化输入的 `INPUT` 语句通用形式：

```
INPUT <pointer-control> variable informat;
```

其中

- `pointer-control`（指针控制）将输入指针置在指定的列上
- `variable`（变量）是变量名
- `informat`（格式符）是指定 SAS 如何读取原始数据的特殊指令。

在本章中，你将学习两种列指针控制。

- `@n` 将输入指针移动到特定的列号。
- `+n` 将输入指针向前移动到相对于当前位置的列号。

让我们先看看 `@n` 指针控制。

## 使用 @n 列指针控制

`@n` 是一个绝对指针控制符，它能将输入指针移动到特定的列号。`@` 将指针移动到第 `n` 列，即正在读取的字段的第一列。

使用格式化输入和 `@n` 指针控制的 `INPUT` 语句通用形式：

```
INPUT @n variable informat;
```

- `variable` 是变量名
- `informat` 是指定 SAS 如何读取原始数据的特殊指令。

让我们使用 `@n` 指针控制在外部文件 `Empdata` 中定位变量。如所示，`LastName` 从第 1 列开始。我们可以从 `@1` 开始。

```
input @1 LastName $7.
```

然而，默认指针就是第 1 列，所以不需要使用指针来读取第一个字段。

```
input LastName $7.
```

## 使用格式化输入 5

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |
| LARSON | AMY | 113 | 32,696.78 |
| MOORE | MARY | 112 | 29,845.89 |
| POWELL | JASON | 103 | 35,099.50 |
| RILEY | JUDY | 111 | 25,309.00 |

接下来，`FirstName` 从第 9 列开始。为了指向第 9 列，在 `INPUT` 语句中使用 `@` 符号：

```sas
input LastName $7. @9 FirstName $5.
```

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |
| LARSON | AMY | 113 | 32,696.78 |
| MOORE | MARY | 112 | 29,845.89 |
| POWELL | JASON | 103 | 35,099.50 |
| RILEY | JUDY | 111 | 25,309.00 |

> `$7` 和 `$5` 格式符将在本章稍后解释。

## 按任意顺序读取列

列指针非常有用。例如，在读取记录时可以使用 `@n` 将指针向前或向后移动。在这个 `INPUT` 语句中，首先读取从第 9 列开始的 `FirstName`。

```
input @9 FirstName $5.
```

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIG | JOHN | 111 | 25,309.00 |

现在让我们读取 `LastName`，它从第一列开始。在这里你必须使用 `@n` 指针控制将指针移回第 1 列。

```
input @9 FirstName $5. @1 LastName $7.
```

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |

`INPUT` 语句的其余部分指定 `JobTitle` 和 `Salary` 原始数据的列位置。

```
input @9 FirstName $5. @1 LastName $7. @15 JobTitle 3.
@19 Salary comma;
```

## 520 第 16 章 在固定字段中读取原始数据

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |

> `$5.`, `$7.`, `$3.` 和 `comma9` 格式符在本章稍后解释。

## +n 指针控制

`+n` 指针控制将输入向前移动到相对于当前位置的列号。`+` 将指针向前移动 `+n` 列。

`INPUT` 语句格式化输入和 `+n` 指针控制的通用形式：

`INPUT +n variable informat;`

- `variable` 是变量名
- `informat` 是指定 SAS 如何读取原始数据的特殊指令。

为了正确读取，理解在读取每个数据值后列指针所在的位置非常重要。让我们来看一个例子。

假设你想按照以下顺序从 `Empdata` 读取数据：`LastName`, `FirstName`, `Salary`, `JobTitle`。因为 `LastName` 的值从第 1 列开始，不需要列指针控制。

```
input LastName $7;
```

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |

使用格式化输入，列指针会移动到刚刚读取的内容的后续列。在这个例子中，读取 `LastName` 后，指针移动到第 8 列。

| 姓 (Last Name) | 名 (First Name) | ID | 薪水 (Salary) |
| :--- | :--- | :--- | :--- |
| EVANS | DONNY | 112 | 29,996.63 |
| HELMS | LISA | 105 | 18,567.23 |
| HIGGINS | JOHN | 111 | 25,309.00 |

为了开始读取从第 9 列开始的 `FirstName`，使用 `+1` 将列指针向前移动 1 列。

```
input LastName $7. +1 FirstName $5.
```

## 使用数据洞（Donuts）

在读取 `FirstName` 后，列指针移动到第 14 列。现在你想要跳过 `JobTitle` 的值并读取 `Salary` 的值，后者从第 19 列开始。因此，将列指针从第 14 列向后移动 5 列。

```
input Name$7. +1 FirstName $5. +5 Salary9.
```

| 12345 | |
|--------+----+10----v----v20----+ |
| EVANS DONNY 112 29,996.63 |
| HELMS LISA 105 18,567.23 |
| HIGGINS JOHN 111 25,309.00 |

最后一个读取的字段包含 `JobTitle` 的值。你可以使用 `@n` 列指针返回到第 15 列。

```
input Name$7. +1 FirstName $5. +5 Salary9.
@15 JobTitle 3.
```

|--------+----+10----v----v20----+ |
| EVANS DONNY 112 29,996.63 |
| HELMS LISA 105 18,567.23 |
| HIGGINS JOHN 111 25,309.00 |

> `$7.`、`$5.`、`comma9.` 和 `3.` 信息将在在本章稍后进行解释。

> 你可以使用符号 `+-(n)` 来将指针向后移动 n 位。有关 `+-(n)` 符号的信息，请参考 SAS 文档。

# 使用格式符（Informats）

## 概述

记住格式化输入 `INPUT` 语句的通用形式：

`INPUT <pointer-control> variable informat.`

格式符（informat）是告诉 SAS 如何读取原始数据的指令。SAS 提供了许多格式符用于读取标准和非标准数据值。这里是一个示例。

表 16.1 用于读取数据的选格式符

| PERCENTw. | DATEw. | NENGOW. |
| $BINARYw. | DATETIMEw. | PDw. |
| $VARYINGw. | HEXw. | PERCENTw. |
| $. | JULIANw. | TIMEw. |
| COMMAw. | MMDYYw. | w.d |

## 522 第 16 章 在固定字段中读取原始数据

注意：

- 每个格式符都包含一个 `w` 值，指示原始数据字段的宽度
- 每个格式符还包含一个点号（`.`），这是一个强制分隔符
- 对于某些格式，可选的 `d` 值指定了隐含的小数位数
- 用于读取字符数据的格式符始终以美元符号 (`$`) 开头

要查看格式符的完整列表，请参考 SAS 文档。

## 读取字符值

`$w` 格式符允许你读取字符数据。`w` 代表数据值的字段宽度（包含原始数据字段的列总数）。

在下例示例中，`S` 表示 `FirstName` 是一个变量，`5` 表示字段宽度为五列，而 `d` 指定了格式符。

```
input @9 FirstName $;
```

+-----+----V10--------+20----+----+
EVANS DONNY 112 29,996.63
HELMS LISA 105 18,567.23
HIGGINS JOHN 111 25,309.00
LARSON ANY 111 32,386.78
MOORE MARY 112 28,945.89
POWELL JASON 103 35,099.50
RILEY JUDY 111 25,309.00
RYAN NEAL 112 28,180.00
WILSON HENRY 113 31,875.46
WOODS CHIP 105 17,098.71

## 读取标准数值数据

用于标准数值数据的格式符是 `w`。`w` 指定数据值的字段宽度，点号作为分隔符，`d` 指定了隐含的小数位数。如果数据已经包含小数点，`w.` 格式符会忽略 `d` 值。

例如，下面的原始数据包含 6 位数字和 1 个小数点。因此，`w.` 格式符需要 7 位宽度才能正确读取该数据。

| 原始数据值 | w. 格式符 | 变量值 |
|--- |--- |--- |
| 340008 | 7. | |

在下面的示例中，15-17 列的 `JobTitle` 只包含数字。记住，标准数值数据可以包含数字、小数点、科学计数法和负号。

## 使用格式符 523

不需要 `d` 值来读取 `JobTitle` 的值。只需将列指针移动到第 15 列，命名变量并指定 3 位字段宽度。

```
input @9 FirstName $5. @1 LastName $7. +7 JobTitle 3;
```

| |----+10----20---| |
| EVANS DONNY 112 29,996.63 |
| HELMS LISA 105 18,567.23 |
| HIGGINS JOHN 111 25,309.00 |
| LARSON AMY 112 32,696.78 |
| MOORE MARY 112 28,945.89 |
| POWELL JASON 103 35,295.50 |
| RILEY JUDY 111 25,309.00 |

务必指定格式符。

## 非标准数值数据

`COMMAw.d` 格式符用于读取数值并移除嵌入的逗号、破折号、美元符号、百分号、左括号和右括号（视为负号）。`COMMAw.d` 格式符有三部分：

| 1. | 格式符 COMMA |
| 2. | 指定字段宽（包括美元符号和小数位）w |
| 3. | 指定隐含小数位（如果值已包含小数点）d |

在示例中，`Salary` 的值包含逗号，这意味着它们是非标准值。`Salary` 从第 19 列开始，因此使用 `@n` 或 `+n` 指针指向第 19 列，然后命名变量。

```
data sasuser.empdata;
file empdata;
input @9 FirstName $5. @1 LastName $7. +7 JobTitle 3.
@19 Salary;
```

1-----+10----+20----+-----
EVANS DONNY 112 29,996.63
HELMS LISA 105 18,567.23
HIGGINS JOHN 111 25,309.00
LARSON AMY 112 32,696.78
MOORE MARY 112 28,945.89
POWELL JASON 103 35,099.50
RILEY JUDY 111 25,309.00

现在添加 `COMMA.d` 并指定字段宽度。值在第 27 列结束，因此字段宽度为 9 列。添加 `RUN` 语句完成 `DATA` 步。

```
data sasuser.empinfo;

in empdata;

input @9 FirstName $5. @1 LastName $7. +7 JobTitle 3.

@19 Salary comma;

run;
```

1-----+10----+20----+-----
EVANS DONNY 112 29,996.63
HELMS LISA 105 18,567.23
HIGGINS JOHN 111 25,309.00
LARSON AMY 112 32,696.78
MOORE MARY 112 28,945.89
POWELL JASON 103 35,099.50
RILEY JUDY 111 25,309.00

如果你使用 `PROC PRINT` 显示数据，则输出中 `Salary` 的值将移除逗号。

```
data sasuser.empinfo;
in empdata;
input @9 FirstName $5. @1 LastName $7. +7 JobTitle 3.
@19 Salary comma;
run;
print data=sasuser.empinfo;
run;
```

图 16.1 `PROC PRINT` `Salary` 的输出

| Obs | FirstName | LastName | JobTitle | Salary |
|---|---|---|---|---|
| 1 | DONNY | EVANS | | 112 29996.63 |
| 2 | LISA | HELMS | | 105 18567.23 |
| 3 | JOHN | HIGGINS | | 111 25309.00 |
| 4 | AMY | LARSON | | 113 32696.78 |
