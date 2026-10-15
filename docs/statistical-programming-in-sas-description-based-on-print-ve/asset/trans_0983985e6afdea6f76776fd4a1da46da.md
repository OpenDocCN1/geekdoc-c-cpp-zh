

字母、数字或下划线。 在不同应用程序之间传输数据集时要小心（例如，从 SAS 到 Excel 或从 Excel 到 SAS，或从 R 到 SAS）。 一个系统中的变量名在另一个系统中可能无效，并在导入数据时导致奇怪的名称。 使用有意义但不会让人打字麻烦的命名约定。 例如，我认为 body_weight 或 BodyWeight 比 X34 更可取，但我不认为我会使用 body_weight_in_kilograms。 在 Display 1.1 中，loggnp 和 pcturban 在含义上很清楚，而且打字相对简单。 关键思想是，使用合理的变量名可以帮助使你的程序具有自文档化功能。

## 1.2.3 不要在程序语句中只使用大写字母（尽管适度使用是合理的）

在电子邮件中使用全大写被视为大喊大叫。 在程序中，我认为全大写会使阅读变得更困难，从而更难调试。 许多程序员喜欢看到变量名、数据集名以及特定的 SAS 名称（如格式、函数等）以大写形式显示。 看下面的代码：

```
PROC REG DATA=COUNTRY;
    TITLE "LITER AND LOGGNP AS PREDICTORS OF LIFE EXPECTANCY OF WOMEN";
    MODEL LIFEWOM = LITER LOGGNP/ TOL VIF COLLINOINT;
    OUTPUT OUT=NEW P=YHAT R=RESID;
RUN;
```

现在，看这段代码：

```
proc reg data=COUNTRY;
    title "LITER and LOGGNP as predictors of life expectancy of women";
    model LIFEWOM = LITER LOGGNP/ tol vif collinoint;
    output out=new p=yhat r=resid;
run;
```

然后，看这段代码：

```
proc reg data=country;
    title "liter and loggnp as predictors of life expectancy of women";
    model lifewom = liter loggnp/ tol vif collinoint;
    output out=new p=yhat r=resid;
run;
```

我认为这三个示例中全大写版本的代码可读性最差。 在另外两个示例中，在大小写混合或全部小写之间的偏好是个人口味问题。

## 1.2.4 缩进自然在一起的程序语句

通过缩进程序语句，你可以突出显示与过程或语句一起出现的行。 或者，你可以识别在循环或条件执行语句中一起执行的代码块。 （关于 DO-END 和 IF-THEN 构造的内容将在后面的章节中详细介绍。）比较以下两个摘自 Display 1.1 的代码段。 在第一种情况下，代码以全大写编写且没有缩进：

```
PROC PRINT DATA=COUNTRY; RUN;
PROC REG DATA=COUNTRY;
TITLE "LITER AND LOGGNP AS PREDICTORS OF LIFE EXPECTANCY OF WOMEN";
MODEL LIFEWOM = LITER LOGGNP/ TOL VIF COLLINOINT;
OUTPUT OUT=NEW P=YHAT R=RESID; RUN;
```

这是第二种情况：

```
proc print data=country;
run;

proc reg data=country;
    title "LITER and LOGGNP as predictors of Life expectancy of women";
    model lifewom = liter loggnp/ tol vif collinoint;
    output out=new p=yhat r=resid;
run;
```

在第二种情况下，很明显调用了两个过程：PROC PRINT 和 PROC REG（以及随 PROC REG 发出的系列语句和命令）。 我认为非大写版本更易于阅读，并且缩进和插入的空白行使你能够轻松识别每个过程所附带的内容。

## 1.3 SAS 程序结构

现在，我已经花了一些时间在编程的美学上，并用一个示例 SAS 程序来吸引你，是时候描述 SAS 程序的基本组成部分了。 SAS 程序通常存储为带有 .sas 扩展名的文件。 在批处理环境中运行 SAS 程序会生成另外两个文件——.log 文件（包含描述 SAS 程序执行期间发生情况的消息）和列表文件（文件扩展名为 .listing、.lst 或 .lis）。 如果你使用程序编辑器以交互方式运行 SAS（例如在 Windows 上），那么你就有相应的窗口——编辑器（类似于 .sas 文件）、日志和输出（类似于 .listing 文件）。

