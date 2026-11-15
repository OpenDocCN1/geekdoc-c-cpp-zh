

```csharp
int i;
int[] items = new int[5];
ComparisonHandler comparisonMethod;

for (i = 0; i < items.Length; i++)
{
    Console.Write("Enter an integer:");
    items[i] = int.Parse(Console.ReadLine());
}

comparisonMethod =
    delegate(int first, int second)
    {
        return first < second;
    };

BubbleSort(items, comparisonMethod);

for (i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}
}
```

在清单 12.11 中，你将对 BubbleSort() 的调用更改为使用匿名方法，以按降序对项目进行排序。请注意，未指定 LessThan() 方法。相反，delegate 关键字直接与代码内联放置。在此上下文中，delegate 关键字用于指定一种“委托文本”，类似于引号指定字符串文本。

你甚至可以直接调用 BubbleSort() 方法，而无需声明 comparisonMethod 变量（参见清单 12.12）。

## 清单 12.12：在不声明变量的情况下使用匿名方法

```csharp
class DelegateSample
{
    // ...

    static void Main(string[] args)
    {

        int i;
        int[] items = new int[5];
        for (i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }

        BubbleSort(items,
            delegate(int first, int second)
            {
                return first < second;
            }
        );

        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
    }
}
```

请注意，在所有情况下，参数类型和返回类型都必须与 ComparisonHandler 数据类型兼容，即 BubbleSort() 第二个参数的委托类型。

总之，C# 2.0 引入了一项新功能——匿名方法，它提供了一种声明无名称方法并将其转换为委托的方式。

## 高级主题

## 无参数匿名方法

方法签名与委托数据类型的兼容性并不排除没有参数列表的可能性。与 lambda 表达式、语句 lambda 和表达式 lambda（参见下一节）不同，匿名方法允许省略参数列表（例如，delegate { return Console.ReadLine() == "" }）。这不常见，但它确实允许相同的匿名方法出现在多个场景中，即使委托类型可能不同。但是请注意，尽管可以省略参数列表，但返回类型仍需与委托的返回类型兼容（除非抛出异常）。

## 系统定义的委托：Func<>

.NET 3.5（C# 3.0）包含一系列名为“Action”和“Func”的泛型委托。System.Func 表示带有返回类型的委托，而 System.Action 对应于没有返回类型的情况。这些委托的签名显示在清单 12.13 中（尽管 in/out 类型修饰符直到 C# 4.0 才添加，如稍后讨论）。

## 清单 12.13：Func 和 Action 委托声明

```csharp
public delegate void Action ();

public delegate void Action<in T>(T arg)

public delegate void Action<in T1, in T2>(
    in T1 arg1, in T2 arg2)

public delegate void Action<in T1, in T2, in T3>(
    T1 arg1, T2 arg2, T3 arg3)

public delegate void Action<in T1, in T2, in T3, in T4>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4)

...

public delegate void Action<
    in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8,
    in T9, in T10, in T11, in T12, in T13, in T14, in T15, in T16>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4,
    T5 arg5, T6 arg6, T7 arg7, T8 arg8,
    T9 arg9, T10 arg10, T11 arg11, T12 arg12,
    T13 arg13, T14 arg14, T15 arg15, T16 arg16)

public delegate TResult Func<out TResult>();

public delegate TResult Func<in T, out TResult>(T arg)

public delegate TResult Func<in T1, in T2, out TResult>(
    in T1 arg1, in T2 arg2)

public delegate TResult Func<in T1, in T2, in T3, out TResult>(
    T1 arg1, T2 arg2, T3 arg3)

public delegate TResult Func<in T1, in T2, in T3, in T4,
    out TResult>(T1 arg1, T2 arg2, T3 arg3, T4 arg4)

...

public delegate TResult Func<
    in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8,
    in T9, in T10, in T11, in T12, in T13, in T14, in T15, in T16,
    out TResult>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4,
    T5 arg5, T6 arg6, T7 arg7, T8 arg8,
    T9 arg9, T10 arg10, T11 arg11, T12 arg12,
    T13 arg13, T14 arg14, T15 arg15, T16 arg16)
```

由于清单 12.13 中的委托定义是泛型的，因此可以使用它们，而无需定义自定义委托。例如，与其声明 ComparisonHandler 委托类型，代码可以简单地使用 Func<int, int, bool> 声明 ComparisonHandler 委托。Func 的最后一个类型参数始终是委托的返回类型。较早的类型参数按顺序对应委托参数的类型。在 ComparisonHandler 的情况下，返回值为 bool（Func 声明中的最后一个类型参数），而类型参数 int 和 int 分别对应 ComparisonHandler 的第一个和第二个参数。在许多情况下，.NET 3.5 框架中包含 Func 委托消除了定义委托的必要性。对于没有返回值（TResult）且不接受参数的委托，应使用 System.Action 或其泛型版本之一。

但是，当此类类型能简化使用委托的编码时，仍应声明委托类型。例如，继续使用 ComparisonHandler 能更明确地指示委托的用途，而 Func<int, int, bool> 仅提供对方法签名的理解。

关于是否声明委托的评估仍然有意义，包括诸如委托标识符的名称是否足以指示意图、委托类型名称是否能澄清其用途，以及使用 .NET 3.5 类型是否会不必要地将程序集的使用限制为 .NET 3.5 客户端等考虑因素。

请注意，即使可以使用泛型 Func 委托替代显式定义的委托，这些类型也不兼容。即使类型参数匹配，也不能将一个委托类型赋给另一个委托类型的变量。例如，不能将 ComparisonHandler 变量赋给 Func<int, int, bool> 变量，也不能将它们互换地作为参数传递，尽管两者都表示接受两个 int 参数并返回 bool 的委托签名。

但是，请注意装饰清单 12.13 中委托的类型参数修饰符。得益于 C# 4.0 添加的协变支持，这些修饰符确实允许在它们之间进行一定程度的强制转换。请考虑以下逆变示例：因为 void Action<in T>(T arg) 带有 in 类型参数修饰符，所以可以将 Action<object> 类型的对象赋给 Action<string> 类型。换句话说，任何具有 void 返回和 object 参数的方法都会隐式转换为仅允许 string 类型参数的更严格委托类型。同样，对于协变和 Func 委托——由于 Func<out TResult>() 在 TResult 上包含 out 类型参数修饰符，因此可以将 Func<string> 的值隐式赋给 Func<object> 变量。（参见清单 12.14。）

## 清单 12.14：使用委托的协变

```csharp
// Covariance
Action<object> broadAction =
    delegate(object data)
    {
        Console.WriteLine(data);
    };

Action<string> narrowAction = broadAction;

// Contravariance
Func<string> narrowFunction =
    delegate()
    {
        return Console.ReadLine();
    };

Func<object> broadFunction = narrowFunction;

// Covariance & Contravariance Combined
Func<object, string> func1 =
    delegate(object data)
    {
        return data.ToString();
    };

Func<string, object> func2 = func1;
```

清单的最后一部分将两种协变概念结合到单个示例中，演示当同时涉及 in 和 out 类型参数时，它们如何同时发生。

在这些泛型委托中需要协变支持，是 C# 现在包含该功能的关键促成因素之一。²

2. 另一个是对 IEnumerable<T> 的协变支持。

