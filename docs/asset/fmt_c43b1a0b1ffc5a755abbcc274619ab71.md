
```sas
title "Demonstrating Multabel Format";
title2 "PROC TABULATE Example";
proc tabulate data=Learn.Survey;
  class Age / MLF;
  table Age * Gender;
  format AgeGroup;
run;
```

这产生了以下输出：

## 程序 22.19：程序 22.19 的输出多标签格式 PROC TABULATE 示例

| | Female | Male |
| --- | --- | --- |
| | N | N |
| Age as 1/1/2006 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

注意某些年龄组没有显示在表中。例如，没有 0 <20 年龄组。要在表中显示所有格式范围，可以使用 `CLASS` 语句中的 `PRELOADFMT` 选项。预加载格式允许 `PROC TABULATE` 列出没有数据的类别。

## 程序 22.20：在 PROC TABULATE 使用 PRELOADDFMT, PRINTMISS 和 MISSTEXT 选项

```sas
title "Demonstrating a Multilabel Format";
title2 "PROC TABULATE Example";
proc tab data=Learn.Survey;
  class Age / MLF preloadfmt;
  table Age;
    Gender / printmiss misstext=' ';
  format AgeGroup.;
run;
```

`PRELOADDFMT` 选项强制过程列出所有格式范围。该选项对 `TABLE` 语句中的 `PRINTMISS` 选项无效。记住 `PRINTMISS` 是包含一个多个 `CLASS` 变量缺失值的指令。最后，`MISSTEXT=` 告诉过程使用哪个字符（或字符）来表示缺失值（点）。在这里你选择一个空格来表示缺失值。最后是输出：

## 图 22.20：程序 22.20 的输出

| Gender | Female | Male |
| --- | --- | --- |
| Age as 1/1/2006 | N | N |
| 0 to <20 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| 80 + | | |
| > or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

现在所有的年龄范围都出现在表中，缺失值打印为空格。

## 22.11 使用 INPUTN 函数执行更复杂的查找

问题：你有一张年份（1944年到1949年）和工作代码的表格。每个年份和工作代码的组合都有对应的苯暴露（百万部分）。以下是表值：

| Year | A | B | C | D | E |
| --- | --- | --- | --- | --- | --- |
| 1944 | 220 | 180 | 210 | 110 | 90 |
| 1945 | 202 | 170 | 208 | 100 | 85 |
| 1946 | 150 | 110 | 150 | 60 | 50 |
| 1947 | 105 | 56 | 88 | 40 | 30 |
| 1948 | 60 | 30 | 40 | 20 | 10 |
| 1949 | 45 | 22 | 22 | 10 | 8 |

给定年份和工作代码计算暴露量的一种方法是为每一年创建一个输入格式，为每个工作代码分配一个包含暴露值的标签。使用输入格式而不是格式，是因为你可以配合自定义输入格式使用 `INPUT`（或你将看到的 `INPUTN`）函数来直接获取数值。如果你“手动”操作，将如下所示：

## 程序 22.21：显示创建多个输入格式的部分程序

```sas
proc format;
  invalidate Exp1944fmt (upcase);
    'A' = 220
    'B' = 180
    'C' = 210
    'D' = 110
    'E' = 90
  other = ;
  invalidate Exp1945fmt (upcase);
    'A' = 202
    'B' = 170
    'C' = 208
    'D' = 100
    'E' = 85
  other = ;
  invalidate Exp1946fmt (upcase);
    'A' = 150
run;
```

创建一个输入控制数据集（`CNTLIN`）来创建所需的输入格式工作量更少。你按照如下操作：

# 第 22 章：使用自定义格式和 Informats 的高级功能 399

## 程序 22.22：使用单个 CNTLN 数据集创建多个 Informats

