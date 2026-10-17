
| 12046 | Clark | Thomas | M | M | 27145 电工 | AU | 05/05/1974 | |
| 12047 | Lewis | Jessica | F | F | 24031 机械工 | AU | 01/01/1979 | |
| 12048 | Walker | Andrew | M | M | 20118 烘焙师 | AU | 08/06/1986 | |
| 12049 | Hall | Laura | F | F | 31998 技工 | AU | 21/09/1982 | |

8-44 第8章 验证与清洗数据

## 使用 Viewtable 窗口清洗数据 – Windows 系统（自学）

1. 选择 SAS 窗口栏上的 `Explorer` 选项卡以激活 `SAS Explorer` 窗口，或选择 `View Contents Only`（仅查看内容）。

![](img/1698e3a97543d6895ff5297aae8fd042_347_0.png)

2. 双击 `Libraries` 显示所有可用库。

![](img/1698e3a97543d6895ff5297aae8fd042_347_1.png)

3. 双击 `Orion` 库以显示该库的所有成员。

![](img/1698e3a97543d6895ff5297aae8fd042_348_0.png)

4. 双击 `Nonsales` 数据在视图窗口中设置数据。

![](img/1698e3a97543d6895ff5297aae8fd042_348_1.png)

5. 从 `Edit` 菜单中选择 `Edit Mode`（编辑模式）。

![](img/1698e3a97543d6895ff5297aae8fd042_349_0.png)

6. 找到以下观测值并进行所需的更改：

| 观测值 | 变量 | 正确值 |
|---|---|---|
| 7 | `Employee_ID` | 120109 |
| 12 | `Gender` | F |
| 14 | `Employee_ID` | 120116 |
| 101 | `Gender` | F |

7. 选择 `X` 关闭 `Viewable` 窗口。更改将保存到数据集中。

## 使用 Viewtable 窗口清洗数据 – UNIX 系统（自学）

1. 选择 `View Contents Only` 激活 `SAS Explorer`。

![](img/1698e3a97543d6895ff5297aae8fd042_350_0.png)

2. 双击 `Libraries` 显示所有可用库。

![](img/1698e3a97543d6895ff5297aae8fd042_350_1.png)

3. 双击 `Orion` 库显示该库的所有成员。

![](img/1698e3a97543d6895ff5297aae8fd042_350_2.png)

4. 双击 `Nonsales` 数据在 `Viewtable` 窗口中打开数据集。

![](img/1698e3a97543d6895ff5297aae8fd042_351_0.png)

5. 从 `Edit` 菜单选择 `Edit Mode`。

6. 找到以下观测值并进行所需的更改：

![](img/1698e3a97543d6895ff5297aae8fd042_351_1.png)

7. 选择 `X` 关闭窗口。更改将保存到数据。

## 使用 FEDIT 窗口清洗数据 - z/OS 系统

1. 在命令行输入 `fsedit orion.nonsales` 并回车激活 `FEDIT` 窗口。

```
Program Editor
Command ==> fsedit orion.nonsales
0001
0002
0003
0004
0005
0007
0008
0009
```

![](img/1698e3a97543d6895ff5297aae8fd042_352_0.png)

2. 找到以下观测值并进行所需的更改：

| 观测值 | 变量 | 正确值 |
|---|---|---|
| 7 | `Employee_ID` | 120109 |
| 12 | `Gender` | F |
| 14 | `Employee_ID` | 120116 |
| 101 | `Gender` | F |

在命令行输入观测值编号并回车进入该观测值。

3. 在命令行输入 `end` 并回车关闭 `FEDIT` 窗口。更改将保存到数据集。

## 8.06 测验（自学）

- 打开 `orion.nonsales` 的 `Viewtable` 窗口。
- 使用 `Viewtable` 窗口交互式地清洗以下观测值：

| 变量 | 观测值 | 无效值 |
|---|---|---|
| `Job_Title` | 10 | Security Guard |

## 程序化清洗数据

`DATA` 步用于程序化清洗无效数据。

使用 `DATA` 步清洗以下观测值：

| 变量 | 观测值 | 无效值 | 正确值 |
|---|---|---|---|
| `Country` | 84, 87, 197, and 200 | au | US |
| | 4 | | 26960 |
| `Salary` | 13 | | 26500 |
| | 20 | | 2401 |
| | 5 | | 21/01/1995 |
| `Hire_Date` | 9 | | 01/11/1978 |
| | 214 | 01/01/1968 | 01/01/1998 |

## 赋值语句

赋值语句评估表达式并将结果赋值给变量。

赋值语句的通用形式为：

```
variable = expression;
```

- `variable` 是现有变量或新变量。
- `expression` 是产生值的操作数和运算符序列。
- 赋值语句评估等号右边的表达式并将存储在等号左侧指定的变量中。

## 赋值表达式

操作数为：

- 字符常量
- 数字常量
- 日期常量
- 字符变量
- 数字变量

运算符包括：

- 代表算术计算的符号
- SAS 函数

## 赋值表达式

示例：

```
Salary = 26960; <- 数字常量
Gender = 'F'; <- 字符常量
Hire Date = '21JAN1995'; <- 日期常量
Country = upcase(Country); <- 函数
```

## SAS 函数

SAS 函数是一个根据参数返回值的程序。

`UPCASE` 函数将参数中的所有字母转换为大写。

`UPCASE` 函数的通用形式为：

```
UPCASE(argument)
```

`argument` 指定任何字符表达式。

## 赋值语句

`orion.nonsales` 数据集中所有的 `Country` 值都需要转换为大写。

```
data work.clean;
set orion.nonsales;
Country=upcase(Country);
run;
```

