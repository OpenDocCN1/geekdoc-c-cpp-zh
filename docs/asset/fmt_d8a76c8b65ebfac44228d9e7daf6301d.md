
`OUT=<libref>SAS-data-set` 指定输出的数据集。

`DATAFILE="filename"` 指定输入 PC 文件、工作表或分隔文件的完整路径和文件名或库引用。

`DBMS=identifier` 指定要导入的数据类型。要导入 DBMS 表格，必须使用有效的数据库标识指定 `DBMS=`。例如，`DBMS=EXCEL` 表示导入 Microsoft Excel 工作表。

`REPLACE` 覆盖现有的 SAS 数据集。如果不指定 `REPLACE`，`PROC IMPORT` 将不会覆盖现有数据集。

`RANGE="range-name | absolute-range"` 通过识别要从指定工作表中导入的单元格区域来划分子集。

`GETNAMES=YES | NO` 用于工作表和分隔文件，决定是否根据输入文件第一行的列名生成 SAS 变量名。注意，如果列名包含 SAS 名称中无效的特殊字符，SAS 会将字符转换为下划线。

`MIXED=YES | NO` 对于包含混合数据类型的列，将数值数据转换为字符数据。默认是 `NO`，这意味着数值将作为缺失值导入到字符列中。如果 `MIXED=YES`，引擎将为该列分配 SAS 字符类型并将所有数值数据转换为字符数据。

`SCANTEXT=YES | NO` 扫描数据源列的文本长度，并使用找到的最长字符串作为 SAS 列宽。

`USEDATE=YES | NO` 指定要使用的格式。如果 `USEDATE=YES`，则在从 Excel 工作簿导入数据时对数据源表中的日期/时间使用 `DATE` 格式。如果 `USEDATE=NO`，则对日期/时间使用 `DATETIME` 格式。

`SCANTIME=YES | NO` 扫描 `DATETIME` 类型字段的所有行值，如果只有时间值（即没有日期或 `datetime` 值），则自动确定 `TIME` 类型。

导入向导从外部数据源读取数据并写入 SAS 数据集。

导入向导的步骤：
1. 选择要导入的文件类型。
2. 找到输入文件。
3. 选择要导入数据的表格范围或工作表。
4. 选择存储导入文件的位置。
5. 保存生成的 `PROC IMPORT` 代码。（可选）

## 6.2 使用 Excel 工作表的更多操作（自学）

### 导入向导：创建 SAS 语句

导入向导可以创建一个包含 `PROC IMPORT` 语句的文件，这些语句可以在 SAS 程序中再次导入数据。如果您希望这些语句是永久的，请输入要保存它们的文件名：

### SAS Log

```
NOTE: WORK.SUBSET2A 数据集成功创建。
```

```
proc print data=work.subset2a;

run;
```

### 部分 PROC PRINT 输出

| Employees Obs ID | First_Name | Last_Name | Gender | Salary | Job Title | Country | Birth Date | Hire_Date |
|---|---|---|---|---|---|---|---|---|
| 1 | 120102 | Tom | Zhou | W | 108250 | Sales Manager | AU | 17JAN1969 | 01JUN1989 |
| 2 | 120103 | Wilson | Zheng | M | 7715 | Sales Manager | AU | 23JAN1960 | 03JAN1973 |
| 3 | 120104 | Samantha | Elvish | F | 28600 | Sales Rep. II | AU | 02AUG1974 | 01JAN1974 |
| 4 | 120122 | Christina | Ngan | F | 27475 | Sales Rep. II | AU | 27JUL1978 | 01JUL1978 |
| 5 | 120123 | Kimiko | Hotstone | F | 28150 | Sales Rep. I | AU | 28SEP1964 | 01OCT1969 |

```
proc contents data=work.subset2a;

run;
```

### 部分 PROC CONTENTS 输出

