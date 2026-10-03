
## SAS 程序示例

以下代码创建数据集 `work.NewSalesEmps`，从 `newemps.csv` 文件中读取数据：

```sas
data work.NewSalesEmps;
  length First_Name $ 18 Job_Title $ 25;
  Last_Name $ 12;
  infile 'newemps.csv' dlm=',;
  input First_Name $__NameSales_
;
```

```sas
data work.NewSalesEmps;
  length First_Name $ 12
  Last_Name $ 18 Job_Title $ 25;
  infile 'newemps.csv' dlm=',;
  input First_Name & Last_Name &
_Title
run;
```

执行上述代码后，日志窗口显示以下信息：

```
NOTE: The infile 'newemps.csv' is: File=workshop\newemps.csv, RECLEN=256
NOTE: 71 records were read from infile 'newemps.csv'.
The minimum record length was 28.
The maximum record length was 37.
NOTE: The data set WORK.NewSalesEmps has 71 observations and 4 variables.
```

使用 `PROC PRINT` 过程打印数据集：

```sas
proc print data=work.NewSalesEmps;
run;
```

日志窗口显示：

```
NOTE: 71 observations read from the data set WORK.NewSalesEmps.
```

### 输出窗口

#### PROC PRINT 输出

| Obs | First_Name | Last_Name | Job_Title | Salary |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Satyam | Denny | Sales Rep. II | 26790 |
| 2 | Monics | Klusch | Sales Rep. IV | 30890 |
| 3 | Kevin | Lyon | Sales Rep. I | 26965 |
| 4 | Petra | Ieyang | Sales Rep. II | 27460 |
| 5 | Marina | Ieyang | Sales Rep. II | 29715 |
| 6 | Shani | Duck | Sales Rep. II | 25795 |
| 7 | Michael | Wilson | Sales Rep. I | 26810 |
| 8 | Andrew | Lebanon | Sales Rep. II | 27465 |
| 9 | Vincent | Eastley | Sales Rep. III | 26985 |
| 10 | Nancy | Barbis | Sales Rep. III | 30265 |
| 11 | Vey | Rull | Sales Rep. II | 26650 |
| 12 | Narel | James | Sales Rep. III | 29990 |
| 13 | Jerry | Snellings | Sales Rep. II | 26465 |
| 14 | Leonid | Karavdic | Sales Rep. II | 27860 |

#### PROC MEANS 输出

The MEANS Procedure
Analysis Variable : Salary

| Job_Title | Obs | N | Mean | Std Dev | Minimum | Maximum |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Sales Rep. I | 21 | 21 | 26418.81 | 713.18948 | 25275.00 | 27475.00 |
| Sales Rep. II | 9 | 9 | 26902.22 | 592.948273 | 26080.00 | 27860.00 |
| Sales Rep. III | 11 | 11 | 29345.91 | 989.431156 | 28025.00 | 30785.00 |
| Sales Rep. IV | 6 | 6 | 31215.00 | 545.497709 | 30305.00 | 31865.00 |
| Temp. Sales Rep. | 24 | 24 | 26265.83 | 732.648069 | 25020.00 | 27480.00 |

## 2.04 多选题投票

你将与哪些操作环境使用 SAS？

- a. Windows
- b. UNIX
- c. z/OS (OS/390)
- d. 其他
- e. 未知

## 使用 SAS 窗口环境提交 SAS 程序 – Windows

- 启动会话。
- 包含并提交 SAS 程序。
- 检查结果。
- 使用帮助功能。

### 启动会话

1. 双击 SAS 图标启动你的 SAS 会话。

调用 SAS 的方法取决于你的操作环境以及任何生效的自定义。

### 包含并提交程序

1. 要将 SAS 程序打开到你的 SAS 会话中，请选择**文件** ⇨ **打开程序**，或点击并选择要包含的文件。要打开程序，你的增强编辑器（Enhanced Editor）必须处于激活状态。

你也可以发布 `INCLUDE` 命令将程序打开（包含）到你的 SAS 会话中。

a. 在增强编辑器激活状态，在命令行输入 `include` 以及包含程序的文件的文件名。
b. 按回车键（`ENTER`）。

程序被包含在增强编辑器中。

```sas
data work.NewSalesEmps;
  length First_Name $ 12
  Last_Name $ 18 Job_Title $ 25;
  infile 'newemps.csv' dlm=',;
  input First_Name & Last_Name &
_Title
; Salary;
run;

proc print data=work.NewSalesEmps;
run;

proc means data=work.NewSalesEmps;
  class Job_Title;
  var Salary;
run;
```

你可以使用增强编辑器执行以下操作：

- 访问并编辑现有的 SAS 程序
- 编写新的 SAS 程序
- 提交 SAS 程序
- 将 SAS 程序保存到文件

在增强编辑器中，你程序的语法通过颜色高亮显示这些项目：

- 步骤边界
- 关键字
- 变量和数据集名称

2. 要提交程序执行，请发布 `SUBMIT` 命令，点击或选择**运行** ⇨ **提交**。程序的输出将显示在输出窗口中。

### 查看结果

