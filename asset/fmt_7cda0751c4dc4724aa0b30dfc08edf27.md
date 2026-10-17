
```
data customers;
  set orion.customer;
  Country_Name=put(Country, $country);
run;

proc freq data=orion.employee_addresses;
  tables Country;
  format Country $extra;
run;
```

> SAS 找不到格式

## 10.1 创建永久格式

### NOFMTERR 系统选项

默认情况下，`FMTERR` 系统选项生效。如果你使用了 SAS 无法加载的格式，SAS 会发出错误信息并停止处理。为了防止默认操作，将系统选项 `FMTERR` 更改为 `NOFMTERR`。

```
OPTIONS FMTERR | NOFMTERR;
```

### 10.03 调查

将当前的 `OPTIONS` 语句替换为以下语句并重新提交 `p21a01`。结果是什么？

```
options nofmterr;
```

![](img/d3bde6e6ab06b1fc622215d982111742_416_0.png)

### 使用 FMTSEARCH= 系统选项

要使用永久格式或搜索多个目录，使用 `FMTSEARCH=` 系统选项来识别要搜索格式的目录。

```
options fmtsearch=(orion orion.MyFmts);
OPTIONS FMTSEARCH=(item-1 item-2...item-n);
```

### 使用 FMTSEARCH= 系统选项

```
options fmtsearch=(orion orion.MyFmts);
```

- 1 SAS 提供的格式
- 2 `work.formats`
- 3 `library.formats`
- 4 `orion.formats`
- 5 `orion.MyFmts`

由于 `orion` 是一个没有目录名的 `libref`，因此假设 `formats` 是目录名称。

SAS 提供的格式总是第一个搜索。`work.formats` 目录总是会被搜索，除非它出现在 `FMTSEARCH` 列表中。如果分配了库 `libref`，则 `library.formats` 目录会在 `FMTSEARCH` 列表中任何其他项之前被搜索。要分配 `libref`，请使用下面的代码：

```
classname library 'SAS-data-library-containing-format-catalog';
```

## 10.04 简答题调查

将当前的 `OPTIONS` 语句替换为以下语句并重新提交 `p210a01`。结果是什么？

```
options fmterr fmtsearch=(orion orion.MyFmts);
```

![](img/d3bde6e6ab06b1fc622215d982111742_418_0.png)

## 维护格式

要维护格式，请执行以下任务之一：

- 编辑创建原始格式的 `PROC FORMAT` 代码。
- 从格式创建一个 SAS 数据集，编辑该数据集，并使用 `CNTLIN=` 重新创建格式。

## 维护永久性格式

![](img/d3bde6e6ab06b1fc622215d982111742_419_0.png)

## 维护永久性格式

`p210d02`

本演示说明了如何从 SAS 数据集中维护永久格式。

- 1. 提交步骤 1，从永久格式创建 SAS 数据集。
- 2. 提交步骤 2，将新的国家代码合并到 `countryfmt` 中。
- 3. 提交步骤 3，用旧和新格式化值替换 Sentry。

```
/* 步骤 1 */
proc format library=orion.myfmts cntlout=countryfmt;
select $country;
run;

proc print data=countryfmt;
run;

proc print data=orion.NewCodes;
run;

/* 步骤 2 */
data countryfmt;
  set countryfmt orion.NewCodes;
run;

/* 步骤 3 */
```

```
proc format library=work.myfmts cntlin=countryfmt fmtlib;
  select $country;
run;
```

### 练习题

如果你自上一次练习以来重新启动了 SAS 会话，请打开并提交数据文件夹中的 `libname.sas` 程序。

## 第 1 级

### 使用 SAS 数据集值创建格式

数据集 `orion.continent` 包含 `Continent_ID` 和 `Continent_Name` 变量。

| 观测值 | Continent_ID | Continent_Name |
|---|---|---|
| 1 | 91 | 北洲 |
| 2 | 93 | 欧洲 |
| 3 | 94 | 非洲 |
| 4 | 95 | 亚洲 |
| 5 | 96 | 澳洲/太平洋 |

- a. 创建一个名为 `continent` 的 `CNTLIN` 数据集，从 `orion.continent` 读取数据并包含 `FmtName`、`Start` 和 `Label` 变量。格式名称应为 `CONTINENT`。
- b. 使用 `CNTLIN=` 从 `continent` 数据集创建格式，并将格式存储在 `orion.MyFfmts` 目录中。
- c. 打开并提交程序 `p210e01`。程序应成功执行，SAS 日志中无错误。

