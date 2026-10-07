
由于此图没有使用数据仓库功能，它是最新的，不会产生任何延迟。这使其成为发布到例如项目状态邮件的理想人选。

更多信息请参阅第 13 章。

在 2010 版本之前，不支持对关系型仓库进行报告。从 2010 版本开始，情况不再如此。仓库之上提供了几个视图来支持报告。这些视图使得查询数据更加容易，并保持了未来版本的兼容性。此外，命名规范已标准化，以区分事实表和维度表。例如，`dbo.WorkItem` 现在是 `dbo.DimWorkItem`，将其标识为维度表。

> **注意** 本章后面提供了关于事实表和维的详细讨论。

除了支持对关系型仓库的查询，工作项跟踪适配器还进行了更新以提高性能。新的适配器现在从操作存储移动到关系型仓库的速度比之前的版本更快。适配器的目标是在正常运行期间将工作项跟踪的延迟保持在五分钟。

在 2012 版本中，关系型仓库的唯一架构更改是：

- 在迭代中增加了开始日期结束日期。
- 删除了 2010 版本中用于仓库配置的一些字段。

# 分析服务立方体的变更

尽管 Team Foundation Server 2005 和 2008 中的立方体提供了有用数据，并且客户使用良好，但仍有改进空间。除了支持架构改进外，Team Foundation Server 2010 的变更改进了可用性、查询性能和处理性能。

Team Foundation Server 2010 对立方体架构的主要更改包括：

- 将“当前工作项”（Current Work Item）和“工作项历史”（Work Item History）度量组合并到“工作项”（Work Item）度量组中。现在只需包含日期度量即可显示历史趋势。

![](img/aaf6096fc6b4485534c737801bdbc4fd_372_0.png)

区域（Area）和迭代（Iteration）维度已作为真正的层次结构合并到工作项（Work Item）维度。

部分维度名称已更新，使其更具意义并提供上下文，特别是在查看整个列表时。例如，平台（Platform）现在是构建平台（Build Platform）。

以“Related...”开头的维度已移动到链接工作项（Linked Work Item）维度。

本章稍后将对度（measures）进行更详细的讨论。

Team Foundation Server 2010 对立方体架构的主要新增包括：

- 立方体现在通过链接工作项（Linked Work Item）和工作项（Work Item）维度支持工作项的层次结构和链接。
- 工作项类型现在可以按类别分组。例如，Bug 类别组包含 Bug 和缺陷（Defect）工作项类型。如果你的团队项目之间使用了不同的术语，并且需要跨所有项目生成一份有意义的报告，这将非常有用。
- 区域路径（Area Path）和迭代路径（Iteration Path）现在作为工作项维度的属性可用。这允许你在报告中跟踪扁平字符串（而不是层次结构）。

如图 14-1 所示，工作项维度中添加了显示，以便于对字段进行分组，而不是仅仅显示一个列表。

| Work Item |
| VSTS Build | VSTS-CMM | VSTS-Code-Review | VSTS-Common | VSTS-Scheduling | VSTS-Team |
| Work Item:Area Path | Work Item:Iteration Path | Work Item:Previous State | Work Item:System:AssignedTo | Work Item:System:ChangedBy |

**图 14-1：工作项维度中的显示文件夹**

> **注意：** 有关数据仓库更改及其背后原因的更多信息，请参阅 John Socha-Leialodha 的三部分文章，标题为“将 Team Foundation Server 2008 报告升级到 2010”（第一部分见：http://aka.ms/UpgradeTfsReports1；第二部分见：http://aka.ms/UpgradeTfsReports2；第三部分见：http://aka.ms/UpgradeTfsReports3）。另请参阅 MSDN 文档“Analysis Services 立方体架构的更改与新增”，地址：http://aka.ms/TfsCubeChanges。

# 可选且更丰富的 SharePoint 集成

与 SharePoint 的集成是 Team Foundation Server 的重要功能。然而，该集成的安装和配置一直是问题的严重来源。与此版本中旨在支持不同服务器拓扑结构的其他架构更改一起，SharePoint 集成现在是可选的。

如果你想使用 SharePoint 集成功能，可以在安装时或以后配置 SharePoint。配置选项设计得非常灵活。

Team Foundation Server 2012 集成同时支持 SharePoint 2007 和 SharePoint 2010。

> **警告：** 当 Team Foundation Server 配置为基础配置或安装在客户端操作系统（如 Windows 8）上时，报告和 SharePoint 集成功能将不可用。如果你使用了任何此类配置并希望启用报告功能，则必须在服务器操作系统上使用标准或高级配置。

# TEAM FOUNDATION SERVER 数据仓库

Team Foundation Server 的报告功能和数据仓库功能由表 14-1 所示的三个存储组成。

**表 14-1：Team Foundation Server 报告数据存储**

