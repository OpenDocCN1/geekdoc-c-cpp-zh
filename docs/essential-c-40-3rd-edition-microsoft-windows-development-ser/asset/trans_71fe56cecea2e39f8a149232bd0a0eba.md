
请注意，不能为匿名类型使用集合初始化器，因为集合初始化器需要构造函数调用，且无法命名构造函数。解决方法是定义一个类似 `static List<T> CreateList<T>(T t) { return new List<T>(); }` 的方法。方法类型推断允许类型参数被推导而非显式指定，因此此解决方案成功允许创建匿名类型的集合。

初始化匿名类型集合的另一种方法是使用数组初始化器。由于无法在构造函数中指定数据类型，数组初始化语法允许使用 new[] 进行匿名数组初始化（参见清单 14.4）。

### 清单 14.4：初始化匿名类型数组

```
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        var worldCup2006Finalists = new[]
        {
            new
            {
                TeamName = "France",
                Players = new string[]
                {
                    "Fabien Barthez", "Gregory Coupet",
                    "Mickael Landreau", "Eric Abidal",
                    // ...
                },
            },
            new
            {
                TeamName = "Italy",
                Players = new string[]
                {
                    "Gianluigi Buffon", "Angelo Peruzzi",
                    "Marco Amelia", "Cristian Zaccardo",
                    // ...
                },
            },
        };
        Print(worldCup2006Finalists);
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

生成的变量是匿名类型项的数组，由于它是数组，因此必须是同质的。

## 什么使类成为集合：IEnumerable<T>

根据定义，.NET 中的集合是一个至少实现 IEnumerable<T> 的类（从技术上讲，它将是非泛型类型 IEnumerable）。这个接口是关键，因为实现 IEnumerable<T> 的方法是支持遍历集合所需的最低实现要求。

第 3 章展示了如何使用 foreach 语句遍历元素数组。语法简单，避免了需要知道元素数量的复杂性。然而，运行时并不直接支持 foreach 语句。相反，C# 编译器会按本节所述转换代码。

### 与数组一起使用 foreach

清单 14.5 演示了一个简单的 foreach 循环，用于遍历整数数组，然后将每个整数打印到控制台。

### 清单 14.5：与数组一起使用 foreach

```
int[] array = new int[]{ 1, 2, 3, 4, 5, 6};
foreach (int item in array)
{
    Console.WriteLine(item);
}
```

从这段代码中，C# 编译器创建了 for 循环的 CIL 等效代码，如清单 14.6 所示。

### 清单 14.6：与数组一起使用 foreach 的编译实现

```
int number;
int[] tempArray;
int[] array = new int[]{1, 2, 3, 4, 5, 6};
tempArray = array;
for (int counter = 0; (counter < tempArray.Length); counter++)
{
    int item = tempArray[counter];
    Console.WriteLine(item);
}
```

在此示例中，请注意 foreach 依赖于 Length 属性和索引运算符 ([]) 的支持。有了 Length 属性，C# 编译器可以使用 for 语句遍历数组中的每个元素。

### 与 IEnumerable<T> 一起使用 foreach

虽然清单 14.6 中所示的代码在长度固定且始终支持索引运算符的数组上效果良好，但并非所有类型的集合都有已知的元素数量。此外，许多集合类（包括 Stack<T>、Queue<T> 和 Dictionary<TKey, TValue> 类）都不支持按索引检索元素。因此，需要一种更通用的方法来遍历元素集合。迭代器模式提供了这种功能。假设你可以确定第一个、下一个和最后一个元素，那么知道数量并支持按索引检索元素就不是必需的。

System.Collections.Generic.IEnumerable<T> 和非泛型 System.Collections.IEnumerable 接口（参见清单 14.8）旨在为遍历元素集合启用迭代器模式，而不是清单 14.6 中所示的长度-索引模式。它们关系的类图如图 14.1 所示。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_596_0.png)

### 图 14.1：IEnumerable<T> 和 IEnumerator 接口

IEnumerator 是 IEnumerable<T> 派生自的接口，包含三个成员。第一个是 bool MoveNext()。使用此方法，你可以在集合中的一个元素和下一个元素之间移动，同时检测是否已遍历完每个项。第二个成员是名为 Current 的只读属性，返回当前正在处理的元素。Current 在 IEnumerable<T> 中被重载，提供了类型特定的实现。在集合类上拥有这两个成员后，可以简单地使用 while 循环遍历集合，如清单 14.7 所示。（Reset() 方法通常会引发 NotImplementedException，因此永远不应调用。如果需要重新开始枚举，只需创建一个新的枚举器。）

### 清单 14.7：使用 while 遍历集合

```
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
int number;
// ...
// This code is conceptual, not the actual code.
while (stack.MoveNext())
{
    number = stack.Current;
    Console.WriteLine(number);
}
```

在清单 14.7 中，MoveNext() 方法在移动到集合末尾之后时返回 false。这取消了循环期间计数元素的需要。

清单 14.7 使用 System.Collections.Generic.Stack<T> 作为集合类型。存在许多其他集合类型；这只是一个示例。Stack<T> 的关键特征是其设计为后进先出（LIFO）集合。需要注意的是，类型参数 T 标识集合中所有项的类型。在集合中收集一种特定类型的对象是泛型集合的关键特征。程序员在添加、删除或访问集合中的项时，了解集合中的数据类型非常重要。

前面的示例展示了 C# 编译器输出的要点，但它并不实际以这种方式编译，因为它省略了有关实现的两个重要细节：交错和错误处理。

### 状态是共享的

清单 14.7 这样的实现的问题是，如果两个这样的循环相互交错——一个 foreach 在另一个 foreach 内部，两者都使用同一个集合——集合必须维护当前元素的状态指示器，以便在调用 MoveNext() 时可以确定下一个元素。问题是，一个交错的循环可能会影响另一个循环。（多线程执行的循环也是如此。）

为解决此问题，集合类不直接支持 IEnumerable<T> 和 IEnumerator 接口。如图 14.1 所示，存在第二个接口，称为 IEnumerable<T>，其唯一方法是 GetEnumerator()。此方法的目的是返回支持 IEnumerable<T> 的对象。集合类不再维护状态，而是由另一个类（通常是嵌套类，以便它可以访问集合的内部）支持 IEnumerable<T> 接口并保持迭代循环的状态。枚举器就像序列中的“光标”或“书签”。你可以有多个书签，移动每个书签都会独立于其他书签遍历集合。使用此模式，foreach 循环的 C# 等效代码将如清单 14.8 所示。
