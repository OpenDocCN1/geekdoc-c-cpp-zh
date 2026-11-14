

在所有情况下，你都必须检查 Binder 对象，查看请求了哪个成员，并执行所需的任何操作。如果有返回值，你需要设置这些值（在指定的 out 参数中），并返回你的重载是否处理了该成员。

如果你打算创建一个支持动态行为的类型，使用 DynamicObject 作为基类是最简单的方法。当然，动态属性包也可以，但让我们再看一个示例，展示动态类型在什么情况下更有用。

LINQ to XML 对处理 XML 进行了一些重大改进，但仍有不足之处。请考虑下面包含太阳系一些信息的 XML 片段：

```
<Planets>
  <Planet>
    <Name>Mercury</Name>
  </Planet>
  <Planet>
    <Name>Venus</Name>
  </Planet>
  <Planet>
    <Name>Earth</Name>
    <Moons>
      <Moon>Moon</Moon>
    </Moons>
  </Planet>
  <Planet>
    <Name>Mars</Name>
    <Moons>
      <Moon>Phobos</Moon>
      <Moon>Deimos</Moon>
    </Moons>
  </Planet>
  <!-- other data elided -->
</Planets>
```

要获取第一个行星，你需要编写类似下面的代码：

```
// Create an XElement document containing
// solar system data:
var xml = createXML();

var firstPlanet = xml.Element("Planet");
```

这还不算太糟，但你深入文档越深，代码就越复杂。获取地球（第三个行星）的代码如下：

```
var earth = xml.Elements("Planet").Skip(2).First();
```

获取第三个行星的名称需要更多代码：

```
var earthName = xml.Elements("Planet").Skip(2).First().Element("Name");
```

当你获取卫星时，代码就非常冗长了：

```
var moon = xml.Elements("Planet").Skip(2).First().Elements("Moons").First().Element("Moon");
```

此外，上述代码只有在 XML 文件包含你要查找的节点时才有效。如果 XML 文件出现问题，某些节点缺失，上述代码将抛出异常。添加处理缺失节点的代码会增加大量代码，仅为了处理潜在错误。到那时，就更难辨别原始意图了。

相反，假设你有一个数据驱动的类型，可以使用元素名称在 XML 元素上提供点号表示法。查找第一个行星可以简单到：

```
// Create an XElement document containing
// solar system data:
var xml = createXML();

Console.WriteLine(xml);

dynamic dynamicXML = new DynamicXElement(xml);

// old way:

var firstPlanet = xml.Element("Planet");

Console.WriteLine(firstPlanet);

// new way:

// returns the first planet.

dynamic test2 = dynamicXML.Planet;
```

获取第三个行星只需使用索引器：

```
// gets the third planet (Earth)
dynamic test3 = dynamicXML["Planet", 2];
```

访问卫星变成了两个链式索引器：

```
dynamic earthMoon = dynamicXML["Planet", 2]["Moons", 0].Moon;
```

最后，因为它是动态的，你可以定义语义，使任何缺失的节点都返回一个空元素。这意味着以下所有内容都将返回空的动态 XElement 节点：

```
dynamic test6 = dynamicXML["Planet", 2]
    ["Moons", 3]; // Earth doesn't have 4 moons
dynamic fail = dynamicXML.NotAppearingInThisFile;
dynamic fail2 = dynamicXML.Not.Appearing.In.This.File;
```

因为缺失的元素将返回缺失的动态元素，你可以继续对其进行解引用，并且知道如果组合的 XML 导航中任何元素缺失，最终结果将是一个缺失的元素。构建这个是另一个派生自 DynamicObject 的类。你必须重写 TryGetMember 和 TryGetIndex，以返回带有相应节点的动态元素。

