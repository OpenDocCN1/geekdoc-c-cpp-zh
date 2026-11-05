
| 构造函数 | 描述 |
|---|---|
| XmlTextWriter (TextWriter) | 创建 XmlTextWriter 类的实例，使用指定的 TextWriter。 |
| XmlTextWriter (Stream, Encoding) | 创建 XmlTextWriter 类的实例，使用指定的流和编码。 |
| XmlTextWriter (String, Encoding) | 创建 XmlTextWriter 类的实例，使用指定的文件和编码。 |

## 示例

```csharp
//the classfile for writing in to xml file
using System.Xml;
class User
{
    public string Name { get; private set; }
    public int Age { get; private set; }
    public DateTime Registered { get; private set; }

    public User(string name, int age, DateTime registered)
    {
        Name = name;
        Age = age;
        Registered = registered;
    }

    public override string ToString()
    {
        return Name;
    }
}
// a collection of test users
List<User> users = new List<User>();
users.Add(new User("Ravi", 42, new DateTime(2020, 3, 1)));
users.Add(new User("Ram", 41, new DateTime(2020, 4, 2)));
users.Add(new User("Raj", 40, new DateTime(2020, 6, 3)));

// the XmlWriter settings
XmlWriterSettings settings = new XmlWriterSettings();
settings.Indent = true;

// writes the users
using (XmlWriter xw = XmlWriter.Create(@"users.xml", settings))
{
    xw.WriteStartDocument(); // the header
}
```

```xml
<name>Ram </name>
<registered>1/2/2020</registered>
</user>
</users>
```

User 的类如下，

```csharp
class User
{
    public string Name { get; private set; }
    public int Age { get; private set; }
    public DateTime Registered { get; private set; }

    public User(string name, int age, DateTime registered)
    {
        Name = name;
        Age = age;
        Registered = registered;
    }
    public override string ToString()
    {
        return Name;
    }
}
```

XML 文件读取代码如下，

```csharp
using (XmlReader xr = XmlReader.Create("users.xml"))
{
    string name = "";
    int age = 0;
    DateTime registered = DateTime.Now;
    string element = "";
    while (xr.Read())
    {
        // reads the element
        if (xr.NodeType == XmlNodeType.Element)
        {
            element = xr.Name; // the name of the current element
            if (element == "user")
            {
                age = int.Parse(xr.GetAttribute("age"));
            }
        }
        // reads the element value
        else if (xr.NodeType == XmlNodeType.Text)
        {
            switch (element)
            {
                case "name":
                    name = xr.Value;
                    break;
                case "registered":
                    registered = DateTime.Parse(xr.Value);
                    break;
            }
        }
        // reads the closing element
        else if ((xr.NodeType == XmlNodeType.EndElement) && (xr.Name == "user"))
            users.Add(new User(name, age, registered));
    }
}
```

## 17.9.3 DOM vs SAX

| 序号 | DOM | SAX |
|---|---|---|
| 1. | 在处理之前将整个 XML 文档存储到内存中。 | 按节点解析。 |
| 2. | 节点可以插入或删除。 | 节点不能插入或删除。 |
| 3. | 在处理之前将整个文档存储在内存中，占据更多内存，在解析器开始解析之前整个 xml 树必须在内存中。 | 不在内存中存储 XML，整个 xml 树在解析器开始解析之前不必加载，它可以处理给定 xml 树的最大深度。 |
| 4. | 遍历可以在任何方向进行。 | 遍历只能自上而下进行。 |
| 5. | DOM 有正式规范。 | SAX 中没有正式规范。 |
| 6. | 从磁盘流式读取是不可能的。 | 从磁盘流式读取是可能的。 |
| 7. | XML 验证期间问题较少。 | XML 验证期间问题更多。 |
| 8. | 它不是事件触发解析器。 | 它是事件触发解析器。 |

## 两分题问答

### Q.1 XML 的特点是什么？

Ans. : XML 的主要特点是：

- 非常容易学习和实现。
- XML 文件是文本文件，且不需要编辑器。
- XML 中的语法规则最少且有限。
- 它是可扩展的，并且指定了标签的结构规则。

