
| 解锁其他用户的更改 | ☐ | ☐ |
| 撤销其他用户的更改 | ☐ | ☐ |
| 管理标记 | ☐ | ☐ |
| 管理权限 | ☐ | ☐ |
| 签入其他用户的更改 | ☐ | ☐ |
| 合并 | ☑ | ☐ |
| 管理分支 | ☐ | ☐ |

**图 12-8**：默认权限

# SharePoint 项目团队门户文档库设置

如果在创建团队项目期间创建了 SharePoint 团队项目门户，则可以在过程模板中指定该新 SharePoint 站点文档库的初始内容。此外，还指定了过程模板的过程指南文档。

图 12-19 显示了使用 MSF Agile 过程模板创建团队项目后生成的默认文档库、文件夹结构的某些文档。

> **警告**：您无法通过自定义过程模板文件来自定义 Microsoft Excel 报告和 SharePoint 仪表板。这些构件是根据您在“新建团队项目”向导中的选择为团队项目创建。

# 292 | 第 12 章 自定义模板

![](img/aaf6096fc6b4485534c737801bdbc4fd_329_0.png)

图-12：默认文档库、文件夹存储和某些可用项

# SQL Server 报告定义

远程站点（Remote Sites）中的初始文件夹结构和报告也可以在模板中指定。图 12-20 显示了在团队项目向导期间将上传到 Reports Manager 站点的文件夹和 SQL 报告定义文件列表。

![](img/aaf6096fc6b4485534c737801bdbc4fd_329_1.png)

图-12：文件夹和 SQL Server 报告定义文件

# 使用过程模板编辑器

与其编辑每个 XML 文件，您可以使用随最新版本 Team Foundation Server Power Tools 附带的过程模板编辑器。过程模板编辑器由一组集成到 Visual Studio Team Explorer 中的工具组成，您可以使用它编辑工作项类型定义、过程模板文件、导出/导入工作项定义、创建/修改全局列表，并包含一个工作项资源管理器以查看团队项目集合中字段的详细信息。

# 使用过程模板编辑器 | 293

Team Foundation Server Power Tools 安装程序可在 Visual Studio Gallery 获取并定期更新。找到 Power Tools 安装程序最新下载的最快方法是搜索词“Team Foundation Server Power Tools”。目前，整个 Visual Studio 产品线的所有 Power Tools 列表位于 `http://aka.ms/TFPowerTools`，但在 Team Foundation Server 发布新版本后，它可能不是完全最新的。在开始安装 Power Tools 之前，请确保关闭所有 Visual Studio 实例，因为安装程序将设置和配置多个加载项。

> 注意：始终确保您使用的是最新版本的 Team Foundation Server。Power Tools 每月都会发布错误修复和新功能。

# 与过程模板工作

与其直接在服务器上编辑工作项（这是一种方法），最佳实践是下载过程模板并使用您偏好的 XML 编辑器编辑。> 注意：第 10 章提供了有关使用过程模板的更多信息

当您将过程模板存储在离线位置时，可以打开 `ProcessTemplate.xml`。图 12-21 显示了团队项目集合中过程模板中的工作项。

# 294 | 第 12 章 自定义模板

![](img/aaf6096fc6b4485534c737801bdbc4fd_330_0.png)

图 12-21：编辑器窗口

从窗口中，您可以轻松编辑工作项类型。例如，您可以通过点击“编辑”按钮来编辑工作项类型。> 注意：如果您想了解更多关于过程模板的信息，可以阅读帮助文档：`C:\Program Files (x86)\Microsoft Foundation Server\2012\Help\ProcessEditor.mht`

# 使用 XML 编辑器和 WITAdmin

管理过程模板和工作项定义的另一种方法是使用您偏好的 XML 编辑器编辑文件，并使用工具导出和导入工作项定义。XML 架构在 MSDN 库中有详细文档：

- 模板架构—`http://aka.ms/ProcessTemplateSchema`
- 工作项类型架构—`http://aka.ms/WITSchema`

名为 `witadmin.exe` 的命令行工具是在您安装 Visual Studio Team Explorer 时安装的。在开发人员命令提示符中（并在具有相应权限的情况下），您可以执行多项管理工作跟踪系统的功能。表 12-6 显示了一些可用命令，但您可以通过执行 `witadmin.exe /` 获取完整列表。

# 表 12-6：witadmin 示例命令

