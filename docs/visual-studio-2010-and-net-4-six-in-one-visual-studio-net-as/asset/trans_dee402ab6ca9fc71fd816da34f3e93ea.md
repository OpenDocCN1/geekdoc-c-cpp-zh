

<Reference> 元素包含两个嵌套元素：

- <Assembly> — 这是强制性的，它包含包含要被引用的程序集名称。该名称可以是程序集的短名称（例如上一个示例所示的 `System.Data.dll`），也可以是其强类型名称（例如 `MyCompany.Widgets.dll`）。
- <Url> — 这是一个可选元素，可以设置为链接，提供有关该程序集和解封装类型的更多详细信息。

## 代码片段函数

<literal> 和 <Object> 元素可能包含一个名为 <Function> 的子元素，该子元素仅由 C# 代码编辑器处理。<Function> 包含一个带有参数的名称，并且当字面量或对象占位符在编辑器中获得焦点时，它就会被执行。

表 3-3 汇总了 C# 代码编辑器可以处理的函数名：

| FUNCTION | DESCRIPTION |
| --- | --- |
| ClassName() | 获取包含插入片段的类名称。此函数在创建构造函数、声明代码或实例化语句时非常有用。 |
| GenerateSwitchCases(EnumLiteral) | 根据 EnumLiteral 定义的类型生成带有相关 case 语句的 switch 语句。EnumParameter 可以是枚举类型，也可以是对具有枚举类型的 <Literal> 的引用。 |
| SimpleTypeName(TypeName) | 将 TypeName 参数中的名称还原为片段插入处上下文中的最简单形式。此函数通过移除类型引用中不必要的命名空间标记，帮助您提高代码的可读性。 |

让我们创建一个示例来展示如何使用这些代码片段。列表 3-3 中的示例有些略显生硬，可能没有太大实际价值，但它确实有助于说明这些函数。它将创建一个枚举成员字段、一个公共构造函数，用于调试并提供一个 switch 语句。

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

如你所示，列表 3-3 包含了五个字面量，其中三个是只读的（`Editable` 属性值为 `false`）。这是刻意为之，因为这些字面量用于定义函数值，而不是供用户编辑。

Debug 字面量使用 `SimpleTypeName` 函数根据其使用的上下文缩短全类型名。如果使用了 `System.Diagnostics` 命名空间，您应该有一个 `using` 句。如果没有这个 `using` 句，在调用 `WriteLine` 成员之前将插入完整的 `System.Diagnostics.Debug` 类型名。

ClassName 字面量使用 `ClassName` 函数替换为片段插入处的类名。

列表 3-1 中复合的部分之一是 cases 字面量依赖于 `GenerateSwitchCases` 函数。如你所示，该函数的参数是另一个字面量 `enumExpr`，用户可以编辑它。

导入此片段后，您可以使用 `log` 快捷键来调用它。图 3-15 显示了如何在 C# 控制台应用程序的 `Program` 类中使用它。

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

*(注：由于原始文本中存在大量重复的段落和说明，此处已根据指令“不要重复输出原文”的原则，对核心逻辑部分进行了翻译和整合。)*