### Q.2 哪个标签用于查找 XML 版本和语法？

Ans. : 为每个 XML 文档声明 XML 版本非常重要，并且需要指定其运行的平台。

```xml
<?xml version="1.1" encoding="ISO-8859-1"?>
```

### Q.3 什么是 XML DOM Document？

Ans. : XML Document 对象表示整个 XML 文档，并且是文档树的根。它提供了对整个 XML 文档的访问 – 节点和元素，并且它有自己的属性。

### Q.4 什么是 XPath？

Ans. : XPath 用于在 XML 文档中查找信息并包含标准函数。XPath 是 XSLT 中的主要元素，并且是 W3C 推荐。

### Q.5 什么是属性？

Ans. : 属性比其他方式提供了有关元素的更多或附加信息。

示例 -

```xml
<Person name = "Bharat" >
```

### Q.6 定义 XML。给出示例。AU : Dec.17

Ans. : 可扩展标记语言 (XML) 用于描述数据。XML 标准是一种灵活的方式，可通过公共互联网以及企业网络创建信息格式并电子共享结构化数据。

XML 文档的基本构建块是元素，由标签定义。

例如，

```xml
<?xml version="1.0" standalone="yes"?>
<conversation>
<greeting>Hello!</greeting>
<response>It is AUT Question Paper I</response>
</conversation>
```

## 长问答题

- Q.1 讨论 XML。 (参见第 17.1 节)
- Q.2 什么是 XML 元素？ (参见第 17.2 节)
- Q.3 如何使用 DOM 操作 XML？ (参见第 17.9 节)
- Q.4 如何使用 SAX 操作 XML？ (参见第 17.9 节)
- Q.5 什么是 XML 模式？ (第 17.5 节)

*XML、操作 XML、SAX 和 DOM 结束 ...*

## 注释

## 单位 - III

## 章节 - 18

## 点对点网络、PNRP、构建 P2P 应用

Syllabus : 点对点网络、构建 P2P 应用、PNRP。

| 节号 | 主题名称 | 页码 |
|---|---|---|
| 18.1 | 点对点 (P2P) 网络 - 简介 | 18 - 2 |
| 18.2 | P2P 术语 | 18 - 2 |
| 18.3 | P2P 架构挑战 | 18 - 3 |
| 18.4 | P2P 网络的用途 | 18 - 4 |
| 18.5 | P2P 网络的好处 | 18 - 4 |
| 18.6 | PNRP - 对等名称解析协议 | 18 - 5 |
| 18.7 | 构建 P2P 应用 | 18 - 13 |
| 18.8 | 点对点应用模型 | 18 - 22 |
| 18.9 | 防火墙和端口 | 18 - 23 |
|  | 两分题问答 | 18 - 23 |
|  | 长问答题 | 18 - 24 |

## 18.1 点对点 (P2P) 网络 - 简介

- P2P 代表 Peer-To-Peer。当两台或多台计算机连接并在不经过单独的服务器计算机的情况下共享资源时，就会创建 P2P 网络。P2P 网络中的所有计算机具有同等特权。在 P2P 网络中，计算机既是服务器也是客户端。无需中央协调。P2P 网络中的计算机通常称为节点。

![](img/3005a4307e6d8f3bb7e76eea28a92357_557_0.png)

## 18.2 P2P 术语

- 在 P2P 网络中，peer 是指客户端的方式。在 P2P 网络中，“客户端”一词没有意义，因为不一定有‘服务器’可供客户端使用。
- 相互连接的对等组被称为可互换的术语 meshes、clouds 或 graphs。如果满足以下条件，则可以说某个组连接良好，
  1. 每对对等体之间都有连接路径，因此每个对等体可以根据需要连接到任何其他对等体。
  2. 对等体之间需要遍历的连接数量相对较少。
  3. 删除一个对等体不会阻止其他对等体相互连接。
- 应该注意的是，这并不意味着每个对等体都必须能够连接到每个其他对等体。事实上，如果对网络进行密切的数学分析，就会发现