| 命令 | 说明 |
| --- | --- |
| Listfields | 特别适用于您需要团队项目集合中所有字段及其详细信息时。每个条目甚至会列出使用该字段的工作项类型和团队项目。使用 `/unused` 关时，还可以获取团队项目集中完全未使用的字段列表。 |
| Changefield | 允许在字段创建后更新现有字段的属性。例如，您可以更新任何名称属性，但您会发现某些属性无法更改。一个例子是工作项类型字段。除非它是 HTML 和 PlainText 之间，否则无法更改工作项类型。 |
| Deletefield | 在字段被任何团队项目的任何工作项类型未使用后，将其完全删除。如果这是使用指定字段的最后一个团队项目，它将在下次仓库处理周期期间从仓库中删除。 |
| Listwit | 有助于列出团队项目中可用的工作项类型。 |
| Rename | 即使团队项目中已有该类型的工作项，也可以重命名现有的工作项类型。例如，您可以在未来的某时刻决定将 Requirement 工作项类型重命名为 User Story 或 Feature。 |
| destroywi, destroywitid | 允许在团队项目中完全删除特定的工作项或工作项类型及其所有现有项。数据不会在仓库中被删除，直到发生完整构建为止。 |

# 表 12-6（续）

| 命令 | 描述 |
| --- | --- |
| exportwitid, importwitid | 允许从团队项目导出和导入工作项类型定义。如果当前存在工作项类型，它将与新的工作项类型定义替换。如果进行了导入，现有的工作项将得到更新。 |
| Listlinktypes | 列出团队项目集合中可用的链接集。 |
| exportlinktype, importlinktype | 允许为团队项目集合导出和导入新的链接类型。如果链接已存在，将对其进行更新。 |
| exportcategories, importcategories | 允许为特定的团队项目导出和导入新的工作项类别定义。如果工作项类别已存在，将对其进行更新。 |
| exportglobalist, importglobalist, destroyglobalist | 分别允许导出、导入和删除团队项目的全局列表定义。如果全局列表同名，它将与新导入的全局列表定义替换。 |
| exportileprocessconfig, exportcommonconfig, importprocessconfig, importcommonconfig | 允许你自定义若干过程配置元素以满足你的敏捷和 Scrum 流程。这些元素控制在 Team Web Access 中提供的交互工具和视觉显示。这在使用 MSF CMMI 和第三方模板来适当配置敏捷工具时也有用。 |
| exportglobalworkflow, importglobalworkflow | 允许你导出或导入全局工作流定义，允许你像在本章之前讨论的那样，在多个类型的工作项之间共享字段和列表项定义。 |

## 向过程模板部署更新

现在你已经掌握了如何完全自定义你的过程模板，你可以以多种方式使用该新过程模板。你可以在以下两种场景之一部署你的过程模板：

- 1. 更新现有团队项目的单个组件
- 2. 在新团队项目的创建向导中使用它

## 在 Team Foundation Server 中上传过程模板

为了让项目集合管理员使用自定义的过程模板创建新项目，你必须将该过程模板添加到团队项目集合的可用过程模板中。你可以使用本章之前描述的过程模板管理器（Process Template Manager）窗口（如图 12-1 和 12-2 所示）来管理可用的过程模板。

你会发现有一个“上传”（Upload）按钮。在上传期间，将对过程模板进行合规性验证，并在验证期间遇到的任何错误都将在消息框中显示。如果上传按钮未启用，你可能连接到了托管的（Hosted）Team Foundation Service 实例。由于 Team Foundation Service 目前不支持自定义过程模板，因此上传按钮将是禁用的。

## 在现有团队项目中编辑工作项

为现有团队项目部署过程模板更新的最常见方法是更新你的工作项类型定义。你可以使用 `witadmin.exe` 的 `import` 命令行选项为团队项目中的现有工作项类型定义导入新定义。

## 关注事项

更新现有团队项目的工作项类型定义可能特别具有风险。你应该始终在测试环境中测试你的工作项类型定义更新，该环境应等待成功的仓库处理周期发生，且更新过程中不会产生任何错误。

某些工作项定义的更改的影响很小，而另一些更改可能需要花费更多精力才能完全实现。例如，向现有的工作项类型定义中添加新的可报告字段不会影响 Team Foundation Service 的健康，除非它与另一个团队项目中具有相同名称但属性不同的字段冲突。每当下一个仓库处理周期开始时，你都会开始看到问题，因为冲突的字段定义将进一步阻碍仓库处理。

另一个影响更大的场景是更改现有工作项类型定义的状态名称。你必须处理旧状态中的所有工作项。此外，可能存在使用该特定名称的现有工作项查询以及依赖旧状态名称的标准报告，所有这些都必须更新。

> 注意：可能用于更改现有工作项状态名称的方法是：在测试环境中测试你的工作项类型定义更新，该环境应等待成功的仓库处理周期发生，且更新过程中不会产生任何错误。

