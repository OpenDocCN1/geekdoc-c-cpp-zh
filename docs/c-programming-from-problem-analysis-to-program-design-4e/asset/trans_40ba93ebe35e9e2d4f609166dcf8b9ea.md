
![](img/36e48639a06772bcb0fa1ea2525b33a3_995_0.png)

**FIGURE 14-31**  使用查询生成器修改 SelectCommand CommandText

你可以在 **Query Builder SQL** 面板中输入示例 14-27 中显示的 SQL 语句，或使用 **Diagram** 面板选择要显示的 Department 表中的附加字段。图 14-31 中显示的 SQL 语句与示例 14.27 中显示的内容略有不同。查询生成器会完全限定所有字段名称引用。与示例 14.27 中显示的 student_ID 不同，字段名称前面加上表名和一个点（即 Student.student_ID）。

## 示例 14.27

```
SELECT student_ID, student_FirstName, student_LastName, major_ID,
       student_Phone, major_Name, major_Chair, major_Phone
FROM Student
INNER JOIN Department ON Student.major_ID = Department.major_ID
```

单击 **Query Builder** 窗口上的 **Execute Query** 按钮，会在屏幕底部的 **Results** 面板中显示查询结果返回的记录，如图 14–31 所示。

> 注：实际上，你可以在打开查询生成器后立即在 SQL 面板中输入 SQL 语句。但是，如果没有显示第二个表，你可能无法正确拼写列名。

当你关闭 **Query Builder** 时，系统会询问你是否要使用新添加的 SelectCommand 重新生成 UpdateCommand、InsertCommand 和 DeleteCommand。看到该消息时，你应选择 **No**。根据你正在构建的应用程序，你可能需要返回并重新检查一个或多个 INSERT、DELETE 或 UPDATE SQL 命令。最好不要让它们自动为你重新生成。如果你选择 **Yes**，你可能会看到一条消息，提示“Dynamic SQL generation is not supported against multiple base tables。”该工具无法从涉及多个表的 SELECT 语句生成动态 DELETE、UPDATE 和 INSERT SQL 语句。TableAdapter 的更新功能取决于其主要 SQL SELECT 查询可用的信息量。

> 注：请记住，如果你在项目中保存了数据库的本地副本，则每次启动应用程序时加载的是项目级别的数据库文件。它不会被更新。每次应用程序运行时，都会在 bin\\Debug 目录中存储数据库的新副本。

## 更新 Windows 窗体

DataGridView 对象曾被用于显示数据。你已看到它如何被自定义以以网格状结构显示多行多列数据。请回忆，它最初是通过从 **Data Sources** 窗口将 Student 表节点拖到窗体上来放置在窗体上的。DataGridView 是在从 **Data Sources** 窗口拖动整个表时用于显示数据的默认控件。在表之间建立关系后，你可以向数据网格添加来自第二个表的列。你可以通过在窗体设计模式下选择数据网格的智能标记来完成此操作。**Edit Columns** 选项会显示先前在图 14–17 中显示的对话框。你可以从此对话框中添加新列。如前所述，你还使用此对话框来更改列的任何属性值。图 14–32 说明了从第二个表添加列。

![](img/36e48639a06772bcb0fa1ea2525b33a3_997_0.png)

**FIGURE 14-32** 从第二个表添加字段

Student ID 已被移动，使其显示在第一列中。专业名称和专业主任已添加到网格中。这些字段的 HeaderText 属性值分别设置为 "Department" 和 "Chair"。Phone 已被移除。图 14-33 显示了从多个表检索数据的新设计。

![](img/36e48639a06772bcb0fa1ea2525b33a3_998_0.png)

FIGURE 14-33 从多个表检索数据

图 14-33 所示应用程序生成的输出使用了复制到项目目录中的原始数据库。

### 使用详细信息视图显示数据

除了以网格状结构显示数据外，还提供详细信息视图。当你选择 Details 并将整个表拖到窗体上时，你会为数据集中的每个列获得 Label 和 TextBox 对象，如图 14-34 所示。

图 14-35 显示了 ConfigToolsExampleDetailView 应用程序的输出。

![](img/36e48639a06772bcb0fa1ea2525b33a3_1000_0.png)

FIGURE 14-35 来自 ConfigToolsExampleDetailView 的输出

