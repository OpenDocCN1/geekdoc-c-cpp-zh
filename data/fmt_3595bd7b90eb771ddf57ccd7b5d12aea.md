
在应用程序中使用 SQL Server Compact 数据库的最简单方法是将它用作独立数据库。虽然你得不到同步的好处，但你确实获得了 SQL Server Compact 更简单（也更小）的部署优势。然而，SQL Server Compact 的真正威力在你将其与完整 SQL Server 数据库的同步一起使用时才会显现。这使你能够更轻松地创建既可在离线又可在在线环境下工作的应用程序。

### 连接到 SQL Server Compact 数据库

与 SQL Server 的其他版本一样，连接到 SQL Server Compact 数据库的关键在于连接字符串。然而，由于 SQL Server Compact 在服务器和集成安全性方面的功能不同，用于连接数据库的选项也不同，其中最重要的是在表 12-1 中描述的选项。只能在 IDE 中设置数据源和密码值。

#### 表 12-1：SQL Server Compact 连接选项

| 选项 | 描述 |
|---|---|
| Provider name | `System.Data.SqlServerCe` |
| Data source | 指向 SDF 文件。由于该文件通常包含在项目中，值可以使用 `DataDirectory` 快捷方式编写：`DataSource=|DataDirectory|\DatabaseName.sdf;` |
| Password | 用于加密数据库的密码。 |
| Max buffer size | 在 SQL Server Compact 将更改刷新到磁盘之前使用的最大内存量，以千字节为单位。默认值是 640，这对每个人来说都足够了。 |
| Max database size | 数据库的最大大小，以兆字节为单位。默认值是 256MB（SQL Server Compact 在设备上运行时为 128MB），最大值是 4096MB（4GB）。 |
| Mode | 数据库文件将如何打开。此值可以是 Read Only、Read Write、Exclusive 或 Shared Read。默认值 Read Write 应该使用，除非你的数据库有特殊需求。 |
| Autoshrink threshold | 由于 SQL Server Compact 数据库会按需增长，因此在需要按需收缩时也可能出现情况，例如当大量数据被删除或需要临时表的复杂操作完成后。当这种情况发生时，此设置标识数据库何时以及收缩多少。默认情况下，SQL Server Compact 会在可用空间空闲 60% 时收缩数据库。通常，除非空间非常紧张，否则你不需要更改此设置。 |

将 SQL Server Compact 用作本地独立数据库在创建小型、易于部署的应用程序时很有用。你可以通过创建一个简单的应用程序将联系人数据存储在 SQL Server Compact 数据库中来看到这一点：

- 1. 创建一个新的 Windows 窗体应用程序项目，命名为 `LocalDatabase`，然后通过右键单击项目并选择 `Add Item` 来添加一个新的本地数据库到你的应用程序（见图 12-1）。

![](img/d99870e80390742f93963da7be0b2e61_472_0.png)

#### 图 12-1

- 2. 添加新数据库后，Visual Studio 还会向项目添加一个新的数据集并启动 Data Source Configuration Wizard。由于你没有使用数据库检索服务器数据，DataSet 最初将为空（见图 12-2）。单击 Finish 以添加新的 DataSet。你稍后会添加表。

![](img/d99870e80390742f93963da7be0b2e61_473_0.png)

#### 图 12-2

3. 在项目中双击 `Contacts.sdf` 文件以在 Server Explorer 窗口中打开它。你现在可以向数据库添加一个名为 `Contacts` 的新表，如图 12-3 所示，并在以下表格中描述。

| 列 | 数据类型 | 描述 |
|---|---|---|
| id | Int | 这应设置为不允许空值，并作为表的 primary key。记住将 Identity 设置为 true。 |
| FirstName | NVarChar (50) | Allow Nulls 应设置为 false。 |
| LastName | NVarChar (50) | Allow Nulls 应设置为 false。 |
| EMail | NVarChar (100) | Allow Nulls 应设置为 true。 |

![](img/d99870e80390742f93963da7be0b2e61_473_1.png)

#### 图 12-3

4. 在 Solution Explorer 中，双击之前添加的 `ContactsDataSet` 以打开设计器并将新创建的表拖到表面上（见图 12-4）。

5. 通过单击 Data Sources 选项卡在 Visual Studio 中打开 Data Sources 窗口。你应该会看到 `ContactsDataSet`，其中包含 `Contacts` 表。将 `Contacts` 表拖到窗体上以创建 DataGridView 控件和导航器（见图 12-5）。你现在应该能够运行应用程序并添加一些数据。

