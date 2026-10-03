
> 所有不等于 `US` 的观测值都执行第二个 `DO` 组中的语句。

## 练习

### 等级 1

#### 4. 条件创建变量

- a. 获取初始程序 `p10904`。
- b. 在 `DATA` 步骤中，创建三个新变量：`Discount`、`DiscountType` 和 `Region`。如果 `Country` 等于 `CA` 或 `US`，
  - `Discount` 等于 `0.10`
  - `DiscountType` 等于 `Required`
  - `Region` 等于 `North America`。如果 `Country` 等于其他值，
  - `Discount` 等于 `0.05`
  - `DiscountType` 等于 `Optional`
- c. 只包含以下变量：`Supplier_Name`、`Country`、`Discount`、`DiscountType`。
- d. 提交程序创建 `PROC PRINT`：

部分 `PROC PRINT` 输出（前 10 个观测值）

| 观测值 | Supplier_Name | Country | Region | Discount | Type |
|---|---|---|---|---|---|
| 1 | Scandinavian Clothing/S | NO | North America | 0.05 | Optional |
| 2 | Peterson | SE | North America | 0.05 | Optional |
| 3 | Prime Sports Ltd | GB | North America | 0.05 | Optional |
| 4 | Top Sports | DK | North America | 0.05 | Optional |
| 5 | Seasons Clothing | US | North America | 0.10 | Required |
| 6 | Sportico | ES | North America | 0.05 | Optional |
| 7 | British Sports | GB | North America | 0.05 | Optional |
| 8 | Eclipse Inc | US | North America | 0.10 | Required |
| 9 | Magnifico Sports | PT | North America | 0.05 | Optional |
| 10 | Sportswear Inc | US | North America | 0.10 | Required |

### 等级 2

#### 5. 无条件和条件创建变量

- a. 编写 `DATA` 步骤读取 `orion.orders` 创建 `Work.ordertype`。
- b. 创建新变量 `DayOfWeek`，其等于 `Order_Date`。
- c. 创建新变量 `Type`，其等于：
  - `Order_Type` 等于 1：`Catalog Sale`
  - `Order_Type` 等于 2：`Internet Sale`
  - `Order_Type` 等于 3：`Retail Sale`
- d. 创建新变量 `SalesAds`，其等于：
  - `Mail`（对应 1）
  - `Email`（对应 2）
- e. 不要包含 `Order_Type`、`Employee_ID` 和 `Customer_ID`。
- f. 编写 `PROC PRINT` 创建：

部分 `PROC PRINT` 输出（前 20 个观测值）

| 观测值 | Order_ID | Date | Type | Ads | Day Of Week |
|---|---|---|---|---|---|
| 1 | 12300523 | 11JAN2003 | 11JAN2003 | Catalog Sale | Mail | 7 |
| 2 | 123008101 | 15JAN2003 | 19JAN2003 | Internet Sale | Email | 4 |
| 3 | 123016683 | 20JAN2003 | 22JAN2003 | Internet Sale | Email | 2 |
| 4 | 123014741 | 28JAN2003 | 28JAN2003 | Catalog Sale | Mail | 3 |
| 5 | 123031565 | 27FEB2003 | 27FEB2003 | Catalog Sale | Mail | 5 |
| 6 | 123033319 | 02MAR2003 | 06MAR2003 | Internet Sale | Email | 1 |
| 7 | 123033566 | 03MAR2003 | 08MAR2003 | Internet Sale | Email | 2 |
| 8 | 123037114 | 09MAR2003 | 11MAR2003 | Internet Sale | Email | 1 |
| 9 | 123040478 | 15MAR2003 | 15MAR2003 | Catalog Sale | Mail | 7 |
| 10 | 123040481 | 22MAR2003 | 22MAR2003 | Catalog Sale | Mail | 7 |
| 11 | 123045031 | 26MAR2003 | 26MAR2003 | Internet Sale | Email | 2 |
| 12 | 123053723 | 24MAR2003 | 25MAR2003 | Internet Sale | Email | 2 |
| 13 | 123055630 | 25MAR2003 | 25MAR2003 | Catalog Sale | Mail | 3 |
| 14 | 123047806 | 28MAR2003 | 30MAR2003 | Internet Sale | Email | 6 |
| 15 | 123048538 | 01APR2003 | 01APR2003 | Catalog Sale | Mail | 3 |
| 16 | 123051355 | 02APR2003 | 03APR2003 | Retail Sale | Email | 4 |
| 17 | 123051369 | 02APR2003 | 03APR2003 | Internet Sale | Email | 4 |
| 18 | 123051373 | 12APR2003 | 18APR2003 | Internet Sale | Email | 6 |
| 19 | 123051375 | 28APR2003 | 20APR2003 | Retail Sale |  | 6 |
| 20 | 123051384 | 18APR2003 | 18APR2003 | Catalog Sale | Mail | |

