
| 022 | 022 | Anthrax |

| 390 | 390 | Rheumatic fever |

| 410 | 410 | Myocardial infarction |

| 493 | 493 | Asthma |

| 540 | 540 | Appendicitis |

程序 22.11 显示了你如何使用这种格式：

# 程序 22.11：使用 CNTLIN= 创建的数据集

```sas
data Disease;
  input ICD10 : $5. @@;
datalines
020 410 500 493
;

title "Listing of Disease";
proc print data=Disease noobs;
format ICD10 $ICDFMT;
run;
```

这是输出：

# 图 22.10：程序 22.11 的输出

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_395_0.png)

注意，ICD-10 代码 500 没有格式。如果你在编写 `PROC` 语句，可以使用关键字 `OTHER` 为不匹配的代码提供标签。如果你想通过使用 `CNTLIN` 数据集来实现这一点，你需要一种方法为 `OTHER` 分配值。`CNTLIN` 数据集使用用于 *高、低、其他* 的变量来表示你想使用这些关键字之一而不是显式的范围值。

如果你想为列表中的所有 ICD-10 代码分配“未找到”的标签，可以如下操作：

# 第 22 章：使用自定义格式和信息格式的高级功能 389

你希望在 Control 数据集的底部添加一个观测值，其 HLO 值为 `o` `OTHER`，`LABEL` 等于 `Not Found`（未找到）。你可以通过使用 `END=` 数据集选项来测试输入数据集的结束来实现这一点。当在 `Codes` 数据集中找到最后一个观测值时，变量 `Last` 为真。此时 HLO 和 LABEL 都被赋予了值，并在数据集的末尾添加了一个新的观测值。以下是数据集列表：

# 图 22.11：数据集 Control 列表

| Start | Label | Fmtname | Type | Hlo |

|---|---|---|---|---|

| 020 | Plague | $ICDFMT | C | |

| 022 | Anthrax | $ICDFMT | C | |

| 390 | Rheumatic fever | $ICDFMT | C | |

| 410 | Myocardial infarction | $ICDFMT | C | |

| 493 | Asthma | $ICDFMT | C | |

| 540 | Appendicitis | $ICDFMT | C | |

| | Not Found | $ICDFMT | C | o |

该数据集中的最后一个观测值包含了将 `OTHER` 设置为 `Not Found` 的指令。虽然我们在程序中决定将 `Start` 设置为缺失值，但实际上这并不是必要的，因为使用的是关键字 `OTHER` 而不是实际的范围。

当在程序 22.11 中使用此新格式时，ICD-10 代码 500 现在被标记为 `Not Found`。以下是 `PROC FORMAT` 的输出（显示格式已添加 `OTHER` 类别）以及疾病列表：

# 图 22.12：通过 FMTLIB 创建的格式

| FORMAT NAME: $ICDFMT | LENGTH: 21 | NUMBER OF VALUES: 7 |

| MIN LENGTH: 1 | MAX LENGTH: 40 | DEFAULT LENGTH: 21 | FUZZ: 0 |

| START | END | LABEL (VER. T7|V8) | 03DEC2017:10:34:16) |

| 020 | 020 | Plague |

| 022 | 022 | Anthrax |

| 390 | 390 | Rheumatic fever |

| 410 | 410 | Myocardial infarction |

| 493 | 493 | Asthma |

| 540 | 540 | Appendicitis |

| **OTHER** | **OTHER** | Not Found |

注意类别 `OTHER` 现在被标记为 `Not Found`。

以下是更新了 $ICDFMT 格式的 Control 数据集列表：

390 《通过示例学习 SAS：程序员指南，第版版》

图 22.13：数据集 Control 列表（已添加 OTHER）

| Unformatted_ICD | ICD10 |

|---|---|

| 020 | Plague |

| 410 | Myocardial infarction |

| 500 | Not Found |

| 493 | Asthma |

显示了 ICD 数据的未格式化和格式化值，以便清晰地看到代码 500 现在显示为 `Not Found`。

## 2.8 更新和维护你的格式

假设你想向 $ICDFmt 中添加一些 ICD-10 代码。实现此点的最简单方法是：首先使用 `PROC FORMAT` 的 `CNTLOUT=` 选项创建一个包含所有格式信息的数据集。然后，你可以在 `DATA` 步中使用该数据集来添加新代码或修改现有代码。

例如，假设你想向 $ICDFMT 格式中添加两个新的 ICD-10 代码：`427.5`（气管炎）和 `466`（心脏停动）。以下程序可以完成此任务：

程序 22.13：使用 CNTLOUT 数据集选项更新现有格式

