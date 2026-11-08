
## PCTN 和 PCTSUM 选项

PCTN 和 PCTSUM 选项用于请求基于尖括号指定分母的百分比计算。PCTN 基于计数（N）计算百分比，而 PCTSUM 基于分析变量的总计计算百分比。

以下示例请求基于计数的百分比。此步骤不需要分析变量（VAR 语句），因为百分比基于计数，且未请求其他统计量。

```sas
proc tabulate data=advrpt.demog;
   class race edu;
   table (race all)*pctn<edu>='%' ❶,
         edu; ❷
run;
```

- ❶ 在 RACE 的每个值内，计算 EDU 每个值的观测百分比。由于 PCTN 嵌套在 RACE 内，分母 <EDU> 是该 RACE 值的总计数。

**8.1.2a 使用尖括号的 Proc Tabulate 百分比**

**受教育年限**

| 种族 |  | 10 | 12 | 13 | 14 | 15 | 16 | 17 | 18 |
|---|---|---|---|---|---|---|---|---|---|
| **1** | **%** | 26.19 | 38.10 | 9.52 | | 11.90 | 4.76 | 4.76 | 4.76 |
| **2** | **%** | | 17.65 | | | | 35.29 | 47.06 | |
| **3** | **%** | | | | 75.00 | 25.00 | | | |
| **4** | **%** | | | | 100.00 | | | | |
| **5** | **%** | | | | | | 50.00 | | 50.00 |
| **全部** | **%** | 14.67 | 25.33 | 5.33 | 13.33 | 9.33 | 13.33 | 13.33 | 5.33 |

- ❷ 列维度基于分类变量 EDU。没有分析变量；因此，计数被转换为百分比。

尽管在此示例中分母的确定很直接，但通常会更复杂。该过程的文档和 Haworth (1999) 给出了更复杂的示例。

## 百分比生成统计量

有时使用尖括号可能难以获得正确的分母。幸运的是，还有几种百分比生成统计量。对于这些统计量中的每一个，分母（可以基于报表、页、行或列）都是预先确定的。

| 百分比适用于： | 百分比频数（N） | 百分比总计（SUM） |
|---|---|---|
| 报表 | reppctn | reppctsum |
| 页 | pagepctn | pagepctsum |
| 列 | colpctn | colpctsum |
| 行 | rowpctn | rowpctsum |

在以下示例中，百分比针对列而不是行。显示的百分比同时使用 N（COLPCTN）和 WT 总计（COLPCTSUM）计算。

```sas
proc tabulate data=advrpt.demog;
   class race;
   var wt;
   table race all,
         wt*(n colpctn mean colpctsum);
run;
```

**8.1.2b Proc Tabulate 列百分比**

**体重（磅）**

| 种族 | N | ColPctN | Mean | ColPctSum |
|---|---:|---:|---:|---:|
| 1 | 42 | 55.26 | 176.14 | 60.00 |
| 2 | 18 | 23.68 | 166.33 | 24.28 |
| 3 | 8 | 10.53 | 112.00 | 7.27 |
| 4 | 4 | 5.26 | 113.50 | 3.68 |
| 5 | 4 | 5.26 | 147.00 | 4.77 |
| 全部 | 76 | 100.00 | 162.24 | 100.00 |

以下示例汇总调查数据。这里的响应变量（RESP）取值为 0 或 1（否或是）。

```sas
proc tabulate data=survey;
   class question;
   var resp;
   table question,
         resp='responses'*(n='total responders' *f= comma7. ❻
         sum='total yes' *f= comma7. ❻
         pctsum='response rate for this question'*f=5.1
         pctn='rate of Yes over whole survey' *f= 5.
         mean='mean Q resp' * f=percent7.1
         ) / rts=40;
run;
```

**8.1.2c 使用 PCTSUM 和 PCTN 的 Proc Tabulate 百分比**

**响应**

| 问题 | 总响应者 | 总“是” | 此问题的响应率 | 整个调查中“是”的比率 | Q 响应均值 |
|---|---:|---:|---:|---:|---:|
| 1 | 10 | 7 | 26.9 | 22 | 70.0% |
| 2 | 8 | 4 | 15.4 | 18 | 50.0% |
| 3 | 9 | 6 | 23.1 | 20 | 66.7% |
| 4 | 7 | 2 | 7.7 | 16 | 28.6% |
| 5 | 11 | 7 | 26.9 | 24 | 63.6% |

请注意，与第一个示例不同，PCTSUM 和 PCTN 的分母未指定。在此 TABULATE 步骤中，假定的分母将跨越整个报表。

