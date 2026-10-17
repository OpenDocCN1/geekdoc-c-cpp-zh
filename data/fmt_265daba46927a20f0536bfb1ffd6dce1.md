
在下面的示例中，输出使用了标题和脚注。

```sas
title1 'Heart Rates for Patients with;
title2 'Participation in Exercise Therapy';
footnote1 'Data from Treadmill Tests';
footnote3 '1st Quarter Admissions';
proc print data=cert.therapy;
var swimjog aerclass;
run;
```

# 输出 6.4 带标题的 PROC PRINT 输出

| ActLevel | Age | Height | Weight | Fee |
|---|---|---|---|---|
| HIGH | 34 | 66 | 152 | 124.80 |
| | 44 | 66 | 140 | 149.75 |
| | 40 | 69 | 163 | 124.80 |
| | 41 | 67 | 141 | 149.75 |
| HIGH | | | | 549.10 |

## SAS 系统

| | | | | |
|---|---|---|---|---|
| LOW | 31 | 61 | 123 | 149.75 |
| | 51 | 71 | 158 | 124.80 |
| | 34 | 73 | 154 | 124.80 |
| | 49 | 64 | 172 | 124.80 |
| | 60 | 71 | 191 | 149.75 |
| LOW | | | | 673.90 |

## SAS 系统

| ActLevel | Age | Height | Weight | Fee |
|---|---|---|---|---|
| MOD | 43 | 63 | 137 | 149.75 |
| | 32 | 67 | 151 | 149.75 |
| | 35 | 70 | 173 | 149.75 |
| | 47 | 72 | 173 | 124.80 |
| | 43 | 65 | 123 | 124.80 |
| | 54 | 71 | 183 | 149.75 |
| MOD | | | | 848.60 2071.60 |

# 输出 6.5 带脚注的 PROC PRINT 输出

| ActLevel | Age | Height | Weight | Fee |
|---|---|---|---|---|
| HIGH | 34 | 66 | 152 | 124.80 |
| | 44 | 66 | 140 | 149.75 |
| | 40 | 69 | 163 | 124.80 |
| | 41 | 67 | 141 | 149.75 |
| HIGH | | | | 549.10 |

# 输出 6.6 带标题和脚注的 PROC PRINT 输出

| ActLevel | Age | Height | Weight | Fee |
|---|---|---|---|---|
| LOW | 31 | 61 | 123 | 149.75 |
| | 51 | 71 | 158 | 124.80 |
| | 34 | 73 | 154 | 124.80 |
| | 49 | 64 | 172 | 124.80 |
| | 60 | 71 | 191 | 149.75 |
| LOW | | | | 673.90 |

# 输出 6.7 带标题和脚注的 PROC PRINT 输出

| ActLevel | Age | Height | Weight | Fee |
|---|---|---|---|---|
| MOD | 43 | 63 | 137 | 149.75 |
| | 32 | 67 | 151 | 149.75 |
| | 35 | 70 | 173 | 149.75 |
| | 47 | 72 | 173 | 124.80 |
| | 43 | 65 | 123 | 124.80 |
| | 54 | 71 | 183 | 149.75 |
| MOD | | | | 848.60 2071.60 |

# 在过程输出中指定标题和脚注 99

输出 6.8 带有标题 1 和标题 3 的 Cert. Therapy PROC PRINT 输出（部分输出）

# 参与运动治疗患者的心心率

| Obs | Swim | WalkJogRun | AerClass |
|---|---|---|---|
| 1 | 14 | 78 | 56 |
| 2 | 19 | 109 | 32 |
| ... | ... | ... | ... |
| 20 | 53 | 65 | 63 |
| 21 | 68 | 49 | 60 |
| 22 | 41 | 70 | 78 |
| 23 | 58 | 44 | 82 |
| 24 | 47 | 57 | 93 |

来自跑步机测试的数据

第一季度入院

输出 6.9 带有标题 1 和标题 2 的 Cert. Therapy PROC PRINT 输出（部分输出）

# 3 月份报告患者的心率

| Obs | AerClass | WalkJogRun | Swim |
|---|---|---|---|
| 1 JAN2012 | 56 | 78 | 14 |
| 2 FEB2012 | 32 | 109 | 19 |
| ... | ... | ... | ... |
| 20 AUG2013 | 63 | 65 | 53 |
| 21 SEP2013 | 60 | 49 | 68 |
| 22 OCT2013 | 78 | 70 | 41 |
| 23 NOV2013 | 82 | 44 | 58 |
| 24 DEC2013 | 93 | 57 | 47 |

来自跑步机测试的数据

第一季度入院

