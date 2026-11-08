

- 8. TITLE1 在调用该例程的 DATA 步之前定义；但是，该标题将不会提供给由 PRNTCRIT 例程执行的宏。

- 9. PRNTCRIT 例程使用来自 ADVRPT.DSNCONTROL 数据集的三个变量进行调用。例程调用中的变量必须与它们定义的顺序相同 ❷。对于传入数据集中的每个观测，都会调用 PRNTCRIT 例程。该例程调用并执行宏 %PRINTIT。与 CALL EXECUTE 例程（将宏调用推入堆栈）不同，%PRINTIT 将立即执行。

- 10. TITLE1 会被遵守，但 TITLE2 将未定义。

由于函数和例程会被编译，我们不能在函数定义中直接使用宏调用。如果我们尝试像这里所示的那样直接指定宏调用，那么 %PRINTIT 会在 PRNTCRIT 例程被编译时执行。

```sas
proc fcmp outlib=advrpt.functions.utilities;
subroutine prntcrit(dsn$, kvar $,cvar $);
    %printit(dsn,kvar,cvar);
. . . . . .
```

像这样的宏调用将用于生成例程或函数代码。应在函数执行期间执行的宏应使用 RUN_MACRO 函数来指定，如上所示。

## 更多信息

DQUOTE 函数在 3.6.7 节中介绍。

## 参见

《Carpenter 的 SAS® 宏语言完全指南（第 2 版）》（Carpenter, 2004）中的第 8 章讨论了在编译代码上下文中宏和宏变量的使用。

### 15.2.4 查看函数定义

用户自定义函数不会出现在 SASHELP.VFUNC 视图或 DICTIONARY.FUNCTIONS 表中。但是，在 Windows 下，您可以通过 FCMP 函数编辑器查看可用函数列表及其属性。

要启动此编辑器，请转到“解决方案”→“分析”→“FCMP 函数编辑器”。可用数据集及其包含的函数的列表显示在左侧窗格中。选择某个函数会弹出编辑器对话框，您可以在其中查看函数定义的详细信息。

![](img/4b16455363806a3241267bf9f49ba5d1_512_0.png)

### 15.2.5 删除函数

虽然函数和例程存储在数据集中，但您不能使用标准数据管理技术来删除某个函数或例程实例。幸运的是，FCMP 过程提供了 DELETEFUNC 和 DELETESUBR 语句，可用于此目的。

就本示例而言，我们假设函数 START 的一个版本已存储在两个不同的位置（两个不同的数据集）。多个数据集的搜索顺序是*从右到左*（这与跨库搜索的顺序相反，例如格式、自动调用）。START 函数将被编写为返回指定间隔类型的第一个日期。

```sas
proc fcmp outlib=work.funcs.dates; ❶
   function start(int$,date);
      return(intck(int,date,0,'b'));
   endsub;
run;
proc fcmp outlib=advrpt.functions.dates; ❷
   function start(int$,date);
      return(intnx(int,date,0,'b')); ❸
   endsub;
run;
options cmplib=(advrpt.functions work.funcs ); ❹
```

- 1. 建立一个临时位置来保存 START 函数。不幸的是，此函数使用 INTCK 函数被错误地指定，将会失败。
- 2. 指定用于收集 DATES 包中函数的永久数据集。

❸ 使用 INTNX 函数的正确版本 START 存储在永久位置。

❹ CMPLIB 选项指定将首先搜索 WORK.FUNCS 数据集，这意味着错误的 START 函数版本 ❶ 将被找到并使用。

我们需要能够从 WORK.FUNCS.DATES 中删除 START 的错误定义。这可以使用 DELETEFUNC 语句来完成。

```sas
proc fcmp outlib=work.funcs.dates;
    deletefunc start; ❻
run;
```

❺ 调用 PROC FCMP 时，OUTLIB 选项指向包含 START 错误定义的包。

❻ 然后可以使用 DELETEFUNC 语句删除特定函数。

使用上面定义 ❹ 的函数库，ADVRPT.FUNCTIONS.DATES 中的 START 版本现在将是唯一可用的版本。

```sas
data list;
  do d = '01jan2010'd to '05feb2010'd;
    styr = start('year',d); ❼
    stmo = start('month',d); ❽
    output;
  end;
  format d styr stmo date9.;
run;
```

❼ START 函数返回包含 D 中存储日期的年份的第一天。

❽ START 函数返回包含 D 中日期的月份的第一天。

## 更多信息

您还可以使用 FCMP 函数编辑器删除函数和例程（参见 15.2.4 节）。

## 15.3 将 RTF 作为数据读取

