
# 管理空间索引 (Manage Spatial Indexes)

# 设置主键 (Set Primary Key)

# 关系 (Relationships)

# 管理检查约束 (Manage Check Constraints)

# 管理 XML 索引 (Manage XML Indexes)

FIGURE 12-20

5. 在表定义下方，您看到一个类似于 VS 中属性格的面板。选中 *Id* 列，在列属性格中向下滚动，直到看到 Identity Specification（标识规范）。展开该项，并将 (Is Identity) 设置为 Yes（是），如图 12-21 所示。

| Has Non-SQL Server Subs: No |

| --- | --- |

| Identity Specification | Yes |

| Identity Increment | 1 |

| Identity Seed | 1 |

| (Is Identity) | Yes |

FIGURE 12-21

6. 按 `Ctrl+S` 保存您的更改。弹出一个对话框，允许您为表提供名称。输入 *Genre* 作为名称并点击 OK 应用您的更改。然后按 `Ctrl+F4` 关闭表设计器。

7. 按照步骤 2 和 3 创建另一个表，但这次创建一个具有以下规格的表，用于存储 Planet Wrox 网站的 CD 和演唱会评论。

# 创建表 (Creating Your Tables) | 431

| 列名 (COLUMN NAME) | 数据类型 (DATA TYPE) | 允许空值 (ALLOW NULLS) | 描述 (DESCRIPTION) |

| --- | --- | --- | --- |

| Id | int | No | 表的主键和标识。 |

| Title | varchar(200) | No | 包含评论标题。 |

| Summary | varchar(max) | No | 包含评论的简短摘要或预告。 |

| Body | varchar(max) | Yes | 包含评论的全文。 |

| GenreId | int | No | 包含评论所属类型的 ID。 |

| Authorized | bit | No | 决定评论是否经过管理员授权发布。 |

| CreateDateTime | datetime | No | 评论创建的日期。 |

| UpdateDateTime | datetime | No | 评论更新的日期。 |

8. 按照步骤 4 和 5 所示，将 Id 列设为主键，并将其（Identity 属性）设置为 Yes。

9. 点击 CreateDateTime 列，然后在列属性格中，在 Default Value（默认值）字段输入 `getdate()`，如图 12-2 所示。如果您不提供值，它将插入当前日期和时间。

10. 对 UpdateDateTime 列重复上述步骤。

11. 完成后，按 `Ctrl+S` 保存表并按 `Ctrl+F4` 关闭表设计器。

## 工作原理 (How it Works)

SSMS 中的表设计器非常简单。您输入列名并为列定义数据类型，工作就完成了一大部分。对于这些列，将 Identity 属性设置为 Yes。这意味着 SQL Server 会自动为插入的每个新行分配一个顺序数字。表中的第一行获得 ID 1，后续行的 ID 递增加 1。您可以通过设置列的 Identity Increment（标识增量）和 Identity Specification（标识规范）来更改此行为。

![](img/9e033e3b9560597824f8b22941d6d8bb_468_0.png)

FIGURE 12-2

您还为 Review 表的 CreateDateTime 和 UpdateDateTime 列分配了默认值。当您在 SQL 语句中显式提供值时，数据库会插入默认值。在“Try Out”部分，此默认值是 `getdate()`，它会自动插入日期和时间。这样您就可以轻松地跟踪评论创建的时间。在随后的章节中，您将看到在更新评论时如何更新 UpdateDateTime 列。

除了您之前通过 SELECT 和 JOIN 语句在 SQL 查询中定义的关系外，您还可以在数据库中创建关系。下一节将讨论关系的益处以及如何在您的数据库中创建它们。

## 创建表之间的关系 (Creating Relationships between Tables)

考虑您到目前创建的表。您创建了一个带有 Id 列的 Genre 表，用于唯一标识行。您还创建了一个带有 GenreId 列的 Review 表。显然，每个评论都应该包含一个指向 Genre 表中行的 ID，以便您知道它属于哪种类型。现在想象您从 Genre 表中删除了一行关联有评论的行。如果没有关系，数据库将允许您这样做。然而，这会带来很多麻烦。如果您尝试将类型与评论一起显示，它将失败，因为不再有匹配的类型。同样，如果您想按类型分组列出系统中的所有评论，您将漏掉那些属于已删除类型的评论。

