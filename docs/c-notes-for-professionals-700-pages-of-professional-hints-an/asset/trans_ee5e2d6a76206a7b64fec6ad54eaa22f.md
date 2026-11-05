
```
var result = list.SkipWhile(i => i == 42);
// Result: 6, 6, 6, 42
```

## Section 66.27: 查询排序 - OrderBy() ThenBy() OrderByDescending() ThenByDescending()

```
string[] names = { "mark", "steve", "adam" };
```

### 升序：

查询语法

```
var sortedNames =
    from name in names
    orderby name
    select name;
```

方法语法

```
var sortedNames = names.OrderBy(name => name);
```

sortedNames 包含名称的顺序如下："adam","mark","steve"

### 降序：

查询语法

```
var sortedNames =
    from name in names
    orderby name descending
    select name;
```

方法语法

```
var sortedNames = names.OrderByDescending(name => name);
```

sortedNames 包含名称的顺序如下："steve","mark","adam"

### 按多个字段排序

```
Person[] people =
{
    new Person { FirstName = "Steve", LastName = "Collins", Age = 30 },
    new Person { FirstName = "Phil", LastName = "Collins", Age = 28 },
    new Person { FirstName = "Adam", LastName = "Ackerman", Age = 29 },
    new Person { FirstName = "Adam", LastName = "Ackerman", Age = 15 }
};
```

查询语法

```
var sortedPeople = from person in people
    orderby person.LastName, person.FirstName, person.Age descending
    select person;
```

方法语法

```
sortedPeople = people.OrderBy(person => person.LastName)
    .ThenBy(person => person.FirstName)
    .ThenByDescending(person => person.Age);
```

结果

- 1. Adam Ackerman 29
- 2. Adam Ackerman 15
- 3. Phil Collins 28
- 4. Steve Collins 30

## Section 66.28: 求和

Enumerable.Sum 扩展方法计算数值的总和。

如果集合的元素本身就是数字，可以直接计算总和。

```
int[] numbers = new int[] { 1, 4, 6 };
Console.WriteLine( numbers.Sum() ); //outputs 11
```

如果元素的类型是复杂类型，可以使用 lambda 表达式指定应计算的值：

```
var totalMonthlySalary = employees.Sum( employee => employee.MonthlySalary );
```

Sum 扩展方法可以处理以下类型：

- Int32
- Int64
- Single
- Double
- Decimal

如果集合包含可空类型，可以使用空合并运算符为 null 元素设置默认值：

```
int?[] numbers = new int?[] { 1, null, 6 };
Console.WriteLine( numbers.Sum( number => number ?? 0 ) ); //outputs 7
```

## Section 66.29: 按一个或多个字段分组

假设我们有一个 Film 模型：

```
public class Film {
    public string Title { get; set; }
    public string Category { get; set; }
    public int Year { get; set; }
}
```

按 Category 属性分组：

```
foreach (var grp in films.GroupBy(f => f.Category)) {
    var groupCategory = grp.Key;
    var numberOfFilmsInCategory = grp.Count();
}
```

按 Category 和 Year 分组：

```
foreach (var grp in films.GroupBy(f => new { Category = f.Category, Year = f.Year })) {
    var groupCategory = grp.Key.Category;
    var groupYear = grp.Key.Year;
    var numberOfFilmsInCategory = grp.Count();
}
```

## Section 66.30: OrderBy

> 按指定值对集合排序。

当值为 integer、double 或 float 时，从最小值开始，这意味着首先得到负值，然后是零，最后是正值（参见示例 1）。

当按 char 排序时，该方法比较字符的 ASCII 值以对集合排序（参见示例 2）。

当对字符串排序时，OrderBy 方法通过查看其 CultureInfo 进行比较，但通常从字母表的第一个字母开始（a,b,c...）。

这种排序称为升序，如果想要相反的顺序则需要降序（参见 OrderByDescending）。

### 示例 1：

```
int[] numbers = {2, 1, 0, -1, -2};
IEnumerable<int> ascending = numbers.OrderBy(x => x);
// returns {-2, -1, 0, 1, 2}
```

### 示例 2：

```
char[] letters = {' ', '!', '?', '[', '{', '*', '1', '9', 'a', 'A', 'b', 'B', 'y', 'Y', 'z', 'Z'};
IEnumerable<char> ascending = letters.OrderBy(x => x);
// returns { ' ', '!', '*', '1', '9', '?', 'A', 'B', 'Y', 'Z', '[', 'a', 'b', 'y', 'z', '{' }
```

