
## 第 119.5 节：使用 Object 实例进行锁定

使用 C# 内置的 lock 语句时需要某个类型的实例，但其状态无关紧要。object 的实例对此非常合适：

```csharp
public class ThreadSafe {
    private static readonly object locker = new object();

    public void SomeThreadSafeMethod() {
        lock (locker) {
            // Only one thread can be here at a time.
        }
    }
}
```

NB. 不应为此使用 Type 的实例（代码中如上 typeof(ThreadSafe)），因为 Type 的实例在 AppDomains 之间共享，因此锁的范围可能会意外包含不应该包含的代码（例如，如果 ThreadSafe 在同一进程中的两个 AppDomains 中加载，则对其 Type 实例的锁定会相互锁定）。

## 第 120 章：yield 关键字

当你在语句中使用 yield 关键字时，表示出现它的 方法、运算符 或 get 访问器 是一个迭代器。使用 yield 定义迭代器时，在为自定义集合类型实现 IEnumerable 和 IEnumerator 模式时，就无需显式额外的类（保存枚举状态的类）。

### 第 120.1 节：简单用法

yield 关键字用于定义一个返回 IEnumerable 或 IEnumerator（以及它们的派生泛型变体）的函数，其值会在调用方遍历返回的集合时按需延迟生成。有关其用途的更多信息，请阅读 remarks 部分。

以下示例中的 yield return 语句位于 for 循环内部。

```csharp
public static IEnumerable<int> Count(int start, int count)
{
    for (int i = 0; i <= count; i++)
    {
        yield return start + i;
    }
}
```

然后你可以这样调用它：

```csharp
foreach (int value in Count(start: 4, count: 10))
{
    Console.WriteLine(value);
}
```

### 控制台输出

```
4
5
6
...
14
```

在 .NET Fiddle 上的实时演示

foreach 语句体的每次迭代都会对 Count 迭代器函数进行一次调用。每次对迭代器函数的调用都会继续执行下一个 yield return 语句，而该语句会在 for 循环的下一次迭代期间执行。

### 第 120.2 节：正确检查参数

迭代器方法要到返回值被枚举时才会被执行。因此，在迭代器外部断言前置条件是有利的。

```csharp
public static IEnumerable<int> Count(int start, int count)
{
    // The exception will throw when the method is called, not when the result is iterated
    if (count < 0)
        throw new ArgumentOutOfRangeException(nameof(count));
    return CountCore(start, count);
}
private static IEnumerable<int> CountCore(int start, int count)
{
    // If the exception was thrown here it would be raised during the first MoveNext()
    // call on the IEnumerator, potentially at a point in the code far away from where
    // an incorrect value was passed.
    for (int i = 0; i < count; i++)
    {
        yield return start + i;
    }
}
```

### 调用方代码（用法）：

```csharp
// Get the count
var count = Count(1,10);
// Iterate the results
foreach(var x in count)
{
    Console.WriteLine(x);
}
```

### 输出：

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10

在 .NET Fiddle 上的实时演示

当方法使用 yield 生成可枚举对象时，编译器会创建一个状态机，在遍历时它会运行到 yield 之前的代码。然后它返回 yield 的项，并保存其状态。

这意味着你在第一次调用方法时不会发现无效参数（传递 null 等）（因为那时只是创建了状态机），只有在尝试访问第一个元素时才会发现（因为只有此时状态机才会运行方法内的代码）。通过将其包装在先检查参数的普通方法中，你可以在方法调用时检查它们。这是一个快速失败的示例。

使用 C# 7+ 时，CountCore 函数可以方便地作为局部函数隐藏在 Count 函数中。请在此处查看示例。

### 第 120.3 节：提前终止

你可以通过传入一个或多个值或元素来扩展现有 yield 方法的功能，这些值或元素可以在函数内定义终止条件，通过调用 yield break 来停止内部循环的执行。

