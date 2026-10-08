
```
shoppingList.Add("Milk");
shoppingList.Remove("Milk"); // 空列表
shoppingList.Add("Honey");
shoppingList.Add("Olives");
shoppingList.Add("Water");
shoppingList[2] = "A lot of " + shoppingList[2];
shoppingList.Add("Fruits");
shoppingList.RemoveAt(0); // 移除 "Honey" (第一个)
shoppingList.RemoveAt(2); // 移除 "Fruits" (最后一个)
shoppingList.Add(null);
shoppingList.Add("Beer");
shoppingList.Remove(null);
Console.WriteLine("We need to buy:");
for (int i = 0; i < shoppingList.Count; i++)
{
    Console.WriteLine("- - " + shoppingList[i]);
}
Console.WriteLine("Position of 'Beer' = {0}");
shoppingList.IndexOf("Beer");
Console.WriteLine("Position of 'Water' = {0}");
shoppingList.IndexOf("Water");
Console.WriteLine("Do we have to buy Bread? " +
shoppingList.Contains("Bread"));
```

上述代码检查了我们链表实现中的所有操作及其特殊情况（如移除第一个和最后一个元素），并证明了动态列表实现工作正常。上述代码的输出如下：

我们需要购买：

- Olives

- A lot of Water

- Beer

'Beer' 的位置 = 2

'Water' 的位置 = -1

我们必须买面包吗？ 否

## 比较静态列表和动态列表

我们通过两种方式实现了抽象数据类型 `ADT` 列表：静态（数组列表）和动态（链表）。一旦编写完成，这两种实现就可以以几乎相同的方式使用。例如，请看以下代码段（使用我们的数组列表和链表）：

### 使用 C# 的计算机编程基础

```csharp
static void Main()
{
    CustomArrayList<string> arrayList = new CustomArrayList<string>();
    arrayList.Add("One");
    arrayList.Add("Two");
    arrayList.Add("Three");
    arrayList[0] = "Zero";
    arrayList.RemoveAt(1);
    Console.WriteLine("Array list: ");
    for (int i = 0; i < arrayList.Count; i++)
    {
        Console.WriteLine(" - " + arrayList[i]);
    }

    DynamicList<string> dynamicList = new DynamicList<string>();
    dynamicList.Add("One");
    dynamicList.Add("Two");
    dynamicList.Add("Three");
    dynamicList[0] = "Zero";
    dynamicList.RemoveAt(1);
    Console.WriteLine("Dynamic list: ");
    for (int i = 0; i < dynamicList.Count; i++)
    {
        Console.WriteLine(" - " + dynamicList[i]);
    }
}
```

使用两种类型列表的结果是相同的

数组列表:

- Zero

- Three

动态列表:

- Zero

- Three

上述示例证明了某些 `ADT` 可以用几种在概念上不同的方式实现，用户可能察觉不到它们之间的差异。尽管如此，不同的实现可能有不同的性能，并占用不同的内存。

这种概念被称为**抽象行为**，是面向对象编程 `OOP` 的基础，可以通过抽象类或接口来实现，正如我们在“面向对象编程原则”章节的“抽象”节中看到的。

## 双向链表

在所谓的双向链表中，每个元素包含其**值**和**两个指针——指向前一个元素和后一个元素**（如果没有此类元素，则为 `null`）。这允许我们向前和向后遍历列表，并且某些操作可以更高效地实现。这是一个示例双向链表的样式：

![](img/251ffe19d2b15f8a8f566ab01924bb12_658_)

# C# 计算机编程基础

`List<bool> boolList = new List<bool>();`

`List<double> realNumbersList = new List<double>();`

让我们考虑 `.NET Framework` 中的一些泛型集合。

## List<T> 类

`List<T>` 是 `ArrayList` 的泛型变体。当我们创建一个 `List<T>` 对象时，我们指定了存储在列表中的元素类型，即我们用某些真实数据类型替换了被标记的 `T`（例如数字或字符串）。

让我们考虑一个创建一个整数元素列表的情况。我们可以通过以下方式实现：

```
List<int> intList = new List<int>();
```

因此，所创建的列表只能包含整数，而不能包含其他对象（例如字符串）。如果我们尝试向 `List<int>` 添加一个类型为 `string` 的对象，将会得到编译错误。通过泛型类型，C# 编译器保护我们在处理集合时不会出现错误。

## List 类 - 基于数组的实现

`List<T>` 的工作方式类似于我们的 `CustomArrayList<T>`。它将元素以数组的形式存储在内存中，该数组部分是已使用的，部分是为新元素留的空白。得益于数组中预留的空白元素，`append` 操作几乎总是能够添加新元素，而无需调整数组大小。当然，有时数组必须调整大小，但由于每次调整都会使数组大小翻倍，因此调整大小发生的频率非常低，与 `append` 操作的数量相比可以忽略不计。我们可以将 `List<T>` 想象成数组，它具有某些容量并被填充到某个程度：

