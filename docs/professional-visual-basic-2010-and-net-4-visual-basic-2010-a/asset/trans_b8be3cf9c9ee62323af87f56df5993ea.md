

由于每种同步场景都需要不同的决策，SQL Server Compact 支持三种不同的同步定义技术：

+   > **远程数据访问 (RDA)** — RDA 是在 SQL Server Compact 与其较大的兄弟版本之间配置同步的最简单方法。使用 RDA，你在 IIS 下创建一个新的虚拟目录。虚拟目录包含 SQL Server CE Agent DLL。然后客户端应用程序发起同步。可以从单个表中拉取或推送数据，并且可以查询数据的子集。虽然这种方法很诱人，但微软已宣布不太可能继续支持该技术；他们不会再为其添加任何新功能。相反，开发人员被鼓励使用 Sync Services。

+   > **合并复制** — 这是内置于 SQL Server 的复制系统。它是一种以 DBA 为中心的模型，数据库管理员配置应用程序之间共享的数据。然后 SQL Server Agent 安排服务器与客户端之间的同步。这种同步形式功能强大，但也是配置最复杂的形式。它需要在服务器上创建发布和同步计划的权限，以及在客户端上创建订阅的权限。创建合并复制发布仅在 SQL Server Standard Edition 及更高版本上受支持，因此你无法在 SQL Server Express 与 SQL Server Compact 之间创建合并复制。

+   > **Sync Framework** — Sync Framework 提供了 RDA 的简易性与合并复制的稳健性。它们使创建使用 SQL Server Compact 数据库作为本地缓存的应用程序变得非常容易。通过添加少量代码，你也可以将其用于双向同步。

以下是使用 Sync Framework 创建单向同步的示例：

+   1. 创建一个新的 Windows Forms Application 项目（此处命名为 `LocalCache`）。
+   2. 向项目中添加一个新的本地数据库缓存项（见图 12-11）。由于它将用于缓存 pubs 数据库的数据，因此命名为 `PubsCache`。
+   3. 本地数据库缓存项使你能够轻松配置 Sync Framework，因为它会启动数据同步向导。向导的第一步是配置两个连接字符串：服务器和客户端。创建一个新的服务器连接字符串连接到第 10 章中使用的 `pubs` 数据库。完成此操作后，向导将在项目中添加一个新的 SQL Server Compact 数据库并创建客户端连接（见图 12-12）。

![](img/d99870e80390742f93963da7be0b2e61_476_0.png)

# FIGURE 12-10

![](img/d99870e80390742f93963da7be0b2e61_477_0.png)

# FIGURE 12-11

![](img/d99870e80390742f93963da7be0b2e61_477_1.png)

# FIGURE 12-12

4. 配置同步的下一步是添加将要同步的表。单击对话框左下角的 Add 按钮并选择 stores 和 titles 表（见图 12-13）。

打开数据来源窗口。此时，你可以更改用于编辑数据的控件。将用于显示 sales 表的控件更改为 DetailsView，将 ord_num 列的控件更改为 Label，并将 stor_id 和 title_id 的控件更改为 ComboBox（见图 12-15）。这使你能够创建一个一次显示一条记录的表单，并为两个同步列提供下拉字段。

9. 现在你可以从数据来源窗口将 sales 表拖到表单上。这将创建 DetailsView 控件以及 BindingNavigator。它还创建了浏览数据所需的连接。将 stores 表从数据来源窗口拖到 stor_id ComboBox 上。这将添加对本地数据的连接。它还将 ComboBox 的可见文本设置为每个商店的名称，而不是简单地显示商店的 id 值。对 titles 表和 title_id ComboBox 重复此操作。表单现在应与图 12-16 所示相似，你应该能够运行应用程序并浏览数据。

![](img/d99870e80390742f93963da7be0b2e61_479_0.png)

10. 你已准备好向应用程序添加同步代码，但需要一种触发它的方法。在表单顶部的工具栏上单击 Save 按钮之后添加一个新按钮。按以下表格所示设置新按钮的属性：

