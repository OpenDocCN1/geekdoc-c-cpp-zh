
# 388 实例式 SAS 学习：程序员指南，第二版

## 程序 22.11：使用 CNTLNIN= 创建的数据集

```sas
data Disease;
input ICD10 : $5. @@;
datalines
020 410 500 493
;

title "Listing of Disease"
proc print data=Disease noobs;
format ICD10 $ICDFMT;
run;
```

以下是输出：

# 图 22.10：程序 22.11 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_394_0.png)

注意，ICD-10 代码 500 没有对应的格式。如果你正在编写自己的 `PROC FORMAT` 语句，可以使用 `OTHER` 关键字为不匹配的代码提供标签。如果你想使用 CNTLN 数据集来实现这一点，你需要一种方法为 `OTHER` 分配一个值。CNTLN 数据集使用变量 `High`, `Low`, `Other` 来指示你想使用这些关键字之一，而不是显式的范围值。

如果你想为不在列表中所有的 ICD-10 代码分配标签 **Found**（已找到），你可以按照以下步骤操作：

# 程序 22.12：为你的格式添加另一个类别

```sas
data Control;
set Learn.Codes (rename=
(ICD10 = Start
Description = Label))
End = Last;)
retain Fmtname '$ICDFMT'
type 'C';
output;

if last then do;
Start = ' ';
Hlo = 'o';
Label = 'Not Found';
output;
end;
run;
```

## 第 22 章：使用自定义格式和输入格式的高级功能 389

你想在 `Control` 数据集的底部添加一个观测值，其 `HLO` 值为 `o` (OTHER)，`LABEL` 等于 `Not Found`（未找到）。你可以使用 `END=` 数据集选项来测试输入数据集的末尾。当数据集中的最后一个观测值被读取时，变量 `Last` 为真。`HLO` 和 `LABEL` 都被分配了一个值，并且在数据集末尾添加了一个单一观测值：这里是数据集列表：

# 图 22.11：数据集 Control 列表

| Start | Label | Fmtname | Type | Hlo |
|---|---|---|---|---|
| 020 | Plague | $ICDFMT | C | |
| 022 | Anthrax | $ICDFMT | C | |
| 390 | Rheumatic fever | $ICDFMT | C | |
| 410 | Myocardial infarction | $ICDFMT | C | |
| 493 | Asthma | $ICDFMT | C | |
| 540 | Appendicitis | $ICDFMT | C | |
| | Not Found | $ICDFMT | | o |

此数据集中的最后一个观测值包含了将 `OTHER` 设置为 `Not Found` 的指令。虽然我们在这个程序中决定将 `Start` 设置为空值，但实际上并不是必须的，因为使用的是关键字 `OTHER` 而不是实际的范围。

当这个新格式在程序 22.11 中使用时，ICD-10 代码 500 现在被标记为 `Not Found`。以下是 `PROC FORMAT` 的输出，显示 `OTHER` 类别已添加到格式中，以及疾病集的列表：

# 图 22.12：由 FMTLIB 选项创建的格式

| FORMAT NAME: $ICDFMT LENGTH: 21 NUMBER OF VALUES: 7 |
| MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH: 21 FUZZ: |
| START | END | LABEL (VER. V7|V8 03DEC2017:10:34:16) |
| 020 | 020 | Plague |
| 022 | 022 | Anthrax |
| 390 | 390 | Rheumatic fever |
| 410 | 410 | Myocardial infarction |
| 493 | 493 | Asthma |
| 540 | 540 | Appendicitis |
| **OTHER** | **OTHER** | Not Found |

注意 `OTHER` 类别现在被标记为 `Not Found`。

以下是带有更新后的 `$ICDFMT` 格式的数据集 `Control` 的列表：

# 390 实例式 SAS 学习：程序员指南，第二版

图 22.13：数据集 Control 列表（已添加 OTHER）

| Unformatted_ICD | ICD10 |
|---|---|
| 020 | Plague |
| 410 | Myocardial infarction |
| 500 | Not Found |
| 493 | Asthma |

显示了 ICD 数据的未格式化和格式化值，以便清晰地看到代码 500 现在显示 `Not Found`。

## 22.8 更新和维护你的格式

假设你想向你的 `$ICDFmt` 中添加一些 ICD-10 代码。实现此点的简单方法是首先使用 `PROC FORMAT` 的 `CNLOUT` 选项创建一个包含所有格式信息的数据集。然后，你可以在 `DATA` 步骤中使用该数据集来添加新代码或修改现有代码。

例如，假设你想在 `$ICDFMT` 格式中添加两个新的 ICD-10 代码：427.5 和 466。以下程序如下：

