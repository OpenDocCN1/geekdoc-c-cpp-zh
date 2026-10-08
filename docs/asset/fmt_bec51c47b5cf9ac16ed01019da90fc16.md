
- 9. **使用队列。** 在队列中添加 `N` 后，取出当前元素 `M` 并向队列添加 `M+1`，然后 `2*M+1`，然后 `M+2`。在循环中对下一个元素重复相同操作。在循环的每一步打印 `M`，如果队列大小达到 `50`，则中断循环并完成计算。

- 10. 使用数据结构 **`queue`**。首先，将 `N` 添加到队列中。循环以下操作直到达到 `M`：从队列中移除 `X` 并添加新元素：`X*2`, `X+2` 和 `X+1`。不要添加大于 `M` 的数字。作为方案的优化，尽量避免队列中重复数字。

- 11. 实现 **`LinkedListNode<T>`** 类，它具有字段 **`Previous`** 和 **`Value`**。它将持有单个节点。还要实现 **`LinkedList<T>`** 来持有整个列表。

- 12. 使用单链表 **`singly linked list`**（与上一个任务类似，但没有 **`Next`** 字段）。

- 13. 修改你的**双向链表**实现以允许从头部和尾部添加元素。**另一种解决方案是使用缓冲区**（参见 http://en.wikipedia.org/wiki/Circular_buffer）。当缓冲区满时，创建一个双倍大小的缓冲区并将元素移动过去。

- 14. 使用**数组**。当你到达最后一个索引时，需要在数组开头添加元素。为了正确计算索引，使用数组长度的模（remainder from division）。当你需要调整数组大时，按照“静态列表”部分实现的方式来实现。

- 15. 使用简单的**冒泡排序**。从最左侧元素开始检查它是否小于下一个元素。如果不是，则与下一个元素**交换位置**，以此此类推，直到遇到较大的元素或数组末尾。返回数组开头并重复此过程多次，直到我们顺序获取了所有元素且不需要移动。

- 16. **算法**非常简单：我们从一个**空队列**开始，在其中放入**根目录**（从这里开始遍历）。之后，直到队列为空，从队列中**移除当前目录**并将其打印，并将**所有子目录**添加到队列。通过这种方式我们遍历整个文件系统。如果文件系统中有循环（如 Windows），该过程将完成。

- 17. 在上一个问题的解决方案中，将队列替换为栈，我们将进行**深度遍历 (DFS)**。

- 18. 使用**广度优先搜索 (BFS)**，从标记为 `"*"` 的位置开始。每个未访问的相邻位置当前数字+1。我们假设 `"*"` 的值为 `0`。队列为空后，我们遍历整个矩阵，如果某些单元格为 `0`，则填充为`"u"`。

# C# 计算机编程基础

![](img/251ffe19d2b15f8a8f566ab01924bb12_681_0.png)

我们从这个**层级结构**中可以获得什么信息？开发人员的直接上是“团队负责人”，但间接来说他们属于“项目经理”。“团队负责人”只属于“项目经理”。另一方面，“开发者 1”没有下属。“项目经理”是层级结构中最高的，没有经理。

我们可以以同样的方式描述项目中的每一个参与者。我们看到这样一个小图为我们提供了一些信息。

# 树的术语

为了更好地理解本章的部分，我们建议读者在每一步都在抽象意义与日常生活中的实际用法之间建立类比。

![](img/251ffe19d2b15f8a8f566ab01924bb12_681_1.png)

我们将简化描述我们**层级结构**的图。我们假设它由圆和连接它们的线组成。为了方便起见，我们用唯一的数字为圆命名，这样我们就可以轻松指定我们正在谈论哪一个。

我们将每个圆称为**节点**，将每条线称为**边**。节点“19”、“21”、“14”位于节点“7”下方，并与其直接相连。这些节点我们称为

# 第 17 章 树与图

节点“7”的直接后代（子节点），节点“7”是它们的父节点。同样地，“1”、“12”和“31”是“19”的子，而“19”是它们的父节点。直观上，我们可以说“21”是“19”的兄弟，因为它们都是“7”的子（反过来亦然——“19”是“21”的兄弟）。对于“1”、“12”、“31”、“23”和“6”， 有一个节点在层级结构中位于它们之前，因此它是它们的间接祖先，没有父节点的节点就是它所有的后代。

根节点（Root）是没有父节点的节点。在我们的示例中，这是节点“7”。

叶子节点（Leaf）是没有子节点的节点。在我们的示例中——“1”、“12”、“31”、“21”、“23”和“6”。

内部节点（Internal nodes）是指既不是叶子节点不是根节点的节点（所有有父节点且至少有一个孩子的节点）。这些节点是“19”和“14”。

路径（Path）是指带有边的节点序列，其中节点不重复。路径的示例是序列“1”、“19”、“7”和“21”。序列“1”、“19”和“23”不是路径，因为“19”和“23”没有连接。

