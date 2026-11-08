
```sas
ods tagsets.excelxp
        style=default
        path="&path\\results"
        body="E11_2.xls";
title1 '11.2 Using the EXCELXP Tagset';
title2 "Using the ExcelXP Tagset";

proc report data=work.advrpt.demog
             nowd split='*';
```

*PROC REPORT 步骤的部分内容未显示*

![](img/4b16455363806a3241267bf9f49ba5d1_361_0.png)

❶ EXCELXP 是 MARKUP 目标中的一个标签集。你也可以在 ODS MARKUP 语句上将该标签集作为选项来指定 ❷。

```sas
ods markup tagset=excelxp ...
```

该标签集的重点在于数据，而不一定在于文本。请注意，使用默认设置时，这两个标题甚至不会出现在 Excel 电子表格中。当然，可以通过使用内嵌的 `titles='yes'` 选项来包含标题。这只是众多可用选项之一。要查看当前可用选项列表，请使用 DOC='help' 选项 ❸，它会将选项列表写入 LOG。

```sas
ODS tagsets.excelxp file="&path\\results\\test.xml"
    options(doc="help");
```

### 另请参阅

EXCELXP 标签集在（Andrews, 2008）中得到了进一步讨论。Eric Gebhart（Gebhart, 2010）撰写了多篇关于该标签集的论文。Vince DelGobbo 撰写了十几篇关于 EXCELXP 标签集的论文。Vince 论文的总索引可在 http://www.sas.com/events/cm/evotms/ExcelXP/ExcelXPpaperIndex.pdf 找到，他和其他 SAS 作者的完整论文列表可在 http://support.sas.com/rnd/papers/index.html 找到。

### 11.2.1 EXCELXP 标签集文档与选项

EXCELXP 标签集的操作通过使用选项来控制。这些选项通过 OPTIONS 选项实现，选项本身括在括号中并跟在 OPTIONS 关键字之后。此处使用 DOC= 选项将标签集的完整文档写入 LOG。如果你想了解该标签集的近期更改，CHANGELOG 选项（doc="changelog"）会显示更改时间以及新功能摘要。

```sas
ODS tagsets.excelxp
    path="&path\\results"
    body="E11_2.xls";
    options(doc="help");
```

### 另请参阅

EXCELXP 标签集不断更新和完善。如果你使用的是 SAS 随附的 EXCELXP 标签集版本，它不太可能是最新版本。你可以阅读 SAS Note #32394（位于 [http://support.sas.com/kb/32/394.html](http://support.sas.com/kb/32/394.html)）来了解如何下载并安装最新版本的 EXCELXP 标签集。

### 11.2.2 生成多工作表工作簿

在将报表或数据集写入 Excel 时，常常需要将其拆分成多个部分，分别写入工作簿中的各个工作表。这可以通过几种不同的方式实现。这里展示的两种技术之间的主要区别在于，你是将报表还是仅将数据发送到电子表格。

将报表写入 Excel 时，EXCELXP 标签集是最灵活的选择。本示例通过 PROC PRINT 演示了这一点。该技术利用 BY 组处理来拆分报表。

```sas
%macro multisheet(dsn=,bylist=);
ods tagsets.excelxp
            style=default
            path="&path\\results"
            body="E11_2_2a.xls"
            options(sheet_name='none'
                    sheet_interval='bygroup'
                    embedded_titles='no');
proc sort data=&dsn out=sorted;
    by &bylist;
proc print data=sorted;
    by &bylist;
    run;
ods tagsets.excelxp close;
%mend multisheet;
%multisheet(dsn=advrpt.demog,bylist=race)
```

- 1. 选择使用 EXCELXP 标签集。
- 2. 让标签集决定工作表名称。
- 3. `SHEET_INTERVAL` 选项决定如何拆分工作表。
- 4. 报表中不会包含标题。这是默认设置。
- 5. 使用 `SHEET_INTERVAL` 选项 `BYGROUP` ③ 时，必须指定 BY 语句。

对于这个宏调用，RACE 的每个水平都会创建一个工作表，包括 RACE 的任何缺失值。

将数据集拆分为多个工作表时，我们不需要动用 EXCELXP 标签集的能力。相反，我们可以使用 PROC EXPORT。这里的 EXPORT 步骤位于 `%DO` 循环内，该循环会针对所选分类变量的每个水平执行一次。

```sas
%macro multsheet(dsn=,cvar=);
    %local varcnt type string i;
    proc sql noprint; ❸
        select distinct &cvar
            into :idvar1 - :idvar&sysmaxlong
            from &dsn;
        %let varcnt = &sqlobs;
    quit;

data _null_; ❹
    if 0 then set &dsn;
    call symputx('type',vtype(&cvar),'l');
    stop;
run;

%do i = 1 %to &varcnt;
    %if &type=N %then %let string=&idvar&i; ❺
    %else %let string="&idvar&i";
    proc export
        data=&dsn(where=(&cvar=&string)) ❻
        outfile="&path\results\E11_2_2b.xls"
        dbms= excel
        replace;
        sheet = "&cvar._&idvar&i"; ❿
    run;
%end;
%mend multsheet;
%multsheet(dsn=advrpt.demog,cvar=race)
```

