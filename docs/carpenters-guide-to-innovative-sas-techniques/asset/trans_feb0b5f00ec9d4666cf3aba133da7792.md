
无论 SAS 的版本如何，也无论 MINOPERATOR 选项的状态如何，都可以通过使用引用函数来屏蔽 IN，使其不被解释为 IN 运算符的助记符。这里使用 %BQUOTE 来屏蔽 &STATE 的解析值，直到表达式求值之后，此时就不会再引起问题。对于这个特定示例，%BQUOTE 还会防止俄勒冈州（OR）和内布拉斯加州（NE）出现解析错误。

```
%if %bquote(&state)=CA %then %put California;
```

### 13.10.2 使用 MINOPERATOR 选项

从 SAS 9.2 开始，你可以选择是否让 IN 运算符可用。选择通过 MINOPERATOR 选项完成（默认是 NOMINOPERATOR）。该选项可以作为系统选项应用，或者——这是我的建议——作为宏语句上的选项应用。

在 13.10.1 节中，宏 %BROKENIN 被展示为在 SAS 9.2 中可正确工作；但是，当 MINOPERATOR 选项打开时，它在 SAS 9.2 中将会失败。与其在系统级别应用 MINOPERATOR，如果在宏级别应用它，你就可以获得更精细的控制程度。在本节剩余示例中，该选项将始终在宏级别设置，并假定系统选项保持关闭（NOMINOPERATOR）。

```
option minoperator;
%macro BrokenIN;
%let state=in;
%if &state=CA %then %put California;
%else %put Not California;
%mend broken;
%brokenin
```

尽管我们通常将字母（IN）称为运算符符号，但 IN 实际上是助记符，而井号（#）才是该运算符的实际符号。如果我们能够关闭助记符并只使用 # 符号，上面讨论的一些混淆就会消失，但目前这并不是一个可选项。

宏 %TESTIN 可用于演示 IN 运算符的使用。这里已设置 NOMINOPERATOR 系统选项 ❶，以模拟默认值（SAS 9.2）。由于我们希望在宏中使用该运算符，所以通过 %MACRO 语句上的 MINOPERATOR 选项 ❷ 将其打开，且仅在执行 %TESTIN 时打开。在此比较中，表达式检查解析后的值是否

```
* system option default value;
option nominoperator; ❶

%macro testIN(dsn=demog) /minoperator; ❷
%if %upcase(&dsn) # AE CONMED DEMOG ❸ %then %do;
%put &dsn count &obscnt(advrpt.&dsn);
%end;
%mend testin;
%testin(dsn=ae)
```

&DSN 位于运算符右侧的可接受值列表 ❸ 中。当值列表用括号括起来时，表达式通常更易读。# 可以替换为助记符。IN 运算符解析为真或假（1 或 0），因此使用隐式的 %EVAL 函数。

```
%upcase(&dsn) in (AE CONMED DEMOG)
```

### 13.10.3 使用 MINDELIMITER= 选项

默认情况下，IN 运算符期望值列表以空格分隔；但是，可以使用 MINDELIMITER= 选项为列表指定替代分隔符。与 MINOPERATOR 选项一样，MINDELIMITER= 选项可以在系统选项级别或宏级别指定，并且再次建议始终在 %MACRO 语句上应用它，而不是在系统级别应用。这里已将 MINDELIMITER= 选项添加到 %MACRO 语句 ❶，以允许使用逗号分隔的值列表 ❷。

```sas
%macro testIN(dsn=demog) /minoperator
    mindelimiter=','; ❶
  %if %upcase(&dsn) in (AE,CONMED,DEMOG) ❷ %then %do;
    %put &dsn count %obscnt(advrpt.&dsn);
  %end;
%mend testin;
%testin(dsn=demog)
```

通过将列表括在括号中并使用 IN 助记符（如这里所做的那样），宏表达式更接近地模仿了 DATA 步的 IN 运算符所使用的语法。

### 13.10.4 这些选项的编译与执行

当使用 MINOPERATOR 和 MINDELIMITER= 的系统选项版本时，理解宏的编译与执行之间的差异很重要。如果你打算在 %MACRO 语句上使用这些选项（正如我所建议的），而不是作为系统选项使用，那么下面讨论的问题不会影响你，因为在编译和执行期间，%MACRO 语句上声明的值都会覆盖系统选项。

### MINDELIMITER= 系统选项

MINDELIMITER= 选项的值在宏编译时设置。此后对该选项的更改不会影响宏的执行。

```sas
options minoperator mindelimiter=','; ❶
%macro testIN(dsn=demog);
  %if %upcase(&dsn) in (AE,CONMED,DEMOG) %then %do;
    %put &dsn count %obscnt(advrpt.&dsn);
  %end;
  %else %PUT &DSN not on the list;
%mend testin;
* change in mindelimiter does not break the macro;
options minoperator mindelimiter=' '; ❷
%testin(dsn=conmed)
```

- ❶ MINDELIMITER= 选项已在宏 %TESTIN 编译之前设置。
- ❷ 在执行之前，MINDELIMITER= 选项的值已改为空白。

