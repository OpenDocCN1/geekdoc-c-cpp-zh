

# 第 19 章 自定义链式数据结构

3. 如果列表包含多个节点，创建一个 `ListNode` 变量 `current` 并将其赋值为 `firstNumber`（第 116 行）。

4. 现在使用 `current` “遍历列表”，直到它指向倒数节点之前的节点。`while` 循环（第 119–122 行）只要 `current.Next` 不等于 `lastNode`，就会将 `current.Next` 赋值给 `current`。

5. 找到倒数第二个节点后，将 `current` 赋值给 `lastNode`（第 125 行），以更新列表中的最后一个节点。

6. 将 `current.Next` 设置为 `null`（第 126 行），以从列表中移除最后一个节点，并在当前节点处终止列表。

7. 返回 `removeItem` 引用（第 129 行）。

在图 19.9 中，部分 (a) 展示了删除操作前的列表。(b) 中的虚线和箭头显示了引用的操作。

![](img/57baed2319be0bb1b5f98674846f2711_826_0.png)

图 19.9 | RemoveFromBack 操作。

# Display 方法

`Display` 方法（图 19.4, 139–161）首先确定列表是否为空（第 141 行）。如果是，`Display` 将显示一个由字符串 "Empty " 和列表名称组成的字符串，然后将 `current` 返回给调用者方法。否则，`Display` 输出列表中的数据。该方法写入一个由字符串 "The "、列表名称和字符串 " is: " 组成的字符串。然后第 149 行创建 `ListNode` 变量 `current` 并将其初始化为 `firstNumber`。只要 `current` 不为空，表示列表中还有更多项。因此，该方法反复显示 `current.Data`，然后将 `current.Next` 赋值给 `current`（第 155 行），移动到列表中的下一个节点。

# 单向链表、循环单链表和双向链表

我们一直在讨论的链表类型是单向链表——它从指向第一个节点的引用开始，每个节点包含一个指向下一个节点“序列”的引用。该列表以一个成员值为 `null` 的节点终止。单向链表只能向一个方向遍历。

循环单链表从指向第一个节点的引用开始，每个节点包含一个指向下一个节点的引用。“最后一个节点”不包含 `null` 引用；相反，最后一个节点指向回第一个节点，从而闭合了“圆”。

![](img/57baed2319be0bb1b5f98674846f2711_827_0.png)

**图 19.10** | 循环单链表。

双向链表（图 19.11）允许正向和反向遍历。这种列表通常用两个“起始引用”实现：一个指向列表的第一个元素，允许从头到尾遍历列表；另一个指向最后一个元素，允许从尾到头遍历列表。每个节点都有一个指向列表中后一个节点的**正向引用**，以及一个指向前一个节点的**反向引用**。如果你的列表包含一个按字母排序的电话簿，搜索名字开头字母靠前的人可能从列表开头开始。搜索名字开头字母靠后的人可能从末尾开始。

![](img/57baed2319be0bb1b5f98674846f2711_827_1.png)

**图 19.11** | 双向链表。

在循环双向链表（图 19.12）中，最后一个节点的正向引用指向第一个节点，第一个节点的反向引用指向最后一个节点，从而闭合了“圆”。

# 19.5 栈

栈可以被看作链表的一种受限版本——它只在顶部接收新节点和释放节点。由于这个原因，栈被称为后进先出（LIFO）数据结构。操作栈的主要操作是 `push` 和 `pop`。`push` 操作向栈顶添加一个新节点。`pop` 操作移除栈顶元素并返回数据项。

栈有许多有趣的应用。例如，当程序调用一个方法时，该方法必须知道如何返回其调用者，因此返回地址被推入方法栈。如果发生了一系列方法调用，返回值将按照先出的顺序推入栈中，以便每个方法都能返回其调用者。栈支持递归方法调用的方式与其支持非递归方法调用的方式相同。

在下一个示例中，我们利用列表和栈之间的关系，通过复用列表来实现一个类。我们展示了两种复用形式：首先，我们通过继承 `List` 来实现栈（图 19.4）。然后，我们通过组合，将一个 `List` 对象作为栈类的私有成员，以相同的方式实现栈。栈在程序执行期间会增长和缩小。

# 继承自 List 的栈类

图 19.13 中的代码通过继承 `List`（图 19.4）创建了一个栈。我们希望栈拥有 `Push`、`Pop` 和 `Empty` 方法。本质上，这些是 `List` 类的 `InsertFront`、`RemoveFront` 和 `Display` 方法。当然，`List` 类包含其他方法（如 `InsertBack` 和 `RemoveBack`），我们更希望通过栈的公共接口访问这些方法（图 19.13）。

```csharp
// 图 19.13: StackInheritance.cs
// 通过继承 List 实现栈。
using LinkedList;

namespace StackInheritance
{
    // 类 StackInheritance 继承了 List 的功能
    public class StackInheritance : List
    {
        // 将名称 "stack" 传递给构造函数
        public StackInheritance() : base("stack") { }

        // 通过插入位于栈顶的 dataValue
        // 位于链表头的 dataValue
        public void Push(object dataValue)
        {
            InsertFront(dataValue);
        }

        // 通过移除栈顶来移除
        // 位于链表头的项
        public object Pop()
        {
            return RemoveFront();
        }
    }
}
```

图 19.13 | 通过继承 List 实现栈。

我们希望栈拥有 `Push`、`Pop` 和 `Empty` 方法。本质上，这些是 `List` 类的 `InsertFront`、`RemoveFront` 和 `Display` 方法。当然，`List` 类包含其他方法（如 `InsertBack` 和 `RemoveBack`），我们更希望通过栈的公共接口访问这些方法（图 19.13）。`StackInheritance` 必须引用 `LinkedList` 库。

`StackInheritance` 的 `Main` 方法（图 19.4）使用 `StackInheritance` 创建对象（第 12 行）。第 15–18 行定义了推入栈的四个值。推入栈的操作（第 21, 23 和 25 行）推入了一个布尔值 `true`、包含 `$` 的字符、包含 `34567` 的整数和一个包含 `"hello"` 的字符串。`while` 循环（3 33–38））栈。当栈为空时，`Pop` 方法抛出 `EmptyListException`，程序显示该异常。程序使用 `Display` 方法（`StackInheritance` 继承自 `List` 类）输出每次操作后的栈。`StackInheritanceTest` 使用 `LinkedList`（图 19.4）和 `StackInheritance`（图 19.13）；因此，`StackInheritance` 的解决方案必须引用这两个类。

```csharp
// 图 19.14: StackInheritanceTest.cs
// 测试 StackInheritance 类。
using System;
using StackInheritanceLibrary;
using LinkedLibrary;

// 展示 StackInheritance 的功能
class StackInheritanceTest
{
    static void Main()
    {
        StackInheritance stack = new StackInheritance();

        // 创建存储在栈中的对象
        bool aBoolean = true;
        char aInchar = '$';
        int aInteger = 34567;
        string aString = "hello";

        // 使用方法向栈添加项
        stack.Push(aBoolean);
        stack.Display();
        stack.Push(aInchar);
        stack.Display();
        stack.Push(aInteger);
        stack.Display();
        stack.Push(aString);
        stack.Display();

        // 从栈中移除项
        try
        {
            object removedObject = stack.Pop();
            Console.WriteLine("{removedObject} popped");
            stack.Display();
        }
        catch (EmptyListException emptyList)
        {
            // 如果发生异常，写入堆栈跟踪
            Console.WriteLine(emptyList.StackTrace);
        }
    }
}
```

栈是: True
栈是: $ True
栈是: 34567 $ True
栈是: hello 34567 $ True

