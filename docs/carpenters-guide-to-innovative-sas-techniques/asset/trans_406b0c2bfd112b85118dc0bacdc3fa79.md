

```sas
proc report data=advrpt.demog nowd;
    column edu sex,wt wt=allwtmean;
    define edu / group 'Years/Ed.';
    define sex / across order=formatted;
    define wt / mean 'Mean' format=5.1;
    define allwtmean / mean 'Mean' format=5.1;

    compute allwtmean;
        _c2_ = _c2_/2.2;
        _c3_ = _c3_/2.2;
        allwtmean = allwtmean/2.2;
    endcomp;
run;
```

生成的报表现在显示，女性的平均体重已成功转换为千克。

### 8.4.3b 在计算块中展示 ACROSS

将 LB 转换为 KG

患者性别：M / F

| 教育年限 | 平均值 | M 平均值 | F 平均值 |
|---:|---:|---:|---:|
| 10 | . | 88.2 | 88.2 |
| 12 | 69.1 | 81.7 | 76.4 |
| 13 | 97.7 | 86.8 | 89.5 |
| 14 | 49.9 | 47.7 | 49.1 |
| 15 | 74.8 | 60.5 | 70.7 |
| 16 | 71.8 | 75.9 | 75.1 |
| 17 | 64.9 | 70.5 | 66.0 |
| 18 | . | 79.1 | 79.1 |

## 8.4.4 使用虚拟列合并计算块

在上一节中，我们通过利用与问题列右侧的报表项相关联的计算块，解决了一个棘手的问题。当右侧没有计算块时，可以基于虚拟列使用计算块来计算这三个平均值。在本例中，ALLWTMEAN 位于其他列的左侧。因此，在 COLUMN 语句中，它的计算块不能用于计算其右侧的报表项。

```sas
proc report data=advrpt.demog nowd;
    column edu wt=allwtmean sex,wt dummy ❶;
    define edu / group 'Years/Ed.';
    define allwtmean / mean 'Overall Mean' format=7.1;
    define sex / across order=formatted;
    define wt / mean 'Mean' format=5.1;
    define dummy / computed noprint ❷;

    compute dummy;
        _c4_ = _c4_/2.2; ❸
        _c3_ = _c3_/2.2;
        allwtmean = allwtmean/2.2;
    endcomp;
run;
```

- ❶ DUMMY 列必须是 COLUMN 语句中最靠右的列。或者至少它必须位于计算块中使用的任何列的右侧。

### 8.4.4 使用 DUMMY 列合并计算块

| 教育年限 | 总体平均值 | 患者性别 F 平均值 | 患者性别 M 平均值 |
| --- | --- | --- | --- |
| 10 | 88.2 |  | 88.2 |
| 12 | 76.4 | 69.1 | 81.7 |
| 13 | 89.5 | 97.7 | 86.8 |
| 14 | 49.1 | 49.9 | 47.7 |
| 15 | 70.7 | 74.8 | 60.5 |
| 16 | 75.1 | 71.8 | 75.9 |
| 17 | 66.0 | 64.9 | 70.5 |
| 18 | 79.1 |  | 79.1 |

- ❷ 在 DUMMY 的 DEFINE 语句中出现了 NOPRINT 选项，因为我们不希望显示该列。

- ❸ 男性和女性值的列号现在发生了变化（_C3_ 现在是女性的平均体重）。由于这三个转换彼此独立，因此可以按任意顺序执行。

## 8.4.5 合并列

有时，我们希望将多个报表项中包含的信息显示在单个列中。这样做可以让我们对报表项的外观有额外的控制。在下面的示例中，我们希望显示平均值及其标准误差，并将值显示为 *平均值*（*标准误*）。

```sas
proc report data=advrpt.demog nowd;
    column edu sex, (wt wt=wtse meanse ❶);
    define edu / group 'Years/Ed.';
    define sex / across order=formatted; ❷
    define wt / mean noprint; ❸
    define wtse / stderr noprint;
    define meanse / computed 'Mean (SE)' format=$15.; ❸

    compute meanse/char length=15; ❹
        _c4_ = cat(put(_c2_,5.2), ' (',put(_c3_,5.2),')'); ❹
        _c7_ = cat(put(_c5_,5.2), ' (',put(_c6_,5.2),')'); ❹
    endcomp;
run;
```

- ❶ WT、其别名 WTSE 以及计算报表项 MEANSE 都嵌套在 SEX ❷ 之下，SEX 的 define 用法为 ACROSS。

- ❷ WT 和 WTSE 的值不会被打印。它们仅用于构成拼接后的值（MEANSE）。

- ❸ 定义了计算报表项 MEANSE。

- ❹ 计算变量 MEANSE 被定义为长度为 15 的字符型。

- ❹ 女性的平均值（_C2_）和标准误（_C3_）被拼接成单个值（_C4_）。

### 8.4.5 在 ACROSS 变量内合并列

性别内的体重

