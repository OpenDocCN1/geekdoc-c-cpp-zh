
### 3. 使用 `LIKE` 运算符和 `KEEP=` 选项

- a. 编写 `DATA` 步。
```sas
data work.tony;
  set orion.customer_dim;
  where Customer_FirstName like 'TOM%';
run;
```
- b. 在 `DATA` 步中添加 `WHERE` 语句。
```sas
data work.tony;
  set orion.customer_dim;
  where Customer_FirstName = 'TONIE';
run;
```
- c. 在 `SET` 语句中使用 `KEEP=` 选项。
```sas
data work.tony;
  set orion.customer_dim(keep=Customer_FirstName Customer_LastName);
  where Customer_FirstName = 'TONIE';
run;
```
- d. 编写 `PROC PRINT` 步。
```sas
proc print data=work.tony;
run;
```

### 4. 为 `Work.youngadult` 添加永久属性

- a. 获取并提交程序。
```sas
data work.youngadult;
  set orion.customer_dim;
  where Customer_Gender='F' and
        Customer_Age between 18 and 36
        Customer Group contains 'Gold';
  keep Customer_Name Customer_Age Customer_Date Customer_Gender Customer_Group;
run;
```

### 5. 为 `Work.sports` 添加永久属性

- a. 编写并提交程序。
```sas
data work.sports;
  set orion.product_dim;
  where Supplier Country in ('ES','NL') and
        Category like '%Sports%';
  drop Obs;
run;
```
- b. 编写 `PROC PRINT` 步。
```sas
proc print data=work.sports;
run;
```
- c. 在 `DATA` 步中添加 `LABEL` 语句和 `FORMAT` 语句。
```sas
data work.sports;
  set orion.product_dim;
  where Supplier Country in ('ES','NL') and
        Category like '%Sports%';
  label Category='Sports Category'
        Product_Name='Product Name (Abbrev)'
        Supplier_Name='Supplier Name (Abbrev)';
  format Category $20.
         Product_Name $15.
         Supplier_Name $15;
  drop Obs;
run;
```

# 5.04 练习 – 正确答案

根据 `WHERE` 语句，哪个值不会被返回？

- a. Office Rep
- b. Sales Rep. IV
- c. service rep III
- d. Representative

```sas
where Job_Title contains 'Rep';
```

# 5.05 练习 – 正确答案

对于给定值，哪个 `WHERE` 语句会返回所有名字以字母 M 开头的观测值？

- a. `where Name like '_, M%';`
- b. `where Name like '%, M%';`
- c. `where Name like '_, M%';`
- d. `where Name like '%, M_';`

| Name |
| --- |
| Elvish, Ienie |
| Ngan, Kimiko |
| Holstone, Sharon |
| Daymond, Lucian |
| Holmster, Fong |
| Denny, Stephen |
| Clarkson, Sharon |
| Kletshchnus, Monica |

![](img/1698e3a97543d6895ff5297aae8fd042_200_0.png)

# 5.06 练习 – 正确答案

哪种数值格式会在标准数值数据前写入导零？

`Zw.d`

`Zw.d` 格式与 `w.d` 格式相似，区别在于 `Zw.d` 用零而不是空格填充右对齐输出。

# 5.07 练习 – 正确答案

哪个 `FORMAT` 语句创建了输出？

- a. `format Birth Date Hire Date ddmmyy9. Term_Date mmyy7;`
- b. `format Birth Date Hire Date ddmmyyyy. Term_Date myyyyyy;`
- c. `format Birth Date Hire Date ddmmyyyy10. Term_Date monyy7;`

| Birth_Date | Hire_Date | Term_Date |
|---|---|-- |
| 21/05/1969 | 15/10/1992 | MAR2007 |

# 5.08 练习 – 正确答案

有多少种日期格式以 EUR 开头？

九个

示例：
`EURDFDDw.` 格式将国际 SAS 日期值以 `dd.mm.yy` 或 `dd.mm.yyyy` 的形式写入。

# 章末练习答案

![](img/1698e3a97543d6895ff5297aae8fd042_203_0.png)

![](img/1698e3a97543d6895ff5297aae8fd042_203_1.png)

# 第 6 章 读取 Excel 工作表

- 6.1 使用 Excel 数据作为输入............................................................................... 6-3
  演示：读取 Excel 工作表 – Windows............................................... 6-15
  练习.................................................................................................................... 6-17
- 6.2 深入使用 Excel 工作表（自学）。....................................... 6-20
  练习.................................................................................................................... 6-36
- 6.3 章末练习........................................................................................... 6-37
- 6.4 答案 ................................................................................................ 6-38
  练习答案 ....................................................................... 6-38
  学生活动答案（投票/测试）....................................................... 6-43
  章末练习答案 ................................................ 6-44

# 6.1 使用 Excel 数据作为输入

执行此操作必须拥有 SAS/ACCESS

### 目标
- 使用 `DATA` 步从 Excel 工作表创建 SAS 数据集。
- 使用 SAS/ACCESS `LIBNAME` 语句像读取 SAS 数据集一样读取 Excel 工作表。

### 业务场景

现有的数据源包含来自澳大利亚和美国的 Orion Star 销售人员信息。
需要创建一个新的 SAS 数据集，它是该现有数据源的子集。
该新的 SAS 数据集必须包含：
- 来自澳大利亚的员工
- 员工的姓名、姓氏、薪水、职位和入职日的描述符和格式

