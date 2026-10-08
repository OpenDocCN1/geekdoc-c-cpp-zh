
通过在集合初始化器中启用对象初始化器，可以使用集合初始化器来处理任何类型的集合，包括字典，这些集合的 `Add` 方法接受多个参数。

## 集合接口

回顾一下所有不同集合的公共成员和属性，你可能会注意到它们在公共接口上存在一些相似性和一致性。这种一致性源于这些集合类所实现的一组接口。有些类实现的接口比其他类更多，但它们都至少实现了一个接口。

集合接口可以分为提供特定集合实现合约的接口和提供支持性实现的接口，例如比较和枚举功能。在第一组中，提供特定集合行为的接口只有四个：

-   **ICollection<>** 定义了操作泛型集合的方法和属性。
-   **IList<T>** 扩展了 **ICollection<>**，提供了操作元素可按索引单独访问的泛型集合的方法和属性。
-   **IDictionary<TKey, TValue>** 扩展了 **ICollection<>**，提供了操作键/值对泛型集合的方法和属性，其中每个键值对的键必须是唯一的。
-   **ISet<T>** 扩展了 **ICollection<>**，提供了操作具有唯一元素并提供集操作的泛型集合的方法和属性。

第二组也只包含四个接口，如下所示：

-   **IComparer<T>** 定义了一个用于比较两个对象的方法。该接口与 **List<\>**.Sort 和 **List<\>**.BinarySearch 方法一起使用，并提供了一种自定义集合排序顺序的方法。**Comparer<\>** 类提供了该接口的默认实现，通常足以满足大多数需求。
-   **IEnumerable<>** 扩展了 **IEnumerable**，并通过暴露一个枚举器来支持对集合的简单迭代。包含此接口是为了与非泛型集合保持一致，通过实现此接口，泛型集合可以在任何期望使用 **IEnumerable** 的地方使用。
-   **IEnumerable<T>** 也支持对集合的简单迭代。
-   **IEqualityComparer<T>** 提供了一种方式来为你提供类型 T 的自定义相等性定义。**EqualityComparer<T>** 类提供了该接口的默认实现，通常足以满足大多数需求。

## 可枚举对象和迭代器

如果你查看 IEnumerable<T> 和 IEnumerator<T> 的定义，你会发现它们很相似。这些接口（及其非泛型对应项）构成了通常所说的*迭代器模式*。

这种模式基本上允许你向实现 IEnumerable<T> 的对象（也称为**可枚举对象**）请求一个枚举器（一个实现 IEnumerator<T> 的对象）。当你拥有一个 IEnumerator<T> 时，你就可以逐个元素地枚举（或迭代）数据。

例如，列表 9.5 中的代码展示了一个典型的 foreach 语句，它遍历整数列表的内容，并打印每个值。

### 列表 9.5 一个简单的 foreach 语句

```csharp
List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
foreach(int i in list)
{
    Console.WriteLine(i);
}
```

这段代码实际上被编译器转换为看起来像列表 9.6 中所示的代码。

### 列表 9.6 编译器展开的 foreach 语句

```csharp
List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
IEnumerator<int> iterator = ((IEnumerable<int>)list).GetEnumerator();
while (iterator.MoveNext())
{
    Console.WriteLine(iterator.Current);
}
```

GetEnumerator 方法由 IEnumerable<T> 接口定义（事实上，它是该接口定义的唯一成员），它仅仅提供了一种可枚举对象暴露枚举器的方法。正是通过枚举器（通过 MoveNext 方法和 Current 属性（由 IEnumerator<T> 和 IEnumerator 接口定义）），你可以向前遍历可枚举对象中包含的数据。

## 为什么有两个接口？

通过保持可枚举对象（**IEnumerable<T>**）和针对该对象的枚举器（**IEnumerator<T>**）之间的区别，你可以对同一个可枚举源进行多次迭代。显然，你不希望这些迭代在遍历数据时相互干扰，因此你需要两个独立的表示（枚举器）来提供当前数据元素以及移动到下一个元素的机制。

## 顺便提一下

