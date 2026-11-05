
## 第 66.42 节：带外部范围变量的 GroupJoin

```csharp
Customer[] customers = Customers.ToArray();
Purchase[] purchases = Purchases.ToArray();

var groupJoinQuery =
    from c in customers
    join p in purchases on c.ID equals p.CustomerID
    into custPurchases
    select new
    {
        CustName = c.Name,
        custPurchases
    };
```

## 第 66.43 节：Linq 量化器

量化器操作如果序列中的某些或全部元素满足条件则返回布尔值。在本文中，我们将看到一些可以使用这些运算符的常见 LINQ to Objects 场景。可以在 LINQ 中使用的量化器操作有 3 种：

All – 用于确定序列中的所有元素是否满足条件。例：

```csharp
int[] array = { 10, 20, 30 };

// Are all elements >= 10? YES
array.All(element => element >= 10);

// Are all elements >= 20? NO
array.All(element => element >= 20);

// Are all elements < 40? YES
array.All(element => element < 40);
```

Any - 用于确定序列中是否有任何元素满足条件。例：

```csharp
int[] query = new int[] { 2, 3, 4 };
query.Any(n => n == 3);
```

Contains - 用于确定序列是否包含指定的元素。例：

```csharp
//for int array
int[] query = new int[] { 1,2,3 };
query.Contains(1);

//for string array
string[] query = {"Tom","grey"};
query.Contains("Tom");

//for a string
var stringValue = "hello";
stringValue.Contains("h");
```

## 第 66.44 节：TakeWhile

TakeWhile 只要条件为真就从序列中返回元素

```csharp
int[] list = { 1, 10, 40, 50, 44, 70, 4 };
var result = list.TakeWhile(item => item < 50).ToList();
// result = { 1, 10, 40 }
```

## 第 66.45 节：Reverse

- 反转序列中元素的顺序。
- 如果没有项目则抛出 ArgumentNullException：source 为 null。

示例：

```csharp
// Create an array.
int[] array = { 1, 2, 3, 4 };                //Output:
// Call reverse extension method on the array.   //4
var reverse = array.Reverse();                  //3
// Write contents of array to screen.            //2
foreach (int value in reverse)                  //1
    Console.WriteLine(value);
```

实时代码示例

请记住，Reverse() 的工作方式可能会根据 LINQ 语句的链式顺序而不同。

```csharp
//Create List of chars
List<int> integerlist = new List<int>() { 1, 2, 3, 4, 5, 6 };

//Reversing the list then taking the two first elements
IEnumerable<int> reverseFirst = integerlist.Reverse<int>().Take(2);

//Taking 2 elements and then reversing only those two
IEnumerable<int> reverseLast = integerlist.Take(2).Reverse();

//reverseFirst output: 6, 5
//reverseLast output: 2, 1
```

实时代码示例

Reverse() 通过缓冲所有内容然后向后遍历工作，这不是很高效，从这个角度来看 OrderBy 也是如此。

在 LINQ-to-Objects 中，有缓冲操作（Reverse、OrderBy、GroupBy 等）和非缓冲操作（Where、Take、Skip 等）。

### 示例：非缓冲 Reverse 扩展

```csharp
public static IEnumerable<T> Reverse<T>(this IList<T> list) {
    for (int i = list.Count - 1; i >= 0; i--)
        yield return list[i];
}
```

实时代码示例

如果在迭代时修改列表，此方法可能会遇到问题。

## 第 66.46 节：Count 和 LongCount

Count 返回 IEnumerable<T> 中的元素数量。Count 还公开了一个可选的谓词参数，允许您过滤要计数的元素。

```csharp
int[] array = { 1, 2, 3, 4, 2, 5, 3, 1, 2 };

int n = array.Count(); // returns the number of elements in the array
int x = array.Count(i => i > 2); // returns the number of elements in the array greater than 2
```

LongCount 的工作方式与 Count 相同，但返回类型为 long，用于计数长度超过 int.MaxValue 的 IEnumerable<T> 序列

```csharp
int[] array = GetLargeArray();

long n = array.LongCount(); // returns the number of elements in the array
long x = array.LongCount(i => i > 100); // returns the number of elements in the array greater than 100
```

## 第 66.47 节：增量构建查询

由于 LINQ 使用延迟执行，我们可以拥有一个查询对象，它实际上不包含值，但在求值时返回其值。因此，我们可以根据控制流动态构建查询，并在完成时对其进行求值：

