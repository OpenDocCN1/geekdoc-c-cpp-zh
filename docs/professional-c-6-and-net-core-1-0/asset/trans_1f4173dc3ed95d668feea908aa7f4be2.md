
利用共享状态，并且仅在必要时复制集合。

不过，更高效的做法是先把集合填满，再将其变成不可变数组。当需要进行某些操作时，可以再次使用可变集合。不可变类型提供的 Builder 类可以帮助实现这一点。

为了实际演示这一点，首先创建一个放入集合的 Account 类。该类型本身是不可变的，并且由于使用了只读自动属性而无法被修改（代码文件 ImmutableCollectionSample/Account.cs）：

```
public class Account
{
    public Account(string name, decimal amount)
    {
        Name = name;
        Amount = amount;
    }
    public string Name { get; }
    public decimal Amount { get; }
}
```

接下来，创建一个 List<Account> 集合并用示例账户填充（代码文件 ImmutableCollectionSample/Program.cs）：

```
var accounts = new List<Account>()
{
    new Account("Scrooge McDuck", 667377678765m),
    new Account("Donald Duck", -200m),
    new Account("Ludwig von Drake", 20000m)
};
```

通过 ToImmutableList 扩展方法，可以从 accounts 集合创建不可变集合。只要打开 System.Collections.Immutable 命名空间，即可使用该扩展方法。

```
ImmutableList<Account> immutableAccounts =
accounts.ToImmutableList();
```

变量 immutableAccounts 可以像其他集合一样被枚举，只是不能修改：

```
foreach (var account in immutableAccounts)
{
    WriteLine($"{account.Name} {account.Amount}");
}
```

除了使用 foreach 语句来迭代不可变列表，你还可以使用 ImmutableList<T> 定义的 ForEach 方法。该方法要求一个 Action<T> 委托作为参数，因此可以传入 lambda 表达式：

```
immutableAccounts.ForEach(a => WriteLine($"{a.Name} {a.Amount}"));
```

使用这些集合时，可以使用 Contains、FindAll、FindLast、IndexOf 等方法。由于这些方法类似于第 11 章讨论的其他集合类中的方法，这里不再明确展示。

如果需要修改不可变集合的内容，集合提供了 Add、AddRange、Remove、RemoveAt、RemoveRange、Replace 和 Sort 等方法。这些方法与普通集合类的方法有很大不同：用于调用这些方法的不可变集合永远不会被修改，而是返回一个新的不可变集合。

## 在不可变集合中使用 Builder

使用前面提到的 Add、Remove 和 Replace 方法，可以轻松地从现有集合创建新的不可变集合。但如果需要执行多次更改（例如为新集合添加和移除元素），这种做法效率并不高。为了通过更多更改来创建新的不可变集合，可以创建一个 Builder。

让我们继续使用示例代码，对集合中的 account 对象进行多项更改。为此，可以通过调用 ToBuilder 方法创建一个 Builder。该方法返回一个你可以更改的集合。在示例代码中，所有金额大于 0 的账户都会被移除。原始的不可变集合不会被修改。使用 Builder 完成更改后，通过调用 Builder 的 ToImmutable 方法创建新的不可变集合。接下来，该集合用于输出所有透支账户：

```
ImmutableList<Account>.Builder builder =
immutableAccounts.ToBuilder();
for (int i = 0; i < builder.Count; i++)
{
    Account a = builder[i];
    if (a.Amount > 0)
    {
        builder.Remove(a);
    }
}

ImmutableList<Account> overdrawnAccounts =
builder.ToImmutable();

overdrawnAccounts.ForEach(a => WriteLine($"{a.Name} {a.Amount}"));
```

除了使用 Remove 方法移除元素外，Builder 类型还提供了 Add、AddRange、Insert、RemoveAt、RemoveAll、Reverse 和 Sort 等方法来修改可变集合。完成可变操作后，调用 ToImmutable 再次获取不可变集合。

## 不可变集合类型与接口

