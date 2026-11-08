
将 MIXED= 的值改为 YES ❶ 并不一定足以使 SCALE 成为字符值；但是，如果将 DBMS 选项的值从 EXCEL 改为 XLS ❶，则 MIXED=YES 语句 ❶ 会生效，并且 SCALE 在数据集 SCALEDATA 中会写为字符变量。

```sas
PROC IMPORT OUT= WORK.scaledata
            DATAFILE= "C:\Temp\makescale.xls"
            DBMS=xls REPLACE; ❶
            GETNAMES=YES; ❶
            GUESSINGROWS=800; ❶
RUN;
```

> 当 MIXED=YES 不实用时，有时可以使用 GUESSINGROWS= 语句来成功确定变量的类型。

当 DBMS=EXCEL 时不能使用 GUESSINGROWS，但在 DBMS=XLS 时可以使用。由于 GUESSINGROWS ❶ 会改变在确定列应为数值型还是字符型之前扫描的行数，因此使用它可能会增加读取数据所需的时间和资源。

### 另请参见

SAS 论坛帖子 http://communities.sas.com/thread/12743?start=0 中有一个使用 NAMEROW= 和 STARTROW= 数据源语句的 PROC IMPORT。帖子 http://communities.sas.com/thread/30405?start=0 讨论了命名区域，并且该帖子与帖子 http://communities.sas.com/thread/12293?start=0 展示了多个数据源语句的用法。

## 1.2.4 导入和导出 CSV 文件

逗号分隔值（CSV）文件多年来一直是在系统之间移动数据的标准文件类型。幸运的是，我们现在有许多更优秀的工具可用，因此不再需要那么频繁地求助于 CSV 文件。尽管如此，它们仍被普遍使用，我们需要了解如何处理它们。

IMPORT 和 EXPORT 过程均可处理 CSV 文件（此功能是 Base SAS 产品的一部分，不需要 SAS/ACCESS 产品）。两者都通过先构建一个 DATA 步，然后执行该 DATA 步来完成转换。

### 构建 DATA 步

当您使用导入/导出向导保存 PROC 步时（参见第 1.2.1 节），生成的 DATA 步不会被保存。幸运的是，您仍然可以通过调出上一次提交的代码来获取生成的 DATA 步。

- 1. 执行 IMPORT/EXPORT 过程。
- 2. 在 Display Manager 中，转到 RUN→Recall Last Submit。

一旦该过程生成的代码加载到编辑器中，您就可以出于其他目的修改它，或者只是从中学习。对于第 1.2.1 节中简单的 PROC EXPORT 步，会生成以下代码：

```sas
%macro rename(headrow=3, rawcsv=, dsn=);
%local lib ds i;
data _null_ ;
   infile "&path\Data\&rawcsv"
      scanover lrecl=32767 firstobs=&headrow;
   length temp $ 32767;
   input temp $;
   i=1;
   do while(scan(temp,i,',') ne ' ');
      call symputx('var'||left(put(i,4.)),scan(temp,i,','),'l');
      i+1;
   end;
   call symputx('varcnt',i-1,'l');
   stop;
run;

%* Determine the library and dataset name;
%if %scan(&dsn,2,.) = %then %do;
   %let lib=work;
   %let ds = %scan(&dsn,1,.);
%end;
%else %do;
   %let lib= %scan(&dsn,1,.);
   %let ds = %scan(&dsn,2,.);
%end;

proc datasets lib=&lib nolist;
   modify &ds;
   rename
   %do i = 1 %to &varcnt;
      var&i = &&var&i
   %end;
   ;
   quit;
%mend rename;

%rename (headrow=3, rawcsv=classwc.csv, dsn=work.classwo)
```

### 另请参见

McGuown (2005) 还讨论了 PROC IMPORT 在读取 CSV 文件时生成的代码。King (2011) 使用数组和哈希表来读取具有未知或可变变量列表的 CSV 文件。这些灵活而高效的技术可以适用于本节所述类型的问题。

## 1.2.5 防止导出空白工作表

当排除条件从给定工作表 ❶ 中排除所有可能的行时，PROC EXPORT 并不能防止我们写入空白工作表。在下面的示例中，我们无意中要求列出所有 SEX='q' 的学生。

```sas
proc export data=sashelp.class(where=(sex='q'))
    outfile='c:\temp\classmates.xls'
    dbms=excel2000
    replace;
    SHEET='sex: Q';
run;
```

当然没有这样的学生，因此生成的工作表是空白的，除了列标题。