要取消所有之前的标题或脚注，请指定 `NULL TITLE` 或 `FOOTNOTE` 语句。`TITLE` 或 `FOOTNOTE` 语句不包含任何数字或文本，并将取消所有生效的脚注和标题。

```sas
title;
/* #1 */
footnote 'Data from Treadmill Tests';
/* #2 */
footnote '1st Quarter Admissions';
proc print data=cert.stress;
var restrhr maxhr rech;
where tolerance='1';
run;
footnote;
/* #3 */
proc means data=cert.stress;
```

# 100 第 6 章 • 创建报告

```sas
where tolerance='I';

var restar maxhr;

run;
```

- 1. 指定 `TITLE1` 语句会取消所有之前的标题，并取消 SAS 系统的默认标题。PRINT 过程和 MEANS 过程在输出中不包含任何标题。
- 2. 在 PRINT 过程之前指定 `FOOTNOTE1` 和 `FOOTNOTE3` 语句，结果将出现在 PROC PRINT 输出中。
- 3. 指定空 `FOOTNOTE` 语句会取消之前定义的生效脚注。

输出 6.10 带有脚注且无标题的 PROC PRINT 输出

| Obs | RestHR | MaxHR | ReCHR |
|---|---|---|---|
| 2 | 68 | 171 | 133 |
| 3 | 78 | 177 | 139 |
| 8 | 70 | 167 | 122 |
| 11 | 65 | 181 | 141 |
| 14 | 74 | 152 | 113 |
| 15 | 75 | 158 | 108 |
| 20 | 78 | 189 | 138 |

![](img/4d880eb3a583bf2815ab53a244818659_111_0.png)

输出 6.11 无脚注且无标题的 PROC MEANS 输出

| Variable | N | Mean | Std Dev | Minimum | Maximum |
|---|---|---|---|---|---|
| RestHR MaxHR | 7 | 72.5142857 | 5.0284903 | 65.000000 | 78.000000 |
| 7 | 170.7142857 | 12.9449383 | 162.000000 | 189.000000 |

## 分配描述性标签

# 为变量临时分配标签

为了通过标记列来增强您的 PROC PRINT：

- 使用 `LABEL` 语句为变量分配描述性标签。
- 在 PROC PRINT 语句中使用 `LABEL` 选项来指定显示这些标签。

语法：`LABEL` 语句：

```sas
LABEL variable1='label1'
      variable2='label2'
      ;
```

标签长度最高可达 256 个字符。用引号将标签括起来。

提示：`LABEL` 语句仅适用于它所出现的 PROC 步骤。

# 示例：在 PROC PRINT 语句中使用 LABEL 选项

在下方的 PROC PRINT 步骤中，变量名 `WalkJogRun` 显示为标签 `Walk/Jog/Run`。请注意 `LABEL` 选项位于 PROC PRINT 语句中。

```sas
proc print data=cert.therapy label;
label walkjogrun='Walk/Jog/Run';
run;
```

示例 6.2 带有标签的 AerClass PROC PRINT 输出（部分输出）

| Date | AerClass | Walk/Jog/Run | Swim |
|---|---|---|---|
| 1 JAN2012 | 56 | 78 | 14 |
| 2 FEB2012 | 32 | 109 | 19 |
| . | . | . | . |
| 20 AUG2013 | 63 | 65 | 53 |
| 21 SEP2013 | 60 | 49 | 68 |
| 22 OCT2013 | 78 | 70 | 41 |
| 23 NOV2013 | 82 | 44 | 58 |
| 24 DEC2013 | 93 | 57 | 47 |

如果您在 PROC PRINT 语句中省略 `LABEL` 选项，PROC PRINT 将使用列名 `walkjogrun`，即使您指定了值。

# 示例：使用多个 LABEL 语句

以下示例说明了多个 `LABEL` 语句的使用。

```sas
proc print data=cert.admit label;
var age height;
label age='Age of Patient';
label height='Height in Inches';
run;
```

- 1 在 PROC PRINT 语句中使用 `LABEL` 选项。如果在 PROC PRINT 语句中省略 `LABEL` 选项，PROC PRINT 将使用变量名。
- 2 可以在分开的 `LABEL` 语句中分配标签。在此示例中，将变量 `Age` 标记为 Patients。
- 3 这是示例中的第二个 `LABEL` 语句。将变量 `Height` 标记为 Inches。

**输出 6.13 带有多个 LABEL 语句的 PROC PRINT 输出（部分输出）**

