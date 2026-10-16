
在这段代码中，声明了一个名为 toys 的变量。我们将其转换为 SelectListItem 类型，以便将从 LINQ 查询中得到的结果行保存下来。我们使用了两个方法，名为 Where 和 Select，用于查找与我们的特定查询相匹配的目标。代码行 ‘toy => toy.Tag == curTag.ID’ 会根据传入的标签选择一个玩具，而代码行 ‘toy => new SelectListItem {Value = toy.Name, Text = toy.ID’ 会根据传入的 ID 和名称来选择玩具。结果——即与指定条件匹配的玩具——被保存到名为 toys 的变量中。

现在，我们将注意力转向 LINQ 与 XML 数据的交互方式。XML 是 Extensible Markup Language（可扩展标记语言）的缩写，是互联网上使用最广泛的语言之一。但它远不止是一组基于文本的静态标签。XML 有时也被称为自定义数据或自描述数据。它的标签用法既可以高度定制，又是标准化的；它在全球范围内被广泛用于共享数据、访问数据和操作数据。我们现在要研究的是如何使用 LINQ 检索 XML 数据、删除数据，以及如何插入和更新数据。

## 检索和删除 XML 数据

每个 XML 数据文件都有一个父标签或根标签（也称为元素），它既封装和定义其子记录的类型，也为它们定义属性。由此产生的子记录或元素中包含真实的数据，可以根据需要对这些数据进行操作。请看下面的示例代码；这就是我们在本节剩余部分中用于 LINQ 查询的 XML 代码：

```
<?xml version='1.0' encoding='utf-8'?>
<Toys>
  <Toy ID='1'>
    <Name>Millie</Name>
    <Price>$0.45</Price>
  </Toy>
  <Toy ID='2'>
<Name>Dove</Name>
<Price>$0.40</Price>
</Toy>
<Toy ID='3'>
  <Name>Rook</Name>
  <Price>$0.55</Price>
</Toy>
</Toys>
```

在此示例中，根元素是 ‘Toys’，它包含几个子元素，每个子元素都是一个 ‘Toy’，并且每个 ‘Toy’ 都有自己名为 ID 的属性，以及两个名为 Price 和 Name 的内部元素。

我们要做的是检索这些子玩具，为此我们使用一个 LINQ 查询，如下所示：

```
private string file = 'SampleData.xml';
```

```
private void GetData()
{
  try
  {
    XDocument doc = XDocument.Load(file);
    var comingToys = from toy in doc.Descendants("Toy")
    select new
    {
      ID= Convert.ToInt32(toy.Attribute("ID").Value),
      Name = toy.Element("Name").Value ,
      Price = toy.Element("Price").Value
    };

    foreach (var x in comingToys)
```

```
```csharp
{
    Console.Write("Toy ID " + x.ID + " ");
    Console.Write("Toy Name " + x.Name + " ");
    Console.WriteLine("Toy Price " + x.Price+ " ");
}

}
catch (Exception err)
{
    Console.WriteLine(err.Message);
}

}
```
```

代码的第一行指向 SampleData.xml，即 XML 示例数据文件。在函数中，我们使用名为 Load() 的函数来加载 xml 文件，加载完成后，使用名为 Doc.Descendants() 的函数检索子 ‘toy’ 元素。之后，选择每个 ‘toy’ 子元素，并检索 ID 以及两个内部元素。这些数据随后被传递给 comingToys，这是一个动态变量。最后，使用 foreach 循环来显示我们检索到的数据。

输出如下：

Toy ID 1 Toy Name Millie Toy Price $0.45

Toy ID 1 Toy Name Dove Toy Price $0.40

Toy ID 1 Toy Name Rook Toy Price $0.55

与此大同小异，如果我们想从 XML 文件中移除某个子元素，可以采用如下方式：

```
```csharp
private string file = 'SampleData.xml';

private void DeleteData (int id)

