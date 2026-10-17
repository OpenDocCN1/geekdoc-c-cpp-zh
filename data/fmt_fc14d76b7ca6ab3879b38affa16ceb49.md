
输出 6.2 和输出 6.3 显示了步骤 6.4 的结果。你可以看到，我们人口中女性多于男性，而且我们的大多数受益人是白人。

## 输出 6.2：2010 年数据中的性别比例

### 2010 年数据中性别的频率

#### FREQ 过程

| 性别 | 频率 | 百比 | 累积频率 | 累计百分比 |
| --- | --- | --- | --- | --- |
| 男性 | 29627 | 44.09 | 29627 | 44.09 |
| 女性 | 37571 | 55.91 | 67198 | 100.00 |

## 输出 6.3：2010 年数据中的种族比例

### 2010 年数据中种族的频率

#### FREQ 过程

| 种族 | 频率 | 百比 | 累积频率 | 累计百分比 |
| --- | --- | --- | --- | --- |
| 白人 | 56409 | 83.94 | 56409 | 83.94 |
| 黑人 | 6652 | 9.90 | 63061 | 93.84 |
| 其他 | 2663 | 3.96 | 65724 | 97.81 |
| 西斯裔 | 1474 | 2.19 | 67198 | 100.00 |

## 年龄组

接下来，让我们定义并分组受益人所属的年龄类别。为了说明目的，假设我们希望计算每位受益人在参考年份开始时（在我们的案例中为 2010 年 1 月 1 日）的年龄。在步骤 6.5 中，我们使用 `ENR.CONTENTR_2010_FNL` 数据计算此变量并将其命名为 `STUDY_AGE`。此外，假设希望创建一个变量来描述受益人属于四个年龄组之一：65 岁、65-74 岁、75-84 岁、85-95 岁及以上。同样在步骤 6.5 中，我们创建了一个变量 `AGE_CATS`，根据 `STUDY_AGE` 的值对受益人进行分组。请注意，我们使用 `PROC FORMAT` 创建了一个格式 `AGE_CATS_FMT`，并将其应用于下方 `AGE_CATS` 的显示。

```sas
* STEP 6.5: 截至 2010 年 1 月 1 日创建 STUDY_AGE 类别 */

/* 步骤 6.5：将 STUDY_AGE 分组到 AGE_CATS 中 */

proc format;

value age_cats_fmt

  0='小于 65 岁'

  1='65-74 岁'

  2='75-84 岁'

  3='85-94 岁'

  4='95 岁及以上';

run;

data age_cats;

  set enr.contr_2010_fnl;

  study_age = floor((2010 - year(dob)) + (month(dob)-1)/12);

  select;

    if study_age < 65 then age_cats = 0;

    else if 65 <= study_age <= 74 then age_cats = 1;

    else if 75 <= study_age <= 84 then age_cats = 2;

    else if 85 <= study_age <= 94 then age_cats = 3;

    else if study_age >= 95 then age_cats = 4;

  end;

  format age_cats $age_cats_fmt.;

run;
```

最后，在步骤 6.6 中，输出 6.4 显示了步骤 6.5 的结果（使用 `ENR.CONTENT_2010_FNL` 交叉制表计算 2010 年 1 月 1 日的 `AGE_CATS` 分组）。你可以通过输出 6.4 检查 `AGE_CATS` 的计算是否准确，并根据需要移除 `where` 子句。此处在步骤 6.6 中，输出 6.4 显示了步骤 6.5 的结果。你可以通过输出 6.4 检查 `AGE_CATS` 的计算是否准确，并根据需要移除 `where` 子句。通过频率分布查看所有受益人的分布。

## 第 6 章：人数数据

```sas
/* 步骤 6.6: 显示 2010 年数据中的年龄特征 */

ods html file="C:\Users\mgillingham\Desktop\SAS Book\FINAL_DATA_ODS_OUTPUT\mgillingham_fig6_6_AGE.html"

  image_dpi=300 style=GrayscalePrinter;

ods graphics on;

title "2010 年数据中年龄与年龄组的交叉制表";

proc freq data=enr.contr_2010_fnl(where=65<=study_age<=70);

  tables study_age * age_cats;

  format age_cats $age_cats_fmt.;

run;

ods html close;
```

这里是频率分布的输出。我们可以看到 `AGE_CATS` 的计算是准确。

## 输出 6.4：年龄组

### 2010 年数据中年龄与年龄组的交叉制表

