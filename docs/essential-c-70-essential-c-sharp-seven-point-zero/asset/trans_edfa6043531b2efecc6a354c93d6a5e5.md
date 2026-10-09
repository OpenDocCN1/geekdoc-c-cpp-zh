

## 高级主题

### 自定义字典相等性比较

为了判断给定的键是否与字典中任何现有键匹配，字典必须能够对两个键进行相等性比较。这与列表必须能够比较两个元素以确定其顺序的方式类似。（示例参见本章前面题为“自定义集合排序”的高级主题。）默认情况下，值类型的两个实例通过检查它们是否包含完全相同的数据进行比较，而引用类型的两个实例则通过检查它们是否引用同一个对象进行比较。然而，在某些情况下，即使两个实例不是完全相同的值或完全相同的引用，也可能会需要能够比较它们是否相等。

例如，假设你希望使用列表 17.2 中的 `Contact` 类型创建一个 `Dictionary<Contact, string>`。但是，你希望任何两个 `Contact` 对象只要拥有相同的姓氏和名字即被视为相等，而无论这两个对象是否在引用上相等。就像你可以提供 `IComparer<T>` 的实现来对列表进行排序一样，你也可以类似地提供 `IEqualityComparer<T>` 的实现来确定两个键是否应被视为相等。该接口要求两个方法：一个返回两个元素是否相等，另一个返回字典可用于促进快速索引的“哈希代码”。列表 17.8 展示了一个示例。

### 列表 17.8：实现 IEqualityComparer<T>

```csharp
using System;
using System.Collections.Generic;

class ContactEquality : IEqualityComparer<Contact>
{
    public bool Equals(Contact x, Contact y)
    {
        if (Object.ReferenceEquals(x, y))
            return true;
        if (x == null || y == null)
            return false;
        return x.LastName == y.LastName &&
               x.FirstName == y.FirstName;
    }

    public int GetHashCode(Contact x)
    {
        if (Object.ReferenceEquals(x, null))
            return 0;
        int h1 = x.FirstName == null ? 0 : x.FirstName.GetHashCode();
        int h2 = x.LastName == null ? 0 : x.LastName.GetHashCode();
        return h1 * 23 + h2;
    }
}
```

要创建一个使用此相等性比较器的字典，你可以使用构造函数 `new Dictionary<Contact, string>(new ContactEquality)`。

## 入门主题

### 相等性比较的要求

如第 10 章所述，相等性和哈希代码算法有一些重要的规则。在集合上下文中，符合这些规则至关重要。就像正确地对列表进行排序需要自定义顺序比较提供全序一样，哈希表也需要自定义相等性比较满足某些保证。最重要的要求是，如果 `Equals()` 对两个对象返回 true，那么 `GetHashCode()` 必须对这两个对象返回相同的值。请注意，反之则不然：两个不相等的项可能拥有相同的哈希代码。（事实上，由于只有 $2^{32}$ 种可能的哈希代码，而不相等的对象数量超过了这个数字，因此*必须*存在两个不相等的项拥有相同的哈希代码！）

第二重要的要求是对同一项进行两次 `GetHashCode()` 调用必须产生相同的结果，至少在该项位于哈希表中期间。但是，请注意，两个“看起来相等”的对象在程序的两次独立运行中并不要求给出相同的哈希代码。例如，完全合法的情况是，某个联系人今天被分配了一个哈希代码，两周后当你第二次运行程序时，“相同”的联系人被赋予了不同的哈希代码。不要将哈希代码持久化到数据库并期望它们在程序的不同运行中保持稳定。

理想情况下，`GetHashCode()` 的结果应该看起来是随机的。也就是说，输入的小幅变化应该导致输出的大幅变化，并且结果应该大致均匀地分布在所有可能的整数值中。然而，要设计一个极其快速且产生分布极好的输出的哈希算法是困难的；尽量找到一个好的折中点。

最后，`GetHashCode()` 和 `Equals()` 不应抛出异常。请注意列表 17.8 中的代码如何仔细处理以避免引用空引用，例如。

总结来说，以下是关键原则：

-   相等的对象必须具有相等的哈希代码。
-   对象的哈希代码在其实例的生命周期内不应改变（至少在它位于哈希表中时）。
-   哈希算法应快速生成分布良好的哈希值。
-   哈希算法应避免在所有可能的对象状态下抛出异常。

## 排序集合：SortedDictionary<TKey, TValue> 和 SortedList<T>

排序集合类（见图 17.4）按照 `SortedDictionary<TKey, TValue>` 的键和 `SortedList<T>` 的值对元素进行排序存储。如果我们将列表 17.7 中的代码修改为使用 `SortedDictionary<string, string>` 而不是 `Dictionary<string, string>`，程序的输出如输出 17.4 所示。

```
OUTPUT 17.4
Error
Information
Verbose
Warning
```

请注意，元素是按键排序的，而不是按值排序的。

由于排序集合必须额外工作以维持元素的排序顺序，因此插入和删除通常比无序字典中值的插入和删除稍慢。

由于排序集合必须按特定顺序存储其项，因此可以通过键和索引访问值。要通过排序列表中的索引访问键或值，使用 **Keys** 和 **Values** 属性。它们分别返回 **IList<TKey>** 和 **IList<TValue>** 实例；结果集可以像其他列表一样进行索引。

![](img/ef6a8a417630b222bfb3f3b949facff0_734_0.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_734_1.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_734_2.png)

图 17.4：排序集合

## 栈集合：Stack<T>

第 12 章讨论了栈集合类（见图 17.5）。栈集合类被设计为后进先出（LIFO）集合。两个关键方法是 `Push()` 和 `Pop()`。

-   `Push()` 将元素插入到集合中。元素不需要唯一。
-   `Pop()` 按添加的相反顺序移除元素。

![](img/ef6a8a417630b222bfb3f3b949facff0_735_0.png)

图 17.5：Stack<T> 类图

要访问栈上的元素而不修改栈，你可以使用 `Peek()` 和 `Contains()` 方法。`Peek()` 方法返回 `Pop()` 将获取的下一个元素。

与大多数集合类一样，你使用 `Contains()` 方法来确定栈中是否存在某个元素。与所有集合一样，也可以使用 foreach 循环来迭代栈中的元素。这允许你访问栈中任何位置的值。但是，请注意，通过 foreach 循环访问值不会将其从栈中移除——只有 `Pop()` 提供此功能。

## 队列集合：Queue<T>

队列集合类，如图 17.6 所示，与栈集合类完全相同，除了它们遵循先进先出（FIFO）的顺序模式。队列中不使用 `Pop()` 和 `Push()` 方法，而是使用 `Enqueue()` 和 `Dequeue()` 方法。队列集合的行为像一根管道：你使用 `Enqueue()` 方法将对象放入队列的一端，并使用 `Dequeue()` 方法从另一端移除它们。与栈集合类一样，对象不需要唯一，并且队列集合类会根据需要自动增加大小。当队列缩小时，它不一定重新占用之前使用的存储空间，因为这样会使插入新元素可能更加昂贵。但是，如果你恰好知道队列将在很长一段时间内保持相同的大小，你可以通过使用 `TrimToSize()` 方法提示它你希望回收存储空间。

![](img/ef6a8a417630b222bfb3f3b949facff0_736_0.png)