| 数据存储 | 数据库名称 | 特性 |
|---|---|---|
| 运行型 (Operational) | `Tfs_Configuration`, `Tfs_Collection` | 规范化，针对检索最新数据进行了优化，且具有事务性。 |
| 关系型仓库数据库 | `Tfs_Warehouse` | 具有星型架构，并包含所有用于分析的历史数据。 |
| Analysis Services 立方体 | `Tfs_Analysis` | 数据经过预聚合、预索引，并包含高级分析功能。 |

除了这三个数据存储外，还有一组计划作业，用于在存储器之间移动数据：

- 仓库适配器作业（有时称为同步作业）定期将更改从运行存储复制到关系型数据库。
- 分析处理作业插入立方体以开始增量或全量处理。

图 14-2 显示了这种数据移动的高层表示。

![](img/aaf6096fc6b4485534c738014fd375_0)

**图 14-2：Team Foundation Server 数据仓库架构**

## 运行型存储 (Operational Stores)

Team Foundation Server 的运行型存储只是支持日常操作的数据库。在之前的版本中，不同的区域有不同的数据库；在 Foundation 2010 中，它们被合并到了单一的 `Tfs_Collection` 中。这些数据库的架构针对报告进行了优化，而不是针对历史数据。

不应直接访问运行型存储。访问它们的唯一接口是通过立方体。

## 关系型仓库数据库与仓库适配器 (Relational Warehouse Database and Warehouse Adapters)

关系型仓库数据库将数据存储在组织为星型架构的表中。星型架构的核心被称为事实表，相关表表示维度。例如，`dbo.CurrentItem` 为运行存储中的每个工作项提供一行。维度表存储给定维度的值。例如，Person 维度被 Work Items 事实表引用。你将在本章后面学习更多关于事实表和维度的知识。

Team Foundation Server 中的每个组件对存储数据的要求不同。运行存储的仓库适配器负责将数据传输到仓库。当你向工作项类型添加新字段并将其标记为可报告时，仓库适配器将对立方体执行架构更改。

然而，这种方法的缺点是，如果你对关系型仓库或立方体进行自定义，必须将其作为自定义仓库适配器进行部署。否则，当仓库重建时，你的自定义内容将会丢失。

> 注意 与之前的 Team Foundation Server 版本一样，具有 `Html` 数据类型的字段不会存储在关系型数据仓库中。因此，无法对这些字段进行查询；你必须使用 Work Item Tracking 模型来查询和检索它们。

### 查询当前工作项视图

使用 `CurrentWorkItemView`，你可以查询关系型数据仓库并使用 Work Item Tracking 模型检索工作项列表。例如，以下是一个工作项查询 (WIQ)，它返回 Contoso 项目中分配给 John Smith 的所有未关闭 Bug：

```sql
SELECT
[System.Id],
[Microsoft.VSTS.Common.StackRank],
[Microsoft.VSTS.Common.Priority],
[Microsoft.VSTS.Common.Severity],
[System.State], [System.Title]
FROM WorkItems
WHERE [System.Project] = 'Contoso'
AND [System.AssignedTo] = 'John Smith'
AND [System.WorkItemType] = 'Bug'
AND [System.State] <> 'Closed'
ORDER BY
[System.State],
[Microsoft.VSTS.Common.StackRank],
[Microsoft.VSTS.Common.Priority],
[Microsoft.VSTS.Common.Severity],
[System.Id]
```

以下是等效查询，从关系型数据仓库中检索相同的数据：

```sql
SELECT
[System.Id],
[Microsoft.VSTS.Common.StackRank],
[Microsoft.VSTS.Common.Priority],
[Microsoft.VSTS.Common.Severity],
[System.State],
[System.Title]
FROM CurrentWorkItemView
WHERE
[ProjectPath] = '\ContosoCollection\Contoso'
AND [System.AssignedTo] = 'John Smith'
AND [System.WorkItemType] = 'Bug'
AND [System.State] <> 'Closed'
ORDER BY
[System.State],
[Microsoft.VSTS.Common.StackRank],
[Microsoft.VSTS.Common.Priority],
[Microsoft.VSTS.Common.Severity],
[System.Id]
```

### 动态检索 Web 地址

人们想要做的操作之一是从报告中的工作项提供指向该工作项 Web Access 视图的超链接。这非常有用，因为它允许其他无需安装 Visual Studio 的情况下与工作项进行交互。

为了能够创建超链接，你需要知道服务器的地址。此外，与其将 URL 作为报告参数呈现或硬编码，理想的方法是以某种方式从数据仓库中检索它。但你可能会问，如何做到呢？

在 SQL 查询内部，关系型数据仓库最初看起来很困难。但是，通过 `DimToolArtifactDisplayUrl` 表中的 `ToolArtifactDisplayUrl` 字段，你可以轻松找到它。

以下 SQL 查询实质上取了第一个构件显示 URL，并检索 `/CollectionName/WorkItemTracking/WorkItem.aspx?artifactMoniker` 之前的字符串部分。这意味着无论服务器是否配置了虚拟目录 (/tf/)，也无论是否使用 HTTPS、自定义端口号等，它都将继续工作。

