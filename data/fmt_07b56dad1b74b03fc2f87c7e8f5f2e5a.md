
该列表的最后一部分将两种方差概念结合在一个示例中，展示了当同时涉及 `in` 和 `out` 类型参数时，它们如何可以同时发生。

允许对泛型委托类型进行引用转换是将协变和逆变转换添加到 C# 4.0 的关键驱动场景之一。（另一个场景是对 `IEnumerable<out T>` 的协变支持。）

Lambda 表达式（和匿名方法）并不是 CLR 内置的。相反，当编译器遇到匿名函数时，它会将其转换为实现所需语义的特殊隐藏类、字段和方法。C# 编译器生成该模式的实现代码，因此开发人员无需自行编写。给定列表 13.12、13.13、13.16 或 13.17 中的代码，C# 编译器生成的 CIL 代码类似于列表 13.19 中显示的 C# 代码。

### 列表 13.19：编译器为 Lambda 表达式生成的 CIL 的 C# 等效代码

```csharp
class DelegateSample
{
    // ...
    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }
        BubbleSort(items,
            DelegateSample._AnonymousMethod_00000000);
        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
    }
}
private static bool __AnonymousMethod_00000000(
    int first, int second)
{
    return first < second;
}
```

在这个示例中，编译器将匿名函数转换为单独声明的静态方法，然后将其实例化为委托并作为参数传递。不出所料，编译器生成的代码与列表 13.8 中的原始代码非常相似，而匿名函数语法旨在简化该过程。然而，如果涉及外部变量，编译器执行的代码转换可能比仅仅将匿名函数重写为静态方法要复杂得多。

## 外部变量

在 lambda 表达式外部声明的局部变量（包括包含方法中的参数）被称为该 lambda 的外部变量。（`this` 引用虽然在技术上不是一个变量，但也被视为外部变量。）当 lambda 体使用外部变量时，该变量就被视为被 lambda 捕获（captured）（或等价地，封闭（closed over））。在列表 13.20 中，我们使用一个外部变量来统计 `BubbleSort()` 执行比较的次数。输出 13.2 显示了该列表的结果。

### 列表 13.20：在 Lambda 表达式中使用外部变量

```csharp
class DelegateSample
{
    // ...
    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        int comparisonCount = 0;
        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }
        BubbleSort(items,
            (int first, int second) =>
            {
                comparisonCount++;
                return first < second;
            });
        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
        Console.WriteLine("Items were compared {0} times.",
            comparisonCount);
    }
}
```

### 输出 13.2

```
Enter an integer:5
Enter an integer:1
Enter an integer:4
Enter an integer:2
Enter an integer:3
5
4
3
2
1
Items were compared 10 times.
```

请注意，`comparisonCount` 出现在 lambda 表达式之外，并在其中递增。调用 `BubbleSort()` 方法后，`comparisonCount` 会打印到控制台。

通常，局部变量的生命周期与其作用域绑定；当控制流离开作用域时，与该变量关联的存储位置不再有效。但是，由捕获外部变量的 lambda 创建的委托可能具有比局部变量通常更长的（或更短的）生命周期，并且委托必须能够每次被调用时都安全地访问外部变量。因此，被捕获变量的生命周期会被延长；保证它至少与捕获它的寿命最长的委托对象一样长。（它甚至可以存活更长时间——编译器生成代码以确保延长外部变量生命周期的具体方式是实现细节，可能会发生变化。）

## 高级主题

### 外部变量的 CIL 实现

C# 编译器负责生成 CIL 代码，在匿名方法和声明它的方法之间共享 `comparisonCount`。

C# 编译器为捕获外部变量的匿名函数生成的 CIL 代码比不捕获任何内容的简单匿名函数的代码更复杂。列表 13.21 显示了用于实现列表 13.20 中代码的外部变量的 CIL 代码的 C# 等效代码。

### 列表 13.21：编译器为外部变量生成的 CIL 代码的 C# 等效代码

```csharp
class DelegateSample
{
    // ...
    private sealed class __LocalsDisplayClass_00000001
    {
        public int comparisonCount;
        public bool __AnonymousMethod_00000000(
            int first, int second)
        {
            comparisonCount++;
            return first < second;
        }
    }
    // ...
    static void Main(string[] args)
    {
        int i;
        __LocalsDisplayClass_00000001 locals =
            new __LocalsDisplayClass_00000001();
        locals.comparisonCount = 0;
        int[] items = new int[5];
        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }
        BubbleSort(items, locals.__AnonymousMethod_00000000);
        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
        Console.WriteLine("Items were compared {0} times.",
            locals.comparisonCount);
    }
}
```

请注意，被捕获的局部变量从未“传递”到任何地方，也从未“复制”到任何地方。相反，被捕获的局部变量（`comparisonCount`）是一个单一变量，编译器通过将其实现为实例字段而不是局部变量来延长了其生命周期。局部变量的所有用法都被重写为字段的用法。

生成的类 `__LocalsDisplayClass` 是一个闭包（closure）——一种数据结构（在 C# 中是类），包含一个表达式以及评估该表达式所需的变量（在 C# 中是公共字段）。

### 意外捕获循环变量

你认为列表 13.22 的输出应该是什么？

### 列表 13.22：在 C# 5.0 中捕获循环变量