```sas
data Exposure;
retain 'I' 'Hlo ' 'U';
length Fmtname $ 10;
do Year = 1944 to 1949;
 Fmtname = cats('Exp',Year,'fmt');
do Start = 'A','B','C','D','E';
  End Label : $3. @;
  output;
end;
end;
drop Year;
datalines;
220 180 210 110 90
202 170 200 100 85
150 110 150 60 50
105 56 88 40 30
60 30 40 20 10
45 22 22 10 8;
;
```

```sas
title "Creating the Exposure Format";
proc format cntlin=inform;
run;
```

**Type=u** 告诉 `PROC FORMAT` 你想要创建一个数值型输入格式（informat）。对于 `HLO` 变量，u 的值告诉该过程在 `INVALUE` 语句中使用 `UPCASE` 选项。你想要如下格式的输入格式：

**yyyyfmt**

在这里，**yyyy** 是从 1944 年到 1949 年的年份值。`CATS` 函数在首先去除任何前导或尾空格后，将每个参数进行拼接（连接）。该函数允许使用数值参数，并执行从数值到字符的转换。以下是 `Exposure` 数据集的前几条观测结果：

### 图 22.21：数据集 Exposure 的部分列表

### 数据集 Exposure 的列表

| Type | Hlo | Fmtname | Start | End | Label |
|---|---|---|---|---|---|
| U | Exp1944fmt | A | | 220 | |
| U | Exp1944fmt | B | | 180 | |
| U | Exp1944fmt | C | | 210 | |
| U | Exp1944fmt | D | | 110 | |
| U | Exp1944fmt | E | | 90 | |
| U | Exp1945fmt | A | | 202 | |
| U | Exp1945fmt | B | | 170 | |
| U | Exp1945fmt | C | | 208 | |
| U | Exp1945fmt | D | | 100 | |

![](img/e9e15d853989558188e1c83b0ae655b0_405_0.png)

400 示例教程学习 SAS：程序员指南，第二版

顺便说一下，如果你想使用 `PROC FORMAT` 的 `SELECT` 语句选择输入格式，你需要在输入格式名称的第一个字符包含一个 `@` 符号。例如，要列出 `EXP1944FMT` 和 `EXP1945FMT` 的内容，将使用程序 22.23：

## 程序 22.23：使用 SELECT 语句显示两个输入格式的内容

```sas
proc format;
    select @Exp1944fmt @Exp1945fmt;
run;
```

当你在 `PROC FORMAT` 中使用 `SELECT` 语句时，没有必要也包含 `FMTLIB` 选项。

让我们继续编写程序。现在你为六年的每一年都有了一个输入格式，你只需要使用年份和代码创建一个输入格式名称，并使用 `INPUTN` 函数配合该名称来检索错误。以下是程序：

## 程序 22.24：使用 INPUTN 函数使用自定义格式执行表查找

```sas
data ReadExp;
    input Worker Year JobCode;
    Exposure = input(JobCode,cats('Exp',Year,'fmt8.'));
    datalines;
001 1944 B
    002 1948 E
    003 1947 C
    005 1945 A
    006 1948 D
    ;
;
```

你不能在这个程序中使用 `INPUT` 函数，因为该函数要求的输入格式名称必须是常量。`INPUTN` 函数允许你在 `DATA` 步中创建输入格式名称。顺便说一下，输入格式名称中的 'N' 会提前告诉 SAS 你将使用的输入格式是字符型还是数值型（在创建名称之前，它无法通过名称是否以 $ 开头来判断）。有两个对应的函数 `PUT` 和 `UTC`，它们允许你在 `DATA` 步中创建字符型或数值型格式名称。

当此程序运行时，输入格式将通过 `CATS` 函数创建。每一年都会创建一个不同的输入格式名称，用于 `INPUTN` 函数。以下是生成数据集列表：

### 图 22.22：数据集 Read_Exp 的列表

### 数据集 Read_Exp 的列表

| Worker | Year | JobCode | Exposure |
|---|---|---|---|
| 001 | 1944 | B | 180 |
| 002 | 1948 | E | 10 |
| 003 | 1947 | C | 88 |
| 005 | 1945 | A | 20 |
| 006 | 1948 | D | 10 |

