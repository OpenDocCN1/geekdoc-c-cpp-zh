
- Visual Studio 查找注册表以构建对话框中的类别结构。这些信息可以在 Visual Studio 2010 配置根节点（`Software\Microsoft\Visual Studio\10.0\Config`）下的 `NewProjectTemplates` 键的 `HKEY_CURRENT_USER` 单元中找到。

- 少数模板文件夹包含一个带有 `.vstdir` 的 XML 文件。这些文件用于声明 `.vstdir` 文件所在文件夹内模板的本地化名称和排序。

如图 4-18 所示，“新建项目”对话框显示了三类型的项目模板层次结构节点：

- 项目类型根节点 — 这些与语言相关，或者更准确地说，与语言服务包相关，如 Visual C# 或 Visual Basic。图 4-18 显示了 Visual C# 的示例。

- 伪节点 — 这些是项目根节点的父文件夹。图 4-18 中的“其他语言”和“其他项目类型”提供了很好的示例。

- 模板文件夹节点 — 这些是项目根节点的子节点，它们被映射到下方带有模板文件的物理文件夹。在图 4-18 中，Visual C# 下的 Windows、Web 和 Silverlight 节点就是它们的示例。

![](img/b5597c749e848b27b0d305153ae16106_124_0.png)

**图 4-18:** 项目模板节点类型

创建模板节点层次级的整个过程有点复杂，因此本文讨论不包含所有细节。相反，这里有几点可以帮助你理解基础：

- 为了生成项目模板层次结构，Visual Studio 使用了 `.zip` 存档中的 `.vtemplate` 文件、`NewProjectTemplates` 键存储的注册表键和值，并结合上述的语言包资源（通过注册表值确定）、模板文件夹结构和 `.vstdir` 文件。

项目根节点和伪文件夹节点在注册表中进行了描述，包含本地化名称、排序顺序信息和文件夹嵌套信息。

模板文件夹层次结构遵循 `ProjectTemplates`（随 Visual Studio 2010 安装的模板）的结构，位于 Visual Studio 安装文件夹下的 `\Common7\IDE\ProjectTemplates\`。对于用户模板，位置位于 `我的文档\Visual Studio 10\Templates\ProjectTemplates\`。这些位置的文件夹层次结构被合并以创建项目类型；这些子文件夹中都有 `.vdir` 文件，它可以描述模板文件夹在其父文件夹中的排序顺序。

当用户点击模板文件夹时，该文件夹中的所有模板都会显示出来。IDE 扫描带有 `.zip` 扩展名的文件夹和嵌入的清单以识别项目模板。当找到适当的文件时，IDE 使用模板清单显示有关该项目模板的信息（图标、名称、描述等）。

查看“新建项目”对话框，你可以看到多个项目模板不仅出现在文件夹中，还出现在其他文件夹中。

## 项模板层次结构

“新建项”对话框与“新建项目”对话框一样，使用分级方法列出可用的项模板。

当你向项目添加项时，宿主项目的根类型决定了其物理文件夹。对于机器模板（随 Visual Studio 2010 安装的模板），位置位于 Visual Studio 安装文件夹下的 `\Common7\IDE\ItemTemplates`。对于用户模板，位置位于 `我的文档\Visual Studio 10\Templates\ItemTemplates`。这些位置的文件夹层次结构被合并以创建项目项类别层次结构。如果这些子文件夹中有任何 `.vdir` 文件，它可以描述模板文件夹在其父文件夹中的排序顺序。

Visual Studio 扫描此文件夹结构寻找带有声明为项模板的清单的 `.zip` 文件。它使用清单文件中的信息显示特定文件夹中的项。

根项目类型可能会过滤项模板。在注册表中，每个 Visual Studio 包有一个 `AddItemFilters` 键，该键可以识别项目类型，并列出应从列表中排除的模板目录或具体模板。模板清单有两个项 `<TemplateID>` 和 `<TemplateGroupID>`可以根据项目根类型对项模板进行进一步过滤和分类。

## 模板清单文件

到目前，清单文件是模板的核心组件。模板清单是一个带有 `.vtemplate` 扩展名的 XML 文件，Visual Studio 模板系统主要将其用于以下目的：

- 它识别出模板文件夹中的 `.zip` 文件并非简单的 `.zip` 归包，而是一个模板定义文件。

- 它使用清单文件（manifest）在“新建项目”或“添加新项”对话框中显示有关模板的信息。

- 它检索为新项目或项目项要创建的项列表。

接下来的讨论将详细说明清单文件的结构，并展示一些示例，以帮助你执行与模板相关的常用任务。

### 清单文件的通用结构

```
<VTemplate Type="_type" Version="2.0.0"
xmlns="http://schemas.microsoft.com/developer/vtemplate/2005">
<TemplateData>
  <TemplateContent>
  </TemplateContent>
  <WizardExtension>
  </WizardExtension>
  <WizardData>

  </WizardData>