- ❸ 使用 PROC SQL 创建一系列宏变量，以保存分类变量（&CVAR）的不同水平。
- ❹ 使用 DATA _NULL_ 步骤判断分类变量是数值型还是字符型。
- ❺ 针对数值型和字符型变量分别建立 WHERE 条件。
- ❻ 使用在 ❺ 中建立的 WHERE 条件对数据集进行子集化。
- ❿ 工作表名称由变量名及其值组合而成。

### 另请参阅

关于该主题必读的论文由 Vince DelGobbo（2007）撰写。这里展示的 PROC EXPORT 示例改编自 SASCommunity.org 上的一篇文章，该文章展示了一个通用性较低的程序，用于将数据集拆分为单独的 EXCEL 工作表 [http://www.sascommunity.org/wiki/Automatically_Separating_Data_into_Excel_Sheets](http://www.sascommunity.org/wiki/Automatically_Separating_Data_into_Excel_Sheets)。

### 11.2.3 查看样式

除了你或你的公司可能创建的自定义样式之外，SAS 还随附了 40 多种预定义样式。由于可供选择的样式如此之多，并且在使用 EXCELXP 标签集将报表写入 Excel 时，并非所有样式属性都会传递到 Excel 电子表格中，因此能够针对每个当前定义的样式可视化你的报表就变得很重要。

%SHOWSTYLES 宏使用宏语言为每个可用样式向 Excel 写入一次报表。

```sas
title1 '11.2.3 Showing Style in Excel';

%macro showstyles;
%local i stylcnt;
proc sql noprint;
   select scan(style,2,'.')
      into: style1-stylemaxlong
      from sashelp.vstyle;
   %let stylcnt = &sqlobs;
quit;

%do i = 1 %to &stylcnt;
   ods markup tagset=excelxp
      path="&path\\results"
      file="&&style&i...xml"
      style=&&style&i
      options(sheet_name="&&style&i"
              embedded_titles='yes');

      title2 "Using the &&style&i Style";
      proc report data=sashelp.class nowd;
         column name sex age height weight;
         define age / analysis mean f=4.1;
         define height / analysis mean f=4.1;
         define weight / analysis mean f=5.1;
         rbreak after / summarize;
         run;
   ods markup close;
%end;
%mend showstyles;
ods listing close;

%showstyles
```

- 1. 使用 SQL 步骤为每个唯一样式名创建一个宏变量。
- 2. 找到的样式数量保存在 `&STYLCNT` 中。
- 3. 在 `%DO` 循环内部，样式名将包含在宏变量引用 `&&STYLE&I` 中。因此，文件名中包含样式名。
- 4. 感兴趣的样式在 STYLE= 选项上指定。
- 5. 工作表名称将是样式名。
- 6. 每个样式的报表代码完全相同。
- 7. 调用 %SHOWSTYLES 宏。

## 11.3 使用转义字符序列进行内联格式设置

有些类型的格式设置很难或无法直接使用 ODS 样式和选项来实现。然而，通过使用转义字符，可以将目标特定的命令直接传递给构建输出的目标。转义字符会提醒 ODS：相关的格式设置字符序列不应由 ODS 直接使用，而应传递给接收目标。

转义字符应当是你在 SAS 程序中不另外使用的字符。由于我倾向于不将波浪号用作否定助记符，因此它是一个很好的转义字符。转义字符通过 ODS ESCAPECHAR 选项指定。

```sas
ods escapechar='~';
```

转义字符用于标记一个转义序列，该序列可能包含一个或多个目标命令或函数。语法因命令类型而异。

| 类型 | 一般形式 | 用于 | 小节 |
|---|---|---|---|
| 格式设置函数 | `~{function text}` | 控制分页、上标、下标。 | 11.3.1<br>11.3.2 |
| 样式修改 | `~S={attribute characteristics}`<br>`~{style elements and attributes}` | 分配样式属性。 | 11.3.3 |
| 序列代码 | `~code` | 操作换行、折行和缩进。 | 11.3.4 |
| 原始文本插入 | `~R/destination "rawtext"`<br>`~R "rawtext"` | 插入目标特定代码。 | 11.3.5 |

### 另请参阅

Carpenter（2007a，第 8.6 节）在 PROC REPORT 步骤的背景下讨论了内联格式设置。

Haworth、Zender 和 Burlew（2009）讨论了转义字符和内联格式设置序列在各种用法中的使用。

Zender（2007）在这篇易读的 SAS Global Forum 论文中涵盖了内联格式设置的所有基础知识。如果你想了解更多，这应该是你阅读的关于该主题的第一篇论文。

