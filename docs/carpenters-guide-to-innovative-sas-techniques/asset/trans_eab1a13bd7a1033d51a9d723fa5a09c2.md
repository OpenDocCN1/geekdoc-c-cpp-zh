
## 使用 PROC TRANSPOSE

- ❶ 转置过程在 BY 语句中一个（或多个）变量所分的组内进行。在本例中，每个不同的 SUBJECT 将形成一行。
- ❷ 列 SODIUM 被转置为行。

### 2.4.1a 不完整指定的观测

| 观测 | Subject | Visit1 | Visit2 | Visit3 | Visit4 | Visit5 | Visit6 | Visit7 | Visit8 | Visit9 | Visit10 | Visit11 | Visit12 | Visit13 | Visit14 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 208 | 13.7 | 14.1 | 14.1 | 14.1 | 13.9 | 13.9 | 14 | 14.0 | 14.1 | 14.1 | 14.1 | 14.1 | 14.1 | 14.1 |
| 2 | 209 | 14.0 | 14.0 | 13.9 | 14.2 | 14.5 | 13.8 | 14 | 13.8 | 14.1 | 14.2 | 14.1 | 14 | 14.1 | 14.1 |

注意患者 208 在第 3 次和第 9 次访视时的 SODIUM 值。将此结果与 2.4 节所示结果进行比较。如果不仔细检查数据，这一点不会立刻显现，但 TRANSPOSE 的陷阱已经被触发，转置后的数据已被破坏。SODIUM 的值*在某些情况下*与错误的访视关联了起来！

使用 PROC TRANSPOSE 时，有两种方法可确定转置将在哪一行或多行内进行。在前面的示例中使用了 BY 语句。然而，由于每个受试者都有多次访视，每个 SUBJECT 内有多行，而这些行成为新列（VISIT1、VISIT2、VISIT3 等）。问题在于，我们的代码中没有任何内容将 VISIT 变量与新列关联起来，而在本例中，新列将是 VISIT1 到 VISIT14 中的一个变量。患者 208 错过了第 3 次和第 9 次访视，因此其第 9 次访视本应归类为 VISIT11。然而，由于这是患者 208 的第 9 个观测，PROC TRANSPOSE 错误地将数据归类为 VISIT9。请注意，患者 208 和 209 都显示了 VISIT3 的数据，尽管两者实际上都错过了第 3 次访视。

ID 语句（前面的示例中未包含）也可用于帮助标识行。该语句指定一个变量，该变量将用于为新列创建变量名。更重要的是，它还将特定行中的值与指定的新列关联起来。

这类问题可通过以下规则轻松解决：BY 和 ID 语句中的变量组合必须能标识到行级。

在下面的 PROC TRANSPOSE 步骤中，添加了 ID 语句。BY 变量 SUBJECT ❶ 和 ID 变量 VISIT ❷ 构成该数据集的一个唯一键（这两个变量的任意给定组合最多标识一个观测）。

```sas
title2 '2.4.1b BY and ID Form a Unique Key';
proc transpose data=lab.chemistry(keep=subject visit sodium)
               out=lab_nonnormal(keep=subject visit);
   by subject; ❶
   id visit; ❷
   var sodium;
run;
```

与 PROC TRANSPOSE 生成的数据集不同，请注意，即使 VISIT3 未出现在未转置数据中，该数据集也包含 VISIT3 的变量。这是 ARRAY 语句 ❶ 中隐式使用 VISIT3 的结果。

## 在 DATA 步中转置

### 2.4.2a 行转列

| 观测 | SUBJECT | VISIT1 | VISIT2 | VISIT3 | VISIT4 | VISIT5 | VISIT6 | VISIT7 | VISIT8 | VISIT9 | VISIT10 | VISIT11 | VISIT12 | VISIT13 | VISIT14 | VISIT15 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 208 | 13.7 | 14.1 | 14.1 | 13.9 | 14.1 | 14.4 | 14.0 | . | . | . | . | . | . | . | . |
| 2 | 209 | 14.0 | 14.0 | 13.9 | 14.2 | 14.5 | 13.8 | 14 | 14 | 13.8 | 14 | 14.1 | 14.2 | 14.1 | 14 | 14.1 |

### 列转行

