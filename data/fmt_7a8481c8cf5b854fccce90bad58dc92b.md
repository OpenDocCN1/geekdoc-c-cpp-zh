
# IMPORT 过程

指定输入 PC 文件、电子表格或分隔符扩展文件的完整路径和文件引用（`fileref`）。文件引用是与输出文件的物理位置关联的 SAS 名称。要分配文件引用，请使用 `FILENAME` 语句。

如果你指定了文件引用、完整路径且文件名不包含特殊字符，则可以省略引号。

除了 `DIS` 外，IMPORT 过程不支持 `FILENAME` 语句的设备类型或访问方法。例如，IMPORT 过程不支持创建临时外部文件的 `TEMP` 类型。

导入（Import）功能只有当 SAS 支持该数据类型时，IMPORT 才能导入数据。SAS 支持数值和字符型数据（例如，不支持二进制对象）。如果你想要导入的数据类型是 SAS 不支持的，则 IMPORT 过程可能无法正确导入。在许多情况下，该过程会尽力尝试转换数据。然而，某些类型是不可能转换的。

交互：默认情况下，IMPORT 过程将分隔符文件读取为变长记录文件。如果你的外部文件是固定长度格式，请使用 `FILENAME` 语句通过 PROC IMPORT 使用 `RECM=F` 和 `LRECL=` 指定输入文件。

当你使用文件引用指定要导入的分隔符文件时，记录长度（`LRECL`）默认为 256，除非你在 `FILENAME` 语句中使用 `LRECL` 选项。IMPORT 过程支持的最大 `LRECL` 值为 32,767。

对于分隔符文件，会扫描前 20 行来确定变量属性。你可以通过 `GUESSINGROWS=` 语句增加扫描的行数。所有值都作为字符字符串读取。如果对数据值应用了日期时间格式或数值输入格式，则类型被声明为数值型。否则，类型保持为字符。

## OUT=<libref> SAS-data-set

通过单级或双级 SAS 名称（库名和成员名）标识输出 SAS 数据集。如果指定的 SAS 数据集不存在，IMPORT 过程将创建它。如果你指定了单级名称，默认情况下，IMPORT 过程使用 `USER` 库（如果已分配）或 `WORK` 库（如果 `USER` 未分配）。

当指定了 `VALIDMEMNAME=EXTEND` 系统选项时，SAS 数据名可以包含单引号。`VALIDMEMNAME=` 扩展了某些 SAS 成员（如 SAS 数据集名）的命名规则。

如果 SAS 数据名包含国家字符或特殊字符，请使用引号。特殊字符的例外是：`/ * ? < > | :~`。使用 `VALIDMEMNAME=` 扩展了某些 SAS 成员（如 SAS 数据集名）的命名规则。更多信息请参见 [VALIDMEMNAME=系统选项](第16页)。

## TABLE=<tablename>

指定输入 DBMS 表的名称。如果名称不包含特殊字符（如问号）、小写字母或空格，可以省略引号。注意，DBMS 表可能是区分大小写的。要求：当导入 DBMS 表时，必须指定 `DBMS=` 选项。

## DBMS=<identifier>

指定要导入的数据类型。以下是 Base 包含的常用 DBMS 标识符：

- **逗号分隔值**。对于扩展名为 `.CSV` 的逗号分隔文件，`DBMS=` 是可选的。
- **JMP 文件**。使用 JMP 7 或更高版本。使用 `DBMS=JMP` 指定 JMP 文件。JMP 变量名可长 255 个字符。
- **制表符分隔值**。指定 `DBMS=DLM` 以导入任何不以 `.CSV` 结尾的分隔符文件。

## REPLACE

覆盖现有数据集。如果省略 `REPLACE`，IMPORT 过程将不会覆盖现有数据集。相反，请使用带有 `REPLACE=` 的 SAS 数据步来替换永久性数据集。

## SAS-data-options

