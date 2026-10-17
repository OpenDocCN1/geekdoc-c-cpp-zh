
你可以在代码中使用占位符，例如上例中的`$end$`和`$selected$`。`$end$`标记在插入代码片段后放置光标的位置。`$selected$`代表文档中选中的文本，当调用环绕类型（surrounding-type）代码片段时，它会被插入其中。

例如，假设你在编辑器中选择了以下文本：

```
Value1,
Value2,
Value3,
```

在此处使用“环绕”功能应用枚举代码片段，将产生以下代码：

```
enum MyEnum
{
    Value1,
    Value2,
    Value3
}
```

光标将放置在`Value3`之后。

代码元素具有具有以下语义的属性：

```xml
<Code Language="C#" Delimiter="&quot;">
<![CDATA[Console.WriteLine("*message*");]]>
</Code>
```

- `Kind` — 这指定了代码片段包含的代码类型，因此指定了代码片段必须插入的位置。它的值可以是`method`、`body`、`decl`、`type`、`file`和`any`。此属性被 Visual Editor 使用，但会被 C# 编辑器忽略。Visual Basic 编辑器在调用代码片段时仅会在正确的位置。例如，当你处于方法体内部时，无法激活类型声明代码片段。C# 编辑器不会进行任何更改，并允许在编辑器源代码的任何位置激活代码片段。

## 声明字面量和对象

在模板中，你可以为字面量参数和对象使用占位符，以便用户更改默认值。例如，在类声明代码片段中，类型名称可以是字面量参数。

这些占位符嵌套在直接位于`<Snippet>`元素中的`<Declarations>`元素中。字面量参数通过`<Declarations>`元素进行描述。字面量参数通过`<Literal>`元素描述，而对象引用通过`<Object>`元素定义。

这些占位符在`<Snippet>`元素中嵌套，如下：

- `<Literal>` — 元素用于在代码片段中引用项。例如，字符串应声明为字面量。
- `<Object>` — 元素用于在代码片段中引用项。例如，Windows 控件、ASP.NET 控件、类型实例应声明为对象。

这两个元素都有一个名为`Editable`的可选属性，默认值为`true`。你可以将其设置为`false`以禁用编辑。

### 表 3-2：`<Literal>`的子元素

| 元素 | 说明 |
| --- | --- |
| `<ID>` | 此必需元素指定字面量或对象的标识符。你必须使用`<ID>`元素。 |
| `<Default>` | 此必需元素指定代码片段插入时参数或对象的默认值。 |
| `<Type>` | 此元素指定字面量或对象的类型。必须有一个`<Type>`元素。 |
| `<Tooltip>` | 此可选元素指定用于字面量或对象的提示。 |
| `<Function>` | 此可选元素指定在代码片段中执行的函数。目前仅用于 C# 编写的）。 |

### 语言特定特性

如前所述，某些代码片段功能的实现取决于语言上下文。例如，Visual Basic 不支持环绕片段（surrounding-snippets），而其他语言支持。相反，Visual Basic 允许在插入代码模板后显示或隐藏代码。

接下来的章节将检查与片段结构相关的特定语言特性。

### `<Imports>`和`<References>`

`<Snippet>`部分有两个子元素仅受 Visual Basic 支持。当你将代码插入文本时，即使它是语法正确的，也可能导致整个源文件无法编译。最重要的原因之一是代码中使用的类型和成员引用在当时无法解析。

你可以使用`<Imports>`元素来定义代码片段插入后应添加的命名空间。例如，如果你的代码片段是关于创建和使用文件的，它可能使用了`System.IO`命名空间。与其在代码模板中使用全类型名称，你可以在`<Snippet>`部分添加以下元素：

```xml
<Imports>
<Import>
  <Namespace>System.IO</Namespace>
</Import>
</Imports>
```

`<Imports>`是包含多个`<Import>`元素的容器，每个元素恰好有一个`<Namespace>`元素。

有时插入的代码应用于项目未引用的程序集中的类型。`<References>`元素是一个包含多个`<Reference>`元素的容器，用于在片段插入代码时提供引用程序集的方法。示例示例了如何使用`<References>`：