### 示例：

```
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

var people = new[]
{
    new Person {Name = "Alice", Age = 25},
    new Person {Name = "Bob", Age = 21},
    new Person {Name = "Carol", Age = 43}
};
var youngestPerson = people.OrderBy(x => x.Age).First();
var name = youngestPerson.Name; // Bob
```

## Section 66.31: Any 和 First(OrDefault) - 最佳实践

我不会解释 Any 和 FirstOrDefault 的作用，因为已经有两个很好的示例。有关更多信息，请参阅 Any 和 First、FirstOrDefault、Last、LastOrDefault、Single、和 SingleOrDefault。

我经常在代码中看到应避免的模式

```
if (myEnumerable.Any(t=>t.Foo == "Bob"))
{
    var myFoo = myEnumerable.First(t=>t.Foo == "Bob");
    //Do stuff
}
```

可以更高效地写成这样

```
var myFoo = myEnumerable.FirstOrDefault(t=>t.Foo == "Bob");
if (myFoo != null)
{
    //Do stuff
}
```

使用第二个示例，集合只需搜索一次，结果与第一个相同。相同的思路也可以应用于 Single。

## Section 66.32: GroupBy 求和与计数

让我们取一个示例类：

```
public class Transaction
{
    public string Category { get; set; }
    public DateTime Date { get; set; }
    public decimal Amount { get; set; }
}
```

现在，让我们考虑一个交易列表：

```
var transactions = new List<Transaction>
{
    new Transaction { Category = "Saving Account", Amount = 56, Date = DateTime.Today.AddDays(1) },
    new Transaction { Category = "Saving Account", Amount = 16, Date = DateTime.Today.AddDays(-10) },
    new Transaction { Category = "Credit Card", Amount = 15, Date = DateTime.Today.AddDays(1) },
    new Transaction { Category = "Credit Card", Amount = 56, Date = DateTime.Today },
    new Transaction { Category = "Current Account", Amount = 100, Date = DateTime.Today.AddDays(5) },
};
```

如果要按类别计算金额总和和计数，可以按如下方式使用 GroupBy：

```
var summaryApproach1 = transactions.GroupBy(t => t.Category)
    .Select(t => new
    {
        Category = t.Key,
        Count = t.Count(),
        Amount = t.Sum(ta => ta.Amount),
    }).ToList();
```

```csharp
Console.WriteLine("-- Summary: Approach 1 --");
summaryApproach1.ForEach(
    row => Console.WriteLine($"Category: {row.Category}, Amount: {row.Amount}, Count: {row.Count}"));
```

或者，你可以一步完成：

```csharp
var summaryApproach2 = transactions.GroupBy(t => t.Category, (key, t) =>
{
    var transactionArray = t as Transaction[] ?? t.ToArray();
    return new
    {
        Category = key,
        Count = transactionArray.Length,
        Amount = transactionArray.Sum(ta => ta.Amount),
    };
}).ToList();

Console.WriteLine("-- Summary: Approach 2 --");
summaryApproach2.ForEach(
    row => Console.WriteLine($"Category: {row.Category}, Amount: {row.Amount}, Count: {row.Count}"));
```

上述两个查询的输出结果相同：

> Category: Saving Account, Amount: 66, Count: 2
>
> Category: Credit Card, Amount: 71, Count: 2
>
> Category: Current Account, Amount: 100, Count: 1

[在 .NET Fiddle 中在线演示](https://dotnetfiddle.net/)

## Section 66.33: SequenceEqual

SequenceEqual 用于比较两个 IEnumerable<T> 序列。

```csharp
int[] a = new int[] { 1, 2, 3 };
int[] b = new int[] { 1, 2, 3 };
int[] c = new int[] { 1, 3, 2 };

bool returnsTrue = a.SequenceEqual(b);
bool returnsFalse = a.SequenceEqual(c);
```

## Section 66.34: ElementAt 和 ElementAtOrDefault

ElementAt 将返回索引 n 处的项。如果 n 不在可枚举对象的范围内，则抛出 ArgumentOutOfRangeException。

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
numbers.ElementAt(2); // 3
numbers.ElementAt(10); // throws ArgumentOutOfRangeException
```

ElementAtOrDefault 将返回索引 n 处的项。如果 n 不在可枚举对象的范围内，则返回 default(T)。
