
## 更多信息

#BYVAL 和 #BYVAR 标题与脚注选项也在第 7.4.3 节中使用，并在第 15.1.2 节中讨论。

## 另请参阅

用法说明 15727 讨论了将 BODYTITLE 选项与 PAGEOF 序列一起使用。

## PDF 和 RTF 目标 - 使用 THISPAGE 和 LASTPAGE

PAGEOF 序列仅适用于 RTF 输出目标；但是，通过使用 THISPAGE 和 LASTPAGE 格式序列，你可以为 RTF 和 PDF 输出目标创建更灵活的分页。与 PAGEOF 序列一样，这些序列设计用于标题和脚注，并且在将 BODYTITLE 选项与 RTF 输出目标一起使用时，可能会出现意外结果。

```sas
ods pdf file="&path\\results\\E11_3_1b.pdf"
             style=printer;
ods rtf file="&path\\results\\E11_3_1b.rtf"
            style=rtf;

title1 '11.3.1b Using In-line Formatting';
title2 '#byvar1 #byval1';
title3 'THISPAGE and LASTPAGE';
title4 h=10pt
       'This is Page ~{thispage} of a Total of ~{lastpage} Pages';
proc means data=demog n mean;
   by symp;
   class sex;
   var wt ht;
   run;
ods _all_ close;
```

![](img/4b16455363806a3241267bf9f49ba5d1_367_0.png)

LASTPAGE 序列的行为类似于 RTF 输出目标中的 PAGEOF。在导入表后，你可能需要执行打印预览或向下滚动几页，才能观察到总页数。

## 11.3.2 上标、下标和匕首符号

除了分页信息之外，你还可以使用内联格式添加上标、下标和匕首符号来突出特定文本。内联格式函数包括：

- `~{super 1}` 使 1 成为上标
- `~{sub 14}` 使数字 14 成为下标
- `~{dagger}` 可以使用匕首符号代替数字。

```sas
title1 '11.3.2 In-line Formatting';
ods escapechar='^';
ods pdf file="&path\results\E11_3_2.pdf"
        style=printer;
title2 'Superscripts and a Dagger ~{dagger}'; ❶
proc report data=adprt.demo nowd split='*';
  column symp wt ht;
  define symp / group 'symptom' order=data;
  define wt   / analysis mean format=6.1
               'Weight~{super 1}' ❷;
  define ht   / analysis mean format=6.1
               'Height~{super 2}' ❸;
  compute after;
    line @1 '~{super 1} ❹Pounds';
    line @1 '~{super 2} ❹Inches';
    line @1 '~{dagger} ❹Using inline formatting';
  endcomp;
run;
ods _all_ close;
```

- ❶ 匕首符号放在标题中。该符号本身在所有输出目标中外观并不相同。
- ❷ 上标用于标注测量单位。在此 PROC REPORT 步骤中，它们同时应用于 DEFINE 语句和 LINE 语句。
- ❸ 列放置表示法（@1）在大多数输出目标中并不可靠，尤其是在使用比例字体时。@1 可以可靠地将文本左对齐；但是，使用类似 @5 的写法不一定能使跨行文本对齐。

**11.3.2 内联格式**

*上标和匕首符号 †*

| 症状 | 体重^1 | 身高^2 |
|---|---|---|
| 02 | 150.2 | 66.8 |
| 10 | 184.4 | 68.5 |
| 06 | 118.8 | 64.0 |
| 04 | 170.8 | 68.7 |
| 03 | 154.5 | 66.5 |
| 09 | 133.0 | 68.0 |
| 05 | 179.5 | 67.5 |
| 01 | 138.5 | 67.5 |

^1 磅  
^2 英寸  
† 使用内联格式

（@1）在大多数输出目标中并不可靠，尤其是在使用比例字体时。@1 可以可靠地将文本左对齐；但是，使用类似 @5 的写法不一定能使跨行文本对齐。

## 更多信息

可以使用内联格式序列代码实现跨行文本对齐；参见第 11.3.4 节。同一示例也演示了匕首符号的用法。

## 11.3.3 更改属性

与文本关联的属性可以使用内联样式修饰符更改。由 ODS 样式设置的大多数标准属性都可以修改。样式修饰符几乎可以用在任何指定文本的地方。这不仅包括标题和脚注，还包括格式化值的标签，甚至数据本身。样式修饰符有两种通用形式。

