

图19.1列出了命名空间`System.Collections.Generic`中的一些集合接口，这些接口在`System.Collections`中也有基于对象的旧式对应版本。许多集合类都实现了这些接口。你也可以根据自己的需求提供特定的实现。

| 接口 | 描述 |
|---|---|
| `IEnumerable<T>` | 一个可枚举的对象——例如，`foreach`循环可以遍历此类对象的元素。该接口包含一个方法`GetEnumerator`，它返回一个`IEnumerator<T>`对象，该对象（如你将在19.3节看到的）可用于遍历集合。实际上，`foreach`在幕后使用的是集合的`IEnumerator<T>`对象。`ICollection<T>`扩展了`IEnumerable<T>`，因此所有集合类都直接或间接地实现了`IEnumerable<T>`。 |
| `ICollection<T>` | 接口`IList<T>`和`IDictionary<K,V>`继承自该接口。包含一个`Count`属性用于确定集合的大小，一个`CopyTo`方法用于将集合内容复制到传统数组，以及一个`IsReadOnly`属性。 |
| `IList<T>` | 一个有序集合，可以像数组一样进行操作。提供`[]`运算符（称为索引器）用于通过int索引访问元素。还包含用于搜索和修改集合的方法，包括`Add`、`Remove`、`Contains`和`IndexOf`。 |
| `IDictionary<K,V>` | 一个值的集合，通过类型为K的任意“键”对象进行索引。提供索引器（`[]`）按键访问元素，以及修改集合的方法（例如`Add`、`Remove`）。`IDictionary<K,V>`的`Keys`属性包含所有键，`Values`属性包含所有存储的值。 |

**图19.1** | 一些常见的泛型集合接口。

## 命名空间`System.Collections.Generic`

使用`System.Collections.Generic`命名空间中的集合，你可以指定集合中存储的确切类型。与基于对象的旧式集合相比，这提供了两个关键优势：

- *编译时类型检查*确保你正在使用与集合匹配的适当类型，否则编译器会发出错误消息。
- 从泛型集合中检索到的任何项都具有正确的类型。对于基于对象的集合，检索到的任何项都作为对象返回。然后，你必须*显式强制转换*该对象为程序操作所需的类型。如果引用对象不具有适当的类型，这可能会导致执行时出现`InvalidCastException`异常。

泛型集合对于存储值类型特别有用，因为它们消除了基于对象的旧式集合所需的装箱和拆箱开销。

在本章中，我们继续讨论数据结构和集合，介绍额外的内置数组功能，以及泛型`SortedDictionary`和`LinkedList`类。命名空间`System.Collections.Generic`还提供了许多其他数据结构，包括`Stack<T>`、`Queue<T>`和`SortedList<K,V>`（一个按键排序的键值对集合，可以通过键或索引访问）。图19.2总结了众多集合类——完整列表请访问

```
https://msdn.microsoft.com/library/system.collections.generic
```

集合类具有由类实现的接口指定的许多常见功能。一旦你知道如何使用几个集合（如`List`、`Dictionary`、`LinkedList`和`SortedDictionary`），你就可以通过它们的在线文档（包含示例代码）来弄清楚如何使用其他集合。

| 类 | 实现接口 | 描述 |
|---|---|---|
| *System命名空间* |  |  |
| Array | IList | 所有传统数组的基类。参见19.3节。 |
| *System.Collections.Generic命名空间* |  |  |
| Dictionary<K, V> | IDictionary<K, V> | 一个泛型、无序的键值对集合，可以通过键快速访问。参见17.9.2节。 |
| LinkedList<T> | ICollection<T> | 一个泛型双向链表。参见19.5节。 |
| List<T> | IList<T> | 一个基于数组的泛型列表。参见9.4节。 |
| Queue<T> | ICollection<T> | 一个泛型先进先出（FIFO）集合。 |
| SortedDictionary<K, V> | IDictionary<K, V> | 一个在二叉树中按键对数据进行排序的字典。参见19.4节。 |
| SortedList<K, V> | IDictionary<K, V> | 类似于`SortedDictionary`，但在内部使用数组。如果数据在插入集合之前已经存在并排序，则插入`SortedList`比`SortedDictionary`更快。如果数据未排序，则插入`SortedDictionary`更快。 |
| Stack<T> | ICollection<T> | 一个泛型后进先出（LIFO）集合。 |
| *System.Collections命名空间的旧式集合* |  |  |
| ArrayList | IList | 模拟传统数组，但会根据需要增长或缩小以适应元素数量。 |

