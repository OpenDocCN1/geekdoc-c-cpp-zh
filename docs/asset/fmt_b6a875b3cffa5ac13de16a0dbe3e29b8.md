
# 第 19 章
## 枚举集合

完成本章后，你将能够：

- 手动定义一个枚举器，并用于遍历集合中的元素。
- 通过创建迭代器来自动实现枚举器。
- 提供额外的迭代器，以不同的顺序步进集合的元素。

第 10 章“使用数组”和第 18 章“使用集合”展示了如何使用数组和集合类来存储数据序列或集合。第 10 章还详细介绍了 `foreach` 语句，你可以用它来步进或遍历集合中的元素。在这些情况下，你将 `foreach` 语句作为一种快速方便的访问数组或集合内容的方法，但现在是时候进一步学习一下该语句的实际工作原理了。当你定义自己的集合类时，这个主题变得至关重要，本章描述了如何让集合变为可枚举的。

## 枚举集合中的元素

第 10 章展示了一个使用 `foreach` 语句列出简单数组中项目的示例。代码如下：

```
int[] pins = { 9, 3, 7, 2 };

foreach (int pin in pins)
{
    Console.WriteLine(pin);
}
```

`foreach` 结构提供了一种优雅的机制，极大地简化了你需要编写的代码，但它只能在特定情况下使用：你只能使用 `foreach` 来遍历一个可枚举的集合。到底什么是可枚举集合？简单的回答是，它是一个实现了 `System.Collections.IEnumerable` 接口的集合。

> 注意
记住 C# 中的所有数组都是 `System.Array` 类的实例。`System.Array` 类是一个实现了 `IEnumerable` 接口的集合类。

`IEnumerable` 接口包含一个名为 `GetEnumerator` 的方法：

```
IEnumerator GetEnumerator();
```

`GetEnumerator` 方法应该返回一个实现 `System.Collections.IEnumerable` 接口的枚举器对象。该枚举器对象用于步进（枚举）集合的元素。`IEnumerable` 接口规定了以下属性和方法：

```
object Current { get; }
bool MoveNext();
void Reset();
```

将枚举器想象为指向列表中元素的指针。初始时，指针指向第一个元素之前。你调用 `MoveNext` 方法将指针移动到列表中的下一个（第一个）项；如果还有项，`MoveNext` 方法返回 `true`，否则则返回 `false`。使用 `Current` 属性访问当前指向的项，使用 `Reset` 方法将指针移回列表第一个项之前。通过使用集合的 `GetEnumerator` 方法创建枚举器，反复调用 `MoveNext` 方法，并使用枚举器获取 `Current` 属性的值，你可以一次一个项目地在集合元素中向前移动。这正是 `foreach` 语句的工作方式。因此，如果你想创建自己的可枚举集合类，必须在你的集合类中实现 `IEnumerable` 接口，并提供一个由集合类 `GetEnumerator` 方法返回的 `IEnumerator` 接口实现。

> **重要**
一眼看上去，很容易混淆 `IEnumerable` 和 `IEnumerator` 接口，因为它们的名称非常相似。务必不要将它们搞混。

你可能注意到 `IEnumerator` 的 `Current` 属性表现出非安全行为，因为它返回的是一个对象而不是特定类型。然而，你应该高兴地知道，Microsoft .NET 类库还提供了泛型 `IEnumerator<T>` 接口，它有一个 `Current` 属性返回 `T`。同样，还有 `IEnumerable<T>` 接口，它包含一个返回 `Enumerator<T>` 对象的 `GetEnumerator` 方法。这两个接口都定义在 `System.Collections.Generic` 命名空间（命名空间）中。如果你正在为 .NET 2.0 或更高版本构建应用程序，在定义可枚举集合时，你应该使用这些泛型接口而不是非泛型版本。

## 手动实现枚举器

在下面的练习中，你将定义一个实现泛型 `IEnumerator<T>` 接口的类，并为第 17 章“介绍泛型”中演示的二叉树创建一个枚举器。

第 17 章说明了遍历二叉树并显示其内容多么简单。因此，你可能会认为定义一个枚举器以相同顺序检索二叉树中的每个元素是一件简单的事。遗憾的是，你错了。主要问题在于定义枚举器时，你必须记住你处于一种结构中，后续对 `MoveNext` 方法的调用可以相应地更新位置。递归算法（例如遍历二叉树时使用的算法）并不便于以易访问的方式在方法调用之间维护状态信息。由于此原因，你首先将二叉树中的数据预处理为更方便的数据结构（队列），并改为枚举该数据结构。当然，遍历二叉树元素的细节对用户是隐藏的！

### 创建 TreeEnumerator 类

