
理解 SAS 支持语句 113

## 5.1 了解 SAS 语句

在使用特定的 SAS 过程进行数据分析之前，你应该了解几个基础的支持性 SAS 选项和语句，这些语句通常与 SAS 数据分析过程配合使用。本章将为你介绍这些选项和语句。

### 5.1.1 使用 TITLE 和 FOOTNOTE 语句

TITLE 语句指示 SAS 在每个输出页的顶部或过程输出的开头放置一行文本。同样，FOOTNOTE 语句在每个输出页的底部放置行。可以指定多达九行标题或脚注行。例如：

```
TITLE 'title text';
FOOTNOTE 'footnote text';
```

或者

```
TITLEN 'title text';
FOOTNOTEN 'footnote text';
```

其中 n 是于 2 到 9 之间的数字。不带数字的 TITLE 或 FOOTNOTE 语句指定初始的 TITLE 或 FOOTNOTE 行。随后的 TITLE 或 FOOTNOTE 行可以使用 TITLE2、TITLE3 等到 TITLE9；FOOTNOTE2、FOOTNOTE3 等到 FOOTNOTE9 定义。（TITLE 或 FOOTNOTE 与数字之间没有空格）。例如：

```
TITLE 'The first line of the title';
TITLE2 'The second line of the title';
TITLE3 'Several lines skipped, then this title on the fifth line';
FOOTNOTE 'This is a footnote';
FOOTNOTE3 'This is a footnote, line 3'
```

在定义标题或脚注时，可以使用单引号或双引号，但在每个定义中必须保持一致。如果你指定了 TITLE 或 FOOTNOTE，它将用于所有后续的 SAS 输出（即使在提交新的 SAS 程序时，只要你没有退出当前的 SAS 软件程序），直到你重新定义 TITLE 或 FOOTNOTE 行为止。例如，如果你在代码中包含一个 TITLE2 语句，它将抵消之前的任何 TITLE2 或更高优先的标题。脚注的工作方式相同。
你可以使用以下语句取消所有的 TITLE 和 FOOTNOTE 行：

```
TITLE; FOOTNOTE;
```

在 SAS 代码的末尾包含此行是一种良好的编程习惯，可以防止散乱的标题或脚注出现在后续的 SAS 输出中。我们已经将这段代码放在了书中使用的 SAS 程序示例文件的末尾。

## 实例演示

在本示例中，输出是使用两个 SAS 过程（PROCS）创建的。为第一个过程定义了 TITLE，并在第二个过程中进行了更改。

- 1. 打开程序文件 DITLE1.SAS。

```
DATA MYDATA;
INFILE 'C:\SASDATA\EXAMPLE.DAT';
INPUT ID 1-3 GP $5 AGE 6-9 TIME1 10-14 TIME2 15-19
TIME3 20-24;
RUN;
PROC PRINT;
TITLE 'Example SAS programs';
TITLE2 'These are data from the example file.';
TITLE4 'Using the EXAMPLE data set.';
FOOTNOTE 'This is a footnote';
PROC MEANS;
TITLE2 'This is output from PROC Means.';
RUN;
TITLE; FOOTNOTE; TURNS OFF TITLE AND FOOTNOTE;
```

- 2. 运行程序并观察输出。PROC PRINT 的部分输出样本如表 5.1 所示。注意，顶部的第 1、2 和 4 行标题行与代码中定义的标题匹配。脚注出现在底部。

### 表 5.1 显示 PROC PRINT 标题和脚注的输出

> 示例 SAS 程序
这些是来自示例文件的数据。

正在使用 EXAMPLE 数据集。

| Obs | ID | GP | AGE | TIME1 | TIME2 | TIME3 |
|---|---|---|---|---|---|---|---|
| 1 | 101 | A | | 12 | 22.3 | 25.3 | 28.2 |
| 2 | 102 | A | | 11 | 22.8 | 27.5 | 33.3 |
| 3 | 104 | B | | 12 | 22.8 | 30.0 | 32.8 |
| 4 | 110 | A | | 12 | 18.5 | 26.0 | 29.0 |
| 5 | 122 | B | | 9 | 19.5 | 25.0 | 25.3 |
| 47 | 591 | B | | 13 | 23.7 | 32.3 | 34.1 |
| 48 | 593 | B | | 11 | 18.9 | 23.1 | 27.7 |
| 49 | 599 | B | | 9 | 20.5 | 24.8 | 30.3 |
| 50 | 604 | B | | 12 | 22.4 | 27.2 | 31.8 |

这是一个脚注

- 3. 观察 PROC MEANS 的第二个输出表（见表 5.2）。注意，对于此输出，第 2 行的标题根据代码中 PROC MEANS 之前的 TITLE2 语句发生了更改，并且所有更高的标题（TITLE4）都被取消了。

### 表 5.2 显示 PROC MEANS 标题和脚注的输出

示例 SAS 程序
这是来自 PROC MEANS 的输出。

MEANS 过程

| Variable | N | Mean | Std Dev | Minimum | Maximum |
|---|---|---|---|---|---|
| ID | 50 | 374.2200 | 167.49834 | 101.0000 | 604.0000 |
| AGE | 50 | 10.46000 | 2.426132 | 4.0000 | 15.0000 |
| TIME1 | 50 | 21.26800 | 1.71695 | 17.0000 | 24.0000 |
| TIME2 | 50 | 27.44000 | 2.659063 | 21.3000 | 32.0000 |
| TIME3 | 50 | 30.49200 | 3.025542 | 22.7000 | 35.9000 |

这是一个脚注

- 4. 在代码中放置一行内容为“This is title”的 TITLE 行，或者在 PROC MEANS 之前根据 TITLE2 语句更改第 2 行的标题，并取消所有更高的标题（TITLE4）。

（注：原文后半部分存在大量重复和乱码，翻译时已根据语意进行逻辑梳理，保留了核心技术指令说明。）
