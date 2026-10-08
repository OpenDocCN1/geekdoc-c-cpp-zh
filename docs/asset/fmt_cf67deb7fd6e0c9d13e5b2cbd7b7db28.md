
```csharp
class Hand
{
public const int HandSize = 13;
    private List<PlayingCard> cards = new List<PlayingCard>(HandSize);
    ...
}
```

### 13. 找到 `AddCardToHand` 方法。

此方法目前包含对手是否已满的检查；如果没有满，则将提供的纸牌添加到 `playingCount` 指定的数组位置。

更新此方法以使用 `List<PlayingCard>` 集合的 `Add` 方法。

此更改不再需要显式跟踪集合持有多少张牌，因为你可以使用集合的 `Count` 属性。因此，从类中移除 `playingCount` 变量，并修改检查手是否满的 `if` 语句以引用集合的 `Count` 属性。

完成后的方法所示，更改部分已加粗：

```csharp
public void AddCardToHand(PlayingCard cardDealt)
{
  if (this.cards.Count >= HandSize)
  {
    throw new ArgumentException("Too many cards");
  }
  this.cards.Add(cardDealt);
}
```

# 14. 在调试菜单上，点击启动调试以编译并运行程序。

### 15. 当游戏表单出现时，点击发牌（Deal）。

> 注意 发牌按钮位于工具栏上。你可能需要展开工具栏以显示该按钮。

验证纸牌已发出，并且填充的手牌如之前所示。再次点击发牌生成另一组随机手牌。

以下图片显示了正在运行的程序：

## 卡牌游戏

| 北 | 南 | 东方 | 西方 |
| --- | --- | --- | --- |
| 黑桃 K | 六梅花 | 四梅花 | 七红桃 |
| 七梅花 | 黑桃 A | 三黑桃 | 八红桃 |
| 八梅花 | 梅花 Q | 三黑桃 | 八方形 |
| 二黑桃 | 梅花 A | 九红桃 | 方形 K |
| 七黑桃 | 八黑桃 | 十黑桃 | 五红桃 |
| 六红桃 | 梅花 K | 二梅花 | 红桃 K |
| 十红桃 | 二红桃 | 五黑桃 | 七方形 |
| 红桃 Q | 梅花 J | 四红桃 | 十方形 |
| 九梅花 | 红桃 A | 黑桃 J | 四方形 |
| 六黑桃 | 五红桃 | 黑桃 Q | 六方形 |
| 五方形 | 三红桃 | 红桃 J | 方形 A（|） |
| 四黑桃 | 九黑桃 | 方形 Q | 三方形 |

返回 Visual Studio 2017 并停止调试。

## 总结

在本章中，你学习了如何使用一些常用的集合类来存储和访问数据。特别是，你学习了如何使用泛型集合类来创建类型安全的集合。你还学习了如何创建 lambda 表达式来搜索集合中的特定项目。

- 如果你想继续阅读下一章，请保持 Visual Studio 2017 运行并转到第 19 章，“枚举集合”。
- 如果你想现在退出 Visual Studio 2017，请在“文件”菜单上点击“退出”。如果看到“另存”对话框，请点击“是”并保存项目。

## 快速参考

| 目标 | 执行此操作 |
| --- | --- |
| 创建集合 | 使用集合类的构造函数。例如： |
点击此处查看代码图像

new

```csharp
List<PlayingCard> cards = new List<PlayingCard>();
```

向集合中添加项

对于列表、哈希集合和基于字典的集合，使用 `Add` 或 `Insert` 方法（视情况定）。对于 `Queue<T>` 集合使用 `Enqueue` 方法。对于 `Stack<T>` 集合使用 `Push` 方法。例如：

点击此处查看代码图像

```csharp
HashSet<string> employees = new HashSet<string>();
employees.Add("John");
```

```csharp
LinkedList<int> data = new LinkedList<int>();
data.AddFirst(101);
```

```csharp
Stack<int> numbers = new Stack<int>();
numbers.Push(99);
```

从集合中移除项

对于列表、哈希集合和基于字典的集合，使用 `Remove` 方法。对于 `Queue<T>` 集合使用 `Dequeue` 方法。对于 `Stack<T>` 集合使用 `Pop` 方法。例如：

点击此处查看代码图像

```csharp
HashSet<string> employees = new HashSet<string>();
employees.Remove("John");
```

```csharp
LinkedList<int> data = new LinkedList<int>();
data.Remove(101);
```

```csharp
Stack<int> numbers = new Stack<int>();
int item = numbers.Pop();
```

查找集合中的元素数量

使用 `Count` 属性。例如：

