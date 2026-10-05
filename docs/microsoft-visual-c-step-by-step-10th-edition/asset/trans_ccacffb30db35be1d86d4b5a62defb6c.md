
该元素，尽管你不能使用数组符号来添加新元素。然而，通常情况下，`List<T>` 类比数组提供了更大的灵活性，并设计用于克服数组表现出的以下限制：

-   如果你想调整数组的大小，必须创建一个新数组，复制元素（如果数组较小，则跳过某些元素），然后更新对原始数组的引用，使其指向新数组。
-   如果你想从数组中删除一个元素，必须将所有后续元素向上移动一个位置。即使这样做也不起作用，因为你最终会得到两个最后一个元素的副本。
-   如果你想向数组中插入一个元素，必须将元素向下移动一个位置以留出空位。然而，你会丢失数组的最后一个元素！

`List<T>` 集合的以下功能解决了这些局限性：

-   你不需要为创建的 `List<T>` 集合指定容量；它可以随着元素的添加而增长和缩小。这种动态行为会带来一定的开销，如果有必要，你可以指定初始大小。但是，如果超过了此大小，`List<T>` 集合将根据需要自动增长。
-   你可以使用 `Remove` 方法从 `List<T>` 集合中删除指定的元素。`List<T>` 集合会自动重新排列元素并关闭空隙。你还可以使用 `RemoveAt` 方法删除 `List<T>` 集合中指定位置的项。
-   你可以使用 `Add` 方法向 `List<T>` 集合的末尾添加元素。你提供要添加的元素。`List<T>` 集合会自动调整大小。
-   你可以使用 `Insert` 方法向 `List<T>` 集合的中间插入元素。同样，`List<T>` 集合会自动调整大小。
-   你可以通过调用 `Sort` 方法轻松地对 `List<T>` 对象中的数据进行排序。

> 注意
与数组一样，如果你使用 `foreach` 遍历 `List<T>` 集合，不能使用迭代变量来修改集合的内容。此外，你不能在遍历 `List<T>` 集合的 `foreach` 循环中调用 `Remove`、`Add` 或 `Insert` 方法；任何尝试都会导致 `InvalidOperationException` 异常。

以下是一个关于你如何创建、操作和遍历 `List<int>` 集合内容的示例：

点击此处查看代码图片

```
using System;
using System.Collections.Generic;
...
List<int> numbers = new List<int>();
// 使用 Add 方法填充 List<int>
foreach (int number in new int[12]{10, 9, 8, 7, 6, 5, 10, 4, 3, 2, 1})
{
    numbers.Add(number);
}

// 在列表倒数第二个位置插入元素，并将
// 最后一项向上移动
// 第一个参数是位置；第二个参数是
// 插入的值
numbers.Insert(numbers.Count-1, 99);

// 删除值为 7 的第一个元素（第 4 个元素，索引）
numbers.Remove(7);

// 删除现在的第 7 个元素
numbers.RemoveAt(6);

// 使用 for 语句遍历剩余的 11 个元素
Console.WriteLine("Iterating using a for statement:");
for (int i = 0; i < numbers.Count; i++)
{
    int number = numbers[i]; // 注意数组符号的使用
    Console.WriteLine(number);
}

// 使用 foreach 语句遍历相同的 11 个元素
Console.WriteLine("\nIterating using a foreach statement:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

这是该代码的输出结果：

点击此处查看图片

Iterating using a for statement:
10
9
8
7
6
5
4
3
2
99
1

Iterating using a foreach statement:
10
9
8
7
6
5
4
3
2
99
1

> 注意
确定 `List<T>` 集合元素数量的方法与查询数组中的项数不同。使用 `List<T>` 集合时，你检查 `Count` 属性；使用数组时，你检查 `Length` 属性。

# LinkedList<T> 集合类

`LinkedList<T>` 集合类实现了双向链表。列表中的每个项都持有该项的值，以及指向列表中下一个项（`Next` 属性）和上一个项（`Previous` 属性）的引用。列表开头的项的 `Previous` 属性设置为 `null`，列表末尾项的 `Next` 属性设置为 `null`。

与 `List<T>` 类不同，`LinkedList<T>` 不支持用于插入或交换元素的数组符号。你可以使用 `AddFirst` 方法在列表开头插入元素，将第一个项向上移动，并将其 `Previous` 属性指向新项。同样，你可以使用 `AddLast` 方法在列表末尾插入元素，将之前末尾项的 `Next` 属性指向新项。你还可以使用 `AddBefore` 和 `AddAfter` 方法在列表中的指定项之前或之后插入元素。（你必须先获取该项。）

你可以通过查询 `First` 属性来查找 `LinkedList<T>` 集合中的第一个项，查询 `Last` 则返回指向列表最后一项的引用。要遍历链表，你可以从一端开始，通过 `Next` 或 `Previous` 引用逐步步进，直到找到一个该属性值为 `null` 的项。此外，你可以使用 `foreach` 语句，它通过 `Remove`、`RemoveFirst` 和 `RemoveLast` 方法遍历 `LinkedList<T>`。

以下示例显示了 `LinkedList<T>` 集合的运行情况。注意代码如何使用 `for` 语句通过 `Next`（或 `Previous`）引用遍历列表，只有在遇到 `null` 引用（即列表结束）时才停止：

点击此处查看代码图片

```
using System;
using System.Collections.Generic;
LinkedList<int> numbers = new LinkedList<int>();
// 使用 AddFirst 方法填充 List<int>
foreach (int number in new int[] { 10, 8, 6, 4, 2 })
{
    numbers.AddFirst(number);
}
// 使用 for 语句遍历
```
Console.WriteLine("Iterating using a for statement:");
for (LinkedList<int> node = numbers.First; node != null; node = node.Next)
{
    Console.WriteLine(node.Value);
}

// 使用 foreach 语句遍历
Console.WriteLine("\nIterating using a foreach statement:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}

// 反向遍历
Console.WriteLine("\nIterating backward:");
for (LinkedList<int> node = numbers.Last; node != null; node = node.Previous)
{
    Console.WriteLine(node.Value);
}
```