- ❻ COMMA7. 格式已应用于这两个统计量。对于 LISTING 目标，在形成列宽时将考虑格式的宽度。对于其他目标（例如此处显示的 PDF（style=minimal）），格式宽度仅用于数字本身的显示，不会影响列宽。

## 另请参阅

在 SAS 论坛帖子 [http://communities.sas.com/message/42094](http://communities.sas.com/message/42094) 中，使用替代编码结构讨论了该调查示例。

## 8.1.3 在 PROC TABULATE 中使用 STYLE= 选项

TABULATE 过程是接受 STYLE 覆盖选项的三个过程之一。它在 TABULATE 中的用法与在 PRINT（参见第 8.5.2 节）和 REPORT（参见第 8.4.6 节）过程中的用法相似，但不完全相同。此选项允许用户通过覆盖 ODS 样式属性来控制表格各个方面的显示方式。

样式可以应用于表格内的多个区域，从一般的整体属性到特定单元格的属性。这些区域包括：

| # | 表格区域 | STYLE= 用于 |
|---|---|---|
| 1 | 框单元格 | BOX= 选项 |
| 2 | 分类标题 | CLASS 语句 |
| 3 | 分类水平 | CLASSLEV 语句 |
| 4 | 分析变量标题 | VAR 语句 |
| 5 | 统计量标题（关键字） | KEYWORD 语句 |
| 6 | 值单元格 | PROC 和 TABLE 语句 |
| 7 | 单个单元格 | PROC 和 TABLE 语句 |

![](img/4b16455363806a3241267bf9f49ba5d1_293_0.png)

左侧是一个相当典型的 TABULATE 表格。表格上的标注数字与上方的标注说明相对应。

以下代码用于生成此示例表格。请注意，RTS= 选项仅适用于 LISTING 目标。此处未显示 ODS 语句，但它们包含在本书的示例代码中。参见 http://support.sas.com/authors。

```sas
proc tabulate data=advrpt.demog;
    class race;
    var ht wt;
    table race,
        (ht wt)*(n*f=2. min*f=4. median*f=7.1 max*f=4.)
        /rts=6;
run;
```

**8.1.3b 使用 Journal 样式的 TABULATE**
*各种 STYLE= 属性已更改*

| 种族 | 身高（英寸）N | 身高（英寸）Min | 身高（英寸）Median | 身高（英寸）Max | 体重（磅）N | 体重（磅）Min | 体重（磅）Median | 体重（磅）Max |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 42 | 62 | 69.0 | 74 | 42 | 109 | 177.0 | 215 |
| 2 | 18 | 62 | 67.0 | 72 | 18 | 98 | 158.0 | 240 |
| 3 | 8 | 64 | 64.0 | 68 | 8 | 105 | 105.0 | 133 |
| 4 | 4 | 64 | 64.5 | 65 | 4 | 112 | 113.5 | 115 |
| 5 | 4 | 65 | 66.5 | 68 | 4 | 147 | 147.0 | 147 |

- 4. 在 VAR 语句上，STYLE= 选项更改与变量标题关联的属性。
- 5. 通过将 N 统计量的标签加粗来调整它。请注意，其他统计量的标题保持不变。
- 6. 仅与 N 统计量关联的单元格属性被加粗。

## 8.1.4 使用 CLASSDATA 选项控制表格内容

TABULATE 过程生成的表格内容在很大程度上受数据中分类变量水平的影响。通过使用 CLASSDATA 选项，我们可以指定一个辅助数据集，以进一步影响表格外观。

对于本节中的示例，数据集 SYMPLS 仅包含变量 SYMP，该变量仅取值为 ‘00’、‘01’ 和 ‘02’。但应注意，在要分析的数据（ADVRPT.DEMOG）中，变量 SYMP 从未取值为 ‘00’，除此之外范围为 ‘01’ 到 ‘10’。

### 将 CLASSDATA 与 EXCLUSIVE 选项一起使用

CLASSDATA= 选项和 EXCLUSIVE 选项在 TABULATE 步骤中的行为和应用与在 MEANS 和 SUMMARY 过程中非常相似（参见第 7.9 节）。CLASSDATA= 选项指定一个包含分类变量水平的数据集。这些水平可能存在于分析数据中，也可能不存在，并可用于强制将水平加入表格或将水平从表格中排除。

当 CLASSDATA= 选项与 EXCLUSIVE 选项一起使用时（如下例所示），仅显示 CLASSDATA= 数据集中的那些水平（包括分析数据集中不存在的任何水平）。

```sas
proc tabulate data=advrpt.demog;
             classdata=symplevels exclusive;
  class symp;
  var ht wt;
  table symp,
        (ht wt)*(n*f=2. min*f=4. median*f=7.1 max*f=4.);
run;
```

