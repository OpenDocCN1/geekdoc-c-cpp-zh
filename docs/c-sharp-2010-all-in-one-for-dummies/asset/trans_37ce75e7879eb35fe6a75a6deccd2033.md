
- 你不再需要像这个类头那样，指定你的集合类实现IEnumerator：

```csharp
public class LinkedList                     // No longer need ': IEnumerator' here
```

## 嗯，当然，事情并没有那么简单

这里难免会有一些可能的“坑”：

- 你必须确保从列表开头开始迭代。

为了实现这一点，新的LinkedList类添加了一个数据成员currentNode，用于跟踪迭代器在列表中的进度。（该成员以前驻留在LinkedListIterator类中。）currentNode成员初始为null，因此迭代器需要检查它。如果为null，则设置currentNode指向列表的头节点。除非head本身为null（列表为空），否则在其余迭代过程中currentNode现在非null。当迭代器最终到达列表末尾时，它确实返回null，这向foreach循环发出停止信号。

- 遍历列表的每一步都需要执行MoveNext()以前所做的工作——前进到下一个节点；因此就有了while循环：

```csharp
// This does what MoveNext() did.
while(currentNode != null)
{
    // This does what Current did.
    yield return currentNode....;      // Portions omitted for a moment
    currentNode = currentNode.forward;
}
```

大多数迭代器块实现都采用循环来遍历集合——有时甚至是内部的foreach循环。（但StringChunks表明这并不是唯一的方法。）

- 当你遍历列表并开始yield return数据时，你必须深入LLNode对象内部提取其存储的数据。列表节点只是一个用于存储字符串、整数、Student等的容器。它要求你yield return的不是currentNode，而是这个：

```csharp
yield return currentNode.Data;          // Now complete
currentNode = currentNode.forward;
```

在底层，原始的枚举器也是这样做的。LLNode的Data属性以object形式返回节点的数据。当时在泛型出现之前的糟糕年代，我特意将原始的非泛型链表设计得尽可能通用。因此它存储对象。

现在，带有yield break语句的while循环正在完成你过去需要付出更多努力才能完成的工作，而由此生成的GetEnumerator()方法与foreach配合使用，就像之前在Main()中一样。

仔细想想，这个实现只是将旧的自定义迭代器类LinkedListIterator的功能移到了LinkedList类本身。可以说，这一切都掩盖在迭代器块之下。

在底层，foreach会为你进行必要的类型转换（假设这是合法的转换）。因此，如果你在列表中存储了字符串，你的foreach循环看起来像这样：

```csharp
foreach(string s in llc)  // foreach does the cast for you here.
{
    Console.WriteLine(s);
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_189_0.png)

关于本章链表的泛型版本（带有迭代器块枚举器），请参阅本书网站上的GenericLinkedListContainer示例。（此处未显示。）该示例演示了如何为string和int实例化泛型LinkedList。你会喜欢在调试器中逐步执行该示例，看看foreach是如何工作的。作为比较，请参阅System.Collections.Generic命名空间中新的内置LinkedList<T>类。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_189_1.png)

抛开整个非泛型集合世界——除了古老而优秀的数组，它当然仍然非常有用且类型安全。使用泛型集合。（当然，我将在下一节中违背这个建议。）

## 还有一个棘手的问题

LinkedList中的原始迭代器实现将其迭代器实现为一个独立的迭代器类，作为LinkedList的伴生类。这种设置有一个很好的特性，而我在前一节中描述的迭代器块版本现在缺少这个特性：你可以轻松地创建多个迭代器对象实例，并让每个实例对链表进行独立的迭代。因此，当iterator2刚刚开始时，iterator1可能已经遍历到列表的一半。

但本章的下一个示例解决了这个问题（尽管是针对更简单的集合，而不是LinkedList）。IteratorBlockIterator坚持使用独立的伴生迭代器对象，可以密切访问集合的内部值。但该迭代器对象本身是使用迭代器块实现的：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_189_2.png)

```csharp
// In file Program.cs:
// IteratorBlockIterator -- Implements a separate iterator object as a
//    companion to a collection class, a la LinkedList, but
//    implements the actual iterator with an iterator block
using System;
using System.Collections;
namespace IteratorBlockIterator
{
    class Program
    {
        // Create a collection and use two iterator objects to iterate
        // it independently (each using an iterator block).
        static void Main(string[] args)
        {
            string[] strs = new string[] { "Joe", "Bob", "Tony", "Fred" };
            MyCollection mc = new MyCollection(strs);

            // Create the first iterator and start the iteration.
            MyCollectionIterator mci1 = mc.GetEnumerator();
            foreach (string s1 in mci1) // Uses the first iterator object
            {
                // Do some useful work with each string.
                Console.WriteLine(s1);

                // Find Tony's boss.
                if (s1 == "Tony")
                {
                    // In the middle of that iteration, start a new one, using
                    // a second iterator, repeated for each outer loop pass.
                    MyCollectionIterator mci2 = mc.GetEnumerator(); // Uses the second iterator object
                    foreach (string s2 in mci2)
                    {
                        // Do some useful work with each string.
                        if (s2 == "Bob")
                        {
                            Console.WriteLine("\t{0} is {1}'s boss", s2, s1);
                        }
                    }
                }
            }

            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }

