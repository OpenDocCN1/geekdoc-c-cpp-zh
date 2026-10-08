
文件系统的目录树可以通过 .NET 内置功能访问：`System.IO.DirectoryInfo`类。它不是作为数据结构存在的，但我们可以获取每个目录的子文件夹和文件，因此我们可以使用标准工具遍历文件系统树。

下面是 Windows 目录树的典型样子：

![Windows目录树](img/251ffe9d2b1a8f5f6ab0192bb12_0.png)

## 目录的递归 DFS 遍历

下一个示例演示了我们如何递归地遍历目录，并在标准输出中打印其树结构：

### DirectoryDFS.cs

```csharp
using System;
using System.IO;

/// <summary>
/// 基于深度优先搜索 (DFS)
/// 的目录遍历示例类
/// </summary>
public static class DirectoryDFS
{
    /// <summary>
    /// 递归遍历目录
    /// </summary>
    /// <param name="dir">要遍历的目录</param>
    /// <param name="spaces">用于表示
    /// 父子关系的空格</param>
    private static void TraverseDir(DirectoryInfo dir, string spaces)
    {
        // 访问当前目录
        Console.WriteLine(spaces + dir.FullName);

        DirectoryInfo[] children = dir.GetDirectories();

        // 为每个子节点访问其子树
        foreach (DirectoryInfo child in children)
        {
            TraverseDir(child, spaces + " ");
        }
    }

    /// <summary>
    /// 递归遍历目录
    /// </summary>
    /// <param name="propertyPath">目录的路径</param>
    static void TraverseDir(string directoryPath)
    {
        TraverseDir(new DirectoryInfo(directoryPath), string.Empty);
    }

    static void Main()
```

正如我们看到的，目录内容的递归遍历算法与我们树的相同。

在这里我们可以看到遍历的结果：

```
C:\
C:\Config.Msi
C:\Documents and Settings\Administrator
C:\Documents and Settings\Administrator\.ARIS70
C:\Documents and Settings\Administrator\.jindent
C:\Documents and Settings\Administrator\.nbi
C:\Documents and Settings\Administrator\.nbi\downloads
C:\Documents and Settings\Administrator\.nbi\log
C:\Documents and Settings\Administrator\.nbi\cache
C:\Documents and Settings\Administrator\.nbi\tmp
C:\Documents and Settings\Administrator\.nbi\wd
```

注意，由于你对硬盘上的某些文件夹没有访问权限，上述程序可能会抛出 `UnauthorizedAccessException`。这在某些 Windows 安装是常见的，因此你可以从另一个目录开始遍历进行测试，例如从 `"C:\Windows\assembly"`。

## 广度优先搜索 (BFS)

让我们看看另一种遍历树的方法。广度优先搜索 (BFS) 是遍历分支数据结构（如树和图）的算法。BFS 算法遍历起始节点，然后是它的直接子节点、它们的直接子节点依此类推。这种方法也被称为波遍历，因为它看起来像波浪

广度优先搜索 (BFS) 算法包含以下步骤：

1. 将起始节点加入队列 `Q`。

2. 当 `Q` 不为空时重复以下两个步骤：

   - 从 `Q` 中取出下一个节点 `v` 并打印它。

   - 将 `v` 的所有子节点加入队列。

BFS 算法非常简单，它总是遍历离起始节点最近的节点，然后是更远的节点，以此类推直到到达最远的节点。BFS 算法广泛应用于解决问题，例如在迷宫中寻找最短路径。

下面是一个 BFS 算法的示例实现，它可以打印文件系统中所有的文件夹：

```cs
DirectoryTraverserBFS.cs
using System;
using System.Collections.Generic;
using System.IO;

/// <summary>
/// 示例类，基于广度优先搜索 (BFS) 算法
/// 遍历指定的目录
/// </summary>
public static class DirectoryTraverserBFS
{
    /// <summary>
    /// 使用 BFS 遍历并打印指定的目录
    /// </summary>
    /// <param name="directory">需要遍历的目录路径</param>
    static void TraverseDir(string directoryPath)
    {
        Queue<DirectoryInfo> visitedDirsQueue =
            new Queue<DirectoryInfo>();
        visitedDirsQueue.Enqueue(new DirectoryInfo(directoryPath));
        while (visitedDirsQueue.Count > 0)
        {
            DirectoryInfo currentDir = visitedDirsQueue.Dequeue();
            Console.WriteLine(currentDir.FullName);

            DirectoryInfo[] children = currentDir.GetDirectories();
            foreach (DirectoryInfo child in children)
            {
                visitedDirsQueue.Enqueue(child);
            }
        }
    }

    static void Main()
    {
        TraverseDir("C:");
    }
}
```