</VTemplate>
```

`VTemplate` 元素具有一个 `Type` 属性，用于识别模板是项目还是项。它的值可以是 `Project` 或 `Item`。作为一种特殊的模板类型，它也可以具有 `ProjectGroup` 值，该值在稍后稍作解释。

`Version` 属性指定了模板的版本号。自 Visual Studio 2005 以来，该值一直是 `2.0.0`。

以下是另外两个基本元素：

- `<TemplateData>` — 这是用于“新建项目”和“添加新项”对话框的模板分类信息和显示字符。

- `<TemplateContent>` — 这指定了包含在模板的文件。

Visual Studio 允许使用可以为模板添加功能的向导。`<WizardExtension>` 和 `<WizardData>` 元素负责指定实现向导的程序集，并传递向导使用的信息。这些元素是可选的。

让我们查看之前创建的命令处理器（Command Processor）项模板的清单文件。列表 4-5 显示了文件。

### 列表 4-5：命令处理器项模板的清单

```
<VTemplate Version="2.0.0"
  xmlns="http://schemas.microsoft.com/developer/vtemplate/2005" Type="Item">
  <TemplateData>
    <DefaultName>Command Processor</DefaultName>
    <Name>Command Processor</Name>
    <Description>此项创建一个命令处理器类</Description>
    <ProjectType>CSharp</ProjectType>
    <SortOrder>10</SortOrder>
    <Icon>_Template.ico</Icon>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem SubType="Target" FileName="$fileinputname.cs"
      ReplaceParameters="true">CommandProcessor.cs</ProjectItem>
  </TemplateContent>