```xml
<References>
<Reference>
  <Assembly>System.Data.dll</Assembly>
  <Url>http://msdn.microsoft.com/en-us/library/system.data.(vs.100).aspx</Url>
</Reference>
<Reference>
  <Assembly>
    MyCompany.Widgets.dll, Version=1.0, Culture=neutral,
    PublicKeyToken=0123456789abcdef
  </Assembly>
  <Url>http://mycompany.com/widgets/overview.html</Url>
</Reference>
</References>
```

`<Reference>`元素包含两个嵌套元素：

- `<Assembly>` — 这是强制性的，它包含包含要被引用的程序集名称。该名称可以是程序集的短名称，例如上一个示例所示的`System.Data.dll`，也可以是其强类型名称，例如`MyCompany.Widgets.dll`。
- `<Url>` — 这是一个可选元素，可以设置为链接，提供有关该程序集和解封装类型的更多详细信息。

## 代码片段函数

`<literal>`和`<Object>`元素可能包含一个名为`<Function>`的子元素，该子元素仅由 C# 代码编辑器处理。`<Function>`包含一个带有参数的名称，并且当字面量或对象占位符在编辑器中获得焦点时，它就会被执行。

### 表 3-3 C# 代码编辑器可以处理的函数名

| FUNCTION | DESCRIPTION |
| --- | --- |
| `ClassName()` | 获取包含插入片段的类名称。此函数在创建构造函数、声明代码或实例化语句时非常有用。 |
| `GenerateSwitchCases(EnumLiteral)` | 根据`EnumLiteral`定义的类型生成带有相关`case`语句的`switch`语句。`EnumParameter`可以是枚举类型，也可以是对具有枚举类型的`<Literal>`的引用。 |
| `SimpleTypeName(TypeName)` | 将`TypeName`参数中的名称还原为片段插入处上下文中的最简单形式。此函数通过移除类型引用中不必要的命名空间标记，帮助您提高代码的可读性。 |

让我们创建一个示例来展示如何使用这些代码片段。列表 3-3 中的示例有些略显生硬，可能没有太大实际价值，但它确实有助于说明这些函数。它将创建一个枚举成员字段、一个公共构造函数，用于调试并提供一个`switch`语句。

```xml
<xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
 <CodeSnippet Format="1.0">
  <Header>
```

## 列表 3-3 (续)

```xml
<Title>枚举日志器</Title>
<Shortcut>loge</Shortcut>
<Author>Istvan (DiveDeeper) Novak</Author>
<Description>为枚举创建一个日志记录方法。</Description>
</Header>
<Snippet>
  <Declarations>
    <Literal>
      <Id>Type</Id>
      <Tooltip>枚举成员类型</Tooltip>
      <Default>EnumType</Default>
    </Literal>
    <Literal Editable="false">
      <Id>Debug</Id>
      <Function>SimpleTypeName(System.Diagnostics.Debug)</Function>
    </Literal>
    <Literal Editable="false">
      <Id>ClassName</Id>
      <Tooltip>类名</Tooltip>
      <Function>ClassName()</Function>
      <Default>ClassNameDefault</Default>
    </Literal>
    <Literal>
      <Id>enumExpr</Id>
      <Tooltip>用于 switch 的枚举</Tooltip>
      <Default>switchExpr</Default>
    </Literal>
    <Literal Editable="false">
      <Id>cases</Id>
      <Function>GenerateSwitchCases($enumExpr)</Function>
      <Default>default:</Default>
    </Literal>
  </Declarations>
  <Code Language="C#">
  <![CDATA[
  private $type $EnumValue;

  public $className($type enumValue)
  {
    _EnumValue = enumValue;
    $Debug.WriteLine("Value : (0)", _EnumValue);
    switch ($enumExpr)
    {
      $cases$
    }
  }
  ]]>
  </Code>
</Snippet>
</CodeSnippets>
```

如你所示，列表 3-3 包含了五个字面量，其中三个是只读的（`Editable`属性值为`false`）。这是刻意为之，因为这些字面量用于定义函数值，而不是供用户编辑。

`Debug`字面量使用`SimpleTypeName`函数根据其使用的上下文缩短全类型名。如果使用了`System.Diagnostics`命名空间，您应该有一个`using`句。如果没有这个`using`句，在调用`WriteLine`成员之前将插入完整的`System.Diagnostics.Debug`类型名。

`ClassName`字面量使用`ClassName`函数替换为片段插入处的类名。

列表 3-1 中复合的部分之一是`cases`字面量依赖于`GenerateSwitchCases`函数。如你所示，该函数的参数是另一个字面量`enumExpr`，用户可以编辑它。