| 教育年限 | F 平均值（标准误） | M 平均值（标准误） |
|---:|---:|---:|
| 10 | . ( . ) | 194.1 ( 5.75) |
| 12 | 152.0 ( 9.71) | 179.8 ( 6.73) |
| 13 | 215.0 ( . ) | 191.0 (12.00) |
| 14 | 109.9 ( 1.78) | 105.0 ( 0.00) |
| 15 | 164.6 (13.72) | 133.0 ( 0.00) |
| 16 | 158.0 ( 0.00) | 167.0 ( 7.70) |
| 17 | 142.8 ( 9.84) | 155.0 ( 0.00) |
| 18 | . ( . ) | 174.0 (15.59) |

计算报表项 MEANSE 是在计算块中通过拼接 MEAN 和 SE 构建的，两者均不单独打印。这也允许我们添加括号。

由于 SEX 的 define 用法为 ACROSS，因此必须在计算块中使用绝对列引用。

## 8.4.6 在 LINES 中使用 STYLE= 选项

当写入 PDF、RTF 和 HTML 等输出目标时，可以使用 STYLE= 选项覆盖 ODS 样式中的值，而无需使用 PROC TEMPLATE 重新定义样式本身。此选项可用于 REPORT、TABULATE 和 PRINT 过程。在 REPORT 中，它可以与计算块中的 LINE 语句一起使用。

```sas
proc report data=advrpt.demog nowd;
    column edu sex, wt (wt=wtse) wt=n wt=allwt;
    define edu / group 'Years/Ed.';
    define sex / ' ' across order=formatted;
    define wt   / mean 'Mean' F=5.1;
    define wtse / stderr 'StdErr' F=5.2;
    define n    / n noprint;
    define allwt / mean 'Overall/Mean' F=5.1;

    compute after/style(lines)={just=center
                                font_face=Arial
                                font_style=italic
                                font_size=10pt};
        line ' ';
        line @10 'Overall Statistics:';
        line @15 n 3. 'Subjects had a mean weight of ' allwt 5.1 ' pounds';
    endcomp;
run;
```

此处使用样式覆盖选项来更改 LINE 语句所写入文本的对齐方式、字体、字体样式和字体大小。

在 LINE 语句中，@10 和 @15 控制文本的最左侧起始位置。这些值在除 LISTING 之外的目标中会被忽略，而 STYLE 选项在 LISTING 目标中会被忽略。

### 8.4.6 在 COMPUTE 语句上使用 STYLE

患者体重

*患者性别：F / M*

| 教育年限 | F 平均值 | F 标准误 | M 平均值 | M 标准误 | 总体平均值 |
|---|---:|---:|---:|---:|---:|
| 10 | . | . | 194.1 | 5.75 | 194.1 |
| 12 | 152.0 | 9.71 | 179.8 | 6.73 | 168.1 |
| 13 | 215.0 | . | 191.0 | 12.00 | 197.0 |
| 14 | 109.9 | 1.78 | 105.0 | 0.00 | 108.1 |
| 15 | 164.6 | 13.72 | 133.0 | 0.00 | 155.6 |
| 16 | 158.0 | 0.00 | 167.0 | 7.70 | 165.2 |
| 17 | 142.8 | 9.84 | 155.0 | 0.00 | 145.2 |
| 18 | . | . | 174.0 | 15.59 | 174.0 |

*总体统计：*

*76 名受试者的平均体重为 160.5 磅。*

在计算块中也可以使用 LINE 语句进行内联格式化，但是，随着格式变得越来越复杂，有几点需要注意。由于 LINE 语句在执行前被合并，你可能无法在计算块内的 LINE 语句级别更改样式属性。在此示例中，STYLE 选项将应用于每个 LINE 语句。

如果确实需要在单个行上更改属性，则内联格式化可能必须在单独的计算块中完成。如果你正在使用 COMPUTE AFTER（报表末尾）计算块，这可能会带来问题。

在下面的示例中，引入了一个人工变量 PAGEFLAG。由于它是一个常量，COMPUTE AFTER PAGEFLAG 块和 COMPUTE AFTER 块都将在报表末尾执行。这将允许使用具有两种不同样式的 LINE 语句。

```sas
* Show the use of the inline formatting;
ods rtf file="&path\results\E8_4_6b.rtf";
ods escapechar='^'; ❶
title1 '8.4.6 Using Inline Formatting';
title2 '^S={just=r} Patient Weight'; ❷
data demog;
set advrpt.demog;
pageflag=1; ❸
run;

proc report data=demog(where=(sex='F')) nowd;
  column pageflag edu sex, (wt wt=wtse) wt=n wt=allwt;
  define pageflag / group noprint; ❹
  . . . . Define statements not shown . . . .
  compute after pageflag;
    line '^S={just=l background=pink} Females Only';
  endcomp;
  compute after/style(lines)={just=center ❺
                              font_face=Arial
                              font_style=italic
                              font_size=10pt};
    line ' ';
    line @10 'Overall Statistics:';
    line @15 n 3. ' Subjects had a mean weight of '
                 allwt 5.1 ' pounds';
  endcomp;
run;
ods rtf close;
```

- ❶ 指定一个转义字符，用于内联格式化序列。

- ❷ 使用内联格式化将标题右对齐。

- ❸ 创建一个常量变量，使我们能够在报表末尾有第二个计算块。

- ❹ 此报表项不会被打印，但由于它的 define 用法为 GROUP，因此可以将计算块与它关联。