SAS 程序有一系列 DATA 步和过程步（称为 PROCs）。 DATA 步以 DATA 语句开始，后跟一组定义数据源、要读取的变量、可能分配的格式、转换、操作等的语句。 过程步以 PROC 语句开始，后跟过程名称。 过程具有语句和选项，每个语句的结尾以分号结束。 程序中的每个语句都以分号结束。 分号是 SAS 程序中的保留字符，分号的遗漏可能是导致 SAS 程序无法运行的最常见错误。

DATA 步用于命名数据集、命名数据集中的变量、将变量标识为数值或字符、标识 SAS 输入数据的来源，并为程序提供读取输入数据文件的方向。 与变量名一样，数据集名最长可达 32 个字符，且命名限制相似。 数据可能在程序中使用 DATALINES 输入，或使用 INFILE 语句从外部文件输入，或从永久保存的 SAS 数据集输入（使用 LIBNAME 或 SET 语句）。

在 Display 1.1 中，我定义了一个名为 country 的 SAS 数据集，其中包含从存储在由宏变量定义的两个目录之一中的外部数据文件 country.data 读取的变量。 （有关宏变量的更多信息，请参阅第 10 章。）该数据集具有以下变量——NAME、AREA、POPNSIZE、PCTURBAN、LANG、LITER、LIFEMEN、LIFEWOM 和 PCGNP。 这些变量的值在输入数据文件中以空格分隔。 其中两个变量——NAME 和 LANG——是字符变量，在 INPUT 语句中在其名称后用 $ 表示。 变量可以在 DATA 步中进行转换或创建新变量。 赋值语句 logarea=log10(area); 创建一个新变量，即 country 数据集中 AREA 变量的以 10 为底的对数。 第 2 章更详细地讨论了导入数据。 第 8 章讨论了作为 DATA 步编程的一部分创建新变量或重新编码变量。

过程步很容易通过在其前面出现的 PROC 语句来识别。 （如果你对计算历史感兴趣，请回顾 PL/I 编程结构。 一段时间，SAS 是一个内部程序使用 PL/I 和 FORTRAN 的产品。 现在它的核心是 C 代码。）SAS 过程可用于生成描述性统计（例如，UNIVARIATE、MEANS、FREQ），或拟合模型（例如，REG、GLM、GENMOD、PHREG），或生成图形显示（例如，SGPLOT、GMAP），或操作和处理数据集（例如，IMPORT、CONTENTS）。

SAS 过程的一般语法为：

```
PROC name DATA=dsn;
    statement 1;  /* often like a subcommand */
    statement 2;
run;
```

### 建议：在 PROC 步中显式命名要使用的 SAS 数据集。

你应该使用 DATA=DSN 选项显式命名在 PROC 步中进行分析的 SAS 数据集。 SAS 在调用 PROC 时使用最后创建的数据集作为默认值。 如果你有长程序，其中数据集被输入、创建、合并、从 PROC 输出等，那么你会很高兴你遵循了这一建议。

### 建议：在每个 DATA 步和 PROC 步后插入 RUN 语句。

始终以 RUN 语句结束 DATA 或 PROC 步的习惯会使 SAS 日志更易于阅读并有助于调试。 将 RUN 语句缩进以使其与关闭的 DATA 或 PROC 步对齐是有帮助的。 （我的同事 Kathy Roggenkamp 断言，遵循这些建议会让你成为一个细心且有知识的程序员，我同意。）一些公司要求对编程代码进行质量保证审查，其中分析师会检查你的代码。 仔细遵守这些建议，加上注释，会使代码更有可能满足审查标准。

Display 1.1 中的示例包含三个 PROC 步。 第一个过程，PROC PRINT，列出 country 数据集中的信息，包括从外部数据文件导入的变量的值和新变量。 第二个过程，PROC REG，拟合多元回归模型。 第三个过程，PROC SGPLOT，生成带有两个拟合叠加的散点图。

某些过程需要额外的语句。 例如，SGPLOT 过程需要至少一个绘图语句（例如，SCATTER、REG、LOESS、HBAR）伴随：