# 程序 22.13：使用 CNTLOUT 更新现有格式

```sas
proc format cnout=Control_Out;
    $ICDFMT;
run;

data New_Control;
    set Control_Out end=Last;
    length Label = $21;
    output;

    if Last then do;
        Hlo = ' ';
        Start = '427.5';
        End = '466';
        Label = 'Cardiac Arrest';
        output;
    end;
run;
```

## 第 22 章：使用自定义格式和输入格式的高级 391

你想在 `Control` 数据集的底部添加一个观测值，其 `HLO` 值为 `o` (OTHER)，且 `LABEL` 等于 `Not Found`。你可以使用 `END=` 数据集选项来测试输入数据集的末尾。当数据集中的最后一个观测值被读取时，变量 `Last` 为真。`HLO` 和 `LABEL` 都被分配了一个值，并且在数据集末尾添加了一个单一观测值：这里是数据集列表：

# 图 22.14：数据集 Control 列表

| FMTNAME | START | END | LABEL |
|---|---|---|---|
| $ICDFMT | 020 | 020 | Plague |
| $ICDFMT | 022 | 022 | Anthrax |
| $ICDFMT | 390 | 390 | Rheumatic fever |
| $ICDFMT | 410 | 410 | Myocardial infarction |
| $ICDFMT | 427.5 | 427.5 | Cardiac Arrest |
| $ICDFMT | 466 | 466 | Bronchitis |
| $ICDFMT | 493 | 493 | Asthma |
| $ICDFMT | 540 | 540 | Appendicitis |
| $ICDFMT | | o | Not Found |

此数据集中的最后一个观测值包含了将 `OTHER` 设置为 `Not Found` 的指令。虽然我们在这个程序中决定将 `Start` 设置为空值，但实际上并不是必须的，因为使用的是关键字 `OTHER` 而不是实际的范围。

当这个新格式在程序 22.11 中使用时，ICD-10 代码 500 现在被标记为 `Not Found`。以下是 `PROC FORMAT` 的输出，显示 `OTHER` 类别已添加到格式中，以及疾病集的列表：

# 392 实例式 SAS 学习：程序员指南，第二版

最后，使用 `CNTLIN=` 选项重新创建 `$ICDFMT`。不是使用 `FMTLIB` 选项，而是 `SELECT` 语句来识别你需要的格式。这里是：

# 图 22.15：新格式

| FORMAT NAME: $ICDFMT LENGTH: 21 NUMBER OF VALUES: 9 |
| MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH: 21 FUZZ: 0 |
| START | END | LABEL (VER. V7|V8 03DEC2017:12:53:38) |
| 020 | 020 | Plague |
| 022 | 022 | Anthrax |
| 390 | 390 | Rheumatic fever |
| 410 | 410 | Myocardial infarction |
| 427.5 | 427.5 | Cardiac Arrest |
| 466 | 466 | Bronchitis |
| 493 | 493 | Asthma |
| 540 | 540 | Appendicitis |
| **OTHER** | **OTHER** | Not Found |

## 22.9 在格式中使用格式

当你定义格式或输入格式标签时，你也可以包含 SAS 或用户编写的格式或输入格式的名称，而不是标签中的字符串。这里有一个例子。

你想使用 `MMDDYYY10.` 输入格式读取从 2018 年 1 月 1 日到 2018 年 12 月 31 日的日期。2018 年 1 月 1 日之前的日期应该格式化为 `Not Open`，2018 年 12 月 31 日之后的日期应该格式化为 `Too Late`。你可以按照以下方式使用嵌套格式来实现这一点：

# 程序 22.14：演示嵌套格式

```sas
proc format;
value Registration low < '01Jan2018'd = 'Not Open'
      '01Jan2018'd - '31Dec2018'd = [mmddyyy10.]
      '01Jan2019'd high = 'Too Late';
run;
```

程序 22.15 使用此格式来处理注册日期并生成日期和名称的列表。

## 第 22 章：使用自定义格式和输入格式的高级功能

## 程序 22.15：在 DATA Step 中使用嵌套格式

```sas
data Conference;
  input @1 Name $10;
    @11 Date mmddyy10;
  format Date Registration;
datalines;
Smith 10/21/2018
Jones 11/13/2017
Harris 01/03/2018
Arnold 02/12/2019
;
```

此处显示了数据集 Conference 的列表：

## 图 22.16：数据集 Conference 的列表

| Name | Date |
| --- | --- |
| Smith | 10/21/2018 |
| Jones | Not Open |
| Harris | 01/03/2018 |
| Arnold | Too Late |

这是 PROC FORMAT 的一个非常强大的功能。它避免了在 DATA Step 中编写 IF-THEN-ELSE 语句的必要性。

