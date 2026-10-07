

## 第3章：读取、写入和导入数据

b. 修改 SAS 程序，在 `DATA` 语句中使用 Windows 文件夹名称，在 C:\SASDATA 文件夹中创建一个名为 WEIGHT 的永久 SAS 数据集：

```
DATA "C:\SASDATA\";
```

（或使用适用于你特定 SAS 实现的相应语句）。查看日志以验证永久数据集是否已创建。

c. 修改 SAS 程序，使用两级 SAS 数据集名称，创建一个名为 MYASLIB.WEIGHT 的永久 SAS 数据集（在之前创建的 SAS 库 MYASLIB 中）：

```sas
DATA MYASLIB.WEIGHT;
```

- I. 为了验证永久数据集是否已创建，请从 MYASLIB 库将其打开到 Viewable 查看器中。
II. 使用 `File -> print` 打印此（整个）表格的副本。

d. 使用以下代码：

```sas
PROC DATASETS;
CONTENTS DATA= MYASLIB.WEIGHT;
RUN;
```

生成 SAS 数据集 MYASLIB.WEIGHT 的内容列表。将 `DATA=` 语句更改为

```sas
CONTENTS DATA=MYASLIB._ALL_;
```

以显示库中所有数据集的内容。

## 3.3 使用 SAS 代码导入 XLSX 数据。

- a. 使用 SAS 代码根据以下标准从 Excel 文件 FAMILY2.XLSX 导入数据：
I. 使用 `OUT=` 语句在 WORK 库中创建一个名为 INCOME 的 SAS 数据集。
II. 使用 `DATAFILE=` 指定你本地硬盘上原始 Excel 文件（XLSX 类型）的位置。
III. 使用 `DBMS=` 指定数据源（参见本章较前的 DBMS 选项图表查看文件类型）。
IV. 使用 `SHEET=` 指定 "Data" 为要导入的 Excel 名称。
V. 如果适用，使用 `GETNAMES=` 指明变量名在数据的第一行。

b. 导入数据后，使用 Viewdata 查看 `WORK.INCOME` 的内容。关闭 Viewdata 数据网格。

c. 使用此代码计算数据的描述性统计量：

```sas
TITLE "在此处输入你的名字";
PROC MEANS DATA=INCOME;
RUN;
```

## 3.4 关于 SAS 库的更多信息。

假设你的 SAS 数据集存储在硬盘上名为 C:\RESEARCH 的物理目录（文件夹）中。

- a. 如果你想在 SAS 中创建一个名为 CLINICAL 的快捷库名，哪条 `LIBNAME` 语句会指定数据的位置？（请填空。）

LIBNAME 'C:\_______';

b. 如果你想在 SAS 程序中使用名为 C:\RESEARCHJAN2009.SAS7BDAT 文件中的数据，请在以下 `DATA =` 语句中填空：

LIBNAME CLINICAL 'C:\RESEARCH';
PROC MEANS DATA = _______ ;

c. 使用以下信息创建一个 LIBNAME 语句：
硬盘位置为 O:\CLINICAL
SAS 库名称为 YOURNAME

LIBNAME '_______';

d. 如果你有一个名为 CLINICAL 的 SAS 库，并且你想创建一个名为 MAY2007 的永久数据集，并存储在硬盘的 C:\RESEARCH 文件夹中，那么在 SAS 代码中使用的文件名是什么？

________。

e. 在此练习的 d 步骤中，你硬盘上的 SAS 数据文件名称是什么？

:\RESEARCH\MAY2007.sas7bdat。

## 3.5 深入学习：SAS 如何读取数据。

在数据步（Data Step）的编译（Compile）、执行（Execution）和输出（Output）阶段，这些任务在过程的哪个阶段发生？

- a. SAS 检查代码查看是否存在错误。
_______阶段
b. SAS 读取数据并执行计算
_______阶段
c. SAS 创建数据集
_______阶段
d. 识别每个变量的类型和长度
_______阶段
e. SAS 创建输入缓冲区（Input Buffer）并将第一条数据记录的内容放入缓冲区
_______阶段
f. SAS 创建 PDV（程序数据集构建表）
_______阶段

g. PDV 中的初始值是

```
_N = 0
ERROR_ = ;
```