```sql
SELECT TOP 1
SUBSTRING(
ToolArtifactDisplayUrl,
0,
PATINDEX(
'/' + ProjectNodeName + '\',
ToolArtifactDisplayUrl
),
1,
'/web/' AS WebAccessBaseUrl
FROM DimToolArtifactDisplayUrl tp
INNER JOIN DimTeamProjectCollectionSK
ON tp.ProjectNodeSK = DimToolArtifactDisplayUrl.TeamProjectCollectionSK
WHERE WorkItemType = 'WorkItemTracking/Workitem'
AND ProjectNodeTypeTypeName = 'Team Project Collection'
```

### 查询工作项历史视图

你可以构建一个“截至（as of）”查询，返回在特定日期之前修改过的每个工作项的最后记录。例如，以下“截至”查询返回了截至 2011 年 12 月底的剩余工作：

```sql
SELECT System, Microsoft.VSTS_Scheduling_RemainingWork
FROM WorkItemHistoryView WHERE SystemChangedDate < '1/1/2012'
AND SystemRevisedDate >= '1/1/2012'
AND RecordCount > 0
AND ProjectPath = '\ContosoCollection\Contoso'
```

### 查询关系型数据仓库的其他考虑

关系型数据仓库不适用于所有查询，因此某些查询使用操作存储的 Work Item Tracking 模型会更快。Team Foundation Server 2010 引入了多个项目集合，这些集合共享关系型数据仓库和立方体。

在对仓库编写查询时，需要记住三个重要的考虑因素：

1. 使用 `ProjectPath` 或 `ProjectGUID` 作为过滤器。项目团队名称在同一逻辑服务器上的多个集合中并不一定是唯一的，而项目路径是带有名称的完全限定路径，且项目的 GUID 是唯一的。
2. 使用唯一键进行联接。例如，工作项 ID 在仓库中不再保证是唯一的，因为相同的工作项 ID 可能存在于不同的团队项目集合中。
3. 注意补偿记录（compensating records）。每当工作项被更新时，仓库中就会添加一对记录。第一条记录会抵消之前的记录。这使得某些类型的关系型数据仓库查询变得变得更快。

> 注意 有关补偿记录的更多信息，请参阅 MSDN 上的“Compensating Records”http://aka.ms/TfsCompensatingRecords 以及“Work Item Tracking Compensating Records”http://aka.ms/TfsCompensatingBlog。

## Analysis Services 立方体

关系型数据仓库中的表不适用于所有查询，因此某些查询使用使用操作存储的 Work Item Tracking 模型会更快。Team Foundation Server 2010 引入了多个项目集合，这些集合共享关系型数据仓库和立方体。

在对仓库编写查询时，需要记住三个重要的考虑因素：

- 使用 `ProjectPath` 或 `ProjectGUID` 作为过滤器。项目团队名称在同一逻辑服务器上的多个集合中并不一定是唯一的，而项目路径是带有名称的完全限定路径，且项目的 GUID 是唯一的。
- 使用唯一键进行联接。例如，工作项 ID 在仓库中不再保证是唯一的，因为相同的工作项 ID 可能存在于不同的团队项目集合中。
- 注意补偿记录。每当工作项被更新时，仓库中就会添加一对记录。第一条记录会抵消之前的记录。这使得某些类型的关系型数据仓库查询变得更快。

# SharePoint 扩展

为了让项目能够与 SharePoint 集，Team Foundation Server（TFS）必须与 SharePoint Web 应用程序关联。为了配置此关联，SharePoint 服务器必须安装并配置适用于 SharePoint 的 Team Foundation Server 扩展（Extensions for SharePoint Products）。

并不要求 SharePoint 安装在 Team Foundation Server 同一台服务器上，甚至不需要由同一组人员管理。许多组织已经拥有现有的 SharePoint 农场，只要安装并配置了扩展，Team Foundation Server 就可以与该农场集成。

扩展包含站点模板、Web门户以及 SharePoint 团队定时器，用于维护团队项目与项目门户之间的关联等。

> 欲更多信息，请参阅 http://aka.ms/Tfs2012SPExt 中的“Extensions for SharePoint Products”。

# Excel 服务与仪表板兼容性

Excel 服务是 SharePoint 企业版的一个功能。它允许将 Excel 工作簿在 SharePoint 服务器上渲染，并以网页的形式呈现给用户。由于以下原因，这非常有用：

- *对于报告生成者，可以在 Excel 中创建数据透视表和数据透视图。*
- *对于报告接收者，不需要额外的软件。报告就是简单的网页。*

> 有关手动集成 Team Foundation Server 和 SharePoint 的详细说明，您应该咨询 MSD 上的文章。请查看 http://aka.ms/Tfs2012AddSP 中的“Add a SharePoint Web Application to Your Deployment”，以及 http://aka.ms/Tfs2012PadashSettings 中的“Configure Settings for Dashboard Compatibility”。

# 向现有项目添加项目门户和报告

出于某些原因，您的团队项目可能没有关联项目门户或报告，例如在以下场景：

- *在创建团队项目时，服务器或团队集合可能尚未配置报告或 SharePoint 集成。*
