
采用与集合初始化器中指定的值兼容的参数。

对于字典，集合初始化器语法稍微复杂一些，因为字典中的每个元素都需要键和值。该语法如清单14.4所示。

**清单14.4：初始化字典**

```csharp
using System;
using System.Collections.Generic;
#if !PRECSHARP6
    // C# 6.0 or Later
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

此清单实际包含两个不同版本的初始化。第一个演示了C# 6.0引入的新语法，它通过允许赋值运算符来表达哪个值与哪个键关联，从而说明名称/值对的意图。第二种语法（在C# 6.0或更高版本中仍然有效）使用花括号将名称和值配对在一起。

允许在不支持`ICollection<T>`的集合上使用初始化器之所以重要，有两个原因。首先，大多数集合（实现`IEnumerable<T>`的类型）并不实现`ICollection<T>`，这大大降低了集合初始化器的实用性。其次，根据方法名和签名与集合初始化器项的兼容性进行匹配，使得初始化到集合中的项更具多样性。例如，只要有一个`Add()`方法的签名与参数`a`兼容，并且有第二个`Add()`方法的签名与`b`、`c`兼容，初始化器现在就可以支持`new DataStore(){ a, {b, c}}`。

请注意，不能为匿名类型提供集合初始化器，因为集合初始化器需要构造函数调用，而无法命名构造函数。解决办法是定义一个方法，例如`static List<T> CreateList<T>(T t) { return new List<T>(); }`。方法类型推断允许隐式推断类型参数，而不是显式指定，因此这种方法可以成功创建匿名类型的集合。

初始化匿名类型集合的另一种方法是使用数组初始化器。由于无法在构造函数中指定数据类型，数组初始化语法允许使用`new[]`进行匿名数组初始化（见清单14.5）。

**清单14.5：初始化匿名类型数组**

```csharp
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
                }
            },
            new
            {
                TeamName = "Italy",
                Players = new string[]
                {
                    "Gianluigi Buffon", "Angelo Peruzzi",
                    "Marco Amelia", "Cristian Zaccardo",
                    // ...
                }
            }
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

结果变量是匿名类型项的数组，由于是数组，该项的类型必须是同类型的。

## 类成为集合的条件：`IEnumerable<T>`

根据定义，.NET中的集合是一个至少实现了`IEnumerable<T>`（或非泛型类型`IEnumerable`）的类。该接口至关重要，因为实现`IEnumerable<T>`的方法是为支持集合迭代所需的最低要求。

第3章展示了如何使用foreach语句遍历元素数组。该语法简单，避免了必须知道元素数量的复杂性。然而，运行时并不直接支持foreach语句。相反，C#编译器会将代码转换为本节所述的形式。

### foreach与数组

清单14.6演示了一个简单的foreach循环，它遍历一个整数数组，然后控制台输出每个整数。

**清单14.6：foreach与数组**

```csharp
int[] array = new int[]{1, 2, 3, 4, 5, 6};

foreach (int item in array)
{
    Console.WriteLine(item);
}
```

从这段代码，C#编译器会生成一个等效的CIL for循环，如清单14.7所示。

**清单14.7：foreach与数组的编译实现**

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

在此示例中，注意foreach依赖于对`Length`属性和索引运算符（`[]`）的支持。有了`Length`属性，C#编译器就可以使用`for`语句遍历数组中的每个元素。

### foreach与`IEnumerable<T>`

虽然清单14.7中的代码在长度固定且始终支持索引运算符的数组上效果很好，但并非所有类型的集合都有已知的元素数量。此外，许多集合类，包括`Stack<T>`、`Queue<T>`和`Dictionary<TKey, TValue>`类，不支持按索引检索元素。因此，需要一种更通用的遍历元素集合的方法。迭代器模式提供了这种能力。假设你可以确定第一个、下一个和最后一个元素，则无需知道计数和按索引检索元素。

`System.Collections.Generic.IEnumerator<T>`和非泛型接口`System.Collections.IEnumerator`（见清单14.9）旨在启用迭代器模式来遍历元素集合，而不是清单14.7中所示的长度-索引模式。它们的关系类图如图14.1所示。

![](img/25683ccec0773ba5b8794b11f2b12877_622_0.png)

**图14.1：** `IEnumerator<T>`和`IEnumerator`接口的类图

`IEnumerator<T>`派生于`IEnumerator`，包含三个成员。第一个是`bool MoveNext()`。使用此方法，你可以从集合中的一个元素移动到下一个元素，同时检测是否已枚举完所有项目。第二个成员是一个名为`Current`的只读属性，返回当前正在处理的元素。`Current`在`IEnumerator<T>`中重载，提供了类型特定的实现。有了集合类中的这两个成员，就可以像清单14.8所示的那样，简单地使用while循环迭代集合。（`Reset()`方法通常会抛出`NotImplemented`异常，因此不应调用它。如果需要重新开始枚举，只需创建一个新的枚举器。）

**清单14.8：使用while迭代集合**

```csharp
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

在清单14.8中，`MoveNext()`方法在移动过集合末尾时返回false。这取代了循环时计数元素的需要。

清单14.8使用`System.Collections.Generic.Stack<T>`作为集合类型。存在许多其他集合类型；这只是一个例子。`Stack<T>`的关键特性是其被设计为“后进先出”（LIFO）集合。注意，类型参数`T`标识了集合中所有项的类型。在集合中收集某一种特定类型的对象是泛型集合的关键特征。程序员在添加、删除或访问集合中的项时，必须知道集合中的数据类型。