在 SAS 9.2 之前，唯一可用的形式是：

```sas
~S={attribute=value}
```

注意，大写 S= 跟在转义字符之后并位于花括号之前。典型用法是更改标题中文本的属性。

```sas
title2 '~S={font_face="times new roman"} ❶ Initial'
       '~S={font_style=roman} ❷ Coded'
       '~S={} ❸ Symptoms';
```

### 11.3.3a 内联格式

初始编码症状

1. 默认的 title2 字体更改为 Times New Roman。
2. 将默认字体样式从斜体更改。
3. 关闭更改并恢复默认值。

从 SAS 9.2 开始，引入了更灵活的样式修饰符形式。通用形式是：

```sas
~{style [element=attribute] text}
```

样式元素及其属性括在方括号内，它们一起位于要应用元素/属性对的文本之前。注意，花括号既括住文本，也括住样式元素。

以下 TITLE 语句生成与上一示例的 TITLE 语句相同的标题行。

```sas
title2 '~{style [font_face="times new roman"]Initial}'
       '~{style [font_style=roman] Coded}'
       ' Symptoms';
```

由于修改后的属性仅应用于花括号内的文本，因此默认属性应用于“Symptoms”。

### 11.3.3b 内联格式

初始编码症状

两种类型的样式修改序列都可以在 TITLE 和 FOOTNOTE 语句之外使用。

```sas
compute after;
  line @3 '~{style [font_weight=bold font_size=3] ~{super 1} Pounds}';
  line @3 '~{style [font_weight=light] ~{super 2} Inches}';
endcomp;
```

![](img/4b16455363806a3241267bf9f49ba5d1_370_0.png)

事实上，它们可用于大多数显示文本的地方。这包括数据、标签和格式化值。此处，样式修改序列应用于 PROC REPORT 计算块内的 LINE 语句中。

## 另请参阅

Haworth、Zender 和 Burlew（2009，第 268 页）基于数据值创建了几个样式修改序列。

## 11.3.4 使用序列代码控制缩进、间距和换行

对于某些输出目标，可以将一系列序列代码与转义字符一起使用，以控制换行、缩进和间距。这些代码对每个主要输出目标的效果可能并不相同，并且性能可能取决于所使用的 SAS 版本。

| 代码序列 | 作用 | 备注 |
|---|---|---|
| `~m` | 缩进位置标记。 | |
| `~2n` | 强制换行（会考虑 `~m`）。 | |
| `~xn` | 强制 *x* 次换行（不考虑 `~m`）。 | *x* = 换行数 |
| `~w` | 可选换行的建议位置。 | |
| `~_` | 创建不间断空格。 | 下划线 |
| `~xz` | 插入四种错误代码之一。 | *x* = 1、2、3 或 4 |

```sas
proc format;
   value $genttl
      'f','F'='Female~2nSubjects'
      'm','M'='Male~2nSubjects';
   run;

title1 "Controlling Line Breaks";
proc report data=drvpt.demog nowd;
   columns sex ht wt;
   define sex / group format=$genttl.
                  'Subject~w Gender';
   define ht  / analysis mean
                  format=5.2
                  'Height~{dagger}';
   define wt  / analysis mean
                  format=6.2
                  'Weight~{dagger}';
   rbreak after / summarize;

   compute after;
      line @1 '~{dagger} English Measures'
         ' ~2nHeight(in.) ~2nWeight(lbs.)';
      line @1 'All ~2nsubjects were screened during'
         ' ~2n intake session at visit one.';
   endcomp;
run;
```

1. ~m 用于标记由 ~2n 序列指定的换行所对应的对齐位置（缩进）。
2. 使用 ~2n 表示法强制换行。如果不强制这些换行，表的宽度将由 LINE 语句决定。
3. ~w 表示可选换行。这意味着如果需要换行，这将是首选的换行位置。在此表中，无论是否使用 ~w，文本都会在空格处换行。
4. 添加匕首符号，以将列标签与单位脚注关联起来。

**控制换行**

| 受试者性别 | 身高† | 体重† |
|---|---:|---:|
| 女性受试者 | 65.06 | 144.55 |
| 男性受试者 | 69.24 | 172.91 |
|  | 67.56 | 161.49 |

† 英制测量  
身高（英寸）  
体重（磅）  
所有受试者在第一次访视的入组环节中接受了筛查。
