

# 与 XML 文档工作的类

```csharp
using System;
using System.Xml;
using System.Collections.Generic;

namespace ProductMaintenance
{
    public class ProductDB
    {
        private const string path = @"C:\C# 2010\Files\Products.xml";

        public static List<Product> GetProducts()
        {
            // create the list
            List<Product> products = new List<Product>();

            // create the XmlReaderSettings object
            XmlReaderSettings settings = new XmlReaderSettings();
            settings.IgnoreWhitespace = true;
            settings.IgnoreComments = true;

            // create the XmlReader object
            XmlReader xmlIn = XmlReader.Create(path

public static void SaveProducts(List<Product> products)
        {
            // create the XmlWriterSettings object
            XmlWriterSettings settings = new XmlWriterSettings();
            settings.Indent = true;
            settings.IndentChars = (" ");

            // create the XmlWriter object
            XmlWriter xmlOut = XmlWriter.Create(path, settings);

            // write the start of the document
            xmlOut.StartDocument();
            xmlOut.WriteStartElement("Products");

            // write each Product object to the xml file
            foreach (Product product in products)
            {
                xmlOut.WriteStartElement("Product");
                xmlOut.WriteAttributeString("Code",
                    product.Code);
                xmlOut.WriteElementString("Description",
                    product.Description);
                xmlOut.WriteElementString("Price",
                    Convert.ToString(product.Price));
                xmlOut.WriteEndElement();
            }

            // write the end tag for the root element
            xmlOut.WriteEndElement();

            // close the XmlWriter object
            xmlOut.Close();
        }
    }
}
```

图 22-10 ProductDB 类的代码（部分 2/2）

# 观点

在本章中，你学习了使用 `XmlReader` 和 `XmlWriter` 类读写 XML 文档的基础知识。掌握了这些技能后，你应该能够将简单的 XML 文档整合到你的应用程序中。你还应该更好地理解你在第 4 节中学到的数据库应用程序内部使用 XML 的方式。

然而，本章只是对 XML 的介绍，忽略了一些重要特性。例如，你可以使用 XML 架构（schemas）来定义 XML 文档的布局。然后，可以使用 .NET 类来确保 XML 文档符合其架构。你还可以使用 DOM（即文档对象模型），将整个 XML 文档视为一个单一的 `XmlDocument` 对象，该对象的属性集合代表了 XML 文档的节点。简而言之，在精通 XML 之前，还有很多东西需要学习。

# 术语

- XML (可扩展标记语言) 标签 父级元素
- XML 文档 根元素
- XML 声明 属性 空白元素
- 开始标签 节点
- 结束标签 当前节点 内容

# 练习 22-1 与 XML 文件操作

- 打开位于 `C:\C# 2010\222CustomerXML` 目录下的项目。这是你为第 12 节练习开发的 `CustomerMaintenance`应用程序，但它不会保存或检索数据。

- 使用 Visual Studio 打开存储在 `C:\C# 2010\Files` 目录下的 `Customers.xml` 文件。这应该会在 XML 编辑器中打开该文件，以便你可以看到数据结构。

- 在 `CustomerDB` 类中，为 `GetCustomers` 和 `SaveCustomers` 方法添加代码，以便它们从 `Customers.xml` 文件读取数据到 `List<Customer>` 对象的列表中，并将 `List<Customer>` 对象的列表中的数据写入 XML 文件。

- 通过添加和删除客户来测试应用程序。要验证数据是否已保存到磁盘，你可以停止应用程序并重新运行。你可以使用 Visual Studio 在 XML 编辑器中查看 XML 文件。或者在 Windows 资源管理器中双击该文件。在大多数系统中，这会在你的默认网络浏览器中显示 XML 文件。

# 23

# 如何使用 LINQ

在本章中，你将学习使用 C# 一项名为 LINQ 的功能的基本技能。LINQ 提供了一种方法，让你使用 C# 语言内置的构造来查询数据源。这样，你就可以使用相同的语言访问各种数据源。

在本章中，我将重点介绍将 LINQ 用于内存数据结构（如数组和泛型列表）。不过，在阅读本章时，请记住，你可以使用相同的技能来查询数据集、关系数据库和 XML 文件。

为了让你直观了解其工作原理，我将在本末介绍两个执行相同功能的应用程序。第一个将使用 LINQ 查询两个泛型列表，第二个将使用 LINQ 查询类型数据集中的两个表。一旦你看到这些应用程序的查询是如此相似，你就应该开始理解使用 LINQ 的真正威力。

| 主题 | 页码 |
| :--- | :--- |
| 使用 LINQ 的基础概念 | 706 |
| LINQ 是如何实现的 | 706 |
| 使用 LINQ 的优势 | 706 |
| 查询操作的三个阶段 | 708 |
| 如何编写 LINQ 查询 | 710 |
| 如何识别查询的数据源 | 710 |
| 如何过滤查询结果 | 712 |
| 如何排序查询结果 | 714 |
| 如何从查询中选择字段 | 716 |
| 如何连接来自两个或多个数据源的数据 | 718 |
| 客户发票应用程序 | 720 |
| 使用泛型列表的 | 720 |
| 用户界面 | 722 |
| 表单代码 | 722 |
| 客户发票应用程序 | 724 |
| 使用类型数据集的 | 724 |
| 数据集架构 | 724 |
| 表单代码 | 726 |
| 观点 | 728 |

# 使用 LINQ 的基础概念

正如其名所示，LINQ（即语言集成查询，Language-Integrated Query）让你能够使用 C# 语言查询数据源。在学习如何编写 LINQ 查询之前，你需要学习一些与 LINQ 相关的概念，例如 LINQ 是如何实现的，以及查询操作的三个阶段是什么。此外，你还想知道从 LINQ 中获得的优势，以便你判断它是否是你想要使用的功能。

# LINQ 是如何实现的

LINQ 实现为由 `Enumerable` 类定义的一组方法。由于这些方法只能在查询操作中使用，因此它们被称为查询运算符。为了方便使用查询运算符，C# 提供了可以访问这些运算符的关键字。如果你曾经用 SQL 编写过查询，那么理解这些关键字应该不会有困难。例如，你使用 `from` 关键字来识别查询的数据源。使用 `where` 关键字来过滤返回的数据。使用 `select` 关键字来标识你想要返回的字段。你将在本章稍后学习如何编写这些关键字。

# 使用 LINQ 的优势

图 23-1 还列出了 LINQ 的若干优势。最大的优势可能是它让你使用相同的语言查询不同类型的数据源。正如你在本章中看到的，例如，可以使用相同的语言查询数组和对象的泛型列表。在阅读本章时请记住，你可以使用相同的技能来查询复杂的数据源，如数据集和数据库。

实现这种功能的关键在于查询语言集成到了 C# 中。正因如此，你不需要为每种数据源学习不同的查询语言。此外，当你输入查询时，可以利用 C# 语言提供的 IntelliSense 功能。编译器可以捕捉查询中的错误（例如数据源中不存在的字段），因此在运行时产生错误。当发生运行时错误时，可以使用 Visual Studio 的调试功能确定其原因。

最后，如果你正在处理关系数据源（如 SQL 数据库），可以使用 Visual Studio 提供的设计工具开发对象-关系映射。然后，你可以使用 LINQ 查询由映射定义的对象，而查询将被转换为数据源所需的格式。这可以显著简化与关系数据源的工作。

![](img/3148667e42d4db35b3d08576aaa1fa01_725_0.png)

