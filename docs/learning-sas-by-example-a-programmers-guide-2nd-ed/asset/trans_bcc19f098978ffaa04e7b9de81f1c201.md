
为 HR 的 DEFINE 语句添加了标签（放在引号中）和列宽。查看此处的输出以了解这两个 DEFINE 语句的效果：

图 15.5：程序 15.5 的输出

| 心率 | 体重 |
|---|---|
| 78 | 120 |
| 58 | 166 |
| 68 | 210 |
| 88 | 288 |
| 54 | 180 |
| 60 | 199 |

现在你看到的是每个观测结果的详细列表，而不是单一的汇总统计量。

## 15.5 生成摘要报告

为了实现这一点，你希望使用 Medical 数据集中每家诊所的平均心率和平均体重。要做到这一点，你需要对变量 `Clinic` 使用 `GROUP` 用法。此外，你需要指定 `MEAN` 为心率和体重的统计量。程序 15.6 执行了这些操作：

程序 15.6：指定 GROUP 用法以创建摘要报告

```
title "Demonstrating a GROUP Usage";
proc report data=learn.medical;
column Clinic HR;
define Clinic / group width=11;
define HR / analysis mean "Average Heart Rate" width=12
format=5;
define Weight / analysis mean "Average Weight" width=12
format=6;
run;
```

每个数值型变量都指定了 `MEAN` 统计量以及格式（format）。`ANALYSIS` 关键字是可选的，因为这是数值型变量的默认用法。你可以按照喜欢的顺序放置这些选项（label、width、format 等）。报告如下所示：

## 242 实例实例学习 SAS：程序员指南，第二版

图 15.6：程序 15.6 的输出

| 诊所 | 平均心率 | 平均体重 |
|---|---|---|
| HMC | 69 | 218 |
| Mayo Clinic | 67 | 170 |

报告中的数字显示了两个诊所中各自的平均心率和平均体重。

## 15.6 演示 PROC REPORT 的 FLOW 选项

PROC REPORT 的一个非常好的特性是当你有长值时，它可以在列内折行文本。为了演示这一特性，这里有一个包含名为 `Comment` 的 50 个字符变量的报告。由于一个值将占据页面大部分宽度，你可以使用 `FLOW` 选项来改进报告的外观。

> 注意：此选项仅影响列表输出。对 HTML 或 PDF 等其他 ODS 目标无效。对于其他 ODS 目标，长文本字段将自动折行。

以下是实现此目的的代码：

程序 15.7：使用 PROC REPORT 演示 FLOW 选项

```
title "Demonstrating the FLOW Option";
proc report data=Medical headline
split="="=74;
column Patno VisitDate DX HR Weight Comment
define Patno /"Patient Name" width=7;
define VisitDate /width=9 format=date9;
define DX /"DX Code" width=4;
define HR /"Heart Rate" width=6;
define Weight /width=6;
define Comment /width=30 flow;
run;
```

该程序有几个新功能。首先，在 `Comment` 变量的 DEFINE 语句中添加了 `FLOW` 选项。这会将注释在 30 的列宽内折行。需要 `SPLIT` 选项来告诉程序你想在单词（空格）之间拆分注释。如果没有此选项，PROC REPORT 将使用斜杠等其他字符作为可能的换行符。`LS=` 选项允许你选择宽。

用于 `DX` 变量的 `RIGHT` 选项将 DX 值右对齐。字符型变量的默认对齐方式是 `LEFT`。对齐选项有 `LEFT`、`RIGHT`、`CENTER`。以下是报告：

图 15.7：程序 15.7 的输出

### 演示 FLOW 选项

