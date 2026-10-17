
SectionDisplayName="My Custom Section"

SectionPriority="75"

Message="This is plain line of text" />

<mtbwa:WriteCustomSummaryInformation

SectionKey="CustomSection"

SectionDisplayName="My Custom Section"

SectionPriority="75"

Message="Open [Work Item 1] (vstfs://WorkItemTracking/WorkItem/1)." />

<mtbwa:WriteCustomSummaryInformation

SectionKey="OpenedWorkItem"

SectionDisplayName="Latest Activity"

SectionPriority="100"

Message="Deployed to [http://tailspinga/] (http://tailspinga/)." />

# 自定义构建过程以在程序集上标记版本号

此时，你可以可以使用在本章中学习到的所有构建和扩展方法来通过端到端的自定义，以便为程序集文件标记一个递增的版本号。这些文件用于程序集在被 MSBuild 编译时的版本控制。打开构建过程模板以添加此功能，并按照后续步骤进行操作。

www.it-ebooks.info

## 定义自定义构建过程参数

为了允许构建编辑器具有关闭此功能的选项，并创建一个文件规范，你可以暴露自定义构建过程参数以便在构建过程模板内部使用。首先，使用在本章之前指定的创建自定义工作流的方法，创建表 18-2 中列出的构建过程参数。

### 表 18-2: 自定义构建过程参数

| 名称 (NAME) | 方向 (DIRECTION) | 参数类型 (ARGUMENT TYPE) | 默认值 (DEFAULT VALUE) |
| --- | --- | --- | --- |
| StampVersionNumber | In | Boolean | True |
| AssemblyInfoSpec | In | String | "*AssemblyInfo.*.*" |

接下来，你将指定显示给用户的适当元数据，包括一个自定义的“版本控制”（Versioning）类别，它将出现在构建中的基础参数和高级参数之间，如图 18-31 所示。

![](img/aaf6096fc6b4485534c737801bdbc4fd_520_0.png)

图 18-31: 指定显示给用户的适当元数据

此外，由于你想对 .NET 程序集使用四部分版本标准，请将 `BuildNumberFormat` 工作流参数的默认值更改如下：

```
$($BuildDefinitionName)_1.0.0($Version.*)
```

这提供了一个四部分的版本号，自动递增最后的构建号。这依赖于编辑构建定义的人在需要根据标准的 .NET 程序集版本原则更新库时，设置其或她的自定义构建号字符串。

# 484 | 第 18 章 自定义构建过程

## 允许该功能可选的

现在是时候将自定义功能添加到自定义构建过程模板本身了。标记程序集信息源文件的最合适位置应该是紧随从版本控制获取最新版本之后，并且在任何编译之前。如果你使用的是基于默认构建过程模板的自定义构建过程模板，你将在 `AgentScope` 活动内部、显示名为 `Initialize Workspace` 的 `Sequence` 活动之后找到它。

你可以开始通过使用你创建的 `StampVersionNumber` 布尔工作流参数作为 `If` 活动的 `Condition`（条件）参数，来允许该过程完全跳过你正在添加的用于标记程序集版本号的功能。请记住，`If` 允许在设计器中的每个放置位置中仅包含一个条件。因此，你可以向放置位置添加一个新的 `Sequence` 活动，如图 18-32 所示。

![](img/aaf6096fc6b4485534c737801bdbc4fd_521_0.png)

图 18-32: 在放置位置添加一个新的 Sequence 活动

www.it-ebooks.info

你可能会将 `If` 活动的 `DisplayName`（显示名称）更改为“If StampVersionNumber”，并把 `Sequence` 的 `DisplayName` 更改为类似“Stamp Version Number”（标记版本号）的内容，如图 18-32 所示，以提高工作流的可读性。

## 定义本地工作流变量

在标记版本号序列期间你可能需要的某些变量在后续过程中并不需要。选择你之前添加的 `Sequence` 活动，并添加表 18-3 中列出的自定义变量。对于变量的范围，使用你之前添加的 `Sequence` 活动的显示名称，以便变量仅在该标记段落内部使用，如图 18-33 所示。

**表 18-3:** 自定义工作流变量

| 名称 (NAME) | 变量类型 (VARIABLE TYPE) | 默认值 (DEFAULT) |
| --- | --- | --- |
| VersionNumberRegularExpression | String | "\d+\.\d+\.\d+\.\d+" |
| VersionString | String | |
| FullAssemblyInfoSpec | String | |
| AssemblyInfoFiles | IEnumerable<String> | |

![](img/aaf6096fc6b4485534c737801bdbc4fd_522_0.png)

**图 18-33:** 在范围内定义变量

## 初始化工作流变量

在能够有效地使用这些变量之前，你必须将它们初始化为相应的值。`Assign` 活动是初始化工作流变量的理想选择。在之前创建的 `Sequence` 中添加一个新的 `Assign` 活动，将其 `To` 参数设置为如下内容：

```
System.Text.RegularExpressions.Regex(VersionNumberExpression).Match(BuildDetail).Value
```

这创建一个包含版本号的新正则表达式，然后它尝试与构建号进行匹配。`VersionString` 变量现在应该初始化为四部分的版本字符串。

```
System.IO.Path.Combine(SourcesDirectory, VersionString)
```
