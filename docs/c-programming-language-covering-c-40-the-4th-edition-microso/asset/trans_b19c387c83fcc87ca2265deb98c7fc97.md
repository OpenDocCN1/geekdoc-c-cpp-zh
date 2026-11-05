
## A.2.7 <para>

此标签用于其他标签内部，例如 <summary>（§A.2.11）或 <returns>（§A.2.12），并允许向文本中添加结构。

语法：

```
<para>content</para>
```

其中

content

段落的文本。

示例：

```
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any nontrivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

## A.2.8 <param>

此标签用于描述方法、构造函数或索引器的参数。

语法：

```
<param name="name">description</param>
```

## A.2.9 <paramref>

此标签用于指示某个词是参数。可以处理文档文件，以某种独特方式格式化此参数。

语法：

```
<paramref name="name"/>
```

其中

name

参数的名称。

示例：

```
/// <summary>This constructor initializes the new point to
/// <paramref name="xor"></paramref>,<paramref name="yor"></paramref>.</summary>
/// <param name="xor">the new point's x-coordinate.</param>
/// <param name="yor">the new point's y-coordinate.</param>
public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## A.2.10 <permission>

此标签允许记录成员的安全可访问性。

语法：

```
<permission cref="member">description</permission>
```

其中

cref="member"

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 转换为文档文件中的规范元素名称。

description

对成员访问权限的描述。

示例：

```
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>
public static void Test() {
    // ...
}
```

## A.2.11 <remark>

此标签用于指定有关类型的额外信息。（使用 <summary>（§A.2.15）描述类型本身以及类型的成员。）

语法：

```
<remark>description</remark>
```

其中

*描述*

备注的文本。

示例：

```
/// <summary>Class <c>Point</c> models a point in a
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point
{
    // ...
}
```

## A.2.12 <returns>

此标签用于描述方法的返回值。

语法：

```
<returns>description</returns>
```

其中

*描述*

返回值的描述。

示例：

```
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
///  without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

## A.2.13 <see>

此标签允许在文本中指定链接。使用 <seealso>（§A.2.14）指示要出现在“另请参阅”部分中的文本。

语法：

```
<see cref="member"/>
```

其中

```
cref="member"
```

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 更改为生成的文档文件中的元素名称。

示例：

```
/// <summary>This method changes the point's location to
/// the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

## A.2.14 <seealso>

此标签允许为“另请参阅”部分生成一个条目。使用 <see>（§A.2.13）指定文本中的链接。

语法：

```
<seealso cref="member"/>
```

其中

```
cref="member"
```

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 更改为生成的文档文件中的元素名称。

示例：

```
// <summary>This method determines whether two points have the same
// location.</summary>
// <seealso cref="operator==" />
// <seealso cref="operator!=" />
public override bool Equals(object o) {
    // ...
}
```

## A.2.15 <summary>

此标签可用于描述类型或类型的成员。使用 <remark>（§A.2.11）描述类型本身。

语法：

```
<summary>description</summary>
```

其中

description

类型或成员的摘要。

示例：

```
// <summary>This constructor initializes the new point to (0,0).</summary>
public Point() : this(0,0) {
}
```

## A.2.16 <value>

此标签允许描述属性。

语法：

```
<value>property description</value>
```

其中

property description

属性的描述。

示例：

```
// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

## A.2.17 <typeparam>

此标签用于描述类、结构、接口、委托或方法的泛型类型参数。

语法：

```
<typeparam name="name">description</typeparam>
```

其中

name

类型参数的名称。

description

类型参数的描述。

示例：

```
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
  ...
}
```

## A.2.18 <typeparamref>

此标签用于指示某个词是类型参数。可以处理文档文件，以某种独特方式格式化此类型参数。

语法：

```
<typeparamref name="name"/>
```

其中

name

类型参数的名称。

示例：

```
/// <summary>This method fetches data and returns a
///   list of <typeparamref name="T" />.</summary>
/// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
  ...
}
```

## A.3 处理文档文件

文档生成器会为源代码中带有文档注释标记的每个元素生成一个 ID 字符串。此 ID 字符串唯一标识一个源元素。文档查看器可以使用 ID 字符串来标识文档所适用的对应元数据或反射项。

文档文件不是源代码的层次化表示；相反，它是一个扁平列表，每个元素都有一个生成的 ID 字符串。

### A.3.1 ID 字符串格式

文档生成器在生成 ID 字符串时遵循以下规则：

- 字符串中不放置空白字符。
- 字符串的第一部分通过一个后跟冒号的单个字符来标识所记录的成员种类。下表列出了已定义的成员种类。

| 字符 | 说明 |
|---|---|
| E | 事件 |
| F | 字段 |
| M | 方法（包括构造函数、析构函数和运算符） |
| N | 命名空间 |
| P | 属性（包括索引器） |
| T | 类型（例如类、委托、枚举、接口和结构） |
| ! | 错误字符串；字符串的其余部分提供有关该错误的信息。例如，文档生成器会为无法解析的链接生成错误信息。 |

- 字符串的第二部分是元素的完全限定名，从命名空间的根开始。元素名称、其封闭类型和命名空间用句点分隔。如果项本身的名称包含句点，则这些句点会被替换为 #（U+0023）字符。（假定没有元素的名称包含此字符。）

对于带参数的方法和属性，后面是参数列表，并括在圆括号中。对于没有参数的成员，省略圆括号。参数之间用逗号分隔。每个参数的编码与 CLI 签名相同，如下所示：

参数由其文档名称表示，该名称基于其完全限定名，并按如下方式修改：

- 表示泛型类型的参数会追加一个 &#96; 字符，后跟类型参数的数量。
- 具有 out 或 ref 修饰符的参数在其类型名后有一个 @。按值传递或通过 params 传递的参数没有特殊表示法。
- 数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量为秩减 1，每个维度的下界和大小（如果已知）用十进制表示。如果未指定下界或大小，则省略它。如果省略某个特定维度的下界和大小，则“:”也一并省略。交错数组每层用一个“[]”表示。
- 具有非 void 指针类型的参数使用类型名后的 * 表示。void 指针使用类型名 System.Void 表示。
- 引用在类型上定义的泛型类型参数的参数使用 &#96; 字符后跟该类型参数的从零开始的索引进行编码。
- 使用在方法中定义的泛型类型参数的参数使用双反引号 &#96;&#96;，而不是类型所用的 &#96;。
- 引用构造泛型类型的参数使用泛型类型编码，后跟“{”，再后跟以逗号分隔的类型参数列表，再后跟“}”。

### A.3.2 ID 字符串示例

以下每个示例展示一段 C# 代码片段，以及从每个能够带有文档注释的源元素生成的 ID 字符串：

类型使用其完全限定名表示，并补充泛型信息：

```
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess {...}
    struct ValueType {...}
```