| Reading SAS Data Sets | | |
| | | |
| Reading Excel Worksheets | | |
| Reading Delimited Data Files | | |
| Reading SAS Data Sets | `libname data; set; ... run;` |
| Reading Excel Worksheets | `libname data; set; ... run;` |
| Reading Delimited Data Files | `data infile; input; ... run;` |

在读取 SAS 数据集和 Excel 工作表时，`LIBNAME` 语句引用 SAS 库。

### 业务场景语法

使用以下语句完成场景：

```sas
LIBNAME libref 'physical-file-name';

DATA output-SAS-data-set;
  SET input-SAS-data-set;
  WHERE where-expression;
  KEEP variable-list;
  LABEL variable = 'label'
        variable = 'label'
        variable = 'label';
  FORMAT(s) format;
RUN;
```

| Employee ID | First Name Last Name | Gender | Salary Job Title | Country | Birth Date | Hire Date |
|---|---|---|---|---|---|---|
| 12050 | John Doe | M | 25000 Sales Manager | AU | 17-Jan-1965 | 06/Jun/85 |
| 12051 | Jane Smith | F | 26000 Sales Rep. | AU | 24-Aug-1965 | 01/Jul/74 |
| 12052 | Kevin White | M | 26100 Sales Rep. | AU | 20-Sep-1964 | 01/Oct/79 |
| 12053 | Kelly Green | F | 21500 Sales Rep. | AU | 20-Sep-1968 | 10/Oct/69 |
| 12054 | Michael Brown | M | 24000 Sales Manager | AU | 15-Dec-1960 | 03/Oct/78 |
| 12055 | Heather Davis | F | 25000 Sales Rep. | AU | 11-May-1972 | 03/Jul/71 |
| 12056 | Steven Clark | M | 29100 Sales Rep. | AU | 4-Jan-1967 | 11/Nov/68 |
| 12057 | Sarah Scott | F | 28500 Sales Rep. | AU | 12-Feb-1966 | 01/Aug/72 |
| 12058 | Paul Young | M | 28000 Sales Rep. | AU | 22-Sep-1962 | 10/Oct/69 |
| 12059 | Linda Hall | F | 21500 Sales Rep. | AU | 24-Aug-1964 | 01/Oct/75 |
| 12060 | Mark Wright | M | 27400 Sales Rep. | AU | 10-Sep-1967 | 01/Aug/71 |
| 12061 | Alice Baker | F | 28250 Sales Rep. | AU | 5-Aug-1969 | 01/Jul/74 |
| 12062 | James Hill | M | 29000 Sales Rep. | AU | 21-Jun-1968 | 01/Sep/71 |
| 12063 | Susan Martin | F | 27100 Sales Rep. | AU | 13-Mar-1970 | 01/Aug/73 |

## `LIBNAME` 语句（回顾）

`LIBNAME` 语句将库引用（libref）分配给 SAS 数据库。

`LIBNAME` 语句的通用形式：

```sas
LIBNAME libref 'SAS-data' <options>;
```

示例：

![](img/1698e3a97543d6895ff5297aae8fd042_209_png)

`LIBNAME` 语句需要引用特定于你的操作环境的 SAS 数据库。

## SAS/ACCESS `LIBNAME` 语句

SAS/ACCESS `LIBNAME` 语句扩展了 `LIBNAME`，支持为 Microsoft Excel 分配库引用。

SAS/ACCESS `LIBNAME` 语句的通用形式：

```sas
LIBNAME libref 'file-name' <options>;
```

这允许你在 `DATA` 步或过程中直接引用工作表，并像处理 SAS 数据集一样读写 Excel 工作表。

`LIBNAME` 语句可以使用 SAS/ACCESS 选项。

例如，

`MIXED=YES | NO`

> 指定是否将具有混合数据类型的列的数值数据转换为字符数据。
> 默认值为 `NO`，这意味着数值数据将作为字符列中的缺失值导入。

以下技术支持说明了作为缺失值导入的列数据：

http://support.sas.com/kb/6/123.html

## SAS/ACCESS `LIBNAME` 语句

需要 SAS/ACCESS Interface to PC Formats 才能使用 SAS/ACCESS `LIBNAME` 语句访问 Excel 工作簿。

示例：

```sas
libname orionxls 's:\workshop\sales.xls';
```

![](img/1698e3a97543d6895ff5297aae8fd042_211_0.png)

SAS/ACCESS Interface to PC Formats 允许从 PC 文件读取数据，在 SAS 报告或应用程序中使用这些数据，并使用 SAS 数据集创建各种格式的 PC 文件。

SAS/ACCESS Interface to PC Formats 提供对 Microsoft Excel, Microsoft Access, dBase, JMP, Lotus 1-2-3, SPSS, Stata 和 Paradox 的访问。

要确定你是否拥有 SAS/ACCESS Interface to PC Formats 的许可证，请提交以下步骤：

```sas
proc setinit;
```

提交后，在 SAS 日志中查看你站点授权的产品。

Linux 和 UNIX 上的 SAS/ACCESS Interface to PC Formats 允许从 Linux 和 UNIX 环境访问 PC 文件。使用 PC Files Server 访问 PC 数据。PC Files Server 运行在 Microsoft Windows 服务器上，而 SAS/ACCESS Interface to PC Formats 运行在 Linux 或 UNIX 客户端服务器上。

# SAS 资源管理器窗口

Excel 工作簿中的每个工作表都被视为一个 SAS 数据集。

![](img/1698e3a97543d6895ff5297aae8fd042_212_0.png)

工作表名称末尾会带有一个美元符号 `$`。

# `CONTENTS` 过程

```sas
proc contents data=orionxls._all;
run;
```
