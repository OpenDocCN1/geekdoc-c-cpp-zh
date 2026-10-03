
`UnitCostPrice` :dollar. `UnitSalesPrice` :dollar;

`run;`

对于 z/OS (OS/39)，使用以下 `INFILE` 语句：

```sas
infile '.workshop.rawdata (prices)' dlm='*' missover;
```

b. 编写一个 `PROC PRINT` 步并在 `DATA` 步中添加 `LABEL` 和 `FORMAT` 语句。

```sas
data work.prices;
infile 'prices.dat' dlm='*' missover;
input ProductID StartDate :date. EndDate :date.
UnitCostPrice :dollar. UnitSalesPrice :dollar;
label ProductID=Product ID
StartDate='Start of Date Range'
EndDate='End of Date Range'
UnitCostPrice='Cost Price per Unit'
UnitSalesPrice='Sales Price per Unit'
format StartDate EndDate mmddyy10.
UnitCostPrice UnitSalesPrice 8.2;
run;
```

```sas
proc print data=work.prices label;
run;
```

## 学生活动答案（投票/测验）

### 7.02 多选题投票 – 正确答案

> a. PDV 在编译时创建。
> b. PDV 持有变量名、类型和初始值。
> c. PDV 在运行时创建。

### 7.03 多选题投票 – 正确答案

> a. 数据被读入 PDV。
> b. PDV 内容输出到输出集。
> c. PDV 在 DATA 步期间创建。

### 7.04 测验 – 正确答案

> a. INPUT 语句正确使用了空格分隔的原始数据。
> b. INPUT 语句正确使用了空格分隔的原始数据。
> c. INPUT 语句正确使用了空格分隔的原始数据。

### 7.05 测验 – 正确答案

> a. DATA 步从原始文件读取数据。
> b. DATA 步从原始文件读取数据。
> c. DATA 步从原始文件读取数据。

### 7.06 测验 – 正确答案

> a. 在 INPUT 语句中使用 MISSOVER 选项。
> b. MISSOVER 选项被添加到 DATA 步中。
> c. MISSOVER 选项被添加到 INPUT 语句中。

### 7.07 测验 – 正确答案

> a. 检查 SAS 日志。
> b. 检查 SAS 日志。
> c. 检查 SAS 日志。

## 8.1 数据验证与清洗简介

+ 目标
- 定义原始数据文件中的数据错误。
- 识别验证数据的步骤。
- 识别清洗数据的技术。
- 定义用于数据验证和清洗的业务场景。

### 业务场景

需要读取一个包含分隔符的原始数据文件，该文件包含来自澳大利亚和美国的 Orion Star 非销售员工信息，以创建一个数据集。

+ 非销售员工数据要求：
- **Employee_ID**（员工ID）、**Salary**（薪水）、**Birth_Date**（出生日期）和 **Hire_Date**（入职日期）必须是数值变量。
- **First**（名）、**Last**（姓）、**Gender**（性别）、**Job_Title**（职位）和 **Country**（国家）必须是字符变量。

## 8.1 练习

SAS 在处理数值数据 Salary 和 Hire Date 时会遇到什么问题？

### Partial nonsales.csv

```
12101,Patrick,Lu,M,183940,Director,AU,08AUG1970,01JUL2003
12104,Karen,Billing,F,46230,Administration Manager,AU,01MAY1954,01JAN1981
12105,Liz,Powy,F,27110,Service Assistant,AU,02DEC1971,01MAY1998
12106,Harvey,Johnson,M,26000,Assistant,AU,02DEC1944,01JAN1974
12107,Sherie,Sheedy,F,30475,Office Assistant,AU,01FEB1978,21JAN1953
12108,Gladys,George,F,27760,Warehouse Assistant,AU,03FEB1964,01AUG2006
12109,Gabrielle,Sarker,P,26495,Warehouse Assistant,AU,21DEC1996,02DEC2005
12110,Doreen,Smith,F,21863,Office Assistant,AU,20NOV1949,01NOV1969
12111,Ubaldo,Selleane,M,28639,Security Guard,AU,23JUL1999,09NOV1998
12112,Itelis,Clabrock,F,25850,,AU,01SEP1990,01SEP1993
12113,Gearby,F,26049,Security Guard,AU,01NOV1984,01JAN1974
12114,Jeannette,Nicholls,M,31285,Security Manager,AU,08FEB1974,01JAN1974
12115,Hughie,Nicholls,M,26250,Service Assistant,AU,01MAY1984,01AUG2005
12116,Austin,Ralton,N,29210,Service Assistant,AU,01JUL1959,01FEB1988
12117,Bill,McClary,M,31670,Cabinet Maker,AU,11SEP1964,01APR1986
```
