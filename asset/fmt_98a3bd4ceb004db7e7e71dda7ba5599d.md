
https://msdn.microsoft.com/library/system.collections.generic

集合类具有其实现的接口所指定的许多功能。一旦你了解如何使用几个集合（如 `List`、`Dictionary`、`LinkedList` 和 `SortedDictionary`），你就可以通过在线文档和示例代码了解如何使用其他集合。

| 类 | 实现的接口 | 描述 |
| --- | --- | --- |
| **System 命名空间** | | |
| Array | IList | 所有泛型数组的基类。见第 21.3 节。 |
| **System.Collections.Generic 命名空间** | | |
| Dictionary<K, V> | IDictionary<K, V> | 泛型无序键值对集合，可以通过键快速访问。见第 17.9.2 节。 |
| LinkedList<T> | ICollection<T> | 泛型双链表。见第 21.5 节。 |
| List<T> | IList | 基于数组的泛型列表。见第 9.4 节。 |
| Queue<T> | ICollection<T> | 泛型先进先出（FIFO）集合。有关队列的信息请见第 19.6 节。 |
| SortedDictionary<K, V> | IDictionary<K, V> | 一个在二叉树中对键的字典。见第 21.4 节。 |
| SortedList<K, V> | IDictionary<K, V> | 与 `SortedDictionary` 类似，但在内部使用数组。如果数据在插入 `SortedList` 之前已经存在并排序，则其插入速度比 `SortedDictionary` 快。如果数据未排序，则在 `Dictionary` 中插入更快。 |
| Stack<T> | ICollection<T> | 泛型后进先出（LIFO）集合。有关栈的信息请见第 19.5 节。 |
| **System.Collections 命名空间的旧版集合** | | |
| ArrayList | IList | 模拟传统数组，但会根据元素数量扩大或缩小。 |

**图 21.2** | 某些 .NET Framework 集合类。（第一部分，共 2 部分）。

# 第 21 章 泛型集合：使用 LINQ/PLINQ 进行函数式编程

| 类 | 实现的接口 | 描述 |
| --- | --- | --- |
| BitArray | ICollection | 内存高效位数组，其中每个位的 0 或 1 代表布尔值 `false` 或 `true`。练习 21.4 要求你使用 `BitArray` 实现埃拉托斯特尼筛法来寻找质数。 |
| Hashtable | IDictionary | 无序的键值对集合，可以通过键快速访问。 |
| Queue | ICollection | 先进先出（FIFO）集合。有关队列的信息请见 19.6 节。 |
| SortedList | IDictionary | 按键排序的键值对集合，可以通过键或索引访问。 |
| Stack | ICollection | 后进先出（LIFO）集合。有关栈的信息请见 19.5 节。 |

图 21.2 | .NET Framework 集合类。（第二部分，共 2 部分）。

我们还讨论了 `IEnumerator<T>` 接口。尽管这些枚举器有不同的实现，但它们都实现了 `IEnumerable<T>`，以便应用程序可以遍历集合。在下一节中，我们将从枚举器和数组操作能力开始讨论。本章介绍了基础的数组处理能力。所有数组都继承自抽象类 `Array` (System)；此类定义了 `Length`，它指定了数组中的元素数量。此外，`Array` 提供了静态方法——例如，`Array` 方法可以反转数组或指定范围内元素的顺序。要查看 `Array` 类静态方法的完整列表：

> https://msdn.microsoft.com/library/system.array

图 21.3 展示了 `Array` 类的几个静态方法。

```c
// Fig. 21.3: UsingArray.cs
// 用于常用数组操作的 Array 类静态方法。
using System;
using static System.Array;
```

图 21.3 | 用于常用数组操作的 Array 类静态方法。（第一部分，共 3 部分）。

```csharp
using System;
// System;
class UsingArray
{
    private static int[] intValues = {1, 2, 3, 4, 5, 6};
    private static double[] doubleValues = {8.4, 9.3, 0.2, 7.9, 3.4};
    private static int[] intValuesCopy;
    static void Main()
    {
        intValuesCopy = new int[intValues.Length]; // 默认为零
        Console.WriteLine("Initial array values:\n");
        PrintArrays(); // 输出初始数组内容
        sort doubleValues
        Sort(doubleValues); // 对 Array 方法 Sort 的无限定调用
        // 将 intValues 复制到 intValuesCopy
        Array.Copy(intValues, intValuesCopy, intValues.Length);
        Console.WriteLine("\Array values after Sort and Copy:\n");
        PrintArrays(); // 输出数组内容
        Console.WriteLine();
        // 在 intValues 中搜索 5
        int result = Array.BinarySearch(intValues, 5);
        Console.WriteLine(result >= 0 ? "5 found in intValues" : "5 not found in intValues");
        // 在 intValues 中搜索 8763
        result = Array.BinarySearch(intValues, 8763);
        Console.WriteLine(result >= 0 ? "8763 found at element in intValues" : "8763 not found in intValues");
    }
}
```