如果我们启动程序来遍历本地磁盘，我们将看到 BFS 首先访问离根目录（深度 1）最近的目录，然后是深度 2、深度 3 等。这里是该程序的示例输出：

```
C:\Config
C:\Program Files
C:\RECYCLEBIN
C:\System Volume Information
C:\Users
C:\Users\Administrator
C:\Users\All Users
C:\Users\Default
...
```

## 二叉树

在上一节中，我们讨论了树的基本结构。在本节中，我们将查看一种特定的树——二叉树。这种树在编程中证明非常有用。树的术语同样适用。尽管如此，下文我们将对这种结构给出一些具体的解释。

二叉树 —— 一种节点度小于或等于 2 的树。我们可以说它是每个节点只有左孩子或右孩子，而非两者兼具的树。某些节点没有孩子，被称为叶子节点。二叉树可以递归地定义如下：单个节点是一个二叉树，它可以有左、右孩子，而这些孩子也都是二叉树。

这里有一个二叉树的示例。节点再次用数字命名。我们可以看到树的根节点是 "14"，左子树（以 19 为根）、右子树（以 15 为根）以及一个右孩子——"21"。我们需要注意的是，二叉树的定义在每个节点的子节点顺序上有一个很大的区别。

![](img/251ffe9d2b15f8a5f66ab_694_0.png)

在上面的插图中展示了两棵不同的二叉树——第一棵的根为 "19"，左孩子为 "23"；第二棵根为 "19"，右孩子为 "23"。如果这是一棵普通树，它们将是相同的。这就是为什么我们说明以下内容：

### 二叉树遍历

二叉树的遍历是一个经典问题，并有解决方案。通常有几种递归遍历二叉树的方法：

- 中序（左-右）—— 算法首先遍历左树，然后是根节点和右树。在我们的示例中，遍历序列为："23", "19", "10", "6", "21", "14", "3", "15"。

- 前序（根-左-右）—— 在这种情况下，算法遍历根节点，然后是左树和右树。在我们的示例中的结果是："14", "19", "23", "6", "10", "21", "15", "3"。

- 后序（右-左-根）—— 在这里我们遍历左树，然后是右树，最后是根节点。遍历后的结果是："23", "10", "6", "15", "19", "14"。

### 二叉树的递归遍历 - 示例

下一个示例展示了使用中序方案遍历的二叉树实现：

```cs
using System;
using System.Collections.Generic;

/// <summary>代表一个二叉树</summary>
/// <typeparam name="T">树中值的类型</typeparam>
public class BinaryTree<T>
{
    /// <summary>存储在当前节点中的值</summary>
    public T Value { get; set; }
    /// <summary>当前节点的左孩子</summary>
    public BinaryTree<T> LeftChild { get; set; }
    /// <summary>当前节点的右孩子</summary>
    public BinaryTree<T> RightChild { get; set; }

    /// <summary>构造一个二叉树</summary>
    /// <param name="value">树节点的值</param>
    /// <param name="leftChild">树的左孩子</param>
    /// <param name="rightChild">树的右孩子</param>
    public BinaryTree(T value, BinaryTree<T> leftChild, BinaryTree<T> rightChild)
    {
        this.Value = value;
        this.LeftChild = leftChild;
        this.RightChild = rightChild;
    }

    /// <summary>构造一个没有孩子的二叉树</summary>
    /// <param name="value">树节点的值</param>
    public BinaryTree(T value) : this(value, null, null) { }

    /// <summary>中序遍历二叉树</summary>
    public void PrintInOrder()
    {
        // 1. 访问左孩子
        if (this.LeftChild != null)
        {
            this.LeftChild.PrintInOrder();
        }

        // 2. 访问子树的根
        Console.Write(this.Value + " ");

        // 3. 访问右孩子
        if (this.RightChild != null)
        {
            this.RightChild.PrintInOrder();
        }
    }

    /// <summary>
    /// 展示如何使用 BinaryTree<T> 类
    /// </summary>
    public class BinaryTreeExample
    {
        static void Main()
        {
            // 根据示例创建二叉树
            BinaryTree<int> binaryTree =
                new BinaryTree<int>(14,
                    new BinaryTree<int>(19,
                        new BinaryTree<int>(23,
                            new BinaryTree<int>(6,
                                new BinaryTree<int>(10,
                                    new BinaryTree<int>(21)))),
                    new BinaryTree<int>(15,
                        new BinaryTree<int>(3, null)));

            // 以中序遍历并打印树
            binaryTree.PrintInOrder();
            Console.WriteLine();

            // 控制台输出：
            // 23 19 10 6 21 14 3 15
        }
    }
}
```