![](img/251ffe19d2b15f8a8f566ab01924bb12_661_0.png)

得益于预先分配的包含 `List<T>` 类元素的数组容量，当需要快速添加元素、提取元素和通过索引访问元素时，它可以是一个极其高效的数据结构。尽管如此，插入和删除元素是非常缓慢的，除非这些元素位于最后一个。

## 第 16 章 线性数据结构

我们可以说 `List<T>` 结合了列表和数组的优点——快速添加、可变以及通过索引直接访问。

## 何时使用 List<T>？

我们已经解释过 `List<T>` 类使用内部数组来保存元素，当数组溢出时，其大小会翻倍。这种实现导致了以下优缺点：

- 通过索引搜索非常快——我们可以以相同的速度访问每个元素，无论元素数量多少。
- 通过值查找元素需要进行多次比较，其比较次数取决于元素数量（在最坏的情况下），即它是缓慢的。
- 插入和删除元素是一项缓慢的操作——当我们添加或删除元素时，特别是当它们不在数组末尾时，我们必须移动其余元素，这是一个缓慢的操作。
- 在添加新元素时，有时我们必须增加数组的容量，这是一个缓慢的操作，但这种情况发生很少，且插入 `List` 的平均速度不取决于元素的数量，即运行速度非常快。

> 当你不预期频繁插入和删除元素，但预期在在列表末尾添加新元素或通过索引访问元素时，请使用 `List<T>`。

## 给定区间内的质数 – 示例

在熟悉了列表结构的实现和 `List<T>` 类之后，让我们来看看如何使用它们。我们将考虑寻找特定区间内质数的问题。为此，我们将使用以下算法：

```
static List<int> GetPrimes(int start, int end)
{
    List<int> primeslist = new List<int>();
    for (int num = start; num <= end; num++)
    {
        bool prime = true;
        double numSq = Math.Sqrt(num);
        for (int div = 2; div <= numSq; div++)
        {
            if (num % div == 0)
            {
                prime = false;
                break;
            }
        }
        if (prime)
        {
            primesList.Add(num);
        }
    }
    return primesList;
}
static void Main()
{
    List<int> primes = GetPrimes(200, 300);
    foreach (var item in primes)
    {
        Console.Write("{0}", item);
    }
}
```

从数学上我们知道，一个数不是质数是因为它在 `[2 ... 给定数的平方根]` 区间内至少有一个因数。对于每个数字，我们在这个区间内寻找因数。如果我们找到了因数，该数就不是质数，我们可以继续处理区间中的下一个数字。通过逐渐添加质数，我们填充了列表，然后遍历并将其打印在屏幕上。上述代码的输出如下：

211 223 227 229 233 239 241 251 257 263 269 271 277 281 283 293

## 列表的并集与交集 – 示例

让我们考虑一个更有趣的例子——写一个可以找到两个数字集合并集和交集的程序。

### 并集

### 交集

![](img/251ffe19d2b15f8a8f566ab01924bb12_663_0.png)

我们可以认为有两个数字列表，我们想要获取两个集合共同拥元素（交集），或者寻找至少属于一个集合的元素（并集）。

让我们讨论该问题的一种解决方案：

```c
static List<int> Union(
    List<int> firstList, List<int> secondList)
{
    List<int> union = new List<int>();
    union.AddRange(firstList);
    foreach (var item in secondList)
    {
        if (!union.Contains(item))
        {
            union.Add(item);
        }
    }
    return union;
}

static List<int> Intersect(List<int> firstList, List<int> secondList)
{
    List<int> intersect = new List<int>();
    foreach (var item in firstList)
    {
        if (secondList.Contains(item))
        {
            intersect.Add(item);
        }
    }
    return intersect;
}

static void PrintList(List<int> list)
{
    Console.Write("{ ");
    foreach (var item in list)
    {
        Console.Write(item + " ");
    }
    Console.WriteLine("}");
}

static void Main()
{
    List<int> firstList = new List<int> { 1, 2, 3, 4, 5 };
    List<int> secondList = new List<int> { 2, 4, 6 };

    List<int> union = Union(firstList, secondList);
    Console.Write("Union: ");
    PrintList(union);

    List<int> intersection = Intersect(firstList, secondList);
    Console.Write("Intersection: ");
    PrintList(intersection);
}
```

# C# 计算机编程基础

并集 = { 1 2 3 4 5 6 }

交集 = { 2 4 }

# 将列表转换为数组及反之

在 C# 中，通过使用提供的 `ToArray()` 方法可以轻松将列表转换为数组。对于相反的操作，我们可以使用 `List<T>(System.Array)` 构造函数。让我们来看一个示例，展示它的用法：

```
static void Main()
{
    int[] arr = new int[] { 1, 2, 3 };
    List<int> list = new List<int>(arr);
    int[] convertedArray = list.ToArray();
}
```

# LinkedList<T> 类
