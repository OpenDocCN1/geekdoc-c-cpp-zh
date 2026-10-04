

使用此工具栏，点击“显示图表”（Show Diagram）“显示条件”（Show Criteria）和“显示 SQL”（Show SQL）按钮来打开它们各自的窗口。工具栏上的前四个按钮现在应该处于按下状态，文档窗口被分为四个区域，每个区域对应工具栏上的一个按钮。图 12-10 显示了带有四个窗格的整个文档窗口。

![](img/9e033e3b9560597824f8b22941d6d8bb_455_0.png)

图 12-10

SQL 窗格显示了用于检索结果窗格中显示的流类型的 SQL 语句。在这种情况下，SQL 语句读取为 `SELECT TOP (200) Id, Name, SortOrder FROM Genre`，用于从表中检索所有列和前 200 行，但你可以轻松地更改它。

- 3. 在 SQL 窗格中，按如下修改查询：`SELECT Id, Name, SortOrder FROM Genre WHERE Id > 4`
- 4. 为了确保 SQL 语句有效，点击“验证 SQL”（Verify SQL）按钮以修复你的 SQL 语句可能包含任何错误。点击“执行 SQL”（Execute SQL）按钮（带有红色感叹号的那个）或按 Ctrl+R。在这两种情况下，SQL 语句都会执行，结果窗格将更新以显示所有 ID 大于 4 的类型。在你的 SQL 窗格中，查询现在被拆分为多行以提高可读性。SQL 语言允许你将语句跨越多行，而不需要换行符。
- 5. 现在查看图表窗格——图 12-10 中显示你图表的对话框上部。在图表窗格中，你可以勾选或取消勾选列名，以确定它们是否出现在查询中。取消勾选 `SortOrder` 列（不要意外更改了条件窗格中该列的勾选标记）。注意，它也会从条件窗格和 SQL 窗格中的 SQL 语句中删除（见图 12-11）。

# 检索和操作数据

![](img/9e033e3b9560597824f8b22941d6d8bb_456_0.png)

图 12-11

在此窗格中，你可以无需编写大量代码即可修改查询。因此，看你如何应用额外的筛选，在 `Name` 的“筛选”（Filter）单元格中输入 'rock%'。这会将结果限制为所有包含 "rock" 单词且 ID 大于 4 的类型（注：此处原文为 larger than 4，译文对应逻辑：*这会将结果限制为所有包含 rock 单词且 ID 大于 4 的类型*）。如果你按 Ctrl+R，结果窗格将更新以反映查询的更改。注意 Visual Studio 是如何添加你的搜索词的（见图 12-12）。

- 7. 要确定排序顺序，使用 `SortOrder` 列。你可以对多个列执行此操作（那些在最终结果集中勾选了“输出”（Output）框的列），也可以对其他列执行。通过 `SortOrder` 列，点击 `Name` 下方的单元格。一旦它现在显示为下拉列表，当你点击该字段以外区域时，SSMS 会在输出列中放置一个标记。你可以点击该标记，再次将列从输出中删除，使其保持可排序状态但不会显示在查询中。然而，对于此练习，你应该保持该列处于选中状态。
- 8. 在 `SortOrder` 的下拉列表中选择降序（desc）。你的最终条件窗格现在看起来像图 12-12。

![](img/9e033e3b9560597824f8b22941d6d8bb_456_1.png)

图 12-12

- 9. 按 Ctrl+R（再次按或点击工具栏上的“执行 SQL”按钮），结果窗格将显示来自 `Genre` 表的符合你标准的行。当你使用图表和条件窗格进行更改时，SSMS 会持续更新 SQL 语句，以包含额外的 `WHERE` 子句：

```sql
SELECT Id, Name, SortOrder
FROM Genre
WHERE (Id > 4) AND (Name LIKE '%rock%')
ORDER BY SortOrder DESC
```

在图 12-13 中。注意，行现在根据 `SortOrder` 列按降序排序。

| id | Name | SortOrder |
|---|---|---|
| 9 | Alternative Rock | 9 |
| | Indie Rock | 7 |
| 7 | Rock | |

图 12-13

# 工作原理

SSMS 中的查询设计器是针对你的数据库创建新查询的非常非常有用的工具。你不需要在 SQL 窗格中手动编码整个 SQL 语句，而是使用图表和条件窗格来可视化地创建查询。你还可以使用 SQL 窗格对 SSMS 生成的代码进行手动微调。

执行的最终查询返回了所有包含 "rock" 单词且 ID 大于 4 的行。步骤 8 中所示查询具有一个由两部分组成的 `WHERE` 子句：第一部分将行限制为 ID 大于 4 的行；第二部分过滤出包含文本 "rock" 的行。这两个标准都使用 `AND` 关键字同时应用，因此只返回 `Alternative Rock`、`Indie Rock` 和 `Rock` 类型，而排除了 `Hard Rock` 和 `Grunge` 类型。

Unicode 数据类型允许你存储许多不同语言的文本。在查询中，你通常可以 ID，因为 SQL Server 会为你处理。有关 ID 的更多信息，请查看此文章：http://tinyurl.com/398wn7

最后，结果根据 `SortOrder` 列按降序排序。注意 `SortOrder` 是一个任意选择的名称。你可以使用 `ORDER BY DESC` 语法按降序排列类型。在此示例中，你可能只从一个表中检索类型数据。然而，在现实世界的应用程序中，你可以通过 `JOIN` 获取来自多个相关表的数据。

# 连接数据

`JOIN` 允许你表示一个或多个表之间的关系。例如，你可以使用 `JOIN` 找到发布在特定类型的 Review 表中的所有结果，并选择该类型的某些列。

`JOIN` 的基本语法如下粗体代码：

```sql
SELECT
  SomeColumn
FROM
  LeftTable
  INNER JOIN RightTable ON LeftTable.SomeColumn = RightTable.SomeColumn
```

第一部分是你之前看到的的 `SELECT` 部分，第二部分引入了 `INNER JOIN` 关键字来指定关系。此查询仅返回 `LeftTable` 中在 `RightTable` 中对应的行。例如，为了返回评论及其所属类型的 ID 和标题，你使用此 SQL 语句：

```sql
SELECT
  Review.Id, Review.Title, Review.Genre
FROM
  Review
  INNER JOIN Genre ON Review.GenreId = Genre.Id
```

注意 `SELECT` 语句中的每个列都带有表名前缀。这清楚地说明了你指的是什么，并在多个表具有相似列名时（例如两个表中存在 `id` 列）避免了冲突。

除了返回匹配行的 `INNER JOIN` 之外，你还可以使用 `OUTER JOIN`。`OUTER JOIN` 无论另一个表中是否存在匹配行都会从一个表中检索评论。以下示例返回了系统中的所有类型以及每个类型中的评论：

```sql
SELECT
  Genre.Id, Genre.Name, Review.Title
FROM
  Genre
  LEFT OUTER JOIN Review ON Genre.Id = Review.GenreId
```

对于分配给类型的每个评论，都会返回包含评论标题的唯一行。然而，如果某个类型没有分配评论，该行仍会被返回，如图 12-14 所示：

| Id | Name | Title |
|---|---|---|
| 5 | Indie Rock | Seoul Youth: The Eternal - Takes to get used but then... |
| 5 | Indie Rock | Farm by Dinosaur |
| 6 | Punk | 21st Century Breakdown by Green Day |
| 7 | Rock | NULL |
| 8 | Grunge | NULL |

`Indie Rock` 类型重复多次，对应 `Review` 表中分配给该类型的每条评论。`Punk` 类型只关联了一个评论，因此它只列出一次。