图 21.3 | 用于常用数组操作的 Array 类静态方法。（第二部分，共 3 部分）。

```csharp
Console.Write("\nValues: ");
// 使用 enumerator 遍历 int 数组
enumerator = intValues.GetEnumerator();
while (enumerator.MoveNext()) {
    Console.Write($"{enumerator.Current}");
}
Console.Write("\nValuesCopy: ");
// 使用 foreach 语句遍历第二个 int 数组
foreach (var element in intValuesCopy) {
    Console.Write($"{element}");
}
Console.WriteLine();
```

初始数组值：
doubleValues: 8.4 9.3 0.2 7.9 3.4
intValues: 1 2 3 4 5 6
intValuesCopy: 0 0 0 0 0 0

执行 Sort 和 Copy 后的数组值：
doubleValues: 0.2.2 3.4 7.9 8.4 9.3
intValues: 1 2 3 4 5 6
intValuesCopy: 1 2 3 4 5 6

在 intValues 的元素 4 处找到 5
在 intValues 中未找到 8763

> 图 21.3 | 用于常用数组操作的 Array 类静态方法。（3 部分中的 3 部分）

## 21.3.1 C# using static 指令

第 3 行和第 5 行的指令使用了命名空间 System（用于 Array 和 Console）和 System.Collections（用于接口 Enumerator，稍后我们将讨论）。第 4 行引入了 C# 6 的 `using static` 指令，用于无需完全限定名称即可访问类型的静态成员——在此情况下为 Array 类的静态成员。第 23 行

```csharp
Sort(doubleValues); // 对 Array 静态方法 Sort 的未限定调用
```

显示了对 Array 静态 Sort 的未限定调用，它等同于
```csharp
Array.Sort(doubleValues); // 调用 Array 静态方法 Sort
```

虽然我们也可以对 Array 的所有静态成员使用未限定调用（例如第 26 行的 Copy 以及第 33 和第 39 行的 BinarySearch），但使用完全限定的方法调用代码更具可读性，这清晰地表明了哪个类包含泛型方法。

## 21.3 Array 类和 Enumerator

### 21.3.2 Array 类的静态字段

我们的类声明了静态数组变量（10–12）。前两行分别将 intValues 和 doubleValues 初始化为 int 数组和 double 数组；`static int intValuesCopy` 用于演示 Array 的 Copy 方法——它初始为 `null`，因此它不引用任何数组。

第 17 行将 intValues 初始化为与 arrayValues 长度相同的数组。第 20 行调用 PrintArrays 方法（46–77）来输出所有三个数组的内容。我们稍后会讨论 PrintArrays 方法。图 21.3 的输出显示 intValuesCopy 的每个元素都被初始化为默认值 0。

### 21.3.3 Array 方法 Sort

第 23 行使用静态数组方法 Sort 对 doubleValues 进行升序排序。数组中的元素必须实现 `IComparable` 接口（所有简单类型都实现了），这使得 Sort 方法能够比较元素以确定它们的顺序。

### 21.3.4 Array 方法 Copy

第 26 行使用静态数组方法 Copy 将元素从 intValues 复制到数组 intValuesCopy。第一个参数是源数组（intValues），第二个参数是目标数组（intValuesCopy），第三个参数是表示要复制的元素数量（在本例中，`intValues.Length` 指定了所有元素）。Array 类还提供了复制数组部分内容的重载。

### 21.3.5 Array 方法 BinarySearch

第 39 行和第 30 行调用静态方法 BinarySearch 对数组 intValues 执行二分查找。BinarySearch 方法接收要搜索的排序数组以及要搜索的键。该方法返回键在数组中未找到（或返回负数）的索引。BinarySearch 假设它接收的是一个排序后的数组。它在未排序数组上的行为是未定义的。第 18 章将详细讨论搜索。

### 21.3.6 Array 方法 GetEnumerator 和接口 IEnumerator