```
proc format cntlout=Control_Out;
    select $ICDFMT;
run;

data New_Control;
    length Label $ 21;
    set Control_Out end=Last;
    output;
    if Last then do;
        Hlo = '427.5';
        Start = Start;
        End = Start;
        Label = 'Cardiac Arrest';
        output;
        Start = '466';
        End = Start;
        Label = 'Bronchitis';
        output;
    end;
;
proc format cntlout=New_Control;
    select $ICDFMT;
run;
```

# 第 22 章：使用自定义格式和信息格式的高级功能 391

你首先运行带有 `CNTLOUT=` 选项的 `PROC FORMAT`，创建一个包含重建格式所需所有信息的输出数据集。`SELECT` 语句允许你选择用于创建此数据集的格式。以下是 Control_Out 数据集的列表：

**图 22:14：数据集 Control_Out 列表**

| FMTNAME | START | END | LABEL | MIN | MAX | DEFAULT | LENGTH |

|---|---|---|---|---|---|---|---|

| ICDMT | 020 | 020 | Plague | 1 | 40 | 21 | 21 |

| ICDMT | 022 | 022 | Anthrax | 1 | 40 | 21 | 21 |

| ICDMT | 390 | 390 | Rheumatic fever | 1 | 40 | 21 | 21 |

| ICDMT | 410 | 410 | Myocardial infarction | 1 | 40 | 21 | 21 |

| ICDMT | 427.5 | 427.5 | Cardiac Arrest | 1 | 40 | 21 | 21 |

| ICDMT | 466 | 466 | Bronchitis | 1 | 40 | 21 | 21 |

| ICDMT | 493 | 493 | Asthma | 1 | 40 | 21 | 21 |

| ICDMT | 540 | 540 | Appendicitis | 1 | 40 | 21 | 21 |

| ICDMT | **OTHER** | **OTHER** | Not Found | 1 | 40 | 21 | 21 |

394 实例型 SAS 学习：程序员指南，第二版

程序 22.16：创建苯浓度水平数据集

```sas
proc format;
invalue YearExp 1946 = 250
                        1947 = 244
                        1948 = 240
                        1949 = 200
                        1950 = 188
                        1951 = 150
                        1952 = 100;

invalue Exp Low <1946 = [7.1]
                    1946 - 1952 = [YearExp].
                    1952 < high = [7.1];

data Benzene;
infile 'C:\Learning\Benzene.txt';
input ID Exposure = Exp4.;
```

第一个输入格式符 `YAREXP` 将 1946 年到 1952 年每年的替换为苯浓度水平。输入格式符 `EXP` 对于小于 1946 或大于 1952 的值使用 SAS 7.1 输入格式符。否则，使用 `YAREXP` 输入格式符。

以下是数据集的列表：

图 22.17：数据集 Benzene 的列表

| ID | Exposure |

|---|---|

| 1 | 9.0 |

| 2 | 188.0 |

| 3 | 21.7 |

| 4 | 100.0 |

| 5 | 17.7 |

这个问题也可以使用格式（formats）而不是输入格式符（informats）来解决。若要使用格式，你需要读取原始数据值并使用 `PUT` 函数获取格式化后的值。由于 `PUT` 函数的结果是字符值，你还需要使用 `INPUT` 函数来获取数值形式的苯浓度水平。创建格式会让过程变得更简单。

## 22.10 多标签格式 Multilab Formats

在正常情况下，如果任何格式范围重叠，你将收到错误消息。然而，如果你在 `VALUE` 语句中使用 `MULTILABEL` 选项，就可以创建一个具有重叠范围的格式。使用多标签的过程可以使用多标签格式（MLF）来生成显示所有格式范围的表格。以下是一个示例。

第 22 章：使用自定义格式和输入格式符的高级功能

你想以两种方式拆分变量 `Age`（来自 Survey 数据集）：一种是每 20 年一个间隔，另一种是以 50 岁为拆分界点。你首先创建一个这样的 `MULTILABEL` 格式：

## 程序 22.17：创建一个 MULTILABEL 格式

```sas
proc format;
value AgeGroup (multiple)
0 - <20 = '00 to <20'
20 - <40 = '20 to <40'
40 - <60 = '40 to <60'
60 - <80 = '60 to <80'
80 - high = '80 +'

0 - <50 = 'Less than 50'
50 - high = '> or to 50';
run;
```

如果没有 `MULTILABEL` 选项，`PROC FORMAT` 会发出关于范围重叠的错误消息并无法创建该格式。

你可以在 `PROC MEANS`、`PROC SUMMARY` 和 `PROC TABULATE` 中使用此格式。以下是一个 `PROC MEANS` 示例：

