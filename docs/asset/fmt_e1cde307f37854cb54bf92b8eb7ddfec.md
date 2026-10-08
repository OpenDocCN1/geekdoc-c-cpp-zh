
```csharp
public override string ToString()
{
    return name + ", " + position;
}
}
}
```

项目已翻译。

# 解析

该类非常简单，没什么好解释的，该类被定义为为`Serializable`（可序列化的）：

```csharp
[Serializable]
public class Person
{
```

并且 `Person` 类型的对象可以被序列化是一个必要的前提条件。

## C# 1 编程入门与 C# 语言

# 注释

类库不是一个程序，因此它是你可以立即尝试的，但它是可以在其他应用程序中使用的 `dll`。你应该做的操作将在下一个示例中解释。类库可以包含更多内容，但通常包含用户定义的类。目标是创建一个包含你经常需要的、且已完成、测试且无错误的类的 `dll`。该 `dll` 就可以提供给其他程序使用，其类的方式与 `.NET` 框架中的所有其他类相同。

# 考试61

二进制序列化

你应该编写一个程序，创建一个 `Person` 对象并将其序列化到文件中。

# 如何操作

开头如往常是一个控制台应用程序项目。这次我将开始将上述 `dll` 关联到项目中。在“解决方案管理器”`Solution Explorer`中，你可以右键点击“引用”`References`并选择“添加引用...”`Add Reference...`。

![](img/f84352ec481fd05dc2bc853aa8989838_239_0.png)

| 低速发动机 | 中速发动机 | 涡轮增压器 | 螺旋桨 | 推进包 | 服务 |
| :--- | :--- | :--- | :--- | :--- | :--- |

环保海洋动力和推进解决方案的设计对于 MAN Diesel & Turbo 关关重要。我们提供全球最大的发动机计划——每台发动机的输出从 450 kW 到 87,220 kW 不等。立即行动！访问.mandieselturbo.com 了解更多。
工程未来——自1758年以来。
MAN Diesel & Turbo

在 bookoon.com 免费下载电子书

# C# 1 编程入门与 C# 语言 对象序列化

![](img/f84352ec481fd05dc2bc853aa8989838_240_0.png)

在下一个窗口中，点击底部的“浏览”`Browse`按钮。你会得到一个文件浏览器并并浏览到 `dll`（项目 `Datatypes` 中的 `Datatypes.dll`）：

![](img/f84352ec481fd05dc2bc853aa8989838_240_1.png)

当你点击“确定”`OK`时，`dll` 被复制到当前项目中，其类现在可以程序可以使用。如果你在“解决方案管理器”中打开“引用”，你可以看到程序可以访问哪些 `dll`，现在包含了 `Datatypes`。其他 `dll` 是 Visual Studio 自动添加引用的某些 `dll`，它们包含了 `.NET` 框架中所有的主类。

在 bookboom.com 免费下载电子书 241

## C# 1 编程入门与 C# 语言

# 对象序列化

![](img/f84352ec481fd05dc2bc853aa8989838_241_0.png)

在带有 `Person` 类的 `dll` 附加到程序后，代码如下所示编写：

```csharp
using System;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
using Datatypes;

namespace Exam61
{
    class Program
    {
        static void Main(string[] args)
        {
            Person pers = new Person("Valborg Kristensen", "Klog kone");
            Serialiser(pers);
        }
        private static void Serialiser(Person pers)
        {
            BinaryFormatter bf = new BinaryFormatter();
            FileStream stream = File.Create("F:\\Temp\\Person.dat");
            bf.Serialize(stream, pers, null);
            stream.Close();
        }
    }
}
```

# 解析

首先注意程序的 `using` 语句。除了 `System.IO` 之外，还定义了命名空间：

`using System.Runtime.Serialization.Formatters.Binary;`

它包含了能够序列化对象所需的类。注意，这里有一个带有 `Person` 类的命名空间定义：

在 bookboom.com 免费下载电子书

`using Datatypes;`

`Main()` 中有一个对象