路径长度（Path length）是连接路径中节点序列的边数。它等于路径中的节点数减 1。我们的示例路径“1”、“19”、“7”和“21”的长度为三。

节点的深度（Depth）我们称为从根节点到特定节点的路径长度。在我们的示例中，“7”具有根深度，“19”深度为一，“23”深度为二。

这里是关于树的定义：

树——一种递归数据结构，由边连接的节点组成。以下陈述适用于树：

- 每个节点可以有 0 个或多个直接后代（孩子）。
- 每个节点最多有一个父节点。只有一个特殊的节点没有父节点——根节点（如果树不为空）。
- 所有节点从根节点都是可的——从根节点到树中的每个节点都有路径。

我们可以给树更具体的定义：一个节点是一棵树，这个节点可以有零个或多个孩子，这些孩子也是树。

树的高度（Height of tree）——所有节点的最大深度。在我们的示例中，高度为 2。

节点的度（Degree of node）我们称为给定节点的直接孩子数量。“19”和“7”的度为三，但“14”的度为二。叶子节点的度为零。

分支因子（Branching factor）是树中所有节点度的最大值。在我们的示例中，节点的最大度为 3，因此分支因子为 3。

# 树的实现 示例

现在我们将看到如何在编程中将树表示为数据结构。我们将动态实现树。我们的树节点内部包含数字，每个节点将有一个零个或多个孩子的列表，这些孩子也是树（遵循我们的递归定义）。

每个节点使用自身进行递归定义。树的每个节点 (`TreeNode<T>`) 包含一个孩子列表，这些是节点 (`TreeNode<T>`)。树也是另一个类 `Tree<T>`，可以是空的，也可以有一个根节点。`Tree<T>` 实现了树的基本操作，如构造和遍历。

让我们看看动态树表示的源代码：

```csharp
using System;
using System.Collections.Generic;

/// <summary>表示一个树节点</summary>
/// <typeparam name="T">节点中值的类型
/// </typeparam>
public class TreeNode<T>
{
    // 包含节点的值
    private T value;

    // 显示当前节点是否有父节点
    private bool hasParent;

    // 包含节点的节点（零个或多个）
    private List<TreeNode<T>> children;

/// <summary>构造一个树节点</summary>
/// <param name="value">节点的值</param>
public TreeNode(T value)
{
    if (value == null)
    {
        throw new ArgumentNullException(
            "不能插入空值!");
    }
    this.value = value;
    this.children = new List<TreeNode<T>>();
}

/// <summary>节点的值</summary>
public T Value
{
  get {
    return this.value;
  }
  set {
    this.value = value;
  }
}
```

```csharp
// <summary>节点孩子的数量</summary>
public int ChildrenCount
{
  get {
    return this.children.Count;
  }
}
```

```csharp
// <summary>向节点添加孩子</summary>
// <param name="child">要添加的孩子</param>
public void AddChild<T>(TreeNode child) {
  if (child == null)
  {
    throw new ArgumentNullException("不能插入空值!");
  }

  if (child.hasParent)
  {
    throw new ArgumentException("节点已经有父节点!");
  }

  child.hasParent = true;
  this.children.Add(child);
}
```

```csharp
/// <summary>获取指定位置的孩子</summary>
/// <param name="index">孩子的索引</param>
/// <returns>孩子</returns>
public TreeNode<T> GetChild(int index)
{
    if (index < 0 || index >= this.children.Count)
    {
        throw new ArgumentOutOfRangeException("索引越界!");
    }
    return this.children[index];
}
```

```csharp
/// <summary>
/// 表示树数据结构
/// </summary>
/// <typeparam name="T">树中值的类型
/// </typeparam>
public class Tree<T>
{
    // 根节点
    private TreeNode<T> root;

    /// <summary>构造树</summary>
    /// <param name="value">节点的值</param>
    public Tree(T value)
    {
        if (value == null)
        {
            throw new ArgumentNullException("不能插入空值!");
        }
        this.root = new TreeNode<T>(value);
    }

    /// <summary>构造树</summary>
    /// <param name="value">根节点的值</param>
    /// <param name="children">根节点的孩子</param>
    public Tree(T value, params Tree<T>[] children)
    : this(value)
    {
        foreach (Tree<T> child in children)
        {
            this.root.AddChild(child.root);
        }
    }

    /// <summary>
    /// 根节点，如果树为空为空
    /// </summary>
    public TreeNode<T> Root
    {
        get
        return this.root;
    }

    /// <summary>
    /// 以深度优先搜索 (DFS) 方式遍历并打印树
    /// </summary>
    /// <param name="root">要遍历的树的根</param>
    /// <param name="spaces">用于表示父子关系的空格</param>
    private void PrintDFS(TreeNode<T> root, string spaces)
    {
        if (root == null)
        {
            return;
        }
        Console.WriteLine(spaces + root.Value);

        TreeNode<T> child = null;
        for (int i = 0; i < root.ChildrenCount; i++)
        {
            child = root.GetChild(i);
            PrintDFS(child, spaces + " ");
        }
    }

    /// <summary>以深度优先搜索 (DFS) 方式遍历并打印树</summary>
    public void TraverseDFS()
    {
        this.PrintDFS(this.root, string.Empty);
    }
}
```

