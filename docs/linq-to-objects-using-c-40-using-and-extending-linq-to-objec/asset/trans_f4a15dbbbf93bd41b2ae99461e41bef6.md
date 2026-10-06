

# 第 3 章 编写基础查询

IEnumerable 原生支持调用者请求集合中的下一个项——此时，将计算下一个项（以 `foreach` 关键字作为示例）。任何实现 `IEnumerable<T>` 模式（它同时也实现了 `IEnumerable`）的集合都将通过 `where` 算符扩展，只要该元素满足谓词表达式（返回 `true`），该算符在被请求时每次将返回一个元素。

过滤谓词表达式通过 Lambda 表达式传递给扩展方法（关于 Lambda 表达式的定义，请参见第 2 章“引言 LINQ to Objects”），尽管查询表达式语法的形式更加整洁。这两种谓词表达式样式都将在后续章节中进行详细的说明和介绍。

# 使用 Lambda 表达式进行 Where Filter

在为 `Where` 算符形成谓词时，谓词接收一个与源集合元素类型相同的输入元素，并返回 `true` 或 `false`（一个布尔值）。为了演示使用简单的 `Where` 谓词，考虑以下代码：

```csharp
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };
```

```csharp
var q = animals.Where(
    a => a.StartsWith("S") && a.Length > 5);

foreach (string s in q)
    Console.WriteLine(s);
```

在此代码中，`animals` 数组中的每个字符串值都通过一个名为 `a` 的范围变量传递给 `Where` 扩展方法。每个字符串都会根据谓词函数进行评估，只有通过测试（返回 `true`）的字符串会被返回到查询结果。对于此示例，只有两个字符串通过了测试并写入控制台窗口。

Spider

Sting-Ray

# 如何过滤结果 (WHERE 子句)

C# 编译器在后台将 Lambda 表达式转换为标准的匿名方法调用（以下代码在功能上等效）：

```csharp
var q = animals.Where(
  delegate(string a) {
    return a.StartsWith("S") && a.Length > 5; });
```

### 什么是延迟执行？
`where` 子句只有在有人（你通过 `foreach` 语句或另一个带有内部 `foreach` 语句的标准查询算符）尝试迭代结果时，才会开始测试谓词；在此之前，迭代器框架会准确记住上一次被请求元素时所在的位置。这被称为延迟执行（Deferred Execution），它允许你对查询何时何时以及如何执行具有某种可预测性和控制力。如果你立即需要结果，可以调用 `List()`、`ToArray()` 或其他导致结果立即具体化为另一种格式的标准算符；否则，查询将会在你开始迭代它时才开始评估。

# Where 过滤查询表达式（首选）

查询表达式的 `where` 子句语法去掉了显式的范围变量定义和 Lambda 表达式算符 (`=>`)，使其变得更加简洁，并且更符合许多开发者熟悉的 SQL 风格子句。由于这些原因，它是首选语法。以下使用查询表达式语法重写之前的示例展示了这些差异：

```csharp
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };
```

```csharp
var q = from a in animals
  where a.StartsWith("S") && a.Length > 5
  select a;
```

```csharp
foreach (string s in q)
  Console.WriteLine(s);
```

# 使用外部方法进行评估

虽然你可以编写查询并内联过滤谓词的代码，但你不必这样做。如果谓词很长并且可能在多个查询表达式中使用，你应该考虑将其放在自己的方法体中（这是任何重复代码的良好实践）。使用外部谓词函数重写之前的示例展示了这种技术：

```csharp
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };

var q = from a in animals
    where MyPredicate(a)
    select a;

foreach (string s in q)
    Console.WriteLine(s);

public bool MyPredicate(string a)
{
    if (a.StartsWith("S") && a.Length > 5)
        return true;
    else
        return false;
};
```

为了通过稍微复杂的场景进一步演示这种技术，列表 3-5 所示的代码创建了一个谓词方法，该方法封装了判断“致命动物”的逻辑。通过将此逻辑封装在一个方法中，它就不需要在应用程序的多个地方重复出现。

# 列表 3-5 使用外部方法的 where 子句——参见输出 3-3

```csharp
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };

var q = from a in animals
    where IsDeadly(a)
    select a;
```

# 如何过滤结果 (WHERE 子句)

```csharp
foreach (string s in q)
    Console.WriteLine("A {0} is deadly.", s);

public static bool IsDeadly(string s)
{
    string[] deadly = new[] { "Spider", "Snake",
    "Shark", "Sting-Ray", "Jellyfish" };
    return deadly.Contains(s);
}
```

# 输出 3-3
A Spider 是致命的。
A Snake 是致命的。
A Shark 是致命的。
A Sting-Ray 是致命的。
A Jellyfish 是致命的。

# 根据索引过滤

`where` 子句允许你根据集合中的索引来过滤元素。当你需要选择特定位置的元素时，这非常有用。

```csharp
string[] animals = new[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };

var q = animals.Select((a, index) => new { a, index })
               .Where(x => x.index % 2 == 0);

foreach (var item in q)
    Console.WriteLine(item.a);
```

# 输出 3-4
```

# 如何返回类型 (Select 投影)

当你对数据库编写查询时，指定要返回的列是本能。目标是将列限制在必要的范围内。这通过在 `Select` 子句后列出列来实现：

```sql
SELECT * FROM Contacts
```

```sql
SELECT ContactId, FirstName, LastName FROM Contacts
```

第一个查询将返回表的每一列和每一行；第二个查询只返回显式指定的列，从而节省了服务器资源。

# Select 投影

投影返回结果的不同方式有：

- 单个结果值或元素，其类型与源项相同
- `IEnumerable<T>`，其中 T 是投影中的任何现有类型
- `IEnumerable<T>`，其中 T 是投影中创建的匿名类型
- `IEnumerable<IGrouping<TKey, TElement>>`，它是共享公共键对象的集合

每种投影样式都有其用途，并在后续章节通过示例进行说明。

# 在 Select 投影中投影了多少数据？与所有良好的数据访问范式一样，定义查询形状时的目标应该是返回尽可能少的属性。这减少了内存占用，并使结果集更容易编码，因为需要处理的属性更少。

# 返回单个结果或元素

某些标准查询算符返回单个值作为结果，或者集合中的单个元素；这些算符列在表 3-1 中。每个这些算符都会结束结果到另一个查询的级联，而是返回单个结果值或源元素。

表 3-1 返回特定结果类型的算符示例（在第 5 和第 6 章介绍）

| 返回类型 | 标准查询算符 |
|---|---|
| 数值 | Aggregate, Average, Max, Min, Sum, Count, LongCount |
| 布尔值 | All, Any, Contains, SequenceEqual |
| 类型 <T> | ElementAt, ElementOrDefault, First, FirstOrDefault, Last, LastOrDefault, Single, SingleOrDefault, DefaultIfEmpty |

