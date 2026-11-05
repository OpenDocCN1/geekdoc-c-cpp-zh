
在单行文档注释中，如果与当前单行文档注释相邻的每个单行文档注释中，`///` 字符后有一个空白字符，则该空白字符不包含在 XML 输出中。

在分隔文档注释中，如果第二行第一个非空白字符是星号，并且相同的“可选空白字符加星号字符”模式在分隔文档注释内每一行的开头重复出现，则该重复模式的字符不包含在 XML 输出中。该模式可以在星号字符前后都包含空白字符。

## 示例：

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
///
public class Point
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

文档注释内的文本必须根据 XML 规则（http://www.w3.org/TR/REC-xml）格式良好。如果 XML 格式不良，则会生成警告，并且文档文件将包含一条注释，说明遇到了错误。

尽管开发者可以自由创建自己的标签集，但 §A.2 中定义了一组建议标签。部分建议标签具有特殊含义：

- `<param>` 标签用于描述参数。如果使用此类标签，文档生成器必须验证指定的参数存在，并且所有参数都在文档注释中描述。如果此类验证失败，文档生成器将发出警告。
- `cref` 特性可以附加到任何标签，以提供对代码元素的引用。文档生成器必须验证该代码元素存在。如果验证失败，文档生成器将发出警告。在查找 `cref` 特性中描述的名称时，文档生成器必须根据源代码中出现的 `using` 语句遵守命名空间可见性。对于泛型代码元素，不能使用常规泛型语法（即 “List<T>”），因为它会产生无效的 XML。可以使用花括号代替尖括号（即 “List{T}”），也可以使用 XML 转义语法（即 “List&lt;T&gt;”）。
- `<summary>` 标签旨在由文档查看器用来显示关于类型或成员的附加信息。
- `<include>` 标签包含来自外部 XML 文件的信息。

请注意，文档文件不提供关于类型和成员的完整信息（例如，它不包含任何类型信息）。要获取关于类型或成员的此类信息，必须将文档文件与对实际类型或成员的反射结合使用。

## A.2 建议标签

文档生成器必须接受并处理任何根据 XML 规则有效的标签。以下标签在用户文档中提供常用功能。（当然，其他标签也是可能的。）

| 标签 | 节 | 用途 |
|---|---|---|
| `<c>` | A.2.1 | 将文本设置为类似代码的字体 |
| `<code>` | A.2.2 | 设置一行或多行源代码或程序输出 |
| `<example>` | A.2.3 | 指示示例 |
| `<exception>` | A.2.4 | 标识方法可抛出的异常 |
| `<include>` | A.2.5 | 包含来自外部文件的 XML |
| `<list>` | A.2.6 | 创建列表或表格 |
| `<para>` | A.2.7 | 允许向文本添加结构 |
| `<param>` | A.2.8 | 描述方法或构造函数的参数 |
| `<paramref>` | A.2.9 | 标识某个词是参数名 |
| `<permission>` | A.2.10 | 记录成员的安全可访问性 |
| `<remark>` | A.2.11 | 描述关于类型的附加信息 |
| `<returns>` | A.2.12 | 描述方法的返回值 |
| `<see>` | A.2.13 | 指定链接 |
| `<seealso>` | A.2.14 | 生成“另请参见”条目 |
| `<summary>` | A.2.15 | 描述类型或类型的成员 |
| `<value>` | A.2.16 | 描述属性 |

| 标签 | 节 | 用途 |
|---|---|---|
| `<typeparam>` | A.2.17 | 描述泛型类型参数 |
| `<typeparamref>` | A.2.18 | 标识某个词是类型参数名 |

### A.2.1 `<c>`

此标签提供一种机制，用于指示描述中的文本片段应使用特殊字体（例如用于代码块的字体）设置。对于实际代码行，请使用 `<code>`（§A.2.2）。

### 语法：

```
`<c>text</c>`
```

### 示例：

```
// <summary>Class <c>Point</c> models a point in a two-dimensional
// plane.</summary>
public class Point
{
    // ...
}
```

### A.2.2 `<code>`

此标签用于以某种特殊字体设置一行或多行源代码或程序输出。对于叙述中的小型代码片段，请使用 `<c>`（§A.2.1）。

### 语法：

```
`<code>source code or program output</code>`
```

### 示例：

```
// <summary>This method changes the point's location by
// the given x- and y-offsets.
// <example>For example:
// <code>
// Point p = new Point(3,5);
// p.Translate(-1,3);
// </code>
// results in <c>p</c>'s having the value (2,8).
// </example>
// </summary>

public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### A.2.3 `<example>`

此标签允许注释中的示例代码指定方法或其他库成员可以如何使用。通常，这也会涉及使用 `<code>` 标签（§A.2.2）。

### 语法：

```
<example>description</example>
```

### 示例：

有关示例，请参见 `<code>`（§A.2.2）。

### A.2.4 `<exception>`

此标签提供一种记录方法可抛出异常的方法。

### 语法：

```
<exception cref="member">description</exception>
```

其中

```
cref="member"
```

成员的名称。文档生成器检查给定成员是否存在，并将 `member` 转换为文档文件中的规范元素名称。

description
异常抛出情况的描述。

### 示例：

```
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        // _
    }
}
```

### A.2.5 `<include>`

此标签允许包含来自源代码文件外部 XML 文档的信息。外部文件必须是格式良好的 XML 文档，并且对该文档应用 XPath 表达式，以指定要包含该文档中的哪些 XML。然后，`<include>` 标签会被来自外部文档的选定 XML 替换。

### 语法：

```
<include file="filename" path="xpath" />
```

其中

```
file="filename"
```

外部 XML 文件的文件名。该文件名相对于包含 `include` 标签的文件进行解释。

```
path="xpath"
```

一个 XPath 表达式，用于选择外部 XML 文件中的部分 XML。

### 示例：

如果源代码包含如下声明：

```
// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class Intlist { ... }
```

并且外部文件 “docs.xml” 具有以下内容：

```
<?xml version="1.0" ?>
<extradoc>
<class name="IntList">
<summary>
Contains a list of integers.
</summary>
</class>
<class name="StringList">
<summary>
Contains a list of integers.
</summary>
</class>
</extradoc>
```

那么输出的文档将与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class Intlist { ... }
```

### A.2.6 `<list>`

此标签用于创建项列表或表格。它可以包含一个 `<listheader>` 块，用于定义表格或定义列表的标题行。（定义表格时，只需提供标题中 `term` 的条目。）

列表中的每一项都用 `<item>` 块指定。创建定义列表时，必须同时指定 `term` 和 *description*。然而，对于表格、项目符号列表或编号列表，只需指定 *description*。

### 语法：

```xml
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

- term
  要定义的术语，其定义在 *description* 中。
- description
  项目符号列表或编号列表中的项，或者 *term* 的定义。

### 示例：

```java
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
    public static void Main () {
        // ...
    }
}
```
