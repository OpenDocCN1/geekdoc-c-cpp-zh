
- c. where style in (RANCH, SPLIT, TWOSWRORY)
- d. where style in ('RANCH', 'SPLIT', 'TWOSWRORY')

- 4. 如果你想对数据进行排序并创建一个临时数据集 `Calc` 来存储排序后的数据，你应该提交以下哪个步骤？
  - a. 
    ```sas
    proc sort data=work.calc out=finance.dividend;
    run;
    ```
  - b. 
    ```sas
    proc sort dividend out=calc;
    by account;
    run;
    ```
  - c. 
    ```sas
    proc sort data=finance.dividend out=work.calc;
    by account;
    run;
    ```
  - d. 
    ```sas
    proc sort from finance.dividend to calc;
    by account;
    run;
    ```

在 `PROC PRINT` 步骤中可以使用以下哪条语句来创建此输出？

| 月份 | 教师 | 航空课程 | 走跑 | 游泳 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 37 | 91 | 83 |
| 2 | 2 | 41 | 102 | 27 |
| 3 | 1 | 52 | 98 | 19 |
| 4 | 1 | 61 | 118 | 22 |
| 5 | 3 | 49 | 88 | 29 |
| 6 | 2 | 24 | 101 | 54 |
| 7 | 1 | 45 | 91 | 69 |
| 8 | 2 | 63 | 65 | 53 |
| 9 | 1 | 78 | 49 | 68 |
| 10 | 1 | | 70 | 41 |
| 11 | 3 | 82 | 44 | 58 |
| 12 | 2 | 93 | 57 | 47 |
| | | 685 | 974 | 570 |

- a. 
  ```sas
  var month instructors;
  instructors aerclass walkjogrun swim;
  ```
- b. 
  ```sas
  var month;
  instructors aerclass walkjogrun swim;
  ```
- c. 
  ```sas
  var month instructors aerclass;
  instructors aerclass walkjogrun swim;
  ```
- d. 以上所有项

- 6. 如果提交以下程序，会发生什么？

```sas
proc sort data=cert.diabetes;
run;
proc print data=cert.diabetes;
var age weight pulse;
where sex='F';
run;
```

- a. `PROC PRINT` 步骤成功运行，按其排序顺序打印观测值。
- b. `PROC SORT` 步骤永久地排序了输入数据集。
- c. `PROC SORT` 步骤产生错误并停止处理，但 `PROC PRINT` 步骤成功运行，按其原始（未排序）顺序打印观测值。
- d. `PROC SORT` 步骤成功运行，但 `PROC PRINT` 步骤产生错误并停止处理。

- 7. 如果提交以下程序，它会创建什么输出？

```sas
proc sort data=cert.loans out=work.loans;
by month amount;
run;
```

```sas
proc print data=work.loans noobs;
var months amount payment;
sum amount payment;
where months<360;
run;
```

a.

| 月数 | 金额 | 付款额 |
| :--- | :--- | :--- |
| 12 | $3,500 | $308.52 |
| 24 | $8,700 | $403.47 |
| 36 | $10,000 | $325.02 |
| 48 | $5,500 | $128.02 |
| 60 | $18,500 | $393.07 |
| 60 | $22,000 | $467.43 |
| | $67,700 | $2,025.53 |

b.

| 月数 | 金额 | 付款额 |
| :--- | :--- | :--- |
| 12 | $3,500 | $308.52 |
| 24 | $8,700 | $403.47 |
| 36 | $10,000 | $325.02 |
| 48 | $5,500 | $128.02 |
| 60 | $18,500 | $393.07 |
| 60 | $22,000 | $467.43 |
| | $67,700 | |

c.

| 月数 | 金额 | 付款额 |
| :--- | :--- | :--- |
| 12 | $3,500 | $308.52 |
| 48 | $5,500 | $128.02 |
| 60 | $18,500 | $393.07 |
| 24 | $8,700 | $403.47 |
| 36 | $10,000 | $325.02 |
| 60 | $22,000 | $467.43 |
| | $67,700 | |

d.

