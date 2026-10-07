
Blum, T., Keislar, D., Wheaton, J., and Wold, E. 1998. “Writing a Web Crawler in the Java Programming Language.” Muscle Fish LLC.

Gantz, J. and Reinsel, D. 2011. “Extracting Value from Chaos.” IDC iView, June 2011. Available at: http://www.emc.com/collateral/analyst-reports/idc-extracting-value-from-chaos.pdf.

Lieberman, H., Fry, C., and Weitzman, L. 2001. “Exploring the Web with Reconnaissance Agents.” Communications of the ACM, 44(8): 69–75.

Manning, C. D., Raghavan, P., and Schutte, H. 2008. Introduction to Information Retrieval. New York, NY: Cambridge University Press.

McCallum, A. K., Nigam, N., Remic, J., and Seymour. K. 2000. “Automating the Construction of Internet Portals with Machine Learning.” Information Retrieval, 3(2): 127–163.

Mearian, L. 2011. “World Data Will Grow by 50X in Next Decade, IDC Study Predicts.” ComputerWorld, June 2011. Available at: http://www.computerworld.com/article/9217988/World_s_data_will_gr

Mitchell, B. 2008. “UNC – Universal Naming Convention – Windows.” About.com: Wireless Networking. Available at: http://comnetworking.about.com/od/windowsnetworking/g/unc-name.htm.

Pant, G. and Mencer, F. 2003. “Topical Crawling for Business Intelligence.” Proceedings of 7th European Conference on Research and Advanced Technology for Digital Libraries (ECDL) 2003. Trondheim, Norway,

Pant, G., Srinivasan, P., and Mencer, F. 2004. “Crawling the Web Dynamics: Adapting to Change, Size, Topology and Use. New York: Springer-Verlag, 153–78.

SAS Information Retrieval Studio, Release 12.1. Administrator’s Guide. Cary, NC: SAS Institute Inc.

SAS Information Retrieval Studio, Release 12.1. User’s Guide. Cary, NC: SAS Institute Inc.

SAS Information Retrieval Studio, Release 12.1. Quick Start Guide. Cary, NC: SAS Institute Inc.

Srinivasan, P., Mitchell, J., Bodeneider, O., Pant, G., and Mencer, F. 2002. “Web Crawling Agents for Retrieving Biomedical Information”. NETTAB 2002: Agents in Bioinformatics, Bologna, Italy, 2002.

默认情况下，虚拟索引服务器和虚拟查询服务器未启用。如果开启它们，它们将与后端索引服务器和查询服务器协同工作，分配文档负载。当您的爬取过程可能检索的文档量达到数级或更多时，启用这些组件有助于提高系统的整体性能并优化磁盘空间或内存利用率。

# 第 3 章将文本数据导入 SAS Text Miner

- SAS Enterprise Miner 和 SAS Text Miner 简介
- SAS Text Miner 中的数据类型、角色和级别
- 在 SAS Enterprise Miner 中创建数据源
- 将文本数据导入 SAS
- 使用文本导入节点（Text Import Node）将数据导入 SAS Text Miner
- `%TMFILTER` 宏
- 将 XLS 和 XML 文件导入 SAS Text Miner
- 使用 SAS字符函数管理文本
- 总结
- 参考文献

本章从对 SAS Enterprise Miner 和 SAS Text Miner 的简要介绍开始。随后我们讨论了如何使用 SAS Text Miner 将各种文件格式的原始数据导入 SAS，以及如何使用网络爬虫从网络导入数据。我们简要讨论并演示了 Perl 正则表达式的强大用法。

## SAS Enterprise Miner 和 SAS Text Miner 简介

SAS Enterprise Miner 是一组允许您收集数据和分析数据的工具。此外，由于您可以在 SAS Enterprise Miner 流程图中嵌入 SAS Text Miner 节点，可以在挖掘过程中将定量变量与非结构化文本相结合。因此，您正在将文本挖掘与传统数据挖掘技术相结合。因此，SAS Text Miner 中的数据类型同时适用于结构化（数值）和非结构化（文本）数据。

数据角色通常根据数据类型而异。对于您想要分析的非结构化（文本）数据，角色通常设置为 Text（文本），测量级别设置为 Nominal（名义）。对于数值数据，有许多选项取决于您的分析目标。例如，当您想使用该数值变量来反映文本数据中每个值的唯一标识符时，可以将该数值变量的角色设置为 ID。当您想使用该数值变量来反映与文本数据中每个值相关的时间戳时，可以将该数值变量的角色设置为 Time ID（时间戳标识符）。当您想将该变量作为任何后续节点中的输入变量时，可以将该变量的角色设置为 Input（输入）。例如，如果您创建了一个标记变量来指示文本中每个值是否存在图形，并希望在随后的分析中使用此标记变量，那么可以为该标记变量分配 numeric（数值）角色到