6. 如果你查看 `Contacts.sdf` 文件的内容，你可能会感到沮丧，因为看不到任何数据。这是因为它不是实际写入的数据库。如果你查看应用程序的 `/bin/debug` 文件夹，你会看到实际的数据库，其中包含添加的数据（见图 12-6）。

![](img/d99870e80390742f93963da7be0b2e61_474_0.png)

![](img/d99870e80390742f93963da7be0b2e61_474_1.png)

![](img/d99870e80390742f93963da7be0b2e61_474_2.png)

### 同步数据

如前所述，虽然你可以使用 SQL Server Compact 作为独立数据库，但它在与远程数据库和同步结合使用时真正表现出色。同步使你在查询数据库时减少所需的网络流量，同时仍在客户端保持最新数据。它可能是单向同步，将最新的服务器更改拉到客户端，也可能是双向的，保持客户端和服务器同步。最佳选择取决于情况。你会在多种场景下在应用程序中使用同步：

- 远程数据镜像应用程序 — 这些应用程序仅将本地数据库用作主数据库的本地副本，通常是数据的子集。在此场景中，如图 12-7 所示，数据流仅单向：从服务器数据库到客户端。最常见的是产品信息、新闻或客户数据，客户端会读取但不会更改。

![](img/d99870e80390742f93963da7be0b2e61_474_3.png)

- 远程数据录入应用程序 — 这些包括销售或 Field Force Automation（SFA 和 FFA）应用程序，例如经典的“旅行销售代理”应用程序。在此场景中，给定数据行仅在一个方向上流动：参考数据下传到客户端，插入上传到服务器，如图 12-8 所示。与远程数据镜像应用程序一样，通常在客户端工作站上安装数据的子集，通常是目录信息和应用程序离线前所需的任何参考数据。然后销售代理外出，进行销售。偶尔，应用程序重新连接到网络时，新客户和销售数据会上传到主数据库，并将更新的目录数据发送到客户端。

- 简单队列应用程序 — 这些应用程序是前一场景的特殊情况。应用程序仅写入本地数据库，并使用同步将更改的数据推送到服务器数据库。这里的区别部分在于意图；这里客户端上的本地数据库用作临时存储空间。定期同步在服务器和客户端连接时在两者之间移动数据。此场景如图 12-9 所示，可提高应用程序的整体性能，特别是在服务器和客户端之间连接缓慢时。它还提供了在网络不可用时访问应用程序的能力。

- 远程数据库应用程序 — 这些应用程序将远程数据库视为数据的“主”副本。在此场景中，如图 12-10 所示，数据可能在客户端或服务器上更改，并且更改在两个方向流动。这是同步客户端最危险的场景，因为数据可能已在两个（或更多）位置以不同方式更改。因此，需要某种形式的冲突解决，以及指定哪些更改优先的策略（例如，最后一次更改覆盖数据，必须手动处理所有冲突以选择有效数据，或组织结构图中职位最高的人所做的更改获胜）。在构建同步解决方案时，最好尽可能避免或限制此场景。

![](img/d99870e80390742f93963da7be0b2e61_475_0.png)

图中标注：Clients inserts submitted on synchronization；Reference data from server；Application stores data locally while offline；Data from server；When network is available, data is pushed to server periodically；Application stores data locally。

Disconnected　　Connected

图 12-8　　　　　　　　　　　 图 12-9

由于每种同步场景都需要不同的决策，SQL Server Compact 支持三种不同的同步定义技术：

+ > **远程数据访问 (RDA)** — RDA 是在 SQL Server Compact 与其较大的兄弟版本之间配置同步的最简单方法。使用 RDA，你在 IIS 下创建一个新的虚拟目录。虚拟目录包含 SQL Server CE Agent DLL。然后客户端应用程序发起同步。可以从单个表中拉取或推送数据，并且可以查询数据的子集。虽然这种方法很诱人，但微软已宣布不太可能继续支持该技术；他们不会再为其添加任何新功能。相反，开发人员被鼓励使用 Sync Services。

+ > **合并复制** — 这是内置于 SQL Server 的复制系统。它是一种以 DBA 为中心的模型，数据库管理员配置应用程序之间共享的数据。然后 SQL Server Agent 安排服务器与客户端之间的同步。这种同步形式功能强大，但也是配置最复杂的形式。它需要在服务器上创建发布和同步计划的权限，以及在客户端上创建订阅的权限。创建合并复制发布仅在 SQL Server Standard Edition 及更高版本上受支持，因此你无法在 SQL Server Express 与 SQL Server Compact 之间创建合并复制。

+ > **Sync Framework** — Sync Framework 提供了 RDA 的简易性与合并复制的稳健性。它们使创建使用 SQL Server Compact 数据库作为本地缓存的应用程序变得非常容易。通过添加少量代码，你也可以将其用于双向同步。

