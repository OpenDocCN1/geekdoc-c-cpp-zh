

## 12.3. 练习

- 创建一个（泛型或非泛型）方法，将字符串数组向左旋转 2 位。例如，给定输入数组 `{"apple", "orange", "banana", "pair", "peach"}`，该方法应返回类似这样的结果：`{"banana", "pair", "peach", "apple", "orange"}`。
- 实现一个方法，将 `int` 类型的列表“就地”向左旋转 1 位，即不创建额外的列表。函数签名可能类似于：`void ShiftByOne(int[] arr)`。调用此函数/方法会将 `arr` 数组中的元素向左移动 1 位。

## 第 13 课。数字排序

### 13.1. 议程 - 泛型方法、类型约束、IEquatable、IComparable、dynamic 强制转换

排序是编程中最常见的操作之一。有许多不同的算法可以排序，例如，将数字列表按升序排列（例如，较小的数字在前，较大的数字在后）。

大多数编程语言库/运行时都附带了大量的排序相关的库函数和方法。.NET 也不例外。在许多情况下，你不需要重新发明轮子，最终只会使用 .NET 提供的（泛型）类型和方法来进行排序及其相关任务。

在本课中，我们将尝试“重新发明轮子”，纯粹是为了好玩。☺ 而且，我们还会给这个古老的排序问题添加一个小转折。具体来说，我们将尝试根据一个列表与特定数字（我们称之为“轴”或“pivot”）的“距离”来对整数列表进行排序。

例如，给定列表 `{9, 3, 19, 1}` 和轴 `4`，列表可以排序为 `{3, 1, 9, 19}`，按距离的升序排列，因为 `3` 和 `4` 之间的距离最小，其次是 `1` 和 `4` 之间的距离，依此类推。

对于 `int` 列表或其他特定数值类型，这样做相对简单。然而，在本课中，我们将尝试以*泛型*方式实现排序方法，特别是跨*所有*数值类型，而不仅仅是 `int`。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_199_0.png)

这是一节选修课。如果你是 C# 新手，或者你在其他编程语言中没有泛型方面的先验经验，那么最好在初次阅读时跳过这一课。如前所述，对于排序等常见操作，你很可能只会使用库函数。.NET 还包含许多接口，如 `IComparer<T>` 和委托，如 `Comparison<T>`，以简化广泛问题范围内的排序工作。

### 13.2. 代码阅读 - 泛型冒泡排序

这个代码示例有点“刻意设计”，部分原因是当前 C# 泛型的局限性。我们仅将这段代码用作示例，以说明 C# 的一些基本概念，包括泛型，而不是作为一个实用的示例。

C# 11.0 将在 2022 年稍晚时候发布，它将包含一项名为“接口中的静态抽象方法”的特性。这解决了我们在本课中解决的问题。

主程序使用整数列表测试在 Example 命名空间中定义的静态排序方法 `Bubble.Sort()`。

**sort-numbers/Program.cs**

```csharp
using Example;

var arr = new int[] { 64, 34, 25, 12, 22, 11, 90 };

var pivot = 20;
Console.WriteLine($"Pivot = {pivot}");

Console.Write("Original array:\t");
Bubble.Print(arr);

Bubble.Sort(arr, pivot);

Console.Write("Sorted array:\t");
Bubble.Print(arr);
```

如前所述，`Bubble.Sort()` 方法是以泛型方式实现的。

**sort-numbers/Bubble.cs**