| # | Variable | Type | Len | Format | Informat | Label |
|---|---|---|---|---|---|---|
| 1 | Birth_Date | Num | 8 | DATE8. | DATE8. | Birth Date |
| 2 | Country | Char | 2 | $2 | $2 | Country |
| 3 | Employee_ID | Num | 8 | $8 | $8 | Employee ID |
| 4 | First_Name | Char | 10 | $10. | $10. | First Name |
| 5 | Gender | Char | 1 | $1 | $1 | Gender |
| 6 | Hire_Date | Num | 8 | DATE8. | DATE8. | Hire Date |
| 7 | Job_Title | Char | 14 | $14. | $14. | Job Title |
| 8 | Last_Name | Char | 12 | $12. | $12. | Last Name |
| 9 | Salary | Num | 8 | | | Salary |

## IMPORT 过程

程序 `p106d04a` 是通过导入向导创建的。

```
PROC IMPORT OUT= WORK.subset2a

DATAFILE="S:\Workshop\sales.xls"

DBMS=EXCEL REPLACE;

RANGE="Australia$"

GETNAMES=YES;

MIXED=NO;

SCANTEXT=YES;

USEDATE=YES;

SCANTIME=YES;

RUN;
```

## 6.3 章节复习

1. 使用哪个语句指向包含 Excel 工作簿路径、文件名和扩展名的物理文件名？
2. 在 SAS 资源管理器中，Excel 工作表名称末尾会出现什么字符？
3. SAS 名称字面量（name literal）的示例是什么？
4. 如何取消库引用（libref）？

## 6.4 解决方案

### 1. 读取 Excel 工作表

- a. 获取初始程序。
- b. 添加一个 `LIBNAME` 语句。

```
libname custfm 'custfm.xls';

proc contents data=custfm._all_

run;

data work.males;

run;

proc print data=work.males label;

run;
```

- c. 提交 `LIBNAME` 语句和 `PROC CONTENTS` 步骤。
- d. 在 `DATA` 步中添加 `SET` 语句。

```
data work.males;

set custfm.'Males$';

run;
```

- e. 在 `DATA` 步中添加 `KEEP` 语句。

```
data work.males;

set custfm.'Males$';

keep First_Name Last_Name Birth_Date;

run;
```

- f. 在 `DATA` 步中添加 `FORMAT` 语句。

```
data work.males;

set custfm.'Males$';

keep First_Name Last_Name Birth_Date;

format Birth_Date year4.

run;
```

- g. 添加 `LABEL` 语句。

```
data work.males;

set custfm.'Males$';

keep First_Name Last_Name Birth_Date;

format Birth_Date year4.

label Birth_Date='Birth Year';

run;
```

- h. 提交程序。

### 2. 读取 Excel 工作表

- a. 编写一个 `LIBNAME` 语句。

```
libname prod 'products.xls';
```

- b. 编写一个 `PROC CONTENTS` 步骤。

```
proc contents data=prod._all_

run;
```

- c. 提交程序。
- d. 编写一个 `DATA` 步。

```
data work.golf;

set prod.'Sports$';

where Category='Golf'

drop Category;

label Name='Golf Products'

run;
```

- e. 编写一个 `LIBNAME` 语句。

```
libname prod clear;
```

- f. 编写一个 `PROC PRINT` 步骤。

```
proc print data=work.golf label;

run;
```

### 3. 读取 Excel 工作表的一个范围

- a. 编写一个 `LIBNAME` 语句。

```
libname xlsdata 'custcaaus.xls' header=no;
```

- b. 编写一个 `PROC CONTENTS` 步骤。

```
proc contents data=xlsdata._all_

run;
```

- c. 提交程序。
- d. 编写一个 `DATA` 步。

```
data work.germany;

set xlsdata.DE;

label F1='Customer ID'

F2='Country'

F3='Gender'

F4='First Name'

F5='Last Name'

F6='Birth Date'

format F6 ddmmyy8.;

run;
```

- e. 编写一个 `LIBNAME` 语句。

```
libname xlsdata clear;
```

- f. 编写一个 `PROC PRINT` 步骤。

```
proc print data=work.germany label;

run;
```

### 4. 使用 PROC COPY 创建 Excel 工作表

- a. 编写一个 `LIBNAME` 语句。

```
libname mnth 'mnth2007.xls';
```

