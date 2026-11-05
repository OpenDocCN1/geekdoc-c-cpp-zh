
以下是这段代码的输出：

```xml
<book>Programming</book>
```

## 解析属性

类型为 XmlNodeType.Attribute 的属性可以按照上面所示的方式解析。不过，更优雅的做法是：当找到 XmlNodeType.Element 类型时，可以使用 XmlTextReader.MoveToNextAttribute 遍历属性：

```csharp
case XmlNodeType.Element:

Console.Write("<" + reader.Name);
while (reader.MoveToNextAttribute())
{
Console.WriteLine(reader.Name+" = "+reader.Value);
}
break;
```

现在，如果向它输入以下 XML：

```xml
<book first="1" second="2">Programming</foo>
```

输出为：

```xml
<book first="1" second="2">Programming</book>
```

此前，属性被忽略，输出为：

```xml
<book>Programming</book>
```

注意，如果元素不包含任何属性，则循环永远不会开始。这意味着无需先检查是否存在属性。可以使用 AttributeCount 属性查找节点上的属性数量。

### 在 .NET 中编写 XML

编写 XML 由 XmlTextWriter 类完成。同样，采用只进方式，可以根据不同的节点类型构建 XML 文件，这些节点会按顺序输出。

首先，创建该类的实例：

```csharp
XmlTextWriter writer = new XmlTextWriter("FirstWrite.xml", null);
```

**第二个参数**在这里设置为 null，它允许我们指定 XML 文件中要使用的编码格式。将其设置为 null 会生成标准的 UTF-8 编码 XML 文件，且文档元素上没有 encoding 属性。

要写入元素和属性，需要使用 XmlTextWriter 中公开的方法。

考虑书的示例，
myBook.xml

<journal>

<book>

```xml
<title>C# Programming</title>

<author>Ravi Wani</author>

<chapters>

  <chapter name="Introduction to XML"/>

</chapters>

</book>

</journal>
```

第一行是元素 journal。
使用 WriteStartElement 方法将其写入 writer：

```csharp
writer.WriteStartElement("journal");
```

在写入所有 Book 元素之前，不要关闭此元素。因此，接下来要添加的节点是 writer 中的一个开始 Book 元素。

```csharp
writer.WriteStartElement("book");
```

要写入 title 元素（<title>C# Programming</title>）。

此类型与之前不同，因为它具有特定值。由于 title 元素上没有更多属性，请使用 WriteElementString 方法：

```csharp
writer.WriteElementString("title", "C# Programming");
```

```csharp
writer.WriteElementString("author", "Ravi Wani");
writer.WriteStartElement("chapters");
```

现在，元素 chapters 带有一个属性 name。

这里，**首先写入元素的开始部分**，然后写入属性，最后关闭元素。

```csharp
writer.WriteStartElement("chapter");

writer.WriteAttributeString("name", "Control Structures");

writer.WriteEndElement();
```

无需说明要关闭哪个元素，因为 writer 会自动为**最后打开的元素**写入结束标签，在本例中即 chapter。

现在以相同方式关闭剩余元素，

```csharp
writer.WriteEndElement();

writer.WriteEndElement();
```

最后，**“刷新”** writer，换句话说，将请求的信息输出到 XML 文件，然后关闭 writer 以释放文件和资源，

```
writer.Flush()
writer.Close()
```

## 17.4 使用序列化创建 XML 文件

- 1. 将 XML 序列化为公共语言运行时对象，使人能够将 XML 文档转换为更易于使用传统编程语言处理的形式。

- 2. .NET 技术是广泛支持的 XML 文件格式。.NET Framework 提供了用于读取、写入以及执行 XML 格式文件其他操作的类。

- 3. 序列化技术是指将对象转换/保存为 XML 格式或流。要在 XML 中使用**序列化**，需要 **XmlSerializer** 类。该类派生自 System.Xml.Serialization。

- 4. **序列化和反序列化**是用于**将对象序列化为 XML**，然后再**反序列化为对象**的两个最重要的方法。

