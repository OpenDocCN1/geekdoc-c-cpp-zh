
## 4.1 PROC SORT 选项

PROC SORT 有许多关联选项，不仅可用于控制该过程的性能和能力，还可控制生成的数据集。其中一个选项 NODUPREC 尤其值得关注，因为误用可能导致意外结果。

### 4.1.1 NODUPREC 选项

我认为 NODUPREC 选项（以及它的别名 NODUPLICATES 和 NODUP）被使用得过于频繁。虽然它的行为正如文档所述，但它*并不*做许多用户认为它会做的事。因此，当我在别人的代码中看到它时，总会引起我的警觉，让我更仔细地检查数据。该选项的大多数用户认为它会删除所有重复观测，虽然这名义上正是它应该做的事，但它*并不一定*会让 PROC SORT 删除*所有*重复观测。事实上，它*只*删除排序后*相邻的*重复观测。当排序过程产生的数据集中重复观测彼此不相邻（它们不是依次连续出现）时，这些重复观测不会被检测到，也不会被删除。

下面的 PROC SORT 使用 NODUPREC 选项，意图是删除任何重复观测。

```sas
title1 '4.1.1a NODUPLICATES in PROC SORT';
proc sort data=advrpt.lab_chemistry
          out=lab_chem
          noduprec;
   by subject;
run;
```

在结果数据集（lab_chem）的清单中可以看到，观测 1 和 3 是重复的，但 PROC SORT 未检测到它们。

**4.1.1a PROC SORT 中的 NODUPLICATES**

| Obs | SUBJECT | VISIT | LABDT | SODIUM | POTASSIUM | CHLORIDE |
|---:|---:|---:|---|---:|---:|---:|
| 1 | 200 | 1 | 07/06/2006 | 140 | 3.6 | 103✓ |
| 2 | 200 | 2 | 07/13/2006 | 144 | 4.81 | 106 |
| 3 | 200 | 1 | 07/06/2006 | 140 | 3.6 | 103✓ |
| 4 | 200 | 4 | 07/13/2006 | 140 | 4.02 | 103 |
| 5 | 200 | 4 | 07/13/2006 | 140 | 4 | 103 |
| 6 | 200 | 5 | 07/21/2006 | 142 | 4.57 | 104 |
| ……清单的部分内容未显示…… |  |  |  |  |  |  |

当 BY 语句中的关键字段*足以*构成主键时，观测必然会被充分重新排序，从而使 NODUPREC 选项按我们希望的方式工作。在前一个示例中，如果 BY 语句还包含 VISIT 和 LABDT 以及 SUBJECT，那么重复记录就会被删除。

```text
NOTE: There were 169 observations read from the data set
      ADVRPT.LAB_CHEMISTRY.
NOTE: 3 duplicate observations were deleted.
NOTE: The data set WORK.LAB_CHEM has 166 observations and 6
      variables.
```

事实上，日志显示，尽管此示例（4.1.1a）中确实删除了三个观测，但被勾选的两行（观测 1 和 3）也是重复的，且两者都未被删除。

当你没有主键，或者不知道哪些变量将构成主键时，保证删除重复观测的唯一方法是在 BY 语句中列出数据集的所有变量。所有变量列表可以使用 _ALL_ 列表缩写来简写。

```sas
by _all_;
```

在实践中，对于重复观测问题，这往往是一种非常低效的解决方案。虽然低效，但如果你的数据集大小使得额外的排序资源不会对你造成很大影响，那么使用 _ALL_ 至少可行，并且能在使用 NODUPREC 时完成我们需要它做的事。一般来说，虽然并非万无一失，但将派生变量（例如方差或标准差）与可能的主键变量一起包含进来，通常足以成功地重新排序观测，使重复观测位于相邻行。

NODUPKEY 选项没有这个问题，因为在检查重复值时只评估关键字段。

### 更多信息

第 2.9.5 节使用 Hash 对象来消除重复观测。第 4.1.6 节在 NOEQUALS 选项的上下文中也讨论了 NODUPREC 选项。

### 4.1.2 DUPOUT= 选项

使用 NODUPREC 或 NODUPKEY 选项时，日志会注明何时删除观测；但是，哪些观测被删除并不明显。如果你希望能够看到这些观测，可以使用 DUPOUT= 选项将被消除的观测保存到一个单独的数据表中。

在下面的示例中，BY 语句现在包含了足够的关键字段，可以重新排序上一节提到的有问题的观测。被删除的观测会写入一个单独的数据集（WORK.REMOVEDOBS）。

```sas
title1 '4.1.2 NODUPLICATES and DUPOUT= in PROC SORT';
proc sort data=advrpt.lab_chemistry
          out=lab_chem
          dupout=RemovedObs
          noduprec;
    by subject visit labdt;
run;
proc print data=removedobs(obs=10);
run;
```

