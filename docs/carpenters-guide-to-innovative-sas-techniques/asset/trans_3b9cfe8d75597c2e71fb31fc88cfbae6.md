
### 更多信息

13.2.2 节和 13.2.3 节中的 SYMPUTX 示例使用第三个参数来完成符号表赋值。

## 13.2.2 使用 SYMPUTX 保存选项的值

宏 %SCALEPOS 用于重新缩放 SAS/GRAPH 的 VPOS 和 HPOS 图形选项。这些选项的值存储在通过调用 SYMPUTX 例程生成的宏变量中。

```sas
%macro ScalePos(hvscale=2.5);
data _null_;
   set sashelp.vgopt(keep=optname setting);
   where optname in ('HPOS','VPOS');
   call symputx(optname,setting,'G'); ❶
run;

options hpos=%sysevalf(&hpos * &hvscale)
       vpos=%sysevalf(&vpos * &hvscale);
%mend scalepos;
options reset=all dev=win;
%scalepos(hvscale=1.5)

   . . . . code not shown . . . .

* Reset the HPOS and VPOS graphics options;
options hpos=&hpos vpos=&vpos; ❷
```

-   ❶ 要创建的宏变量的名称存储在变量 OPTNAME 中，因此 SYMPUTX 例程的第一个参数不是常量。第三个参数可以是大写或小写，它允许我们将这些宏变量放入全局符号表。
-   ❷ 这些宏变量可在稍后用于将图形选项重置回其原始值。

这种将变量传递到全局符号表的技术假设我们知道宏变量 &HPOS 和 &VPOS 要么尚不存在，要么宏 %SCALEPOS 可以更改它们的值。如果不是这种情况，那么我们就有可能发生宏变量冲突（参见 13.1 节）。

### 另见

检索、存储和重新建立选项及其值的其他方法可在 Carpenter (2004, 第 10.3.1 节) 中找到。

## 13.2.3 使用 SYMPUTX 构建宏变量列表

在宏语言中处理项目列表非常常见，并且有多种方式可以创建和处理这些列表中的项目（Fehd and Carpenter, 2007）。创建宏变量列表的一种常见方式是使用 SYMPUTX。

以下 DATA 步是某个宏的一部分，该宏创建 SAS 数据集中所有属于同一类型（数值型或字符型）的变量列表。要创建的宏变量的名称将采用 &VARNAME1、&VARNAME2 等值。

```sas
data _null_;
  set sashelp.vcolumn(where=(libname="&upcase(&lib)" &
      memname="&upcase(&mem)" &
      type="&type")) end=eof;
  call symputx('varname'||left(put(_n_,9.)),name,'L');
  if eof then call symputx('varcnt',_n_);
run;
```

通过使用 CATS 函数执行拼接，CALL SYMPUTX 本来可以有所简化。

```sas
call symputx(cats('varname',_n_),name,'L');
```

使用 DATA 步并不是创建带编号宏变量列表的唯一方式，甚至也不一定是最简单的方式。有关 PROC SQL 示例，请参见本节附带的示例代码。

### 更多信息

在 13.5 节中，使用 PROC SQL 步创建宏变量列表。

### 另见

在宏语言中，处理列表有四种主要方式。Fehd 和 Carpenter (2007) 讨论了这些方式。Rozhetskin (2010) 给出了许多清晰而直接的示例，说明如何使用列表处理来完成各种任务。Crawford (2006) 介绍了一个简化列表处理的宏。

## 13.3 通用程序——同一主题的变体

宏语言首先是一种代码生成器。因此，它的优势之一是创建并存储可重用代码。接下来的两节讨论通用化过程。随着你对宏语言越来越熟练，并且对过程本身越来越得心应手，你可能会发现本节中展示的某些步骤会被压缩甚至省略。

### 13.3.1 程序通用化的步骤

由于宏程序可能难以调试，通常更容易从可工作的（非宏）步或程序开始。然后检查代码并使用以下步骤修改它：

-   识别那些在不同使用场景中会发生变化的内容。
-   将这些项目转换为宏语言元素。
-   使用带有合理默认值的命名参数。

```sas
proc means data=advrpt.demog noprint;
  class sex;
  var ht wt;
  output out=stats
    n=
    mean=
    stderr= / autoname;
run;
```

考虑以下简单的 PROC MEANS 步。我们希望将该步通用化，以便能够针对任何数据集以及任何分类变量和分析变量列表进行处理。我们可能还希望允许用户选择该过程是否生成打印输出。代码中的加粗部分是我们需要使用宏语言元素控制的内容。这些是依赖于运行时条件的项目。

```sas
proc means data=&dsn &print;
  class &classlst;
  var &varlst;
  output out=&outdsn
    n=
    mean=
    stderr= / autoname;
run;
```