尽管 MINDELIMITER= 选项的值已经更改 ❷，%TESTIN 宏仍将正确运行。这意味着，在编译依赖于 MINDELIMITER= 系统选项的宏之前，你必须知道该选项的当前值，或者在编译宏之前显式设置该系统选项。但是，在执行宏时，你不需要知道当前设置。

### MINOPERATOR 系统选项

对于 MINOPERATOR 系统选项，应用的是宏执行时生效的值。无论是 MINOPERATOR 还是 NOMINOPERATOR 在

```
77  options nominoperator; ❽
78  %testin(dsn=comed)
ERROR: Required operator not found in expression:
upcase(&dsn) in (AE,COMED,DEMOG)
ERROR: The macro TEST will stop executing.
```

宏编译期间设置，都无关紧要；但是，如果在调用宏时 NOMINOPERATOR 生效，则宏将失败。这里显示的 LOG 表明，在前一示例 ❼ 中成功执行的宏 %TEST，在 MINOPERATOR 选项关闭 ❽ 时失败。

请记住，如果你始终将这些系统选项的值设置为 %MACRO 语句上的选项，就无需担心它们的当前设置。

## 13.11 使用 MFILE 系统选项

通常，在调试宏时，选项 MPRINT、SYMBOLGEN 和 MLOGIC 足以找到代码中的问题。当宏嵌套时，你还可以使用 MLOGICNEST 和 MPRINTNEST 选项。不过，有时你只是需要一把更大的锤子。MFILE 系统选项为我们提供了另一种查看宏结果的方式。

宏语言主要是一种代码生成器，而 MFILE 系统选项允许我们保存由宏生成的代码。保存的代码将完全不含任何宏引用。这里为演示目的，宏 %PRINTIT 执行一个简单的 PROC PRINT。

```sas
%Macro PRINTIT(dsn,varlist=,obs=);
proc print data=&dsn
  %if &obs ne %then (obs=&obs);
  %if &varlist ne %then var &varlist;;
  run;
%mend printit;

options mprint mfile; ❶
filename mprint ❷ "&path\\sascode\\Chapter13\\E13_11_mfile.sas" ❸;
%printit(dsn=advrpt.demog,varlist=subject lname fname dob,obs=4)
```

- ❶ 为了使用 MFILE 系统选项，还必须打开 MPRINT 选项。
- ❷ 生成的 SAS 代码写入与文件引用 MPRINT 关联的文件（它必须是 MPRINT；你不能选择此文件引用的名称）。

生成的 SAS 代码写入文件（E13_11_mfile.sas ❸），并在所有宏引用和逻辑都已解析并执行后包含如下 PROC PRINT：

```
proc print data=advrpt.demog (obs=4);
var subject lname fname dob;
run;
```

宏引用函数有若干个。每个都略有不同，而且差异往往相当细微。幸运的是，为了屏蔽特殊字符，你不需要完全理解各种引用函数中的每一个。几乎所有的引用需求都可以通过 %BQUOTE 和 %NRSTR 引用函数满足。下表简要总结其中一些函数。

| 引用函数 | 此函数的超能力 |
|---|---|
| %STR | 易于输入——能引用大多数常见特殊字符。 |
| %BQUOTE | 能引用比 %STR 更多的字符。 |
| %NRSTR | 屏蔽 & 和 %，并阻止它们被解析或执行。 |
| %UNQUOTE | 移除宏屏蔽字符。 |

每个返回文本的宏函数（例如 %LEFT、%UPCASE、%TRIM、%SYSFUNC）都有一个引用类似函数（其中一些可能以 Q 开头），它返回屏蔽了特殊字符的文本。这包括宏语言触发符 & 和 %。例如，函数调用 %LEFT(A&P) 会尝试将 &P 解析为宏变量，而引用类似函数（%QLEFT）则不会。无论在使用这些函数之前字符是否已被屏蔽，它们都会在返回文本中被取消屏蔽，除非使用了引用类似函数。

```sas
%let p = proc;
%let store=
   %nrstr( My favorite store is the A&P. );
%put |&store|;
%put %left(&store);
%put %qleft(&store);
```

```text
7  %put |&store|;
   | My favorite store is the A&P. |
8  %put %left(&store);
My favorite store is the A&P.
9  %put %qleft(&store);
My favorite store is the A&P.
```

%NRSTR 允许保留前导和尾随空格，并且还会屏蔽 &P，从而不会尝试将其解析为宏变量。

&STORE 的值包含前导和尾随空格以及一个被屏蔽的 &P。

%QLEFT 将文本左对齐，并允许解析 &P。（&P 被替换为字母 proc）。注意，句点被视为宏变量名称的一部分，并且也会被替换。

%QLEFT 将文本左对齐，但不会移除 A&P 周围的屏蔽字符。

在工作中，我通常倾向于使用 %BQUOTE 和 %NRSTR 引用函数，几乎排除了其他函数。对于文本函数，我的一般规则是使用 Q 对应版本，除非有理由不这样做。

## 另见

Whitlock（2003）介绍并讨论了宏引用的方方面面——如果你是宏引用的新手，可以从这里开始。Rosenbloom 和 Carpenter（2011b）专门讨论了与包含特殊字符的宏变量相关的问题。Carpenter（2004，第 7.1 节）详细讨论了宏引用。