h. 一旦 SAS 填充了 PDV 且数据步中没有更多代码行，它会将 PDV 的内容发送到 __________ 缓冲区。

## 4 为分析准备数据

## 学习目标

- * 能够使用解释性名称为变量标记标签
* 能够创建新变量
* 能够使用 SAS® IF-THEN-ELSE 语句
* 能够使用 DROP 和 KEEP 选择变量
* 能够使用 SET 语句
* 能够使用 PROC SORT
* 能够追加和合并数据集
* 能够使用 PROC FORMAT
* 深入学习：能够在一组中找到第一个和最后一个值

你已经将数据输入 SAS，但在 SAS 中使用它们之前，通常需要进行修正、执行计算并以其他方式为分析准备数据。这一步在课堂环境中经常被忽视，因为你通常使用准备好分析的教材数据。当你收集自己的数据时，甚至从数据库获取数据时，在分析中使用它们之前可能需要进行一些更改。

> SAS® Essentials: Mastering SAS for Data Analytics, Second Edition. Alan C. Elliott and Wayne A. Woodward. © 2016 John Wiley & Sons, Inc. Published 2016 by John Wiley & Sons, Inc.

## 第4章：为分析准备数据

本章讨论的所有数据处理语句都出现在程序的 `DATA` 步中，`PROC FORMAT` 除外。这意味着，它们出现在 `DATA` 语句之后。

## 4.1 带解释性名称的变量

使用标签为变量提供描述性名称。数据集通常包含晦涩的名称，如 ID、WT 等。对于熟悉数据的人来说，这些是有意义的。如果你希望让输出更易读，为变量创建标签是很好的做法。在 SAS 中，可以使用标签。

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
FORMAT BDATE WORDDATE12;
LABEL FNAME="First Name"; * 完成标签*;
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME      LNAME      BDATE
--------------------------------
1 Bill       Smith      08JAN 1952
2 Jane       Jones      02FEB 1953
3 Clyde       York      23MAR 1949
```

注意，只有 FNAME 有标签。现在为 LNAME 和 BDATE 添加标签：

```sas
LABEL FNAME="First Name"
LNAME="Last Name"
BDATE="Birth Date";
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME      LNAME      BDATE
--------------------------------
1 Bill       Smith      08JAN 1952
2 Jane       Jones      02FEB 1953
3 Clyde       York       23MAR 1949
```

现在，所有变量都显示了标签。

此外，还可以更改日期格式：

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
FORMAT BDATE WORDDATE12;
LABEL FNAME="First Name"
LNAME="Last Name"
BDATE="Date of Birth";
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   First Name   Last Name   Date of Birth
--------------------------------------------
1 Bill        Smith       08 January 1952
2 Jane        Jones       02 February 1953
3 Clyde        York        23 March 1949
```

## 4.2 标签的长度

在 `LABEL` 语句中，标签的长度是的。

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
FORMAT BDATE WORDDATE12;
LABEL FNAME="First Name"
LNAME="Last Name"
BDATE="Date of Birth";
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   First Name   Last Name   Date of Bir
--------------------------------------------
1 Bill        Smith       08 January 1952
2 Jane        Jones       02 February 1953
3 Clyde        York        23 March 1949
```

注意，“Date of Birth”被截断为“Date of Bir”。这是因为标签的默认限制为 20 个字符。要显示完整的标签，可以使用 `LABELMAX` 选项：

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
FORMAT BDATE WORDDATE12;
LABELMAX=30;
LABEL FNAME="First Name"
LNAME="Last Name"
BDATE="Date of Birth";
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   First Name   Last Name   Date of Birth
--------------------------------------------
1 Bill        Smith       08 January 1952
2 Jane        Jones       02 February 1953
3 Clyde        York        23 March 1949
```

## 4.3 重命名变量

你可以在 `DATA` 语句中使用 `AS` 语句来重命名变量。

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
AS FNAME AS FirstName LNAME AS LastName BDATE AS BirthDate;
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FirstName    LastName     BirthDate
------------------------------------
1 Bill        Smith       08 January 1952
2 Jane        Jones       02 February 1953
3 Clyde        York        23 March 1949
```

你也可以在 `PROC PRINT` 语句中使用 `RENAME` 选项来重命名：

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT rename=(FNAME=FirstName LNAME=LastName BDATE=BirthDate);
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FirstName    LastName     BirthDate
------------------------------------
1 Bill        Smith       08 January 1952
2 Jane        Jones       02 February 1953
3 Clyde        York        23 March 1949
```