你也可以使用 DATA 步对数据集进行规范化。在前面的示例中，我们将两名患者的一些实验室数据从规范形式转换为非规范形式。现在我们将使用类似的 DATA 步将其转换回原始形式。

```sas
title2 '2.4.2b Columns to Rows';
data lab_normal(keep=subject visit sodium);
   set lab_nonnormal(keep=subject visit:); ❻
   by subject;
   array visits {16} visit1-visit16; ❼
   do visit = 1 to 16; ❽
      sodium = visits{visit}; ❾
      output lab_normal; ❿
   end;
run;
```

- ❻ 转换所需的变量保留在传入数据集中。
- ❼ 声明 VISITS 数组，其中每次访视作为一个元素。
- ❽ DO 循环的索引是 VISIT，每次访视时递增。索引变量 VISIT 被添加到程序数据向量中，并将写入新数据集。

### 2.4.2b 列转行

| 观测 | SUBJECT | visit | sodium |
| --- | --- | --- | --- |
| 1 | 208 | 1 | 13.7 |
| 2 | 208 | 2 | 14.1 |
| 3 | 208 | 3 | . |
| 4 | 208 | 4 | 14.1 |
| 5 | 208 | 5 | 14.1 |
| 6 | 208 | 6 | 13.9 |
| 7 | 208 | 7 | 14.0 |
| 8 | 208 | 8 | 14.0 |
| 9 | 208 | 9 | 14.0 |
| 10 | 208 | 10 | . |
| 11 | 208 | 11 | . |
| 12 | 208 | 12 | . |
| 13 | 208 | 13 | . |
| 14 | 208 | 14 | . |
| 15 | 208 | 15 | . |
| 16 | 208 | 16 | . |
| 17 | 209 | 1 | 14.0 |
| 18 | 209 | 2 | 14.0 |
| 19 | 209 | 3 | . |

表中部分内容未显示

- ❾ 变量 SODIUM 由以 VISIT 作为索引标识的数组元素创建。
- ❿ 由于 OUTPUT 语句位于 DO 循环内，它将为 DO 循环的每次迭代写一个观测。

生成的数据集将为每个患者 × 访视组合各有一个观测。现在这包括原本不存在的组合。

在本例中，SUBJECT 208 现在有 VISIT 3 以及 VISIT 11 至 VISIT16 的观测，并且这些访视的 SODIUM 值都适当地缺失。

通过向 OUTPUT 语句 ❿ 添加 IF 条件，可以轻松删除 SODIUM 值缺失的观测。

```sas
if sodium gt .z then output lab_normal;
```

## 2.5 填充稀疏数据

有时在录入数据时，只有当存在特定值时才创建观测。仅反映缺失值或计数数据中计数为 0 的观测不会被创建。这会生成更稠密的数据，因为缺失值会更少。根据包含了哪些观测，整个分类水平或分类水平的组合可能从数据中缺失。这意味着数据本身并未反映真实的抽样方案。有时我们需要显示所有可能的水平——而不仅仅是那些具有非缺失值的水平。

创建带有适当缺失值的观测，有时被称为创建稀疏（较不稠密）数据。

本节所示的示例使用 LAB_CHEMISTRY 数据，该数据每个患者每次访视有一行。错过的访视不会在数据中表示，也不会在表格和报告中表示。

LAB_CHEMISTRY 数据中的每位患者（SUBJECT）都应对前 10 次访视中的每一次有一个观测，并且可能有也可能没有第 11 至 16 次访视的后续随访。我们需要确保每位患者对前 10 次访视都有观测。

### 2.5.1 已知的行模板

当我们知道分类变量应取值的完整列表时，可以构建一个模板并将其合并回原始数据。合并包含分类变量所有可能组合的模板的过程，会将适当的观测添加到数据集中。对于下面的示例，我们希望每个 SUBJECT 至少具有前 10 次访视。

```sas
proc sort data=advrpt.lab_chemistry ❶
        out=lab_chemistry;
    by subject visit;
run;
proc sort data=advrpt.lab_chemistry
        out=sublist(keep=subject) ❷
        nodupkey; ❸
    by subject;
run;
data subvislist;
    set sublist;
    do visit = 1 to 10; ❹
        output subvislist;
    end;
run;
data sparsed;
    merge subvislist ❺
        lab_chemistry;
    by subject visit; ❻
run;
```