```csharp
namespace Example;

static class Bubble {
    internal static void Sort<T>(IList<T> arr, T pivot) where T :
        IEquatable<T>, IComparable<T> {
        for (var i = 0; i < arr.Count - 1; i++) {
            for (var j = 0; j < arr.Count - i - 1; j++) {
                if (Compare(arr[j], arr[j + 1], pivot) > 0) {
                    (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
                }
            }
        }
    }

    private static int Compare<T>(T l, T r, T pivot) where T :
        IEquatable<T>, IComparable<T> {
        var (dl, dr) = (Distance(l, pivot), Distance(r, pivot));
        return dl.Equals(dr) ? 0 : (dl.CompareTo(dr) > 0 ? 1 : -1);
    }

    private static T Distance<T>(T l, T r) where T : IComparable<T> =>
        (l.Compare(r) > 0) ? Subtract(l, r) : Subtract(r, l);

    private static T Subtract<T>(T l, T r) where T : notnull =>
    (l, r) switch {
        (sbyte il, sbyte ir) => (T)(dynamic)(il - ir),
        (short il, short ir) => (T)(dynamic)(il - ir),
        (int il, int ir) => (T)(dynamic)(il - ir),
        (long il, long ir) => (T)(dynamic)(il - ir),
        (nint il, nint ir) => (T)(dynamic)(il - ir),
        (float il, float ir) => (T)(dynamic)(il - ir),
        (double il, double ir) => (T)(dynamic)(il - ir),
        (decimal il, decimal ir) => (T)(dynamic)(il - ir),
        _ => (T)((dynamic)l - (dynamic)r),
    };

    internal static void Print<T>(IEnumerable<T> arr) =>
        Console.WriteLine($"{{string.Join(", ", arr)}}");
}
```

#### 13.2.1. 解释

这是一个示例输出：

```text
$ dotnet run

Pivot = 20
Original array: {64, 34, 25, 12, 22, 11, 90}
Sorted array:  {22, 25, 12, 11, 34, 64, 90}
```

你可以验证，它们确实是基于其值相对于轴点（在本示例运行中为 20）的“距离”或“差异”进行排序的。

#### 13.2.2. 语法

C# 编程语言支持极其强大的泛型。事实上，它的“大哥”C++，早在 30 年前就将泛型/模板引入主流编程，现在在泛型特性方面也追随 C# 的脚步。

> 顺便提一下，C++20 标准包含许多强大的新特性，包括“概念”（concepts）。如果你已经有一段时间没有使用 C++，或者你从未用 C++ 编程，那么强烈建议以新的/全新的视角审视“现代 C++”。

然而，尽管泛型具有许多高级特性，当前 C# 泛型的设计仍有一些局限性。

例如，目前没有办法创建一个可以跨所有不同数值类型使用的泛型方法或类。或者用于支持某些基本操作（如加法或乘法）的类型。

虽然这本身并不是一个很大的限制，但由于数值类型和基本操作是编程中如此关键的一部分，即使有了 C# 的高级泛型支持，你有时也会感到受限。

例如，C# 中大约有十种数值类型。你不想为每种数值类型实现相同的方法（不使用泛型）。这就是最初使用泛型模板的全部意义所在。

这不仅仅局限于数字类型。一般来说，没有通用方法来指定你无法控制的一组类型，例如内置类型，或其他第三方库中的类型等。对于你自己定义的类型，你始终可以使用接口类型约束等其他手段。

> 例如，Haskell 有一个“类型类”（Typeclass）的概念，用于对一组相关类型进行分组/指定。“更现代”的命令式语言，如 Rust 和 Swift，也包含类似的概念，如 Trait 和 Protocol。它们与 C# 基于接口的类型约束略有不同，且稍微更通用一些。鼓励感兴趣的读者从其他资源中探索更多关于此主题的内容。

本课中的示例代码展示了创建跨所有数值类型（甚至可能更多）的泛型方法的一种方法。

这是一个演示，表明它*可以*这样做，但未必*应该*以这种方式做。本书中的所有示例代码，包括此示例，主要用于说明 C# 编程语言的特性。

让我们从主驱动程序开始。此示例主程序创建一个整数数组，然后调用 `Bubble.Sort()` 根据数组中数字相对于预设锚点 `pivot == 20` 的距离对数字进行排序。

如前所述，我们使用泛型实现“按距离排序”方法。特别是跨所有不同的数值类型。也就是说，即使我们使用双精度浮点数数组，该方法也应该有效。

但首先，让我们看一下实现的非泛型版本，特别是针对整数数组的版本。当方法被特化为 `int` 类型时，编译器将使用我们在本课时介绍的泛型模板生成类似的结果。