### 示例是如何运行的？

这个二叉树实现与普通树的实现有所不同，并且被大大简化。

我们有一个递归类定义 `BinaryTree<T>`，它包含一个值以及相同类型的左、右孩子节点。

# 第 17 章 树与图

在本章中，我们将查看一类更具体的二叉树——**有序树**。它们利用了二叉树节点的一个一个重要属性——每个节点中的**唯一标识键**。这些键的一个重要属性是它们是[可比较的](#)。一种重要的有序树类型是所谓的**平衡搜索树**。

## 对象之间的可比较性

在继续之前，我们将介绍以下定义，在后续的介绍中将需要它。

**可比较性** - 如果存在以下三个依赖关系中的**恰好一个**，我们称两个对象 A 和 B 为**可比较的**：

- "A 小于 B"

- "A 大于 B"

- "A 等于 B"

同样，如果以下三种可能性中恰好有一个为真（即 A < B、A > B 或 A = B），我们也称两个键 **A 和 B 是可比较的**。

树的的节点可以包含不同的字段，但我们可以考虑它们的唯一键，并且我们希望这些键是可比较的。让我们来看一个例子。我们有两个特定的节点 A 和 B：

![](img/251ffe19d2b15f8a8f566ab01924bb12_698_0.png)

在这种情况下，A 和 B 的键持有整数 19 和 7。从数学上我们知道，整数（与复数不同）是**可比较的**，根据上面的推理，我们有权将它们作为键。这就是为什么我们可以说“A 大于 B”，因为“19 大于 17”。

> **请注意！在这种情况下，节点上显示的数字是它们的唯一标识键，而不是像之前那样仅仅是一些数字。**

我们得出了**有序二叉搜索树**的定义：

**有序二叉树（二叉搜索树）** 是一种二叉树，其中每个节点都有一个唯一的键，每两个键之间都是可比较的，并且树的组织方式使得每个节点都满足以下条件：

- **左子树**中的所有键都**小于**其自身的键。

- **右子树**中的所有键都**大于**其自身的键。

### 有序二叉搜索树的属性

在下面的图中，我们给出了有序二叉搜索树的例子。我们将使用这个例子来给出二叉树顺序的一些重要属性：

![](img/251ffe19d2b15f8a8f566ab01924bb12_699_0.png)

根据定义，我们知道每个节点的左子树只包含比自己小的元素，而右子树中只包含更大的元素。这意味着如果我们想从根节点开始查找元素，我们要么已经找到了它，要么应该在它的左子树或右子树中搜索它，这将节省不必要的比较。例如，如果我们在树中搜索 23，我们不会在 19 的左子树中搜索它，因为 23 肯定不在那里（23 大于 19，所以最终在右子树中）。这为我们节省了与左树中每个元素进行的 5 次不必要的比较，但如果我们使用链表，就必须进行这 5 次比较。

根据元素的顺序可以推导出，树中的最小元素（如果是根节点本身的话）没有左后继节点。在我们的例子中，最小元素是 7，最大元素是 35。下一个有用的属性是，节点左子树中的每一个元素都小于该节点右子树中的每一个元素。

### 有序二叉搜索树 – 示例

下一个例子展示了二叉搜索树的简单实现。我们的目标是为树中的添加、搜索和删除元素提供方法。对于上述的每一个操作，我们都会给出详细的解释。注意，我们的二叉搜索树不是平衡的，在某些情况下可能性能较差。

### 有序二叉搜索树：节点的实现

和之前一样，现在我们将定义一个内部类，用于描述节点的结构。这将清晰地区分并封装我们树内部包含的节点结构。我们定义为内部的独立类 `BinaryTreeNode<T>` 仅对有序树类可见。

以下是它的定义：

| BinaryTreeNode.cs |