```
**************************
/* Part C */
/* 使用 continent. */
**************************

data countries;
  set orion.continent;
  Continent_Name=put(Continent_ID, continent);
run;

proc print data=countries(obs=10);
  title 'Continent Names';
run;
```

- d. 打开程序 `p210e01d`。

```
p210e01d
****************************************************************/
/* 当使用 CNTLOUT 选项创建 START 和 END 时 */
/*它们被创建为字符型*/
****************************************************************/
data continentfmt;
set continentfmt orion.NewContinent;
run;
```

- 1) 在 `DATA` 步骤之前，添加一个带有 `CNTLOUT` 选项的 `PROC FORMAT` 步骤，从 `CONTINENT` 格式创建一个名为 `continentfmt` 的控制输出数据集。
- 2) 提交程序向 `continentfmt` 数据集添加新的观测值。
- 3) 添加另一个带有 `CNTLIN=` 选项的 `PROC FORMAT` 步骤，读取 `continentfmt` 数据集并重新创建 `CONTINENT` 格式。在 `PROC FORMAT` 步骤中使用 `FMTLIB` 选项以确保新值已添加到 `CONTINENT` 格式中。

## 第 2 级

- 2. 使用 SAS 数据集创建包含包含范围的格式

数据集 `orion.ages` 包含三个变量：`First_Age`、`Last_Age` 和 `Description`。

| 观测值 | First_Age | Last_Age | Description |
|---|---|---|---|
| 1 | 15 | 30 | 15-30岁 |
| 2 | 30 | 45 | 31-45岁 |
| 3 | 45 | 60 | 46-60岁 |
| 4 | 60 | 75 | 61-75岁 |

部分内容 `orion.ages`

- a. 从 `orion.ages` 数据集创建格式并将其永久存储在 `orion.MyFmts` 目录中。使用相应的选项查看格式中的值。
- b. 编写一个 `DATA` 步骤来创建 `sales` 数据集，从 `orion.ages` 数据集中读取 `Employee_ID` 和 `Birth_Date` 变量。创建一个新变量 `Age`，即员工在当前的年龄，另一个名为 `Age_Cat` 的变量是使用 `AGE` 格式的 `Age` 变量值。使用以 `AGE` 为基础的 `YRDIF` 函数计算带小数的员工精确年龄。
- c. 打印 `sales` 数据集的前五个观测值，以确认新变量已正确创建。

```
PROC PRINT Output (as of July 18, 2012)
Sales Set
| Obs | Employee_ID | Birth_Date | Age | Age_Cat |
|---|---|---|---|---|
| 1 | 102102 | 11AUG1973 | 38 | 31-45 years |
| 2 | 102103 | 22JAN1953 | 59 | 46-60 years |
| 3 | 102121 | 02AUG1948 | 63 | 61-75 years |
| 4 | 102122 | 27JUL1958 | 53 | 45-59 years |
| 5 | 102123 | 28SEP1968 | 43 | 30-44 years |
```

### 挑战

- 3. 使用 SAS 数据集创建包含排除范围的格式

`orion.ages_mod` 包含三个变量：`First_Age`、`Last_Age` 和 `Description`。

部分内容 `orion.ages_mod`

| Obs | First_Age | Last_Age | Description |
|---|---|---|---|
| 1 | 15 | 30 | 15-29 years |
| 2 | 30 | 45 | 30-44 years |
| 3 | 45 | 60 | 45-59 years |
| 4 | 60 | 75 | 60-75 years |

- a. 从 `orion.ages_mod` 数据集创建格式并永久存储在 `orion.MyFmts` 目录中。使用相应的选项查看格式的值。`Description` 变量需要包含在格式中。
- b. 编写一个 `DATA` 步骤，从 `orion.ages` 数据集中读取 `Employee_ID` 和 `Birth_Date` 变量。创建一个新变量 `Age`，即员工在当前的年龄，另一个名为 `Age_Cat` 的变量是使用 `AGE` 格式的 `Age` 变量值。使用以 `AGE` 为基础的 `YRDIF` 函数计算带小数的员工精确年龄。
- c. 打印 `sales` 数据集的前五个观测值，以确认新变量已正确创建。使用 `AGE` 格式来获得正确的结果。