| 月数 | 金额 | 付款额 |
| :--- | :--- | :--- |
| 12 | $3,500 | $308.52 |
| 24 | $8,700 | $403.47 |
| 36 | $10,000 | $325.02 |
| 48 | $5,500 | $128.02 |
| 60 | $18,500 | $393.07 |
| 60 | $22,000 | $467.43 |
| | $67,700 | |

- 8. 哪条语句同时满足了两个条件？
  - `amount` 小于 5000。
  - `account` 为 101-92 或 `rate` 等于 05。

  a. 
  ```sas
  where amount <= 5000 and
  account='101-92' or rate = 05;
  ```
  b. 
  ```sas
  where (amount <= 5000 and account='101-92'
  rate = 05);
  ```
  c. 
  ```sas
  where amount <= 5000 and
  (account='101-92' or rate = 05);
  ```
  d. 
  ```sas
  where amount <= 5000 or account='101-92'
  and rate = 05;
  ```

`PROC PRINT` 默认显示什么？

- a. `PROC PRINT` 不创建默认报告；必须指定要显示的行。
- b. `PROC PRINT` 显示数据集中的所有观测值和变量。如果你需要额外的观测值列，可以请求。
- c. `PROC PRINT` 按以下顺序显示列：观测值列、所有字符变量和数值变量。
- d. `PROC PRINT` 显示数据集中的所有观测值和变量，最左侧为观测值列，变量按它们在数据集中的顺序显示。

# 第 7 章

# 理解步骤处理

SAS 如何处理程序 ............................................ 109

编译阶段 ........................................ 112

程序数据向量 (PDV) ................................... 112

语法检查 ........................................ 112

数据集变量 ....................................... 112

数据集描述部分 ................................ 113

执行阶段 ........................................ 115

变量初始化 ................................................ 115

`SET` 语句 ............................................ 115

按顺序处理语句 ...................................... 115

`DATA` 步骤结束 ................................................. 116

`DATA` 步骤迭代 ........................................ 117

文件结束标记 ....................................... 119

执行阶段结束 ................................ 119

调试 `DATA` 步骤 ................................................ 120

编译阶段错误诊断 ...................... 120

执行阶段错误诊断 ........................ 121

数据错误调试 .............................................. 121

使用赋值语句清理无效数据 ............... 123

测试你的程序 ................................................ 125

限制观测值 ................................... 125

示例：在 SAS 日中查看执行 ......................... 125

章节测试 ................................................... 126

# SAS 如何处理程序

当你提交一个 `DATA` 步骤时，SAS 处理该 `DATA` 步骤并创建一个新的 SAS 数据集。`DATA` 步骤分两个阶段处理：

## 图 7.1 DATA 步骤

| 新 SAS 数据集 | |
| :--- | :--- |
| 编译阶段 | 描述部分 |
| 执行阶段 | 数据部分 |

当你提交执行 `DATA` 时，SAS 检查 SAS 语句的语法并进行编译。在此阶段，SAS 识别每个新变量的类型和长度，并确定后续对变量的每次引用是否需要类型转换。在编译阶段，SAS 创建以下内容：

- 程序数据向量 (PDV)
- 描述信息

编译阶段完成后，创建新数据集的描述部分。

默认情况下，简单的 `DATA` 步骤为每个创建的观测值迭代一次。简单 `DATA` 步骤执行阶段的操作流描述如下：

1. `DATA` 步骤从 `DATA` 语句开始。每次执行 `DATA` 语句时，`DATA` 步骤开始迭代，`_N_` 自动变量加 1。`_N_` 自动变量代表 `DATA` 步骤迭代的次数。
2. SAS 将新创建的程序变量在程序数据向量 (PDV) 中设为空。
3. SAS 从 SAS 数据集中直接读取观测值到 PDV。你可以使用 `MERGE`、`SET`、`MODIFY` 或 `UPDATE` 语句读取记录。
4. SAS 按顺序执行任何后续编程语句并更新 PDV。
5. 当 SAS 执行 `DATA` 步骤中的最后一个语句时，所有值（临时变量和标记为删除的变量除外）都作为单个观测值写入数据集。注意，用 `SET`、`MERGE`、`MODIFY` 或 `UPDATE` 语句读取的变量在此处不会重置为空。
6. SAS 计数另一个迭代，读取下一个观测值，并执行当前观测值的后续编程语句。
7. 当 SAS 在 SAS 数据集中遇到文件结束时，`DATA` 步骤终止。

