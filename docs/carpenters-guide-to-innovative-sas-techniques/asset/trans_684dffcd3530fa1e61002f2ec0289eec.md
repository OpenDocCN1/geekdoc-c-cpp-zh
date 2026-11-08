

在计算块（compute block）内对各语句进行求值的过程中，LINE 语句实际上会被移到步（step）的末尾。上面的计算块实质上就变成了这里所示的代码块。这种行为和我们在 DATA 步中看到的任何行为都完全不同。

```sas
compute after sex; ①
    if wt.n ge 35 then do; ②
    end;
    else;
    line 'Overall mean weight is: ' meanwt 5.1; ③
    line 'Patient Count Below 35'; ④
endcomp;
```

因此，我们不能有条件地执行 LINE 语句；但我们可以有条件地构建将由 LINE 语句显示的内容。

```sas
compute after sex;
    if wt.n ge 35 then do;
        text='Overall mean weight is: '||put(meanwt,5.1); ⑤
    end;
    else text = 'Patient Count Below 35'; ⑤
        line text $31.; ⑥
endcomp;
```

- ⑤ 这里我们创建一个临时变量（TEXT），它将承载要显示的目标值。
- ⑥ 然后执行 LINE 语句。

## 另请参阅

SAS 示例 #37763 中讨论了 PROC REPORT 中 LINE 语句的条件执行，参见 http://support.sas.com/kb/37/763.html。

### 8.4.10 LINE 语句的条件准备

| 患者性别 | 种族 | 患者数量 | 平均体重 |
|---|---:|---:|---:|
| F | 1 | 14 | 159.0 |
| F | 2 | 10 | 148.6 |
| F | 3 | 3 | 105.0 |
| F | 4 | 4 | 113.5 |
|  |  | **患者数量低于 35** |  |
| M | 1 | 28 | 184.7 |
| M | 2 | 8 | 188.5 |
| M | 3 | 5 | 116.2 |
| M | 5 | 4 | 147.0 |

总体平均体重为：174.4

## 8.5 使用 PROC PRINT

PROC PRINT 是每个人都会经常使用的过程之一。它旨在转储数据，通常不用于生成漂亮的输出。然而，你可以通过 PRINT 做一些事情，即使这个标准过程也能变得更有用。

### 8.5.1 同时使用 ID 和 BY 语句

尽管 PRINT 过程没有 CLASS 语句，但你可以结合使用 BY 和 ID 语句来将各组分隔开。这两个语句共有的变量将对 PROC PRINT 生成的标准报告产生两个更改。

```sas
title1 '8.5.1 PRINT with BY and ID Statements';
proc print data=advrpt.clinicnames;
  by region;
  id region;
  var clinum clinnname;
run;
```

在左侧的 PRINT 步骤中，BY 和 ID 语句都使用了变量 REGION。以这种方式同时使用时，REGION 的值对于每个区域只写入一次（这是 PROC REPORT 对 GROUP 和 ORDER 变量的默认行为）。此外，在每个 REGION 之后插入了一个空行。

**8.5.1 带 BY 和 ID 语句的 PRINT**

| 区域 | 诊所编号 | 诊所名称 |
|---:|---:|---|
| 1 | 011234 | Boston National Medical |
|  | 014321 | Vermont Treatment Center |
| 10 | 107211 | Portland General |
|  | 108531 | Seattle Medical Complex |
| 2 | 023910 | New York Metro Medical Ctr |
|  | 024477 | New York General Hospital |
|  | 026789 | Geneva Memorial Hospital |
| ... | ... | *此表的部分内容未显示 ...* |

当 BY 语句中的所有变量也以相同顺序出现在 ID 语句的开头时，就会生成这种专门的 PROC PRINT 布局。

### 8.5.2 将 STYLE= 选项与 PROC PRINT 一起使用

STYLE= 选项（在第 8.1.3 和 8.4.6 节中讨论）也可以与 PROC PRINT 一起使用。这是一个样式覆盖选项，用于更改所选 ODS 样式生成的属性。

在下面显示的通用语法中，请注意属性被花括号括起来。

```
style<(location)>={attribute=attribute_value}
```

在当前的 SAS 版本中，你可以使用方括号代替花括号。

*位置*的指定是可选的，因为省略时会有一个默认赋值。然而，你通常需要指定位置，因为它用于控制属性赋值应用到何处。支持的位置包括：