点击此处查看代码图像

```csharp
List<PlayingCard> cards = new List<PlayingCard>();
int noOfCards = cards.Count;
```

定位集合中的项

对于基于字典的集合，使用数组表示法。对于列表，使用 `Find` 方法。例如：

点击此处查看代码图像

```csharp
Dictionary<string, int> ages = new Dictionary<string, int>();
ages.Add("John", 47);
int johnAge = ages["John"];
List<Person> personnel = new List<Person>(); // 注意：此处原文代码似乎有断层，按逻辑翻译
```

*修正：原文中代码块逻辑如下：*

```csharp
Dictionary<string, int> ages = new Dictionary<string, int>();
ages.Add("John", 47);
int johnAge = ages["John"];
List<Person> personnel = new List<Person>();
Person match = personnel.Find(p => p.ID == 3);
```

注意：`Stack<T>`、`Queue<T>` 和哈希集合不支持搜索，尽管你可以通过 `Contains` 方法测试哈希集合的成员性。使用 `foreach` 语句或 `for` 语句。例如：

遍历集合的元素

点击此处查看图像

```csharp
LinkedList<int> numbers = new LinkedList<int>();
for (LinkedListNode<int> node = numbers.First; node != null; node = node.Next)
{
  int number = node.Value;
  Console.WriteLine(number);
}
foreach (int number in numbers)
{
  Console.WriteLine(number);
}
```

## 19 枚举集合

完成本章后，你能够：

- 手动定义枚举器
- 实现 `IEnumerable<T>` 接口
- 提供可以步过的迭代器

但到底什么是可枚举的？简单的回答是实现了 `IEnumerable` 的集合。`IEnumerable` 接口包含一个名为 `GetEnumerator` 的方法：

`IEnumerator` 接口指定了以下属性和方法：

点击此处查看图像

```csharp
object Current { get; }
bool MoveNext();
void Reset();
```

认为枚举器是指元素的指针。初始时，指针指向元素之前。调用 `MoveNext` 方法将指针移动到下一个（第一个）元素；如果还有其他元素，`MoveNext` 方法返回 `true`，否则返回 `false`。使用 `Current` 属性访问当前指向的项目，并使用 `Reset` 方法将指针返回第一个元素。通过使用集合的 `GetEnumerator` 方法创建枚举器，反复调用 `MoveNext` 方法并使用枚举器获取值，你可以每次移动集合的元素。这正是 `foreach` 语句所做的。因此，如果你想创建自己的可枚举类，必须在你的集合中实现 `IEnumerable` 接口，并提供一个供 `GetEnumerator` 方法返回的 `IEnumerator` 实现。

> **重要** 初看起来，很容易混淆 `IEnumerable` 和 `IEnumerator` 接口，因为它们的名称非常相似。千万不要搞混。

如果你观察仔细，你会发现 `IEnumerator` 的 `Current` 属性表现出非类型安全的行为，因为它返回的是对象而不是特定类型。然而，你应该高兴的是，NET Framework 类库还提供了泛型的 `IEnumerable<T>` 接口，它的 `Current` 属性返回 `T`。同样，还有一个 `IEnumerable<T>` 接口包含一个 `GetEnumerator` 方法，该方法返回 `IEnumerator<T>` 对象。这两个接口都定义在 `System.Collections.Generic` 命名空间中，如果你正在为 .NET Framework 2.0 或更高版本构建应用程序，你应该使用这些泛型接口而不是非泛型版本。

## 手动实现枚举器

在练习中，你将定义一个实现泛型 `IEnumerable<T>` 接口的类，并为第 17 章“介绍泛型”中演示二叉树类创建一个枚举器。

递归算法（如在遍历二叉树时使用的算法）并不便于以易访问的方式在方法调用之间维护状态信息。因此，你将首先将二叉树中的数据预处理为一种更易处理的结构（队列），并实际上对该数据结构进行枚举。当然，这种巧妙的手段对于遍历二叉树元素的的用户来说是隐藏的！

### 创建 TreeEnumerator 类