```csharp
Person pers = new Person("Valborg Kristensen", "Klog kone");
```

任务是将此对象写入文件。这意味着必须将两个成员变量 `name` 和 `position` 存储为 `string` 类型对象。不仅要保存对象，你还必须能够再次读取该对象，如上面所述，你还存储了关于对象类型的信息。对象以原始字节存储，可以再次加载为 `Person` 对象——由两个 `string` 类型对象组成——前提是这些信息与对象的数据字节一起保存。这个过程被称为序列化，为了使这种可能性实现，对象的类型必须定义为 `Serializable`，并且对象的所有实例变量都必须是 `Serializable`。在这种情况下，所有条件都满足了：`Person` 类被定义为 `Serializable`，成员变量是 `string` 类型，`string` 是 `Serializable` 的。所有简单类型和 `.NET` 框架类型也是如此。

要序列化一个对象，你必须使用所谓的格式化器 `Formatter`。有多种选择，不同的 `Formatter` 类型定义在 `System.Runtime.Formatters` 命名空间中，但它们的共同点是序列化对象时包含了对象反序列化时所需的信息。然而，它们在存储对象的格式上有所不同。在这种情况下，我使用二进制格式化器，它以二进制格式存储对象。

![](img/f84352ec481fd05dc2bc853aa8989838_242_0.png)

## C# 1 编程入门与 C# 语言

### 解释

`Deserializer()` 方法尝试反序列化存储在 `F:\Temp\Person.dat` 中的一个 `Person` 类型对象。第一个程序创建了一个 `BinaryFormatter`。接下来，它创建了一个指向文件的流，并对对象进行反序列化。如果可以反序列化 `Person` 对象（如果文件存在且包含一个 `Person` 对象），则该方法返回该对象。否则，该方法返回 `null`。注意，这需要进行类型强制转换为 `Person` 对象。

# 注释

当你反序列化一个对象时，它的类型可能与其被序列化时的类型相同。这里我们必须记住，对象的类型也由包含其类型的命名空间 `namespace` 标识。这就是为什么在上面的示例中，我将 `Person` 类放在一个类库中，以便让 `Person` 在两个程序中都是同一种类型。

## Exam63

## XML 序列化

这个示例在原理上与前两个完全相同，但程序没有使用 `BinaryFormatter`，而是使用 `XmlSerializer`，因此对象以 XML 格式存储，而不是二进制数据。

# 如何操作

再次，从引用包含 `Person` 类的 `dll` 开始。代码如下所示：

```csharp
using System;
using System.IO;
using System.Xml.Serialization;
using Datatypes;

namespace Exam63
{
    class Program
    {
        static void Main(string[] args)
        {
            Save();
            Load();
        }
        public static void Save()
        {
            Person pers = new Person("Knud Andersen","Skarpretter");
            Serializer(pers);
        }
        public static void Load()
        {
            Person pers = Deserializer();
            if (pers != null) Console.WriteLine(pers);
        }
    }
}
```

在 bookhoon.com 下载免费电子书

## C# 1 编程入门与 C# 语言

```csharp
private static void Serializer(Person pers)
{
    XmlSerializer xs = new XmlSerializer(typeof(Person));
    FileStream stream = File.Create("F:\Temp\Person.xml");
    xs.Serialize(stream, pers);
    stream.Close();
}

private static Person Deserializer()
{
    Person pers = null;
    try {
        XmlSerializer xs = new XmlSerializer(typeof(Person));
        FileStream stream = File.OpenRead("F:\Temp\Person.xml");
        pers = (Person)xs.Deserialize(stream);
        stream.Close();
    }
    catch {
        return pers;
    }
}
```

### 解释

代码实际上没有变化，主要的区别在于程序使用了不同的命名空间，因此也使用了其他的序列化对象。

![](img/f84352ec481fd05dc2bc853aa8989838_245_0.png)

## C# 1 编程入门与 C# 语言 对象序列化

将对象序列化为 xml 的优点是，任何能读懂文本文件的人都可以读取并解释它。它不需要了解 `BinaryFormatter` 所使用的二进制格式。

