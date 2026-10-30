

## FIGURE 7.3

外部链接数据的 Datasheet 视图。

![](img/1e45673ab6eca9d20e67635ff5b9b318_256_0.png)

## Limitations of linked data

尽管本章描述使用链接数据时如同其为 Access 的本地表一样，但某些操作无法对链接数据执行。此外，被禁止的操作在一定程度上取决于链接到 Access 的数据类型。

这些限制相对容易理解。链接数据永远不属于 Access 所有。链接到 Access 的外部文件由各自的应用管理。例如，Excel 工作表由 Excel 管理。Access 随意修改 Excel 工作表中的数据是武断的——也是危险的。例如，由于许多 Excel 操作依赖于工作表中行列的相对位置，插入一行可能会破坏 Excel 对数据执行的计算和其他操作。删除一行可能会扭曲 Excel 工作表中的命名范围，造成类似问题。由于 Access 没有实际方法去理解外部数据文件的所有者对其执行的所有操作，微软选择了保守的做法，不允许 Access 修改可能给数据所有者带来问题的 数据。

以下列表描述了链接数据的限制：

- **Access data:** 你可以对链接表中的数据执行的操作没有限制。你不能删除或重命名源表。并且你也不能更改源表的字段或数据类型。

## Chapter 7: Linking to External Data

- 2. **选择功能区的 外部数据 选项卡，然后单击 导入和链接 → 新数据源 → 从数据库 → Access。** Get External Data – Access Database 对话框出现（如图 7.4 所示）。

## FIGURE 7.4

使用 Get External Data 对话框选择要对外部数据源执行的操作类型。

![](img/1e45673ab6eca9d20e67635ff5b9b318_258_0.png)

- 3. **单击 Browse 按钮。** File Open 对话框出现。
- 4. **定位 Chapter07_Link.accdb 并单击 Open。** File Open 对话框关闭，你返回到 Get External Data – Access Database 对话框。
- 5. **选择链接的选项按钮并在 Get External Data – Access Database 对话框中单击 OK。** Link Tables 对话框使你能够从所选数据库（本例中为 Chapter07_Link）中选择一个或多个表。图 7.5 显示了 Link Tables 对话框打开在 Chapter07_Link.accdb 上。

## FIGURE 7.5

使用 Link Tables 对话框选择要链接的 Access 表。

![](img/1e45673ab6eca9d20e67635ff5b9b318_259_0.png)

**6.** 选择 **tblSalesPayments** 并单击 **OK**。双击表名不会链接该表——你必须先选中它，然后单击 OK。

链接 tblSalesPayments 后，Access 返回到对象列表并显示新链接的表。图 7.6 显示了 tblSalesPayments 已链接到当前数据库。注意附着在 tblSalesPayments 上的特殊图标。此图标表示该表链接到外部数据源。用鼠标悬停在链接表上会显示该链接表的数据源。

> **TIP**
> 
> 你可以一次链接多个表，只需在 Link Tables 对话框中单击 OK 按钮前选中多个表。单击 Select All 按钮可选择所有表。选中所有表后，你可以单击单个选择以取消选中它们。

## Linking to ODBC data sources

关于数据共享的一项重要进展是微软和其他厂商建立了开放数据库连接 Open Database Connectivity（ODBC）标准。ODBC 是软件厂商用来为数据库产品创建驱动程序的规范。该规范

使你的 Access 应用程序能够以标准方式在许多不同的数据库平台上使用数据。如果你编写符合 ODBC 规范的应用程序，那么你的应用程序将能够使用任何其他 ODBC 兼容的后端。

## FIGURE 7.6

导航窗格中添加了 tblSalesPayments。悬停在链接表图标上会显示其来源。

![](img/1e45673ab6eca9d20e67635ff5b9b318_260_0.png)

例如，假设你创建了一个使用 SQL Server 数据库后端的 Access 应用程序。实现此需求最常见的方式是使用 SQL Server ODBC 驱动程序。开发应用程序后，你发现其中一个分支机构也想使用该应用程序，但他们使用 Oracle 作为数据库主机。如果你的应用程序严格遵循 ODBC 语法，那么你应该能够通过获取 Oracle ODBC 驱动程序来使用相同的应用程序与 Oracle。不仅厂商为自己的产品提供驱动程序，而且现在还有专门创建和提供 ODBC 驱动程序的软件厂商。

## Linking to non-database data

你也可以链接到非数据库数据，例如 Excel、HTML 和文本文件。当你选择其中一种数据源类型时，Access 会运行 Link Wizard，引导你完成整个过程。

## FIGURE 7.7

Get External Data – Excel Spreadsheet 对话框的第一个屏幕。

![](img/1e45673ab6eca9d20e67635ff5b9b318_262_0.png)

- 5. **选择 Products 工作表。** Link Spreadsheet Wizard 会引导你完成多个不同的屏幕，在其中指定诸如 第一行包含列标题 以及要应用于 Excel 工作表中每一列的数据类型等细节。Link Spreadsheet Wizard 的最后一屏会要求输入新链接表的名称。
- 6. **单击 Finish。** 链接表建立完成，你返回到 Access 环境。

与数据库开发中的许多其他事情一样，链接到外部数据源所涉及的许多决策都基于数据在应用程序中的使用方式。此外，你为字段和其他细节提供的名称对你的应用程序有直接影响。

## FIGURE 7.8

Link Spreadsheet Wizard 的主屏幕。

![](img/1e45673ab6eca9d20e67635ff5b9b318_263_0.png)

## Linking to HTML files

由于 Access 对此过程施加了相当严重的限制，本书未详细介绍链接到 HTML 文档中数据的过程。例如，Access 无法从任意 HTML 文件中检索数据。数据必须以 HTML 表格的形式呈现，按行列格式排列，并且数据必须相对干净（不存在异常数据或数据混合，例如文本、图像和数值数据组合在单个 HTML 表格内）。

如果你在页面上遇到多个 HTML 表格，或数据以层次结构方式呈现（父数据和子数据），你很可能会遇到问题。

> Tip
> 链接到任意 HTML 文档充其量是碰运气。你最好链接到专门为 Access 应用程序准备的数据源的 HTML 文档，而不是尝试处理任意 HTML 文件。如果有人要费力创建专门用于作为 Access 数据源的 HTML 文档，生成逗号分隔值 CSV 或定宽文本文件可能比 HTML 更佳。CSV 文件中每一行的字段由逗号分隔，常用于在应用程序之间移动数据。CSV 和定宽文件类型将在下一节中讨论。

链接 HTML 数据的过程与链接到 Excel 电子表格类似：

- 1. 在功能区的 外部数据 选项卡上单击 导入和链接 > 新数据源 > 从文件 > HTML 文档。Get External Data – HTML Document 对话框出现。
- 2. 选择 Link to the Data Source by Creating a Linked Table 选项，然后单击 Browse。File Open 对话框出现，使你能够搜索要链接的 HTML 文件。

从这一点开始，链接到 HTML 数据的过程与链接到其他类型数据文件类似，包括提供字段名称和链接数据的其他细节。图 7.9 显示了 Link HTML Wizard 的第一个屏幕。单击 Advanced 按钮可进入 Link Specification 对话框（如图 7.10 所示），在其中你可以提供字段名称和其他细节。

## FIGURE 7.9

Link HTML Wizard 对话框显示 HTML 文件中的数据。

![](img/1e45673ab6eca9d20e67635ff5b9b318_264_0.png)