**图19.2** | 一些.NET框架集合类。（第1部分，共2部分。）

| 类 | 实现接口 | 描述 |
|---|---|---|
| BitArray | ICollection | 一个内存高效的位数组，其中每个位的0或1值表示bool值false或true。 |
| Hashtable | IDictionary | 一个无序的键值对集合，可以通过键快速访问。 |
| Queue | ICollection | 一个先进先出（FIFO）集合。 |
| SortedList | IDictionary | 一个按键排序的键值对集合，可以通过键或索引访问。 |
| Stack | ICollection | 一个后进先出（LIFO）集合。 |

**图19.2** | 一些.NET框架集合类。（第2部分，共2部分。）

我们还讨论了`IEnumerator<T>`接口。每个集合类的枚举器允许你遍历集合。虽然这些枚举器有不同的实现，但它们都实现了`IEnumerator<T>`接口，以便应用程序可以遍历集合的元素（例如，使用foreach语句）。在下一节中，我们通过研究枚举器和数组操作的功能来开始讨论。集合类直接或间接实现`ICollection<T>`和`IEnumerable<T>`（或其基于对象的等效接口`ICollection`和`IEnumerable`，用于旧式集合）。

### 19.3 类Array与枚举器

第8章介绍了基本的数组处理功能。所有数组都隐式继承自抽象基类Array（`System`命名空间）；该类定义了属性`Length`，用于指定数组中的元素数量。此外，类`Array`还提供了提供数组处理算法的`static`方法。通常，类`Array`会重载这些方法——例如，`Array`的`Reverse`方法可以反转整个数组或指定元素范围中的元素顺序。有关类`Array`的`static`方法的完整列表，请访问

> https://msdn.microsoft.com/library/system.array

图19.3演示了类`Array`的几个`static`方法。

```csharp
1  // Fig. 19.3: UsingArray.cs
2  // Array class static methods for common array manipulations.
3  using System;
4  using static System.Array;
```

**图19.3** | 用于常见数组操作的Array类静态方法。（第1部分，共3部分。）

```csharp
using System.Collections;
// demonstrate algorithms of class Array
class UsingArray
{
    private static int[] intValues = {1, 2, 3, 4, 5, 6};
    private static double[] doubleValues = {8.4, 9.3, 0.2, 7.9, 3.4};
    private static int[] intValuesCopy;

    // method Main demonstrates class Array's methods
    static void Main()
    {
        intValuesCopy = new int[intValues.Length]; // defaults to zeroes

        Console.WriteLine("Initial array values:\n");
        PrintArrays(); // output initial array contents

        // sort doubleValues
        Sort(doubleValues); // unqualified call to Array static method Sort

        // copy intValues into intValuesCopy
        Array.Copy(intValues, intValuesCopy, intValues.Length);

        Console.WriteLine("\nArray values after Sort and Copy:\n");
        PrintArrays(); // output array contents
        Console.WriteLine();

        // search for 5 in intValues
        int result = Array.BinarySearch(intValues, 5);
        Console.WriteLine(result >= 0 ?
            "5 found at element {0} in intValues" :
            "5 not found in intValues");

        // search for 8763 in intValues
        result = Array.BinarySearch(intValues, 8763);
        Console.WriteLine(result >= 0 ?
            "8763 found at element {0} in intValues" :
            "8763 not found in intValues");
    }

    // output array content with enumerators
    private static void PrintArrays()
    {
        Console.Write("doubleValues: ");

        // iterate through the double array with an enumerator
        IEnumerator enumerator = doubleValues.GetEnumerator();

        while (enumerator.MoveNext())
        {
            Console.Write($"{enumerator.Current} ");
        }
    }
}
```

