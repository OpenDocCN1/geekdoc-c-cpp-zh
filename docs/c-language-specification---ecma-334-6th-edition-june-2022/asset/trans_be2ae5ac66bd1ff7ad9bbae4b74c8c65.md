
```
```
: '/*' Delimited_Comment_Section* ASTERISK+ '/*'
;
```
```

在 *单行文档注释* 中，如果在与当前 *单行文档注释* 相邻的每个 *单行文档注释* 上，`///` 字符之后存在一个 *空白* 字符，则该 *空白* 字符不包含在 XML 输出中。

在 *分隔文档注释* 中，如果第二行的第一个非 *空白* 字符是 *星号*，并且可选的 *空白* 字符和一个 *星号* 字符的相同模式在 *分隔文档注释* 内的每一行的开头重复出现，则重复模式的字符不包含在 XML 输出中。该模式可以在 *星号* 字符之后以及之前包含 *空白* 字符。

### 示例

```
```csharp
/// <summary>
/// Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
    /// <summary>
    /// Method <c>Draw</c> renders the point.
    /// </summary>
    void Draw() {...}
}
```
```

文档注释中的文本必须根据 XML 的规则良好形成。([http://www.w3.org/TR/REC-xml](http://www.w3.org/TR/REC-xml))。如果 XML 格式错误，将生成警告，并且文档文件将包含一条注释，说明已遇到错误。

虽然开发人员可以自由创建自己的标签集，但在 §D.3 中定义了一组推荐标签。某些推荐标签具有特殊含义：

- The `<param>` tag is used to describe parameters. If such a tag is used, the documentation generator must verify that the specified parameter exists and that all parameters are described in documentation comments. If such verification fails, the documentation generator issues a warning.
- The `cref` attribute can be attached to any tag to provide a reference to a code element. The documentation generator must verify that this code element exists. If the verification fails, the documentation generator issues a warning. When looking for a name described in a `cref` attribute, the documentation generator must respect namespace visibility according to using statements appearing within the source code. For code elements that are generic, the normal generic syntax (e.g., `"List<T>"`) cannot be used because it produces invalid XML. Braces can be used instead of brackets (e.g., `"List{T}"`), or the XML escape syntax can be used (e.g., `"List&lt;T&gt;"`).
- The `<summary>` tag is intended to be used by a documentation viewer to display additional information about a type or member.
- The `<include>` tag includes information from an external XML file.

请注意，文档文件并未提供有关类型和成员的完整信息（例如，它不包含任何类型信息）。要获取有关类型或成员的此类信息，必须将文档文件与对类型或成员的反射结合使用。

## D.3 推荐标签

### D.3.1 通用

文档生成器必须接受并处理根据 XML 规则有效的任何标签。
以下标签在用户文档中提供常用功能。（当然，其他标签也是可能的。）

| Tag | Reference | Purpose |
|---|---|---|
| `<c>` | §D.3.2 | 将文本设置为类似代码的字体 |
| `<code>` | §D.3.3 | 设置一行或多行源代码或程序输出 |
| `<example>` | §D.3.4 | 表示一个示例 |
| `<exception>` | §D.3.5 | 标识方法可能抛出的异常 |
| `<list>` | §D.3.6 | 创建列表或表格 |
| `<include>` | §D.3.6 | 从外部文件包含 XML |
| `<para>` | §D.3.8 | 允许向文本添加结构 |
| `<param>` | §D.3.9 | 描述方法或构造函数的参数 |
| `<paramref>` | §D.3.10 | 标识某个词是参数名 |
| `<permission>` | §D.3.11 | 记录成员的安全可访问性 |
| `<remarks>` | §D.3.12 | 描述有关类型的附加信息 |
| `<returns>` | §D.3.13 | 描述方法的返回值 |
| `<see>` | §D.3.14 | 指定链接 |
| `<seealso>` | §D.3.15 | 生成“另请参阅”条目 |
| `<summary>` | §D.3.16 | 描述类型或类型的成员 |
| `<typeparam>` | §D.3.17 | 描述泛型类型或方法的类型参数 |
| `<typeparamref>` | §D.3.18 | 标识某个词是类型参数名 |
| `<value>` | §D.3.17 | 描述属性 |

### D.3.2 <c>

该标签提供了一种机制来指示描述中的文本片段应设置为特殊字体，例如用于代码块的字体。对于实际代码的行，请使用 <code> (§D.3.3)。

语法：

```
<c>text</c>
```

### 示例

```
/// <summary>
/// Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
    // ...
}
```

### D.3.3 <code>

该标签用于将一行或多行源代码或程序输出设置为某种特殊字体。对于叙述中的小型代码片段，请使用 <c> (§D.3.2)。

语法：

```
<code>source code or program output</code>
```

### 示例

```
// <summary>
// This method changes the point's location by the given x- and y-offsets.
// <example>
// For example:
// <code>
// Point p = new Point(3,5);
// p.Translate(-1,3);
// </code>
// results in <c>p</c>'s having the value (2,8).
// </example>
// </summary>
public void Translate(int dx, int dy)
{
    X += dx;
    Y += dy;
}
```

### D.3.4 <example>

该标签允许在注释中包含示例代码，以指定方法或其他库成员可能如何使用。通常，这也将涉及使用 <code> (§D.3.3) 标签。

语法：

```
<example>description</example>
```

### 示例

请参阅 <code> (§D.3.3) 以获取示例。

### D.3.5 <exception>

该标签提供了一种记录方法可能抛出的异常的方法。

语法：

```
<exception cref="member">description</exception>
```

其中

- cref="member" 是成员的名称。文档生成器检查给定成员是否存在，并将 member 翻译为文档文件中的规范元素名称。
- description 是描述引发异常的情况的描述。

### 示例

```
public class DataBaseOperations
{
    // <exception cref="MasterFileFormatCorruptException">
```
```
/// Thrown when the master file is corrupted.
/// </exception>
/// <exception cref="MasterFileLockedOpenException">
/// Thrown when the master file is already open.
/// </exception>
public static void ReadRecord(int flag)
{
    if (flag == 1)
    {
        throw new MasterFileFormatCorruptException();
    }
    else if (flag == 2)
    {
        throw new MasterFileLockedOpenException();
    }
    // ...
}
```

### D.3.6 <include>

该标签允许包含来自源代码文件外部的 XML 文档的信息。外部文件必须是格式良好的 XML 文档，并且会将 XPath 表达式应用于该文档以指定要包含的 XML。随后 <include> 标签将被外部文档中选定的 XML 替换。

语法：

```
<include file="filename" path="xpath" />
```

其中

- file="filename" 是外部 XML 文件的文件名。文件名是相对于包含 include 标签的文件解释的。
- path="xpath" 是选择外部 XML 文件中部分 XML 的 XPath 表达式。

### 示例

如果源代码包含如下声明：

```
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

并且外部文件 "docs.xml" 具有以下内容：

```
<?xml version="1.0"?>
<extradoc>
    <class name="IntList">
        <summary>
            Contains a list of integers.
        </summary>
    </class>
    <class name="StringList">
        <summary>
            Contains a list of strings.
        </summary>
    </class>
</extradoc>
```

那么输出的文档与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### D.3.7 <list>

该标签用于创建项目列表或表格。它可以包含 <listheader> 块来定义表格或定义列表的标题行。（在定义表格时，只需提供标题中的 term 条目。）

列表中的每个项目都用 <item> 块指定。在创建定义列表时，必须同时指定 term 和 description。但是，对于表格、项目符号列表或编号列表，只需指定 description。

### 语法

```
<list type="bullet" | "number" | "table">
  <listheader>
    <term>term</term>
    <description>description</description>
  </listheader>
  <item>
    <term>term</term>
    <description>description</description>
  </item>
  ...
  <item>
    <term>term</term>
    <description>description</description>
  </item>
</list>
```

其中

- term 是要定义的术语，其定义在 description 中。
- description 是项目符号或编号列表中的一个项目，或术语的定义。

### 示例

```
public class MyClass
{
    /// <summary>Here is an example of a bulleted list:
    /// <list type="bullet">
    /// <item>
    /// <description>Item 1.</description>
    /// </item>
    /// <item>
    /// <description>Item 2.</description>
    /// </item>
    /// </list>
    /// </summary>
    public static void Main()
    {
        // ...
    }
```