以下是使用 Sync Framework 创建单向同步的示例：

+ 1. 创建一个新的 Windows Forms Application 项目（此处命名为 `LocalCache`）。
+ 2. 向项目中添加一个新的本地数据库缓存项（见图 12-11）。由于它将用于缓存 `pubs` 数据库的数据，因此命名为 `PubsCache`。
+ 3. 本地数据库缓存项使你能够轻松配置 Sync Framework，因为它会启动数据同步向导。向导的第一步是配置两个连接字符串：服务器和客户端。创建一个新的服务器连接字符串连接到第 10 章中使用的 `pubs` 数据库。完成此操作后，向导将在项目中添加一个新的 SQL Server Compact 数据库并创建客户端连接（见图 12-12）。

![](img/d99870e80390742f93963da7be0b2e61_476_0.png)

## FIGURE 12-10

![](img/d99870e80390742f93963da7be0b2e61_477_0.png)

## FIGURE 12-11

![](img/d99870e80390742f93963da7be0b2e61_477_1.png)

## FIGURE 12-12

4. 配置同步的下一步是添加将要同步的表。单击对话框左下角的 Add 按钮并选择 `stores` 和 `titles` 表（见图 12-13）。

打开数据来源窗口。此时，你可以更改用于编辑数据的控件。将用于显示 `sales` 表的控件更改为 DetailsView，将 `ord_num` 列的控件更改为 Label，并将 `stor_id` 和 `title_id` 的控件更改为 ComboBox（见图 12-15）。这使你能够创建一个一次显示一条记录的表单，并为两个同步列提供下拉字段。

9. 现在你可以从数据来源窗口将 `sales` 表拖到表单上。这将创建 DetailsView 控件以及 BindingNavigator。它还创建了浏览数据所需的连接。将 `stores` 表从数据来源窗口拖到 `stor_id` ComboBox 上。这将添加对本地数据的连接。它还将 ComboBox 的可见文本设置为每个商店的名称，而不是简单地显示商店的 id 值。对 `titles` 表和 `title_id` ComboBox 重复此操作。表单现在应与图 12-16 所示相似，你应该能够运行应用程序并浏览数据。

![](img/d99870e80390742f93963da7be0b2e61_479_0.png)

10. 你已准备好向应用程序添加同步代码，但需要一种触发它的方法。在表单顶部的工具栏上单击 Save 按钮之后添加一个新按钮。按以下表格所示设置新按钮的属性：

| 属性 | 值 |
|---|---|
| Name | `SyncButton` |
| DisplayStyle | Text |
| Text | Sync |

![](img/d99870e80390742f93963da7be0b2e61_479_1.png)

11. 双击新创建的 `SyncButton` 以添加执行同步的代码。你需要添加什么代码？幸运的是，开发人员已为你编写了大部分代码。右键单击 `PubsCache.sync` 文件并选择 View Designer 查看设计器。单击右下角的 Show Code Example 链接以显示所需代码（见图 12-17）。

![](img/d99870e80390742f93963da7be0b2e61_479_2.png)

12. 单击 Copy Code to the Clipboard 按钮复制代码。将代码添加到 `SyncButton` 单击事件中，如以下代码所示。除了执行实际同步的代码外，你还需要添加重新加载数据到 DataSet 的行：

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

13. 运行应用程序（见图 12-18）。你应该能够查看和编辑 `sales` 数据。对服务器上的某个商店或标题进行更改。你应该只能在单击 Sync 按钮后看到更改。

Sync Services 和 SQL Server Compact 的添加为 Visual Basic 开发人员提供了又一个客户端配置和数据工具。你可以在不牺牲太多磁盘或内存开销的情况下获得功能强大且经过充分测试的数据存储和查询机制。

![](img/d99870e80390742f93963da7be0b2e61_480_0.png)

FIGURE 12-18

## SQL SERVER 的内置 XML 功能

SQL Server 提供的两个主要 XML 相关功能如下：

+ FOR XML — T-SQL SELECT 语句的 FOR XML 子句使行集能够作为 XML 文档返回。FOR XML 子句生成的 XML 文档在生成的文档层次结构、每列数据转换、二进制数据的表示、生成的 XML 架构以及各种其他 XML 细微差别方面高度可定制。

+ OPENXML — OPENXML 是对 Transact-SQL 的扩展，使存储过程调用能够将 XML 文档作为行集进行操作。随后，此行集可用于执行各种任务，例如 SELECT、INSERT INTO、DELETE 和 UPDATE。

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
```