当您希望在后续任何建模节点（如回归）中使用该变量作为目标变量时，将变量设置为 **Target**（目标）。例如，如果您在文本数据中有表示正面、负面或中立情感的数值变量，并且您想使用文本数据预测此情感变量，则可以将情感变量分配为 **Target** 角色。数值数据的其他可用数据角色，请参阅 SAS Enterprise Miner 的在线帮助。

对于数值数据，共有五种可能的测量级别，取决于创建或收集数据时使用的测量标度。**Unary（单值）**级别用于变量在数据集中每个观测值具有相同值的情况。**Binary（二分）**级别用于分类变量具有两个不同值的情况。**Nominal（名义）**级别用于分类变量具有三个或更多值的情况，且测量属性反映观测值的不同值仅代表不同的类别。**Ordinal（序数）**级别用于分类变量具有三个或更多值的情况，且属性的测量属性反映出不同值存在自然顺序，但可以对其进行类算术操作。**Interval（间距）**级别用于变量具有许多数值的情况，且属性的测量属性反映了标度中有意义且相等的间隔。

## 在 SAS Enterprise Miner 中创建数据源

在通过 SAS Text Miner 处理任何数据之前，必须将数据导入 SAS Enterprise Miner 项目。以下讨论将引导您完成创建 SAS Enterprise Miner 项目、创建 SAS 库、创建图表以及创建数据源。

### (a) 创建 SAS Enterprise Miner 项目

访问和启动 SAS Enterprise Miner 的具体步骤取决于安装类型。访问欢迎窗口的常用程序是选择 开始 (Start) > 程序 (Programs) > SAS > 分析 (Analytics) > SAS Enterprise Miner（或者如果在桌面上双击 SAS Enterprise Miner 图标）。

### 图 3.2：SAS Enterprise Miner 欢迎窗口

要定义项目，您需要指定项目名称以及项目在 SAS Foundation Server 上的位置。

- 从主菜单选择 **文件 (File) > 新 (New) > 新项目 (New Project)**，或在欢迎窗口中点击 **新项目 (New Project)**。

在第一步打开新项目向导。输入项目名称并指定机器上某个文件夹的路径，将项目保存在该处。

### 图 3.3：SAS Enterprise Miner 创建新项目向导

![](img/2c338747b5eaca8c1cd68dcd87c24126_86_0.png)

- 点击 **下一步 (Next)**。要完成项目定义，请在下一步中点击 **完成 (Finish)**。

SAS Enterprise Miner 客户端应用程序将打开您创建的项目。

### 图 3.4：创建项目后的 SAS Enterprise Miner 窗口

![](img/2c338747b5eaca8c1cd68dcd87c24126_87_0.png)

## 创建 SAS 库

SAS 库将 SAS Enterprise Miner 与原始数据源连接，这些数据是您分析的基础。要定义 SAS 库，您需要知道要与 SAS Enterprise Miner 连接的数据的名称和位置。

- 从主菜单选择 **文件 (File) > 新 (New) > 库 (Library)**。

### 图 3.5：SAS Enterprise Miner 库向导——第 1 步

![](img/2c338747b5eaca8c1cd68dcd87c24126_87_1.png)

- 点击 **下一步 (Next)**。在第 2 步，为库输入名称 (book)，并指定数据所在的文件夹路径。

### 图 3.6：SAS Enterprise Miner 库向导——第 2 步

- 点击 **下一步 (Next)**。点击 **完成 (Finish)**。

或者，在选中项目名称的情况下，在属性面板中打开项目启动代码对话框，输入以下代码并运行它以创建库：

```sas
libname Book 'C:TextMining\BookData';
```

现在，SAS Enterprise Miner 可以可以使用 SAS 库中的所有可用数据。

### (c) 创建 SAS Enterprise Miner 图表

SAS Enterprise Miner 中的所有分析通常通过向图表添加节点来完成。

- 要创建图表，从主菜单选择 **文件 (File) > 新 (New) > 图表 (Diagram)**。

### 图 3.7：SAS Enterprise Miner 创建新图表

![](img/2c338747b5eaca8c1cd68dcd87c24126_88_0.png)

- 为您的图表输入适当名称（如 Text Analysis），并点击 **确定 (OK)**。

### 图 3.8：SAS Enterprise Miner 图表

![](img/2c338747b5eaca8c1cd68dcd87c24126_89_0.png)

数据源将 SAS Enterprise Miner 与现有数据连接。在本示例中，使用了闭式问题和开放式问题。`Survey_FavStop` 是数据集。

- 点击 **下一步 (Next)**。

- 数据源向导的第 3 步提供有关数据的信息。点击 **下一步 (Next)**。

- 数据源向导的第 4 步开始元数据定义。点击 **下一步 (Next)**。

- 数据源向导的第 5 步显示元数据。点击 **下一步 (Next)**。

- 数据源向导的第 6 步允许您创建数据集。对于大多数情况，除非数据可用数据集可用，否则跳过元数据。点击 **下一步 (Next)**。