### 等级 3

#### 6. 使用 `WHEN` 语句在 `SELECT` 组中创建变量

关于 `SELECT` 组的文档可以在 `SAS Help -> Products -> Base SAS 9.4 -> Language Reference -> Language Elements -> Statement` 中找到。

- a. 编写 `DATA` 步骤读取 `orion.nonsales` 创建 `Work.gifts`。
- b. 创建新变量 `DayOfWeek`，其等于 `Order_Date`。
- c. 创建新变量 `Type`，其等于：
  - `Order_Type` 等于 1：`Catalog Sale`
  - `Order_Type` 等于 2：`Internet Sale`
  - `Order_Type` 等于 3：`Retail Sale`
- d. 创建新变量 `SalesAds`，其等于：
  - `Mail`（对应 1）
  - `Email`（对应 2）
- e. 不要包含 `Order_Type`、`Employee_ID` 和 `Customer_ID`。
- f. 编写 `PROC PRINT` 创建：

部分 `PROC PRINT` 输出（前 235 个观测值）

| 观测值 | Order_ID | First | Last | Gift1 | Gift2 |
|---|---|---|---|---|---|
| 1 | 12300523 | Patrick | | Perfume | |
| 2 | 123008101 | Karen | | | Cookware |
| 3 | 123016683 | Liz | Povey | Perfume | |
| 4 | 123014741 | John | Hornsey | Cologne | |
| 5 | 123031565 | Sherie | Sheedy | Perfume | |
| 6 | 123033319 | Gladys | Gromek | Perfume | |
| 7 | 123033566 | Gabriele | Baker | | Cookware |
| 8 | 123037114 | Dennis | Entwistle | Cologne | |
| 9 | 123040478 | Useldo | | Cologne | |
| 10 | 123040481 | Ellis | Glattback | Perfume | |
| 11 | 123045031 | Riu | Horsey | Perfume | |
| 12 | 123053723 | Jeanette | Buddery | Coffee | |
| 13 | 123055630 | Hugh | Nicholas | Cologne | |
| 14 | 123047806 | Austen | Ralston | Cologne | |
| 15 | 123048538 | Bill | Mccleary | Cologne | |
| 16 | 123051355 | | | | | |
| 17 | 123051369 | | | | | |
| 18 | 123051373 | | | | | |
| 19 | 123051375 | | | | | |
| 20 | 123051384 | | | | | |

## `WHERE` 语句（复习）

`WHERE` 语句对符合特定条件的观测值进行子集处理。`WHERE` 语句的一般形式：

```
WHERE where-expression;
```

`where-expression` 是由操作数和运算符组成的序列，形成了一组指令，用于定义选择观测值的条件。

- 操作数包括常数和变量。
- 运算符是请求比较、算术计算或逻辑操作的符号。

## 处理 `WHERE` 语句

`WHERE` 语句在观测值进入程序数据向量（program data vector）之前进行选择。

![](img/1698e3a97543d6895ff5297aae8fd042_426_0.png)

### 9.07 测验

为什么 `WHERE` 语句在这个 `DATA` 步中不起作用？