```csharp
IEnumerable<VehicleModel> BuildQuery(int vehicleType, SearchModel search, int start = 1, int count = -1) {
    IEnumerable<VehicleModel> query = _entities.Vehicles
        .Where(x => x.Active && x.Type == vehicleType)
        .Select(x => new VehicleModel {
            Id = v.Id,
            Year = v.Year,
            Class = v.Class,
            Make = v.Make,
            Model = v.Model,
            Cylinders = v.Cylinders ?? 0
        });
}
```

我们可以有条件地应用过滤器：

```csharp
if (!search.Years.Contains("all", StringComparer.OrdinalIgnoreCase))
    query = query.Where(v => search.Years.Contains(v.Year));

if (!search.Makes.Contains("all", StringComparer.OrdinalIgnoreCase)) {
    query = query.Where(v => search.Makes.Contains(v.Make));
}

if (!search.Models.Contains("all", StringComparer.OrdinalIgnoreCase)) {
    query = query.Where(v => search.Models.Contains(v.Model));
}

if (!search.Cylinders.Equals("all", StringComparer.OrdinalIgnoreCase)) {
    decimal minCylinders = 0;
    decimal maxCylinders = 0;
    switch (search.Cylinders) {
        case "2-4":
            maxCylinders = 4;
            break;
```

```csharp
case "5-6":
    minCylinders = 5;
    maxCylinders = 6;
    break;
case "8":
    minCylinders = 8;
    maxCylinders = 8;
    break;
case "10+":
    minCylinders = 10;
    break;
}
if (minCylinders > 0) {
    query = query.Where(v => v.Cylinders >= minCylinders);
}
if (maxCylinders > 0) {
    query = query.Where(v => v.Cylinders <= maxCylinders);
}
}
```

我们可以根据条件为查询添加排序顺序：

```csharp
switch (search.SortingColumn.ToLower()) {
    case "make_model":
        query = query.OrderBy(v => v.Make).ThenBy(v => v.Model);
        break;
    case "year":
        query = query.OrderBy(v => v.Year);
        break;
    case "engine_size":
        query = query.OrderBy(v => v.EngineSize).ThenBy(v => v.Cylinders);
        break;
    default:
        query = query.OrderBy(v => v.Year); //The default sorting.
}
```

我们的查询可以定义为从给定点开始：

```csharp
query = query.Skip(start - 1);
```

并定义为返回特定数量的记录：

```csharp
if (count > -1) {
    query = query.Take(count);
}
return query;
}
```

一旦我们有了查询对象，我们就可以使用 foreach 循环或返回一组值的 LINQ 方法（如 ToList 或 ToArray）来评估结果：

```csharp
SearchModel sm;

// populate the search model here
// ...

List<VehicleModel> list = BuildQuery(5, sm).ToList();
```

## 第 66.48 节：使用 Func<TSource, int, TResult> 选择器进行 Select - 用于获取元素的排名

SELECT 扩展方法的一个重载还传递正在 SELECT 的集合中当前项目的索引。以下是一些用法。

### 获取项目的“行号”

```csharp
var rowNumbers = collection.OrderBy(item => item.Property1)
    .ThenBy(item => item.Property2)
    .ThenByDescending(item => item.Property3)
    .Select((item, index) => new { Item = item, RowNumber = index })
    .ToList();
```

### 获取项目在其组内的排名

```csharp
var rankInGroup = collection.GroupBy(item => item.Property1)
    .OrderBy(group => group.Key)
    .SelectMany(group => group.OrderBy(item => item.Property2)
        .ThenByDescending(item => item.Property3)
        .Select((item, index) => new
        {
            Item = item,
            RankInGroup = index
        })).ToList();
```

### 获取组的排名（在 Oracle 中也称为 dense_rank）

```csharp
var rankOfBelongingGroup = collection.GroupBy(item => item.Property1)
    .OrderBy(group => group.Key)
    .Select((group, index) => new
    {
        Items = group,
        Rank = index
    })
    .SelectMany(v => v.Items, (s, i) => new
    {
        Item = i,
        DenseRank = s.Rank
    }).ToList();
```

用于测试此功能，您可以使用：

```csharp
public class SomeObject
{
    public int Property1 { get; set; }
    public int Property2 { get; set; }
    public int Property3 { get; set; }

    public override string ToString()
    {
        return string.Join(", ", Property1, Property2, Property3);
    }
}
```

以及数据：

```csharp
List<SomeObject> collection = new List<SomeObject>
```