下一个示例使用了用户自定义的输入格式（informats）。在这个示例中，你被提供了关于苯暴露的数据。其中某些值是每百万部分的实际苯水平，而另一些值是工人暴露的年份。对于 1946 年到 1952 年的每一年，苯水平都制表了。对于范围之外的年份，报告了实际苯水平。接下来显示了来自 Benzene.txt 的一些样本数据，包含年份或苯水平：

```
001 90
002 1950
003 217
004 1952
005 177
```

所有的苯水平都远小于任何年份值，因此不会混淆是将某个值读作年份还是苯水平。通过像这样嵌套输入格式，可以极大地简化创建 ID 和苯水平的数据集创建过程：

## 程序 22.16：创建苯水平数据集

```sas
proc format;
  value YearExp 1946 = 250
                    1947 = 244
                    1948 = 240
                    1949 = 200
                    1950 = 188
                    1951 = 150;
  1952 -;
  value Exp Low - <1946 = [7.1]
                    1946 - 1952 = [Yearexp].
                    1952< high = [7.1];

data Benzene;
  infile 'C:\Learning\Benzene.txt';
  input Exposure = Exp4.;
```

第一个输入格式 YAREXP 为 1946 年到 1952 年的每一年替换一个苯水平。输入格式 EXP 对于小于 1946 或大于 1952 的值使用 SAS 7.1 输入格式。否则，使用 YAREXP 输入格式。

以下是该数据集的列表：

## 图 22.17：数据集 Benzene 的列表

## 数据集 Benzene 的列表

| ID | Exposure |
| --- | --- |
| 1 | 9.0 |
| 2 | 188.0 |
| 3 | 21.7 |
| 4 | 100.0 |
| 5 | 17.7 |

这个问题也可以使用格式（formats）而不是输入格式（informats）来解决。使用格式，你需要读取原始数据值并使用 PUT 函数来获取格式化后的值。由于 PUT 函数的结果是字符值，你还需要使用 INPUT 函数来获取作为数值形式的苯水平。创建格式会使该过程变得简单得多。

## 22.10 多标签格式 (Multilab Formats)

在正常情况下，如果你的任何格式范围发生重叠，你将收到错误消息。但是，如果你在 VALUE 语句中使用 MULTILABEL 选项，就可以创建一个具有重叠范围的格式。某些使用多标签的过程随后可以使用 MULTILABEL 格式 (MLF) 来生成显示所有格式范围的表格。这里有一个示例。

你想以两种方式对变量 Age（来自 Survey 数据集）进行细分：一种是每 20 年一个间隔，另一种是按 50 岁作为分界点进行划分。你首先像这样创建一个 MULTILABEL 格式：

## 程序 22.17：创建一个 MULTILABEL 格式

```sas
proc format;
  value AgeGroup (multilabel)
    0 <20 = '00 to <20'
    20 <40 = '20 to <40'
    40 <60 = '40 to <60'
    60 <80 = '60 to <80'
    80 - high = '80 +'

    0 <50 = 'Less than 50'
    50 - high = '> or = to 50';
run;
```

如果没有 MULTILABEL 选项，PROC FORMAT 会发出关于范围重叠的错误消息并无法创建格式。

你可以在 PROC MEANS、PROC SUMMARY 和 PROC TABULATE 中使用此格式。这是一个 PROC MEANS 示例：

## 程序 22.18：在 PROC MEANS 中使用 MULTILABEL 格式

```sas
title "Demonstrating Multilabel Format"
title2 "PROC MEANS Example";
proc means data=Learn.Survey / MLF;
  class Age;
  var Salary;
  format AgeGroup;
run;
```

如果你想使用格式的这一功能，在 CLASS 语句中使用 MLF 选项是重要的。以下是输出：

## 图 22.18：程序 22.18 的输出

## 多标签格式 PROC示例

| Analysis Variable : Salary | Obs | Mean | Std Dev | Maximum |
| --- | --- | --- | --- | --- |
| Age of 1/1/2006 | N | | | |
| 20 to <40 | 3 | 3 | 29186.67 | 6798.13 | 36560.00 |
| 40 to <60 | 2 | 2 | 76111.50 | 16234.56 | 76100.00 |
| 60 to <80 | 2 | 2 | 109000.00 | 26870.06 | 90000.00 |
| > or = to 50 | 3 | 3 | 98041.00 | 26857.01 | 76123.00 |
| Less than 50 | 4 | 4 | 40915.00 | 24104.46 | 76100.00 |

你可以将 MULTILABEL 格式配合 PROC TABULATE 创建有趣的表格。这里有一个按性别计算年龄频率的程序：

## 程序 22.19：多标签格式
