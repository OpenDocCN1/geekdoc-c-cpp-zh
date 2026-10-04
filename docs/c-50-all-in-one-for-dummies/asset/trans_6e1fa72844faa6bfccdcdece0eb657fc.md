

```sharp
class EvenNumbers
{
    //DescendingEvens -- 这是一个“命名迭代器”。
    //  同时也演示了 yield break 关键字
    //  查看在 Main() 中如何使用 foreach 调用它。
    public System.Collections.IEnumerable DescendingEvens(int top,
        int stop)
    {
        // 将 top 设置为最近的偶数。
        // 如果 top / 2 的余数不为0。
        if (top % 2 != 0)
            top -= 1;
        // 从 top 向下到 stop 以上的偶数。
        for (int i = top; i >= stop; i -= 2)
        {
            if (i < stop)
                yield break;
            // 在每次迭代时返回下一个偶数。
            yield return i;
        }
    }
}
```

`DescendingEvens()` 方法接受两个参数（这是一个实用的添加），这些参数设置了你想要开始的偶数的上限以及你想要停止的下限。生成的第一个偶数将等于 `top` 参数，或者如果 `top` 是奇数，则等于它下方最近的偶数。生成的最后一个偶数将等于 `stop` 参数的值（或者如果 `stop` 是奇数，则等于它上方最近的偶数）。然而，该方法本身并不返回 `int`；它返回 `IEnumerable` 接口。但它仍然包含一个 `yield return` 语句来返回一个偶数，然后等待下一次从 `foreach` 循环中调用。这就是 `int` 产出的地方。

![](img/6df7bb88e9302e98442acc219cfbd7fc_181_0.png)

这个示例展示了另一个没有底层集合的集合——例如本章前面提到的 `StringChunks`。请注意，这个是计算出来的——方法“`yield returns”的是一个计算后的值，而不是存储或硬编码的值。这是实现无集合集合的另一种方法。（你也可以从数据源或网络服务中检索项目）。最后，该示例显示你可以以任何你喜欢的方式迭代集合：例如，向下而不是向上，或者以2为步长而不是以1为步长。

![](img/6df7bb88e9302e98442acc219cfbd7fc_181_1.png)

迭代器也不必是的。考虑以下迭代器，只要你想要请求它们，它就会交付一个新的数字：

```sharp
public System.Collections.IEnumerable PositiveIntegers()
{
    for (int i = 0; ; i++)
    {
        yield return i;
    }
}
```

这个示例实际上是一个无限循环。你可能想要传递一个用于停止迭代的值。以下是你如何在 `Main()` 的 `foreach` 循环中调用 `DescendingEvens()` 的方法。（在上一个示例中调用 `PositiveIntegers()` 的效果也类似。）这个示例还演示了传递奇数作为限制值会发生什么——这是 `%` 运算符的另一种用法：

```csharp
// 实例化 EvenNumbers“集合”类。
EvenNumbers en = new EvenNumbers();
// 迭代它：打印从 10 到 4 的偶数。
Console.WriteLine("\nstream of descending evens :\n");
foreach (int even in en.DescendingEvens(11, 3))
{
    Console.WriteLine(even);
}
```

此调用产生了一个从 10 到 4 的偶数整数列表。还要注意 `foreach` 是如何指定的。你必须实例化一个 `EvenNumbers` 对象（集合类）。然后，在 `foreach` 语句中，通过该对象调用命名的迭代器方法：

```csharp
EvenNumbers en = new EvenNumbers();
foreach(int even in en.DescendingEvens(nTop, nStop)) ...
```

如果 `DescendingEvens()` 是静态的，你甚至不需要实例化。
[/content]

[content]

# 第8章 泛型（Buying Generic）

## 本章内容

-   **让你的代码泛型化且真正强大**（Making your code generic and truly powerful）
-   **编写你自己的泛型类**（Writing a generic class）
-   **编写泛型方法**（Writing generic methods）
-   **使用泛型接口和委托**（Using generic interfaces and delegates）

## 编写新的处方（Writing a New Prescription: Generics）

泛型有什么之处？它们之所以优秀有两个原因：安全和性能。