我们可以通过首先识别那些具有一行或多行的 SEX 水平来防止这种情况发生。生成变量值列表的方法有很多；不过，SQL 步非常适合将这些值放入宏变量以供进一步处理。

要导出的数据集名称以及分类变量，作为命名参数传递给宏 %MAKEXLS。

```sas
%macro makexls(dsn=,class=);
%local valuelist listnum i value;
proc sql noprint;
select distinct &class ➋
       into :valuelist separated by ' ' ➌
       from &dsn;
%let listnum = &sqlobs;
quit;

%* One export for each sheet;
%do i = 1 %to &listnum; ➍
  %let value = %scan(&valuelist,&i,%str( )); ➎
  proc export data=&dsn(where=(&class="&value")) ➏
              outfile="c:\temp\&dsn..xls"
              dbms=excel2000
              replace;
              SHEET="&class.&value";
%end;
run;
%mend makexls;
%makexls(dsn=sashelp.class,class=sex)
```

- ➋ 使用 SQL 步构建分类变量的不同值列表。
- ➌ 这些值保存在宏变量 &VALUELIST 中。
- ➍ 使用 %DO 循环遍历各个值，这些值使用 %SCAN 函数从列表 ➎ 中提取。
- ➏ 然后 PROC EXPORT 步为所选值创建工作表。

### 另请参见

在 sasCommunity.org 上的文章“Automatically_Separating_Data_into_Excel_Sheets”中可以找到将数据集拆分为单独工作表的类似示例。
http://www.sascommunity.org/wiki/Automatically_Separating_Data_into_Excel_Sheets

## 1.2.6 使用命名区域

默认情况下，PROC IMPORT 和 LIBNAME 语句的 EXCEL 引擎期望 EXCEL 数据以某种方式排列（列标题如果存在，位于第一行 A 列；数据从第二行开始）。然而，数据作为报告的一部分或较大表的子集交付并不罕见。一种解决方案是手动将数据剪切并粘贴到空白工作表中，使其符合默认布局。创建命名区域通常要容易得多。

**来自 SASHELP.CLASS 的数据**

| 变量名 | 姓名 | 性别 | 年龄 | 身高 | 体重 |
|---|---|---|---|---|---|
|  | Alfred | M | 14 | 69 | 112.5 |
|  | Alice | F | 13 | 56.5 | 84 |
|  | Barbara | F | 13 | 65.3 | 98 |
|  | Carol | F | 14 | 62.8 | 102.5 |
|  | Henry | M | 14 | 63.5 | 102.5 |
|  | James | M | 12 | 57.3 | 83 |
|  | Jane | F | 12 | 59.8 | 84.5 |
|  | Janet | F | 15 | 62.5 | 112.5 |
|  | Jeffrey | M | 13 | 62.5 | 84 |

此处显示的 EXCEL 电子表格包含 SASHELP.CLASS 数据集（这里仅显示其中一部分）；但是，已添加标题和列。使用默认设置时，PROC IMPORT 将无法成功读取此工作表。

为便于使用此电子表格，为 C3-G22 定义的矩形创建了命名区域。该区域被命名为 'CLASSDATA'。现在可以在从该工作表读取数据时使用此命名区域。

```sas
    libname seexls excel "&path\data\Ei_2_6classmates.xls";

    data class;
       set seexls.classdata; ①
    run;
    libname seexls clear; ②
```

命名区域（CLASSDATA）的使用方式与使用工作表名称 ① 一样。

② 在 LIBNAME 语句中使用引擎时，务必清除 libref，以便您可以在 SAS 之外使用该电子表格。

```sas
    proc import out=work.classdata
        datafile= "&path\data\Ei_2_6classmates.xls"
        dbms=xls replace;
    getnames=yes;
    range='classdata'; ③
    run;
```

使用 PROC IMPORT 读取命名区域时，使用 RANGE= 语句 ③ 指定感兴趣的命名区域。由于命名区域的名称在工作簿中是唯一的，因此不需要工作表名称。

### 更多信息

EXCEL LIBNAME 引擎在第 1.1 节中介绍。

## 1.3 DATA 步 INPUT 语句

INPUT 语句包含大量选项，使其极其灵活。由于关于基本 INPUT 语句的文章已经很多，这里只收集了少数似乎未充分使用的选项。

### 另请参见

有关使用 INPUT 语句读取原始数据的概述，可在 SAS 文档 http://support.sas.com/publishing/pubcat/chaps/58369.pdf 中找到。Schreier (2001) 简要概述了自动 _INFILE_ 变量，以及有关读取原始数据的其他信息。

