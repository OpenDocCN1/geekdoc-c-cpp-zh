
## 36

## LINQ to Objects

第 34 课和第 35 课讲解了如何使用 Visual Studio 的向导构建简单的数据库程序。它们展示了将程序连接到数据源的众多方法之一。

*语言集成查询*（LINQ）提供了另一种弥合程序与数据之间鸿沟的方法。然而，LINQ 并非只是提供另一种访问数据库中数据的方式；它还能帮助程序访问存储在许多位置的数据。LINQ 让程序可以使用相同的技术来访问存储在数据库、数组、集合或文件中的数据。

LINQ 提供了四种基本技术，让你可以访问存储在各种位置的数据：

- LINQ to SQL——数据存储在 SQL Server 数据库中
- LINQ to Dataset——数据存储在其他数据库中
- LINQ to XML——数据存储在 XML（可扩展标记语言）文件中
- LINQ to Objects——数据存储在集合、列表、数组、字符串、文件等中

本课中，你将学习如何使用 LINQ to Objects。你将学习如何从列表、集合和数组中提取数据，以及如何处理结果。

### LINQ 基础

使用 LINQ 处理数据需要三个步骤：

- 1. 创建数据源。
- 2. 构建一个 LINQ 查询，从数据源中选择数据。
- 3. 执行查询并处理结果。

你可能以为第三步是两个独立的步骤：“执行查询”和“处理结果”。然而，在实践中，LINQ 实际上直到必须执行时才会执行查询——也就是当程序尝试访问结果时。这称为*延迟执行*。

例如，以下代码显示 0 到 99 之间的偶数：

```csharp
    // Display the even numbers between 0 and 99.
    private void Form1_Load(object sender, EventArgs e)
    {
        // 1. Create the data source.
        int[] numbers = new int[100];
        for (int i = 0; i < 100; i++) numbers[i] = i;

        // 2. Build a query to select data from the data source.
        var evenQuery =
            from int num in numbers
            where (num % 2 == 0)
            select num;

        // 3. Execute the query and process the result.
        foreach (int num in evenQuery) Console.WriteLine(num.ToString());
    }
```

程序首先创建数据源：一个包含数字 0 到 99 的数组。在这个示例中，数据源相当简单，但在其他程序中，它可能复杂得多。它可能不是数字数组，而是 Customer 对象列表，或者包含 OrderItem 对象列表的 Order 对象数组。

接下来，程序构建一个查询，从列表中选择偶数。我稍后会详细解释查询，但下面的列表描述了此查询的关键部分：

- var——这是查询返回的任何内容的数据类型。在此示例中，结果将是 IEnumerable<int>，但一般来说，LINQ 查询的结果可能具有一些非常奇怪的数据类型。大多数开发者不会试图弄清楚查询将返回什么，而是使用隐式数据类型 var。var 关键字告诉 C# 编译器推断数据类型并使用该类型，这样你就不需要使用特定的数据类型。
- evenQuery——这是代码给查询起的名称。你可以把它看作一个变量，表示 LINQ 稍后将产生的结果。
- from int num in numbers——这意味着查询将从 numbers 数组中选择数据。它将使用 int 变量 num 遍历数组中的值。因为 num 遍历这些值，所以它被称为查询的范围变量。（如果省略 int 数据类型，编译器将隐式推断其数据类型。）
- where (num % 2 == 0)——这是查询的 where 子句。它确定从数组中选择哪些项。此示例选择偶数（其中 num 模 2 为 0）。
- select num——这告诉查询要返回什么。在此例中，查询返回所选值对应的范围变量 num 中的内容。通常你会希望返回范围变量的值，但也可以返回其他内容，例如 2 * num，或使用以 num 作为参数的构造函数创建的新对象。

> 注意：如果你能确定更具体的数据类型，我通常不建议对变量使用 var。当你使用 var 时，你无法确定编译器会使用什么数据类型。如果编译器为之后必须协同工作的变量选择了不同的数据类型，这可能会导致混乱。
> 
> 例如，在以下代码中，第三条语句是允许的，因为你可以将 int 值存储到 double 中，但第四条语句不允许，因为 double 可能无法放入 int 中：
> 
> ```
> var x = 1.2;    // double.
> var y = 1;      // int.
> x = y;          // Allowed.
> y = x;          // Not allowed.
> ```
> 
> 如果你确实知道数据类型，就直接使用它，而不要用 var。

