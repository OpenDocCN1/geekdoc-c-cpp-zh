
12. `Hand` 类当前使用名为 `cards` 的数组来保存手牌的扑克牌。将 `cards` 变量的定义修改为 `List<PlayingCard>` 集合，如此处加粗所示：

Click here to view code image

```
class Hand
{
    public const int HandSize = 13;
    private List<PlayingCard> cards = new List<PlayingCard>(HandSize);
    ...
}
```

13. 找到 `AddCardToHand` 方法。

此方法当前检查手牌是否已满；如果未满，它会将作为参数提供的牌添加到 `cards` 数组中 `playingCardCount` 变量指定的索引处。

更新此方法以改用 `List<PlayingCard>` 集合的 `Add` 方法。

此更改也消除了显式跟踪集合中牌数的必要性，因为你可以使用 `cards` 集合的 `Count` 属性。因此，从类中删除 `playingCardCount` 变量并修改检查手牌是否已满的 `if` 语句，使其引用 `cards` 集合的 `Count` 属性。

完成的方法应如下所示，其中更改以加粗突出显示：

Click here to view code image

```
public void AddCardToHand(PlayingCard cardDealt)
{
    if (this.cards.Count >= HandSize)
    {
        throw new ArgumentException("Too many cards");
    }
    this.cards.Add(cardDealt);
}
```

- 14. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。
- 15. 当 Card Game 表单出现时，单击 Deal。

**注意**：Deal 按钮位于命令栏上。你可能需要展开命令栏以显示该按钮。

验证牌是否已发牌并且填充的手牌如前所示。再次单击 Deal 以生成另一组随机手牌。以下图像显示了正在运行的应用程序：

### Card Game

- North
- King of Diamonds
- Ten of Diamonds
- Four of Hearts
- Queen of Hearts
- Six of Hearts
- Five of Hearts
- Five of Clubs
- Jack of Diamonds
- Two of Spades
- Three of Diamonds
- Three of Hearts
- Ten of Spades
- King of Clubs

- South
- Ace of Spades
- Ace of Clubs
- Eight of Diamonds
- Ace of Hearts
- Six of Clubs
- Seven of Clubs
- Eight of Clubs
- Queen of Spades
- Four of Spades
- King of Hearts
- King of Spades
- Ten of Hearts
- Nine of Diamonds

- East
- Ace of Diamonds
- Jack of Spades
- Queen of Diamonds
- Nine of Hearts
- Ten of Clubs
- Six of Spades
- Two of Clubs
- Three of Spades
- Two of Diamonds
- Eight of Spades
- Jack of Hearts
- Two of Hearts
- Jack of Clubs

- West
- Five of Spades
- Nine of Clubs
- Seven of Hearts
- Seven of Diamonds
- Seven of Spades
- Five of Diamonds
- Four of Clubs
- Nine of Spades
- Six of Diamonds
- Eight of Hearts
- Three of Clubs
- Queen of Clubs
- Four of Diamonds

16. 返回 Visual Studio 2015 并停止调试。

### Summary

在本章中，你学习了如何使用一些常见的集合类来存储和访问数据。特别是，你学习了如何使用泛型集合类来创建类型安全的集合。你还学习了如何创建 lambda 表达式以在集合中搜索特定项。

- 如果你想继续下一章，请保持 Visual Studio 2015 运行并转到第 19 章，“Enumerating collections。”
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

### Quick reference

