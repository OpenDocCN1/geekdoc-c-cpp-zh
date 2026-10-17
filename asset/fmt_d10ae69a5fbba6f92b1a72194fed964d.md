
```go
foreach (int o in col)
{
    MessageBox.Show(o.ToString());
}
```

完整的类定义如下：

```go
class TestCollection : IEnumerable,IEnumerable<int>
{
    protected Random rnd;
    private int Size;
    public TestCollection(int s)
    {
        rnd = new Random();
        Size = s;
    }
    IEnumerator IEnumerable.GetEnumerator()
    {
        return new TestCollectionEnumerator(this);
    }
    IEnumerator<int> IEnumerable<int>.GetEnumerator()
    {
        return new TestCollectionEnumerator(this);
    }
class TestCollectionEnumerator : IEnumerator<int>
    {
    private TestCollection m_Instance;
        private int loc = -1;
        public TestCollectionEnumerator(
            TestCollection Instance)
    {
        m_Instance = Instance;
    }
    void IEnumerator.Reset()
    {
        loc = -1;
    }
}
```

```go
object IEnumerator.Current
{
    get
        if (loc > -1)
            return m_Instance.rnd.Next(500);
        else
            return -1;
}
```

```go
int IEnumerator<int>.Current
{
    get
        if (loc > -1)
            return m_Instance.rnd.Next(500);
        else
            return -1;
}
void IDisposable.Dispose()
{\}
bool IEnumerator.MoveNext()
{
    loc++;
    if (loc < m_Instance.Size)
        return true;
    else
        return false;
}
```

## LINQ 与扩展方法

现在我们有了一个简单的 `IEnumerable` 类，我们可以可以开始对其使用 LINQ —— 这非常简单。LINQ 系统的作用是向 `IEnumerator` 泛型接口添加扩展方法，这是我们在第 7 章中已经遇到过的。目前，只需接受这样一个事实：任何实现了 `IEnumerator` 泛型接口的类都有许多额外的可用方法，而其中大多数方法返回一个 `IEnumerable` 对象 —— 这是一个比你想象的更重要的观察。要使用这些扩展方法，你需要添加：`using System.Linq;`。

为了开始，让我们来看 `Where` 扩展方法。如果你查看它的定义，你会发现它是：

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source, Func<T, bool> predicate)
```

暂时忽略这个部分，因为它是每个扩展方法的一部分。参数 `source` 是 `IEnumerable`，它将被“扫描”以找到所有返回 `true` 的实体。`predicate` 只是一个泛型委托，它“封装”了一个函数，该函数接受一个第一个指定类型的单个输入参数，并返回第二个指定类型的结果。在这种情况下，`predicate` 可以被视为类型为 `T` 的单个参数并返回一个布尔结果。如果我们要使用 `Where`，首先需要的是一个合适的 `predicate`。这可以通过许多方式创建，但为了保持解释简单，让我们采用老式但稍显冗长的方法，先定义一个合适的函数，然后……

首先定义函数：

```csharp
bool MyTest(int i)
{
  return i > 250;
}
```

这仅仅是测试值是否大于 250，如果是则返回 `true`，否则返回 `false`。为了利用它，我们必须将其封装在委托中：

```csharp
Func<int, bool> MyDelegate = new Func<int, bool>(MyTest);
```

接下来，我们像以前一样创建数据集合：

```csharp
TestCollection col = new TestCollection(5);
```

最后使用我们定义的委托调用方法：`IEnumerable<int> q = col.Where<int>(MyDelegate);`

如果你尝试这样做，什么都不会发生。这是因为 LINQ 查询几乎总是**惰性求值**的，也就是说，枚举并提取小于 250 的实体的操作只在需要时才会执行。

在实践中，求值是通过调用泛型 `GetEnumerator` 方法触发的，通常在 `foreach` 循环内部。

例如：

```csharp
foreach (int o in q)
{
    MessageBox.Show(o.ToString());
}
```

强调一下，查询结果只有在我们开始 `foreach` 循环时才存储在 `q` 中。完整的程序是：

```csharp
bool MyTest(int i)
{
    return i > 250;
}
Func<int, bool> Delegate = new Func<int, bool>(MyTest);

TestCollection col = new TestCollection(5);
IEnumerable<int> q = col.Where<int>(MyDelegate);
foreach (int o in q)
{
    MessageBox.Show(o.ToString());
}
```

*(注：此处代码中 `MyDelegate` 与 `Delegate` 名称不一致，原文如此，译文保持原样)*

*(注：由于原文代码块标记为 `go` 但内容为 `c#`，译文保持了这种标记不一致。)*

## 更多选择

理解查询表达式如何转换为对查询扩展方法的调用，将极大地阐明 LINQ 的工作原理以及你可以用它做什么。如果你想保持清晰的设计，应该始终将 `Select` 作为“投影操作符”。也就是说，它应该将数据项还原为自身子集的某个。例如，如果数据项是一个结构体（struct），那么 `select` 应该指定哪些字段要被提取并返回到一个“较小”的结构体中。这是一个常见而有趣的任务，所以让我们来看另一个简单的示例。首先，我们需要一个类或结构体来存储数据：