# 404 实例化学习 SAS：程序员指南，第二版

**图 23.1：数据集 OnePer 的列表**

### 数据集 Learn.OnePer 的列表

| Subj | Dx1 | Dx2 | Dx3 |
| --- | --- | --- | --- |
| 001 | 450 | 430 | 410 |
| 002 | 250 | 240 | |
| 003 | 410 | 250 | 500 |
| 004 | 240 | | |

注意，某些受试者有三个诊断代码，有些有两个，而一个（受试者 004）只有一个。你如何获取诊断代码的频率分布？例如，受试者 001 的第三诊断诊断是 410，而受试者 003 的相同代码列在 `Dx1`。如果数据集结构如下所示，计算诊断代码的频率将更加简单：

**图 23.2：数据集 ManyPer 的列表**

### 数据集 Learn.ManyPer 的列表

| Subj | Visit | Diagnosis |
| --- | --- | --- |
| 001 | 1 | 450 |
| 001 | 2 | 430 |
| 001 | 3 | 410 |
| 002 | 1 | 250 |
| 002 | 2 | 240 |
| 003 | 1 | 410 |
| 003 | 2 | 250 |
| 003 | 3 | 500 |
| 004 | 1 | 240 |

数据集 `ManyPer` 每个受试者有从一到三个观测值。以下是实现此转换的程序：

# 第23章：重构 SAS 数据集 405

## 程序 23.1：从每个受试者一个观测的数据集创建每个受试者有多个观测的数据集

```sas
data Learn.ManyPer;
set Learn.OnePer;
array Dx{3};

do Visit = 1 to 3;
  if missing(Dx{Visit}) then delete;
  Diagnosis = Dx{Visit};
  output;
end;

  keep Subj Diagnosis Visit;
run;
```

虽然你不需要使用数组来解决这个问题，但它确实让程序变得更加紧凑。`DX` 数组有三个元素：`Dx1`、`Dx2` 和 `Dx3`，如果你省略了变量列表，变量名默认为数组名并在末尾附加数字 1 到 n。

让我们花时间描述一下这个程序是如何工作的（如果该程序对你来说直观上清晰，可以跳过本节）。`DO` 循环从 `Visit` 等于 1 开始。`MISSING` 函数测试值 `Dx[1]`（等同于 `Dx1`）是否缺失。对于受试者 001，没有任何诊断代码是缺失的，因此该 `IF` 语句对该受试者永远为假。一个新变量 `Diagnosis` 被赋值为数组 `Dx[1]` 的值（与变量 `Dx1` 相同），该值等于 450。此时，程序程序数据向量（`PDV`）包含以下内容：

| Subj | Dx1 <drop> | Dx2 <drop> | Dx3 <drop> | Visit | Diagnosis |
|---|---|---|---|---|--|
| 001 | 450 | 430 | 410 | 1 | 450 |

由于 `KEEP` 语句的存在，在 `DO` 循环底部，只有 `Subj`、`Visit` 和 `Diagnosis` 被写入数据集 `ManyPer` 中。

在 `DO` 循环的下一次迭代中，`Visit` 等于 2，`Diagnosis` 等于 430，这些值被写入数据集 `ManyPer` 的第二个观测值中。最后，`Visit` 被设置为 3，`Diagnosis` 被设置为 410，第三个观测值被写入输出数据集。

`DATA` 步已到达底部。由于尚未到达 `OnePer` 数据集的末尾，来自 `OnePer` 数据集的一个新观测值进入 `PDV`，处理继续进行。由于受试者 002 的第三个诊断（`Dx3`）是的，`MISSING` 函数返回真值，`DELETE` 语句返回到数据集顶部，观测值不会被写入数据集 `ManyPer`。（同样假设如果存在任何缺失的 `Dx` 代码，它们会位于非缺失代码之后。）