#### FREQ 过程

| 年龄 | 年龄组 | 频率 | 百比 | 累积频率 | 累计百分比 |
| --- | --- | --- | --- | --- | --- |
| 65 | 0 | 514 | 10.00 | 514 | 10.00 |
| 66 | 0 | 522 | 10.14 | 1036 | 20.14 |
| 67 | 0 | 535 | 10.33 | 1571 | 30.47 |
| 68 | 0 | 568 | 10.93 | 2139 | 41.40 |
| 69 | 0 | 580 | 11.16 | 2719 | 52.56 |
| 70 | 0 | 581 | 11.14 | 3300 | 63.60 |
| 65 | 1 | 590 | 11.43 | 3890 | 75.13 |
| 66 | 1 | 602 | 11.60 | 4492 | 86.73 |
| 67 | 1 | 615 | 11.69 | 5107 | 98.42 |
| 68 | 1 | 618 | 11.70 | 5725 | 100.00 |

## 地理特征

显示地理特征的一些有效方法有哪些？显然，按州分组可能太宽了。在某些情况下，按邮政编码查看可能太细了。我们使用医院转诊区域（HRR）、医院服务区（HSA）或大统计区（MSA）。

## 第 6 章：处理入保数据 65

在步骤 6.10 中，我们将县名和州名合并到入保数据中。首先，对 SSA（社会安全局）提供的 `ENR.CONTENTR_2010 FNL` 进行排序，然后对 SSA 的 `ENR.CONTENTR_2010 FNL` 和 `SRC.MSABEA_SSA` 数据集进行部分合并，并保留入保数据集中所有数据。通过这种方式，我们为在 2010 年 12 个月内连续参加 Medicare FFS（服务付费）的受益人文件中的每个受益人分配了州名和县名。

```sas
/* 步骤 6.10：对连续入保数据进行排序并与 MSABEA 文件合并 */

proc sort data=enr.contentr_2010_fnl; by ssa; run;

data enr.contentr_2010_fnl;

  merge enr.contentr_2010_fnl(in=a) src.msabea_ssa(in=b);

  if a;

run;
```

最后，在步骤 6.11 中，我们简单打印 `ENR.CONTENTR_2010_FNL` 数据集中新添加的州名和县名变量（显示前 10 条记录）。

```sas
/* 步骤 6.11：在 2010 入保数据中显示 SSA 州和县名 */

ods html file="C:\Users\mgillingham\Desktop\SASBook\FINAL_DATAVOD_OUTPUT\mgillingham_fig6_11.html"

image_dpi=300 style=GrayscalePrinter;

ods graphics on / imagefmt=png;

title "2010 年数据中的 SSA 州和县名";

proc print data=enr.contentr_2010_fnl(obs=10);

  var bene_id ssa state county;

run;

ods html close;
```

## 使用 Medicare 行政数据进行 SAS 编程

我们使用 `ODS` 显示步骤 6.11 输出的前 10 条记录，如下输出 6.5 所示。

## 输出 6.5：SSA 州和县名

### 2010 年数据中的 SSA 州和县名

| Obs | BENE_ID | ssa | state | county |
|---|---|---|---|---|
| 1 | 33B522FC84AC4 | 01000 | AL | AUTUGA |
| 2 | 3BA6CAAE365744 | 01000 | AL | AUTUGA |
| 3 | 401FA84E59107B | 01000 | AL | AUTUGA |
| 4 | 52DA53C34BC51E | 01000 | AL | AUTUGA |
| 5 | 57ED3C7629AO0D | 01000 | AL | AUTUGA |
| 6 | 5F2E2ABA48D093 | 01000 | AL | AUTUGA |
| 7 | 69C964585037A2 | 01000 | AL | AUTUGA |
| 8 | 9BED49598074EC | 01000 | AL | AUTUGA |
| 9 | B5C863CDB0D54 | 01000 | AL | AUTUGA |
| 10 | FE68EC62A83519 | 01000 | AL | AUTUGA |

## 算法：创建 2010 年数据的最终文件

为了后续的编程，我们将入保信息合并到 `ENR.CONTENT_2010_FNL`。在步骤 6.12 中，我们根据受益人标识对 `ENR.CONTENT_2010_FNL` 进行排序。

```sas
/* 创建最终的连续入保数据 */

proc sort data=enr.contentr_2010_fnl; 

by bene_id;

run;
```