| 属性 | 值 |
|---|---|
| Name | SyncButton |
| DisplayStyle | Text |
| Text | Sync |

![](img/d99870e80390742f93963da7be0b2e61_479_1.png)

11. 双击新创建的 SyncButton 以添加执行同步的代码。你需要添加什么代码？幸运的是，开发人员已为你编写了大部分代码。右键单击 PubsCache.sync 文件并选择 View Designer 查看设计器。单击右下角的 Show Code Example 链接以显示所需代码（见图 12-17）。

![](img/d99870e80390742f93963da7be0b2e61_479_2.png)

12. 单击 Copy Code to the Clipboard 按钮复制代码。将代码添加到 SyncButton 单击事件中，如以下代码所示。除了执行实际同步的代码外，你还需要添加重新加载数据到 DataSet 的行：

```
Private Sub SyncButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles SyncButton.Click
    Dim syncAgent As PubsCacheSyncAgent = New PubsCacheSyncAgent()
    Dim syncStats As Microsoft.Synchronization.Data.SyncStatistics = _
        syncAgent.Synchronize()
    Me.TitlesTableAdapter.Fill(Me.PubsDataSet.titles)
    Me.StoresTableAdapter.Fill(Me.PubsDataSet.stores)
End Sub
```

LocalCache 中的代码片段

13. 运行应用程序（见图 12-18）。你应该能够查看和编辑 sales 数据。对服务器上的某个商店或标题进行更改。你应该只能在单击 Sync 按钮后看到更改。

Sync Services 和 SQL Server Compact 的添加为 Visual Basic 开发人员提供了又一个客户端配置和数据工具。你可以在不牺牲太多磁盘或内存开销的情况下获得功能强大且经过充分测试的数据存储和查询机制。

![](img/d99870e80390742f93963da7be0b2e61_480_0.png)

FIGURE 12-18

# SQL SERVER 的内置 XML 功能

SQL Server 提供的两个主要 XML 相关功能如下：

+   FOR XML — T-SQL SELECT 语句的 FOR XML 子句使行集能够作为 XML 文档返回。FOR XML 子句生成的 XML 文档在生成的文档层次结构、每列数据转换、二进制数据的表示、生成的 XML 架构以及各种其他 XML 细微差别方面高度可定制。

+   OPENXML — OPENXML 是对 Transact-SQL 的扩展，使存储过程调用能够将 XML 文档作为行集进行操作。随后，此行集可用于执行各种任务，例如 SELECT、INSERT INTO、DELETE 和 UPDATE。

SQL Server 对 OPENXML 的支持只是调用存储过程的问题。能够使用 Visual Basic 结合 ADO.NET 执行存储过程调用的开发人员可以充分利用 SQL Server 对 OPENXML 的支持。FOR XML 查询在使用 ADO.NET 时存在一定的注意事项。要理解此注意事项，请考虑以下对 Northwind 数据库的 FOR XML 查询：

```
SELECT ShipperID, CompanyName, Phone FROM Shippers FOR XML RAW
```

此 FOR XML RAW 查询的输出生成了以下 XML：

```
<row ShipperID="1" CompanyName="Speedy Express" Phone="(314) 555-9831" />
<row ShipperID="2" CompanyName="United Package" Phone="(314) 555-3199" />
<row ShipperID="3" CompanyName="Federal Shipping" Phone="(314) 555-9931" />
```

相同的 FOR XML RAW 查询可以从 ADO.NET 按如下方式执行：

```
Dim adapter As New _
    SqlDataAdapter("SELECT ShipperID, CompanyName, Phone " & _
    "FROM Shippers FOR XML RAW",
    "SERVER=localhost;UID=sa;PWD=sa;Database=Northwind;")

Dim ds As New DataSet
adapter.Fill(ds)
Console.Out.WriteLine(ds.GetXml())
```