> 注意：如果你将 `DELETE` 替换为 `CONTINUE`，那么即使缺失的 `Dx` 代码存储在任何 `Dx` 变量中，该程序也能正常工作。有关 `CONTINUE` 语句的描述请参见第 8 章。

## 23.3 将每个受试者有多个观测的数据集转换为每个受试者一个观测的数据集：DATA 步

如果你想反过来，从一个每个受试者有多个观测的数据集创建一个每个受试者一个观测的数据集？这个过程要复杂一些，你需要采取一些特殊的预防措施。

例如，你从数据集 `ManyPer` 开始，并想创建一个像 `OnePer` 那样的数据集。以下是实现方法：

## 程序 23.2：从每个受试者有多个观测的数据集创建每个受试者一个观测的数据集

```sas
proc sort data=Learn.ManyPer
  by Subj Visit;

data OnePer;
  set ManyPer;
  by Subj;
  array Dx1-Dx3(3);
  retain Dx1-Dx3;
  if first.Subj then call missing(of Dx1-Dx3);
  Dx(Visit) = Diagnosis;
  if last.Subj then output;
run;
```

如果你按 `Subj` 对输入数据集进行排序（原始数据集已经是 `Subj` 顺序了，但包含排序是为了使程序更具通用性，尽管对于此示例不需要）。接下来，你设置一个数组来持有三个值并保留这些变量。你需要保留这三个变量，因为它们不是来自 SAS 数据集，默认情况下，在 `DATA` 步的每次迭代中它们每个都被设为缺失值。`RETAIN` 语句防止了这种情况发生。接下来，当你开始处理每个受试者的第一次访问（visit）时，你将 `Dx` 的三个值设为空白。如果不这样做，访问次数少于三次的受试者可能会获得来自上一个受试者的诊断。`CALL MISSING` 程序可以一次性将任何数值和字符值设为空白。对于许多 SAS 函数和 `CALL` 程序，如果你使用以 `Var–Var` 形式的变量列表，你需要在变量列表之前加上关键字 `OF`。

如果你需要引用 `First` 和 `Last` 变量，请参阅下一章对这些变量的讨论。接下来，你将 `Diagnosis` 的值分配给适当的 `Dx` 变量（如果 `Visit=1` 则为 `Dx1`，`Visit=2` 则为 `Dx2`，`Visit=3` 则为 `Dx3`）。最后，如果你正在处理患者的最后一次访问，则输出一个保留了 `Subj` 和 `Dx1–Dx3` 变量的单个观测值。

数据集 `OnePer` 的列表与本章所示的相同。

## 23.4 将每个受试者一个观测的数据集转换为每个受试者有多个观测的数据集：PROC TRANSPOSE

`PROC TRANSPOSE` 也可以用于重构数据集。有时，`PROC TRANSPOSE` 提供了一个快速且简单的解决方案——有时 `PROC TRANSPOSE` 的解决方案也可以是复杂的。通常情况下，数据 步解决方案让你对重构过程有更多的控制。正如你在第一个 `PROC TRANSPOSE` 示例中看到的那样，你需要添加一些数据集选项（参见程序 23.4）以实现与原始数据 步相同的结果。

以下程序尝试解决与 23.2 节相同的问题。你从一个重构 `OnePer` 数据集的程序开始，但并没有完全解决问题。这里是代码：

## 程序 23.3：使用 PROC TRANSPOSE 每个受试者一个观测的数据集（首次尝试）

```sas
***注意：数据集已经是 Subj 顺序；
proc transpose data=Learn.OnePer
  by Subj;
  out=ManyPer;
  var Dx1-Dx3;
run;
```

`PROC TRANSPOSE` 获取一个输入数据集并输出一个原始行变为列的数据集。`BY` 语句对每个 `Subj` 值执行操作。结果如下。

**图 23.3：数据集 ManyPer 的列表（转置法）**

# 数据集 ManyPer 的列表