这些应用程序并未编写任何实际的程序语句。Data Source Configuration 工具用于识别数据源表。数据绑定控件是从 Data Sources 窗口放置到窗体上的。DataSet Designer 用于在表之间创建关系。TableAdapter 使用已识别表的数据填充 Dataset 对象。窗体和数据绑定标签的文本属性已更改。所有这些都是使用集成开发环境中的工具完成的。

## 修改连接字符串

如果你在连接数据库时遇到问题，可能需要修改连接字符串并重新将数据库附加到你的应用程序。你可以使用多种方法更改连接字符串。你之前读到过当连接字符串随应用程序保存时如何更改 XML App.config 文件。另一种方法是使用属性设计器的 Settings 页面修改项目的设置。你可以通过 Solution Explorer 窗口访问此页面。Settings.settings 文件位于 Properties 文件夹内。双击 Settings.settings 文件会打开应用程序的设置文件。从那里，你可以单击 Value 框并浏览以附加数据库文件。图 14-36 同时显示了 Settings.settings 窗口和 App.config 文件。Settings 页面显示在图的上方。

![](img/36e48639a06772bcb0fa1ea2525b33a3_1001_0.png)

**FIGURE 14-36** 修改 Settings.settings 和 App.config 文件

**注意** 你可以将应用程序解决方案文件夹中的 SQL Server 数据库文件复制到包含其他 SQL Server 数据库的目录中。例如，我的 SQL Server 数据库文件存储在

`C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data.`

要查找 SQL Server 数据库文件的路径，请搜索以 `.mdf` 结尾的文件。

如前所述，当你将数据库文件附加到应用程序时，你可能会收到一条消息，询问你是否希望将数据库的本地副本与应用程序一起存储。拥有本地副本在你只打算显示数据时效果很好，也使测试更容易。但是，如果你对数据库进行更改并希望数据库更改对其他应用程序可用，你可能不希望为其制作本地副本。

## 语言集成查询 (LINQ)

正如你在本章中所体验到的，编程语言和数据库在表示和操作数据方面存在差异。程序将数据作为对象进行操作，但程序所需的信息通常存储在关系数据库中。如你之前所见，为了使编程语言能够访问数据库中的信息，它们使用需要将查询指定为字符串的 API。当你编写查询的字符串时，在编译时不会进行错误检查，也没有 IntelliSense 的帮助。情况进一步复杂化的是，每种数据源类型的查询略有不同：SQL 数据库、Access 数据库等等。LINQ 通过让你使用编程语言编写查询来改变这一点。它允许你针对

### 表格 14-9 一些 LINQ 查询运算符

| 查询子句关键字 | 描述 |
|---|---|
| select | 对集合进行投影，检索构成对象的特定数据成员。如果未识别数据成员，则返回所有数据成员。选择会创建一个不同类型的对象，该对象具有与原始类相同数量或部分的数据成员。在表格格式中，select 选择特定的列。 |
| where | where 运算符返回满足一组谓词规则的特定对象。不匹配规则的对象会被过滤掉。 |
| sum/min/max/<br>average/<br>aggregate | 从集合中的每个元素检索某个数值，并分别用它来查找集合中所有元素的总和、最小值、最大值、平均值或聚合值。 |
| join/groupjoin | 使用每个集合中对象的匹配键对两个集合执行内部连接。与 select 运算符一样，结果是不同类的实例化。 |
| take/takewhile | take 运算符从集合中检索前 *n* 个对象；takewhile 使用谓词选择与谓词匹配的对象。 |
| skip/skipwhile | 与 take 和 takewhile 相反。它们都跳过集合中的前 *n* 个对象，或与谓词匹配的对象。 |
| orderby/thenby | 用于根据某个键指定集合中元素的排序顺序。默认是升序。要指定降序，请使用 orderbydescending 运算符。thenby 运算符和 thenbydescending 使你能够在第一个排序内进行第二次排序。 |
| reverse | 反转集合。 |
| groupby | 采用提取键值的委托，并为每个不同的键值返回一个 IGrouping<Key, Values> 对象的集合。然后可以使用 IGrouping 对象枚举特定键值的所有对象。 |
| distinct | 从集合中删除键值的重复实例。 |
| union/intersect/<br>except | 分别用于对两个序列执行并集、交集和差集操作。 |
| count | 检索给定集合中的元素数量。 |

