

# 使用 C# 进行 SQL Server 数据库编程

```csharp
System.Collections.ArrayList fruits = new System.Collections.ArrayList();
fruits.Add("apple");
fruits.Add("mango");

IEnumerable<string> query = fruits.Cast<string>().Select(fruit => fruit);
foreach (string fruit in query) {
    Console.WriteLine(fruit);
}
```

// 这段代码的运行结果是：

- apple
- mango

图 4.6 cast 操作符示例代码。

单向关系。单向关系的一个示例是 `Customer` 类，它拥有一个类型为 `City` 的属性，而 `City` 类没有作为 `Customer` 对象集合的属性。如果你有一个 `City` 对象列表并想要找到每个城市的所有客户，可以使用连接（join）操作来查找它们。

LINQ 框架提供的方法是 `Join` 和 `GroupJoin`。这些方法执行等值连接，即根据键的相等性匹配两个数据源的连接。在关系数据库术语中，`Join`实现了内连接（inner join），它是连接的一种类型，只返回在另一个数据源中有匹配项的对象。`GroupJoin` 方法在关系数据库术语中没有直接对应项，但它是内连接和外连接的超集。左外连接（Left outer join）是返回第一个（左）数据源每个元素的连接，即使它在另一个数据源中没有关联元素。

图 4.7 显示了使用该操作符的示例。我们需要根据 `faculty_name` 从 `Course` 表中查询所选教职人员的所有课程 (course_id)。问题在于，`Course` 表中没有 `faculty_name` 列，只有 `faculty_id` 与相关的 `course_id` 关联。因此，我们必须首先根据 `faculty_name` 从 `Faculty` 表获取 `faculty_id`，然后从 `Course` 表中查询 `course_id`。这个问题可以通过图 4.7 所示的连接操作符方法得到有效解决。

### 类型（转换目的）
该方法使用延迟执行实现。立即返回的值是一个包含执行该操作所需的所有信息的对象。该方法表示的查询在通过调用 `GetEnumerator` 方法或在 Visual C# 中使用 `foreach` 对对象进行枚举之前是不会执行的。

```csharp
var courseinfo = Courses
    .Join(Faculty, ci => ci.faculty_id, o => o.faculty_id)
    .Where(fi => fi.faculty_name == ComboName.Text)
    .Select(new {
        course_id = ci.course_id
    });
foreach (var cid in courseinfo) {
    CourseList.Items.Add(cid.course_id);
}
```

图 4.7 Join 操作符示例代码。

# 集合集成查询 (LINQ) 简介

```csharp
System.Collections.ArrayList fruits = new System.Collections.ArrayList(2);
fruits.Add("Mango");
fruits.Add("Orange");
// ApplyOfType<T>()
IEnumerable<string> query = fruits.OfType<string>();
Console.WriteLine("Elements of type 'string':");
foreach (string fruit in query)
    Console.WriteLine(fruit);

// 这段代码的运行结果是：
Elements of type 'string':
Mango
Orange
```

图 4.8 OfType 操作符示例代码。

图 4.8 显示了使用该操作符的代码片段。`OfType<T>(IEnumerable)` 方法仅返回源中可以转换为 T 的元素。如果要在元素无法转换为指定类型时接收异常，请使用 `Cast<T>(IEnumerable)`。
该方法是少数几个可以应用于非参数化类型集合（如 `ArrayList`）的标准查询方法之一。这是因为 `OfType<TResult>` 扩展了 `IEnumerable<T>` 类型，不仅可以应用于基于参数化 `IEnumerable<T>` 类型的集合，还可以应用于实现 `IEnumerable` 的集合。
通过对实现 `IEnumerable` 的集合应用 `OfType<TResult>`，你可以获得使用标准查询操作符查询集合的能力。例如，为 `OfType<TResult>` 指定 Object 类型参数将在 C# 中返回一个 `IEnumerable<Object>` 类型的对象，可以对该对象应用标准查询操作符。

### OrderBy（排序目的）
此操作符方法用于根据 `keySelector` 升序排序输入序列中的元素。输出序列将是 `IOrderedEnumerable<T>` 类型的有序序列。`IEnumerable` 和 `IQuery` 类都包含此操作符。图 4.9 显示了使用该操作符的示例。

```csharp
public static void OrderByEx()
{
    Pet[] pets = new Pet[] { new Pet { Name="Barley", Age=8 },
                             new Pet { Name="Boots", Age=4 },
                             new Pet { Name="Whiskers", Age=1 } };
    IEnumerable<Pet> query = pets.OrderBy(pet => pet.Age);
    foreach (var pet in query)
        Console.WriteLine("{0} - {1}", pet.Name, pet.Age);
}

// 这段代码的运行结果是：
Whiskers - 1
Boots - 4
Barley - 8
```

图 4.9 OrderBy 操作符示例代码。

```csharp
IEnumerable<int> squares = Enumerable.Range(1, 5).Select(x => x * x);
foreach (int num in squares)
    Console.WriteLine(num);
```

// 这段代码的运行结果是：

- 1
- 4
- 9
- 16
- 25

# 图 4.10 Select 选择符的示例代码。

# Select（投影目的）

`IEnumerable` 和 `IQueryable` 类都包含此操作符方法。该方法通过延迟执行实现。立即返回的值是一个存储了执行该操作所需的所有信息的对象。该方法表示的查询在直接调用 `GetEnumerator` 方法或在 Visual C# 中使用 `foreach` 执行对象之前是不会执行的。此投影方法通过转换函数选择器（selector），为源序列中的每个值产生一个值。如果选择器返回的值本身是一个集合，则由调用者手动遍历子序列。在这种情况下，让查询返回一个单一合并的值序列可能更好。要实现这一点，请使用 `SelectMany` 方法代替 `Select`。尽管 `SelectMany` 在返回之前的工作原理与 `Select` 类似。在查询语法中，Visual C# 子句中的 `select` 翻译为调用 `Select`。`where` 子句翻译为调用 `Where`。由于图 4.10 显示了使用该操作符的示例代码。

# Where（限制目的）

`IEnumerable` 和 `IQueryable` 类都包含此操作符方法。该方法通过延迟执行实现。立即返回的值是一个存储了执行该操作所需的所有信息的对象。该方法表示的查询在直接调用 `GetEnumerator` 方法或在 Visual C# 中使用 `foreach` 执行对象之前是不会执行的。图 4.11 显示了使用该操作符的示例代码。在查询语法中，Visual C# 子句中的 `where` 翻译为调用 `Where <TSource,IEnumerable<TSource>,Func<TSource,Boolean>>`。

```csharp
List<string> fruits = new List<string>{"apple", "banana", "mango", "orange", "blueberry", "grape", "strawberry" };
IEnumerable<string> query = fruits.Where(fruit => fruit.Length < 6);
foreach (string fruit in query)
    Console.WriteLine(fruit);

// 这段代码的运行结果是：
apple
mango
grape
```

# 图 4.11 Where 操作符的示例代码。

# 语言集成查询 (LINQ) 简介

```csharp
// 创建字符串数组
string[] names = { "Hartono, Tommy", "Adams, Terry", "Andersen, Henriette", "Hedlund, Magnus", "Ito, Shu" };
string name = names.ElementAt(2);
Console.WriteLine("The name chosen is {0}", name);
// 这段代码的运行结果是：
Andersen, Henriette
```

图 4.12 ElementAt 操作符的示例代码。

