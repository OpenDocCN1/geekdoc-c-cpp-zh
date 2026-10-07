

## 语言对比：Java—泛型

Java 中泛型的实现完全在编译器中完成，而不是在 Java 虚拟机中完成。最初开发 Java 的 Sun Microsystems 公司（在 Oracle 接手之前很久）采取了这种方法，以确保任何更新的 Java 虚拟机都不需要分发泛型支持。

Java 的实现使用了类似于 C++ 模板和 C# 泛型的语法，使用了类型参数和约束。然而，它并没有对值类型和引用类型进行区别对待。因此，Java 泛型在执行效率上的提升并不像 C# 那样。事实上，每当 Java 编译器返回数据时，它都会从指定的约束到基类 `Object` 注入自动向下转换。Java 编译器在编译时生成一个单一的专用类型，并用它来实例化任何泛型。最后，由于 Java 虚拟机原生不支持泛型，因此无法在执行时确定实例的类型，反射的其他用法也受到严重限制。

# 总结

在 C# 程序中，使用 `object`（特别是在集合语境下）应该让你考虑是否使用泛型解决问题会更好。消除类型转换带来的类型安全性提升、消除装箱（boxing）性能开销以及减少重复代码，都是显著的改进。

第 15 章更多地关注无的 `Collections.Generic` 命名空间。正如其名，该命名空间几乎完全由泛型类型组成。它提供了某些类型最初如何转换为使用泛型的清晰示例。然而，在处理这些主题之前，我们将研究表达式（expressions），它们为 C# 3.0 中处理集合的操作提供了重大的改进。

# 委托和 Lambda 表达式

之前的章节详细讨论了如何创建类来封装数据和操作。随着你创建越来越多的类，你将发现它们之间存在常见的模式。一种常见模式是将对象传递给方法，以便该方法反过来可以调用对象上的某个方法。例如，如果你向方法传递一个 `IComparer<int>` 引用，很有可能被调用的方法会调用所提供对象的 `compare()` 方法。在这种情况下，接口仅仅是传递一个可以调用的单个方法引用的方式。考虑第二个示例，即你启动了一个新进程。理想情况下，你不希望阻塞或反复检查（轮询）进程何时完成，而是希望方法异步运行，然后调用回调函数，被调用的方法将在调用完成后调用该回调函数来通知调用者。

每次当你想要传递方法时都定义一个新接口似乎是没有必要的。在本章中，我们描述了如何创建和使用一种称为“委托”（delegate）的特殊类，它允许你将方法像其他任何数据一样处理。我们随后展示了如何使用 Lambda 表达式轻松地创建自定义委托实例。

# 第 13 章：委托和 Lambda 表达式

本章包含区块，描述了如果你需要处理遗留的 C# 2.0 代码应该如何使用匿名方法；如果你在使用较新的代码，可以很大程度上忽略这些部分。我们以讨论表达式树（expression trees）结束本章，它允许你在执行时使用编译器对 Lambda 表达式的分析。

| 8. 表达式树 | 1. 引入委托 | 为什么使用委托 |
| :--- | :--- | :--- |
| 7. 外部变量 | 委托作为数据类型 | |
| 6. 委托具有结构等性 | 委托和 Lambda 表达式 | 2. 声明委托类型 |
| 5. 匿名方法 | 3. Lambda 表达式 | 委托内部：实例化委托 |
| 4. 语句 Lambda | | |

## 引入委托

资深的 C 和 C++ 程序员长期以来一直使用函数指针将一个方法的引用作为参数传递给另一个方法的机制。C# 通过使用委托实现了类似的功能。委托允许你捕获方法的引用并像处理其他对象一样传递它，并像处理其他任何方法一样调用捕获的方法。让我们考虑一个说明这种技术可能实用的示例。

## 定义场景

虽然效率不高，但最简单的排序算法之一是冒泡排序。列表 13.1 显示了 `BubbleSort()` 方法。

代码列表 13.1：BubbleSort() 方法

```csharp
public static class SimpleSort
{


- 1. C# 3.0 中添加的 Lambda 表达式。C# 2.0 及之前的版本使用匿名方法来创建自定义委托。

```csharp
public static void BubbleSort(int[] items)
{
    int i;
    int j;
    int temp;

    if(items == null)
    {
        return;
    }

    for(i = items.Length - 1; i >= 0; i--)
    {
        for(j = 1; j <= i; j++)
        {
            if(items[j] > items[j - 1])
            {
                temp = items[j - 1];
                items[j - 1] = items[j];
                items[j] = temp;
            }
        }
    }
    // ...
}
```

此方法将按升序对整数数组进行排序。

假设你需要对列表 13.1 中的整数进行升序或降序排序。你可以复制代码并将“大于”运算符替换为“小于”运算符，但仅仅为了更改一个操作符就复制几行代码似乎不是一个好主意。作为一种更简洁的替代方案，你可以传递一个额外的参数来指示如何执行排序，如列表 13.2 所示。

## 代码列表 13.2：BubbleSort() 方法，升序或降序

```csharp
public class SimpleSort2
{
    public enum SortType
    {
        Ascending,
        Descending
    }
```

```csharp
public static void BubbleSort(int[] items, SortType sortOrder)
{
    int i;
    int j;
    int temp;

    if(items == null)
    {
        throw new ArgumentNullException(nameof(items));
    }

    for(i = items.Length - 1; i >= 0; i--)
    {
        for(j = 1; j <= i; j++)
        {
            bool swap = false;
            switch(sortOrder) {
                case SortType.Ascending:
                    swap = items[j - 1] > items[j];
                    break;
                case SortType.Descending:
                    swap = items[j - 1] < items[j];
                    break;
            }
            if(swap) {
                temp = items[j - 1];
                items[j - 1] = items[j];
                items[j] = temp;
            }
        }
    }
    // ...
```

然而，这段代码仅处理了可能的排序顺序中的两种。如果你按字典顺序对它们排序（例如 1, 10, 11, 12, 2, 20, ...），或者通过其他标准进行排序，那么 `SortType` 值和相应的 `switch` 情况很快就会变得繁琐。

## 委托数据类型

为了增加代码的灵活性并减少重复，你可以将比较方法作为 `BubbleSort()` 方法的参数。为了将方法作为参数，需要一个数据类型来表示该方法；该数据类型通常被称为委托，因为它将调用“委托”另一个方法。你可以使用方法的名称作为委托实例。你也可以使用 Lambda 表达式作为委托，以便在处表示简短代码，而不是为它创建一个方法。列表 13.3 包含了对 `BubbleSort()` 方法的修改，它接收一个 Lambda 表达式参数。在这里，委托数据类型是 `Func<int, int, bool>`。

列表 13.3：带委托参数的 BubbleSort()

```csharp
public class DelegateSample
{
    // ...

    public static void BubbleSort(
        int[] items, Func<int, int, bool> compare)
    {
        int i;
        int j;
        int temp;

        if(compare == null)
        {
            throw new ArgumentNullException(nameof(compare));
        }

        if(items == null)
        {
            return;
        }

        for(i = items.Length - 1; i >= 0; i--)
        {
            for(j = 1; j <= i; j++)
            {
                if (compare(items[j - 1], items[j]))
```

- 2. 从 C# 3.0 开始。
- 3. 在 C# 7.0 中，你可以创建局部函数并同样使用函数名称作为委托。