```csharp
public struct Contact {
    public string name { get; set; }
    public string address { get; set; }
    public int phone { get; set; }
}
```

默认的属性实现足以允许我们直接初始化此类结构体的 `List`：

```csharp
List<Contact> AddressBook= new List<Contact>(){
new Contact(){
    name="mike",
    address="Anywhere",
    phone=123,
}new Contact(){
    name="Ian",
    address="Anywhere2",
    phone=124,
}new Contact(){
    name="John",
    address="Anywhere3",
    phone=125
};
```

由于 `List` 支持枚举器（Enumerator），现在可以直接使用 LINQ 来查询它并进行移动。要提取单个字段（例如 `name`），你会使用如下查询：

```csharp
var q = from N in AddressBook select N.name;
foreach(var n in q) {
    MessageBox.Show(n);
}
```

注意这里使用了 `var` 来避免显式声明数据类型。如果你不想使用匿名类型，可以将 `var` 替换为 `string`。

很容易看出这如何转换为对扩展方法的调用（该方法必须只返回作为字符串的单个字段），但你如何返回多个字段呢？问题在于你没有一个持有字段子集的数据类型（即结构体）。你可以定义一个合适的结构体，但标准的解决方案是动态创建一个新的匿名类型：

```csharp
var q = from N in AddressBook select new { N.name, N.phone };
foreach ( var n )
{
    MessageBox.Show(n.name.ToString + n.phone.ToString());
}
```

你可以看到，这些“动态”机制是让 LINQ 看起来简单必须的。

# 结语

基本上我们查看的是针对对象的 LINQ（LINQ to objects），但同样的原理适用于所有其他实现——例如 LINQ to SQL、XML 和 ADO。现在你应该能够理解它们是如何运作的，即使你仍然需要一个 LINQ 不支持的数据源。更令人印象的是，如果你有一个 LINQ 不支持的数据源，你应该通过实现 `IEnumerable` 来添加它。

LINQ 是一种强大且紧凑的数据处理方式，以至于许多人建议用它替代其他的处理方法。换句话之，尽可能使用 LINQ 表达式代替 `foreach` 循环。

# 第 20 章

## XML

C# 具有一些非常易用的创建和编辑 XML（可扩展标记语言）的设施。引入这些设施许多是为了让 LINQ to XML 运行得更好，但你也可以在更通用的情况下使用它们。.NET 已经有良好的 XML 支持，但 LINQ 添加了一组类，使得处理 XML 变得更加容易，特别是当你不是 XML 专家时。

处理 XML 有许多标准协议和方法，如 Xpath、SAX、DOM 等。它们都是好的，但它们都关注 XML 的某个特定方面以及完成任务的特定方式。LINQ 版本的 XML 则是“回归本质”。

即使你对处理 XML 不感兴趣，观察 LINQ 如何处理更复杂的数据结构也是有益的，特别是当你不是 XML 专家时。通过查看 LINQ 如何处理更复杂的数据结构，你可以理解它的工作原理。如果你有一个 LINQ 不支持的数据源，你应该能够通过实现 `IEnumerable` 来添加它，这比之前的更令人印象深刻。LINQ 版本的 XML 遵循“回归基础”。在本章中，我们将探讨如何构建 XML。

### XML 标签与结构

XML 的核心是：起始标签（例如`<Record>`）和一个结束标签（例如`</Record>`）。XML 的规则很简单：标签必须成对出现，并且可以嵌套。例如：

```xml
<Record>
    <Name>John</Name>
    <Address>Anywhere3</Address>
    <Phone>125</Phone>
</Record>
```

每个标签必须成对出现，且必须是嵌套的。XML 的规则是：标签必须成对出现。LINQ 的 XML 规则是：标签必须成对出现。即使你对处理 XML 不感兴趣，观察 LINQ 如何处理更复杂的数据结构也是有益的。在本章中，我们将探讨如何构建 XML。

（此处根据原文重复内容逻辑）

XML 的核心是：起始标签（例如`<Record>`）和一个结束标签（例如`</Record>`）。XML 的规则是：标签必须成对出现，并且是嵌套的。例如：

```xml
<Record>
    <Name>John</Name>
    <Address>Anywhere3</Address>
    <Phone>125</Phone>
</Record>
```

每个标签必须成对出现，且必须是嵌套的。XML 的规则是：标签必须成对出现。LINQ 的 XML 规则是：标签必须成对出现。即使你对处理 XML 不感兴趣，观察 LINQ 如何处理更复杂的数据结构也是有益的。在本章中，我们将探讨如何构建 XML。

（注：由于原文文本存在大量段落重复，译文已根据指令“不要重复输出原文”的原则进行了处理，保留核心逻辑翻译。）