除了 ImmutableArray 和 ImmutableList 之外，NuGet 包 System.Collections.Immutable 还提供了更多不可变集合类型，如下表所示：

| 不可变类型 | 描述 |
| --- | --- |
| `ImmutableArray<T>` | `ImmutableArray<T>` 是一个结构，内部使用数组类型，但不允许更改底层类型。该结构实现了 `IImmutableList<T>` 接口。 |
| `ImmutableList<T>` | `ImmutableList<T>` 在内部使用二叉树来映射对象，并实现 `IImmutableList<T>` 接口。 |
| `ImmutableQueue<T>` | `ImmutableQueue<T>` 实现 `IImmutableQueue<T>` 接口，该接口允许通过 Enqueue、Dequeue 和 Peek 以先进先出的方式访问元素。 |
| `ImmutableStack<T>` | `ImmutableStack<T>` 实现 `IImmutableStack<T>` 接口，该接口允许通过 Push、Pop 和 Peek 以先进后出的方式访问元素。 |
| `ImmutableDictionary<TKey, TValue>` | `ImmutableDictionary<TKey, TValue>` 是一个不可变集合，包含无序的键/值对元素，实现 `IImmutableDictionary<TKey, TValue>` 接口。 |
| `ImmutableSortedDictionary<TKey, TValue>` | `ImmutableSortedDictionary<TKey, TValue>` 是一个不可变集合，包含有序的键/值对元素，实现 `IImmutableDictionary<TKey, TValue>` 接口。 |
| `ImmutableHashSet<T>` | `ImmutableHashSet<T>` 是一个不可变的无序哈希集，实现 `IImmutableSet<T>` 接口。该接口提供第 11 章中介绍的集合功能。 |
| `ImmutableSortedSet<T>` | `ImmutableSortedSet<T>` 是一个不可变的有序集合，实现 `IImmutableSet<T>` 接口。 |

与普通集合类一样，不可变集合也实现接口——例如 `IImmutableList<T>`、`IImmutableQueue<T>` 和 `IImmutableStack<T>`。这些不可变接口的最大区别在于，所有对集合进行更改的方法都会返回一个新集合。

## 在不可变数组中使用 LINQ

要在不可变数组中使用 LINQ，`ImmutableArrayExtensions` 类为 LINQ 方法（如 `Where`、`Aggregate`、`All`、`First`、`Last`、`Select` 和 `SelectMany`）定义了优化版本。你只需直接使用 `ImmutableArray` 类型并打开 `System.Linq` 命名空间，即可使用这些优化版本。

`ImmutableArrayExtensions` 类型定义的 `Where` 方法如下所示，用于扩展 `ImmutableArray<T>` 类型：

```
public static IEnumerable<T> Where<T>(
    this ImmutableArray<T> immutableArray, Func<T, bool> predicate);
```

普通的 LINQ 扩展方法扩展的是 `IEnumerable<T>`。由于 `ImmutableArray<T>` 是更好的匹配项，因此在调用 LINQ 方法时会使用优化版本。

> 注意：LINQ 将在第 13 章“语言集成查询”中详细讲解。

## 并发集合

不可变集合可以轻松地在多线程中使用，因为它们无法被修改。如果你希望使用可由多个线程修改的集合，.NET 在 `System.Collections.Concurrent` 命名空间中提供了线程安全的集合类。线程安全集合能够防止多个线程以冲突方式访问它们。

为实现集合的线程安全访问，定义了 `IProducerConsumerCollection<T>` 接口。该接口最重要的方法是 `TryAdd` 和 `TryTake`。`TryAdd` 尝试向集合添加项，但如果集合被锁定，无法添加项，则可能失败。为了提供此信息，该方法返回一个布尔值，指示成功或失败。`TryTake` 以相同方式告知调用者成功或失败，并在成功时从集合返回一个项。以下列表描述了 `System.Collections.Concurrent` 命名空间中的集合类及其功能：

- `ConcurrentQueue<T>` — 此类使用无锁算法实现，并使用多个 32 项数组，这些数组以链表形式组合在一起。