然后，这些依赖项被转换为宏语言元素，在本例中为宏变量。这些宏变量的值可以通过多种不同方式提供。对于简单、最直接的情况，可以在宏调用中作为参数提供这些值。

宏 %MYMEANS 使用关键字参数来指定宏参数。此外，该宏还执行一些逻辑检查。

```sas
%macro mymeans(dsn=advrpt.demog,
        classlst=sex,
        varlst=ht wt,
        outdsn=stats,
        print=noprint ❶);
proc means data=&dsn
%if &outdsn = %then print; ❷
%else &print; ❸
%if &classlst ne %then %do; class &classlst;%end; ❹
%if &varlst ne %then %do; var &varlst; %end; ❺
%if &outdsn ne %then %do; ❻
  output out=&outdsn n= mean= stderr= / autoname;
%end;
run;
%mend mymeans;
```

-   ❶ 默认情况下不会写入打印输出；但是，如果没有指定汇总数据集 ❷，则会自动生成打印输出。
-   ❷ 用户可以通过将 &PRINT 设置为 PRINT 来同时请求打印输出和汇总数据集。第二个分号用于结束 PROC 语句。
-   ❸ 仅当指定了一个或多个变量时，才会写入 CLASS 和 VAR 语句。此处并非真的需要 %DO 块，但它们消除了使用双分号的需要，例如在 %ELSE ❸ 上使用的那种双分号。
-   ❹ 当提供了汇总数据集的名称时，就会写入 OUTPUT 语句。

以下对 %MYMEANS 宏的调用展示了其灵活性。

这次对 %MYMEANS 的调用将更改数据集和分析变量，使用默认分类变量，并且不会生成打印输出。

```sas
%mymeans (dsn=sashelp.class, varlst=height weight)
```

```sas
%mymeans (outdsn=)
```

这里仅使用该宏的所有标准默认值生成打印输出。

两个系统选项 MAUTOSOURCE 和 SASAUTOS= 用于控制自动调用库的使用。访问自动调用库的能力通过 MAUTOSOURCE 系统选项开启（默认情况下该选项为开启状态）。自动调用库的物理位置使用 SASAUTOS= ❶ 系统选项指定。

```sas
* Default option settings;
options mautosource
    ❶sasautos=sasautos❷;
```

默认情况下，SASAUTOS= 选项的值是一个自动复合文件引用（fileref），其名称也是 SASAUTOS ❷。该文件引用指向多个位置（具体是哪些位置以及有多少个，在某种程度上取决于你的 SAS 版本以及你发布的产品）。这些位置用于存放 SAS 提供的自动调用宏定义。

你可以将自己的宏定义添加至自动调用库：将它们存储在一个或多个位置，然后将这些位置添加到 SASAUTOS= 选项。注意使用的是 FILENAME 语句，而不是 LIBNAME ❸ 语句。在基于目录的系统中，文件引用将指向目录层级，而在 zOS 下则指向分区数据集。

```sas
filename mymacs "<phys path to my macro definitions>";
filename prjmacs "<phys path to the project macro definitions>";
filename comacs "<phys path to the company wide macro definitions>";
options mautosource
    ❶sasautos=(mymacs prjmacs comacs sasautos ❷);
```

唯一的进一步约束是宏名称必须与包含该定义的文件的名称匹配。如果要为宏 %ABC 创建定义，则从 %MACRO ABC 语句到 %MEND ABC 语句应存储在名为 ABC.SAS 的文件中（在 zOS 下则是名为 ABC 的成员名）。在 UNIX 操作系统上，存储宏定义的文件的名称必须全部为小写字符（abc.sas）。

调用 %ABC 宏时，SAS 将按照 SASAUTOS= 选项中指定的位置（从左到右）搜索程序 ABC.SAS。找到该文件后，会包含宏定义，编译从 %MACRO 到 %MEND 的宏定义，然后执行 %ABC 宏。

虽然包含宏定义的文件可以包含除 %MACRO 到 %MEND 语句之外的代码，但这样做并不是好主意。通过分离代码，使给定文件只包含以其命名的宏的定义，宏定义会变得更容易查找和控制。

使用自动调用库时，有几点注意事项需要留意。首先，务必包含自动文件引用 SASAUTOS ❷。否则将导致无法使用 SAS 提供的自动调用宏。其次，务必使用文件引用（fileref）而不是库引用（libref）来指定库位置。即使你指向的是一个位置而不是特定文件，也要使用 FILENAME 语句。虽然使用库引用指定 SASAUTOS= 选项时不会发出错误，但在访问该库时使用库引用 ❸ 会导致问题。

```sas
* WRONG WAY TO SPECIFY THE LIBRARY!!!;
libname ❸ comacs "c:\temp";
options mautosource
    sasautos=(comacs ❸ sasautos ❷);

%silly
```