```
data work.december;

set orion.sales;

BonusMonth=month(Hire_Date);

Bonus=500;

Compensation=sum(Salary,Bonus);

where Country='AU' and BonusMonth=12;

run;
```

> 在 `where` 语句中不能使用计算机变量！（`where` 语句筛选执行得太早了）

## 子集 `IF` 语句

子集 `IF` 语句继续处理那些符合条件的观测值。子集 `IF` 语句的一般形式：

```
IF expression;
```

`expression` 是操作数和运算符组成的序列，形成了一组指令，用于定义选择观测值的条件。

- 操作数包括常数和变量。
- 运算符是请求比较、算术计算或逻辑操作的符号。

## 子集 `IF` 语句

示例：

```
if Salary > 50000;
```

```
if Last Name='Smith' and First Name='Joe';
```

```
if Country not in ('GB', 'FR', 'NL');
```

```
if Hire Date = '15APR2008';
```

```
if BirthMonth = 5 or BirthMonth = 6;
```

```
if upcase(Gender)='M';
```

```
if 40000 <= Compensation <= 80000;
```

```
if sum(Salary,Bonus) < 43000;
```

特殊的 `WHERE` 运算符如 `BETWEEN AND`、`IS NULL`、`IS MISSING`、`CONTAINS` 和 `LIKE` 无法与子集 `IF` 语句。

## 处理子集 `IF` 语句

子集 `IF` 语句决定观测值是否继续在程序数据向量中被处理。

![](img/1698e3a97543d6895ff5297aae8fd042_428_0.png)

## 处理子集 `IF` 语句

![](img/1698e3a97543d6895ff5297aae8fd042_429_0.png)

### 业务场景

仅包含在 12 月有奖金月份澳大利亚员工。

```
data work.december;

set orion.sales;

where Country='AU';

BonusMonth=month(Hire_Date);

if BonusMonth=12

Bonus=500;

Compensation=sum(Salary,Bonus);

run;
```

## 部分 `SAS` 日志

> NOTE: 从数据集 `ORION.SALES` 中读取了 83 个观测值。
> `WHERE Country='AU';`
> NOTE: 数据集 `WORK.DECEMBER` 包含 3 个观测值和 12 个变量。

### 9.08 测验

你可以只写一个 `IF` 语句吗？
* 是
* 否

```
data work.december;

set orion.sales;

where Country='AU';

BonusMonth=month(Hire_Date);

if BonusMonth=12

Bonus=500;

Compensation=sum(Salary,Bonus);

data work.december;

set orion.sales;

BonusMonth=month(Hire_Date);

if BonusMonth=12

Bonus=500;

Compensation=sum(Salary,Bonus);
```

## `WHERE` 语句对比 / `IF` 语句

| 步骤和用法 | WHERE | IF |
|---|---|---|
| `PROC` 步 | 是 | 否 |
| `DATA` 步（源变量） | | 否 |
| `INPUT` 语句 | 否 | 是 |
| 赋值语句 | 否 | 是 |
| `SET` 语句（单个数据集） | 是 | 是 |
| `SET/MERGE` 语句（多个数据集） | | |
| 所有数据集中的变量 | 是 | | |
| 所有数据集中的变量 | 否 | 是 |

## `IF-THEN DELETE` 语句（自学）

子集 `IF` 语句的替代方案是 `IF-THEN DELETE` 语句。`IF-THEN DELETE` 语句的一般形式：

```
IF expression THEN DELETE;
```

`DELETE` 语句停止处理当前观测值。当 `DELETE` 执行时，当前观测值不会写入数据集，`SAS` 会立即返回 `DATA` 步的开头。

## `IF-THEN DELETE` 语句（自学）

```
data work.december;

set orion.sales;

where Country='AU';

BonusMonth=month(Hire_Date);

if BonusMonth ne 12 then delete;

Bonus=500;

Compensation=sum(Salary,Bonus);

run;

data work.december;

set orion.sales;

where Country='AU';

BonusMonth=month(Hire_Date);

if BonusMonth=12;

Bonus=500;

Compensation=sum(Salary,Bonus);

run;
```