指定数据选项。例如，要为结果数据集命名，可以使用 `READ=` 或 `WRITE=` 数据选项。要仅导入符合指定条件的数据，可以使用 `WHERE=` 数据集选项。在导入分隔符文件、逗号分隔文件或制表符分隔文件时，无法指定数据选项。

## 示例：导入扩展名为 XLSX 的 Excel 文件

此示例导入了一个 Excel 文件并创建了一个临时 SAS 数据集 `Work.Bootsales`。

```
options validname=v7;
proc import datafile='C:\Users\Student1\cert\boots.xlsx'
    dbms=xlsx
    out=work.bootsales
    replace;
    sheet=0;
    getnames=yes;
run;
proc contents data=bootsales;
run;
proc print data=bootsales;
run;
```

- 1 `VALIDNAME=V7` 语句强制 SAS 将空格转换为下划线。在 SAS 中，变量名不能包含空格。
- 2 在导入 Excel 工作表时，使用 `REPLACE` 选项覆盖现有数据集。`OUT=` 选项标识输出数据集。
- 3 `GETNAMES=` 语句从 Excel 工作表中导入变量名。
- 4 使用 `GETNAMES=` 语句从数据集的第一行读取变量名。
- 5 使用 `CONTENTS` 过程显示数据集的描述部分。

## 示例：导入带有 TXT 扩展名的空格分隔文件

此示例导入了一个空格分隔的文件，并创建一个名为 `Work.States` 的临时 SAS 数据集。以下输入数据包含了当您想避免单词之间的空格分隔其值时，用引号括起值。

| 州 | 州府 | 鸟类 |
|---|---|---|
| South Georgia | Atlanta | 'Brown Thrasher' |
| State 'North Carolina' | Raleigh | Cardinal |
| North Connecticut | Hartford | Robin |
| West Washington | Olympia | 'American Goldfish' |
| Midwest Illinois | Springfield | Cardinal |

您可以提交以下代码来导入文件。

```
options validname=v7;
filename data='C:\Users\Student1\state_data.txt' lrecl=100;
proc import datafile=stdata
    dbms=dlm
    out=state
    replace;
    delimiter=' ';
    getnames=yes;
run;
proc print data=states;
run;
```

- 1 指定文件引用（`fileref`）和文件位置。如果文件具有固定长度格式，请指定 `LRECL=` 系统选项。`LRECL=` 系统选项在使用外部文件时指定默认记录长度。
- 2 指定输入文件并指定其为分隔文件。`DBMS=` 选项指定要导入的数据类型。如果分隔符类型是 TAB 或 CSV 以外的字符，则 `DBMS=` 选项为 `DLM`。`REPLACE` 选项覆盖现有的 SAS 数据集。`OUT` 标识输出的 SAS 数据集。
- 3 在 `DELIMITER` 语句中指定一个空格。`GETNAMES=` 语句用于从数据的第一行生成变量名。

### 输出 4.4 PROC 打印：Work.States 数据集

| Obs | Region | 州 | 州府 | 鸟类 |
|---|---|---|---|---|
| 1 | South | Georgia | Atlanta | Brown Thrasher |
| 2 | South | North Carolina | Raleigh | Cardinal |
| 3 | North | Connecticut | Hartford | Robin |
| 4 | West | Washington | Olympia | American Goldfish |
| 5 | Midwest | Illinois | Springfield | Cardinal |

## 示例：导入带有 CSV 扩展名的逗号分隔文件

此示例导入了一个逗号分隔的文件并创建一个临时 SAS 数据集 `Work.Shoes`。输入文件 `Boot.csv` 是一个逗号分隔文件，使用逗号分隔变量的分隔文本文件。

```
options validname=v7;
proc import datafile='C:\Users\Student1\cert\boot.csv' /* 91 */
    dbms=csv
    out=shoes
    replace;
    getnames=no;
run;
proc print data=work.shoes;
run;
```