```csharp
public static IEnumerable<int> CountUntilAny(int start, HashSet<int> earlyTerminationSet)
{
    int curr = start;

    while (true)
    {
        if (earlyTerminationSet.Contains(curr))
        {
            // we've hit one of the ending values
            yield break;
        }

        yield return curr;

        if (curr == Int32.MaxValue)
        {
            // don't overflow if we get all the way to the end; just stop
            yield break;
        }

        curr++;
    }
}
```

上述方法将从给定的起始位置迭代，直到遇到 earlyTerminationSet 中的其中一个值。

```csharp
// Iterate from a starting point until you encounter any elements defined as
// terminating elements
var terminatingElements = new HashSet<int>{ 7, 9, 11 };
// This will iterate from 1 until one of the terminating elements is encountered (7)
foreach(var x in CountUntilAny(1,terminatingElements))
{
    // This will write out the results from 1 until 7 (which will trigger terminating)
    Console.WriteLine(x);
}
```

### 输出：

- 1
- 2
- 3
- 4
- 5
- 6

在 .NET Fiddle 上的实时演示

### 第 120.4 节：更相关的用法

```csharp
public IEnumerable<User> SelectUsers()
{
    // Execute an SQL query on a database.
    using (IDataReader reader = this.Database.ExecuteReader(CommandType.Text, "SELECT Id, Name FROM Users"))
    {
        while (reader.Read())
        {
            int id = reader.GetInt32(0);
            string name = reader.GetString(1);
            yield return new User(id, name);
        }
    }
}
```

当然，从 SQL 数据库获取 IEnumerable<User> 的方法还有其他方式——这只是演示了你可以使用 yield 将任何具有“元素序列”语义的东西转换为可供他人遍历的 IEnumerable<T>。

### 第 120.5 节：延迟求值

只有当 foreach 语句移动到下一个项目时，迭代器块才会求值到下一个 yield 语句。

考虑以下示例：

```csharp
private IEnumerable<int> Integers()
{
    var i = 0;
    while(true)
    {
        Console.WriteLine("Inside iterator: " + i);
        yield return i;
        i++;
    }
}

private void PrintNumbers()
{
    var numbers = Integers().Take(3);
    Console.WriteLine("Starting iteration");

    foreach(var number in numbers)
    {
        Console.WriteLine("Inside foreach: " + number);
    }
}
```

这将输出：

```
Starting iteration
Inside iterator: 0
Inside foreach: 0
Inside iterator: 1
Inside foreach: 1
Inside iterator: 2
Inside foreach: 2
```

查看演示

因此：

- “Starting iteration”最先被打印，即使迭代器方法是在打印它的行之前被调用的，因为行 Integers().Take(3); 实际上并未开始迭代（没有调用 IEnumerator.MoveNext()）
- 打印到控制台的行在迭代器方法内部的行和 foreach 内部的行之间交替，而不是迭代器方法内部的所有行先求值
- 此程序因 .Take() 方法而终止，即使迭代器方法有一个永远不会跳出的 while true。

### 第 120.6 节：Try...finally

如果迭代器方法在 try...finally 内部有 yield，那么返回的 IEnumerator 在对其调用 Dispose 时会执行 finally 语句，前提是当前求值点位于 try 块内部。

给定以下函数：

```csharp
private IEnumerable<int> Numbers()
{
    yield return 1;
    try
    {
        yield return 2;
        yield return 3;
    }
    finally
    {
        Console.WriteLine("Finally executed");
    }
}
```

调用时：

```csharp
private void DisposeOutsideTry()
{
    var enumerator = Numbers().GetEnumerator();

    enumerator.MoveNext();
    Console.WriteLine(enumerator.Current);
    enumerator.Dispose();
}
```

然后它打印：

```
1
```

查看演示

调用时：

```csharp
private void DisposeInsideTry()
{
    var enumerator = Numbers().GetEnumerator();

    enumerator.MoveNext();
    Console.WriteLine(enumerator.Current);
    enumerator.MoveNext();
    Console.WriteLine(enumerator.Current);
}
```
