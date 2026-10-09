

在能够不参考示例代码而从零开始编写事件代码之前，你可能需要进行一些练习。然而，事件是后续章节中异步、多线程编程的重要基础。

## 15
## 使用标准查询运算符的集合接口

C# 3.0 中增加的最显著功能在于集合，这归功于一个名为**语言集成查询**（LINQ）的编程 API。通过一组扩展方法和 lambda 表达式，LINQ 为处理集合提供了更优越的 API。事实上，在这本书的早期版本中，关于集合的章节紧跟在关于泛型的章节之后，并且位于关于委托的章节之前。然而，由于 lambda 表达式对 LINQ 至关重要，如果不先讲解委托（lambda 表达式的基石），就不可能再像以前那样讲解集合了。既然你在前面两章中已经对 lambda 表达式有了坚实的基础，我们现在就可以深入探讨集合的细节——这是一个横跨三章的主题。本章的重点从**标准查询运算符**开始，这是一种通过直接调用扩展方法来利用 LINQ 的手段。

在介绍集合初始化器之后，本章涵盖了各种集合接口，并探讨了它们之间的关系。这是理解集合的基础，因此你应该仔细研读相关材料。关于集合接口的章节还包括 C# 3.0 中为实施标准查询运算符而添加的 `IEnumerable<T>` 扩展方法的讲解。

![](img/ef6a8a417630b222bfb3f3b949facff0_640_0.png)

与集合相关的类和接口分为两类：支持泛型的和不支持泛型的。本章主要讨论泛型集合接口。只有在你编写需要与早期版本运行时互操作的组件时，才应使用不支持泛型的集合类。这是因为以前非泛型形式中可用的所有内容都有强类型的泛型替代方案。虽然这些概念仍然适用于两种形式，但我们不会明确讨论非泛型版本。¹

本章最后对匿名类型进行了深入的讨论——这些主题我们在第 3 章的几个高级主题章节中仅做了简要介绍。匿名类型有趣之处在于，它们被 C# 7.0 中的元组所掩盖——我们将在本章末尾进一步讨论这一主题。

### 集合初始化器

集合初始化器允许程序员在实例化时以类似于数组声明的方式构建具有初始成员集合的集合。在集合初始化可用之前，必须在集合实例化后显式地向集合添加元素——使用类似 `System.Collections.Generic.ICollection<T>` 的 `Add( )` 方法。使用集合初始化后，`Add( )` 调用是由 C# 编译器生成的，而不是由开发者明确编码的。代码清单 15.1 展示了如何使用集合初始化器来初始化集合。

**代码清单 15.1：集合初始化**

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<string> sevenWorldBlunders;
        sevenWorldBlunders = new List<string>()
        {
            // Quotes from Ghandi
            "Wealth without work",
            "Pleasure without conscience",
            "Knowledge without character",
            "Commerce without morality",
            "Science without humanity",
            "Worship without sacrifice",
            "Politics without principle"
        };

        Print(sevenWorldBlunders);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

这种语法不仅类似于数组初始化，还类似于对象初始化器，即跟随在构造函数之后的花括号。如果在构造函数中没有传入参数，则数据类型后面的括号是可选的（这与对象初始化器一样）。

集合初始化器要成功编译，需要满足一些基本要求。理想情况下，应用集合初始化器的集合类型应该是实现了 `System.Collections.Generic.ICollection<T>` 的类型。这确保了集合包含编译器生成的代码可以调用的 `Add()` 方法。然而，也存在一种放松版的要求，它仅要求存在一个或多个 `Add()` 方法，这些方法可以作为扩展方法（C# 6.0）或作为实现了 `IEnumerable<T>` 类型的实例方法——即使该集合没有实现 `ICollection<T>`。`Add()` 方法需要接受与集合初始化器中指定的值兼容的参数。

对于字典，集合初始化器语法稍微复杂一些，因为字典中的每个元素都需要键和值。这种语法如代码清单 15.2 所示。

**代码清单 15.2：使用集合初始化器初始化 Dictionary<>**

```csharp
using System;
using System.Collections.Generic;
#if !PRECsharp6
// C# 6.0 or later
Dictionary<string, ConsoleColor> colorMap =
    new Dictionary<string, ConsoleColor>
    {
        ["Error"] = ConsoleColor.Red,
        ["Warning"] = ConsoleColor.Yellow,
        ["Information"] = ConsoleColor.Green,
        ["Verbose"] = ConsoleColor.White
    };
#else
// Before C# 6.0
Dictionary<string, ConsoleColor> colorMap =
    new Dictionary<string, ConsoleColor>
    {
        { "Error", ConsoleColor.Red },
        { "Warning", ConsoleColor.Yellow },
        { "Information", ConsoleColor.Green },
        { "Verbose", ConsoleColor.White}
    };
#endif
```

此代码清单包含初始化的两个不同版本。第一个展示了 C# 6.0 中引入的新语法，通过允许赋值运算符表达哪个值与哪个键相关联，从而表达名称/值对的意图。第二种语法（在 C# 6.0 或更高版本中仍然有效）使用花括号将名称和值配对。

允许在不支持 `ICollection<T>` 的集合上使用初始化器是重要的，原因有两个。首先，大多数集合（实现了 `IEnumerable<T>` 的类型）并不同时实现 `ICollection<T>`，这大大降低了集合初始化器的实用性。其次，通过匹配方法名称和签名与集合初始化器项的兼容性，使得初始化到集合中的项目具有更大的多样性。例如，只要存在一个签名与 `a` 兼容的 `Add()` 方法以及第二个签名与 `b, c` 兼容的 `Add()` 方法，初始化器现在就可以支持 `new DataStore(){ a, {b, c}}`。

### 什么使一个类成为集合：IEnumerable<T>

根据定义，.NET 中的集合是一个至少实现了 `IEnumerable<T>`（或非泛型类型 `IEnumerable`）的类。该接口至关重要，因为实现 `IEnumerable<T>` 的方法是对集合进行迭代所需的最小条件。

第 4 章展示了如何使用 `foreach` 语句迭代元素数组。这种语法简单，避免了必须知道有多少个元素的复杂性。然而，运行时并不直接支持 `foreach` 语句。相反，C# 编译器将按照本节描述的方式转换代码。

#### 带有数组的 foreach

代码清单 15.3 演示了一个简单的 `foreach` 循环，它迭代一个整数数组，然后将每个整数打印到控制台。

**代码清单 15.3：带有数组的 foreach**

```csharp
int[] array = new int[]{1, 2, 3, 4, 5, 6};

foreach (int item in array)
{
    Console.WriteLine(item);
}
```

从这段代码中，C# 编译器创建了 `for` 循环的等效 CIL，如代码清单 15.4 所示。

**代码清单 15.4：带有数组的 foreach 的编译实现**

```csharp
int[] tempArray;
int[] array = new int[]{1, 2, 3, 4, 5, 6};

tempArray = array;
for (int counter = 0; (counter < tempArray.Length); counter++)
{
    int item = tempArray[counter];

    Console.WriteLine(item);
}
```

