
部分 `PROC PRINT` 输出

| Last_Name | First_Name | Salary |
|---|---|---|
| Denny Kletschkus | Satyakam | 26780 |
| Lyon | Monica | 30890 |
| Kevin | Kevin | 26955 |
| Soltau | Petra | 27440 |
| Iyengar | Marina | 29715 |
| Duckett | Shani | 25795 |
| Wilson | Frank | 26810 |
| Minas | Michael | 26970 |
| Liebman | Amanda | 27465 |
| Eastley | Vincent | 20965 |

## 练习

### 第一级

#### 1. 检查数据部分

a. 获取初始程序 `p104e1`。
b. 在 `PROC CONTENTS` 步骤之后，添加一个 `PROC PRINT` 步骤来显示名为 `Work` 的数据集的所有观测值、所有变量和 `Obs` 列。
c. 提交程序以创建以下 `PROC PRINT` 报告：

部分 `PROC PRINT` 输出（124 个观测值中的前 10 个）

| Obs | ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Total |
|---|---|---|---|---|---|---|
| 1 | 120265 | | | | | 25 |
| 2 | 120267 | 15 | 15 | | | 60 |
| 3 | 120269 | 20 | 20 | | | 80 |
| 4 | 120270 | 20 | 10 | 5 | | 35 |
| 5 | 120271 | | 20 | 20 | | 80 |
| 6 | 120272 | 10 | 10 | 10 | | 40 |
| 7 | 120275 | | 15 | 15 | | 60 |
| 8 | 120660 | 25 | 25 | | | 100 |
| 9 | 120662 | 10 | | | | 20 |
| 10 | 120663 | | | | | 5 |

d. 在 `PROC PRINT` 步骤中，添加 `VAR` 语句和 `NOOBS` 选项，仅显示 `Employee_ID` 和 `Total` 变量。
e. 提交程序以创建以下 `PROC PRINT` 报告：

部分 `PROC PRINT` 输出（124 个观测值中的前 10 个）

| Employee_ID | Total |
|---|---|
| 120265 | 25 |
| 120267 | 60 |
| 120269 | 80 |
| 120270 | 35 |
| 120271 | 80 |
| 120272 | 40 |
| 120275 | 60 |
| 120660 | 100 |
| 120662 | 20 |
| 120663 | 5 |

### 第二级

#### 2. 检查描述符部分

a. 获取初始程序 `p104e2`。
b. 在 `PROC CONTENTS` 步骤之后，添加 `PROC PRINT` 步骤来显示 `Work` 的描述符。
c. 提交程序并回答以下问题：
数据中有多少个观测值？
数据中有多少个变量？
数据集的长度是多少？
d. 在 `PROC CONTENTS` 步骤之后，添加带有选项的 `PROC PRINT` 语句来显示 `Work`。
e. 提交程序创建以下 `PROC PRINT` 报告：

| Product_Name | Supplier_Name |
|---|---|
| Black | Top Sports |
| Large | Top Sports |
| Base | Top Sports |
| Duffle | Top Sports |
| Feel | Top Sports |
| Jaguar | Top Sports |
| Feather | Top Sports |
| Gold | Top Sports |
| Olive | Top Sports |
| Deer | SAS.a. |
| Westker | SAS.a. |
| Hammock | SAS.a. |
| Sioux | SAS.a. |
| West | Miller Inc. |

## 4.1 检查描述符和数据部分

### 第三级

#### 3. 使用时间和日期值

a. 获取并提交初始程序 `p104e3`。
b. 注意 `PROC PRINT` 输出中的 `CurrentTime` 和 `CurrentDateTime`。
c. 使用帮助功能查找关于 SAS 如何存储时间的文档。进入 `CONTENTS` 帮助标签并选择 `SAS Products` ⇒ `Base SAS` ⇒ `SAS 9.2 Language`。
d. 完成以下：
时间值是自今天午夜以来的秒数。
日期值是自 1960 年 1 月 1 日以来的秒数。

## 4.2 访问库

目标
* 解释 SAS 库的概念。
* 使用 `LIBNAME` 语句分配库引用名 (`libref`)。
* 说明永久库和临时库的区别。
* 使用 `CONTENTS` 过程浏览库的内容。
* 使用资源管理器调查库。

### SAS 库

你可以将 SAS 库想象成文件柜中的一个抽屉，数据集是其中的一个文件。

| 基于目录的系统 | SAS 库是一个目录。 |
|---|---|
| Windows 示例：`s:\workshop` | |
| UNIX 示例：`/users/userid` | |
| z/OS (3960) 示例：`userid.workshop.sasdata` | |

