
```sas
title "Applying the ORDER Usage for Two Variables"
proc report data=Learn.Sales;
column EmID Quantity TotalSales;
define EmID / order "Employee ID" width=11;
define TotalSales / descending order "Total Sales" width=9 format=dollar9;
define Quantity / width=8 format=comma8;
run;
```

因为你希望报告显示每个员工总销售额的降序，请在 `ORDER` 之前加上 `DESCENDING` 关键字。记住，报告中 `ORDER` 变量的顺序由它们在 `COLUMN` 语句中的顺序控制。

以下是该报告：

### 图 15.11：程序 15.12 的输出（部分列表）

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_258_0.png)

报告按员工升序排列，并按总销售额降序排列。

## 15.11 创建多列报告

`PROC REPORT` 可以创建电话簿风格的多列报告。当你只有少数变量需要报告并想节省纸张时，这种方法特别有用。数据集 `Assign` 包含科目编号（`Subject`）和分组（A、B 或 C）。使用 `REPORT` 的 `PANELS=` 选项，可以多列形式打印此报告。如果你指定了一个很大的面板数量，`PROC REPORT` 会根据给定的行宽尽可能适应多个面板。

> 注意：与 `FLOW` 选项一样，此选项仅影响列表输出。它对 HTML 或 PDF 等其他 ODS 目标没有影响。如果你的输出目标是 PRINTER、PDF 或 RTF，可以在 ODS 语句中使用 `COLUMNS=` 选项。

以下是该程序：

## 程序 15.13：创建多列报告

```sas
title "Random Assignment - Three Groups"
proc report data=Learn.Assign panels=99
      headline Group;ps=16;
      columns Subject Group;
      define Subject / display=7;
      define Group / widths=5;
```

页大小（`PS`）设置为 16（限制每页 16 行），以便你可以看到 `PANELS=` 选项的效果。在此程序中，对 `Subject`（数值变量）使用了 `DISPLAY`。因为 `Group`（字符变量）默认就是显示，所以你本也会获得详细报告。不过，包含它是可以的。以下是报告：

图 15.12：程序 15.13 的输出

| Subject | Group | Subject | Group | Subject | Group |
|---|---|---|---|---|---|
| 1 | C | 13 | A | 25 | B |
| 2 | B | 14 | A | 26 | C |
| 3 | B | 15 | C | 27 | B |
| 4 | A | 16 | A | 28 | A |
| 5 | B | 17 | C | 29 | B |
| 6 | A | 18 | B | 30 | B |
| 7 | C | 19 | B | 31 | B |
| 8 | C | 20 | B | 32 | B |
| 9 | B | 21 | C | 33 | C |
| 10 | A | 22 | C | 34 | C |
| 11 | C | 23 | C | 35 | A |
| 12 | C | 24 | C | 36 | A |

## 15.12 生成报告断符

`PROC REPORT` 可以使用 `BREAK` 和 `RBREAK` 语句对分析变量生成总计和小小计。`RBREAK` 代表 report break，用于在报告顶部或底部报告统计摘要（通常是总和或平均值）。`BREAK` 语句用于在 `GROUP` 或 `ORDER` 变量值变化时报告统计摘要。让我们来看例子。

使用 `Sales` 数据集，你希望在报告底部查看 `Quantity` 和 `TotalSales` 的总量。以下程序生成此报告：

## 程序 15.14：请求报告断符（RBREAK）语句

```sas
title "Producing Report Breaks";
proc report data=Learn.Sales;
column Quantity TotalSales;
define Quantity / width=8 format=comma8;
define TotalSales / "Total Sales" width=9
format=dollar9;

break after / summarize;
```

`RBREAK` 关键字是一个位置，`BEFORE` 将统计数据放在开头，`AFTER` 将其放在结尾。`SUMMARY` 选项根据你是否请求来打印摘要。报告如下：

图 15.13：程序 15.14 的输出

| Quantity | TotalSales |
| --- | --- |
| 100 | $1,995 |
| | $19,995 |
| 5 | $53 |
| | 100 | $669 |
| | 100 | $889 |
| 2 | $20,000 |
| | 10 | $300 |
| | 100 | $599 |
| | 1 | $5,129 |
| | 1 | $9,109 |
| | 3 | $15,597 |
| | 3 | $15,597 |
| 50 | $300 |
| | 1,000 | $1,990 |

允许按姓对报告进行排序，但从报告中删除了此变量。在程序 15.16 的列表中，请注意报告的行是按姓排序的：

# 图 15.16：程序 15.16 的输出

| 姓名 | 员工 ID | 总销售额 |
|---|---|---|
| Glenda Johnson | 0177 | $21,651 |
| Sharon Lu | 9888 | $2,290 |
| Jason Nguyen | 0017 | $21,990 |
| George Smith | 1843 | $46,780 |

## 15.14 使用 PROC REPORT 计算新变量