在执行查询的最后一步中，代码会遍历 LINQ 产生的结果。代码在控制台窗口中显示每个 int 值。只有当程序尝试迭代查询结果时，查询才会实际执行。

以下各节更详细地描述 LINQ 查询的一些关键部分：where 子句、order by 子句和 select 子句。

### WHERE 子句

使用 LINQ 最常见的原因可能是用 where 子句筛选数据。where 子句可以包含使用 &&、||、> 和其他布尔运算符的常规布尔表达式。它可以使用范围变量及其提供的任何属性或方法（如果它是对象）。它甚至可以执行计算并调用函数。

> 注意：where 子句是可选的。如果省略它，查询将选择其范围内的所有项。

例如，以下查询与前面选择偶数的查询类似，只是这个查询的 where 子句使用 IsPrime 方法仅选择质数。（IsPrime 函数如何工作对本次讨论并不重要，因此这里没有展示。你可以在本课下载的 Find Primes 程序中看到它。）

```
var primeQuery =
    from int num in numbers
    where IsPrime(num)
    select num;
```

图 36-1 所示的 Find Customers 示例程序（也可在本课网站上的代码下载中获得）演示了多个 where 子句。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_541_0.png)

图 36-1

以下代码显示了 Find Customers 程序使用的 Customer 类。它包括一些自动实现的属性，以及一个重写的 ToString 方法，用于显示 Customer 的值：

```
class Customer
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public decimal Balance { get; set; }
    public DateTime DueDate { get; set; }

    public override string ToString()
    {
        return FirstName + " " + LastName + "\t" +
            Balance.ToString("C") + "\t" + DueDate.ToString("d");
    }
}
```

以下代码显示了 Find Customers 程序如何显示使用不同 where 子句选择的相同客户数据：

```csharp
// Display customers selected in various ways.
private void Form1_Load(object sender, EventArgs e)
{
    DateTime today = new DateTime(2020, 4, 1);
    //DateTime today = DateTime.Today;
    this.Text = "Find Customers (" + today.ToString("d") + ")";

    // Make the customers.
    Customer[] customers =
    {
        new Customer() { FirstName="Ann", LastName="Ashler",
            Balance = 100, DueDate = new DateTime(2020, 3, 10) },
        new Customer() { FirstName="Bob", LastName="Boggart",
            Balance = 150, DueDate = new DateTime(2020, 2, 5) },
        // ... Other Customers omitted ...
    };

    // Display all customers.
    allListBox.DataSource = customers;

    // Display customers with negative balances.
    var negativeQuery =
        from Customer cust in customers
        where cust.Balance < 0
        select cust;
    negativeListBox.DataSource = negativeQuery.ToArray();

    // Display customers who owe at least $50.
    var owes50Query =
        from Customer cust in customers
        where cust.Balance <= -50
        select cust;
    owes50ListBox.DataSource = owes50Query.ToArray();

    // Display customers who owe at least $50
    // and are overdue at least 30 days.
    var overdueQuery =
        from Customer cust in customers
        where (cust.Balance <= -50) &&
              (DateTime.Now.Subtract(cust.DueDate).TotalDays > 30)
        select cust;
    overdueListBox.DataSource = overdueQuery.ToArray();
}
```

程序首先创建一个名为 today 的 DateTime，并将其设置为 2020 年 4 月 1 日。在真实应用程序中，你可能会使用当前日期（已注释掉），但此程序使用那个特定日期，以便与示例数据良好配合。然后，程序在其标题栏中显示该日期（以便你可以将其与 Customers 的到期日期进行比较），并创建一个 Customer 对象数组。

接下来，代码将 allListBox 控件的 DataSource 属性设置为该数组，以便 ListBox 显示所有 Customer 对象。Customer 类重写的 ToString 方法使其显示每个 Customer 的姓名、余额和到期日期。

然后，程序执行以下 LINQ 查询：

```
// Display customers with negative balances.
var negativeQuery =
    from Customer cust in customers
    where cust.Balance < 0
    select cust;
negativeListBox.DataSource = negativeQuery.ToArray();
```

此查询的 where 子句选择 Balance 属性小于 0 的 Customers。该查询返回一个 IEnumerable，但 ListBox 的 DataSource 属性要求 IList 或 IListSource，并且