- 5. 在 C# 中使用 XML 序列化和反序列化时需要记住的事项——
  - i) 在 **XML 序列化**中只能序列化公共对象。因此它也被称为**浅序列化。**
  - ii) 继承自 IEnumerable 和 ICollection 的类也可以序列化，但它只序列化集合，而不序列化公共属性。
  - iii) 私有或只读属性、方法、索引器不能使用此 XML 序列化进行序列化。

- 6. **XML 序列化**的反向过程称为 XML 反序列化。在 XML 序列化中，对象被转换为 XML 流/文件，而将该 XML 流/文件再次转换为对象称为 **XML 反序列化。C# 中的 XML 序列化和反序列化**是 .Net 中最重要的主题。

## 7. 示例

```
/* XML Serialization and Deserialization in C# */

using System;
using System.Xml.Serialization;

namespace XMLCreationTest
{
    public class XMLTest1
```

```csharp
{
    public String value1;
    public String value2;
}

class Program
{
    static void Main(string[] args)
    {
        XMLTest1 xtest = new XMLTest1() { value1 = "Value 1", value2 = "Value 2" };
        XmlSerializer xs = new XmlSerializer(xtest.GetType());
        xs.Serialize(Console.Out, xtest);
        Console.ReadKey();
    }
}
```

实际序列化由 **XmlSerializer** 类的实例完成，该类来自 System.Xml.Serialization 命名空间。序列化器的构造函数需要引用它应处理的对象类型——可以通过实例化对象的 *GetType()* 方法获取，或者调用 *typeof()* 函数并将类名指定为唯一参数来获取。

***Serialize()*** 方法接受已定义类型的对象，将该对象转换为 XML，然后将信息写入已定义的流（在本例中为控制台输出流的 TextWriter 对象）。示例代码的 XML 输出如下所示：

```xml
<?xml version="1.0" encoding="ibm850"?>
<Test xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="
             http://www.w3.org/2001/XMLSchema">
  <value1>Value 1</value1>
  <value2>Value 2</value2>
</Test>
```

XML 输出中的元素和属性名称由对象中属性和字段的名称设置。

## 8. 反序列化 XML 数据

反序列化是获取 XML 格式数据并将其转换为 .NET Framework 对象的过程：与上面所示过程相反。只要 XML 格式良好且准确匹配目标类型的结构，反序列化就是相对直接的任务。

在以下示例中，前面示例的 XML 输出被硬编码到字符串中，但它也可以从网络流或外部文件获取。**XmlSerializer** 类

用于将该字符串反序列化为 Test 类的实例，然后示例将字段打印到控制台。为了获得可传入 XmlSerializer 构造函数的合适流，声明了一个 StringReader（来自 System.IO 命名空间）。

```csharp
using System;
using System.IO;
using System.Xml.Serialization;

namespace XMLCreationTest
{
    public class XMLTest2
    {
        public String value1;
        public String value2;
    }

    class Program
    {
        static void Main(string[] args)
        {
            String xData = "<?xml version=\"1.0\" encoding=\"ibm850\"?><Test xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><value1>Value 2</value1><value2>Value 2</value2></Test>";
            XmlSerializer xs = new XmlSerializer(typeof(Test));
            XMLTest2 test = (XMLTest2)xs.Deserialize(new StringReader(xData));
            Console.WriteLine("V1: " + test.value1);
            Console.WriteLine("V2: " + test.value2);
        }
    }
}
```

## 9. 重写类的序列化

如前所述，类的所有公共属性和字段都会自动可序列化，并且通常无需使用任何指令或属性即可转换为 XML。私有属性和字段默认不会被序列化。要包含这些内容，并且更精确地控制对象如何序列化为 XML，可以重写整个序列化过程。

## 10. 使用属性控制序列化

当序列化数据以便与其他应用程序交换时，或者当遵循预定义的 XML 架构时，能够更改过程中使用的元素和属性名称是很有用的。