    // A simple collection of strings
    public class MyCollection
    {
        // Implement collection with an old-fashioned ArrayList.
        // Internal, so separate iterator object can access the strings.
        internal ArrayList _list = new ArrayList();

        public MyCollection(string[] strs)
        {
            foreach (string s in strs)
            {
                _list.Add(s);
            }
        }

        // GetEnumerator -- As in LinkedList, returns one of your
        // iterator objects.
        public MyCollectionIterator GetEnumerator()
        {
            return new MyCollectionIterator(this);
        }
    }

    // MyCollectionIterator -- The iterator class for MyCollection
    // (MyCollection is in a separate file.)
    public class MyCollectionIterator
    {
        // Store a reference to the collection.
        private MyCollection _mc;

        public MyCollectionIterator(MyCollection mc)
        {
            this._mc = mc;
        }
    }
}
```

```csharp
// GetEnumerator -- This is the iterator block, which carries
//     out the actual iteration for the iterator object.
public System.Collections.IEnumerator GetEnumerator()
{
    // Iterate the associated collection's underlying list,
    // which is accessible because it's declared internal.
    foreach (string s in _mc._list)
    {
        yield return s;    // The iterator block's heart
    }
}
```

`IteratorBlockIterator`中的集合并不值得大书特书：一个简单的类，包装了一个字符串`ArrayList`。它的`GetEnumerator()`方法只是简单地返回伴生迭代器类的一个新实例，就像`LinkedList`中一样：

```csharp
// GetEnumerator -- As in LinkedList, returns one of your
//     iterator objects.
public MyCollectionIterator GetEnumerator()
{
    return new MyCollectionIterator(this);
}
```

有趣的是那个迭代器类的内部。它也包含一个`GetEnumerator()`方法。这个方法使用迭代器块实现，负责完成迭代工作。下面是这个方法：

```csharp
// GetEnumerator -- This is the iterator block, which carries
//     out the actual iteration for the iterator object.
public System.Collections.IEnumerator GetEnumerator()
{
    // Iterate the associated collection's underlying list,
    // which is accessible because it's declared internal.
    foreach (string s in _mc._list)
    {
        yield return s;    // The iterator block's heart
    }
}
```

这个方法可以访问伴生集合中包含的`ArrayList`，因此它的`yield return`语句可以依次返回每个字符串。

但关键在于`Main()`方法，其中创建了两个迭代器对象的副本。第二个`foreach`循环嵌套在第一个`foreach`循环中，因此输出看起来像这样：

```
Joe
Bob
Tony

Fred    Bob is Tony's boss
```

