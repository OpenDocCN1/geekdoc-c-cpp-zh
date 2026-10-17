
```csharp
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

图 22-10 `ProductDB` 类的代码（部分 2/2）

# 观点

在本章中，你学习了使用 `XmlReader` 和 `XmlWriter` 类读写 XML 文档的基础知识。掌握了这些技能后，你应该能够将简单的 XML 文档整合到你的应用程序中。你还应该更好地理解你在第 4 节中学到的数据库应用程序内部使用 XML 的方式。

然而，本章只是对 XML 的介绍，忽略了一些重要特性。例如，你可以使用 XML 架构（schemas）来定义 XML 文档的布局。然后，可以使用 .NET 类来确保 XML 文档符合其架构。你还可以使用 DOM（即文档对象模型），将整个 XML 文档视为一个单一的 `XmlDocument` 对象，该对象的属性集合代表了 XML 文档的节点。简而言之，在精通 XML 之前，还有很多东西需要学习。

## 术语

- XML (可扩展标记语言) 标签 父级元素
- XML 文档 根元素
- XML 声明 属性 空白元素
- 开始标签 节点
- 结束标签 当前节点 内容

# 练习 22-1 与 XML 文件操作

- 打开位于 `C:\C# 2010\222CustomerXML` 目录下的项目。这是你为第 12 节练习开发的 `CustomerMaintenance` 应用程序，但它不会保存或检索数据。
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

# 用于处理 LINQ 的 C# 关键字

| 关键字 | 描述 |
|---|---|
| from | 标识查询的数据源。 |
| where | 提供一个条件，根据该条件从数据源检索元素。 |
| orderby | 指明查询返回元素的排序方式。 |
| select | 指定返回元素的内容。 |
| join | 合并来自两个数据源的数据。 |

# 使用 LINQ 的优势

- 通过将查询语言与 C# 集成，让你轻松地查询数据源。
- 通过提供 IntelliSense（智能感应）、编译时语法检查和调试支持，让你轻松地开发查询数据源的应用程序。
- 因为你对每种类型的数据源都使用相同的基础语法，所以查询查询查询变得简单。
- 通过提供创建对象关系映射的设计器工具，让你轻松地使用对象来处理关系型数据源。

## 描述

- 语言集成查询 (LINQ) 提供了一组查询运算符，作为 C# 语言的关键字可用。你使用这些关键字来定义查询表达式，以识别你想从数据源中检索的数据。
- 要对数据源使用 LINQ，数据源必须实现 `IEnumerable<T>` 接口或其他实现 `IEnumerable<T>` 的接口（如 `IQueryable<T>`）。有关接口的更多信息，请参见第 15 章。
- 支持非泛型 `IEnumerable` 接口的数据源（如数组或列表）用于 LINQ。

# 注意

- LINQ 运算符实现为 `Enumerable` 类的方法。尽管你可以直接执行这些方法，但你更有可能使用 C# 语言内置的关键字。

![](img/3148667e42d4db35b3d08576aaa1fa01_726_0.png)

# 查询操作的三个阶段

图 23-2 展示了查询操作的三个阶段，并使用数组说明了这些阶段。第一阶段是获取数据源。这取决于你正在处理的数据源类型。对于此处显示的数组，获取数据源意味着定义一个名为 `numbers` 的数组并为其元素赋值。此外，该数组包含五个值为 0, 1, 2, 3 和 4 的整数。

第二阶段是定义查询表达式。该表达式识别数据源以及要从该数据源检索的数据。例如，图中的查询表达式从 `numbers` 数组中检索偶数。它还将这些整数按降序排列。（如果你不理解此查询表达式的语法，请担心。你将在后续主题中学习如何编写查询表达式。）

注意这里，查询表达式存储在查询变量中。这是必要的，因为该查询在定义时并不会执行。还要注意，查询变量没有用显式类型声明。相反，它是根据查询返回的元素类型隐式赋予类型的。在这种情况下，因为查询返回整数，所以查询变量被赋予了 `IEnumerable<int>` 类型。

对于这项工作，数据源必须实现 `IEnumerable` 或 `IEnumerable<T>` 接口。如果你不熟悉接口（接口由一组对或多个属性、方法和事件的声明组成，但不提供这些属性、方法和事件的实现），如果你想了解更多关于接口的信息，可以阅读第 15 章。对于图中的示例，你只需要知道数组实现了 `IEnumerable` 接口。

查询操作的第三阶段是执行查询。要做到这一点，你通常使用如图所示的 `foreach` 语句。在这里，查询表达式返回的每个元素都被添加到字符串变量中。然后，在处理完所有元素后，将字符串显示在消息框中。如你所见，此消息框列出了查询表达式定义的 4 到 0 的偶数。

顺便说一下，你可能注意到我在此示例的每行中包含了两个制表符。这些字符是为了使对话框足够宽以容纳整个标题。没有这些字符，标题会被截断。