[自定义敏捷工具](https://aka.ms/AgileProcess)

## 工作量、剩余工作和栈优先级

- 工作量（Effort）
- 剩余工作（Remaining Work）
- 栈优先级（Stack Rank）

用于“任务”工作类型中“剩余工作”字段剩余值所使用的单位。如果您想使用“小时”以外的内容（例如故事点），则可以在此处编辑该设置：

```xml
<xml version="1.0" encoding="utf-8"?>
<CommonProjectConfiguration>
  <TypeFields>
    <TypeField rename="Microsoft.VSTS.Scheduling.RemainingWork"
      type="RemainingWork" format="{0} h" />
    <TypeField rename="Microsoft.VSTS.Common.StackRank" type="Order" />
    <TypeField rename="Microsoft.VSTS.Scheduling.StoryPoints" type="Effort" />
  </TypeFields>
</CommonProjectConfiguration>
```

此外，产品待办列表优先级工具将在项目重新编译时自动使用项目的“堆栈排序”（stack rank）。您使用“顺序”（Order）字段，它将自动填充值，以便待办列表项能够从低到高的顺序进行排序。

## 定义团队

默认情况下，Team Foundation 项目中的团队是根据它们拥有的“区域路径”（Area Path）节点定义的。但是，如果您不使用区域路径来定义团队，可以使用备用字段。例如，您可能在所有工作项上都有一个名为“部门”（Department）的自定义字段，用以定义哪些工作项属于它们。您可以通过在以下常用配置中设置“团队”（Team）字段的使用来实现：

```xml
<xml version="1.0" encoding="utf-8"?>
<CommonProjectConfiguration>
  <TypeFields>
    <TypeField rename="System.AreaPath" type="Team" />
  </TypeFields>
</CommonProjectConfiguration>
```

## 其他过程配置自定义

在 `CommonConfiguration.xml` 和 `AgileConfiguration.xml` 文件中提供了其他类型的过程配置。以下列表包含了一些额外自定义的示例：

- 从产品待办列表视图的“快速添加”面板中移除项。例如，除了设置标题外，您可能还想为每个新项指定工作量估算。
- 从待办列表和迭代视图中添加或删除列。
- 更改工作项和团队成员可以分配的活动列表。
- 更改计算迭代容量和渲染实时燃尽图时使用的工作日。默认情况下，周六和周日被视为非工作日，但您可以将额外的工作移除或包含为非工作日。
- 在不同的工具选项中配置作父项和子项的项目类型。
- 自定义用于利益相关者反馈工具的可用选项和工作项。

## 通用工作项类型自定义

对现有的过程模板通常会进行某些自定义。以下讨论提供了其中一些常用自定义的概述。

## 添加新状态

团队通常认为标准过程模板中提供的状态并不很好地适应他们的团队流程。他们可能决定在工作流中创建一个新状态。

如果避免添加过多的状态，可以让终端用户在与工作项的正常日常交互中更容易理解和使用这些状态。这还将减少为了自定义报告以利用每个状态而所需的工作量。相反，您可以使用“状态”和“原因”的组合来帮助您在查询或报告工作项时区分特定状态的工作项。

添加状态可以很容易地完成。例如，如果您想在工作项类型定义中添加一个“提议”（Proposed）状态，可以向以下添加片段：

```xml
<WORKFLOW>
<STATES>
  <STATE value="Proposed">
  </STATE>
  <STATE value="Active">
</FIELDS>
  <FIELD refname="Microsoft.VSTS.Common.ClosedDate">
    <EMPTY />
  </FIELD>
  <FIELD refname="Microsoft.VSTS.Common.ClosedBy">
...
```

您可能还想移动字段（例如，清空“关闭日期”和“关闭人”字段），并更改某些现有的转换以利用新状态。

> 注意：关于在工作项类型定义中添加新状态的完整文章可以在 MSDN 库中找到：`http://aka.ms/WITCustomizeStates`。

然而，添加状态意味着报告将受到影响。MSF Agile 过程中的某些报告可能会受到影响：

- **Bug 状态报告**——此报告有一个堆叠面积图，按状态列出 Bug，并为每个状态分配了特定的颜色。此外，它显示了分配给每个团队成员的“已解决”（Resolved）和“活动”（Active）状态的 Bug 数量。
- **故事概述报告**——此报告显示了每个用户故事打开了多少个 Bug，并以分段条形图显示。
- **所有迭代状态**——此报告显示了每个迭代路径中存在多少个 Bug，并按状态以分段条形图显示。

## 显示自定义链接类型
