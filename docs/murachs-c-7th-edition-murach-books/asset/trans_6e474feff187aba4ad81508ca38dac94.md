

## join 子句的基本语法

```
join elementName in collectionName on keyName1 equals keyName2
```

### 一个从两个通用列表中连接数据的示例

### Customer 类

```
public class Customer
{
    public int CustomerID { get; set; }
    public string Name { get; set; }
}
```

### 获取两个数据源的代码

```
List<Invoice> invoiceList = InvoiceDB.GetInvoices();
List<Customer> customerList = CustomerDB.GetCustomers();
```

### 一个从两个数据源中连接数据的查询表达式

```
var invoices = from invoice in invoiceList
    join customer in customerList
    on invoice.CustomerID equals customer.CustomerID
    where invoice.InvoiceTotal > 150
    orderby customer.Name, invoice.InvoiceTotal descending
    select new { customer.Name, invoice.InvoiceTotal };
```

### 执行查询的代码

```
string invoiceDisplay = "Customer Name\t\tInvoice amount\n";
foreach (var invoice in invoices)
{
    invoiceDisplay += invoice.Name + "\t\t";
    invoiceDisplay += invoice.InvoiceTotal.ToString("c") + "\n";
}
MessageBox.Show(invoiceDisplay, "Joined Customer and Invoice Data");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_617_0.png)

### 描述

- join 子句让你能够基于匹配的键值将来自两个或多个数据源的数据合并起来。查询结果将只包括满足 equals 运算符指定的条件的元素。
- 你可以扩展上面所示的语法以从额外的数据源中连接数据。

## 如何使用扩展方法和 lambda 表达式

本章前面我提到过，LINQ 提供的查询运算符是以方法形式实现的，你可以直接调用这些方法而不是使用 C# 的 LINQ 子句。在接下来的主题中，你将学习这些方法的工作原理以及如何使用它们来实现 LINQ 功能。

### 扩展方法的工作原理

提供 LINQ 功能的大多数方法都是以扩展方法形式实现的。扩展方法与普通方法类似，只是它是在使用它的数据类型之外定义的。图 18-8 中的示例展示了其工作原理。这里，一个名为 FormattedPhoneNumber() 的方法被实现为 String 类的扩展方法。

你应该注意到实现此方法代码的三个方面。首先，它是一个存储在静态类中的静态方法，这是扩展方法的必要条件。其次，该方法的第一个参数的数据类型标识了该方法所扩展的 .NET 类或结构。在本例中，参数是 string，因此该方法扩展了 String 类。第三，第一个参数的声明前面有 this 关键字。

一旦你定义了扩展方法，就可以在此图示的方式中使用它。首先，你声明一个与方法第一个参数相同类型的变量。在本例中，声明了一个 string 变量并赋值为电话号码的数字。然后，将扩展方法作为该字符串的方法执行。请注意，你不会向该方法的第一个参数传递值。相反，方法执行时对象的取值会被赋给该参数。如果方法定义了任何额外参数，则其值会按此处所示传递给方法。

### 一个扩展 String 数据类型的方法

### 一个格式化电话号码的扩展方法的类

```
public static class StringExtensions
{
	public static string FormattedPhoneNumber(this string phone, string separator)
	{
		return phone.Substring(0, 3) + separator
		       + phone.Substring(3, 3) + separator
		       + phone.Substring(6, 4);
	}
}
```

### 使用扩展方法的代码

```
string phoneNumber = "5595551212";
string formattedPhoneNumber = phoneNumber.FormattedPhoneNumber(".");
MessageBox.Show(formattedPhoneNumber + "\t", "Extension Method");
```

### 生成的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_619_0.png)

- 扩展方法提供了从该数据类型的定义外部为数据类型添加方法的功能。扩展方法必须在静态类中编码。
- 扩展方法的第一个参数标识其所扩展的数据类型，并且必须以 this 关键字为前缀。你在调用方法时不会向此参数传递值。相反，你在由第一个参数标识的数据类型的实例上调用该方法。

### lambda 表达式的工作原理

如果你读过第 13 章，你已经知道如何使用 lambda 表达式与委托。如果没有读过该章节，图 18-9 总结了使用 lambda 表达式的概念。

简而言之，*lambda 表达式* 是一个没有名称的函数，它计算一个表达式并返回其值。如本图所示，lambda 表达式的语法由参数列表后跟 lambda 运算符和一个表达式组成。请注意，如果 lambda 表达式使用单个参数，则可以省略括号。

要使用 lambda 表达式，你将其分配给 *委托* 类型，该类型指定了方法的签名。本图中的第一个示例说明了其工作原理。这里，第一条语句定义了一个名为 compareDel 的委托类型，它接受一个 decimal 值并返回一个 Boolean 值。然后，第二条语句声明了该类型的委托名为 invoiceOver150 并将其分配给一个 lambda 表达式。在本例中，lambda 表达式检查名为 total 的 decimal 参数是否大于 150。如果是，表达式将返回 true 值。否则，它将返回 false 值。

在此示例中，lambda 表达式被分配给一个变量。然后，在执行 lambda 表达式的代码中，该变量用于引用 lambda 表达式并传入 decimal 值。然而，当你使用 lambda 表达式与 LINQ 时，你会将其内联编码，如下所述。

### lambda 表达式的基本语法

```
(parameterList) => expression
```

### 一个测试条件的 lambda 表达式

### 在类级别声明委托类型的语句

```
delegate bool compareDel(decimal total);
```

### 定义 lambda 表达式并将其分配给由委托类型创建的变量的语句

```
compareDel invoiceOver150 = total => total > 150;
```

### 执行 lambda 表达式的代码

```
decimal invoiceTotal = 188.46m;
string invoiceMessage = "";
invoiceMessage += "Invoice Total: " + invoiceTotal.ToString("c") +
    "\n" + "Invoice over $150: " +
    invoiceOver150(invoiceTotal);