幸运的是，所有的泛型集合（以及非泛型集合）已经实现了 **IEnumerable<T>**, **IEnumerable**, **IEnumerator<T>**, 和 **IEnumerator**，因此你可以直接使用它们，而不必自己编写迭代器机制的额外复杂性。

如果你希望自己的类提供类似的行为怎么办？你当然可以让你的类实现 **IEnumerable<T>** 并编写自己的 **IEnumerator<T>** 派生类，但如果你使用迭代器，这样做就不是必须的。这允许编译器为你完成所有繁重的工作。

迭代器是一个方法、属性 get 访问器或运算符，它返回一组有序的值，这些值都是同一类型。`yield` 关键字告诉编译器其所在的代码块是一个迭代器块。`yield` return 语句返回每个元素，而 `yield` break 语句结束迭代。此类迭代器方法、访问器或运算符的主体有以下限制：

-   不允许使用不安全代码块。
-   参数不能是 ref 或 out 参数。
-   `yield` return 语句不能位于 try-catch 块内的任何位置。如果它后面跟着一个 `finally` 块，它可以位于 try 块中。
-   `yield` break 语句可以位于 try 块或 catch 块中，但不能位于 `finally` 块中。
-   `yield` 语句不能位于匿名方法中。

列表 9.7 展示了使用迭代器产生与列表 9.6 相同输出的代码。

## 列表 9.7 一个简单的迭代器

```csharp
class Program
{
    static IEnumerable<int> GetEvenNumbers()
    {
        yield return 0;
        yield return 2;
        yield return 4;
        yield return 6;
        yield return 8;
    }

    static void Main()
    {
        foreach(int i in GetEvenNumbers())
        {
            Console.WriteLine(i);
        }
    }
}
```

迭代器可以做的事情远不止简单地产生值。只要你遵守前面提到的限制，迭代器可以具有任意程度的复杂性，用于确定要产生的值。列表 9.8 产生与列表 9.7 相同的输出，但使用了一个更复杂的迭代器。

## 列表 9.8 一个更复杂的迭代器

```csharp
class Program
{
    static IEnumerable<int> GetEvenNumbers()
    {
        for (int i = 0; i <= 9; i++)
        {
            if (i % 2 == 0)
            {
                yield return i;
            }
        }
    }

    static void Main()
    {
        foreach(int i in GetEvenNumbers())
        {
            Console.WriteLine(i);
        }
    }
}
```

## 总结

在本章中，你学习了如何使用数组和集合来处理大量数据。数组是最简单的集合类型，并得到语言的直接支持，而其他集合类型，如 List<T> 和 Stack<T>，提供了更多的灵活性，使你能够创建自己专门的集合。你还学习了索引器如何使你的类提供与数组和集合相同的基于索引的访问类型。最后，你查看了可用的不同集合接口，并看到了如何轻松地使用初始化器语法声明和初始化数组和集合。

这完成了你的编程基础。你现在知道了语言语法以及创建自己的类、结构体、枚举和集合的基础知识，以及如何操作字符串数据和控制程序流程。

## 问答

-   **问.** 什么是数组？
    **答.** 数组是一个按数字索引的对象集合，这些对象都具有相同的编译时类型。

-   **问.** C# 中的数组是从零开始还是从一开始索引？
    **答.** C# 中的数组使用从零开始的索引方案。

-   **问.** C# 中的数组可以调整大小吗？
    **答.** C# 中的数组可以使用 `Array.Resize` 静态方法间接调整大小，该方法根据需要创建一个新数组，并将旧数组中的值复制到新数组中。

-   **问.** 什么是索引器？
    **答.** 索引器是一种特殊类型的属性，它允许类像数组一样被索引。索引器通过签名而不是名称来标识，并且必须是实例成员。

-   **问.** 什么是 `List<>` 集合？
    **答.** `List<>` 集合是最常用的集合，类似于数组，但根据需要动态调整大小。

-   **问.** 什么是字典？
    **答.** 字典是一种不允许重复的集合，可以提供一组键和一组值之间的映射。