| 患者编号 | 访诊日期 | DX 代码 | 心率 | 体重 | 注释 |
|---|---|---|---|---|---|
| 001 | 21OCT2006 | 7 | 78 | 120 | 患者已持续咳嗽 3 周。 |
| 003 | 01SEP2006 | 8 | 58 | 166 | 患者于 2006/7/1 使用了 β 受体阻滞剂 |
| 002 | 01OCT2006 | 9 | 68 | 210 | 患者已使用抗生素 10 天体重 |
| 004 | 11NOV2006 | 9 | 88 | 288 | 建议患者减肥 |
| 007 | 01MAY2006 | 7 | 54 | 180 | 这一直处于高压力状态下 |
| 050 | 06JUL2006 | 123 | 60 | 199 | 将此患者转诊精神健康部门进行评估 |

这是一份详细报告，显示了数据中的所有观测值。你可能会奇怪为什么这样，因为数值型变量的默认用法是 `ANALYSIS`（以 `SUM` 为默认统计量）。由于患者（`Patno`）是一个字符型变量（用法为 `DISPLAY`）并且它包含在报告中，因此报告中数值型变量的用法也必须是 `DISPLAY`。报告中的一个 `DISPLAY` 变量会强制其他变量的用法变为 `DISPLAY`。某些程序员倾向于显式地为报告中的每个变量编写用法。因此，程序 15.7 可以这样写：

### 程序 15.8：显式为每个变量定义用法
```
title "Demonstrating the FLOW Option"
proc report data=Learn:Medical headline
  split="; len=74;
  column Patno VisitDate DX HR Weight Comment;
  define Patno / display "Patient Number" width=7;
  define VisitDate / display "Visit Date" width=9 format=;
  define DX / display "DX Code" width=4;
  define HR / display "Heart Rate" width=6;
  define Weight / display width=6;
  define Comment / display width=30 flow;
```

## 15.7 使用两个分组变量

为了演示如何将一个分组嵌套在另一个分组中，我们使用名为 `Bicycles` 的数据集。该数据集包含销售自行车的国家、自行车型号（道路、山地或混合型）、制造商、销售数量和总销售额。目标是按国家和型号细分总销售额。要做到这一点，`Country` 和 `Model` 变量被定义为 `GROUP` 用法。以下是程序 15.9：

### 程序 15.9：使用 PROC REPORT 演示多组分组

```
title "Multiple Group Usage"
proc report data=learn.medical headline ls=80;
column Model Manuf Units TotalSales;
define Country / group width=14;
define Model / group width=13;
define Manuf / width=12;
define Units / sum "Number of Units" width=8
format=comma;
define TotalSales / sum "Total Sales (in thousands)"
width=15 format=dollar10;
```

注意现在 Model 位于报告开头，且Country 嵌套在 Model 中。

图 15.9：程序 15.10 的输出（部分列表）

| 型号 | 国家 | 制造商 | 数量 | 总销售额（千） |
|---|---|---|---|---|
| 混合型 | 法国 | Trek | 1100 | $594 |
| | 意大利 | Trek | 700 | $483 |
| | 美国 | Trek | 4500 | $2925 |
| | 英国 | Trek | 800 | $392 |
| | | Cannondale | 500 | 440 |
| 山地自行车 | 法国 | Trek | 5600 | $7280 |
| | | Cannondale | 800 | $1519 |
| | 意大利 | Trek | 3400 | $6382 |
| | 美国 | Trek | 6000 | $7200 |
| | | Cannondale | 4000 | $10800 |
| | 英国 | Trek | 1211 | $1358 |
| 道路自行车 | 法国 | Trek | 3400 | $8500 |

## 15.9 更改报告中的行顺序

如果你想使用 `PROC PRINT` 获取排序后的列表，必须先用 `PROC SORT` 对数据集进行排序。`PROC REPORT` 允许你在过程内部请求排序顺序的报告。这通过在 `DEFINE` 语句中请求 `ORDER` 用法来实现。

例如，假设你想要获取销售数据中包含 `EmpID`、`Quantity` 和 `TotalSales` 变量的列表。此外，你希望按 `EmpID` 排序。以下是该程序：

### 程序 15.11：演示 PROC REPORT 的 ORDER 用法

```
title "Listing from SALES in EmpID Order";
```