当像此处所示定义并执行查询时，该过程被称为**延迟执行**（deferred execution）。相比之下，在定义时就执行的查询使用**立即执行**（immediate execution）。当在查询表达式执行的方法需要访问查询返回的单个元素时，通常会发生立即执行。例如，为了获取查询返回的元素计数，你可以在查询表达式上执行 `Count` 方法。然后，查询将立即执行，以便计算计数。尽管 LINQ 提供了几种方法来返回此类值，但你不会在书中学习到它们。

# 查询操作的三个阶段

- 获取数据源。如果数据源是数组，例如你必须声明数组并为其元素赋值。
- 定义查询表达式。
- 执行查询以返回结果。

# 从数组检索数据的 LINQ 查询

```csharp
int[] numbers = new int[6];
for (int i = 0; i < numbers.Length; i++)
numbers[i] = i;
```

# 在 numbers 中定义查询的语句

```csharp
var numberList = from number in numbers
where number % 2 == 0
orderby number descending
select number;
```

# 执行查询的代码

```csharp
string numberDisplay = "";
foreach (var number in numberList)
numberDisplay += number + "\t\n";
MessageBox.Show(numberDisplay, "Sorted Even Numbers");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_728_0.png)

## 描述

- 上述过程被称为延迟执行，因为查询在定义时并不执行。当程序通过 `foreach` 语句访问查询返回的单个元素时，查询才会执行。由于查询在定义时并不执行，它存储在查询变量中。注意，查询变量没有显式类型。相反，它是根据查询返回的元素类型隐式赋予的。在这种情况下，查询变量被赋予类型为 `IEnumerable<int>`。
- 当查询在定义时就执行时，它使用立即执行。这通常发生在执行的方法需要访问查询返回的单个元素时。例如，为了获取查询返回的元素计数，你可以在查询表达式上执行 `Count` 方法。然后，查询将立即执行，以便计算计数。尽管 LINQ 提供了几种方法来返回此类值，但你不会在书中学习到它们。
- 图 23-2 查询操作的三个阶段

# 如何编写 LINQ 查询

现在你对什么是 LINQ 查询有了基本的了解，你需要学习编写查询的语法。

# 如何为查询识别数据源

要识别查询的数据源，你可以看到 23-3 所示的 `from` 子句。该句声明了一个用于表示元素的变量，并命名了数据源，数据源必须实现 `IEnumerable<T>`。它还可以为变量指定类型，通常是省略的。如果省略，它由数据源元素的类型决定。

图中的第一个示例显示了如何对名为 `sales` 的数组使用 `from` 子句。示例中的第一个语句声明了数组并为其元素赋值。然后，第二个语句定义了查询表达式，它由 `from` 子句和 `select` 子句组成。该表达式存储在名为 `salesList` 的查询变量中。最后，`foreach` 语句遍历查询返回的值并计算这些值的总和。

此时，你应该意识到查询表达式必须以 `from` 子句开头，以识别数据源。这样，C# 就知道查询的数据源是什么，并根据此帮助你构建查询。此外，查询表达式必须以 `select` 子句或 `group` 子句结束。在本示例中，`select` 子句仅指示查询返回数组元素。

在本章的后半部分，你将看到可以使用 `select` 子句从数据源的每个元素返回所需的字段。

图中第二个示例显示了如何对泛型发票列表使用 `from` 子句。在这里，你可以看到 `Invoice` 类由一组自动实现的属性组成。然后，随后的语句创建了一个基于此类的列表，并使用 `InvoiceDB` 类的 `GetInvoices` 方法从中加载发票。注意，你不需要知道该方法是如何工作的。你只需要知道它返回一个 `List<Invoice>` 对象。该对象随后赋值给名为 `invoiceList` 的变量。

# from 子句的语法

from [type] elementName in collectionName

# 一个使用小数型数组的示例

获取数据源的语句

```csharp
decimal[] salesTotals = new decimal[4] = {1286.45m, 2433.49m, 2893.85m, 2094.53m};
```

定义查询表达式的语句

```csharp
var salesList = from sales in salesTotals
select sales;
```

# 执行查询的代码

```csharp
decimal sum = 0;
foreach (var sales in salesList)
sum += sales;
```

# 一个使用泛型发票列表作为数据源的示例

Invoice 类

```csharp
public class Invoice {
    public int InvoiceID { get; set; }
    public int CustomerID { get; set; }
    public DateTime InvoiceDate { get; set; }
    public decimal ProductTotal { get; set; }
    public decimal SalesTax { get; set; }
    public decimal Shipping { get; set; }
    public decimal InvoiceTotal { get; set; }
}
```

获取数据源的语句

```csharp
List<Invoice> invoiceList = InvoiceDB.GetInvoices();
```

定义查询表达式的语句

```csharp
var invoices = from invoice in invoiceList
select invoice;
```

# 执行查询的代码

```csharp
decimal sum = 0;
foreach (var invoice in invoices)
sum += invoice.InvoiceTotal;
```
