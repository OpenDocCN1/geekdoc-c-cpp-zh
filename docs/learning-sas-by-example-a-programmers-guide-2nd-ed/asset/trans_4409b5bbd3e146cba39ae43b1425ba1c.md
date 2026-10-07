

## 程序 21.10: 从外部文件读取外部文件名

```sas
data ReadMany;
infilele 'C:\books\Learning\Filenames.txt';
input ExternalNames $ 40;
infile dummy filevar=ExternalNames end=Last;
do until (Last);
  input .;
  output;
end;
run;
```

在这里，数据文件 `Filenames.txt` 包含了你想要读取的文件名。`INFILE` 语句中的 `FILEVAR` 选项使用存储在变量 `ExternalNames` 中的文件名。你需要包含一个虚拟文件（dummy file，你可以称它为任何东西——SAS 会忽略它），以保持 `INFILE` 语句的语法完整性。`DO UNTIL` 循环从第一个文件开始读取数据，直到读取最后一条记录（此时变量 `Last` 变为 1）。然后程序返回到 `DATA` 步的顶部，从 `Filenames.txt` 文件中读取一个新文件名，并继续处理。

程序 21.10 的变体是将外部文件的名称放在 `DATALINES` 语句之后，如下例所示：

## 程序 21.11: 使用 DATALINES 语句读取外部文件名

```sas
data ReadMany;
input ExternalNames $ 40;
infile dummy filevar=ExternalNames end=Last;
do until (Last);
  input .;
  output;
end;
datalines;
C:\books\Learning\Datal.txt
C:\books\Learning\MoreData.txt
C:\books\Learning\Fred.txt
```

将文件名直接放在程序中可能比将它们放在外部文件中更方便。

## 21.10 读取多行数据以创建一个观测值

在“过去”，当许多平面文件的最大长度为 80 字节时，有必要将一组数据（一个观测值）放置在多行中。即使在今天你也可能遇到这个问题。

例如，你有一个原始数据文件（Health.txt），每个受试者有两行（记录），数据布局如下：

| 变量 | 描述 | 行号 | 起始列 | 长度 | 类型 |
|---|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 1 | 3 | 字符 |
| DOB | 出生日期 | 1 | 4 | 10 | mm/dd/yyyy |
| Weight | 重量（磅） | 1 | 14 | 3 | 数字 |
| HR | 心率 | 2 | 4 | 3 | 数字 |
| SBP | 收缩性血压 | 2 | 7 | 3 | 数字 |
| DBP | 舒张性血压 | 2 | 10 | 3 | 数字 |

以下是一个读取该数据文件并创建一个名为 `Health` 的临时 SAS 数据集的程序：

## 程序 21.12: 读取多行数据以创建一个观测值

```sas
data Health;
  infile 'C:\books\Learning\Health.txt' pad;
  input @1 Subj $3
        @4 DOB mmddyyy10.
        @14 Weight $3.
        @7 SBP $3.
        @10 DBP $3.
  format DOB mmddyyy10.;
run;
```

该程序的隐藏特性是行指针，即 `INPUT` 语句中的井号——或者年轻人可能会称它的哈希标签（#)。`#` 指针告诉 SAS 当每个观测值有多个行数据时应该读取哪一行。

来自 `PROC PRINT` 的 SAS 数据列表所示：

![](img/e9e15d853989558188e1c83b0ae655b0_374_0.png)

## 图 21.7: 数据集 Health 的列出

数据集 Health 的列出内容

| Subj | DOB | Weight | HR | SBP | DBP |
|---|---|---|---|---|---|
| 001 | 12/25/1944 | 210 | 80 | 160 | 100 |
| 002 | 05/11/1966 | 102 | 88 | 122 | 76 |
| 003 | 08/03/2000 | 66 | 90 | 102 | 62 |

读取此文件的另一种方法是使用相对行指针（正斜杠 `/`），告诉 SAS 跳过到下一行输入。使用此方法重写的程序 21.12 如下所示：

## 程序 21.13: 使用另一种方法读取多行数据以创建一个 SAS 观测值

```sas
data health;
infile ':C:\books\Learning\Health.txt' pad;
  @1 Subj $;
  @4 DOB mmddyy10;
  @14 Weight 3. /
  @4 HR 3;
  @7 SBP 3;
  @10 DBP 3;
format DOB mmddyy10;
run;
```

