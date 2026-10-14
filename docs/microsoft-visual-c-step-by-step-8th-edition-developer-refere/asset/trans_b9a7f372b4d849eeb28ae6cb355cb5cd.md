

```
IComparable<TItem>
{
}
```

5. 将以下三个私有变量添加到 TreeEnumerator<TItem> 类中，如以下代码中以粗体所示：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    private Tree<TItem> currentData = null;
    private TItem currentItem = default(TItem);
    private Queue<TItem> enumData = null;
}
```

currentData 变量将用于保存正在枚举的树的引用，而 currentItem 变量将保存 Current 属性返回的值。你将使用从树中节点提取的值填充 enumData 队列，并且 MoveNext 方法将依次从该队列返回每个项目。default 关键字在本章后面“使用类型参数定义变量的初始化”部分中进行了说明。

6. 向 TreeEnumerator<TItem> 类添加一个接受名为 data 的 Tree<TItem> 参数的构造函数。在构造函数的正文中，添加一条语句将 currentData 变量初始化为 data：

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

7. 在构造函数之后立即向 TreeEnumerator<TItem> 类添加以下名为 populate 的私有方法：

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
    {
        if (tree.LeftTree != null)
        {
```

```
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

此方法遍历二叉树，将其包含的数据添加到队列中。使用的算法与 Tree<TItem> 类中的 WalkTree 方法使用的算法类似，该方法在第 17 章中进行了描述。主要区别在于，而不是将 NodeData 值附加到字符串中，该方法将这些值存储在队列中。

8. 返回 TreeEnumerator<TItem> 类的定义。在类声明中，将鼠标悬停在 IEnumerator<TItem> 文本上。在出现的下拉上下文菜单上（带有灯泡图标），单击 Implement Interface Explicitly。

此操作为 IEnumerator<TItem> 接口和 IEnumerator 接口中的方法生成存根并将其添加到类的末尾。它还为 IDisposable 接口生成 Dispose 方法。

# Note

IEnumerator<TItem> 接口继承自 IEnumerator 和 IDisposable 接口，这就是为什么它们的方法也会出现的原因。事实上，属于 IEnumerator<TItem> 接口的唯一项目是泛型 Current 属性。MoveNext 和 Reset 方法属于非泛型 IEnumerator 接口。第 14 章“使用垃圾回收和资源管理”描述了 IDisposable 接口。

9. 检查已生成的代码。

属性和方法的正文包含一个默认实现，该实现只是抛出 NotImplementedException 异常。你将在以下步骤中用真正的实现替换此代码。

10. 使用此处以粗体显示的代码更新 MoveNext 方法的主体：

Click here to view code image

```
bool IEnumerator.MoveNext()
{
```

```
if (this.enumData == null)
{
    this.enumData = new Queue<TItem>();
    populate(this.enumData, this.currentData);
}

if (this.enumData.Count > 0)
{
    this.currentItem = this.enumData.Dequeue();
    return true;
}

return false;
}
```

枚举器的 MoveNext 方法的目的是双重的。第一次调用时，它应该初始化枚举器使用的数据并前进到要返回的第一个数据项。（在第一次调用 MoveNext 之前，Current 属性返回的值未定义，应导致异常。）在这种情况下，初始化过程包括实例化队列，然后调用 populate 方法用从树中提取的数据填充队列。

对 MoveNext 方法的后续调用应仅遍历数据项，直到没有剩余为止，dequeuing 项目直到队列为空，就像本例中一样。必须牢记，MoveNext 实际上并不返回数据项——这是 Current 属性的目的。MoveNext 所做的只是更新枚举器中的内部状态（即 currentItem 变量的值设置为从队列中提取的数据项），以供 Current 属性使用，如果有下一个值则返回 true，否则返回 false。

11. 按如下方式以粗体修改泛型 Current 属性的 get 访问器的定义：

Click here to view code image

```
TItem IEnumerator<TItem>.Current
{
    get
    {
        if (this.enumData == null)
        {
            throw new InvalidOperationException("Use MoveNext before calling Current");
        }

        return this.currentItem;
    }
}
```

# Important

请确保将代码添加到 Current 属性的正确实现中。保留非泛型版本 System.Collections.IEnumerator.Current，其默认实现抛出 NotImplementedException 异常。

Current 属性检查 enumData 变量以确保已调用 MoveNext。（在第一次调用 MoveNext 之前，此变量将为 null。）如果不是这种情况，属性将抛出 InvalidOperationException——这是 .NET Framework 应用程序用于指示在当前状态下无法执行操作的常规机制。如果之前已调用 MoveNext，它将已更新 currentItem 变量，因此 Current 属性需要做的就是返回此变量中的值。

12. 找到 IDisposable.Dispose 方法。如以下代码中以粗体所示，注释掉 throw new NotImplemented-Exception(); 语句。枚举器不使用需要显式释放的资源，因此此方法无需执行任何操作。但是，它仍然必须存在。有关 Dispose 方法的更多信息，请参阅第 14 章。

Click here to view code image

```
void IDisposable.Dispose()
{
    // throw new NotImplementedException();
}
```

13. 构建解决方案，如果报告任何错误，请更正错误。

# Initializing a variable defined with a type parameter

你应该已经注意到定义和初始化 currentItem 变量的语句使用了 default 关键字。currentItem 变量是使用类型参数 TItem 定义的。当程序被编写和编译时，可能还不知道将为 TItem 替换的实际类型——这个问题只有在代码执行时才解决。这使得指定变量应如何初始化变得困难。诱惑是将它设置为 null。但是，如果为 TItem 替换的类型是值类型，则这是非法的赋值。（你不能将值类型设置为 null，只能将引用类型设置为 null。）同样，如果你期望类型为数字而将其设置为 0，如果使用的类型实际上是引用类型，则这将是非法的。还有其他可能性——例如，TItem 可能是布尔值。default 关键字解决了这个问题。用于初始化变量的值将在语句执行时确定。如果 TItem 是引用类型，default(TItem) 返回 null；如果 TItem 是数字，default(TItem) 返回 0；如果 TItem 是布尔值，default(TItem) 返回 false。如果 TItem 是结构体，则结构体中的各个字段将以相同的方式初始化。（引用字段设置为 null，数字字段设置为 0，布尔字段设置为 false。）

# Implementing the IEnumerable interface

在以下练习中，你将修改二叉树类以实现 IEnumerable<T> 接口。GetEnumerator 方法将返回一个 TreeEnumerator<TItem> 对象。

## Implement the IEnumerable<TItem> interface in the Tree<TItem> class

- 1. 在 Solution Explorer 中，双击文件 Tree.cs 以在 Code and Text Editor 窗口中显示 Tree<TItem> 类。

- 2. 修改 Tree<TItem> 类的定义，使其实现 IEnumerable<TItem> 接口，如以下代码中以粗体所示：

Click here to view code image

```
public class Tree<TItem> : IEnumerable<TItem> where TItem :
IComparable<TItem>
```

请注意，约束始终放在类定义的末尾。

- 3. 将鼠标悬停在类定义中的 IEnumerable<TItem> 接口上。在出现的下拉上下文菜单上，单击 Implement Interface Explicitly。

此操作生成 IEnumerable<TItem>.GetEnumerator 和 IEnumerable.GetEnumerator 的实现