1. 启动 Visual Studio 2022，如果它尚未运行。
2. 打开 `BinaryTree` 解决方案，它位于 `Microsoft Press\VCS\Chapter19\BinaryTree` 文件夹。该解决方案包含了你在第 17 章创建的 `BinaryTree` 项目的副本。
3. 在解决方案管理器中，选择 `BinaryTree` 项目。然后打开项目菜单并选择“添加”以打开“新建项”对话框。
4. 在中间面板中，选择“类”模板，在名称框中输入 `TreeEnumerator.cs`，然后选择“添加”。这将为 `Tree<TItem>` 对象生成枚举器。为了确保类的安全，必须提供类型参数并实现 `IEnumerator<T>` 接口。此外，类型参数必须是枚举 `Tree<TItem>` 对象的有效类型，因此它必须被约束为 `IComparable<TItem>`。（BinaryTree 类要求项提供比较的方法）。
5. 在显示 `TreeEnumerator.cs` 文件的代码编辑器窗口中，修改 `TreeEnumerator` 类的定义以满足这些要求，如下例加粗所示：

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
}
```

> 注意
Visual Studio 将显示一些警告和错误消息，因为 `IEnumerator` 接口期望你实现尚未添加的方法和属性。你稍后会定义这些项。

6. 在 `TreeEnumerator<TItem>` 类中添加如下代码加粗的三个私有变量：

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    private Tree<TItem> currentData = null;
    private Tree<TItem> currentItem = default(TItem);
    private Queue<TItem> enumData = null;
}
```

`currentData` 变量将用于持有枚举树的引用 `currentItem` 将存储 `Current` 属性返回的值。你用从树节点中提取的值填充 `enumData` 队列，`MoveNext` 方法将依次返回队列中的每个项。

> 注意
`default` 关键字将在本节稍后的“初始化使用类型参数定义的变量”侧边栏中解释。

7. 在 `TreeEnumerator<TItem>` 类中添加一个接受 `Tree<TItem>` 参数 `data` 的构造函数。在构造函数的体中，添加加粗所示的语句将 `currentData` 变量初始化为 `data`：

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }
}
```

8. 在 `TreeEnumerator<TItem>` 类中，紧接构造函数之后添加以下**粗体**所示名为 `populate` 的私有方法：

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }
    private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
    {
        if (tree.LeftTree is not null)
        {
            populate(enumQueue, tree.LeftTree);
        }
        enumQueue.Enqueue(tree.NodeData);
        if (tree.RightTree is not null)
        {
            populate(enumQueue, tree.RightTree);
        }
    }
}
```

该方法遍历二叉树，并将其中包含的数据添加到队列中。使用的算法与第 17 章中描述的 `Tree<TItem>` 类中的 `WalkTree` 方法类似。主要区别在于，该方法不是将 `NodeData` 值附加到字符串，而是将这些值存储在队列中。

返回 `IEnumerator<TItem>` 类的定义。然而在类声明中，将鼠标悬停在文本 `IEnumerator<TItem>` 上。在出现的下拉上下文菜单中（带有灯泡图标），选择“**显式实现所有成员**”。这将为 `IEnumerator<TItem>` 接口和 `IEnumerator` 接口中的方法生成实现，并将它们添加到类的末尾。它还会为 `IDisposable` 接口生成 `Dispose` 方法。

> 注意
`IEnumerator<TItem>` 接口继承自 `IEnumerator` 和 `IDisposable` 接口，这就是为什么它们的方法也会出现。事实上，属于 `IEnumerator<TItem>` 接口的唯一项是泛型属性 `Current`。`MoveNext` 和 `Reset` 方法属于非泛型的 `IEnumerator` 接口。第 14 章“使用垃圾收集和资源管理”描述了 `IDisposable` 接口。

检查生成的代码。属性和方法的主体包含默认实现，该实现仅抛出 `NotImplementedException`。你将在接后的步骤中替换这些代码。

更新 `MoveNext` 方法的主体，并将 `throw new NotImplementedException()` 语句替换为此处**粗体**所示的代码。

```
bool IEnumerator.MoveNext()
{
    if (this.enumData is null)
{
  this.enumData = new Queue<TItem>();
  populate(this.enumData, this.currentData);
}
if (this.enumData.Count > 0) {
  this.currentItem = this.enumData.Dequeue();
  return true;
}
return false;
}
```

`MoveNext` 方法的作用有两个。当它被第一次调用时，它初始化枚举器使用的数据，并移动到第一个要返回的数据上。（在第一次调用 `MoveNext` 之前，`Current` 属性返回的值是未定义的，并且会导致异常。）在这种情况下，初始化过程包括实例化队列，然后调用 `populate` 方法用从树中提取的数据填充队列。