| Obs Age of Patient | Height in Inches |
|---|---|
| 1 | 27 | 72 |
| 2 | 34 | 66 |
| ...more observations | | |
| 17 | 43 | 65 |
| 18 | 25 | 75 |
| 19 | 22 | 63 |
| 20 | 41 | 67 |
| 21 | 54 | 71 |

# 示例：使用单个语句分配多个标签

您也可以使用单个语句分配多个标签。

```sas
/* #1 */
proc print data=cert.admit label;
var level height weight;
label actlevel='Activity Level'
      height='Height in Inches'
      weight='Pounds';
run;
```

- 1 在 PROC PRINT 语句中使用 `LABEL` 选项。
- 2 `LABEL` 语句为不同的变量分配标签。注意，在结束语句之前，您不需要分号。

**输出 6.14 带有 LABEL 语句的 PROC PRINT 输出（部分输出）**

| Obs Activity Level | Height in Inches | Pounds |
|---|---|---|
| 1 | 72 | 168 |
| 2 | 75 | 177 |
| 3 | 63 | 179 |
| 4 | 67 | 181 |
| 5 | 66 | 182 |
| 6 | 69 | 183 |
| 7 | 71 | 184 |
| 8 | 72 | 185 |
| 9 | 73 | 186 |
| 10 | 74 | 187 |
| 11 | 75 | 188 |
| 12 | 76 | 189 |
| 13 | 77 | 190 |
| 14 | 78 | 191 |
| 15 | 79 | 192 |
| 16 | 80 | 193 |
| 17 | 65 | 194 |
| 18 | 65 | 195 |
| 19 | 63 | 196 |
| 20 | 67 | 197 |
| 21 | 71 | 198 |

# 永久分配的标签

当在 PROC 步骤中使用 `LABEL` 语句时，标签仅适用于该步骤的输出。然而，在 DATA 步骤中，标签可以随数据集保存。

```sas
data cert.stress;
set cert.stress;
label tolerance='Tolerance Rate';
run;
```

标签被写入数据集，并可以被后续过程重复使用。例如，下面的 DATA 步骤创建了永久标签。

输出 6.15 使用永久标签

| Obs | Departure Date | Bordered |
|---|---|---|
| 1 | 042012 | 146 |
| 2 | 072012 | 155 |
| 3 | 042012 | 146 |
| 4 | 072012 | 155 |

注意 PRINT 语句仍然需要 `LABEL` 选项来显示永久标签。有关分配标签的更多信息，请参见第 100 页的“分配描述性标签”。

# Quiz

为每个问题选择最佳答案。在附录中检查您的答案。

1. 哪个 PRINT 步骤创建了显示标签的示例输出？提示：首先显示 CONTENTS 输出以帮助您。

| Variable | Type | Len | Format |
|---|---|---|---|
| 6 Boarded | Num | 8 | |
| 2 Date | Num | 8 | DATE7 |
| 3 Depart | Num | 8 | TIME5 |
| 8 Deplaned | Num | 8 | |
| 5 Dest | Char | 3 | |
| 1 Flight | Char | 3 | |
| 4 Org | Char | 3 | |
| 9 Revenue | Num | 8 | |
| 7 Transferred | Num | 8 | |

| Date | On | Changed | Flight |
|---|---|---|---|
| 042012 | 232 | 18 | 219 |
| 052012 | 160 | 4 | 219 |
| 062012 | 163 | 14 | 219 |
| 072012 | 241 | 9 | 219 |
| 082012 | 183 | 11 | 219 |
| 092012 | 211 | 18 | 219 |
| 102012 | 167 | 7 | 219 |

a. `proc print data=cert.lagaguardia noobs; var on changed flight; where on>160; run;`

b. `proc print data=cert.lagaguardia; var date on changed flight; where changed>3; run;`

c. `proc print data=cert.lagaguardia label; id date; var boarded transferred='On'; label boarded='Changed'; where flight='219'; run;`

d. `proc print data=cert.lagaguardia noobs; id date; var date on changed flight; where flight='219'; run;`

2. 如果标签未存储在数据，以下哪个 PROC PRINT 步骤是正确的？

a. `proc print data=cert.totals label; label region='Region 8 Yearly Totals'; run;`

b. `proc print data=cert.totals; label region8='Region 8 Yearly Totals' run;`

c. `proc print data=cert.totals noobs; run;`

d. `proc print data cert.totals label; run;`

3. 下面哪条语句可以从一个数据集中仅选择 sort style 值为 RANCH、SPLIT 或 TWOSWRORY 的观测值？

- a. `where style='RANCH' or 'SPLIT' or 'TWOSWRORY'`
- b. `where style in 'RANCH' or 'SPLIT' or 'TWOSWRORY'`

# 第 105 章节测试

```sas
run;
```