```
public class DynamicXElement : DynamicObject
{
    private readonly XElement xmlSource;

    public DynamicXElement(XElement source)
    {
        xmlSource = source;
    }

    public override bool TryGetMember(GetMemberBinder binder,
        out object result)
    {
        result = new DynamicXElement(null);
        if (binder.Name == "Value")
        {
            result = (xmlSource != null) ?
                xmlSource.Value : "";
            return true;
        }

        if (xmlSource != null)
            result = new DynamicXElement(
                xmlSource.Element(XName.Get(binder.Name)));
        return true;
    }

    public override bool TryGetIndex(GetIndexBinder binder,
        object[] indexes, out object result)
    {
        result = null;
        // This only supports [string, int] indexers
        if (indexes.Length != 2)
            return false;
        if (!(indexes[0] is string))
            return false;
        if (!(indexes[1] is int))
            return false;

        var allNodes = xmlSource.Elements(indexes[0].ToString());
        int index = (int)indexes[1];
        if (index < allNodes.Count())
            result = new DynamicXElement(allNodes.ElementAt(index));
        else
            result = new DynamicXElement(null);
        return true;
    }

    public override string ToString()
    {
        if (xmlSource != null)
            return xmlSource.ToString();
        else
            return string.Empty;
    }
}
```

大部分代码使用了你在本节前面看到的代码中类似的概念。TryGetIndex 方法是新的。它必须在客户端代码调用索引器以检索 XElement 时实现动态行为。

使用 DynamicObject 可以更轻松地实现具有动态行为的类型。DynamicObject 隐藏了创建动态类型的大部分复杂性。它包含大量实现，用于为你处理动态分派。此外，有时你想要创建动态类型，但无法使用 DynamicObject，因为你需要不同的基类。出于这个原因，我将向你展示如何通过自己实现 IDynamicMetaObjectProvider 来创建动态字典，而不是依赖 DynamicObject 来完成繁重的工作。

```
class DynamicDictionary2 : IDynamicMetaObjectProvider
{
    #region IDynamicMetaObjectProvider Members
    DynamicMetaObject IDynamicMetaObjectProvider.GetMetaObject(
        System.Linq.Expressions.Expression parameter)
    {
        return new DynamicDictionaryMetaObject(parameter,
            this);
    }
    #endregion

    private Dictionary<string, object> storage = new Dictionary<string, object>();

    public object SetDictionaryEntry(string key, object value)
    {
        if (storage.ContainsKey(key))
            storage[key] = value;
        else
            storage.Add(key, value);
        return value;
    }

    public object GetDictionaryEntry(string key)
    {
        object result = null;
        if (storage.ContainsKey(key))
        {
            result = storage[key];
        }
        return result;
    }

    public override string ToString()
    {
        StringWriter message = new StringWriter();
        foreach (var item in storage)
            message.WriteLine("{0}:{1}", item.Key, item.Value);
        return message.ToString();
    }
}
```

每次调用 GetMetaObject() 时，它都会返回一个新的 DynamicDictionaryMetaObject。复杂性就在这里开始。每次调用 DynamicDictionary 的任何成员时，都会调用 GetMetaObject()。如果你调用同一个成员十次，GetMetaObject() 就会被调用十次。即使 DynamicDictionary2 中的方法是静态定义的，GetMetaObject() 也会被调用，并可以拦截这些方法以调用可能的动态行为。请记住，动态对象被静态类型化为 dynamic，因此没有定义编译时行为。每个成员访问都会动态分派。

DynamicMetaObject 负责构建表达式树，以执行处理动态调用所需的任何代码。其构造函数将表达式和动态对象作为参数。构造完成后，将调用其中一个 Bind 方法。其职责是构建一个包含执行动态调用所需表达式的 DynamicMetaObject。让我们逐一介绍实现 DynamicDictionary 所需的两个 Bind 方法：BindSetMember 和 BindGetMember。

BindSetMember 构建一个表达式树，该树将调用 DynamicDictionary2.SetDictionaryEntry() 以在字典中设置值。以下是其实现：

