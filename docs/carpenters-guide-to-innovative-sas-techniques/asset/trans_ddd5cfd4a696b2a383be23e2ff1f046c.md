
### 2.5.4 使用 CLASSDATA

```sas
proc sort data=advrpt.demog(keep=subject)
    out=subjects nodupkey;
by subject;
run;

data Visits;
    set subjects;
    do visit = 1 to 16; ❶
        output visits;
    end;
run;

proc means data=advrpt.lab_chemistry
        classdata=visits ❷
        noprint ways exclusive;
    class subject visit;
    var sodium potassium chloride;
    output out=allmeans ❸ sum=;
run;
```

数据集 WORK.VISITS 被构造为对 16 个潜在访视中的每一个都有一条观测 ❶。然后，该数据集与 CLASSDATA= 选项 ❷ 以及 PROC MEANS 步骤中的 EXCLUSIVE 选项一起使用。

尽管在 LAB_CHEMISTRY 数据集中没有受试者具有访视 3，且 SUBJECT 210 没有访视 9，但在由 PROC MEANS 创建的汇总数据集 (WORK.ALLMEANS) ❸ 中，每个受试者都将拥有全部十六次访视的汇总行。此处显示的受试者 210 现在同时具有访视 3 ❹ 和访视 9 ❺。

> **旁注：** CLASSDATA 数据集必须包含每个 CLASS 变量。

| 观测 | SUBJECT | VISIT | sodium | potassium | chloride |
|---:|---:|---:|---:|---:|---:|
| 161 | 210 | 1 | 14.0 | 5.0 | 103 |
| 162 | 210 | 2 | 14.2 | 4.0 | 103 |
| **163** | **210** | **3** | **.** | **.** | **.** ❹ |
| 164 | 210 | 4 | 14.1 | 3.9 | 101 |
| 165 | 210 | 5 | 14.4 | 4.7 | 105 |
| 166 | 210 | 6 | 14.5 | 4.7 | 104 |
| 167 | 210 | 7 | 14.3 | 4.7 | 103 |
| 168 | 210 | 8 | 14.1 | 4.4 | 102 |
| **169** | **210** | **9** | **.** | **.** | **.** ❺ |
| 170 | 210 | 10 | 14.2 | 4.3 | 106 |
| 171 | 210 | 11 | 14.2 | 4.1 | 104 |
| 172 | 210 | 12 | 13.9 | 4.0 | 103 |
| 173 | 210 | 13 | 14.2 | 4.4 | 104 |
| 174 | 210 | 14 | 14.1 | 4.1 | 99 |
| 175 | 210 | 15 | 13.8 | 3.8 | 99 |
| 176 | 210 | 16 | 14.3 | 5.0 | 104 |

### 更多信息

CLASSDATA 选项还在第 7.9 节（PROC MEANS 和 PROC SUMMARY）以及第 8.1.4 节（PROC TABULATE）中讨论。

### 2.5.5 使用预加载格式

对于 TABULATE、MEANS、SUMMARY 和 REPORT 过程，预加载格式可用于向输出表添加行。与第 2.5.4 节所示的 CLASSDATA 选项类似，此方法将稀疏行添加到表中，而不是数据集中。因此，我们既不需要修改原始数据，甚至也不需要制作副本。

```sas
proc format; ❶
value visits
1='1'
2='2'
3='3'
4='4'
5='5'
6='6'
7='7'
8='8'
9='9'
10='10';
run;

ods pdf file="&path\results\E2_5_5.pdf";
proc report data=advrpt.lab_chemistry nowd
    completerows; ❷
    column visit sodium potassium chloride;
    define visit / group
        f=visits. preloadfmt ❸
        "Visit" order=data;
    define sodium /analysis mean f=5.2;
    define potassium /analysis mean f=5.3;
    define chloride /analysis mean f=5.1;
run;
ods pdf close;
```

假设我们需要生成一份实验室访视的实验室化学值均值报告。无论这些访视是否出现在数据中，报告都必须包含前 10 次访视。

- ❶ 创建一个格式，其中包含前 10 次访视中的每一次。
- ❷ PROC REPORT 特有的 COMPLETEROWS 选项用于确保预加载格式中的每一行都会出现在报告中。
- ❸ 使用预加载格式时，PRELOADFMT 选项将始终存在。此处，通过将 PRELOADFMT 选项和要预加载的格式都放在 DEFINE 语句上，使二者相关联。生成的报告的一部分显示在右侧。

### 更多信息

预加载格式还可用于排除观测，并在第 12.1 节中更详细地介绍和讨论。

**2.5.5 使用预加载格式**
**使用 COMPLETEROWS 的 PROC REPORT**

