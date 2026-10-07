
![](img/6f22e781b7ad899a8ef005cc7e22e7e0_92_2.png)

选择“完成”，SAS 将将数据写入 Excel 电子表格（或选择“下一步”将 `PROC EXPORT` 语句写入文件）。在这里，文件名为 `C:\books\learning` 文件夹下的 `Sales.xlsx`，表名为 `Table1`。

你可以通过 `XLS` 或 `XLSX` 引擎将 Excel 电子表格视作 SAS 数据集。例如，假设你想对 `C:\books\learning` 文件夹中名为 `Wages.xls` 的电子表格中的数据运行 SAS 过程。以下 `LIBNAME` 语句允许直接访问此电子表格：

```sas
libname Read 'C:\books\learning\Wages.xls';
```

你现在可以访问该文件中的任何工作表。此特定的电子表格包含两个工作表：`Temporary` 和 `Permanent`。假设你想计算 `Permanent` 工作表中 `Wage` 和 `Hours Worked` 的平均值。以下是执行此操作的 SAS 语句：

## 程序 6.3：使用 XLSX 读取电子表格

```sas
title "Statistics from Spreadsheet"
libname Read 'C:\books\learning\Wages.xls';
proc means data=Read.'Permanent$'
    var Wage Hours_Worked;
run;
```

程序中有几个重要的点需要注意。首先，由于 SAS 要求工作表名称后跟一个美元符号，而 SAS 数据集名称中通常不允许出现美元符号，你需要使用字面量（literal）来实现此。在程序 6.3 中，你将工作表名称（`Permanent$`）放在单引号中，并随后跟上一个允许你将无效字符作为 SAS 名称一部分的表示法。注意：为了让此命名字面量生效，你必须将 `VALIDNAME` 设置为 `ANY`。要做到这一点，请提交以下语句：`validvarname=any;`

接下来，记住 `Hours Worked` 不是一个合法的 SAS 名称，规则是 SAS 会用下划线替换空格。因此，你需要将此列命名为 `Hours_Worked`。这里是 SAS 输出：

图 6.13：`PROC MEANS` 的输出

| Variable | Mean |
|---|---|
| Wage | 2560 |
| Hours_Worked | 37.2 |

使用 `OBS=n` 数据选项是检查大型数据集数据值的非常有用的方法。通过这种方法，我们可以确保进度正确，并且你可以将 `OBS=n` 数据集选项与 `FIRSTOBS=m` 选项结合。`FIRSTOBS=m` 值定义你想要处理的第一条观测；`OBS=m` 选项是你想要处理的最后一条观测。如果你想在库 `libref` 的一个名为 `Verbig` 的大型 SAS 数据集中列出第 100 到 110 条观测值，使用 `OBS=LASTOBS` 也是一个好主意。你可以这样组合 `FIRSTOBS` 和 `OBS=` 选项：

## 程序 6.2：今天使用 FIRSTOBS 和 OBS= 选项

```sas
title "Observations 100 through 110 in VERBIG";
proc print data=Project.Verbig(firstobs=100 obs=110);
run;
```

程序 6.2 产生一个包含 11 条观测的列表（从第 100 条观测到第 110 条观测）。

使用 Enterprise Guide 或 SAS Studio 导入 Excel 工作表更加简单。例如，使用 SAS Studio 时，你不需要选择输入格式——它会查看文件扩展名（例如 `XLS` 或 `XLSX`）并自动选择正确的导入方法。

## 6.4 使用 ODS 将 SAS 输出转换为 CSV 文件

使用 `ODS`（Output Delivery System）将 SAS 输出导出到 CSV 文件是一种常见需求，特别是当你需要将数据共享给不支持 SAS 的软件时。

你可以使用 `ODS CSV` 语句来实现此功能。首先通过 `ODS CSV` 指定文件路径，然后运行你的过程，最后使用 `ODS CLOSE;` 关闭输出流。

以下是将一个数据集导出为 CSV 的示例：

```sas
ods csv file='C:\books\learning\output.csv';
proc print data=Wages_Permanent;
run;
ods close;
```

执行上述代码后，`C:\books\learning` 文件夹下将生成一个 `output.csv` 文件。你可以用任何文本编辑器或电子软件打开它。

## 6.5 使用 ODS 将 SAS 输出转换为 CSV 文件

使用 `ODS`（Output Delivery System）将 SAS 输出导出到 CSV 文件是一种常见需求，特别是当你需要将数据共享给不支持 SAS 的软件时。

你可以使用 `ODS CSV` 语句来实现此功能。首先通过 `ODS CSV` 指定文件路径，然后运行你的过程，最后使用 `ODS CLOSE;` 关闭输出流。

以下是将一个数据集导出为 CSV 的示例：

```sas
ods csv file='C:\books\learning\output.csv';
proc print data=Wages_Permanent;
run;
ods close;
```