对 `MoveNext` 方法的后续调用将遍历数据项，直到没有剩余项，如本例所示，从队列中取出项直到队列为空。请记住，`MoveNext` 实际上并不返回数据项；那是 `Current` 属性的。所有 `MoveNext` 更新都是更新枚举器中的内部状态（即变量 `onItem` 的值被设置为从队列中提取的数据项），供 `Current` 属性使用，如果存在下一个值则返回 `true`，否则返回 `false`。

12. 修改泛型属性 `Current` 的 `get` 访问器（get accessor）定义，并将表达式的主体成员替换为此处**粗体**所示的代码：

```
TItem IEnumerator<TItem>.Current {
  get {
    if (this.enumData == null)
{
  throw new InvalidOperationException("在调用 Current 之前使用 MoveNext");
    }
  return this.currentItem;
  }
}
```

> **重要**
> 确保将代码添加到 `Current` 属性的正确实现中。保留非泛型版本 `System.Collections.Enumerator.Current` 的默认实现，该实现抛出 `NotImplementedException` 异常。

`Current` 属性检查 `enumData` 变量以确保已调用了 `MoveNext`。在第一次调用 `MoveNext` 之前，该变量为 `null`。如果不是如此，该属性将抛出 `InvalidOperationException`。这是 .NET 用于表示当前状态无法执行操作的惯机制。如果已经调用了 `MoveNext`，它将更新 `currentItem` 变量，因此 `Current` 属性只需要返回该变量中的值。

1. 找到 `IDisposable.Dispose` 方法。按照后续代码注释掉 `throw new NotImplementedException();` 语句。枚举器没有任何需要显式释放的资源，因此此方法不需要执行任何操作。但它必须存在。关于 `Dispose` 方法的更多信息，请参阅第 14 章。

```
void IDisposable.Dispose()
{
  // throw new NotImplementedException();
}
```

14. 生成解决方案，如果报告了错误，请进行纠正。

### 初始化使用类型参数定义的变量

你应该已经注意到定义初始化 `currentItem` 的语句使用了 `default` 关键字：

```
private TItem currentItem = default(TItem);
```

`currentItem` 变量使用类型参数 `TItem` 定义。当编写并编译程序时，替换 `TItem` 的实际类型可能未知；只有在代码执行时才能解决此问题。这使得难以指定初始化。

倾向于将其设置为 `null`。然而，如果替换 `TItem` 的值类型，这种赋值是不允许的（你不能将值类型设置为 null）。

还有其他可能性，例如 TItem 可能是布尔值。`default` 关键字解决了这个问题。在语句执行时将确定使用的值。如果 `TItem` 是引用类型，`default(TItem)` 返回 `null`；如果 `TItem` 是数值，返回 `0`；如果 `TItem` 是布尔值，返回 `false`。如果 `TItem` 是结构体，则以相同的方式初始化。（引用字段被设置为 `null`，数值字段被设置为 `0`，布尔字段被设置为 `false`。）

## 实现 IEnumerator 接口

在接下来的练习中，你将修改二叉树类来实现 `IEnumerable<T>` 接口。`GetEnumerator` 方法将返回一个 `TreeEnumerator<TItem>` 对象。

### 在 Tree<TItem> 类中实现 IEnumerable<TItem>

1. 在解决方案管理器中，双击 `Tree.cs` 文件以在代码文本编辑器中显示 `Tree<TItem>` 类。
2. 修改 `Tree<TItem>` 类的定义，使其实现 `IEnumerable<TItem>` 接口，如下代码粗体所示：

```
public class Tree<TItem> : IEnumerable<TItem> where TItem : IComparable<TItem>
```

注意约束始终放在类定义的最后。

> 与 `TreeEnumerator` 类一样，你会收到一些错误消息和警告，因为 `IEnumerable` 接口某些你尚未定义的方法和属性。你可以暂时忽略这些消息。

3. 将鼠标悬停在类定义中的 `IEnumerable<TItem>` 接口上。在出现的下拉菜单中，选择“**显式实现所有成员**”。这将为 `IEnumerable<TItem>.GetEnumerator` 和 `IEnumerable.GetEnumerator` 方法生成实现并将它们添加到类中。（因为泛型 `IEnumerable<TItem>` 接口继承自 `IEnumerable`，所以非泛型的 `IEnumerable` 接口方法也被实现了。）
4. 找到类末尾附近的泛型 `IEnumerable<TItem>.GetEnumerator` 方法。修改 `GetEnumerator()` 方法的主体，替换现有的 `throw` 语句，如下例中的**粗体**部分所示：

```
IEnumerable<TItem> IEnumerable<TItem>.GetEnumerator()
{
```
