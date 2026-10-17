
2. 在输出窗口中查看 `PROC CONTENTS` 和 `PROC PRINT` 结果。

3. 选择 SAS 栏上的资源 (Explorer) 选项卡以激活资源管理器，或者选择 查看 (View) ⇨ 仅内容 (Contents Only)

![](img/1698e3a97543d6895ff5297aae8fd042_218_0.png)

双击库 (Libraries) 显示所有可用库。

![](img/1698e3a97543d6895ff5297aae8fd042_219_0.png)

双击 `Orionxls` 库以显示该库的所有 Excel 工作表。

提交最后一个 `LIBNAME` 语句以解配库引用。

## 练习题

### 第一级

#### 1. 读取 Excel 工作格

- a. 获取起始程序 `p106e01`。
- b. 在 `PROC CONTENTS` 步骤之前添加 `LIBNAME` 语句，创建一个名为 `CUSTOM` 的库引用（libref），引用名为 `custfm.xls` 的 Excel 工作簿。
- c. 提交 `LIBNAME` 语句和 `PROC CONTENTS` 步骤，创建以下 `PROC CONTENTS` 报告：

第 1 页，共 3 页

| CONTENTS 过程 | |
| :--- | :--- |
| 目录 | Libref: CUSTOM |
| 引擎 | EXCEL |
| 物理名称 | custfm.xls |
| 用户 | Admin |
| # 名称 | 成员类型 | 成员类型 |
| 1 Females$ | DATA | TABLE |
| 2 Males$ | DATA | TABLE |

- d. 在 `DATA` 步中添加 `SET` 语句，读取包含男性数据的工作格。
- e. 在 `DATA` 步中添加 `KEEP` 语句，仅包含 `First_Name`、`Last_Name` 和 `Birth_Date` 变量。
- f. 在 `DATA` 步中添加 `FORMAT` 语句，将 `Birth_Date` 显示为四位年份。
- g. 添加 `LABEL` 语句，将 `Birth_Date` 的列标题更改为 `Birth Year`。
- h. 提交包含最后一个 `LIBNAME` 语句的程序，并创建以下 `PROC PRINT` 报告：

部分 `PROC PRINT` 输出（47 个观测值的前 5 个）

| 观测值 | 名 | 姓 | 年份 |
| :--- | :--- | :--- | :--- |
| 1 | James | Kvarniq | 1974 |
| 2 | David | Black | 1969 |
| 3 | Markus | Sepke | 1988 |
| 4 | Ulrich | Heyde | 1939 |
| 5 | Jimmie | Evans | 1954 |

### 第二级

#### 2. 读取 Excel 工作格

- a. 写一个 `LIBNAME` 语句创建一个名为 `PROD` 的库引用，引用名为 `products.xls` 的 Excel 工作簿。
- b. 写一个 `PROC CONTENTS` 步骤查看 `PROD` 的所有内容。
- c. 提交程序确定 `products.xls` 中四个工作格的名称。
- d. 写一个 `DATA` 步读取包含运动数据的工作格，创建一个名为 `Work.golf` 的新数据集。

`Work.golf` 数据集应该：
- 仅包含 `Category` 等于 `Golf` 的观测值
- 不包含 `Category` 变量
- 为 `Name` 变量包含为 `Golf Products` 的标签。

- e. 写一个 `LIBNAME` 来创建 `PROD` 库引用。
- f. 写一个 `PROC PRINT` 步骤创建以下报告：

部分 `PROC PRINT` 输出（56 个观测值的前 10 个）

| 观测值 | Golf Products |
| :--- | :--- |
| 1 | Ball Bag |
| 2 | Red/White/Black Staff 9 Bag |
| 3 | Tee Holder |
| 4 | Bb Softspikes - Xp 22-pack |
| 5 | Bretagne Performance Tg Men's Golf Shoes L. |
| 6 | Bretagne Soft-Tech Men's Glove, left |
| 7 | Bretagne St2 Men's Golf Glove, left |
| 8 | Bretagne Stabilites 2000 Goretex Shoes |
| 9 | Bretagne Stabilities Tg Men's Golf Shoes |
| 10 | Bretagne Stabilities Women's Golf Shoes |

### 第三级

#### 3. 读取 Excel 工作格的范围