## 4.4 删除变量

使用 `DROP` 语句从数据集中删除变量。

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
DROP LNAME;
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME        BDATE
----------------------
1 Bill       08 January 1952
2 Jane       02 February 1953
3 Clyde       23 March 1949
```

你也可以使用 `KEEP` 语句仅保留特定变量：

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
KEEP FNAME BDATE;
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME        BDATE
----------------------
1 Bill       08 January 1952
2 Jane       02 February 1953
3 Clyde       23 March 1949
```

## 4.5 创建新变量

可以在 `DATA` 步中创建新变量。

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
YEAR = YEAR(BDATE);
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME        LNAME        BDATE           YEAR
--------------------------------------------
1 Bill        Smith       08 January 1952   1952
2 Jane        Jones       02 February 1953   1953
3 Clyde        York        23 March 1949       1949
```

你还可以使用表达式来创建新变量：

```sas
DATA MYDATA;
INPUT @1 FNAME $11. @12 LNAME $12. @24 BDATE DATE9;
YEAR = YEAR(BDATE);
MONTH = MONTH(BDATE);
DATALINES;
Bill Smith 08JAN1952
Jane Jones 02FEB1953
Clyde York 23MAR1949
;
PROC PRINT;
RUN;
```

运行上述程序后，输出将显示如下：

```
Observations: 3

   FNAME        LNAME        BDATE           YEAR        MONTH
------------------------------------------------------
1 Bill        Smith       08 January 1952   1952             1
2 Jane        Jones       02 February 1953   1953             2
3 Clyde        York        23 March 1949       1949             3
```

## 4.6 使用 SET 语句

`SET` 语句用于从现有数据集读取数据。

```sas
DATA NEWDATA;
SET MYDATA;
RUN;
```

这会创建一个名为 `NEWDATA` 的新数据集，包含 `MYDATA` 的所有内容。

你也可以在 `SET` 语句中合并多个数据集：

```sas
DATA COMBINED;
SET DATA1 DATA2;
RUN;
```

这会将 `DATA1` 和 `DATA2` 的行追加到 `COMBINED` 中。

## 4.7 合并数据集

使用 `MERGE` 语句根据公共键合并数据集。

```sas
DATA COMBINED;
MERGE DATA1(by=ID) DATA2(by=ID);
BY ID;
RUN;
```

注意：在合并之前，数据集必须按 `BY` 变量进行排序。

## 4.8 使用 PROC FORMAT

使用 `PROC FORMAT` 创建自定义格式。

```sas
PROC FORMAT;
VALUE grade_fmt
1 = 'Low'
2 = 'Medium'
3 = 'High';
END;
```

然后在 `PROC PRINT` 中使用该格式：

```sas
PROC PRINT DATA=MYDATA;
FORMAT grade=grade_fmt.;
RUN;
```

## 4.9 排序数据集

使用 `PROC SORT` 对数据集进行排序。

```sas
PROC SORT DATA=MYDATA;
BY LNAME;
RUN;
```

## 4.10 追加数据集

使用 `SET` 语句将一个数据集的行追加到另一个数据集。

```sas
DATA APPENDED_DATA;
SET DATA1 DATA2;
RUN;
```

这会将 `DATA2` 的所有行追加到 `DATA1` 之后。

## 4.11 练习

- 练习 1：创建一个名为 `STUDENTS` 的数据集包含 `ID`、`NAME` 和 `GRADE`。
- 练习 2：使用 `DROP` 删除 `GRADE` 变量。
- 练习 3：使用 `KEEP` 只保留 `ID` 和 `NAME`。
- 练习 4：创建一个新变量 `PASS`，如果 `GRADE >= 60` 则为 'Yes'，否则为 'No'。
- 练习 5：使用 `PROC SORT` 按 `NAME` 排序。
- 练习 6：使用 `PROC FORMAT` 为 `GRADE` 创建等级格式（A, B, C, D, F）。