- b. 编写一个 `PROC COPY` 步骤。

```
proc copy in=orion out=mnth;

select mnth7_2007 mnth8_2007 mnth9_2007;

run;
```

- c. 编写一个 `PROC CONTENTS` 步骤。

```
proc contents data=mnth._all_;

run;
```

- d. 编写一个 `LIBNAME` 语句。

```
libname mnth clear;
```

### 5. 使用导入向导读取 Excel 工作表

- a. 使用导入向导。

### 连接到 MS Excel

### 导入向导 - 选择表

### 导入向导 - 选择库和成员

- b. 编写一个 `PROC PRINT` 步骤。

```
proc print data=work.children;

run;
```

- c. 打开 `children.sas`。

```
PROC IMPORT OUT=children

DATAFILE="S:\Workshop\products.xls"

DBMS=EXCEL

RANGE="Children$"

GETNAMES=YES;

MIXED=NO;

SCAN=YES;

USEDATE=YES;

SCANTIME=YES;

RUN;
```

### 使用 EXPORT 过程创建 Excel 工作表

- a. 编写一个 `PROC IMPORT` 步骤。

```
proc export data=orion.mnth7_2007

outfile='mnth7.xls'

dbms=excel replace
```

- b. 提交程序。

### 学生解答

6.1 正确答案 哪个 `PROC PRINT` 步骤显示了来自美国的工作表？
- a. `proc print data=orion.'UnitedStates';`
- b. `proc print data=orion.'UnitedStates$'`
- c. `proc print data=orion.'UnitedStates';`
- d. `proc print data=orion.'UnitedStates$'`

## 章节复习解答

## 第 7 章 分隔数据

- 7.1 使用分隔数据作为输入...............................7-3
- 7.2 使用非标准分隔数据作为输入.........................7-30
- 7.3 章节复习......................................................7-48
- 7.4 解决方案...............................................7-49
- 学生解答.......................................7-52
- 章节复习解答.....................................7-55

### 7.1 使用分隔数据作为输入

目标
- 使用 `DATA` 步从分隔文件中创建 SAS 数据集。
- 查看原始数据文件时 `DATA` 步的编译和执行阶段。
- 通过 `LENGTH` 语句显式定义变量长度。

### 业务场景

现有数据源包含来自澳大利亚和美国的销售信息。需要创建该数据源的子集。新的 SAS 数据集必须包含：
- 仅来自澳大利亚的销售代表
- 员工的姓、名、工资、职位和入职日期
- 描述符部分的标签和格式

### 业务场景

| 读取 SAS 数据集 | `libname data_; set data_; run;` |
|---|---|
| 读取 Excel 工作表 | `libname data_; set data_; run;` |
| 读取分隔原始文件 | `data infile_; run;` |

### sales.csv

部分 `sales.csv`

```
12102,Tom,Zhou,M,10825,Sales Manager,AU,11AUG1969,02MAR1970

12103,William,Dawes,M,87975,Sales Manager,AU,22JAN1974,01/01/1974

12104,Irene,French,F,26648,Sales Rep,II,02AUG1949,01/01/1974

12105,Christina,Ngan,F,27275,Sales Rep,II,27JUL1954,07/01/1978

12106,Kevin,Holmes,F,26390,Sales Rep,AU,01SEP1964,10/01/1985

12107,Lucian,Damonyd,M,26640,Sales Rep,AU,13MAY1959,03/01/1979

12108,George,Hofmeister,M,32040,Sales Rep,IV,06DEC1954,01/01/1963

12109,Satskyam,Denny,M,26780,Sales Rep,II,08SEP1988,08/01/2006

12110,Jackson,Tahoe,M,31938,Sales Rep,II,05MAR1953,01/01/1992

12111,Monika,Kletsch,F,30890,Sales Rep,IV,14JUN1986,11/01/2006

12112,Alvin,Roebeck,M,30070,Sales Rep,III,22NOV1964,10/01/1985

12113,Kevin,Lyon,M,26955,Sales Rep,I,14DEC1984,05/01/2006
```