{

    try
```

```
{
    XDocument sampleXML = XDocument.Load(file);
    IEnumerable<XElement> cToy =
    sampleXML.Descendants("Toy").Where(c => (int)c.Attribute("ID") ==
    id);
    cToy.First().Remove();
    sampleXML.Save(file);
}
    catch (Exception e)
    {
    Console.WriteLine(e.Message);
    }
}
```

加载目标文件后，上述代码将遍历子 ‘toys’ 元素，以找到与我们传入的玩具 ID 相匹配的元素。找到之后，使用名为 Remove() 的函数移除匹配项，并保存文件。

## 插入和更新 XML 数据

向 XML 文件添加数据所采用的途径也与此没有太大区别。实质上，我们真正需要的只是一个 XElement 类型的对象，其签名与目标文件中已经存在的元素相匹配。然后，通过使用 XDocument 类型的对象，将该对象插入数据文件：

```
private string file = 'SampleData.xml';
```

```
private static void InsertData(string name, string price)
{
    try
    {
    XDocument doc = XDocument.Load(file);
    XElement newToy = new XElement("Toy", new
    XElement("Name", name), new XElement("Price", price));
    var lastToy = doc.Descendants("Toy").Last();
```

```
int newID = Convert.ToInt32 (lastToy.Attribute ("ID").Value);
newToy.SetAttributeValue("ID",++newID);
doc.Element ("Toys").Add (newToy);
doc.Save (file);
}
catch (Exception err)
{
Console.WriteLine(err.Message);
}
}
```

创建了 XDocument 类型的对象之后，我们还创建了一个 XElement 类型的对象，其签名与已经存在的 Toy 元素相匹配。这是通过代码行 XElement newToy = new XElement('Toy', new XElement('Name', name), new XElement('Price', price))'' 完成的。然后，我们使用名为 doc.Descendants('Toy').Last() 的函数，从名为 lastToy 的变量中获取最后一个玩具元素。

当我们获得该元素后，使用代码行 newToy.SetAttributeValue('ID',++newID)"，在将属性设置到新元素的同时，检索 ID 的值并对其递增。最后，使用名为 Add() 的函数插入玩具对象，并保存对文件的更改。

在我们的示例文件中，现在又多了一个子元素。例如，如果我们向上述函数传入名称 ‘John ’ 和价格 $0.1，那么结果将如下所示：

```
<Toy ID='4'>
  <Name>Hare</Name>
  <Price>$0.65</Price>
</Toy>
```

要更改已经存在的 XML 数据或元素，我们首先需要根据某些条件（即带有我们想要更改的数据值）找到目标元素，这正是代码行 XElement cToy = doc.Descendants('Toy') 所做的工作。在这一行中，(c=>c.Attribute('ID').Value.Equals(id)" 通过查找与我们提供的 ID 相匹配的元素来实现这一点，并让 XElement 对象 cToy 指向该元素。一旦我们获得了对该元素的引用，就可以使用 cToy.Element('Price').Value = price 更新其内部元素的值。最后，保存包含所有更改的 XML 文档。

```
private string file = 'SampleData.xml';
private static void UpdateData(string name, string price, int id)
{
    try
    {
    XDocument doc = XDocument.Load(file);
    IEnumerable<XElement> cToy =
    doc.Descendants("Toy").Where (c=>(int)c.Attribute("ID") == id);
    cToy.First().Element("Name").Value = name;
    cToy.First().Element("Price").Value = price;
    doc.Save(file);
    }
    catch (Exception err)
    {
    Console.WriteLine(err.Message);
    }
}
```

现在，假设我们向上述函数再传入三个值作为参数——id=1、name=Alligator 和 price=$0.75。一旦上述函数执行完毕，XML 数据文件将不再显示 id=1 处名为 Millie 的玩具，取而代之的是 name=Alligator：

```
<Toy ID='1'>
  <Name>Alligator</Name>
  <Price>$0.75</Price>
```

</Toy>

接下来，我们继续学习 PLINQ 和并行类。

## 并行类和 PLINQ

PLINQ（即 Parallel LINQ，并行 LINQ）不过是 LINQ 模式的一种并行实现。PLINQ 查询与标准的 LINQ to Objects 查询非常相似。与标准 LINQ 查询一样，PLINQ 查询可以操作任何内存中的 IEnumerable 或 IEnumerable\<T\> 数据源。它们的执行是延迟的，这意味着在指定的查询被枚举之前，执行不会开始。

主要区别在于，PLINQ 会尽量利用系统上的每一个处理器，其做法是将每个数据源划分为多个段；然后，数据查询在多个处理器上以独立的工作线程并行地对每个段执行。在某些情况下，使用 PLINQ 可以确保查询速度大幅提升。

通过并行执行，对于某些查询类型，PLINQ 可以与旧代码相比带来显著的性能改进，而这通常只需向数据源添加一个名为 AsParallel 的查询即可实现。然而，对于某些查询类型，使用并行只会拖慢它们的速度，因此理解 PLINQ 非常重要。

我们将使用 Lambda 表达式来定义委托，并且会介绍 PLINQ 类，以及 PLINQ 查询是如何创建的。你不会看到对一切内容的深入剖析，更多的是带有示例的概述。

### ParallelEnumerable 类

PLINQ 的大部分功能都在名为 System.Linq.ParallelEnumerable 的类中公开。该类以及 System.Linq 的其他命名空间类型都被编译到名为 System.Core.dll 的程序集中，Visual Studio（C# 和 Visual Basic）中的默认项目都会引用该程序集，并导入相应的命名空间。

使用 ParallelEnumerable，你可以获得 LINQ to Objects 支持的每一个标准查询运算符的实现，但