## 程序 22.18：在 PROC MEANS 中使用多标签格式

```sas
title "Demonstrating a Multilab Format"
title2 "PROC MEANS Example"
proc means data=Learn.Survey / MLF;
  class Age;
  var Salary;
  format AgeGroup;
run;
```

如果要使用格式的这一功能，在 `CLASS` 语句中使用 `MLF` 选项是重要的。以下是输出结果：

## 图 22.18：程序 22.18 的输出

### 展示多标签格式

PROC MEANS Example

| Analysis Variable : Salary Yearly | | | | | | | |

| Age of 1/1/2006 | N Obs | Mean | StDev Dev | Minimum | Maximum |

| 20 to <40 | 3 | 3 | 29186.67 | 6798.13 | 23060.00 | 36500.00 |

| 40 to <60 | 2 | 2 | 76111.50 | 16234.56 | 76100.00 | 76123.00 |

| 60 to <80 | 2 | 2 | 109000.00 | 26870.06 | 90000.00 | 128000.00 |

| > to 50 | 3 | 3 | 98041.00 | 26857.01 | 76123.00 | 128000.00 |

| Less than 50 | 4 | 4 | 40915.00 | 24104.46 | 23060.00 | 76100.00 |

检查此输出显示了按 `Age` 以两种方式拆分的平均 `Salary`：一种是 20 年一个间隔，另一种是以 50 岁为拆分界点。

你可以结合 `PROC TABULATE` 使用 `MULTILABEL` 格式来创建有趣的表格。以下是一个按 `Gender` 计算 `Age` 频率的程序：

## 程序 22.19：展示多标签格式

```sas
title "Demonstrating a Multilab Format"
title2 "PROC TABULATE Example"
proc tabulate data=Learn.Survey;
  class Age / MLF;
  table Age Gender;
  format AgeGroup;
run;
```

这产生了以下输出：图 22.19：程序 22.19 的输出注意某些年龄组没有显示在表中。例如，<20 年组没有受访者。要在表中查看所有可能的格式范围，可以使用 `CLASS` 语句中的 `PRELOADMT` 选项。预加载格式允许 `PROC TABULATE` 列出没有数据的类别。以下是带有 `PRELOADMT` 选项和两个控制缺失值的代码：

## 程序 22.20：在 PROC TABULATE 中使用 PRELOADFMT, PRINTMISS 和 MISTEXT 选项

```sas
title "Demonstrating Multilab Format"
title2 "PROC TABULATE Example"
proc tabulate data=Learn.Survey;
class Age / MLF prelodfmt;
table Age Gender / printmiss misstext=''
format Age.;
run;
```

`PRELOADMT` 选项强制过程列出所有格式范围。该选项在 `TABLE` 语句中使用 `PRINTMISS` 时没有影响。`PRINTMISS` 是针对包含一个或多个缺失值的类的指令。最后，`MISTEXT` 选项告诉过程用什么字符（或字符）打印缺失值（默认是点）。这里选择了一个空格来表示缺失值。最后，输出如下：现在表中出现了所有年龄范围，缺失值显示为空。

## 22.1 使用 INPUTN 函数执行更复杂的查找

本章的最后一个示例使用函数在 `DATA` 步中执行双表查找。此部分有点复杂，你可能想跳过它或参考 SAS Help `http://documentation.sas.com`。

问题是：你有一个年份（1940到1949年）和工作代码表。每个年份和工作代码的组合都有对应的苯浓度（百万分之一）。以下是表格值：

| Year | A | B | C | D | E |

|---|---|---|---|---|---|

| 1944 | 220 | 180 | 210 | 110 | 90 |

| 1945 | 202 | 170 | 208 | 100 | 85 |

| 1946 | 150 | 110 | 150 | 60 | 50 |

| 1947 | 105 | 56 | 88 | 40 | 30 |

| 1948 | 60 | 30 | 40 | 20 | 10 |

| 1949 | 45 | 22 | 22 | 10 | 8 |

给定年份和工作代码来计算浓度的一种方法是为每年创建一个输入格式符，并为每个工作代码分配一个标签。直接使用 `INPUTN` 函数工作量更少。步骤如下：

## 程序 22.21：使用单个数据集创建输入格式符

```sas
data Exposure;
  retain Type 'I' 'U';
  length Fmtname $10;
  do Year = 1944 to 1949;
    Fmtname = cats('Exp',Year, 'fmt');
    do Start = 'A','B','C','D','E';
      End = Start :3.
      output;
    end;
  drop Year;
datalines;
220 180 210 110 90
202 170 208 100 85
150 110 150 60 50
105 56 88 40 30
60 30 40 20 10
45 22 22 10 8;
run;
```