| 操作 | 执行方法 |
|---|---|
| 创建一个新的集合 | 使用集合类的构造函数。例如：<br>`List<PlayingCard> cards = new List<PlayingCard>();` |
| 向集合添加一项 | 对列表、哈希集和字典型集合，使用适当的 `Add` 或 `Insert` 方法。对 `Queue<T>` 集合使用 `Enqueue` 方法。对 `Stack<T>` 集合使用 `Push` 方法。例如：<br>`HashSet<string> employees = new HashSet<string>();`<br>`employees.Add("John");`<br>`...`<br>`LinkedList<int> data = new LinkedList<int>();`<br>`data.AddFirst(101);`<br>`...`<br>`Stack<int> numbers = new Stack<int>();`<br>`numbers.Push(99);` |
| 从集合中移除一项 | 对列表、哈希集和字典型集合使用 `Remove` 方法。对 `Queue<T>` 集合使用 `Dequeue` 方法。对 `Stack<T>` 集合使用 `Pop` 方法。例如：<br>`HashSet<string> employees = new HashSet<string>();`<br>`employees.Remove("John");`<br>`...`<br>`LinkedList<int> data = new LinkedList<int>();`<br>`data.Remove(101);`<br>`...`<br>`Stack<int> numbers = new Stack<int>();`<br>`...`<br>`int item = numbers.Pop();` |
| 查找集合中的元素数量 | 使用 `Count` 属性。例如：<br>`List<PlayingCard> cards = new List<PlayingCard>();`<br>`...`<br>`int noOfCards = cards.Count;` |
| 在集合中定位一项 | 对字典型集合，使用数组下标。对列表，使用 `Find` 方法。例如：<br>`Dictionary<string, int> ages = new Dictionary<string, int>();`<br>`ages.Add("John", 47);`<br>`int johnsAge = ages["John"];`<br>`...`<br>`List<Person> personnel = new List<Person>();`<br>`Person match = personnel.Find(p => p.ID == 3);`<br>注意：`Stack<T>`、`Queue<T>` 和哈希集集合类不支持搜索，尽管你可以通过使用 `Contains` 方法来测试某项是否在哈希集中。 |
| 遍历集合中的元素 | 使用 `for` 语句或 `foreach` 语句。例如：<br>`LinkedList<int> numbers = new LinkedList<int>();`<br>`...`<br>`for (LinkedListNode<int> node = numbers.First; node != null; node = node.Next)`<br>`{`<br>`    int number = node.Value;`<br>`    Console.WriteLine(number);`<br>`}`<br>`...`<br>`foreach (int number in numbers)`<br>`{`<br>`    Console.WriteLine(number);`<br>`}` |

# 第 19 章。枚举集合

完成本章后，你将能够：

- 手动定义一个枚举器，用于遍历集合中的元素。
- 通过创建迭代器自动实现枚举器。
- 提供额外的迭代器，以不同顺序遍历集合中的元素。

第 10 章“使用数组”和第 18 章“使用集合”展示了如何使用数组和集合类来保存数据序列或集合。第 10 章还详细介绍了 `foreach` 语句，你可以使用它来遍历集合中的元素。在这些章节中，你将 `foreach` 语句用作访问数组或集合内容的一种快速便捷方式，但现在是时候了解此语句实际工作原理的更多内容了。当你定义自己的集合类时，此主题变得很重要，本章将描述如何使集合可枚举。

## 枚举集合中的元素

第 10 章展示了使用 `foreach` 语句列出简单数组中项目的示例。代码如下所示：

```
int[] pins = { 9, 3, 7, 2 };
foreach (int pin in pins)
{
    Console.WriteLine(pin);
}
```

`foreach` 结构提供了一种优雅的机制，大大简化了你需要编写的代码，但它只能在特定情况下使用——你只能使用 `foreach` 来遍历可枚举集合。

那么什么是可枚举集合呢？简短的回答是，它是一个实现了 `System.Collections.IEnumerable` 接口的集合。

### 注意

> 请记住，C# 中的所有数组实际上都是 `System.Array` 类的实例。`System.Array` 类是一个实现了 `IEnumerable` 接口的集合类。

`IEnumerable` 接口包含一个名为 `GetEnumerator` 的方法：

```
IEnumerator GetEnumerator();
```

`GetEnumerator` 方法应返回一个实现了 `System.Collections.IEnumerator` 接口的枚举器对象。枚举器对象用于遍历集合的元素。`IEnumerator` 接口指定了以下属性和方法：

```
object Current { get; }
bool MoveNext();
void Reset();
```

可以将枚举器视为指向列表中元素的指针。最初，指针指向第一个元素之前。你调用 `MoveNext` 方法将指针向下移动到列表中的下一个（第一个）项目；`MoveNext` 方法应返回 `true` 如果确实还有另一项，返回 `false` 如果没有。你使用 `Current` 属性访问当前指向的项目，并使用 `Reset` 方法将指针返回到列表中第一个项目之前。通过使用集合的 `GetEnumerator` 方法创建枚举器，反复调用 `MoveNext` 方法，并使用枚举器检索 `Current` 属性的值，你可以一次一个地向前移动集合中的元素。这正是 `foreach` 语句所做的。因此，如果你想创建自己的可枚举集合类，你必须在集合类中实现 `IEnumerable` 接口，并且还提供 `IEnumerator` 接口的实现，以便由集合类的 `GetEnumerator` 方法返回。

