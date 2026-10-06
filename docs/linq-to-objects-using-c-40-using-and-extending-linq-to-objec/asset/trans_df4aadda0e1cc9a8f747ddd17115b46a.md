

# 动态类型 245

为了使这变得更加简单，`System.Dynamic.DynamicObject` 类型提供了一个新的动态类型。

任何传统的对象类型都可以被声明为 `dynamic` 类型。对于所有没有实现 `IDynamicMetaObjectProvider` 接口的动态对象，将使用 `Microsoft.CSharp.RuntimeBinder` 在运行时查找属性和方法调用。图 8-1 所示的示例代码显示了 Intellisense 气泡正尝试声明一个声明为 `dynamic` 的整数类型。（运行时通过初始化表达式解析类型，就像局部类型推断的 `var` 关键字一样。）即使方法调用在项目的任何地方都没有定义，在设计时或编译时也不会发生任何编译错误。当执行此代码时，运行时将使用反射尝试查找并执行虚构的方法 `MethodNotDefinedAnywhere`，这当然会抛出异常失败：

Microsoft.CSharp.RuntimeBinder.RuntimeBinderException: 'int' 不包含 'MethodNotDefinedAnywhere' 的定义。

```
dynamic o = 1;
o.MethodNotDefinedAnywhere();
dynamic.expression
此操作将在运行时解析
```

图 8-1 任何声明为 `dynamic` 类型的对象都在运行时解析。在编译时不会报告任何错误。

如果该方法已实际声明，它将像任何传统的方法或属性调用一样被简单调用。

拥有一个没有实现 `IDynamicObject` 接口的类型应该是罕见的。当类型在编译时已知，不应使用 `dynamic` 关键字来代替适当的类型定义。在处理匿名类型时，也不应使用它来代替 `var` 关键字，因为该类型在编译时是知的。`dynamic` 关键字应该仅用于声明 `IDynamicMetaObjectProvider` 的实现者，并用于与其他动态语言进行互操作以及 COM 互操作。

# 246 章节 C# 4.0 特性

何时使用 VAR 和 DYNAMIC 类型声明。根据情况应该使用哪种类型定义这可能会让人感到困惑。以下是我的建议：

- **具体类型（Concrete type）**——只要你在编写代码时知道类型就使用它。如果你在定义字段、属性或返回类型时知道该类型——就使用它！

- **var 关键字**——在声明匿名类型或捕获投影到匿名类型的 LINQ 查询结果时使用它。

- **dynamic 关键字**——仅在声明动态类型时使用，这通常意味着实现了 `IDynamicMetaObjectProvider` 的类型。这些可以是自定义类型，或者是 Microsoft 为 COM 互操作提供的运行时绑定器之一，用于与 IronPython 和 IronRuby 等动态语言互操作。声明未实现此接口的类型会导致运行时开销。

特定的绑定器是为了支持特定的目的编写的。IronRuby、IronPython 和 COM 互操作只是在 C# 4.0 内部支持动态语言行为的可用绑定器中的。然而，你可以编写自己的绑定器并使用这些类型来解决一些常见的编码问题，正如你很快将在一个示例中看到的，在该示例中，使用自定义动态类型暴露文本文件数据，并将这些数据用作 LINQ to Objects 查询的源。

# 在 LINQ 查询中使用动态类型

起初，你可能会发现 LINQ 不支持动态类型而感到失望。LINQ 完全依赖扩展方法来执行每个表达式操作。由于编译后的程序集中缺少相关信息，扩展方法无法在运行时解析。扩展方法通过 `using` 子句将包含扩展方法的程序集添加到作用范围内来引入作用域的，这在编译时对于方法解析是可用的，但在运行时不可用——因此没有 LINQ 支持。然而，这仅意味着你不能将集合类型定义为 `dynamic`，但你可以在实例级（被查询集合中的类型）使用动态类型，你将在此示例看到。

对于此示例，我们创建了一个类型，允许以优雅的方式读取和查询逗号分隔文本文件，这在从另一个应用程序导入数据时通常有用。我所说的“优雅”是指不在我们的导入代码的字符串字面量中硬编码任何列定义，而是允许直接访问字段，就像访问传统的属性访问器一样。这种接口通常被称为流式接口（fluent interface）。考虑到列表 8-5 所示的示例 CSV 文件内容，目的是允许编码人员通过在第一行定义的相关的标头名称直接引用每行的数据列——即 `FirstName`、`LastName` 和 `State`。

# 列表 8-5 作为示例内容的逗号分隔值 (CSV) 文件内容

```
FirstName, LastName,State
Troy, Magennis, TX
Janet, Doherty, WA
```

第一行包含文件每一行的列名，这种特定的实现预期始终如此。在对这种格式的文件编写 LINQ 查询时，通过标头名称引用列中的每行值使查询变得易于理解。目标是编写列表 8-6 所示的代码，并且此代码无需为处理的每个 CSV 文件类型提供特定的基类即可通过编译。（这就像针对给定的输入标头定义对动态匿名类型进行编码。）

# 列表 8-6 流式读取 CSV 文件内容而无需特定基类的查询代码

```
var q = from dynamic line in new CsvParser(content)
where line.State == "WA"
select line;
```

动态类型允许我们根据逗号分隔的文本，，在在运行时是必要的。为了解析第一行，我们需要第二个类型来管理此过程，如列表 8-8 所示，并被称为 `CsvParser`。这是为了确定用于该行之后的代码标头，以及 ` `IEnumerable` 实现将提供每一行提供任何查询查询。

 7-7 表示动态动态类型 类

```
public class CsvLine : System.DynamicObject
{
    string[] _lineContent;
    List<string> _headers;

    public CsvLine(string line, List<string> headers)
    {
        this._lineContent = line.Split(',');
        this._headers = headers;
    }

    public override bool TryMember(
        GetMemberBinder binder,
        out object result)
    {
        result = null;

        // 找到位置并获取值
        int index = _headers.IndexOf(binder.Name);
```

# 动态类型 249

```
if (index >= 0 && index < _lineContent.Length)
{
    result = _lineContent[index];
    return true;
}

return false;
```

为了解析第一行，我们需要第二个类型来管理此过程，如列表 8-8 所示，并被称为 `CsvParser`。这是为了确定用于该行之后的代码标头，以及 `IEnumerable` 实现将提供每一行提供任何查询查询。

 248 章节 C# 4.0 特性

```cs
public class CsvParser : IEnumerable
{
    List<string> _headers;
    string[] _lines;
}
```

```cs
public CsvParser(string csvContent)
{
    _lines = csvContent.Split('\\n');

    // 捕捉标题行并记住位置
    if (_lines.Length > 0)
        _headers = _lines[0].Split(',').ToList();
}

public IEnumerator GetEnumerator()
{
    for (int i = 1; i < _lines.Length; i++)
    {
        yield return new CsvLine(_lines[i], _headers);
    }
}

IEnumerator IEnumerable.GetEnumerator()
{
    return GetEnumerator();
}
```

*(注：由于提供的原始文本在某些地方存在明显的段落重复和错乱，翻译时已根据上下文逻辑进行了对齐处理以确保通通。)*