- a. 写一个 `LIBNAME` 语句创建一个名为 `custaux.xls` 的库引用。此 Excel 工作簿没有列名。在 `LIBNAME` 语句中添加相应的选项，不使用第一行数据作为列名。

相应选项的文档可以在 SAS Help and Documentation 的 Contents 选项卡找到（SAS Products ⇒ SAS/ACCESS ⇒ SAS/ACCESS 9.2 for PC Files: Reference ⇒ LIBNAME Statement and Pass-Through Facility on 32-Bit Microsoft Windows ⇒ File-Specific Reference ⇒ Excel Workbook Files）。

- b. 写一个 `PROC CONTENTS` 步骤查看 `XLSDATA` 的所有内容。

#### 6.1 使用 Excel 数据作为输入

- c. 提交程序。Excel 范围内任何不包含美元符号名称的成员。
- d. 写一个 `DATA` 步读取包含德国 (DE) 的范围，创建一个名为 `Work.germany` 的新数据集。根据所需的报告添加恰当的标签和格式。
- e. 写一个 `LIBNAME` 来清除 `XLSDATA` 库引用。
- f. 写一个 `PROC PRINT` 步骤创建以下报告：

| 观测值 | ID | 国家 | 性别 | 名 | 姓 | 日期 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 9 | DE | F | Cornelia | Krahl | 27/02/74 |
| 2 | 11 | DE | F | Elke | Wallstab | 16/08/74 |
| 3 | 13 | DE | M | Markus | Sepke | 21/07/88 |
| 4 | 16 | DE | M | Ulrich | Heyde | 16/01/39 |
| 5 | 19 | DE | M | Oliver S. | Füß | 23/02/64 |
| 6 | 33 | DE | M | Rolf | Robak | 24/02/39 |
| 7 | 42 | DE | M | Thomas | Leitmann | 09/02/79 |
| 8 | 50 | DE | M | Gert-unter | Mendler | 16/01/34 |
| 9 | 61 | DE | M | Carsten | Maestr | 08/07/44 |
| 10 | 65 | DE | F | Ines | Deisser | 20/07/69 |

#### 6.2 更多 Excel 操作（自学）

##### 目标
- 使用 `DATA` 步从数据集创建 Excel 工作格。
- 使用 `COPY` 过程创建 Excel 工作格。
- 使用 `IMPORT` 向导读取 Excel 工作格。
- 使用 `EXPORT` 向导创建 Excel 工作格。

##### 创建工作格
除了读取外，`SAS/ACCESS LIBNAME` 语句配合 `DATA` 步也可以创建 Excel 工作格。

```sas
libname orionxls 'workspace\qtr2007.xls';

data orionxls.qtr1_2007;

  set orionxls.qtr1_2007;

run;

data orionxls.qtr2_2007;

  set orionxls.qtr2_2007;

run;

proc contents data=orionxls._all_;

run;

libname orionxls;
```

##### 创建工作格
部分 SAS Log
```sas
data orionxls.qtr1_2007;

  set orionxls.qtr1_2007;

run;
```
NOTE: SAS 变量标签、格式未写入数据库。
NOTE: ORION.QTR1_2007 有 22 个观测值。

```sas
data orionxls.qtr2_2007;

  set orionxls.qtr2_2007;

run;
```
NOTE: SAS 变量标签、格式未写入数据库。
NOTE: ORION.QTR2_2007 有 36 个观测值。

##### 创建工作格
部分 `PROC CONTENTS` 输出

| CONTENTS 过程 目录 | |
| :--- | :--- |
| 库引用 | ORIONLS |
| 引擎 | EXCEL |
| 物理名称 | qtr2007a.xls |
| 用户 | Admin |

| 名称 | 成员类型 |
| :--- | :--- |
| 1 | qtr1_2007$ DATA |
| 2 | qtr2_2007$ DATA |
| 3 | qtr2_2007 DATA |
| 4 | qtr2_2007$ DATA |

![](img/1698e3a9754d6895ff5297ae8fd042_224_0.png)

在 Excel 中，命名区域是单元格区域的描述性名称。

##### 创建工作格

