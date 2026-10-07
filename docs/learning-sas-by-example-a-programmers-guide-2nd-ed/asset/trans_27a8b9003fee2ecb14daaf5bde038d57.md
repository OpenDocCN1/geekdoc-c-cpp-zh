
为这些变量添加格式可以大大提高输出的可读性，如下：

图 17.3：程序 17.4 的部分输出

## 添加格式

| 性别 | 频率 | 百比 |
|---|---|---|
| 女性 | 3 | 42.86 |
| 男性 | 4 | 57.14 |

| 州长工作得好吗？ | | |
| Ques1 | 频率 | 百比 |
|---|---|---|
| 强烈不同意 | 1 | 14.29 |
| 不同意 | 2 | 28.57 |
| 中立意见 | 1 | 14.29 |
| 同意 | 1 | 14.29 |
| 强烈同意 | 2 | 28.57 |

财产产税

| 应该禁令枪支 | | |
| Ques3 | 频率 | 百比 |
|---|---|---|
| 强烈不同意 | 1 | 14.29 |
| 不同意 | 3 | 42.86 |
| 中立意见 | 1 | 14.29 |
| 同意 | 1 | 14.29 |
| 强烈同意 | 1 | 14.29 |

注意，格式标签显示在频率表中。

## 288 实例实例 SAS 学习：程序员指南（第二版）

## 17.5 使用格式对值进行分组

由于 PROC FREQ 对格式化后的值计算频率，因此你可以使用格式将值分组到更大的类别中。数据集 `Survey` 包含一个 `Age`（年龄）变量。假设你想为年龄生成频率，并分为三组。你还想查看问题 5 (Ques5)，将值 1 和 2 合并为“通常不同意”类别，将值 4 和 5 合并为“通常同意”类别。你可以使用格式完成这些任务，如下程序所示：

### 程序 17.4：使用格式对值进行分组

```
proc format;
value AgeGroup
  low-<30 = 'Less than 30'
  30-<60 = '30 to 59'
  60-higher = '60 and higher';

value $Agree_Disagree
  '1','2' = 'Generally disagree'
  '3' = 'No opinion'
  '4','5' = 'Generally agree';

title "Using Formats to Create Groups";
proc freq data=Learn.Survey;
  tables Age Ques5 / nocum;
  format AgeGroup Ques5 $Agree_Disagree;

run;
```

这是一个独特的技巧，因为你不需要创建一个新的数据集。如果你想查看不同组的频率，只需要创建一个新格式。以下是输出结果：

### 图 17.4：程序 17.4 的输出

### 使用格式创建分组

| 截至2006年1月1日的年龄 | |
| 年龄 | 频率 |
| 30岁以下 | 2 |
| 30 到 59 岁 | 3 |
| 60岁及以上 | 2 |
| 学校需要扩大 | |
| Ques5 | 频率 |
| 通常不同意 | 3 |
| 中立意见 | 3 |
| 通常同意 | 1 |

年龄频率现在被分为三个类别，Ques5 的李克特量表只有三个类别。

## 17.6 使用 PROC FREQ 对值进行分组时的问题

当 PROC FREQ 使用格式化值创建分组时，可能会出现问题。当你使用关键字 `OTHER` 作为范围来创建格式时，所有不匹配格式的值将将被在一起。PROC FREQ 将它们所有值分配给该变量中值最低的值。

例如，你有一个包含以下值的数据集 `Grouping`（分组）：

图 17.5：数据集 `Grouping` 的数据值

| Obs | X | Obs | X | Obs | X |
|---|---|---|---|---|---|
| 1 | 2 | 5 | 4 | 9 | 5 |
| 2 | 2 | 6 | 4 | 10 | 5 |
| 3 | 3 | 7 | 4 | 11 | 5 |
| 4 | 3 | 8 | missing | 12 | 6 |

你编写了以下程序：

### 程序 17.5：演示 PROC FREQ 分组值中的问题