在这两种方法之间，作者更倾向于使用 `#` 行指针而不是斜杠表示法，因为这使得程序更易读且不易出错。

## 21.11 条件条件读取数据（单个末尾 @ 符号）

某些数据比你目前看到的要复杂。例如，你可能在一个文件中混合了多种记录类型。为了从这种类型的文件中读取值，你需要使用末尾的符号来解决这个问题。你可能在一个文件中混合了多种记录类型。不幸的是，在第二个年份，数据是混合的。SAS 提供了单个末尾的符号（@）来解决这个问题。这是一个例子：

2005 年的数据布局

| 变量 | 描述 | 起始列 | 长度 | 类型 |
|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 3 | 字符 |
| DOB | 出生日期 | 4 | 10 | 字符 |
| Weight | 重量（磅） | 1 | 14 | 3 | 数字 |
| HR | 心率 | 2 | 4 | 3 | 数字 |
| SBP | 收缩性血压 | 2 | 7 | 3 | 数字 |
| DBP | 舒张性血压 | 2 | 10 | 3 | 数字 |

2006 年的数据布局

| 变量 | 描述 | 起始列 | 长度 | 类型 |
|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 3 | 字符 |
| DOB | 出生日期 | 4 | 10 | 字符 |
| Gender | 性别 | 14 | 14 | 字符 |
| Balance | 账户余额 | 15 | 21 | 数字 |

2005 年的数据布局

| 变量 | 描述 | 起始列 | 长度 | 类型 |
|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 3 | 字符 |
| DOB | 出生日期 | 4 | 10 | 字符 |
| Gender | 性别 | 14 | 14 | 字符 |
| Balance | 账户余额 | 15 | 21 | 数字 |

2006 年的数据布局

| 变量 | 描述 | 起始列 | 长度 | 类型 |
|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 3 | 字符 |
| DOB | 出生日期 | 4 | 10 | 字符 |
| Gender | 性别 | 14 | 14 | 字符 |
| Balance | 账户余额 | 15 | 21 | 数字 |

来自 `Survey56.txt` 的一些数据行：

```
001ABED 2005
002ABCD 2006
005AADD 2005
007BBC2006
001ABED 2005
002ABCD2006
```

## 第 21 章：使用高级技术

## 程序 21.14: 尝试读取混合类型文件的错误

这里是问题：

```sas
data Survey;
infile 'C:\books\Learning\Survey56.txt' pad;
input @1 Year$;
if Year = '2005' then
    input @4 Number $3 Q1 $1 Q2 $1 Q3 $1 Q4 $1;
else if Year = '2006' then
    [此处省略]
run;
```

那个小小的 @ 符号改变了一切！现在，SAS 在读取 `Year` 值后，会在同一行执行相应的 `INPUT` 语句。“保持行”的意思是将指针留在当前位置，而不是跳转到下一行。

## 21.12 末尾 @ 符号的更多示例

显示更多末尾 @ 的例子可能有所帮助。假设你有一个包含男性和女性的数据文件。假设你只想读取女性的数据。一种方法是读取所有感兴趣的变量（包括性别），测试性别是否等于 F。如果是，则保留该观测值。

| 变量 | 描述 | 起始列 | 结束列 | 数据类型 |
|---|---|---|---|---|
| Subj | 受试者编号 | 1 | 3 | 字符 |
| DOB | 出生日期 | 4 | 13 | 字符 |
| Gender | 性别 | 14 | 14 | 字符 |
| Balance | 账户余额 | 15 | 21 | 数字 |

这样做效率低下。更好的方法是读取性别值进行检查，如果性别等于 F，则读取剩余值。

让我们使用 `Bank.txt` 作为说明它是如何工作的示例：

```sas
data Females;
  infile 'C:\books\Learning\Bank.txt' pad;
  input @14 Gender $. @;
  if Gender != 'F' then delete;
  input @1 Subj $3;
        @4 DOB mmddyyy10.
        @15 Balance 7.;
run;
```

## 21.13 从单行输入创建多个观测值

有时你希望将多个受试者的数据放置在同一行中（或者有人给了你一个这样的文件）。例如，假设你有一组 X,Y 坐标，并想创建一个 SAS 数据集。一种方法是在每行输入中放置一对点，如下：