输出窗口（Output window）默认打开。

- 它是主要窗口之一，并且默认打开。
- 每当按顺序生成输出时，它都会变成活动窗口。
- 它会自动按照输出生成的顺序进行记录。

你可以发布 `CLEAR` 命令或选择**编辑**（Edit）->**清除全部**（Clear All）来清除窗口内容，或者点击 □（新建图标）。

若要在输出窗口中水平滚动，请使用水平滚动条或发布 `RIGHT` 和 `LEFT` 命令。

在 Windows 环境中，输出窗口显示提交的程序生成的最后一页输出。

要在输出窗口中垂直滚动，请使用垂直滚动条、发布 `FORWARD` 和 `BACKWARD` 命令，或使用键盘上的 `PAGE UP` 或 `PAGE DOWN` 键。

> 你也可以使用 `TOP` 和 `BOTTOM` 命令在输出窗口中垂直滚动。

1. 滚动到顶部以查看 `PRINT` 过程的输出。

## 2.2 提交 SAS 程序

2. 要打开日志（Log）窗口并浏览程序生成的消息，请发布 `LOG` 命令、选择**窗口**（Window）->**日志**（Log），或点击日志图标。

### 日志 (Log)

- 它是主要窗口之一，并且默认打开。
- 你的 SAS 会话的审计跟踪；消息按照程序生成的顺序写入日志。

3. 要清除窗口内容，请发布 `CLEAR` 命令、选择**编辑**（Edit）->**清除全部**（Clear All），或者你可以点击 □（新建图标）。

日志窗口包含了提交的编程语句，以及关于以下内容的说明：

- 任何被读取的文件
- 读取的记录
- 程序执行和结果

在此示例中，日志窗口中没有警告或错误消息。如果程序包含错误，相关的警告和错误消息也会写入 SAS 日志。

### 使用帮助功能

1. 要打开帮助功能，选择**帮助**（Help）⇒ **SAS 帮助与文档**（SAS Help and Documentation）或点击。
2. 选择**内容**（Contents）选项卡。
3. 从内容选项卡中选择 **SAS 产品**（SAS Products）⇒ **Base SAS**。

主要的 SAS 语法书籍是《Base SAS 9.2过程指南》（Base SAS 9.2 Procedures Guide）和《SAS 9.2 语言参考：字典》（SAS 9.2 Language Reference: Dictionary）。推荐阅读《SAS 9.2 语言参考：概念和使用 Base SAS 逐步编程》来学习 SAS 概念。

4. 例如，选择 **Base SAS 9.2过程指南** ⇒ **过程**（Procedures）⇒ **PRINT 过程**（The PRINT Procedure）以查找 `PRINT` 过程的文档。

#### PRINT 过程

- 概述：`PRINT` 过程
- 语法：`PRINT` 过程
- `PRINT` 语句
  - `BY` 语句
  - `ID` 语句
  - `PAGEBY` 语句
  - `SUM` 语句
  - `SUMBY` 语句
  - `VAR` 语句
- 结果：`PRINT` 过程
- 示例：使用 `PRINT` 过程进行打印
  - 示例 1：在列头中选择变量
  - 示例 2：自定义列头中的文本
  - 示例 3：为观测值组创建报告的独立章节
  - 示例 4：使用单个 `BY` 组对数值变量排序
  - 示例 5：使用多个 `BY` 变量对数值变量求和
  - 示例 6：限制报告中的运行次数
  - 示例 7：控制包含许多变量的报告布局
  - 示例 8：使用 `BY` 组和 `ID` 变量控制布局
  - 示例 9：打印 SAS 库中的所有数据集

## 在 SAS 窗口环境下提交 SAS 程序 – UNIX

p02d01

- 启动 SAS 会话。
- 提交 SAS 程序。
- 查看结果。
- 使用帮助功能。

### 启动 SAS 会话

1. 在你的 UNIX 会话中，输入相应的命令启动 SAS 会话。

> 调用 SAS 的方法取决于你的操作系统以及站点生效的任何自定义。

### 包含并提交程序

1. 要打开帮助功能，选择**帮助**（Help）⇒ **SAS 帮助与文档**（SAS Help and Documentation）或点击。
2. 选择**内容**（Contents）选项卡。
3. 从内容选项卡中选择 **SAS 产品**（SAS Products）⇒ **Base SAS**。
4. 例如，选择 **Base SAS 9.2过程指南** ⇒ **过程**（Procedures）⇒ **PRINT 过程**（The PRINT Procedure）以查找 `PRINT` 过程的文档。

### 包含和提交 SAS 程序

1. 要将 SAS 程序包含（复制）到您的 SAS 会话中，请发布 `INCLUDE` 命令。

a. 在程序编辑器（Program Editor）的命令行中输入 `include` 以及包含您的程序的的文件。
b. 按 `ENTER`（回车键）。

程序已包含在程序编辑器中。

你可以使用程序编辑器执行以下操作：

- 访问并编辑现有的 SAS 程序
- 编写新的 SAS 程序
- 提交 SAS 程序
- 将编程语句保存到文件中