| 访视 | sodium | potassium | chloride |
|---|---|---|---|
| 1 | 14.01 | 4.206 | 100.6 |
| 2 | 14.07 | 4.294 | 101.3 |
| 3 |  |  |  |
| 4 | 14.05 | 4.231 | 102.8 |
| 5 | 14.21 | 4.500 | 101.4 |
| 6 | 14.16 | 4.506 | 100.3 |
| 7 | 14.03 | 4.314 | 100.2 |

此列表将包含从 VISIT1 到 VISIT10（含端点）之间的所有变量。作为一般规则，所有变量是否已经存在于 PDV 上并不重要，并且它们在 PDV 上的顺序也不重要。然而，与任何变量列表一样，这种用法本身可能会产生意外后果。

在下面的 ARRAY 语句中，只有前 10 次访视会包含在数组中；但是，如果其中一个变量尚未存在于 PDV 上，则会添加它。

```sas
array vis [10] visit1 - visit10;
```

KEEP 语句不会建立变量，因此与前面的 ARRAY 语句不同，列表中尚未存在于 PDV 上的变量将导致错误。如果 PDV 上没有 VISIT3 变量，则下面的 KEEP 语句将产生警告。

```sas
keep visit1 - visit10;
```

此类列表可用于任何需要变量列表的地方。这包括 KEEP、DROP、VAR、RETAIN 等语句和选项。接受值列表的函数（例如 MIN、MAX、MEAN）需要使用 OF 运算符，以防止与减法混淆。

```sas
m = max(of visit1 - visit10);
```

### 依赖 PDV 顺序的列表（命名范围）

当 PDV 上变量的顺序已知时，可以使用双连字符来指定列表。与上面显示的公共前缀变量列表不同，PDV 上变量的顺序非常重要，并且这种形式的变量列表不能用于创建变量。以下 PROC CONTENTS 步骤显示 ADVRPT.DEMOG 中的变量及其在 PDV 上的相对位置（通过使用 VARNUM 选项——VARNUM 选项取代了现已过时的 POSITION 选项）。

```sas
title1 '2.6.1 Variable Shorthand Lists';
title2 'List of variables and their positions';
proc contents data=advrpt.demog varnum;
run;
```

生成的列表显示了变量名称、属性及其顺序。

### 2.6.1 变量简写列表

变量及其位置列表

*CONTENTS 过程*

**按创建顺序排列的变量**

| # | 变量 | 类型 | 长度 | 格式 | 标签 |
|---:|---|---|---:|---|---|
| 1 | SUBJECT | Num | 8 |  |  |
| 2 | CLINNUM | Char | 6 |  | 诊所编号 |
| 3 | LNAME | Char | 10 |  | 姓氏 |
| 4 | FNAME | Char | 6 |  | 名字 |
| 5 | SSN | Char | 9 |  | 社会安全号码 |
| 6 | SEX | Char | 1 |  | 患者性别 |
| 7 | DOB | Num | 8 | DATE7. | 出生日期 |
| 8 | DEATH | Num | 8 | DATE7. | 死亡日期 |
| 9 | RACE | Char | 1 |  | 种族 |
| 10 | EDU | Num | 8 |  | 受教育年限 |
| 11 | WT | Num | 8 |  | 体重（磅） |
| 12 | HT | Num | 8 |  | 身高（英寸） |
| 13 | SYMP | Char | 2 |  | 症状代码 |
| 14 | death2 | Num | 8 | DATE9. |  |

变量列表 `LNAME--SYMP` 包括数据集 `ADVPRT.DEMOG` 中的所有变量（数值型和字符型），但 `SUBJECT`、`CLINNUM` 和 `DEATH2` 除外。

包含列表修饰符 `NUMERIC` 和 `CHARACTER` 可用于将列表限制为仅数值型或仅字符型。同样，该列表依赖于顺序并包含端点，前提是它们类型正确。列表 `DOB--NUMERIC--HT` 排除 `RACE`，而列表 `SEX--character--SYMP` 仅包含三个变量（`SEX`、`RACE` 和 `SYMP`）。

包含错误类型不会导致错误。指定 `death--character--symp` 将正确包含两个变量 `RACE` 和 `SYMP`。

与使用单个连字符的列表缩写（公共前缀编号列表）不同，这种列表形式不能用于创建变量或向 PDV 添加变量。但是，它可以用于其他需要变量列表的地方。

### 警告

由于 PDV 上变量的顺序对大多数 SAS 程序员来说通常次要，因此在使用这些形式的列表时要非常小心。如果变量顺序因某种原因发生变化，列表可能不再是你想要的结果。

### 使用冒号运算符（名称前缀）

以公共前缀命名的变量（带或不带数字后缀）可以通过在前缀后跟冒号来列出。

对于由以下 PROC SUMMARY 生成的数据集 STATS，你可以通过使用列表 `HT_:.` 选择与 HT 关联的所有统计量。