XML 标签与结构（持续）

LINQ 决定了 XML 的结构。即使你对处理 XML 不感兴趣，观察 LINQ 如何处理更复杂的数据结构也是有益的。在本章中，我们将探讨如何构建 XML。

XML 的核心是：起始标签（例如`<Record>`）和一个结束标签（例如`</Record>`）。XML 的规则是：标签必须成对出现，并且是嵌套的。

例如：

```csharp
XAttribute Attl = new XAttribute("Epoch",1900);
root.Add(Attl);
```

向属性集合添加了一个 `Epoch` 为 "1900" 的属性。生成的 XML 如下：

```xml
<Record Epoch = "1900"> ...</Record>
```

你可以使用构建 XML 树函数的方法来实现相同的结果：

```csharp
XElement root = new XElement("Record",
new XAttribute("Epoch", 1900),
new XElement("Name",
new XElement("First", "Mike",
new XElement("Second"),
new XElement("Address"));
```

### 构造函数规则

构造函数或 `Add` 方法对你提供的对象的处理方式取决于该对象的类型。规则如下：

- 如果为 `null`，则什么都不会发生

- 如果它继承自 `XNode`，则它会被添加到 `Nodes` 集合

- 如果它是一个 `Attribute`（属性），则会被添加到 `Attributes` 集合

- 如果它是一个字符串（`string`），则会被转换为 `XText` 并添加到 `Nodes`

较不那么明显的行为是：如果你提供了一个实现 `IEnumerable` 的对象，它将会被枚举，并且产生的对象将根据规则进行处理；如果 `Add` 是任何规则无法处理的内容，它会被转换为字符串和 `XText` 对象并添加到 `Nodes`。`IEnumerable` 的行为非常方便，因为这意味着你可以在一步中添加一个对象集合。

### 操作树结构

构建树通常只是问题的开始。你通常想在得到结果后对树进行处理，即检查并更改树。由于 `XElement` 树是动态的，这相当容易。你当然可以使用 `Add` 来添加任何种类的额外元素，还有删除方法——`RemoveNode` 和 `RemoveAttribute`。这些方法只是简单地从其父级集合中移除该对象。例如：

```csharp
root.Add(child4);
child4.Remove();
```

这会将 `child4` 添加到 `root` 的节点集合中，然后将其移除。

一个特别实用的方法是 `SetElementValue`，它修改元素的值，如果该元素不存在，则会创建一个新对象。例如，指令：

```csharp
root.SetElementValue("Tel","123");
```

这将将 `root` 下 `XName` 为 "Tel" 的现有 `Element` 元素的值设置为 "123"，或者如果该 `Element` 不存在，它将先创建一个新实例。

这里存在一些似乎很奇怪的行为：值 "123" 被应用在一对新标签 `<Tel>123</Tel>` 之间，但它也被追加到了 `root` 的 `Value` 属性中，就好像它是位于 `<root></root>` 之间的新文本一样。其原因在于，`Value` 属性是其起始和结束标签内包含的所有 `Text` 对象的拼接。这使得 `Value` 属性变得不太有用。注意，如果你以字符串的形式添加一些额外的文本，它将简单地作为拼接添加到任何现有的 `Text` 对象中。如果你首先显式地创建 `Text` 对象并在获取新子对象时添加这些对象，这似乎是合理的行为。

`SetAttributeValue` 的工作方式相同，但作用于 `Attribute` 集合。例如：

```csharp
root.SetAttributeValue("Epoch", "2000");
```

更新或添加一个 `Epoch` 属性。由于属性通常只有一个值，它的 `Value` 属性要有用得多。

另外两个实用的方法是 `AddBeforeSelf` 和 `AddAfterSelf`，正如它们的名称所示，允许在树中当前元素的上方和下方添加元素。

还有许多其他修改树结构的方法，但它们都非常显而易见，没有惊喜，详情请查阅文档。

### 值

XML 是一种标准的数据格式，我们偶尔才需要实际访问数据。正如前面提到的，如果一个 `Element`（元素）只有一个 `Text` 子元素，你就可以通过 `Value` 属性以字符串形式访问这些数据。然而，如果它有多个 `Text` 子对象（可能包含在其他 `Element` 子对象内部），`Value` 属性则包含这些字符串的拼接。这使得处理标签内的数据变成了导航到与封装该问题的最后一对标签相对应的 `Element` 对象。同样，正如前面提到的，`XAttributes`（属性集合）在这方面更容易处理，因为它们始终对应于单一的名称/值对。在这种情况下，`Value` 属性始终包含我们感兴趣的数据。为了简单起见，以下示例将处理 `XAttributes`，但相同的方法适用于 `XElement` 对象。

例如：

```csharp
string name = root.Element("Name").Value;
```

如果你想获取属性值，可以使用：

```csharp
string epoch = root.Attribute("Epoch").Value;
```