这使得 `PROC REPORT` 在所有 SAS 过程中显得与众不同。对于大多数 SAS 过程，如果你想执行任何计算，都需要先运行一个 DATA 步阶。

假设你想报告 Medical 数据集中患者的体重，但不是以磅（数据集中使用的单位）报告体重，而是想以公斤为单位查看体重。程序 15.17 使用了一个计算块（compute block）来实现这一目标。

# 程序 15.17：使用 PROC REPORT 计算新变量

```
title "Computing a New Variable";
proc report data=Learn_Medical;
column Patno Weight=Wtkg;
define Patno / display "Patient Number" width=7;
define Weight / computed "Weight in Kg"
compute Wkg;
Wtkg = Weight / 2.2;
width=6 format=6.1;
endcomp;
run;
```

注意关于此程序的以下几点：

- 新变量 (`Wtkg`) 和你用于计算它的变量 (`Weight`) 都列在 `COLUMN` 语句中。计算值必须跟在定义它的变量之后，这很重要。如果你不想在报告中包含体重的原始值，请在 `Weight` 的 `DEFINE` 语句中使用关键字 `NOPRINT`。
- 在你新变量的 `DEFINE` 语句中使用 `COMPUTED` 用法。
- 使用 `COMPUTE` 和 `ENDCOMP` 语句创建一个 `COMPUTE` 块。你在这个块内部定义你的变量。

正如你将在下一个示例中看到的，该块可以包含编程逻辑以及算算术计算。

以下是输出结果：

图 15.17：程序 15.17 的输出

| 患者编号 | 体重（公斤） |
|---|---|
| 001 | 54.5 |
| 003 | 75.5 |
| 002 | 95.5 |
| 004 | 130.9 |
| 007 | 81.8 |
| 050 | 90.5 |

## 15.15 在 COMPUTE 块中计算字符变量

我们在上一个示例中提到的，你可以在 `COMPUTE` 块中包含编程逻辑。在这个示例中，你想根据心率 (`HR`) 创建一个新的字符变量 (`Rate`)，其值为快 (`Fast`)、正常 (`Normal`) 或慢 (`Slow`)。以下是该程序：

程序 15.18：在 COMPUTE 块中计算字符变量

```
title "Creating a Character Variable in a COMPUTE Block";
proc report data=Learn.Medical;
column Patient HR Rate;
define Patient / display "Patient Number" width=7;
define HR / display "Heart Rate" width=5;
define Weight / display width=6;
compute Rate / length=6;
if HR gt 75 then Rate = 'Fast';
else if HR gt 55 then Rate = 'Normal';
else if not missing(HR) then Rate='Slow';
endcomp;
run;
```

与之前一样，你将在 `COLUMN` 语句中包含你正在计算的变量。`COMPUTE` 语句现在包含了关键字 CHARACTER，告诉 SAS `Rate` 是一个字符变量。选项 `LENGTH=6` 定义了该变量的存储长度。

接下来，计算 `Rate` 的逻辑语句被夹在 `COMPUTE` 和 `ENDCOMP` 语句之间。以下是输出结果：

图 15.18：程序 15.18 的输出

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_265_0.png)

新变量 (`Rate`) 现在被包含在报告中。

## 15.16 使用 PROC REPORT 创建 ACROSS 变量

除了创建简单的列报告，`PROC REPORT` 还可以创建表格风格的报告，变量的每个唯一值都会在报告中形成一个新列。

这是通过对你的变量使用 `ACROSS` 用法实现的。在后续示例中，`Bicycle` 数据集中的每种自行车（混合型、山地和公路）都将用于在报告中创建单独列：

程序 15.19：演示 PROC REPORT 中的 ACROSS 用法

```
***Demonstrating an Across Usage;
title "Demonstrating an Across Usage"
proc report data=Learn.Bicycles;
  column Model,Units; / group widths=14;
  define Model / across "Model"
  define Units / sum "# of Units" width=14
    format=comma8;
run;
```

除了将 `Model` 定义为 Across 变量外，你还需要告诉过程对于表格的每行显示什么值。`COLUMN` 语句中的 `Model`、`Units` 术语是给 `PROC REPORT` 的指令，报告每个 `Model` 类别的单元数量。这里的列表应该有助于澄清其工作原理：

图 15.19：程序 15.19 的输出

| 模型 | 混合型自行车 | 山地自行车 | 公路自行车 | 国家 |
|---|---|---|---|---|
| 数量 | 1100 | 6400 | 4300 | 法国 |
| | 700 | 3400 | 5000 | 意大利 |
| | 500 | 10000 | 7000 | 美国 |
| | | 1211 | 3364 | |

## 15.17 使用 ACROSS 用法显示统计

你可以使用 `ACROSS` 用法来创建一个报告，显示每个变量层级的统计信息。你想要报告数据集中性别、类型和年龄的平均值。你还需要以列的形式显示年龄。程序 15.20：使用 ACROSS 用法显示统计