| Order_Id | 类型 |  | 订单日期 |交付日期 |
| :--- | :--- | :--- | :--- | :--- |
| 124165073 | 24 | | 1/5/07 | 1/14/07 |
| 1241685379 | 89 | | 1/30/07 | 2/10/07 |
| 1241686271 | 13 | | 2/14/07 | 2/21/07 |
| 1241689282 | 53 | | 2/27/07 | 3/9/07 |
| 1241690441 | 53 | | 3/12/07 | 3/21/07 |
| 1241702920 | 171 | | 3/30/07 | 4/8/07 |
| 1241703172 | 3953 | | 4/6/07 | 4/15/07 |
| 1241712465 | 25 | | 4/17/07 | 4/26/07 |
| 1241713813 | 2686 | | 4/30/07 | 5/9/07 |
| 1241714456 | 10 | | 5/10/07 | 5/19/07 |
| 1241715145 | 171 | | 5/14/07 | 5/23/07 |
| 1241716486 | 18 | | 5/22/07 | 5/31/07 |
| 1241716538 | 24 | | 6/3/07 | 6/12/07 |
| 1241718029 | 70183 | | 6/7/07 | 6/16/07 |
| 1241718620 | 19 | | 6/11/07 | 6/20/07 |

## 导入/导出向导和过程

向导和过程具有相似的功能；向导是点击式界面，而过程是基于代码的。

要在 SAS 窗口环境中调用向导，请选择**文件 (File)** 和**导入数据 (Import Data)** 或**导出数据 (Export Data）**。

![](img/1698e3a97543d6895ff5297aae8fd042_227_0.png)

### 导入向导

导入向导允许您从外部数据源读取数据并写入 SAS 数据集。

- 导入向导的步骤：
1. 选择要导入的文件类型。
2. 找到输入文件。
3. 选择要导入数据的表格范围或工作表。
4. 选择存储导入文件的位置。
5. 保存生成的 `PROC IMPORT` 代码。（可选）

#### 导入向导

1. 选择要导入的文件类型。

![](img/1698e3a97543d6895ff5297aae8fd042_228_0.png)

#### 导入向导

2. 找到输入文件。

![](img/1698e3a97543d6895ff5297aae8fd042_228_1.png)

#### 导入向导

3. 选择要导入数据的表格范围或工作表。

![](img/1698e3a97543d6895ff5297aae8fd042_229_0.png)

#### 导入向导

4. 选择存储导入文件的位置。

![](img/1698e3a97543d6895ff5297aae8fd042_229_1.png)

#### 6.2 使用 Excel 工作表的更多操作（自学）

#### 5. 保存生成的 `PROC IMPORT` 代码。（可选）

##### 导入向导：创建 SAS 语句

导入向导可以创建一个包含 `PROC IMPORT` 语句的文件，这些语句可以在 SAS 程序中再次导入数据。
如果您希望这些语句是永久的，请输入要保存它们的文件名：

![](img/1698e3a97543d6895ff5297aae8fd042_230_0.png)

##### 导入向导

###### SAS Log

NOTE: `WORK.SUBSET2A` 数据集成功创建。

```sas
proc print data=work.subset2a;

run;
```

###### 部分 `PROC PRINT` 输出

| Employees Obs ID | First_Name | Last_Name | Gender | Salary | Job Title | Country | Birth Date | Hire_Date |
|---|---|---|---|---|---|---|---|---|
| 1 | 120102 | Tom | Zhou | W | 108250 | Sales Manager | AU | 17JAN1969 | 01JUN1989 |
| 2 | 120103 | Wilson | Zheng | M | 7715 | Sales Manager | AU | 23JAN1960 | 03JAN1973 |
| 3 | 120104 | Samantha | Elvish | F | 28600 | Sales Rep. II | AU | 02AUG1974 | 01JAN1974 |
| 4 | 120122 | Christina | Ngan | F | 27475 | Sales Rep. II | AU | 27JUL1978 | 01JUL1978 |
| 5 | 120123 | Kimiko | Hotstone | F | 28150 | Sales Rep. I | AU | 28SEP1964 | 01OCT1969 |

##### 导入向导

```sas
proc contents data=work.subset2a;

run;
```

###### 部分 `PROC CONTENTS` 输出

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

##### IMPORT 过程

程序 `p106d04a` 是通过导入向导创建的。

```sas
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