MessageBox.Show(invoiceMessage, "Invoice Test");
```

### 生成的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_621_0.png)

### 描述

- lambda 表达式由一个未命名的函数组成，该函数计算单个表达式并返回其值。
- lambda 表达式通常作为参数传递给接受委托的方法，该委托指定了方法的签名。许多 LINQ 方法接受委托作为参数，如上所示。有关委托的更多信息，请参阅第 13 章。

### 如何编码基于方法 的查询

要编码基于方法 的查询，你使用 LINQ 扩展方法。例如，图 18-10 顶部表格列出了用于实现常见 C# LINQ 子句的扩展方法。这些扩展方法定义了一个或多个接受 lambda 表达式的参数。像上一图中的 invoiceOver150 变量一样，这些参数代表委托，指定了方法的签名。例如，Where() 方法的第二个参数被定义为接受一个具有两个参数的函数的委托。第一个参数是源元素，第二个参数是布尔表达式。

本图中的第一个示例说明了其工作原理。这里，查询使用了四个扩展方法。此基于方法 的查询等同于你在图 18-6 中看到的查询表达式，该表达式从发票列表创建匿名类型。此查询使用的每个方法都接受一个 lambda 表达式。对于每个 lambda 表达式，参数列表包含一个参数，表示源元素，在本例中为发票。然后，Where() 方法的 lambda 表达式的表达式体是一个布尔表达式，OrderBy() 和 ThenByDescending() 方法的表达式体是一个指定用于排序的字段的表达式，而 Select() 方法的表达式体是一个标识查询应返回的值的对象。

本图中的第二个示例是用于从 Invoice 对象列表和 Customer 对象列表中连接数据的基于方法 的查询。这等同于你在图 18-7 中看到的第二个查询表达式。

为了从两个列表中连接数据，Join() 方法在 Invoice 对象列表上执行。然后，向此方法传递四个参数。第一个参数是要与 Invoice 对象列表连接的 Customer 对象列表。第二个和第三个参数是标识将用于连接对象的 Invoice 和 Customer 对象的字段的 lambda 表达式。在本例中，如果它们的 CustomerID 字段匹配，则 Invoice 对象将与 Customer 对象连接。最后，第四个参数是一个 lambda 表达式，指定要从两个对象中包含的值。请注意，为此工作，lambda 表达式包含两个参数，标识这两个对象。

连接的结果是一个匿名类型，其中包含第四个参数指定的字段。然后，对此匿名类型执行的任何后续扩展方法都会在此基础上执行。在本例中，包括 Where()、OrderBy() 和 ThenByDescending() 方法。请注意，我在这些方法的 lambda 表达式中使用了不同的参数名，以表明它们指的是匿名类型而不是 Customer 或 Invoice 对象。

还请注意，此查询不包含 Select() 方法。这是因为连接创建的匿名类型已包含后续方法所需的所有字段以及要包含在结果中的所有字段。如果你在查询中需要使用额外的字段，但又不想将这些字段包含在结果中，则可以包含一个 Select() 方法，该方法创建一个仅包含你想要的字段的另一个匿名类型。这得到了说明