```
proc format;
value Two
low-3 = 'Group 1'
4-5 = 'Group 2'
other = 'Other values';
run;
ntitle "Grouping Values (First Try)";
proc freq data=Learn.Grouping;
tables X / nocopercent;
format X Two.;
run;
```

查看数据集 `Grouping` 中的值，你本预期会在 Group 1 中看到四个值，在 Group 2 中看到六个值，一个 `Other values` 值和一个缺失值。以下是你得到的结果：

图 17.6：程序 17.5 的输出

| X | 频率 |
|---|---|
| Group 1 | 4 |
| Group 2 | 6 |
| Frequency Missing = 2 |

## 290 实例实例 SAS 学习：程序员指南（第二版）

由于缺失值（missing）和值 6 都属于 `OTHER` 类别，它们被分配了两者中较小的值（缺失），导致了此输出。

要修复这个问题，你需要在创建格式时为缺失值分配一个单独的类别，如下例所示：

### 程序 17.6：修复分组问题

```
proc format;
value Two
low-3 = 'Group 1'
4-5   = 'Group 2'
      = 'Missing'
other = 'Other values';

run;
```

现在，缺失值和其他值不再被放在同一个组中。以下是结果：

### 图 17.7：在缺失类别中为缺失值添加标签

| 分组值（添加缺失值类别） | |
| X 频率 |
| Group 1 4 |
| Group 2 6 |
| Other values 1 |
| Frequency Missing = 1 |

通过为缺失值添加单独的标签，值 6（观测值 12）被放置在 `Other values` 类别中。

## 17.7 在频率表中显示缺失值

SAS 通常会在频率表下方的单独列表中列出缺失值的频率。你可以通过包含 `TABLES MISSING` 选项要求 SAS 将缺失值视为任何其他值并将其包含在频率表中。这不仅将缺失值的计数带入频率表，还改变了 SAS 报告百分比的方式。如果没有 `MISSING` 选项，百分比列中的值通常不是你想要的值。为了清晰起见，让我们带上 `MISSING` 运行 PROC FREQ：

### 程序 17.7：演示 MISSING 选项的影响

```
proc format;
    value Two
    low-3 = 'Group 1'
    4-5 = 'Group 2'
    other = 'Other values';
run;

title "Missing Option Absent";
proc freq data=Learn.Grouping;
    tables X / nocum;
    format X Two.;
run;

title "Missing Option Present";
proc freq data=Learn.Grouping;
    tables X / missing;
    format X Two.;
run;
```

以下是输出：

图 17.8：程序 17.7 的输出

| X | 频率 | 百比 |
|---|---|---|
| Group 1 | 4 | 36.36 |
| Group 2 | 6 | 54.55 |
| Other values | 1 | 9.09 |
| Missing | 1 | 9.09 |

等待，最后的部分的文本似乎乱了。让我根据提供的文本流重构。

## 292 实例实例 SAS 学习：程序员指南（第二版）

## 17.8 修改 PROC FREQ 中值的顺序

默认情况下，PROC FREQ 根据内部值对值排序（即使变量有格式）。你可以使用 `ORDER=` 选项更改频率列表。PROC FREQ 的 `ORDER=` 有效值如下：

| Order= 选项 | 效果 |
|---|---|
| Internal (默认) | 按内部值排序 |
| Formatted | 按格式排序 |
| Freq | 从最高频率到最低频率排序 |
| Data | 根据数据中的顺序排序 |

注意这些选项不会影响缺失值，缺失值总是列在第一个。

为了演示这些选项如何工作，我们从一个包含 1, 2, 3, 4 和缺失值的数据集 `(Test)` 开始，其频率所示：

| 内部值 | 格式化值 | 频率 |
|---|---|---|
| 1 | Yellow | 2 |
| 2 | Blue | 3 |
| 3 | Red | 4 |
| 4 | Green | 1 |

