
```csharp
public class DelegateSample
{
    //...

    public static void Main()
    {
        int[] items = new int[5];

        for (int i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer: ");
            string? text = Console.ReadLine();
            if (!int.TryParse(text, out items[i]))
            {
                Console.WriteLine($"{text} is not a valid integer.");
                return;
            }
        }

    public static void BubbleSort(int[] items, __AnonymousMethod_00)
    {
        for (int i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
    }

    private static bool __AnonymousMethod_00(int first, int second)
    {
        return first < second;
    }
}
```

在此示例中，编译器将匿名函数转换为单独声明的静态方法，该方法被实例化为委托并作为参数传递。惊讶的是，编译器生成的代码看起来与示例 13.8 非常相似。然而，如果涉及到外部变量，编译器执行的代码转换比重写匿名函数为静态方法复杂得多。

## 外部变量

在 Lambda 表达式之外声明的局部变量（包括方法的参数）被称为该 Lambda 的外部变量。（这个引用虽然技术上不是变量，也被认为是外部变量。）当 Lambda 主体使用外部变量时，该变量被 Lambda 捕获（等效地说是闭包）。在示例 13.20 中，我们使用外部变量来计算 `BubbleSort()` 执行了多少次比较。输出 13.2 显示了此列表的结果。

### 示例 13.20：在 Lambda 表达式中使用外部变量

```csharp
public class Program
{
    public static void Main()
    {
        int[] items = new int[5];
        int comparisonCount = 0;

        for (int i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer:");
            string text = Console.ReadLine();
            if (!int.TryParse(text, out items[i]))
            {
                Console.WriteLine($"{text} is not a valid integer.");
                return;
            }
        }

        DelegateSample.BubbleSort(items,
            (int first, int second) =>
            {
                comparisonCount++;
                return first < second;
            });

        for (int i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
        Console.WriteLine("Items were compared {0}",
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

注意，`comparisonCount` 出现在 Lambda 表达式之外，并在内部进行递增。调用 `BubbleSort()` 方法后，打印了 `comparisonCount`。通常，局部变量的生命周期与其作用域绑定；当控制离开作用域时，与变量相关的存储位置不再有效。但从捕获外部变量的 Lambda 创建的委托生命周期可能比局部变量长（或短），并且委托在每次调用时都必须能够访问该外部变量。因此，被捕获变量的生命周期被延长了：它保证至少与捕获它的生存委托一样长。（而且它可能比这更长——编译器生成确保外部变量延长的代码是一个实现细节，可能会更改。）

## 第 13 章：委托与 Lambda 表达式

C# 编译器负责生成在匿名方法和声明它的方法之间共享 `comparisonCount` 的 CIL 代码。

### 静态匿名函数

为了避免捕获匿名函数外部的数据产生任何意外后果，C# 9.0 在声明中启用了 `static` 修饰符。这导致编译器验证没有对匿名函数声明之外的数据进行闭包。（这与函数是实例还是静态无关。）要观察此行为，请参见示例 13.21。

### 示例 13.21：声明静态匿名函数

```csharp
int comparisonCount = 0;
DelegateSample.BubbleSort(items,static (int first, int second) => Error CS8820: A static anonymous function
    //不能包含对 comparisonCount 的引用。
    comparisonCount++;
    return first < second;
);

for (int i = 0; i < items.Length; i++) {
    Console.WriteLine(items[i]);
}
Console.WriteLine("Items were compared {0}",
    comparisonCount);