- 1 指定输入文件，`DATAFILE=` 指定输入文件，`OUT=` 指定输出数据集。`DBMS=` 指定要导入的数据类型。如果文件类型是 CSV，则 `DBMS=` 选项为 `CSV`。`REPLACE` 选项覆盖现有的 SAS 数据集。
- 2 将 `GETNAMES=` 语句设置为 `NO`，以使用数据的第一行作为变量名。

### 输出 4.5 PROC 打印：Work.Shoes 数据集

| Obs | VAR1 | VAR2 | VAR3 | VAR4 | VAR5 | VAR6 | VAR7 |
|---|---|---|---|---|---|---|---|
| 1 | Africa | Addis Ababa | 12 | 29761 | 19182 | 769 | |
| 2 | Asia | Bangkok | 1 | 1996 | 9576 | 80 | |
| 3 | Canada | Calgary | 8 | 17720 | 63280 | 472 | |
| 4 | Central America | Kingston | 33 | 102372 | 39376 | 4454 | |
| 5 | Eastern Europe | | | | | | |
| 6 | Middle East | | | | | | |
| 7 | Pacific | | | | | | |
| 8 | South America | | | | | | |
| 9 | United States | | | | | | |
| 10 | Western Europe | | | | | | |

*(注：原文表格第5-10行数据不全，此处保持结构一致)*

## 示例：导入制表符分隔文件

### 输出 4.5 PROC 打印：Work.Shoes (制表符分隔文件示例)

| Obs | Name | Gender | Age |
|---|---|---|---|
| 1 | Louise | F | 12 |
| 2 | James | M | 12 |
| 3 | John | M | 12 |
| 4 | Robert | M | 12 |
| 5 | Alice | F | 13 |
| 6 | Barbara | F | 13 |
| 7 | Jeffery | M | 13 |
| 8 | Carol | F | 14 |
| 9 | Judy | F | 14 |
| 10 | Alfred | M | 14 |
| 11 | Henry | M | 14 |
| 12 | Jenet | F | 15 |
| 13 | Mary | F | 15 |
| 14 | Ronald | M | 15 |
| 15 | William | M | 15 |
| 16 | Philip | M | 16 |

## 读取并验证数据

### 验证读取数据的代码

在读取完整文件之前，您可以通过限制读取的观测值来验证读取数据的代码。您可以在 IMPORT 过程之前使用 `OPTIONS` 语句限制 SAS 从外部文件中读取的观测数。

```
options obs=5;
proc import datafile="C:\Users\Student1\cert\boot.csv"
    dbms=csv
    out=shoes
    replace;
run;
```

### 检查 DATA 步处理

在 PROC IMPORT 运行 DATA 步读取数据后，日志中的消息确认了数据已正确读取。日志指示如下：

- 从输入文件 `'C:\Users\Student1\cert\boot.csv'` 中读取了五条记录
- 创建的数据集 `work.shoes` 有五个观测值和变量。

### 4.2 SAS 日志

```
NOTE: 输入文件 'C:\Users\Student1\cert\boot.csv' 是：
FileName=C:\Users\Student1\cert\boot.csv,
RECPW=WCL=3276, File Size (bytes)=657,
Last Modified=25Jun2018:13:37:49,
Create Time=25Jun2018:13:37:49

NOTE: 从输入文件 'C:\Users\Student1\cert\boot.csv' 中读取了 5 条记录。最小记录长度为 51。最大记录长度为 81。
NOTE: 数据集 SHOES 拥有 5 个观测值和 7 个变量。

NOTE: WORK.SHOES 数据集成功创建。
NOTE: 从 C:\Users\Student1\cert\boot.csv 在 WORK.SHOES 中创建了 5 行。
```

## 读取整个外部文件

要修改 PROC 步骤以读取整个外部文件，请将默认值恢复为 `OBS=MAX` 系统类型。为此，请设置 `OBS=MAX` 并重新运行程序。

```
options obs=max;
proc import datafile="C:\Users\Student1\cert\boot.csv"
    dbms=csv
    out=shoes
    replace;
    getnames=no;
run;
```

> 注意：SAS Studio 在每次提交代码之前都会使用 `OBS=MAX`。