导入此片段后，您可以使用`log`快捷键来调用它。图 3-15 显示了如何在 C# 控制台应用程序的`Program`类中使用它。

```csharp
Program.cs
FileAssociations.Program
enumValue
class Program
    static void Main(string[] args)
    {
        Console.WriteLine("");
        Console.WriteLine("Hello");
    }
```

代码片段可以组成分级文件夹结构。例如，Visual C# 代码片段包含以下文件夹：

- `NetFX3` — 这些是针对 .NET 3.0 新特性的代码片段。
- `OfficeDevelopment` — 这些是帮助完成 Microsoft Office 开发任务的代码片段。
- `other` — 这是存放其他代码片段的文件夹。目前，在此处可以找到几个 WF 代码片段。
- `Refactoring` — 这些是由 C# 语言服务用于重构函数的代码片段。
- `Visual C#` — 这些是与 C# 语言相关的通用代码片段（属性、事件、类等）。

系统文件夹拥有所谓的索引文件来列出代码片段。这些文件确实存在，其名称在 Visual Basic 中为`SnippetIndex.xml`，对于其他语言为`SnippetsIndex.xml`。这些索引文件的格式超出了本书的范围，但你可以自由地打开并查看它们。

### 添加和删除代码片段

代码片段管理器（Code Snippets Manager）允许你添加包含代码片段的自定义文件夹。如前文所述，代码片段管理器仅存储文件夹的路径。通过使用“添加”按钮，你可以仅为所选语言添加顶级文件夹。当你点击“添加”按钮时，会弹出一个带有代码片段目录的文件夹选择对话框，让你指定要添加的文件夹。在你将文件夹添加到目录后，它将显示在文件夹列表中。你可以立即浏览其内容。

当你在列表中选择一个文件夹并点击“删除”按钮时，你可以将其从代码库中移除。当然，此操作不会删除文件夹的内容；它只是将其从代码片段管理器处理的列表中剔除掉。你只能移除顶级文件夹。当你选择子文件夹或代码片段时，“删除”按钮将被禁用。

请小心删除系统文件夹。代码片段管理器允许你删除它们，且不会进行任何确认。如果你不小心删除了系统文件夹，稍后可以通过选择你移除的物理文件夹来重新添加它。在再次添加后，Visual Studio 会将其识别为系统文件夹并进行正确处理。

### 导入代码片段

如果你有一个组织良好的文件夹，包含大量代码片段，可以使用代码片段管理器将该文件夹添加到相应的语言中。然而，如果你有尚未组织在任何文件夹中的`.snippet`文件，可以对其进行导入，并将其中的代码片段成为你库的一部分。

在选择了一个或多个`.snippet`文件后，点击“导入”按钮开始导入代码片段。图 3-19 显示的“导入代码片段”对话框将弹出，让你为每个文件选择导入文件夹。

![](img/b5597c749e848b27b0d305153ae16106_96_0.png)

**图 3-19：** 使用导入代码片段对话框

窗口的左格显示代码片段文件夹，右格列出要导入的用户文件夹。当导入代码片段文件时，文件会被物理复制到所选文件夹中。如图 3-19 所示，你可以为每个单独的文件设置导入文件夹。一个文件可以复制到一个或多个文件夹中。图 3-19 展示了这样的情况：选定的代码片段都要导入到“My Code Snippets”文件夹中，而其中仅有一个准备放入“My Special Snippets”。

代码代码片段管理器允许你仅将代码片段导入到顶级用户文件夹。

你可以选择支持不同语言的代码片段文件夹。“导入代码片段”对话框会根据其宿主语言对其进行分组。你可以点击“上一个”和“下一个”按钮在语言之间翻页，并选择合适的文件夹。对话框左侧代码片段面板上方的标签会告诉你面板列出的文件的宿主语言。

当你点击“完成”按钮时，代码片段文件将立即导入到所选文件夹并准备就绪。

## 高级代码片段功能

到本章为止，你已经学习了代码片段的概念、`.snippet`文件格式以及代码片段管理器的作用。让我们看看代码片段的高级功能。

## 一个文件中的多个代码片段

`.snippet`文件的设计初衷就是允许包含多个`<Snippet>`元素，如代码段 4 所示。

代码段 4：一个文件中的多个代码片段