```

通常情况下，考虑默认使用静态局部函数声明，仅在需要时切换到限制较少的版本，从而增加闭包的意图性。

## 高级主题

### 外部变量的 CIL 实现

C# 编译器为捕获外部变量的匿名函数生成的 CIL 代码比不捕获变量的匿名函数代码要复杂。示例 13.22 显示了实现示例 13.20 中外部变量的 C# 等效 CIL 代码。

#### 示例 13.22：编译器为外部变量生成的 CIL 代码等

```sharp
public class Program
{
    // ...
    private sealed class __DisplayClass_00000001
    {
        public int comparisonCount;
        public bool __AnonymousMethod_00000000(int first, int second)
        {
            comparisonCount++;
            return first < second;
        }
    }
}
```

```sharp
public static void Main()
{
    __DisplayClass_00000001 locals = new();
    locals.comparisonCount = 0;
    int[] items = new int[5];

    for (int i = 0; i < items.Length; i++)
    {
        Console.Write("Enter an integer: ");
        string? text = Console.ReadLine();
        if (!int.TryParse(text, out int i))
        {
            Console.WriteLine($"{text} is not a valid integer.");
            return;
        }
    }

    DelegateSample.BubbleSort(items, locals.__AnonymousMethod_00000000);
    for (int i = 0; i < items.Length; i++)
    {
        Console.WriteLine(items[i]);
    }

    Console.WriteLine("Items were compared {0} times.", locals.comparisonCount);
}
```

注意，捕获的局部变量并没有被“传递”或“复制”。相反，捕获的局部变量 (`comparisonCount`) 是通过将其实现为实例字段来扩展其生命周期的。生成的 `DisplayClass` 是一个数据结构（C# 中为类），包含了评估表达式所需的变量（C# 中为公共字段）。

## 高级主题

### 意外捕获循环变量

你认为示例 13.23 的输出应该是？

#### 示例 13.23：C# 5.0 中捕获循环变量

```sharp
public class CaptureLoop
{
    public static void Main()
    {
        var items = new string[] { "Moe", "Larry", "Curly" };
        var actions = new List<Action>();
        foreach(string item in items)
        {
            actions.Add(() => Console.WriteLine(item));
        }
        foreach(Action action in actions)
        {
            action();
        }
    }
}
```

大多数人期望输出如输出 13.3 所示，在 C# 5.0 中确实如此。但在 C# 的之前的版本中，输出如输出 13.4 所示。

### 输出 13.3：C# 5.0 输出

```
Moe

Larry

Curly
```

### 输出 13.4：C# 4.0 输出

```
Curly

Curly