### 分配库

无论使用哪种操作系统，都通过为每个库分配引用名 (`libref`) 来标识 SAS 库。

### SAS 库

当 SAS 会话启动时，SAS 会自动创建一个临时库和一个永久库供你访问。

`Work` – 临时库
`Sasuser` – 永久库

`Work` 库及其 SAS 数据文件在 SAS 会话结束后会被删除。

在永久库中的 SAS 数据集在 SAS 会话结束后将会保存。

### SAS 库

你还可以创建并访问自己的永久库。

`orion` – 永久库

## 建立连接

当你提交 `LIBNAME` 语句时，SAS 中的 `libref`（库引用名）与你操作系统上文件的物理位置之间就会建立起连接。

![](img/1698e3a97543d6895ff5297aae8fd042_121_0.png)

当你的会话结束时，`libref` 与文件物理位置之间的链接就会断开。

## 4.05 调查

在交互式 SAS 会话中，每当你提交一个程序时，必须重新提交 `LIBNAME` 语句。

- 正确
- 错误

## 两级 SAS 文件名

每个 SAS 文件都有一个两个层级的名称：`libref.filename`

数据集 `orion.sales` 是 `orion` 库中的一个 SAS 文件。

- 第一个名称（`libref`）指库（library）。
- 第二个名称（`filename`）指库中的文件。

![](img/1698e3a97543d6895ff5297aae8fd042_122_0.png)

## 临时 SAS 文件名

如果省略 `libref`，默认的 `libref` 为 `Work`。

![](img/1698e3a97543d6895ff5297aae8fd042_122_1.png)

```sas
data NewSalesEmps;

  length FirstName $ 12 Job Title $ 25 LastName $ 18;

  infile 'newemps.csv' dlm=',';

  input FirstName $ LastName $ Job_Title $ Salary;

run;

proc print data=work.NewSalesEmps;

run;
```

## 浏览 SAS 数据库

![](img/1698e3a97543d6895ff5297aae8fd042_123_0.png)

SAS 资源器允许你在窗口化环境中管理文件。

在 SAS 资源器中，你可以执行以下操作：

- 查看当前 SAS 会话期间所有可用库的列表
- 导航以查看特定库的所有成员
- 显示 SAS 数据集的描述部分（descriptor portion）

## 浏览 SAS 数据库

在许多主机上，SAS 窗口环境默认打开 SAS 资源器。如果它没有默认出现，你可以发出 `SAS EXPLORER` 命令来调用此窗口。

可以通过选择以下项打开 SAS 资源器：

- 仅查看内容 (View Contents Only)

或

- 资源器视图 (View Explorer)

在“仅查看内容”视图中，SAS 资源器是一个面板窗口，包含你的 SAS 环境的内容。当你打开文件夹时，文件夹内容将替换相同窗口中之前的内容。

在 SAS 资源器窗口的资源器视图中，文件夹显示在左侧的树视图中，文件夹内容显示在右侧的列表视图中。

带有 `_ALL_` 关键字的 `CONTENTS` 过程会生成数据库中所有 SAS 文件的列表。

```sas
PROC CONTENTS DATA=libref._ALL_ NODS;

   RUN;
```

- `NODS` 选项抑制数据集的描述部分。
- `NODS` 仅配合 `_ALL_` 关键字使用。

如果你使用的是非交互式或批量 SAS 会话，`CONTENTS` 过程是 `EXPLORER` 命令的替代方案。

## 访问和浏览 SAS 数据库 – Windows

`p104d04`

1. 获取并检索以确认程序 `p104d04`。

```sas
libname orion 's:\workshop';

proc contents data=orion.all_ nodes;

run;
```

2. 检查日志以确认 `orion` `libref` 已分配。

```sas
libname orion 's:\workshop';

NOTE: Libref. ORION was successfully assigned as follows:

Engine: V9

Physical Name: s:\workshop
```

3. 在输出窗口中查看 `PROC CONTENTS` 输出。

部分 `PROC CONTENTS` 输出

`CONTENTS` 过程

目录