由于我们使用足够的关键字段来重新排序上一节提到的有问题的观测，该重复观测现在也被删除了。❶

**4.1.2 PROC SORT 中的 NODUPLICATES 和 DUPOUT=**

| Obs | SUBJECT | VISIT | LABDT | SODIUM | POTASSIUM | CHLORIDE |
|---:|---:|---:|---|---:|---:|---:|
| 1 | 200 | 1 | 07/06/2006 | 140 | 3.6 | 103 ❶ |
| 2 | 200 | 9 | 09/13/2006 | 139 | 4.06 | 103 |
| 3 | 201 | 2 | 07/14/2006 | 140 | 4.15 | 101 |
| 4 | 202 | 6 | 07/29/2006 | 139 | 5.68 | 96 |

尽管我们检测到了这些重复观测，但如果不使用我们已知的足够关键字段，就无法保证这些就是所有重复观测。

## 针对 PTSD 的 EMDR 治疗

眼动脱敏与再加工（EMDR）是一种心理治疗方法，最初旨在减轻与创伤性记忆相关的痛苦。EMDR 治疗促进对创伤性记忆和其他不良生活经历的获取与加工，使其达到适应性解决。

### EMDR 如何工作？

EMDR 治疗采用结构化的八阶段方法，包括：

- 病史采集与治疗计划
- 准备
- 评估
- 脱敏
- 植入
- 身体扫描
- 结束
- 再评估

在脱敏阶段，来访者专注于创伤性记忆，同时经历双侧刺激（通常是眼动）。这被认为有助于大脑以类似快速眼动睡眠期间发生的方式加工记忆。

> “EMDR 并不会抹去记忆，而是改变记忆在大脑中的存储方式，降低其情绪负荷。”

### EMDR 的有效性

EMDR 被 WHO、APA 和 SAMHSA 认可为治疗 PTSD 的有效方法。研究表明，许多患者在 6–12 次治疗后有显著的症状减轻。

```sas
proc sort data=advrpt.clinicnames(keep=region)
          out=regions2
          sortseq=linguistic ❶ (numeric_collation=on) ❷
          nodupkey;
   by region;
run;
```

## 区分大小写的重排序

取决于排序序列，小写字母要么全部排在大写字母之前，要么全部排在其后。本节示例从 ADVRPT.DEMOG 数据集中取出前五个姓名，并将它们复制为全大写和全小写形式，以及原始混合大小写形式。

```sas
proc sort data=names
          out=namesE
          sortseq=ebcdic;
   by lname;
run;
title3 'EBCDIC Sequence';
proc print data=namesE;
run;
```

**EBCDIC 序列**

| Obs | lname |
| --- | --- |
| 1 | adams |
| 2 | adamson |
| 3 | alexander |
| 4 | antler |
| 5 | atwood |
| 6 | Adams |
| 7 | Adamson |
| 8 | Alexander |
| 9 | Antler |
| 10 | Atwood |
| 11 | ADAMS |
| 12 | ADAMSON |
| 13 | ALEXANDER |
| 14 | ANTLER |
| 15 | ATWOOD |

**ASCII 序列**

| Obs | lname |
| --- | --- |
| 1 | ADAMS |
| 2 | ADAMSON |
| 3 | ALEXANDER |
| 4 | ANTLER |
| 5 | ATWOOD |
| 6 | Adams |
| 7 | Adamson |
| 8 | Alexander |
| 9 | Antler |
| 10 | Atwood |
| 11 | adams |
| 12 | adamson |
| 13 | alexander |
| 14 | antler |
| 15 | atwood |

并排比较显示了这两种主要排序序列之间的差异（生成 ASCII 序列的代码在示例程序中）。

```sas
proc sort data=names
          out=namesC
          sortseq=linguistic (case_first=upper); ❸
   by lname;
run;
```

**Case_First=Upper**

| Obs | lname |
| --- | --- |
| 1 | ADAMS |
| 2 | Adams |
| 3 | adams |
| 4 | ADAMSON |
| 5 | Adamson |
| 6 | adamson |
| 7 | ALEXANDER |
| 8 | Alexander |
| 9 | alexander |
| 10 | ANTLER |
| 11 | Antler |
| 12 | antler |
| 13 | ATWOOD |
| 14 | Atwood |
| 15 | atwood |

我们可以使用关键字限定符进一步细化排序。

CASE_FIRST=UPPER ❸ 限定符使大写优先于小写。但请注意，该顺序仍与同样优先处理大写字母的 ASCII 不同。这里的敏感性体现在单词内部，而不是在整个单词列表范围内。CASE_FIRST 关键字限定符也可以取值 LOWER。