```csharp
/// <summary>
/// 显示 Tree<T> 类的示例用法
/// </summary>
public static class TreeExample
{
```

```csharp
static void Main()
{
    // 从示例中创建树
    Tree<int> tree =
        new Tree<int>(7,
            new Tree<int>(19,
                new Tree<int>(1),
                new Tree<int>(12),
                new Tree<int>(31)),
            new Tree<int>(21,
                new Tree<int>(14,
                    new Tree<int>(23),
                    new Tree<int>(6))));

    // 使用深度优先搜索遍历并打印树
    tree.TraverseDFS();

    // 控制台输出：
    // 7
    // 19
    // 1
    // 12
    // 31
    // 21
    // 14
    // 23
    // 6
}
```

## 我们的实现是如何运作的？

让我们简单地讨论一下给定的代码。在我们的示例中，我们有一个 `Tree<T>`，它实现了实际的树结构。我们还有一个 `TreeNode<T>` 类，它代表树的单个节点。

与节点相关的函数（创建节点、向此节点添加子节点以及获取子节点数量）都是在 `TreeNode<T>` 级别实现的。

其余功能（例如遍历树）是在 `Tree<T>` 级别实现的。在逻辑上将功能划分在两个类之间，使得我们的实现更具活性。

我们将实现分为两个类的原因是，某些操作对于每个独立节点是典型的（例如添加子节点），而另一些操作是关于整棵树的（例如通过数字搜索节点）。在这种实现的变体中，树是一个知道其根节点的类，而每个节点知道它的子节点。在这种实现中，我们可以有一个空树（当 `root = null` 时）。

以下关于 `TreeNode<T>` 实现的一些细节。树的每个节点由私有字段 `value` 和子节点列表 `children` 组成。子节点列表由相同类型的元素组成。每个节点都包含一个指向其直接子节点的引用列表。还有公共属性用于访问节点字段的值。可以从外部类调用的方法有：

- `AddChild(TreeNode<T> child)` - 添加子节点
- `TreeNode<T> GetChild(int index)` - 通过给定的索引返回子节点
- `ChildrenCount` 返回特定节点的子节点数量

为了满足每个节点只有一个父节点的条件。此信息仅在类内部使用，我们在 `AddChild(Tree<T> child)` 方法中需要它。在该方法内部，我们检查要添加的节点是否已经存在，如果是，则抛出一个异常，表示这是可能的。

在 `Tree<T>` 类中，我们只有一个获取属性 `TreeNode<T> Root`，它返回树的根节点。

## 深度优先搜索 (DFS) 遍历

`Tree<T>` 类中实现了 `TraverseDFS()` 方法，该方法调用私有方法 `PrintDFS(TreeNode<T> root, string spaces)`，该方法按深度遍历树，并使用右移（添加空格）在标准输出中按树形布局打印元素。

深度优先搜索算法允许精确访问树的每个节点一次。有多种算法可以遍历树，我们将只讨论其中两种：DFS（深度优先搜索）和 BFS（广度优先搜索）。

DFS 算法从给定的节点开始，按照树的层次结构向下移动。当它到达一个没有子节点可以访问或已经过的节点时，它会返回到上一个节点。我们可以通过以下简单步骤描述深度优先搜索算法：

- 遍历当前节点（例如，在控制台上打印它或以某种方式对其进行处理）。
- 顺序递归地遍历当前节点的每个子节点（遍历当前节点的子树）。这可以通过对每个子节点递归调用相同的方法来实现。

## 创建树

为了让创建树变得更容易，我们定义了一个特殊的构造函数，它接受输入参数为节点值和它的子树列表。这允许我们提供任意数量的 `Tree<T>` 类型的参数（子树）。我们在创建示例树时使用了完全相同的构造函数。

## 遍历硬盘器目录

让我们从树的另一个示例开始：文件系统。你是否注意到你硬盘上的目录实际上是一个分层结构，即一棵树？我们有文件夹（树节点），它们可能包含子文件夹和文件（它们也是树节点）。

你可以联想到许多使用树的现实生活例子，对吧？

让我们更详细地查看 Windows 文件系统。正如我们日常经验所知的，我们在硬盘上创建文件夹，这些文件夹可以包含子文件夹和文件。子文件夹也可以包含子文件夹，依此类推，直到达到某些深度限制。
