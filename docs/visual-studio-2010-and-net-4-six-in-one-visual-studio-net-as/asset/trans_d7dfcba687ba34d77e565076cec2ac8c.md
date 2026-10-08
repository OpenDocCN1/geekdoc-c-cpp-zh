

- 它识别出模板文件夹中的 .zip 文件并非简单的 .zip 归包，而是一个模板定义文件。
- 它使用清单文件（manifest）在“新建项目”或“添加新项”对话框中显示有关模板的信息。
- 它检索为新项目或项目项要创建的项列表。

接下来的讨论将详细说明清单文件的结构，并展示一些示例，以帮助你执行与模板相关的常用任务。

## 清单文件的通用结构

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

VTemplate 元素具有一个 `Type` 属性，用于识别模板是项目还是项。它的值可以是 `Project` 或 `Item`。作为一种特殊的模板类型，它也可以具有 `ProjectGroup` 值，该值在稍后稍作解释。

`Version` 属性指定了模板的版本号。自 Visual Studio 2005 以来，该值一直是 `2.0.0`。

以下是另外两个基本元素：

- `<TemplateData>` — 这是用于“新建项目”和“添加新项”对话框的模板分类信息和显示字符。
- `<TemplateContent>` — 这指定了包含在模板的文件。

Visual Studio 允许使用可以为模板添加功能的向导。`<WizardExtension>` 和 `<WizardData>` 元素负责指定实现向导的程序集，并传递向导使用的信息。这些元素是可选的。

让我们查看之前创建的命令处理器（Command Processor）项模板的清单文件。列表 4-5 显示了文件。

## 列表 4-5：命令处理器项模板的清单

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

## <TemplateData> 元素

该元素在提供模板的分类和显示信息方面起着关键作用，还定义了一些影响“新建项目”和“添加新文件”对话框行为的点。`<TemplateData>` 没有属性，但它可能包含许多子元素。表 4-1 总结了负责模板显示特性的元素。

## 表 4-1：<TemplateData> 子元素 — 显示特性

| 子元素 | 描述 |
|---|---|
| `<Name>` | 此必填元素指定模板在“新建项目”或“添加新项”对话框中显示的名称。 |
| `<Description>` | 此指定模板在“新建项目”或“添加新项”对话框中显示的描述。此元素是必填的。 |
| `<Icon>` | 此指定作为模板图标的图像文件的路径和文件名，该图标出现在“新建项目”或“添加新项”对话框中。 |
| `<PreviewImage>` | 此指定作为在线模板预览图的图像文件的路径和文件名。此预览图显示在“新建项目”、“添加新项”对话框中，以及 Visual Studio 库中。 | |
| `<DefaultName>` | 此元素是必填的。对于项目，此元素指定在磁盘上存储项目的目录名称。对于项，它指定源文件的文件名。 |
| `<ProvideDefaultName>` | 此可选元素指定 Visual Studio 项目系统是否会在“添加新项”或“新建项目”对话框中为模板生成默认名称。该元素的文本必须是 `true` 或 `false`，默认值是 `false`。 |
| `<Hidden>` | 此元素指定模板是否出现在“新建项目”或“添加新项”对话框中。该元素的文本必须是 `true` 或 `false`，默认值是 `false`。 |
| `<SortOrder>` | 此可选元素定义了项目或项模板在对话框中的顺序。对于用户模板，此值会被忽略，因为这些值按字母顺序排序。默认值为 100，且所有值必须是十的倍数。排序值低的模板将比排序值高的模板之前出现在“新建项目”或“添加新项”对话框中。 |
| `<NumberOfParentCategoriesToRollUp>` | 此可选值指定了到模板的父类别数量，将在“新建项目”或“添加新项”对话框中显示该模板。例如，如果具有此元数据的模板放置在顶层 Visual C# 节点下方两个文件夹处，且此值设置为 `2`，则该模板也将出现在“新建项目”对话框的 Visual C# 类别节点下。如果未设置此节点，模板将仅出现在其物理所在的节点中。 |
| `<LocationFieldMRUPref>` | 此指定“新建项目”和“添加新项”对话框中最近使用的路径。 |

`<Name>`、`<Description>` 和 `<Icon>` 元素的内容可以从嵌入到 Visual Studio 包的资源中获取。在这种情况下，这些节点的 `Package` 和 `ID` 属性应分别用于程序包 GUID 和资源标识符。

模板根据项目类型设计，并且是特定语言或与语言无关。表 4-2 所示的子元素描述了这些特性。

## 表 4-2：<TemplateData> 子元素 — 项目与语言

| 子元素 | 描述 |
| --- | --- |
| `<ProjectType>` | 此值指定了我们将创建的模板类型，并且必须包含以下值之一：
- CSharp, FSharp, Visual Basic — 分别创建一个 Visual C#、F# 或 Visual Basic 项目或项。
- Web — 指定该模板创建一个 Web 项目或项。在这种情况下，项目或项的语言在 `<ProjectSubType>` 元素中定义。 |
| `<ProjectSubType>` | 这是一个可选元素，为 `<ProjectType>` 元素提供子类别。此值用于两种场景：
如果项目是智能设备项目，`SmartDevice-NETCF1` 和 `SmartDevice-NETCF2` 值表示模板目标是 .NET Compact 版本 1.0 或 2.0。
如果 `<ProjectType>` 为 Web，此元素指定模板的编程语言。在这种情况下，可用的值 `CSharp` 和 `VisualBasic` 与 Visual C# 和 Visual Basic 语言相关。 |

`<TemplateData>` 的其他子元素仅由项目或项模板处理。你可以将这些元素放入任何清单文件中，未解析的元素会被模板类型忽略。表 4-3 显示了由项模板创建的子元素。

## 表 4-3：<TemplateData> 子元素 — 项模板特定元素

| 子元素 | 描述 |
| --- | --- |
| `<TemplateID>` | 此可选元素代表项模板的标识符，该模板通过 `<TemplateGroupID>` 元素分类到项模板组中。如果省略此元素，则使用 `<Name>` 作为项模板的标识符。此元素用于 Visual Studio 包定义项模板的高级场景。 |
| `<TemplateGroupID>` | 此值是可选的，用于指定项模板类别的标识符。此元素用于 Visual Studio 定义项模板的高级场景。 |