| # own | 成员类型 | 文件大小 | 最后修改时间 |
| :--- | :--- | :--- | :--- |
| | Libref | | ORION |
| | Engine | | V9 |
| | Physical Name | | s:\workshop |
| | File Name | | s:\workshop |
| 1 BUDGET | DATA | 5120 | 12Feb08:00:57 |
| 2 COUNTRY | DATA | 17408 | 12Feb08:00:57 |
| | COUNTRY | INDEX | 17408 | 12Feb08:00:57 |
| 3 CUSTOM | DATA | 33792 | 12Feb08:00:57 |
| 4 CUSTOM_DIM | DATA | 33792 | 12Feb08:00:57 |
| 5 CUSTOM_TYPE | DATA | 17408 | 12Feb08:00:57 |
| | CUSTOM_TYPE | INDEX | 9216 | 12Feb08:00:57 |
| 6 EMPLOYEE_ADDRESSES | DATA | 74752 | 12Feb08:00:57 |
| 7 EMPLOYEE_DONATIONS | DATA | 25600 | 12Feb08:00:57 |
| 8 EMPLOYEE_ORGANIZATION | DATA | 41984 | 12Feb08:00:57 |
| 9 EMPLOYEE_PAYROLL | DATA | 33792 | 12Feb08:00:57 |
| 10 LOOKUP_COUNT | DATA | 37888 | 12Feb08:00:57 |
| 11 MNTH7_2007 | DATA | 5120 | 12Feb08:00:57 |
| 12 MNTH8_2007 | DATA | 5120 | 12Feb08:00:57 |
| 13 MNTH9_2007 | DATA | 5120 | 12Feb08:00:57 |
| 14 NONSALES | DATA | 33792 | 12Feb08:00:57 |

## 4.2 访问 SAS 库

4. 在 SAS 窗口上选择资源器选项卡以激活 SAS 资源器，或选择[仅查看内容](img/1698e3a97543d6895ff5297aae8fd042_126_0.png)。5. 双击库以显示所有库](img/1698e3a97543d6895ff5297aae8fd042_126_1.png)。

## 第 4 章 熟悉数据集

6. 双击 `Orion` 库显示该库的所有成员](img/1698e3a97543d6895ff5297aae8fd042_127_0.png)。
7. 右键点击 `Sales` 数据集并选择属性](img/1698e3a97543d6895ff5297aae8fd042_127_1.png)。此视图提供了数据集的常规信息，例如存储它的库、创建日期、观测数量等。你可以选择属性窗口顶部的“列”选项卡来获取有关列的特定信息。8. 关闭属性窗口。9. 双击 `Sales` 数据集或右键点击文件打开。`orion.sales` 的视图所示：

| ID | 名字 | 姓 | 性别 | 职位 | 出生日期 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 12102 | Zhou | M | 10250 | 1979 |
| 2 | 12103 | Wilson | M | 8975 | 1956 |
| 3 | 12101 | Jervey | E | 26800 | 1984 |
| 4 | 12102 | Wright | F | 27465 | 198 |
| 5 | 12103 | Kiminko | M | 26910 | 1973 |
| 6 | 12104 | Duncan | M | 26480 | 123 |
| 7 | 12105 | Forest | F | 33040 | 185 |
| 8 | 12106 | Sajalak | M | 26780 | 1043 |
| 9 | 12107 | Shayn | M | 28100 | 694 |
| 10 | 12108 | Myrta | F | 20985 | 965 |
| 11 | 12109 | Alvin | M | 30600 | 178 |
| 12 | 12110 | Kevin | L | 26995 | 914 |
| 13 | 12111 | Maruki | M | 32600 | 720 |
| 14 | 12112 | Fanieose | K | 29525 | -3952 |
| 15 | 12113 | Petra | S | 28915 | -398 |
| 16 | 12114 | Sofia | F | 27440 | 9606 |
| 17 | 12115 | Platts | M | 32430 | 331 |
| 18 | 12116 | August | L | 29605 | 719 |
| 19 | 12117 | Mariger | F | 25785 | 701 |
| 20 | 12118 | Shani | D | 26010 | 701 |
| 21 | 12119 | Young | W | 26810 | 976 |
| 22 | 12120 | Melba | F | 27465 | 1045 |
| 23 | 12121 | Amanda | E | 28905 | 1025 |
| 24 | 12122 | Vincent | E | 28905 | 9661 |
| 25 | 12123 | Phil | F | 26790 | 25 |
| 26 | 12124 | Varee | B | 30625 | 956 |
| 27 | 12125 | Sandy | M | 26030 | 31 |
| 28 | 12126 | Cecile | F | 29965 | 42 |
| 29 | 12127 | Roland | M | 25980 | 47 |
| 30 | 12128 | Michael | Z | 28480 | 53 |
| 31 | 12129 | Jace | L | 25430 | 54 |
| 32 | 12130 | John | F | 29965 | 6 |

## 访问和浏览 SAS 数据库 – UNIX

`p104d04`

1. 获取并检索以确认程序 `p104d04`。

```sas
libname orion '/users/userid';

proc contents data=orion.all_ nodes;

run;
```