图 7.2 显示了读取原始数据的 `DATA` 步骤处理的一般流程。

## 图 7.2 DATA Step 处理的编译与执行阶段

![](img/4d880eb3a583bf2815ab53a244818659_122_0.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_1.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_2.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_3.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_4.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_5.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_6.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_7.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_8.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_9.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_10.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_11.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_12.png)
![](img/4d880eb3a583bf2815ab53a244818659_122_13.png)

### 编译阶段

#### 程序数据向量 (PDV)

PDV 是内存中的一个逻辑区域，SAS 在此区域逐个构建数据集。当程序执行时，SAS 读取数据值或通过执行 SAS 语言语句创建数据值。这些数据值被分配给 PDV 中相应的变量。从这里开始，SAS 将这些值作为单个观测值写入 SAS 数据集。

除了数据集变量和计算变量外，PDV 还包含这些自动变量：

- `_N_` 变量，用于计算 `DATA` step 迭代的次数。
- `_ERROR_` 变量，用于指示数据执行过程中发生的错误。当没有错误时，`_ERROR_` 的值为 0。当发生错误时（无论一个错误还是多个错误），该值被设置为 1。其默认值为 0。

注意：SAS 不将这些变量写入输出数据集。

#### 语法检查

在编译阶段，SAS 会扫描 `DATA` step 中的每条语句，寻找语法错误。以下是示例：

#### 数据集变量

`SET` 语句被编译时，新数据集中的每个变量都会在 PDV 中添加一个槽位。通常，变量属性（如长度和类型）在第一次遇到该变量时确定。

```sas
data work.update;
set cert.invent;
Total=instock+backord;
SalePrice=(CostPerUnit*0.65)+CostPerUnit;
format CostPerUnit SalePrice dollar6.2;
run;
```

### 图 7.3 程序数据向量

| Item | IDnum | InStock | BackOrd | CostPerUnit | _N_ | _ERROR_ |
|---|---|---|---|---|---|---|

在 `DATA` step 中通过赋值语句创建的任何变量也会添加到 PDV 中。例如，赋值语句创建了两个变量：`Total` 和 `SalePrice`。随着语句的编译，变量被添加到 PDV 中。变量的属性由表达式定义。因为该表达式包含算术运算符并产生数值，所以 `Total` 和 `SalePrice` 被定义为数值型变量，并分配默认长度 8。

```sas
data work.update;
set cert.invent;
Total=instock+backorder;
SalePrice=(CostPerUnit*0.65)+CostPerUnit;
format CostPerUnit SalePrice dollar6.2;
run;
```

### 图 7.4 程序数据向量

| Item | IDnum | InStock | BackOrder | CostPerUnit | Total | SalePrice | _N_ | _ERROR_ |
|---|---|---|---|---|---|---|---|---|

## SAS 数据集的描述部分 (Descriptor Portion)

描述部分是 SAS 为每个 SAS 数据集创建并维护的信息，包括数据集属性及其成员属性。以下是示例：

- 数据集的名称及其成员类型
- 数据集的创建日期
- 变量的名称、数据类型（字符或数值）和长度

扩展属性描述信息由用户定义，包括属性名称、变量名称和属性值。描述信息还包含关于扩展属性的信息（如果在数据集中定义了的话）。你可以使用 `CONTENTS` 过程显示描述信息。

```sas
proc contents data=work.update;
run;
```

**图 7.5** CONTENTS 过程输出：数据集描述符

| Data Set Name | Observations | |
|---|---|---|
| WORK UPDATE: DATA | 9 | |
| Member Type | Variables | 7 |
| Engine | Indexes | 0 |
| Created | V9 | 07/25/2018 15:13:34 | Observation Length | 64 |
| Last Modified | 07/25/2018 15:13:34 | Deleted Observations | 0 |
| Protection | Compressed | NO |
| Data Set Type | Sorted | NO |
| Data Representation | latin1 (Windows) |
| Engine/Host Dependent Information | |
|---|---|
| Data Set Page Size | 65536 |
| Number of Data Set Pages | 1 |
| First Date | 1 |
| Max Obs per Page | 102 |