这是该代码的输出结果：

点击此处查看图片

Iterating using a for statement:
10
8
6
4
2

Iterating using a foreach statement:
10
8
6
4
2

Iterating backward:
2
4
6
8
10

# Queue<T> 类

`Queue<T>` 类实现了先进先出的机制。元素在队尾插入到队列（`Enqueue` 操作），并从队首移除（`Dequeue` 操作）。

以下代码是 `Queue<int>` 及其常用操作的示例：

点击此处查看图片

```
using System;
using System.Collections.Generic;

Queue<int> numbers = new Queue<int>();

// 填充队列
Console.WriteLine("Populating the queue:");
foreach (int number in new int[]{9, 3, 7, 2})
{
    numbers.Enqueue(number);
    Console.WriteLine($"{number} has joined the queue");
}

// 遍历队列
Console.WriteLine("\nThe queue contains the following items:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}

// 清空队列
Console.WriteLine("\nDraining the queue:");
while (numbers.Count > 0)
{
    int number = numbers.Dequeue();
    Console.WriteLine($"{number} has left the queue");
}
```

这是该代码的输出结果：

点击此处查看图片

Populating the queue:
9 has joined the queue
3 has joined the queue
7 has joined the queue
2 has joined the queue
The queue contains the following items:
9
3
7
2

Draining the queue:
9 has left the queue
3 has left the queue
7 has left the queue
2 has left the queue

# PriorityQueue<TElement, TPriority> 集合类

`PriorityQueue<TElement, TPriority>` 扩展了 `Queue<T>` 类的概念，为每个队列元素关联优先级。该类接收两个参数：第一个是队列元素的类型，第二个指示优先级的类型（通常是 `int`，但可以是任何可比较类型）。元素被入到队尾，但如果它们具有更高的优先级，则比寿命更长的元素更早取出。具有相同优先级的元素的入队和出队顺序相同，与普通队列一致。

以下代码显示了一个示例，说明了不同优先级的元素如何入队和取出。优先级值越小的优先级越高（优先级为 1 的元素在优先级 2 的元素之前取出）：

点击此处查看代码图片

```
using System;
using System.Collections.Generic;
// 创建队列
// 数据项是字符串。第二个类型参数（int）
// 指示优先级
PriorityQueue<string, int> messages = new PriorityQueue<string, int>();

// 向队列添加不同优先级的消息
messages.Enqueue("Twas", 1);
messages.Enqueue("Brilling", 1);
messages.Enqueue("and", 2);
messages.Enqueue("the", 3);
messages.Enqueue("Slithy", 2);
```