为了避免此类问题并保持您的数据库处于健康且一致的状态，您可以在两个表之间创建关系。数据库将阻止您意外删除仍有其他行关联的表中的行。

除了数据保护外，关系还帮助您使数据模型更加清晰。如果您通过图表（您在下一次练习中将使用）查看数据库，将发现表与之间的关系有助于您理解表是如何连接的以及它们代表什么数据。

您可以通过创建一个表的主键和另一个表中的一列来定义关系。另一个表中的列被称为外键。在 Review 和 Genre 表的情况下，Review 表的 GenreId 列指向 Genre 表的主键 Id，使 GenreId 成为外键。在下一次练习中，您将看到如何创建两个表之间的关系，并执行 SQL 语句显示该关系如何帮助您。

## 尝试创建两个表之间的关系 (TRY OUT Creating a Relationship between Tables)

在视觉上添加两个表之间的关系之前，您需要添加图表。图表是帮助您理解数据的可视化工具。

1. 在资源管理器中，展开您的 Wrox 数据库，右键点击 Databases （如图 12-18 所示），并点击 New。如果是第一次向数据库添加图表，可能会弹出一个询问是否要让 SSMS 成为数据库的所有者。点击 Yes。如果没有收到此提示也可以工作。后续可能会提示，为了使用图表，SSMS 需要创建一些对象。再次点击 Yes。

2. 在接下来的 Add 框中，选择您之前创建的两个表（按住 `Ctrl` 键点击每个项），点击 Add 添加表，然后点击 OK 关闭 Add 框。

3. 如必要，使用拖放调整图表中的表，使其相邻。

4. 在 Genre 表上，点击 Id 列的左边距（它应该带有黄色钥匙，表示它是主键），将其拖入 Review 表的 GenreId 列并释放鼠标。

5. 弹出两个对话框，允许您自定义关系的详细信息。在顶部的窗口中，确认选择 Genre 作为主键表 (Primary Key Table)，并将 Review 作为外键表 (Foreign Key)。点击 OK 关闭顶部窗口。

对话框仍然存在，如图 12-23 所示，注意 Enforce Foreign Key Constraint（强制执行外键约束）已设置为 Yes。此属性确保您不会在仍有关联行的情况下删除 Genre 表中的行。点击 OK 关闭此对话框。

6. 图表窗口应显示两个表之间有一条线。在 Genre 表侧，您应该看到一个黄色钥匙，表示该表包含关系的主键。在另一端，您应该看到无限符号（旋转 90 度的数字8），表示 Review 表可以有许多使用相同 GenreId 的行。您可以在图 12-24 中看到该图表。

## 第 12 章 数据库简介

| Review * | Genre * |

| --- | --- |

| 💡 Id | 💡 Id |

| Title | Name |

| Summary | SortOrder |

| Body | |

| Genre | |

| Authorized | |

| CreateDateTime | |

| UpdateTime | |

图 12-24

请注意，在你的图表中，两个两个表之间的连线头部并不一定指向特定的列；它们只是指向整个表。这可能会引起混淆，因为你可能会认为其他列实际上也是相关的。要确认参与该关系的列，请右键点击两个表之间的连线并选择“属性 (Properties)”。表和列规范 (Table and Columns Specification) 将显示哪些列和表参与了该关系，如图 12-25 所示。

你可以拖动线条到正确的列。这不会影响表，但会让查看图表的人更清楚你的意图。

- 7. 按 `Ctrl+S` 保存对图表的更改。你可以输入更具描述性的名称如 Reviews 和 Genres 并点击确定。你会收到另一个警告，提示你正要对 Review 和 Genre 表进行更改。点击“是”应用更改。

- 8. 返回到对象管理器 (Object Explorer)，展开 Tables 节点，右键点击 Genre 表并选择“编辑前 200 行 (Edit Top 200 Rows)”。如果你没有看到你的表，请点击对象管理器工具栏上的刷新图标。通过输入 Name 和 SortOrder 输入几个不同的类型。当你在 SortOrder 字段中按 Tab 键离开当前行时，该行会被插入数据库，且 Id 将被填充一个唯一的、顺序数字。你最终将得到一个类似于图 12-26 所示的列表。