- 数据源向导的第 7 步允许您为数据设置角色。点击 **下一步 (Next)**。

- 数据源向导的最后一步提供数据的摘要详情。点击 **完成 (Finish)**。

`Survey_FavStop` 数据源已添加到项目中，现在已准备好进行分析。

### 图 3.9：SAS Enterprise Miner 文本分析

![](img/2c338747b5eaca8c1cd68dcd87c24126_90_0.png)

### 图 3.10：SAS Enterprise Miner 文本分析

![](img/2c338747b5eaca8c1cd68dcd87c24126_91_0.png)

## 将文本数据导入 SAS

正如第 1 章所述，挖掘过程的第一步是收集数据并建立有时称为语料库 (corpus)的内容。通常，语料库代表特定领域的文档。例如，一年发表的所有论文可以作为一个语料库。虽然收集数据看起来是一个简单任务，但它是挖掘过程中枯燥且最具挑战性的步骤之一。这是因为非结构化数据以多种形式存在，无法直接处理。在在使用 SAS 之前，通常需要数据转换步骤。

数据收集很大程度上取决于业务问题。这涉及回答以下简单问题：

- 项目需要什么数据？
  - 客户评论、申请文档、新闻文章、电子邮件等。
- 数据在何处可用？
  - 目录、数据库、数据仓库、网络等。
- 数据以什么形式可用？
  - PDF 文件、XML 页面、Word 文档、网页等。
- 何时收集数据（收集非静态数据时）？
  - 特定事件之前或之后、频繁更新的维基或博客。

一旦确定了解决当前问题所需的数据，挑战就是收集数据并将其转换为 Miner 可用的格式。您可能会遇到以下任何情况：

1. 数据已以 SAS 数据集的形式可用。
2. 数据以文本文件（PDF、XML、HTML、Word 等）的形式存在于目录或数据库中。
3. 需要从网上收集数据。

文本挖掘过程要求数据以 SAS 数据集的形式存在（其他格式请参见情况 2 和 3）。在第一种情况下，您可以直接创建数据源并进行文本挖掘。在后两种情况下，必须将源数据转换为 SAS 数据集。使用 SAS 访问功能从商业数据库中创建 SAS 数据集有多种方法。

SAS Enterprise Miner 中的引导数据导入向导或文件导入节点。其中具有挑战性的部分是从文本文件中创建 SAS 数据集。SAS Text Miner 能够从目录或网络上的可用文本文件中动态创建 SAS 数据集。这是通过使用 SAS Text Miner 中的 Text 节点来实现的。

在第 2 章中，你已经学习了如何使用 SAS Information Retrieval Studio 从网络和本地文件收集数据。使用 SAS Retrieval Studio 收集的数据会被输入到 SAS Text Miner 中进行进一步挖掘。接下来的章节将详细讨论使用 SAS Text Miner 收集文本数据的不同方法。

## 使用 Text 节点将数据导入 SAS Text Miner

Text Mining 节点集合中的 Text 节点可将数据作为 SAS 数据集导入 SAS Text Miner。源数据可以存在于任何专有文件格式的目录中。Text Import 节点需要安装并运行 SAS Document Server 以执行文档转换。Text 节点支持超过 100 种格式，其中包含以下：

- Microsoft Word (`.doc`, `.docx`)
- Microsoft Excel (`.xls`, `.xlsx`)
- Microsoft PowerPoint (`.ppt`, `.pptx`)
- 富文本格式 (`.rtf`)
- Adobe Acrobat (`.pdf`)
- ASCII (`.txt`)

该节点需要一个包含所有源文件的源目录（或导入文件目录）以及一个保存所有转换后文件的目标目录。SAS Text Miner 会遍历源目录，从该目录中的文件中提取文本，并在目标目录中创建纯文本文件。任何 SAS Text Miner 无法读取的格式的源文件将从文档转换中排除。同样，如果每个文件中的字符数超过 32,000，文件将被截断。如果源数据是从网络收集的，节点将在提取过程之前爬取网站、检索文件并将它们放入源目录。该节点可以轻松识别文档语言，然后将文档转码为会话编码。偏好编程的分析师可以执行相同的文本导入任务。他们可以使用 `%TMFILTER` 宏来自动执行该过程。我们将在下一节中讨论该宏。

### (a) 从 PDF 文件中提取文本并创建 SAS 数据集

假设你想分析数以千计的 PDF 格式且存储在桌面或网络位置上的文档。你希望将每个 PDF 文件表示为一个分析单元（即一个 PDF 文件的内容应恰好位于表格或 SAS 数据集的某一个单元格中，如显示 3.11 所示）。

### 显示 3.11：将每个 PDF 文档映射到 SAS 数据集的每个单元格

| PDF 语料 | SAS 数据集 |
| :--- | :--- |
|  | Doc Text |
|  | 1 |
|  | 2 |
|  | 3 |
|  | 4 |
|  | 5 |
|  | 6 |