RTF 是微软公司于 20 世纪 80 年代末开发的一种专有文档文件格式。与 MS Word 的 .DOC 二进制文件不同，RTF 文件可以被文本编辑器读取。这意味着如果我们把 RTF 文件当作文本处理，就可以使用 SAS 将 RTF 文件作为数据读取和写入，这为使用 SAS DATA 步和 SAS 宏语言带来的强大功能和灵活性打开了大门。

本节中的示例通过填写空白来修改一份“临床试验报告统一标准”（CONSORT）流程图。

## 参见

这些具体示例在 Carpenter 和 Fisher（2011）中有更详细的介绍。

### 15.3.1 RTF 图表补全

CONSORT 表的布局取决于研究设计，包括研究组（ARMS）的数量和研究阶段。然而，本节讨论的技术完全独立于研究设计。此过程的第一步是创建 CONSORT 表的模板形式。该 RTF 表将包含所有需要的信息，并带有空白字段。此图显示了 CONSORT 表的“入组”（Enrollment）部分，该部分将显示受试者数量及其相对于研究的状态。通常，N= 值在确定后会被手工填写。

![](img/4b16455363806a3241267bf9f49ba5d1_514_0.png)

### 15.3.2 模板准备

模板通过使用唯一代码填写每个单独字段来为 SAS 使用做好准备。在这里，前六个字段的唯一代码是 TOTASSESSED、TOTEXCL、INELIG、DECLIN、EXCLOTH 和 NRAN。就我们的目的而言，我们假设这些名称在表中不会在其他地方出现。除了唯一性之外，您选择的代码并不重要，但对于更复杂的表，字段代码名称可用于帮助确保值被插入到正确的位置。

![](img/4b16455363806a3241267bf9f49ba5d1_514_1.png)

### 15.3.3 RTF 作为数据

幸运的是，我们几乎不需要了解 RTF 代码，就可以使用 SAS 处理它。快速查看上一节中生成该图的部分 RTF 代码，可以看到一种大多不可读的文本语言。然而，仔细检查会发现我们指定的关键字之一（DECLIN）。

```text
\par }{\rtlch\fcs1 \af0\afs16 \ltrch\fcs0 \f3\fs16\lang0\langfe1033\langnp0
\fs16\lang4105\langfe1033\langnp15\insrsid260155\harchdist516310 }{\rt
\f1\fs20\lang4105\langfe1033\langnp15\insrsid519091\loch\fcs1 \fcs
\par }{\rtlch\fcs1 \af0\afs16 \ltrch\fcs0 \f3\fs16\lang0\langfe1033\langnp0
```

我们的方法是让 SAS 读取 RTF 文本字符串，找到相应的代码，用感兴趣的值替换这些代码，然后写回修改后的 RTF 文本字符串。搜索和替换操作将使用 TRANSTRN 函数处理，该函数将第二个参数的所有出现位置替换为第三个参数。就我们的目的而言，每个代码应该只出现一次。

用于读取和写入 RTF CONSORT 表的 DATA 步相当简单。

```sas
filename confile1 "C:\temp\CONSORT_Diagram1.rtf";
filename confile2 "C:\temp\CONSORT_Diagram2.rtf";

data _null_;
  infile confile1 lrecl=3000;
  input;
  _infile_ = transtrn(_infile_,'TOTASSESSED','345');
  _infile_ = transtrn(_infile_,'TOTEXCL','56');
  _infile_ = transtrn(_infile_,'INELIG','35');
  _infile_ = transtrn(_infile_,'DECLIN','17');
  _infile_ = transtrn(_infile_,'EXCLOTH','4');
  _infile_ = transtrn(_infile_,'NRAN','289');
  file confile2 lrecl=3000;
  put _infile_;
run;
```

RTF 没有固定的最大记录长度；但是，长度通常低于 500 个字符。这里将 LRECL 设置为 3000——以防万一。传入的 RTF 文件由 fileref CONFILE1 指定。新版 CONSORT 表写入 CONFILE2 fileref 指定的文件中。

_INFILE_ 我们将每个 RTF 行读作一个完整的实体。然后对这个字符串进行搜索并替换相应的代码。在此示例中，TRANSTRN 函数将文本“TOTASSESSED”替换为我们提供的相应数字（345）。在左侧的图中，我们可以看到在模板版本表中使用的占位符代码已被 SAS 程序中提供的值替换。在上面引用的论文（Carpenter 和 Fisher, 2011）中，展示了提供自动化元数据驱动编码解决方案的宏代码。

![](img/4b16455363806a3241267bf9f49ba5d1_515_0.png)