```csharp
class CaptureLoop
{
  static void Main()
  {
      var items = new string[] { "Moe", "Larry", "Curly" };
      var actions = new List<Action>();
      foreach (string item in items)
      {
          actions.Add(( )=> { Console.WriteLine(item); } });
      }
      foreach (Action action in actions)
      {
          action();
      }
  }
}
```

大多数人期望输出如输出 13.3 所示，在 C# 5.0 中确实如此。然而，在之前的 C# 版本中，输出如输出 13.4 所示。

### 输出 13.3：C# 5.0 的输出

```
Moe
Larry
Curly
```

### 输出 13.4：C# 4.0 的输出

```
Curly
Curly
Curly
```

Lambda 表达式会捕获一个变量，并且始终使用该变量的最新值；它不会捕获并保留委托创建时该变量的值。这通常是你想要的——毕竟，在清单 13.20 中捕获 `comparisonCount` 的目的就是为了确保在自增时使用其最新值。循环变量并不例外；当你捕获一个循环变量时，每个委托都捕获同一个循环变量。当循环变量发生变化时，所有捕获了该循环变量的委托都会看到这一变化。因此，C# 4.0 的行为虽然有其合理性，但几乎从不是代码作者的初衷。

在 C# 5.0 中，C# 语言发生了变化，`foreach` 循环的循环变量现在被视为每次循环迭代时都是一个新的变量；因此，每个委托创建都捕获一个不同的变量，而不是所有迭代共享同一个变量。然而，这一变更并未应用于 `for` 循环：如果你使用 `for` 循环编写类似代码，在 `for` 语句头部声明的任何循环变量在被捕获时都会被视为单一的外部变量。如果你需要编写在 C# 5.0 和早期 C# 版本中表现相同的代码，请使用清单 13.23 中所示的模式。

### 清单 13.23：C# 5.0 之前的循环变量捕获变通方法

```csharp
class DoNotCaptureLoop
{
    static void Main()
    {
        var items = new string[] { "Moe", "Larry", "Curly" };
        var actions = new List<Action>();
        foreach (string item in items)
        {
            string _item = item;
            actions.Add(
                () => { Console.WriteLine(_item); } );
        }
        foreach (Action action in actions)
        {
            action();
        }
    }
}
```

现在，显然每次循环迭代都有一个全新的变量；每个委托依次封闭在一个不同的变量上。

## 准则

**避免**在匿名函数中捕获循环变量。

## 表达式树

到目前为止，我们看到 Lambda 表达式是声明一种可以转换为委托类型的“内联”方法的简洁语法。表达式 Lambda（但不是语句 Lambda 或匿名方法）也可以转换为**表达式树**。委托是一种对象，它允许你将方法像其他对象一样传递并在任意时间调用它。表达式树是一种对象，它允许你传递编译器对 Lambda 主体的分析结果。那你为什么需要这种能力呢？显然，编译器在生成 CIL 时，编译器的分析结果对编译器很有用，但在执行时拥有一个表示该分析结果的对象对开发人员有什么用呢？让我们看一个例子。

### 将 Lambda 表达式用作数据

考虑以下代码中的 Lambda 表达式：

```csharp
persons.Where(
    person => person.Name.ToUpper() == "INIGO MONTOYA");
```

假设 `persons` 是一个 `Person` 类型的数组，并且 `Where` 方法中对应 Lambda 表达式参数的形参是委托类型 `Func<Person, bool>`。编译器会发出一个包含 Lambda 主体代码的方法。它生成代码，创建一个指向发出方法的委托，并将该委托传递给 `Where` 方法。`Where` 方法返回一个查询对象，当执行该对象时，它将委托应用于数组的每个成员以确定查询结果。

现在假设 `persons` 不是 `Person []` 类型，而是一个代表远程数据库表的对象，该表包含数百万人的数据。表中每一行信息的记录都可以从服务器流式传输到客户端，然后客户端可以创建对应于该行的 `Person` 对象。对 `Where` 的调用返回一个代表查询的对象。当在客户端请求该查询的结果时，结果是如何确定的？

一种技术是将数百万行数据从服务器传输到客户端。你可以从每一行创建一个 `Person` 对象，从 Lambda 创建一个委托，并在每个 `Person` 上执行该委托。这在概念上与数组场景没有不同，但成本高得多得多。

第二种更好的技术是设法将 Lambda 的含义（“过滤掉所有姓名不是 `Inigo Montoya` 的行”）发送到服务器。数据库服务器针对快速执行此类过滤进行了优化。然后，服务器可以选择仅将匹配行中数量很少的部分流式传输到客户端；客户端只需创建那些已经由服务器判定匹配查询的对象，而不是创建数百万个 `Person` 对象并拒绝其中几乎所有的对象。但是，Lambda 的含义是如何发送到服务器的呢？

此场景是将表达式树添加到语言中的动机。转换为表达式树的 Lambda 表达式变成了表示描述 Lambda 表达式的数据的对象，而不是实现匿名函数的已编译代码。由于表达式树表示的是数据而非已编译代码，因此可以在运行时分析 Lambda 并利用该信息来构建在数据库上执行的查询（例如）。接收到的表达式树（通过 `Where()`）可能被转换为传递给数据库的 `SQL` 查询，如清单 13.24 所示。

### 清单 13.24：将表达式树转换为 SQL where 子句

```
persons.Where( person => person.Name.ToUpper() == "INIGO MONTOYA");
select * from Person where upper(Name) = 'INIGO MONTOYA';
```