</VTemplate>
```

与其在这里解释所有细节（稍后将进行），让我们解密这个模板定义的具体内容。

#### `<TemplateData>` 元素

该元素在提供模板的分类和显示信息方面起着关键作用，还定义了一些影响“新建项目”和“添加新文件”对话框行为的点。`<TemplateData>` 没有属性，但它可能包含许多子元素。表 4-1 总结了负责模板显示特性的元素。

### 表 4-1：`<TemplateData>` 子元素 — 显示特性

| 子元素 | 描述 |
|---|---|
| `<Name>` | 此必填元素指定模板在“新建项目”或“添加新项”对话框中显示的名称。 |
| `<Description>` | 此指定模板在“新建项目”或“添加新项”对话框中显示的描述。此元素是必填的。 |
| `<Icon>` | 此指定作为模板图标的图像文件的路径和文件名，该图标出现在“新建项目”或“添加新项”对话框中。 |
| `<PreviewImage>` | 此指定作为在线模板预览图的图像文件的路径和文件名。此预览图显示在“新建项目”、“添加新项”对话框中，以及 Visual Studio 库中。 |
| `<DefaultName>` | 此元素是必填的。对于项目，此元素指定在磁盘上存储项目的目录名称。对于项，它指定源文件的文件名。 |
| `<ProvideDefaultName>` | 此可选元素指定 Visual Studio 项目系统是否会在“添加新项”或“新建项目”对话框中为模板生成默认名称。该元素的文本必须是 `true` 或 `false`，默认值是 `false`。 |
| `<Hidden>` | 此元素指定模板是否出现在“新建项目”或“添加新项”对话框中。该元素的文本必须是 `true` 或 `false`，默认值是 `false`。 |
| `<SortOrder>` | 此可选元素定义了项目或项模板在对话框中的顺序。对于用户模板，此值会被忽略，因为这些值按字母顺序排序。默认值为 100，且所有值必须是十的倍数。排序值低的模板将比排序值高的模板之前出现在“新建项目”或“添加新项”对话框中。 |
| `<NumberOfParentCategoriesToRollUp>` | 此可选值指定了到模板的父类别数量，将在“新建项目”或“添加新项”对话框中显示该模板。例如，如果具有此元数据的模板放置在顶层 Visual C# 节点下方两个文件夹处，且此值设置为 `2`，则该模板也将出现在“新建项目”对话框的 Visual C# 类别节点下。如果未设置此节点，模板将仅出现在其物理所在的节点中。 |
| `<LocationFieldMRUPref>` | 此指定“新建项目”和“添加新项”对话框中最近使用的路径。 |

`<Name>`、`<Description>` 和 `<Icon>` 元素的内容可以从嵌入到 Visual Studio 包的资源中获取。在这种情况下，这些节点的 `Package` 和 `ID` 属性应分别用于程序包 GUID 和资源标识符。

模板根据项目类型设计，并且是特定语言或与语言无关。表 4-2 所示的子元素描述了这些特性。

### 表 4-2：`<TemplateData>` 子元素 — 项目与语言

| 子元素 | 描述 |
| --- | --- |
| `<ProjectType>` | 此值指定了我们将创建的模板类型，并且必须包含以下值之一：<br>- CSharp, FSharp, Visual Basic — 分别创建一个 Visual C#、F# 或 Visual Basic 项目或项。<br>- Web — 指定该模板创建一个 Web 项目或项。在这种情况下，项目或项的语言在 `<ProjectSubType>` 元素中定义。 |
| `<ProjectSubType>` | 这是一个可选元素，为 `<ProjectType>` 元素提供子类别。此值用于两种场景：<br>如果项目是智能设备项目，`SmartDevice-NETCF1` 和 `SmartDevice-NETCF2` 值表示模板目标是 .NET Compact 版本 1.0 或 2.0。<br>如果 `<ProjectType>` 为 Web，此元素指定模板的编程语言。在这种情况下，可用的值 `CSharp` 和 `VisualBasic` 与 Visual C# 和 Visual Basic 语言相关。 |

`<TemplateData>` 的其他子元素仅由项目或项模板处理。你可以将这些元素放入任何清单文件中，未解析的元素会被模板类型忽略。表 4-3 显示了由项模板创建的子元素。

### 表 4-3：`<TemplateData>` 子元素 — 项模板特定元素

| 子元素 | 描述 |
| --- | --- |
| `<TemplateID>` | 此可选元素代表项模板的标识符，该模板通过 `<TemplateGroupID>` 元素分类到项模板组中。如果省略此元素，则使用 `<Name>` 作为项模板的标识符。此元素用于 Visual Studio 包定义项模板的高级场景。 |
| `<TemplateGroupID>` | 此值是可选的，用于指定项模板类别的标识符。此元素用于 Visual Studio 定义项模板的高级场景。 |
| `<SupportsMasterPage>` | 此可选元素仅用于 Web 项目模板，用于指定在“添加新项”对话框中是否启用“选择主页”复选框。该元素的文本必须为 true 或 false，默认值为 false。 |
| `<SupportsCodeSeparation>` | 此可选元素仅用于 Web 项目模板，用于指定在“添加新项”对话框中是否启用“放置在单独文件中”复选框。该元素的文本必须为 true 或 false，默认值为 false。 |
| `<SupportsLanguageDropDown>` | 此可选元素仅用于 Web 项目模板，用于指定在“添加新项”对话框中是否启用“语言”选项。该选项允许您选择从模板创建的新项时要使用的编程语言。该元素的文本必须为 true 或 false，默认值为 false。 |

表 4-4 汇总了特定于项目模板的 `<TemplateData>` 子元素。

#### 表 4-4：`<TemplateData>` 子元素 — 项目模板特定元素

| 子元素 | 描述 |
| :--- | :--- |
| `<BuildOnLoad>` | 此元素指定在从模板创建项目时是否生成解决方案。该元素的文本必须为 true 或 false，默认值为 false。 |
| `<CreateInPlace>` | 此元素指定是在指定位置创建项目并执行参数替换，还是在临时位置执行参数替换并将项目保存到指定位置。如果该元素的值为 true（默认值），则在“新建项目”对话框中指定的 Location创建项目并执行参数替换。如果为 false，则在临时位置执行参数替换，然后将项目复制到指定位置。 |
| `<CreateNewFolder>` | 此元素指定是否为实例的实例化创建一个文件夹。该元素的文本必须为 true 或 false，默认值为 true。托管指定模板的项目项目系统必须支持此选项。 |

#### 表 4-4（续）

| 子元素 | 描述 |
| :--- | :--- |
| `<PromptForSaveOnCreation>` | 此元素指定在创建项目时，是否使用“新建项目”对话框提示用户选择保存位置的保存。如果将此元素设置为 true，则会提示用户选择保存位置。如果为 false，则不会进行提示，在这种情况下将创建一个临时项目。 |
| `<EnableLocationBrowseButton>` | 在“新建项目”对话框中，Location 文本框指定保存新项目的目录。Browse 按钮通过显示“项目位置”对话框帮助您找到此目录，该对话框允许您轻松地导航到计算机上的不同目录，然后将其选择为保存新项目的目录。该文本必须为 true 或 false，表示在“新建项目”对话框中是否显示 Browse 按钮。默认值为 true。 |
| `<LocationField>` | “新建项目”对话框中的 Location 文本框允许用户更改保存新项目的默认目录。此元素指定该文本框应该是启用的、禁用的还是隐藏。因此，元素的值为 Enabled（启用）、Disabled（禁用）和 Hidden（隐藏）。 |

现在你已经熟悉了 `<TemplateData>` 元素，就可以理解 Basic Console 项目模板中以下定义代表的含义了：

```
<TemplateData>
<Name>Basic Console</Name>
<Description>此控制台处理简单命令</Description>
<ProjectType>CSharp</ProjectType>
<ProjectSubType></ProjectSubType>
<Order>1000</Order>
<CreateNewFolder>true</CreateNewFolder>
<DefaultName>Basic Console</DefaultName>
<ProvideDefaultName>true</ProvideDefaultName>
<LocationField>Enabled</LocationField>
<EnableLocationBrowseButton>true</EnableLocationBrowseButton>
<Icon>Template.ico</Icon>
</TemplateData>
```

| 子元素 | 说明 |
|---|---|
| OpenInHelpBrowser | 此可选属性指定当从模板创建项目时，是否应在“帮助”查看器中打开该项。只有本地于项目的 HTML 文件和文本文件可以在帮助浏览器中打开。此属性无法通过此属性打开外部 URL。默认值为 false。 |
| OpenOrder | 此可选属性指定一个数值，表示项目项在各自的视图（编辑器、Web 浏览器或帮助程序）中打开的顺序。所有值均为 10 的倍数。OpenOrder 值较小的项目先打开。 |

基本命令控制台清单的 `<TemplateContent>` 部分如下所示：