PrintArrays 方法（46–77）使用 Array 类遍历数组的元素。Array 类实现了 `IEnumerator`（`IEnumerable<T>` 的非泛型版本）。所有数组都继承自 Array，因此 `int[]` 和数组类型都实现了 `IEnumerator` 方法 `GetEnumerator`，它返回一个可以迭代集合的 enumerator——此方法始终返回一个位于第一个元素之前的 enumerator。接口 `IEnumerator` 定义了 `MoveNext` 和属性 `Current`：

- `MoveNext` 将 enumerator 移动到集合中的下一个元素。第一次调用 `MoveNext` 将 enumerator 移动到集合的第一个元素——如果存在元素，`MoveNext` 返回 `true`；否则方法返回 `false`。
- `Reset` 方法将 enumerator 置于集合的第一个元素之前。
- 属性 Current 返回集合中当前位置的对象（由上一次调用 `MoveNext` 决定）。

Enumerator 不能修改集合的内容，只能获取内容。

![](img/57baed2319be0bb1b5f98674846f2711_890_0.png)

### 常见编程错误 21.1

> 在创建集合的 enumerator 后修改该集合，该 enumerator 将立即失效。

在创建集合的 enumerator 后修改该集合，该 enumerator 将立即失效。

## 负载因子

负载因子影响哈希方案的性能。负载因子是哈希表中存储的对象数量与哈希表总单元数之比。随着这个比例的增加，冲突的概率往往会增加。

# 性能提示 21.1

哈希表中的负载因子是空间/时间权衡的经典示例；通过增加负载因子，我们可以获得更好的内存利用，但由于哈希冲突增加，应用程序运行得更慢。通过降低负载因子，由于哈希冲突减少，我们可以获得更速度，但由于哈希表大部分保持为空，我们的内存利用率会较低。

# 哈希函数

哈希函数执行计算以确定数据在哈希表中的位置。哈希函数被应用于对象键值对中的键。任何对象都可以作为键。因此，由于所有对象都继承自类对象方法 `GetHashCode`，大多数类都是哈希表键的候选者，例如 `string` 类，它重写了此方法以针对特定类型执行高效的哈希值计算。

## 21.4.2 使用 SortedDictionary 集合

.NET Framework 提供了 `IDictionary<K,V>`（图 21.1 描述）的字典实现。图 21.4 中的应用程序演示了泛型类 `SortedDictionary`。与实现哈希表的 `Dictionary` 不同，`SortedDictionary` 将其键值对存储在二叉搜索树中（在第 19.7 节引入）。正如类名所示，`SortedDictionary` 中的条目按键排序。对于实现了 `IComparable<T>` 的键类型，`SortedDictionary` 使用 `IComparable<T>.CompareTo` 的结果对键进行排序。尽管有这些实现细节，但我们对 `Dictionary` 和 `SortedDictionary` 使用相同的公共方法、属性和字典。在许多场景下，这些类是可交换的——这就是面向对象编程的魅力所在。

# 性能提示 21.2

由于 `SortedDictionary` 将其元素保持在二叉树中排序，获取或插入键值对需要 `O(log n)` 时间，与线性搜索后再插入相比，这是非常快的。

```csharp
// 图 21.4: SortedDictionaryTest.cs
// 应用程序统计字符串中每个单词出现的次数
// 并将其存储在泛型排序字典中。
using System;
using System.Text.RegularExpressions;
using System.Collections.Generic;
```

图 21.4 | 应用程序统计字符串中每个单词出现的次数并将其存储在泛型排序字典中。（3 部分第 1 部分）。

## 21.4 字典集合

```csharp
class SortedDictionaryTest
{
    static void Main()
    {
        // 根据用户输入创建排序字典
        SortedDictionary<string, int> dictionary = CollectWords();
        DisplayDictionary(dictionary); // 显示排序字典内容
    }
    // 从用户输入创建排序字典
    private static SortedDictionary<string, int> CollectWords()
    {
        var dictionary = new SortedDictionary<string, int>();
        Console.WriteLine("Enter a string: "); // 提示输入
        string input = Console.ReadLine(); // 获取输入
        // 将文本拆分为标记
        string[] words = Regex.Split(input, @"\s+");
        // 处理输入的单词
        foreach (var word in words)
        {
            var key = word.ToLower(); // 获取小写单词
            if (dictionary.ContainsKey(key))
            {
                ++dictionary[key];
            }
            else
            {
                // 向字典添加计数为 1 的新单词
                dictionary.Add(key, 1);
            }
        }
```