文件 `Person.xml` 的内容如下：

```xml
<xml version="1.0"?>
<Person xmlns="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsi="http://www.w3.org/2001/XMLSchema">
  <Name>Knud Andersen</Name>
  <Position>Skarpretter</Position>
</Person>
```

如果你查看生成的数据，你会发现仅仅能反序列化对象是不够的。如果一个对象是可 XML 序列化的，有几点是必须的：
- 必须有一个默认构造函数
- 实例变量必须有 `get` 和 `set` 属性

虽然二进制序列化（以及下方所示的 SOAP 序列化）不需要这些，但在类中同时附加默认构造函数和必要的属性是一个好主意。

## SOAP 序列化

这个示例与上面完全相同，不同在于这次对象是使用 SOAP 协议进行序列化的。在所有其他示例中，必须有对类型类型 `dll` 的引用，但这次有一个小小的观察：soap 格式位于 Visual Studio 所引用的命名空间中，因此需要手动设置命名空间引用（见下文）。然后可以编写代码：

```csharp
using System;
using System.IO;
using System.Serialization.Formatters.Soap;
using Datatypes;

namespace Exam64
{
  class Program
  {
    static void Main(string[] args)
    {
        Save();
        Load();
    }
}
```

在 bookboom.com 下载免费电子书

## C# 1 编程入门与 C# 语言 对象序列化

```csharp
public static void Save() {
    Person pers = new Person("Gudrun Mortensen", "Heks");
    Serializer(pers);
}
public static void Load() {
    Person pers = Deserializer();
    if (pers != null) Console.WriteLine(pers);
}
private static void Serializer(Person pers) {
    SoapFormatter sf = new SoapFormatter();
    FileStream stream = File.Create("F:\\Temp\\Person.txt");
    sf.Serialize(stream, pers);
    stream.Close();
}
private static Person Deserializer() {
    Person pers = null;
    try {
        SoapFormatter sf = new SoapFormatter();
        FileStream stream = File.OpenRead("F:\\Temp\\Person.txt");
        pers = (Person)sf.Deserialize(stream);
        stream.Close();
    }
    catch {
        return pers;
    }
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_245_0.png)

在 bookboom.com 下载免费电子书

## C# 1 编程入门与 C# 语言

### 解释

当你反序列化一个对象时，它的类型可能与其被序列化时的类型相同。这里我们必须记住，对象的类型也由包含其类型的命名空间标识。这就是为什么在在上面的示例中，我将 `Person` 类放在一个类库中，以便让 `Person` 在两个程序中都是同一种类型。

```xml
<xml version="1.0"?>
<Person xmlns="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsi="http://www.w3.org/2001/XMLSchema">
  <Name>Gudrun Mortensen</Name>
  <Position>Heks</Position>
</Person>
```

## SOAP 序列化

这个示例与上面完全相同，不同在于这次对象是使用 SOAP 协议进行序列化的。在所有其他示例中，必须有对类型类型 `dll` 的引用，但这次有一个小小的观察：soap 格式位于 Visual Studio 所引用的命名空间中，因此需要手动设置命名空间引用（见下文）。然后可以编写代码：

```csharp
using System;
using System.IO;
using System.Serialization.Formatters.Soap;
using Datatypes;

namespace Exam64
{
  class Program
  {
    static void Main(string[] args)
    {
        Save();
        Load();
    }
}
```

## C# 1 编程入门与 C# 语言 对象序列化

```csharp
public static void Save() {
    Person pers = new Person("Gudrun Mortensen", "Heks");
    Serializer(pers);
}
public static void Load() {
    Person pers = Deserializer();
    if (pers != null) Console.WriteLine(pers);
}
private static void Serializer(Person pers) {
    SoapFormatter sf = new SoapFormatter();
    FileStream stream = File.Create("F:\\Temp\\Person.txt");
    sf.Serialize(stream, pers);
    stream.Close();
}
private static Person Deserializer() {
    Person pers = null;
    try {
```
