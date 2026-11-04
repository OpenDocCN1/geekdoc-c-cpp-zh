
我们在第 9 章详细介绍了声明类及其成员的机制，但如你所见，这并不复杂。最终，我们希望能够将该类型的实例用作 foreach 语句的源：

```csharp
foreach (int prime in new PrimeGenerator())
{
    Console.WriteLine(prime);

    Console.Write("Want More? ");
    if (!Console.ReadLine().ToLower().StartsWith("y"))
        break;
}
```

注意，我们正在利用 foreach 语句的灵活性，因为我们没有实现任何 IEnumerable 接口。没有理由不实现这些接口，但为了保持简单，我暂时选择省略接口实现的细节。

接下来是枚举器本身。这里，我们需要有两个成员：一个是 MoveNext 方法；另一个是带有可用 get 访问器的 Current 属性。现在不必过于担心细节，而要关注我们漂亮的算法现在需要如何在多次 MoveNext 调用之间维护状态。对 MoveNext 的调用表示消费者——在我们的例子中是 foreach 语句——正在向我们请求下一个元素。此时，我们需要知道我们返回给调用方的上一个质数是什么，并开始搜索下一个质数。当我们找到一个时，需要跳出循环，将其赋给 _current 字段（该字段在 Current 属性中用于向调用方返回值），然后从 MoveNext 返回，表示我们找到了一个：

```csharp
class PrimeEnumerator
{
    private int _current = 1;

    public bool MoveNext()
    {
        for (int num = _current + 1; num < int.MaxValue; num++)
        {
            bool foundDiv = false;

            for (int div = 2; div <= Math.Sqrt(num); div++)
            {
                if (num % div == 0)
                {
                    foundDiv = true;
                    break;
                }
            }
        }
    }
}
```

```csharp
if (!foundDiv)
{
    _current = num;
    return true;
}
}

return false;
}

public int Current
{
    get { return _current; }
}
}
```

注意我如何将外层循环绑定到 int.MaxValue 以避免溢出条件，否则我们会进入负整数领域，在那里质数定义不明确（更糟的是，我们的算法会无法处理）。图 7.20 展示了在实践中使用迭代器进行质数的惰性计算。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_423_0.png)

图 7.20 按需计算质数。

如你所见，手工创建迭代器是可行的，但并不十分吸引人。而且这里我们甚至还没有处理资源释放（通过 IDisposable）或迭代器内部更复杂的控制流。从 C# 2.0 开始，可以使用迭代器让编写这种复杂东西变得容易得多。事实上，LINQ to Objects 的实现几乎完全基于此特性（你将在第 20 章看到）。

还记得我们的 PrintPrimes 示例吗？如果不记得，请翻回“for 循环”一节并记住它。现在看看下面的代码，找出几处差异：

```csharp
static IEnumerable<int> GetPrimes(int max)
{
    for (int num = 2; num < max; num++)
    {
        bool foundDiv = false;

        for (int div = 2; div <= Math.Sqrt(num); div++)
        {
            if (num % div == 0)
            {
                foundDiv = true;
                break;
            }
        }

        if (!foundDiv)
        {
            yield return num;
        }
    }
}
```

为方便起见，我用粗体标出了差异：

- 方法的返回类型变成了 IEnumerable<int>。如果使用下一点提到的特性，这有可能将整个方法体变成一个迭代器。
- 我们不再使用普通 return 关键字从方法返回，而是改用 yield return 关键字逐个地将对象返回给调用方。

在内部，迭代器所做的正是我们手工完成的事情：它们构建一个状态机，跟踪控制权让出时的执行位置，以便后续的 MoveNext 调用可以在前一次调用停止的状态继续。此外，生成器迭代器代码确保正确清理迭代器代码中使用的资源。它还处理多线程访问，以便多个迭代可以同时进行。不深入细节，我们只瞥一眼生成代码的宏观结构。图 7.21 通过 ILDASM 的视角展示了迭代器的复杂性。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_425_0.png)

图 7.21 为迭代器生成的代码。

现在我们要做的就是调整我们的消费代码：

```csharp
foreach (int prime in GetPrimes(int.MaxValue))
{
    Console.WriteLine(prime);

    Console.Write("Want More? ");
    if (!Console.ReadLine().ToLower().StartsWith("y"))
        break;
}
```

迭代器最重要的特性无疑是它保持代码可读，就像代码最初期望的样子。大家都知道 return；现在你只需使用 yield return，而不必操心暂停和恢复迭代器执行相关的所有簿记工作。所有这类底层工作都由编译器处理。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_425_1.png)

为了激发你对 LINQ 的兴趣，我们来揭示它的一个查询运算符的实现：Where（一个方法，因此首字母大写）。我们在之前的示例中已经使用过 where 子句（一个关键字，因此小写）来筛选出内存占用大于 50MB 的那些进程：

```csharp
const int MB = 1024 * 1024;
var memHungry = from proc in Process.GetProcesses()
    where proc.WorkingSet64 > 50 * MB
    select new { proc.ProcessName, MB = proc.WorkingSet64 / MB };
```

where 关键字只是对 Where 方法调用的一种语法糖，在此上下文中，Where 方法被称为查询运算符。我们将在第 19 章介绍 LINQ 时更详细地说明查询表达式到方法调用的这种转换，但前面代码中的查询表达式“脱糖”后如下：

```csharp
var memHungry =
    Process.GetProcesses()
    .Where(proc => proc.WorkingSet64 > 50 * MB)
    .Select(proc => new { proc.ProcessName, MB = proc.WorkingSet64 / MB });
```

LINQ to Objects 的 Where 运算符实现如下：

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
                                    Func<T, bool> predicate)
{
    foreach (T item in source)
    {
        if (predicate(item))
        {
            yield return item;
        }
    }
}
```

我在这里省略了一些关于参数验证的细节，你稍后会看到。更重要的是理解这个迭代器如何工作。首先，注意它是一个泛型方法，可以处理任何 IEnumerable<T> 作为输入。第一个参数带有 this 修饰符这一事实使它成为扩展方法。这允许该参数出现在左侧，从而实现略微不同且更自然的调用语法：

```csharp
result = src.Where(predicate);
```

应包含在结果序列中。而这正是 `if` 语句中发生的情况。如果谓词返回 true，该元素就会被返回给调用方。而所有这些都以惰性方式完成：当调用方停止从查询中提取元素时，就不再分析更多元素，循环随之终止。很迷人，不是吗？

LINQ 使我们能够任意将多个运算符链接在一起。对于筛选，使用 `Where`；它接收一个序列并产生一个新序列。在我们的示例查询中，我们将这个筛选操作的输出送入由 `Select` 完成的投影，从而产生另一个序列。我们可以继续这样做，使用排序、分组、聚合等操作。这个概念在图 7.22 中以图形方式说明。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_428_0.png)

图 7.22 查询中不同迭代器之间的交互。

这种齿轮和链条的使用恰好说明了这一点。`foreach` 语句本质上是在拉动链条，使 `Select` 齿轮转动。在内部，它使用 `foreach` 语句从 `Where` 查询运算符的结果中抽取数据。而后者最终从数据源消费数据；在我们的例子中是 `Process.GetProcesses()`。一旦消费的 `foreach` 语句停止运行（例如由于 `break` 语句），通过链条连接的迭代器也会停止运转。

我们稍后会更详细地讨论 LINQ，但我希望你马上记住一件事。如果你正在编写循环结构来处理数据，LINQ 可能是更好的选择。一方面，它显著提高了代码可读性；另一方面，惰性可以成为避免不必要计算的优势。