Curly
```

Lambda 表达式捕获变量并始终使用变量的最新值；它不会捕获创建委托时变量所的值。这通常正是你想要的——毕竟，示例 13.20 中捕获 `comparisonCount` 的目的就是确保在递增时使用其最新值。循环变量也不无区别；当你捕获循环变量时，每个委托都捕获同一个循环变量。当循环变化时，每个捕获该循环变量的委托都能看到这种变化。因此，C# 4.0 的行为是合理的——但几乎不是代码作者想要的。

在 C# 5.0 中，C# 语言发生了更改，`foreach` 循环的循环变量现在每次迭代时都被视为新变量；因此，每个委托都创建一个不同的变量，而不是所有迭代共享同一个变量。然而，此更改未应用于 `for` 循环：如果你使用 `for` 循环编写类似的代码，语句头部声明的任何循环变量在捕获时仍被视为单个外部变量。如果你需要编写在 C# 5.0 和之前的 C# 版本中运行相同的代码，请使用示例 13.24 所示的模式。

### 示例 13.24：C# 5.0 之前的循环变量捕获变通方案

```sharp
public class DoNotCaptureLoop {
    public static void Main() {
        var items = new string[] { "Moe", "Larry", "Curly" };
        var actions = new List<Action>();
        foreach(string item in items)
        {
            string _item = item;
            actions.Add(
                () => Console.WriteLine(_item));
        }
        foreach(Action action in actions)
        {
            action();
        }
    }
}
```

现在每个循环迭代显然都有一个新变量；每个委托转而闭包了不同的变量。

> ### 指南
> **避免**捕获循环变量。

# 表达式树

到为止，我们已经看到 lambda 转换为表达式树后变成了代表数据而非编译代码的对象。由于表达式树代表的是数据而非编译代码，因此可以在执行时分析 lambda 并使用信息构建一个在数据库上执行的查询。例如，`Where()` 接收到的表达式树可能会转换为 SQL 查询，如示例 13.25 所示。

## 将 Lambda 表达式作为数据

考虑以下 lambda：

```csharp
persons.Where(person => person.Name.ToUpper() == "INIGO MONTOYA");
```

假设 `persons` 是 `Persons` 数组，`Where` 方法返回委托类型 `Func<Person, bool>`。编译器接收到的表达式树在数组上执行。现在假设 `persons` 不是数组，而是一个代表包含数据的对象的。调用 `Where` 时，结果是如何定的？

一种技术是将数百万行传输到客户端。客户端可以从每行数据创建一个 `Person` 对象，从 lambda 创建委托并执行它。第二种好得多的是以某种方式将 lambda 的含义（过滤掉除 Montoya 外的所有行）发送到服务器。数据库服务器经过优化，可以快速执行此类过滤。然后服务器只需将少量的匹配行流到客户端。因此，客户端不是创建数百万个对象并拒绝几乎所有对象，而是只创建那些由服务器确定的符合查询的对象。但 lambda 的含义是如何到达服务器的呢？

# 表达式树是对象图

在执行时，lambda 转换为表达式树后变成包含 `System.Linq.Expressions` 命名空间对象的对象图。图中的根对象代表 lambda 本身。该对象引用代表参数、返回类型和体表达式的对象，如图 13.3 所示。对象图包含了编译器关于的所有信息

## 表达式树 719

该 lambda。该信息随后可以在执行时被用于创建一个查询。或者，根 lambda 表达式有一个方法 `Compile`，它可以即时生成 CIL 并创建一个实现所描述 lambda 的委托。

![](img/ffe0f34eac7523830420733690014d17_753_0.png)

图 13.3：lambda 表达式树类型

图 13.4 显示了 lambda 实体中一元和二元表达式在对象图中找到类型。

`UnaryExpression` 表示如 `--count` 这样的表达式。它有一个子节点 `Operand`，类型为 `Expression`。`BinaryExpression` 有两个子表达式 `Left` 和 `Right`。这两个类型都有一个识别特定运算符的 `NodeType` 属性，并且继承自基类。还有 30 多种表达式类型，例如 `NewExpression`、`ParameterExpression`、`MethodCallExpression` 和 `LoopExpression`，它们代表了（几乎）C# 和 Visual Basic 中所有可能的表达式。

# 第 13 章：委托与 Lambda 表达式

![](img/ffe0f34eac7523830420733690014d17_754_0.png)

## 委托与表达式树

lambda 表达式的有效性在编译时通过完全语义分析进行验证，无论转换为委托还是表达式树。转换为委托的 lambda 会导致编译器将 lambda 作为方法发射，并在执行时生成创建该方法委托的代码。转换为表达式树的 lambda 会导致编译器生成在执行时创建 `LambdaExpression` 实例的代码。但在使用语言集成查询 (LINQ) API 时，编译器如何知道是要生成委托在本地执行查询，还是生成表达式树以便将查询信息发送到远程数据库服务器呢？

构建 LINQ 查询的方法（如 `Where()`）是扩展方法。扩展 `IEnumerable<T>` 接口的方法版本接收委托参数；扩展 `IQueryable<T>` 接口的方法接收表达式树参数。因此，编译器可以使用正在被查询的

的的

图 13.4：一元和二元表达式树类型

## 表达式树 721

的类型来决定是否从作为参数提供的 lambda 创建委托或表达式树。

例如考虑以下代码中的 `Where()` 方法：

```csharp
persons.Where(person => person.Name.ToUpper() == "INIGO MONTOYA");
```

在 `System.Linq.Enumerable` 类中声明的扩展方法签名为：
