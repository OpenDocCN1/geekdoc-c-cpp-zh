

## 查询操作的三个阶段

1. 获取数据源。如果数据源是一个数组，例如，你必须声明数组然后为其元素赋值。
2. 定义查询。
3. 执行查询以返回结果。

## 一个从数组检索数据的 LINQ 查询

### 定义数组的代码

```
int[] numbers = new int[6];
for (int i = 0; i < numbers.Length; i++)
    numbers[i] = i;
```

### 定义查询表达式的语句

```
var numberList = from number in numbers
    where number % 2 == 0
    orderby number descending
    select number;
```

### 执行查询的代码

```
string numberDisplay = "";
foreach (var number in numberList)
    numberDisplay += number + "\t\t\n";
MessageBox.Show(numberDisplay, "Sorted Even Numbers");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_607_0.png)

### 描述

- 上述描述的过程称为 *延迟执行*，因为查询在定义时不会被执行。相反，它在应用程序尝试访问查询返回的各个元素时才被执行，例如当查询在 foreach 语句中使用时。
- 如果查询在定义时未被执行，它会被存储在一个 *查询变量* 中。在这种情况下，查询变量被隐式键入为 `IEnumerable<T>`，其中 `T` 是每个元素的类型。在上面的示例中，`numberList` 变量被赋予类型 `IEnumerable<int>`，因为 `numbers` 数组包含整数。
- 如果查询需要访问查询表达式所标识的各个元素，则会发生 *立即执行*。在这种情况下，查询表达式不会保存在查询变量中。

## 如何编写查询表达式

现在你对 LINQ 查询是什么有了基本了解，你需要学习编写查询表达式的语法。这就是你在接下来的主题中将要学习的内容。

### 如何标识查询的数据源

要标识查询的数据源，你使用图 18-3 中所示的 from 子句。如你所见，此子句声明了一个范围变量，用于表示数据源的每个元素，并命名数据源，该数据源必须是实现 `IEnumerable` 或 `IEnumerable<T>` 接口的集合。它还可以为范围变量声明一个类型，尽管类型通常被省略。如果省略，则由数据源中元素的类型决定。

本图中的第一个示例展示了如何使用 from 子句与名为 `salesTotals` 的十进制数数组。在此示例中，第一条语句声明数组并为其元素赋值。然后，第二条语句定义查询表达式，该表达式仅由 from 子句和 select 子句组成。此表达式存储在名为 `salesList` 的查询变量中。最后，foreach 语句遍历查询返回的值并计算这些值的总和。

到目前为止，你应该意识到查询表达式必须始终以标识数据源的 from 子句开头。这样，C# 就知道查询的数据源是什么，并且可以根据该数据源帮助你构建查询的其余部分。此外，查询表达式必须以 select 子句或 group 子句结束。在本图中的示例中，select 子句只是表示应由查询返回数组元素。然而，在本章后面，你会看到你可以使用 select 子句仅从数据源的每个元素中返回你想要的字段。

本图中的第二个示例展示了如何使用 from 子句与发票的泛型列表。这里，你可以看到 Invoice 类由一组自动实现的属性组成。然后，随后的语句创建基于此类的列表，并使用 `InvoiceDB` 类的 `GetInvoices()` 方法将发票加载到其中。请注意，了解此方法的工作原理对你来说并不重要。你只需要知道它返回一个 `List<Invoice>` 对象。此对象随后被赋给名为 `invoiceList` 的变量。

下一条语句定义查询表达式，其中包括一个 from 子句，将 `invoiceList` 标识为数据源。此表达式被赋给名为 `invoices` 的查询变量。然后，此变量在 foreach 语句中使用以计算发票中 `InvoiceTotal` 字段的总和。

你可能已经注意到在本图中的两个示例中，查询表达式中使用的变量和 foreach 循环中使用的变量具有相同的名称。这是有意义的，因为它们都引用数据源中的一个元素。然而，你应该知道你不必为这些变量使用相同的名称。事实上，当你编写更复杂的查询表达式时，你会希望使用不同的变量名来表示它们所引用的元素的差异。当你在本章后面看到 select 子句时，这将更有意义。

### from 子句的语法

```
from [type] elementName in collectionName
```

### 使用十进制数数组的示例

获取数据源的语句

```
decimal[] salesTotals = new decimal[4] {1286.45m, 2433.49m, 2893.85m, 2094.53m};
```

定义查询表达式的语句

```
var salesList = from sales in salesTotals select sales;
```

执行查询的代码

```
decimal sum = 0;
foreach (var sales in salesList)
    sum += sales;
```

### 使用泛型发票列表作为数据源的示例

Invoice 类

```
public class Invoice
{
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

```
List<Invoice> invoiceList = InvoiceDB.GetInvoices();
```

定义查询表达式的语句

```
var invoices = from invoice in invoiceList select invoice;
```

执行查询的代码

```
decimal sum = 0;
foreach (var invoice in invoices)
    sum += invoice.InvoiceTotal;
```

### 描述

- from 子句标识查询的数据源并声明一个范围变量，该变量用于表示数据源的每个元素。
- 如果你在查询表达式中使用的范围变量和在执行查询的 foreach 语句中使用的迭代变量引用相同类型的元素，你应为它们赋予相同的名称以提高清晰度。否则，你应为它们赋予不同的名称以表示它们所引用的元素的类型。
- from 子句必须是查询表达式中的第一个子句。此外，查询表达式必须以 select 子句或 group 子句结束。

## 如何过滤查询结果

要过滤查询结果，你使用图 18-4 中所示的 where 子句。在此子句中，你指定元素必须满足的条件才能由查询返回。条件被编码为你在第 5 章中学到的布尔表达式。本图中的两个示例说明了其工作原理。

第一个示例中的 where 子句指定为了从 `salesTotals` 数组返回一个元素，其值必须大于 2000。请注意，这里 from 子句声明的范围变量在 where 子句中用于引用查询返回的元素。然后，执行查询的代码将返回的值添加到一个字符串中，然后该字符串在消息框中显示。如果你将此消息框中列出的值与图 18-3 中显示的数组中的值进行比较，你会看到小于 2000 的值已被省略。

第二个示例类似，但它使用了发票的泛型列表。这里，where 子句表示只有发票总额大于 150 的发票才应由查询返回。请再次注意，from 子句声明的范围变量用于引用查询返回的元素。这次，因为每个元素都是一个 Invoice 对象，where 子句上的条件可以引用该对象的成员。