### 重要

乍一看，很容易将 `IEnumerable` 和 `IEnumerator` 接口混淆，因为它们的名字如此相似。请务必不要混淆它们。

如果你仔细观察，你会注意到 `IEnumerator` 接口的 `Current` 属性表现出非类型安全行为，因为它返回 `object` 而不是特定类型。然而，你应该很高兴知道 Microsoft .NET Framework 类库还提供了泛型 `IEnumerator<T>` 接口，其 `Current` 属性返回 `T` 而不是对象。同样，还有一个包含返回 `Enumerator<T>` 对象的 `GetEnumerator` 方法的 `IEnumerable<T>` 接口。这两个接口都定义在 `System.Collections.Generic` 命名空间中，如果你为 .NET Framework 版本 2.0 或更高版本构建应用程序，你应该在定义可枚举集合时使用这些泛型接口而不是非泛型版本。

## 手动实现枚举器

在以下练习中，你将定义一个类来实现泛型 `IEnumerator<T>` 接口，并为第 17 章“介绍泛型”中演示的二叉树类创建一个枚举器。

第 17 章说明了遍历二叉树并显示其内容是多么容易。因此，你会倾向于认为定义一个以相同顺序检索二叉树中每个元素的枚举器将是微不足道的事。可悲的是，你会弄错。主要问题是，在定义枚举器时，你需要记住你在结构中的位置，以便后续对 `MoveNext` 方法的调用可以适当地更新位置。递归算法，例如在遍历二叉树时使用的算法，并不适合以易于访问的方式在方法调用之间维护状态信息。因此，你将首先将二叉树中的数据预处理为更易于处理的数据结构（队列），并实际枚举此数据结构。当然，这种狡猾对遍历二叉树元素的用户是隐藏的！

## 创建 TreeEnumerator 类

1. 如果尚未运行，请启动 Microsoft Visual Studio 2015。
2. 打开 `BinaryTree` 解决方案，该解决方案位于你的文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 19\BinaryTree` 文件夹中。此解决方案包含你在第 17 章中创建的 `BinaryTree` 项目的工作副本。你将在此项目中添加一个新类，以实现 `BinaryTree` 类的枚举器。
3. 在解决方案资源管理器中，单击 `BinaryTree` 项目。在 Project 菜单上，单击 Add Class 以打开 Add New Item – BinaryTree 对话框。在中间窗格中，选择 Class 模板，在 Name 框中键入 `TreeEnumerator.cs`，然后单击 Add。

`TreeEnumerator` 类为 `Tree<TItem>` 对象生成枚举器。为了确保类是类型安全的，你必须提供类型参数并实现 `IEnumerator<T>` 接口。此外，类型参数必须是 `Tree<TItem>` 对象有效类型，以便类可以枚举它，因此它必须受约束以实现 `IComparable<TItem>` 接口（`BinaryTree` 类要求树中的项目提供用于排序目的的比较手段）。

4. 在显示 `TreeEnumerator.cs` 文件的代码和文本编辑器中，修改 `TreeEnumerator` 类的定义以满足这些要求，如以下示例中以粗体显示的那样：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
}
```

5. 将以下三个私有变量添加到 `TreeEnumerator<TItem>` 类中，如以下代码中以粗体所示：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    private Tree<TItem> currentData = null;
    private TItem currentItem = default(TItem);
    private Queue<TItem> enumData = null;
}
```

`currentData` 变量将用于保存正在枚举的树的引用，而 `currentItem` 变量将保存 `Current` 属性返回的值。你将使用从树中节点提取的值填充 `enumData` 队列，并且 `MoveNext` 方法将依次从该队列返回每个项目。`default` 关键字在本章后面“使用类型参数定义变量的初始化”部分中进行了说明。

6. 向 `TreeEnumerator<TItem>` 类添加一个接受名为 `data` 的 `Tree<TItem>` 参数的构造函数。在构造函数的正文中，添加一条语句将 `currentData` 变量初始化为 `data`：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }
}
```

7. 在构造函数之后立即向 `TreeEnumerator<TItem>` 类添加以下名为 `populate` 的私有方法：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
    {
        if (tree.LeftTree != null)
        {
            populate(enumQueue, tree.LeftTree);
        }
        enumQueue.Enqueue(tree.NodeData);
        if (tree.RightTree != null)
        {
            populate(enumQueue, tree.RightTree);
        }
    }
}
```

