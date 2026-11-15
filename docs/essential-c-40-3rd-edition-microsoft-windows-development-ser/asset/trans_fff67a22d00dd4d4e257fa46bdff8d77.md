
Customer>、Dictionary<Guid, Order> 和 Dictionary<long, Order> 将需要新的内部类型定义，例如。

## 语言对比：Java—泛型

Sun 对 Java 泛型的实现完全在编译器内进行，而不在 Java 虚拟机内。Sun 这样做是为了确保，因为使用了泛型，就不需要分发更新的 Java 虚拟机。

Java 的实现使用与 C++ 模板和 C# 泛型相似的语法，包括类型参数和约束。但由于它不对值类型和引用类型区别对待，未修改的 Java 虚拟机无法支持值类型的泛型。因此，Java 泛型无法获得 C# 的执行效率。事实上，每当 Java 编译器需要返回数据时，它都会注入从指定约束（如果已声明）或基础 Object 类型（如果未声明）的自动向下转换。此外，Java 编译器在编译时生成一个单一的专用类型，然后用它来实例化任何构造类型。最后，由于 Java 虚拟机不原生支持泛型，无法在执行时确定泛型类型实例的类型参数，反射的其他用途也受到严重限制。

## 摘要

泛型改变了 C# 1.0 的编码风格。在几乎所有 C# 1.0 代码中使用 object 的场景下，泛型在 C# 2.0 及更高版本中都成为了更好的选择，以至于在集合方面使用 object 至少应被视为可能需要泛型实现的信号。提高的类型安全性、避免强制转换以及减少代码膨胀带来了显著改进。同样，在代码传统上使用 System.Collections 命名空间的地方，应改为选择 System.Collections.Generic。

第 16 章将探讨最普遍的泛型命名空间之一 System.Collections.Generic。该命名空间几乎完全由泛型类型组成。它提供了清晰的示例，说明一些最初使用 object 的类型后来是如何转换为泛型的。然而，在探讨这些主题之前，我们将研究表达式，它们为使用集合提供了 C# 3.0（及更高版本）的重大改进。

## 委托和 Lambda 表达式

前几章广泛讨论了如何使用面向对象开发的许多内置 C# 语言设施来创建类。从类实例化的对象封装了数据和对数据的操作。随着你创建越来越多的类，你会看到这些类之间关系中的常见模式。

这种模式之一是传递一个表示接收者可以调用的方法的对象。将方法用作数据类型及其对发布-订阅模式的支持是本章的重点。C# 2.0 和 C# 3.0 都为该领域的编程引入了额外的语法。虽然 C# 3.0 完全支持之前的语法，但在许多情况下，C# 3.0 将弃用旧式语法的使用。然而，我将早期语法放入了高级主题块中，除非你需要支持早期编译器，否则可以大体忽略。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_517_0.png)

## 委托简介

资深 C 和 C++ 程序员长期以来一直使用方法指针作为将可执行步骤作为参数传递给另一个方法的手段。C# 使用委托实现相同的功能，委托将方法封装为对象，从而实现在运行时绑定的间接方法调用。考虑一下此方法有用的示例。

## 定义场景

虽然不一定高效，但也许最简单的排序例程之一是冒泡排序。清单 12.1 显示了 BubbleSort() 方法。

### 清单 12.1：BubbleSort() 方法

```csharp
static class SimpleSort1
{
    public static void BubbleSort(int[] items)
    {
        int i;
        int j;
        int temp;

        if(items==null)
        {
            return;
        }

        for (i = items.Length - 1; i > 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                if (items[j - 1] > items[j])
                {
                    temp = items[j - 1];
                    items[j - 1] = items[j];
                    items[j] = temp;
                }
            }
        }
    }
    // ...
}
```

此方法将按升序对整数数组进行排序。

但是，如果你想支持按降序排序整数的选项，基本上有两种选择。你可以复制代码并将大于运算符替换为小于运算符。或者，你可以传入一个额外参数，指示如何执行排序，如清单 12.2 所示。

### 清单 12.2：BubbleSort() 方法，升序或降序

```csharp
class SimpleSort2
{
    public enum SortType
    {
        Ascending,
        Descending
    }

    public static void BubbleSort(int[] items, SortType sortOrder)
    {
        int i;
        int j;
        int temp;

        if(items==null)
        {
            return;
        }

        for (i = items.Length - 1; i >= 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                switch (sortOrder)
                {
                    case SortType.Ascending :
                        if (items[j - 1] > items[j])
                        {
                            temp = items[j - 1];
                            items[j - 1] = items[j];
                            items[j] = temp;
                        }

                        break;
                    case SortType.Descending :
                        if (items[j - 1] < items[j])
                        {
                            temp = items[j - 1];
                            items[j - 1] = items[j];
                            items[j] = temp;
                        }
                        break;
                    }
                }
            }
        }
    }
    // ...
}
```

但是，这只能处理可能的排序顺序中的两种。如果你想按字母顺序排序、随机化集合或通过其他标准排序，那么 BubbleSort() 方法和相应的 SortType 值的数量很快就会变得难以管理。

## 委托数据类型

为了提高灵活性（并减少代码重复），你可以将比较方法作为参数传递给 BubbleSort() 方法。此外，为了将方法作为参数传递，需要有一种可以表示该方法的数据类型——换句话说，就是委托。清单 12.3 包含对 BubbleSort() 方法的修改，该修改接受一个委托参数。在此示例中，委托数据类型是 ComparisonHandler。

### 清单 12.3：带委托参数的 BubbleSort() 方法

```csharp
class DelegateSample
{
// ...
public static void BubbleSort(
int[] items, ComparisonHandler comparisonMethod)
{
int i;
int j;
int temp;
if(items==null)
{
return;
}
if(comparisonMethod == null)
{
throw new ArgumentNullException("comparisonMethod");
}
for (i = items.Length - 1; i >= 0; i--)
{
    for (j = 1; j <= i; j++)
    {
        if (comparisonMethod(items[j - 1], items[j]))
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

ComparisonHandler 是一种表示用于比较两个整数的方法的数据类型。在 BubbleSort() 方法中，你在条件表达式内使用 ComparisonHandler 的实例，名为 comparisonMethod。由于 comparisonMethod 表示一个方法，调用该方法的语法与直接调用方法相同。在此示例中，comparisonMethod 接受两个整数参数，并返回一个布尔值，指示第一个整数是否大于第二个整数。

也许比特定算法更值得注意的是，ComparisonHandler 委托被强类型化为返回 bool 且仅接受两个整数参数。与任何其他方法一样，对委托的调用也是强类型化的，如果数据类型不匹配，C# 编译器会报告错误。让我们考虑一下委托在内部的工作原理。

## 委托内部

C# 将所有委托（包括 ComparisonHandler）定义为间接派生自 System.Delegate，如图 12.1.1 所示。

第一个属性的类型是 System.Reflection.MethodInfo，我将在第 17 章中介绍。MethodInfo 描述特定方法的签名，包括其名称、参数和返回值类型。此外

1. C# 标准不指定委托实现的类层次结构。但是，.NET 的实现确实间接派生自 System.Delegate。