执行上述代码后，`C:\books\learning` 文件夹下将生成一个 `output.csv` 文件。你可以用任何文本编辑器或电子软件打开它。

# 第 6 章：从 Excel 电子表格读取和写入数据

## 程序 6.1：使用 PROC PRINT 列出数据集前四条观测

```sas
title "The First Four Observations of Wages_Permanent";
proc print data=Wages_Permanent (obs=4);
run;
```

以下是输出：

图 6.7：程序 6.1 的输出

# Wages_Permanent 的前四条观测

| Obs | Subject | Date | Hours | Rate_Per_Hour | Wage |
|---|---|---|---|---|---|
| 1 | M75 | 04APR2006 | 33 | 54 | $1,782.00 |
| 2 | F399 | 23AUG2006 | 56 | 75 | $4,200.00 |
| 3 | M766 | 11MAY2006 | 12 | 75 | $900.00 |
| 4 | M287 | 28FEB2006 | 40 | 50 | $2,000.00 |

SAS 根据 Excel 的列标题创建了变量名。它将列标题中的无效字符（如逗号、空格）替换为下划线 `_`。使用 SAS 资源管理器或 `PROC CONTENTS` 查看此数据每个变量的类型（字符或数值）和长度也是一个好主意。你可能需要使用 `PROC DATASETS` 修改一个或多个变量的格式，或者编写一个短的 `DATA` 步对你希望转换为数值型但由于某种原因仍为字符型的变量执行字符到数值的转换。

使用 `OBS=n` 数据选项是检查大型数据集数据值的非常有用的方法。通过这种方法，我们可以保持进度，并且你可以将 `OBS=n` 数据集选项与 `FIRSTOBS=m` 选项结合。`FIRSTOBS=m` 值定义你想要处理的第一条观测；`OBS=m` 选项是你想要处理的最后一条观测。如果你想在库 `libref` 的一个名为 `Verbig` 的大型 SAS 数据集中列出第 100 到 110 条观测值，使用 `OBS=LASTOBS` 也是一个好主意。你可以这样组合 `FIRSTOBS` 和 `OBS=` 选项：

### 程序 6.2：使用 FIRSTOBS 和 OBS= 选项

```sas
title "Observations 100 through 110 in VERBIG";
proc print data=Project.Verbig(firstobs=100 obs=110);
run;
```

程序 6.2 产生一个包含 11 条观测的列表（从第 100 条观测到第 110 条观测）。

使用 Enterprise Guide 或 SAS Studio 导入 Excel 工作表更加简单。例如，使用 SAS Studio 时，你不需要选择输入格式——它会查看文件扩展名（例如 `XLS` 或 `XLSX`）并自动选择正确的导入方法。

## 6.3 从 SAS 数据集创建 Excel 电子表格

在离开这里之前，让我们看看如何使用导出向导（Export Wizard）将 SAS 数据集转换为 Excel 电子表格。从“文件”菜单中，选择“导出数据”，然后选择“Microsoft Excel”。

假设你想将 `Sales` 数据集（位于 `C:\books\learning` 文件夹中）转换为 Excel 电子表格。首先，你需要确保你拥有该文件夹的库引用。例如，执行以下语句：

```sas
libname Learn 'C:\books\learning';
```

然后，按照以下步骤操作：

- 从“文件”菜单，选择“导出数据”。

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_91_0.png)

在下一个屏幕，输入 `LIBENAME` 和你想导出的 SAS 数据集名称（此例为 `Sales`），并点击“下一步”。

## 图 6.9：命名库和数据集名称

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_91_1.png)

下一步，从下拉菜单中选择 Microsoft Excel。

图 6.10：选择 Microsoft Excel

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_92_0.png)

你可以浏览或输入 Excel 电子表格的名称。

图 6.11：命名 Excel 工作簿

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_92_1.png)

你也可以命名特定的表。

图 6.12：提供表名

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_92_2.png)

选择“完成”，SAS 将将数据写入 Excel 电子表格（或选择“下一步”将 `PROC EXPORT` 语句写入文件）。在这里，文件名为 `C:\books\learning` 文件夹下的 `Sales.xlsx`，表名为 `Table1`。

你可以通过 `XLS` 或 `XLSX` 引擎将 Excel 电子表格视作 SAS 数据集。例如，假设你想对 `C:\books\learning` 文件夹中名为 `Wages.xls` 的电子表格中的数据运行 SAS 过程。以下 `LIBNAME` 语句允许直接访问此电子表格：

```sas
libname Read 'C:\books\learning\Wages.xls';
```

你现在可以访问该文件中的任何工作表。此特定的电子表格包含两个工作表：`Temporary` 和 `Permanent`。假设你想计算 `Permanent` 工作表中 `Wage` 和 `Hours Worked` 的平均值。以下是执行此操作的 SAS 语句：