- 9. 使用“编辑前 200 行”命令从对象管理器打开 Review 表，并输入几条评论行。对于 Genre 字段，提供你之前在 Genre 表中插入的某些 ID。

![](img/9e033e3b9560597824f8b22941d6d8bb_471_0.png)

图 12-25

*Genre*

创建你的表 | 435

你现在可以创建 Title、Summary 和 Body 字段，并将 Authorized 设置为 True。记住，你不必为这些列输入值。如果你省略了它们，数据库将自动为你插入默认值。注意，你不能自己在 Id 列中插入值。因为这是一个标识字段 (Identity field)，数据库会自动提供值。如果你遇到关于列缺少缺值的错误，请确保你在上一个练习中输入了正确的默认值。当你完成一行的输入后，点击该行（在新行上，即下方的空白处）以将该行插入到表中。你的行列表看起来应该与图 12-27 相似，当然，你选择的列可能会不同。

| Id | Title | Summary | Body | Genre | Authorized |

|---|---|---|---|---|---|

| 1 | Sonic Youth-Davidson Nation... | Summary for item 1 | Body item 1 | 5 | True |

| 2 | Sonic Youth-Davidson Nation... | Summary for item 2 | Body item 2 | 5 | True |

| 3 | Noah Jones - Not Too Late | Summary for item 3 | Body item 3 | | True |

| 4 | Di Tiao - In Search of Sunrise | Summary for item 4 | Body item 4 | 12 | True |

图 12-27

10. 右键点击上面的 Genre 表并选择“编辑前 20 行 (Edit Top 20 Rows)”。随后，查询设计器上的 SQL 格按钮使用相同工具栏上的“更改类型 (Change Type)”来创建一个 DELETE 查询。修改查询以删除你在第 9 步中链接评论的类型 ID，如下：

```
DELETE FROM Genre Where Id = 5
```

此代码将尝试删除独立摇滚 (Indie Rock) 类型。然而，因为评论与其相连，删除操作应该失败。按 `Ctrl+R` 执行查询。SSMS 现在不会从 genre 表中删除该行，而是向你显示图 12-28 所示的对话框。

![](img/9e033e3b9560597824f8b22941d6d8bb_472_0.png)

图 12-28

## 工作原理

当你在两个表之间建立关系时，当你尝试插入、更新或删除数据时，数据库将强制执行关系。在这个示例中，Review 表中的行在 Genre 表中有一个存在于 Review 表的行。当你尝试从 Genre 表中删除一行时，数据库发现该类型正被 Review 表中的某行使用，从而取消删除操作。在第 15 章中，你将学习如何在网站中处理这种情况，并向用户展示一条友好的消息。

现在你已经了解了处理数据库的概念，可以准备下一章了，下一章将向你展示如何使用许多可用 ASP.NET 控件操作你的数据库。

## 实用数据库技巧

以下列表提供了关于操作数据库的一些实用技巧：

- 因为数据库是网站的核心，所以你需要仔细考虑它的设计。在开始在此基础上构建网站之前，预先考虑良好的设计是尤为重要的。当你有很多页面访问你的数据库时，这会变得困难。

- 始终为你的考虑主键。

- 避免空格。

- 为了删除需要的行。

- 为了定义表之间的关系。

- 为了限制返回的行数。

- 为了保护你的数据。

## 总结

操作数据库的能力是你开发技能的一项良好补充。现在的网站都使用数据库，因此理解如何操作它们很重要。

要访问和操作关系型数据库中的数据，请使用称为结构化查询语言（SQL）的语言。在其他元素中，定义四个关键字允许你执行 CRUD——创建、读取、更新、删除——操作。

`SELECT` 语句允许你从一个或多个表中检索数据。要访问多个表，可以使用可用的 JOIN 类型。要限制查询返回的行数，使用 WHERE 子句。要对查询返回的结果集进行排序，使用 ORDER BY 子句。要在数据库中创建新行使用 INSERT 语句，使用 UPDATE 语句更改现有行。最后，删除不再需要的行使用 DELETE 语句。像 SELECT 和 UPDATE 语句一样，DELETE 接受一个可选的 WHERE 子句来限制删除的行。