## 10.2 答案 10-23

3) 添加另一个带有 `CNTLIN=` 的 `PROC FORMAT` 步骤，读取 `continentfmt` 数据集并重新创建 `CONTINENT` 格式。在此 `PROC FORMAT` 步骤中使用 `FMTLIB` 以确保新值添加到 `CONTINENT` 格式中。

```
proc format library=orion.MyFmts cntlin=continentfmt
  fmtlib;
  select continent;
```

## 2. 从 SAS 数据集创建包含范围的格式

a. 从 `orion.ages` 数据集创建一个格式并将其永久存储在 `orion.MyFmts` 目录。使用相应的选项查看格式中的值。

```
data ages
  set orion.ages (rename=(First_Age=Start Last_Age=End
                               Description=Label));
  retain FmtName 'ages';

proc format library=orion.MyFmts fmtlib cntlin=ages;
  select ages;
```

b. 编写一个 `DATA` 步骤创建一个 `sales` 数据集，从 `orion.sales` 数据集中读取 `Employee_ID` 和 `Birth_Date` 变量。创建一个名为 `Age` 的新变量，表示员工截至当前日年龄，以及另一个名为 `Age_Cat` 的新变量，使用 `AGE` 格式获取变量 `Age` 的值。

```
data sales
  set orion.sales (keep=Employee_ID Birth_Date);
  Age_int=yrdiff(Birth_Date, today(), 'AGE');
  Age_Cat=put(Age, ages).
```

c. 输出 `sales` 数据集的前五个观测值，以确认新变量已正确创建。

```
proc print data=sales(obs=5);
  format Birth_Date date9.
  title 'Sales Data Set';
```

## 3. 从 SAS 数据集创建包含排除范围的格式

a. 从 `orion.ages_mod` 数据集创建一个命名格式 `ages_mod` 并将其永久存储在 `orion.MyFmts` 目录中。使用相应的选项查看格式中的值。

```
data ages_mod;
set orion.ages_mod(rename=(First_Age=Start Last_Age=End
Description=Label));
retain fmtname 'ages_mod';
EEXCL='Y';
run;

proc format library=orion.MyFmts fmtlib cntlinn=ages_mod;
select ages_mod;
run;
```

b. 编写一个 `DATA` 步骤创建一个 `sales` 数据集，从 `orion.sales` 数据集中读取 `Employee_ID` 和 `Birth_Date` 变量。创建一个名为 `Age` 的新变量，表示员工截至当前日年龄，以及另一个名为 `Age_Cat` 的新变量，使用 `AGES_MOD` 格式获取变量 `Age` 的值。

```
options fmtsearch=(orion.MyFmts);
data sales:
  set orion.sales(keep=Employee_ID Birth_Date);
  Age=int(yrdif(Birth_Date, today(), 'AGE'));
  Age_Cat=put(Age, ages_mod.);
run;
```

c. 输出 `sales` 数据集的前五个观测值，以确认新变量已正确创建。

```
proc print data=sales(obs=5);
  format birth date date9;
title 'Sales Data Set'
run;
```

## 学生活动答案（调查/测验）

## 10.01 多选题调查 – 正确答案

哪个程序的效率更高？

+   a. 方案 1
b. 方案 2
c. 它们的效率应该相等。

+   - `RETAIN` 语句在编译时分配一个初始值。
- `RENAME=` 选项在编译时重命名新数据集中的变量。

## 使用 NOFMTERR 系统选项

默认情况下，`FMTERR` 系统选项生效。如果你使用了 SAS 无法加载的格式，SAS 会发出错误消息并停止处理该步骤。

要防止默认操作，将系统选项 `FMTERR` 改为 `NOFMTERR`。

```
OPTIONS FMTERR | NOFMTERR;
```

## 10.02 简答调查 – 正确答案

提交程序 `p210a01`。

在你在 SAS 日志中看到了哪些错误消息？

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

## 10.03 简答 – 正确答案

将当前语句替换为以下内容并重新提交 `p210a01`。结果是什么？

```
options fmtlib;
```

## 10.04 简答 – 正确答案

1004 简答 – 正确答案

将当前语句替换为以下内容并重新提交 `p210a01`。结果是什么？