- **数据** — 单元格（也即 COLUMNS 或 COL）
- **小计** — 子总计（用于 SUM 语句）
- **总计** — 整体总计（用于 SUM 语句）
- **表头** — 列标题（也即 HEAD 和 HDR）
- **N** — 当指定 N 选项时使用
- **观测** — OBS 列中的单元格
- **观测表头** — OBS 列的标题
- **表** — 控制表格结构，如单元格宽度

STYLE= 选项可以应用于 PROC PRINT 语句以及其他过程步语句。指定的位置与包含该选项的语句的组合，将决定该选项修改表格的哪一部分。

并非所有样式选项位置都适用于所有 PRINT 语句。下表显示了可用的位置以及可以应用它们的语句。

| PROC 语句 | 支持的样式位置 |
|---|---|
| PROC PRINT | data header, n, obs, obsheader, table |
| BY | 无 |
| ID | header, data |
| VAR | header, data |
| SUM | header, data, total, grandtotal |

可以修改的样式属性包括：

- BACKGROUND
- BORDERCOLOR
- BORDERCOLORDARK
- BORDERCOLORLIGHT
- FONT_FACE
- FONT_WEIGHT
- FOREGROUND

### 在 PROC 语句中

当 PROC 语句上使用 STYLE= 选项时，这些属性往往控制着这个特别迷人的表格的整体外观。

```sas
title1 'Using STYLE= with PRINT';
title2 '8.5.2a on the PROC Statement';
proc print data=advrpt.demog(obs=5)
             style(column)=[background=cyan]
             style(header)=[background=yellow
                            font_weight=bold]
             style(obs)=[background=pink]
             style(obsheader)=[background=cyan]
             ;
    var clinnum subject sex dob;
run;
```

- 1. 每列中的所有数据值的背景色都被重置。
- 2. 列标题的两个属性被重置。
- 3. OBS 列的背景色设置为粉红色。
- 4. OBS 列标题的背景色更改为青色。

![](img/4b16455363806a3241267bf9f49ba5d1_321_0.png)

### 支持语句

尽管与 PROC 语句一起使用的样式属性通常应用于整个表格，但在支持语句上应用的 STYLE= 选项可以让你进行更具体的控制。此外，这些属性往往覆盖在 PROC 语句上设置的属性。

与 CLASS 语句（参见第 7.1 节）类似，可以拆分为多个语句，PRINT 的几个允许变量列表的语句也可以拆分为多个语句。

```sas
proc print data=advrpt.demog(obs=5)
              style(column)=[background=cyan]
              style(header)= [background=yellow
                              font_weight=bold]
              ;
  id clinnum / style(hdr data)=(background=blue
                                 foreground=white);
  var subject / style(header)=(background=red
                                foreground=white)
                style(column)=(background=red
                               foreground=white);
  var sex dob edu;
  sum edu / style(grandtotal)=(font_weight=bold
                                background=blue
                                foreground=white);
run;
```

这允许你为不同的变量指定不同的选项。在应用 STYLE= 选项 ❸❹ 时，我们可以利用这一能力。

- ❶ PROC 语句上的 STYLE= 选项会覆盖与 ODS 样式 JOURNAL 关联的默认值。

**在支持语句上使用 STYLE= 与 PRINT 8.5.2b**

| 诊所编号 | 受试者 | 性别 | 出生日期 | 教育程度 |
|---|---:|---:|---|---:|
| 024960 | 200 | F | 12AUG51 | 17 |
| 082287 | 201 | F | — | 16 |
| 066789 | 202 | M | 15AUG30 | 12 |
| 063742 | 203 | M | 15JUN34 | 12 |
| 023910 | 204 | M | 14FEB? | 14 |
|  |  |  | 总计 | 59 |

- ❷ 为 ID 变量指定了两个位置。注意，HEADER 位置被缩写为 HDR。
- ❸ 指定了两个 STYLE= 选项，每个都有自己的位置。由于两者具有相同的属性，它们可以像 ❷ 中那样合并。
- ❹ VAR 语句被拆分为两个语句。这些变量没有样式覆盖，将使用在 PROC 语句 ❶ 中指定的属性。
- ❺ 列总计收到了三个属性覆盖。

## 更多信息

用于产生交通灯效果的样式覆盖选项在第 11.5.4 节中讨论。