```
title "Average Blood Counts"
proc report data=Learn;
column Gender BloodType Age;
def Gender / group width=8;
def BloodType / group "Blood Type";
def Age / ACROSS "Age Group";
. / format=8;
run;
```

`COLUMN` 语句显示了 `WBC`（白细胞）和 `RBC`（红细胞）的平均值。你还需要以列的形式显示年龄。以下是输出结果：

图 15.20：程序 15.20 的输出

| 性别 | 血液类型 | 20-29 | 30-39 | 40-49 | 50-59 | 60-69 | 70-79 |
|---|---|---|---|---|---|---|---|
| 女性 | 白细胞 | 7112 | 6556 | 7251 | 7033 | 7762 | 810 |
| | 红细胞 | 5.50 | 4.70 | 5.53 | 5.85 | 5.59 | 5.82 |
| 男性 | 白细胞 | 6988 | 7043 | 6995 | 7138 | 7769 | 7077 |
| | 红细胞 | 5.47 | 5.48 | 5.41 | 5.47 | 5.41 | |

# 高血压患者

| 性别 | 收缩压 (SBP) | 舒张压 (DBP) | 是否高血压? |
|---|---|---|--|
| 男 | 144 | 90 | 是 |
| 女 | 110 | 62 | 否 |
| 男 | 130 | 80 | 否 |
| 女 | 120 | 70 | 否 |
| 男 | 142 | 82 | 是 |
| 男 | 150 | 96 | 是 |
| 女 | 138 | 88 | 否 |
| 女 | 132 | 76 | 否 |

- 5. 使用 SAS 数据集 `BloodPressure` 生成一个显示性别和年龄的报告，以及一个名为 `AgeGroup` 的新变量。`AgeGroup` 的值根据年龄（`Age`）的值分为 <= 50 或 > 50。为此变量标签为“Age Group”。你的报告应该如下：

## 患者年龄分组

| 性别 | 年龄 | 年龄组 |
|---|---|---|
| 男 | 23 | <= 50 |
| 女 | 68 | > 50 |
| 男 | 55 | > 50 |
| 女 | 28 | <= 50 |
| 男 | 35 | <= 50 |
| 男 | 45 | <= 50 |
| 女 | 48 | <= 50 |
| 女 | 78 | > 50 |

- 6. 使用 SAS 数据集 `BloodPressure` 生成一个显示性别、年龄、收缩压、舒张压的报告。按照所示的性别和年龄对报告排序：

## 按性别和年龄排序的受者

| 性别 | 年龄 | 收缩压 | 舒张压 |
|---|---|---|---|
| 女 | 28 | 120 | 70 |
| | 48 | 138 | 88 |
| | 68 | 110 | 62 |
| | 78 | 132 | 76 |
| 男 | 23 | 144 | 90 |
| | 35 | 142 | 82 |
| | 45 | 150 | 96 |
| | 55 | 130 | 80 |

- 7. 使用 SAS 数据集 `Blood` 生成一个报告，显示每个性别和血型（`BloodType`）组合的平均胆固醇（`Chol`）。你的报告应该如下：

## 各性别和血型的平均胆固醇

| 性别 | 血型 | 平均胆固醇 |
|---|---|---|
| 女 | A | 201.4 |
| | AB | 166.5 |
| | B | 208.1 |
| | O | 205.6 |
| 男 | A | 201.5 |
| | AB | 191.2 |
| | B | 211.1 |
| | O | 197.9 |

- 8. 使用数据集 `Blood` 生成一个类似于此的报告。表格中的数字是每种血型和性别组合的平均白细胞（`WBC`）计数和红细胞（`RBC`）计数。

## 调查数据集报告

| 受者 ID | 截至2006/1/1的年龄 | 性别 | 年薪 | 平均响应 |
|---|---|---|---|---|
| 001 | 小于 30 岁 | 男 | $28,000 | 1.8 |
| 002 | 51 以上 | 女 | $76,123 | 2.6 |
| 003 | 30 到 50 岁 | 男 | $36,500 | 1.8 |
| 004 | 51 以上 | 女 | $128,000 | 3.2 |
| 005 | 小于 30 岁 | 男 | $23,060 | 3.0 |
| 006 | 51 以上 | 男 | $90,000 | 3.4 |
| 007 | 30 到 50 岁 | 男 | $76,100 | 3.6 |

- 9. 使用 SAS 数据集生成一个显示 ID、性别、年龄、变量以及这五个变量平均值的报告。你的报告应该如下：

## 调查集报告

| 受者 ID | 截至2006/1/1的年龄 | 性别 | 年薪 | 平均响应 |
|---|---|---|---|---|
| 001 | 小于 30 岁 | 男 | $28,000 | 1.8 |
| 002 | 51 以上 | 女 | $76,123 | 2.6 |
| 003 | 30 到 50 岁 | 男 | $36,500 | 1.8 |
| 004 | 51 以上 | 女 | $128,000 | 3.2 |