- 1. 如果 Visual Studio 2017 尚未运行，请启动它。
- 2. 打开 BinaryTree 解决方案，它位于你“文档”文件夹中的 `Microsoft Press\VCSBS\Chapter 19\BinaryTree` 文件夹中。该解决方案包含第 17 章中创建的 BinaryTree 项目的可运行副本。你将向此项目添加一个新类以实现 BinaryTree 类的枚举器。
- 3. 在“解决方案管理器”中，点击 BinaryTree 项目。在“项目”菜单上，点击“添加类”打开“新建项 - BinaryTree”对话框。在中间窗格中，选择“类”模板，在“名称”框中输入 `TreeEnumerator.cs`，然后点击“添加”。
- 4. `TreeEnumerator` 类将为 `Tree<TItem>` 对象生成一个枚举器。为了确保类的类型安全，你必须提供一个参数并实现 `IEnumerator<...>` 接口。此外，该类型必须是类所枚举的 `Tree<TItem>` 对象的有效类型，因此它必须限制实现 `IComparable<TItem>` 接口（BinaryTree 类要求树中的项提供一种用于排序比较的方法）。

在显示 `TreeEnumerator.cs` 文件的代码和文本编辑器中，修改 `TreeEnumerator` 类的定义以满足这些要求，如下例中的粗体所示：

点击此处查看代码图像

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
  IComparable<TItem>
{}
```

- 5. 在 `TreeEnumerator<TItem>` 类中添加后续代码中加粗所示的以下三个私有变量：

点击此处查看代码图像

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
  IComparable<TItem>
{
  private Tree<TItem> currentData = null;
  private TItem currentItem = default(TItem);
  private Queue<TItem> enumData = null;
}
```

`currentData` 变量将用于持有被枚举树的引用，`currentItem` 变量将持有由 `Current` 属性返回的值。你用从树节点中提取出的值填充 `enumData` 队列，而 `MoveNext` 方法将依次从该队列中返回每个项。`default` 关键字将在本章稍后的“使用类型参数初始化变量”节中解释。

- 6. 为 `TreeEnumerator<TItem>` 类添加一个接受 `Tree<TItem>` 参数 `data` 的构造函数。在构造函数体中，添加粗体语句将 `currentData` 变量初始化为 `data`：

点击此处查看代码图像

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
  IComparable<TItem>
{
  public TreeEnumerator(Tree<TItem> data)
  {
    this.currentData = data;
  }
}
```

- 7. 在 `TreeEnumerator<TItem>` 类中，紧接构造函数添加以下加粗所示的名为 `populate` 的私有方法：

点击此处查看代码图像

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
  IComparable<TItem>
{
  public TreeEnumerator(Tree<TItem> data)
  {
    this.currentData = data;
  }
  private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
  {
    if (tree.LeftTree != null)
    {
      populate(enumQueue, tree.LeftTree);
    }

    enumQueue.Enqueue(tree);

    if (tree.RightTree != null)
    {
      populate(enumQueue, tree.RightTree);
    }
  }
}
```

此方法 `populate` 遍历二叉树并将其项添加到队列中。`MoveNext` 的逻辑与第 17 章描述的 `Tree<TItem>` 类中的 `NodeData` 方法相似，不同在于它并不返回数据，而是将项入队。

- 8. 返回到 `TreeEnumerator` 的定义。在类声明处，悬停在 `IEnumerator` 上，点击灯泡图标，并选择“实现接口”。
- 9. 检查生成的代码。`MoveNext` 方法只是抛出了 `NotImplementedException`。
- 10. 更新 `MoveNext` 的体，将 `throw NotImplementedException()` 替换为以下代码：

点击此处查看代码图像

```cs
bool MoveNext()
{
    if (this.enumData == null)
    {
        enumData = new Queue<TItem>();
        populate(enumData, currentData);
    }

    if (this.enumData.Count > 0)
    {
        currentItem = enumData.Dequeue();
        return true;
    }

    return false;
}
```

枚举器 `MoveNext` 的目的实际上有两个。当它第一次被调用时，它初始化队列并调用 `populate` 方法用数据填充它（在调用 `MoveNext` 之前，`Current` 返回的值是未定义的且会导致异常）。在这种情况下，初始化过程包括实例化队列并调用 `populate` 方法。随后的 `MoveNext` 调用将一直移动直到没有项，出队列项直到队列为空。记住，`MoveNext` 更新枚举器的内部状态（即将 `currentItem` 设置为从队列中提取的项）以供 `Current` 属性使用，如果有下一个值则返回 `true`，否则返回 `false`。

- 11. 修改通用 `Current` 属性的 `get` 访问器定义，将表达式成员替换为以下粗体代码：

点击此处查看代码图像

```cs
TItem IEnumerator<TItem>.Current
{
    get
    {
        if (this.enumData == null)
        {
            throw new InvalidOperationException("MoveNext before calling Current");
        }
        return this.currentItem;
    }
}
```

> **重要** 请确保将代码添加到正确的 `Current` 实现中。保留通用 `System.Collections.IEnumerator.Current` 抛出 `NotImplementedException` 的默认实现。