## 程序 6.3：使用 XLSX 读取电子表格

```sas
title "Statistics from Spreadsheet"
libname Read 'C:\books\learning\Wages.xls';
proc means data=Read.'Permanent$'
    var Wage Hours_Worked;
run;
```

程序中有几个重要的点需要注意。首先，由于 SAS 要求工作表名称后跟一个美元符号，而 SAS 数据集名称中通常不允许出现美元符号，你需要使用字面量（literal）来实现此。在程序 6.3 中，你将工作表名称（`Permanent$`）放在单引号中，并随后跟上一个允许你将无效字符作为 SAS 名称一部分的表示法。注意：为了让此命名字面量生效，你必须将 `VALIDNAME` 设置为 `ANY`。要做到这一点，请提交以下语句：`validvarname=any;`

接下来，记住 `Hours Worked` 不是一个合法的 SAS 名称，规则是 SAS 会用下划线替换空格。因此，你需要将此列命名为 `Hours_Worked`。这里是 SAS 输出：

图 6.13：`PROC MEANS` 的输出

| Variable | Mean |
|---|---|
| Wage | 2560 |
| Hours_Worked | 37.2 |

## 图 6.15：在导航窗中选择任务和工具 81

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_96_0.png)

这将允许你访问子菜单，包括“导入数据”。

## 图 6.16：选择导入数据

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_96_1.png)

你可以从列表中拖动文件，或点击“选择文件”来选择要导入的文件。

图 6.17：将文件拖入“拖放放置区域”或点击“选择文件”

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_97_0.png)

选择你想要导入的文件。记住，此文件要么位于默认共享文件夹（`SASUniversity\MyFolders`），要么位于你在虚拟机上创建的另一个共享文件夹。

图 6.18：选择文件

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_97_1.png)

SAS Studio 将根据文件扩展名（例如 `XLS` 或 `XLSX`）自动使用正确的导入方法。

## 第 6 章：从 Excel 电子表格读写数据 83

图 6.19：点击运行图标

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_98_0.png)

你将获得为 SAS 数据集和库命名的选择。完成后，点击运行图标。

SAS Studio 将自动显示 `PROC CONTENTS` 的输出，以便你可以查看所有变量的变量名、类型和存储长度。

图 6.20：变量和属性的部分列表

| Variable | Type | Len | Format | Informat | Label |
|---|---|---|---|---|---|
| 8 | Final | Num | 8 | BEST. | Final |
| 2 | ID | Num | 8 | BEST. | IO |
| 5 | Midterm | Num | 8 | BEST. | Midterm |
| 1 | Name | Char | 10 | $10. | Name |
| 3 | Quiz1 | Num | 8 | BEST. | Quiz1 |
| 4 | Quiz2 | Num | 8 | BEST. | Quiz2 |
| 6 | Quiz3 | Num | 8 | BEST. | Quiz3 |
| 7 | Quiz4 | Num | 8 | BEST. | Quiz4 |

希望这一短节能让你信服 SAS Studio（无论是否带有 SAS University Edition）是易于使用的。

## 6.7 习

奇数题的解答位于书末。所有题目的解答均供教授参考。如果你是教授，请访问书籍的配套网站 `support.sas.com/cody` 了解如何获取所有题目的解答。

- 1. 使用 SAS 资源器窗口（或 Enterprise Guide 或 SAS Studio 中的导入功能）读取电子表格 `drugtest.xls` 并将其转换为名为 `Drugtest` 的临时 SAS 数据集。使用 `PROC PRINT` 列出该数据集中的观测值。

- 2. 运行以下程序创建一个 CSV 文件。将程序中指定的文件夹替换为你选择的文件夹：

```sas
data Soccer:
input Team : $20. Wins Losses;
datalines;
Reading 20 3
Raritan 10 10
Branchburg 3 18
Somerville 5 18
;
options nodate nonumber;
title;
ods list close;
ods csv file='C:\books\learning\Soccer.csv';
proc print data=Soccer noobs;
run;

ods csv close;
ods listing;
```

在你的电脑上打开 Excel 并打开 CSV 文件（你必须更改文件类型为 .csv）。它看起来应该是这样的：

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_99_0.png)

使用“文件►另存为”下拉菜单将其保存为电子表格并命名为 `Soccer.xls`。

现在，使用 SAS 导入向导将此电子表格转换为名为 `Soccer` 的永久 SAS 数据集，并放在你选择的文件夹中。

- 3. 使用 `XLS` 引擎读取问题 2 中创建的 *soccer.xls* 文件。表名为 `SOCCER`。（你需要使用名称常量 `'SOCCER$''n` 来读取此文件。）

# 第 7 章：执行条件处理

7.1 引言 ................................................................................................ 87

7.2 IF 和 ELSE IF 语句 ................................................................ 87

7.3 子集 IF 语句 ....................................................................................... 90