本书第二部分展示了如何使用内置数据库工具创建具有关系的表。此外，你看到了表之间的关系如何保护你的数据不损坏或孤立。

## 练习题

- 1. 如果你尝试从 Genre 表中删除在 Review 表中有匹配的行，删除 将失败。这是如何可能的？

- 2. 如果你尝试从 Review 表中删除其 GenreId 设置为 Genre 表中现有类型 ID 的行，删除 将成功。这是为什么呢？

- 3. 假设你想清理数据库，决定删除 Review 表中 Id 等于 100 的所有行。写一个 SQL 语句来删除这些行。

- 4. 假设你想删除 ID 为 4 的类型。但在删除该类型之前，你想将分配给该类型的评论重新分配给另一个 ID 为 11 的类型。你需要哪些 SQL 语句来实现这一点？

- 5. 写一个 SQL 语句将 Rock (摇滚) 类型更新为 Punk Rock (朋克摇滚)。你有两种方法编写此 WHERE 子句。

你可以在附录 A 中找到这些练习题的答案。

# 本章你学到的内容

| | |

|---||-|

| CRUD | 用于数据库中处理数据的四种基本 SQL 操作：创建（Create）、读取（Read）、更新（Update）和删除（Delete） |

| 外键 | 指定表中中的某一列，它引用另一个表的主键，以实施引用完整性 |

| 标识 (Identity) | 分配给新行的自动顺序数字 |

| JOIN | 允许你在查询中表示两个或多个表之间的关系，以查找相关数据 |

| 主键 | 由表中的一个或多个列组成，用于唯一标识表中的某行 |

| 关系型数据库 | 一种数据库，数据存储在单独的、类似电子表格的表中，这些表可以相互引用 |

| 关系 | 定义一个或多个表之间的关系，并帮助你实施引用完整性 |

| 表 | 数据库中的一种对象，允许你存储数据 |

# 13

## 显示和更新数据

在本章你将学习到：

- 如何使用 GridView、DetailsView 和 DataSource 等控件显示、插入、编辑和删除数据

- 如何使用 ASP.NET 验证控件创建一个丰富的界面，使用户在插入和编辑数据的同时维护数据完整性

- 在应用程序中存储连接字符串的最佳方法，以便于后续更新

本章的 WROX.COM 代码下载

你可以在 www.wrox.com/go/beaspnet451 的 Download Code 标签上找到本章的 wrox.com 代码下载。代码位于第 13 文件夹中。

在本章中，你将学习如何使用 ASP.NET 自带的热门数据控件显示、插入、更新和删除数据。除了用于在网页中显示和编辑数据的视觉控件，你还将学习如何使用 SqlDataSource 控件，它是数据库与 ASPX 页面之间的桥梁。

你首先需要查看的是可用的数据控件，将在下一节中讨论。

## 数据控件

为了让你能够高效地处理系统中的数据，ASP.NET 提供了两组数据感知控件：数据绑定控件和数据源控件。

第一组包含你用于显示和编辑数据的控件，例如用户界界面中的 GridView、Repeater 和 ListView 控件。数据源控件用于从数据源（如数据库或 XML 文件）检索数据，然后为数据绑定控件提供数据。图 13-1 显示了工具箱中 Data 类别下可用数据控件的完整列表。

接下来的三个章节提供了 Data 类别所有控件的快速概述。在本章的剩余部分，你将更详细地了解这些控件的工作原理以及如何使用它们。

### 数据绑定控件

图 13-1 所示工具箱中的七个控件是所谓的数据绑定控件。你使用它们在你的网页上显示和编辑数据。GridView、DataList、ListView 和 Repeater 都用于同时显示多行，它们也被称为列表控件。DetailsView 和 FormView 设计用于一次显示单行。DataPager 是一个辅助控件，用于为 ListView 控件提供分页功能。

### 列表控件

由于 ASP.NET 提供了多个控件来显示列表

图 13-2 显示了一个典型的 GridView。

| Id | Title | CreateDateTime |

|---|---|---|