该程序包含三个步骤：一个 `DATA` 步骤和两个 `PROC` 步骤。

发布 `MIT` 命令来执行您的程序。

## 2. 程序输出的第一页显示在输出窗口（Output window）中。

![](img/1698e3a97543d6895ff5297aae8fd042_52_0.png)

### 查看结果

输出窗口

- 是主要窗口之一，且默认打开
- 每当接收到输出时，它都会变成活动窗口
- 自动按照生成的顺序累积输出。

你可以发布 `CLEAR` 命令或选择 **Edit**（编辑）⇨ **Clear All**（全部清除）来清空窗口内容。

要在输出窗口中水平滚动，请发布 `RIGHT`（向右）和 `LEFT`（向左）命令。

要在输出窗口中垂直滚动，请发布 `FORWARD`（向前）和 `BACKWARD`（向后）命令。

- 你也可以使用 `TOP`（顶部）和 `BOTTOM`（底部）命令在输出窗口内垂直滚动。

发布 `END` 命令。如果 `PRINT` 过程中产生了多页输出，将到达输出的最后一页。如果 `PRINT` 过程中只产生了一页输出，`END` 命令将允许 `MEANS` 程序执行并产生其输出。

![](img/1698e3a97543d6895ff5297aae8fd042_53_0.png)

你可以在输出窗口命令行发布 `AUTOSROLL 0` 命令，使一次提交的所有 SAS 输出一次性放在输出窗口中。这消除了需要发布 `END` 命令来单独运行每个步骤的需求。

`AUTOSROLL` 命令在您的 SAS 会话期间持续有效。如果你希望在每次调用 SAS 时都启用此设置，可以在输出窗口命令行输入 `autoscroll 0; wswave` 来保存此设置。

发布 `END` 命令返回程序编辑器。

程序执行后，你可以在日志窗口（Log window）中查看消息。

日志窗口

- 是主要窗口之一，且默认打开。
- 作为你 SAS 会话的记录；消息按照程序生成的顺序顺序写入日志中。

你可以发布 `CLEAR` 命令来清空窗口内容。

日志窗口包含最近提交的编程语句，以及关于以下内容的说明：

- 任何被读取的文件
- 被读取的记录
- 程序执行情况和结果

在此示例中，日志窗口不包含任何警告或错误消息。如果你的程序包含错误，相关的警告和错误消息也会写入 SAS 日志。

## 2.2 提交 SAS 程序 2-29

发布 `END` 命令返回程序编辑器。

### 使用帮助功能

1. 要打开帮助功能，请选择 **Help**（帮助）-> **SAS Help and Documentation**（SAS 帮助与文档）或点击。
2. 选择 **Contents**（内容）选项卡。
3. 从 **Contents** 选项卡中，选择 **SAS Products** -> **Base SAS**。

主要的 Base SAS 语法书籍是《Base SAS 9.2 Procedures Guide》和《SAS 9.2 Language Reference: Dictionary》。推荐使用 SAS 9.2 Language Reference: Concepts and Step-by-Step Programming with Base SAS Software 来学习 SAS 概念。

4. 例如，选择 **Base SAS 9.2 Procedures Guide** -> **Procedures**（过程） -> **The PRINT Procedure**（PRINT过程）来查找 `PRINT` 过程的文档。

> 也可以通过以下链接从浏览器访问帮助功能：
> http://support.sas.com/documentation/index.html

从此网页，可以选择 Base SAS。SAS 语法书籍提供 HTML 或 PDF 版本。

## 使用 SAS Enterprise Guide 提交 SAS 程序

p102d01

- 启动 SAS Enterprise Guide。
- 包含并提交 SAS 程序。
- 查看结果。
- 管理项目（可选）。
- 使用帮助功能。

### 启动 SAS Enterprise Guide

1. 双击 Enterprise Guide 图标启动 SAS 会话。

你调用 Enterprise Guide 的方法取决于你所在地生效的任何自定义。本演示基于 Enterprise Guide 4.2。

![](img/1698e3a97543d6895ff5297aae8fd042_55_0.png)

2. 通过选择关闭 Welcome to SAS Enterprise Guide 窗口。

### 包含和提交 SAS 程序

1. 要将 SAS 程序打开到 Enterprise Guide，请选择 **File**（文件）-> **Open**（打开）-> **Program**（程序），或选择 **Program**（程序）然后选择你想要包含的文件。

程序被包含在工作区域的 **Program**（程序）选项卡中。

![](img/1698e3a97543d6895ff5297aae8fd042_56_0.png)

你可以使用 Program 选项卡执行以下操作：

- 访问并编辑现有的 SAS 程序
- 编写新的 SAS 程序
- 提交 SAS 程序
- 将编程语句保存到文件中

在 Program 选项卡中，程序中的语法经过颜色编码以显示这些项目：

- 关键字（keywords）
- 变量名（variable names）

3. 修改 Program 选项卡中的 `INFILE` 语句以包含文件的路径。

```sas
data work.Newps;
  infile 'C:\workshop\newemps.csv';
  input First_Name $ Job_Title $;
run;
```