| 员工ID | 职位 | 国家 |
|---|---|---|
| 120101 | Director | AU |

## 赋值语句

`orion.nonsales` 数据集中所有的 `Country` 值都需要转换为大写。

```
data work.clean;
set orion.nonsales;
Country=upcase(Country);
run;
```

| 员工ID | 职位 | 国家 |
|---|---|---|
| 120101 | Director | AU |

![](img/1698e3a97543d6895ff5297aae8fd042_356_0.png)

## 赋值语句

`orion.nonsales` 数据集中所有的 `Country` 值都需要转换为大写。

```
data work.clean;
set orion.nonsales;
Country=upcase(Country);
run;
```

| 员工ID | 职位 | 国家 |
|---|---|---|
| 120104 | Administration Manager | au |

## 赋值语句

`orion.nonsales` 数据集中所有的 `Country` 值都需要转换为大写。

```
data work.clean;
set orion.nonsales;
Country=upcase(Country);
run;
```

| 员工ID | 职位 | 国家 |
|---|---|---|
| 120104 | Administration Manager | AU |

## 8.5 清洗无效数据

## 赋值语句

```
proc print data=work.clean;
var Employee_ID Job_Title Country;
run;
```

部分 `PROC PRINT` 输出

| 观测值 | ID | 标题 | 国家 |
|---|---|---|---|
| 84 | 120695 | Warehouse Assistant II | AU |
| 85 | 120696 | Warehouse Assistant I | AU |
| 86 | 120697 | Warehouse Assistant IV | AU |
| 87 | 120698 | Warehouse Assistant I | AU |
| 88 | 120710 | Business Analyst II | US |
| 89 | 120711 | Business Analyst III | US |
| 90 | 120712 | Marketing Manager | US |
| 91 | 120713 | Marketing Assistant III | US |

## 8.07 测验

哪个变量可以专门识别薪资无效的观测值？

| 观测 | 员工 ID | 性别 | 薪资 | 职位 | 出生日期 | 入职日期 |
|---|---|---|---|---|---|---|
| 2 | 120104 | M | 46230 | 行政经理 | bu | 11/05/1954 | 01/01/1981 |
| 4 | 120106 | F | 30475 | 办公室助理 II | au | 23/12/1944 | 01/01/1974 |
| 6 | 120107 | M | 27420 | 助理 III | AI | 01/02/1930 | 21/01/1953 |
| 10 | 120111 | M | 26889 | 安保员 II | bu | 23/07/1949 | |
| 12 | 120112 | F | 31285 | 安全经理 | au | 17/02/1968 | 01/07/1990 |
| 13 | 120115 | M | 28520 | 员助理 I | au | 08/25/1964 | 01/01/1974 |
| 15 | 120116 | F | 27018 | 办公室行政人员 | au | 13/08/1958 | 01/02/1965 |
| 20 | 120191 | F | 24101 | 培训师 | us | 17/01/1959 | 01/02/2003 |
| 84 | 120695 | | 28180 | 仓库助理 | bu | 13/07/1964 | 01/07/1998 |
| 91 | 120696 | M | 32100 | 销售助理 II | au | 07/25/1954 | 01/08/1979 |
| 101 | 120723 | F | 30960 | 通信专员 I | US | 10/08/1949 | 01/01/1974 |
| 125 | 120725 | M | 21480 | 产品文员 III | au | 20/06/1974 | 01/01/1995 |
| 197 | 120994 | F | 31640 | 办公室行政人员 I | us | 16/06/1974 | 01/11/1994 |
| 200 | 120987 | F | 27420 | 货运管理员 | us | 21/11/1974 | 01/09/1986 |
| 214 | 121011 | M | 25730 | 员助理 I | US | 11/03/1944 | 01/01/1968 |

## 程序化数据数据

可以使用 `DATA` 步骤程序化地清理无效数据。

使用 `DATA` 步骤清理以下观测值：

| 变量 | 观测 | 无效值 | 正确值 |
|---|---|---|---|
| 国家 | 2, 84, 87, 125, 197 和 200 | au or us | AU or US |
| | 4 | | 26960 |
| 薪资 | 13 | 2650 | 26500 |
| | 20 | 2401 | 24015 |
| | 5 | 21/01/1953 | 21/01/1995 |
| 入职日期 | 9 | | 01/01/1978 |
| | 214 | 01/01/1968 | 01/01/1968 |

## IF-THEN 语句

`IF-THEN` 语句对满足特定条件的观测值执行 SAS 语句。

`IF-THEN` 语句的一般形式：

```
IF expression THEN statement;
```

- `expression` 是操作数和运算符的序列，形成一组定义选择观测值条件的指令集。
- `statement` 是任何可执行的语句，例如赋值语句。

如果满足 `IF` 子句中的条件，则 `IF-THEN` 语句会对该观测值执行 SAS 语句。

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
run;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120105 | 27110 | 秘书 |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120105 | 27110 | 秘书 |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120105 | 27110 | 秘书 |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120105 | 27110 | 秘书 |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120105 | | 秘书 |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
run;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120106 | 26960 | 办公室助理 II |

## IF-THEN 语句

所有 `Salary` 的值都必须在 24000 - 50000 的范围内。

```sas
TRUE
data work.clean;
set orion.nonsales;
if Employee_ID=120106 then Salary=26960;
if Employee_ID=120115 then Salary=26500;
if Employee_ID=120191 then Salary=24015;
run;
```

| 员工 ID | 薪资 | 职位 |
|---|---|---|
| 120106 | 26960 | 办公室助理 II |

## IF-THEN 语句
