
```csharp
if (node != null)
{
    // 遍历左子树
    InorderHelper(node.LeftNode);
}
// 输出节点数据
Console.Write($"{node.Data}");
// 遍历右子树
InorderHelper(node.RightNode);
}
// 开始后序遍历
public void PostorderTraversal()
{
    PostorderHelper(root);
}
// 执行后序遍历的递归方法
private void PostorderHelper(TreeNode node)
{
    if (node != null)
    {
        // 遍历左子树
        PostorderHelper(node.LeftNode);
    }
    // 遍历右子树
    PostorderHelper(node.RightNode);
    }
    // 输出节点数据
    Console.Write($"{node.Data}");
}
}
```

# 第 19 章 自定义链数据结构

- 3. 处理节点中的值（第 113 行）。
- 4. 调用 `InorderHelper` 递归遍历右子树（第 116 行）。

中序遍历在处理该节点左子树的值之前，不会处理该节点中的值。图 19.22 中树的中序遍历如下：

```
6 13 17 23 32 48
```

二叉搜索树的中序遍历按升序顺序显示节点值。创建二叉搜索树的过程实际上是对数据进行排序（当配合中序遍历时）——因此，这个过程被称为二叉树排序。

# 前序遍历算法

`PreorderHelper` 方法（第 83–96 行）定义了前序遍历的步骤。步骤如下：

- 1. 如果参数为空，则不处理树。
- 2. 处理节点中的值（第 88 行）。
- 3. 调用 `PreorderHelper` 递归遍历左子树（第 91 行）。
- 4. 调用 `PreorderHelper` 递归遍历右子树（第 94 行）。

前序遍历在访问每个节点时处理其节点值。在处理完给定节点的值后，前序遍历会处理左子树的值，然后处理右子树的值。图 19.22 中树的前序遍历如下：

```
27 13 17 42 33 38
```

# 后序遍历算法

`PostorderHelper` 方法（第 127–140 行）定义了后序遍历的步骤。步骤如下：

- 1. 如果参数为空，则不处理树。
- 2. 调用 `PostorderHelper` 递归遍历左子树（第 132 行）。
- 3. 调用 `PostorderHelper` 递归遍历右子树（第 135 行）。
- 4. 处理节点中的值（第 138 行）。

后序遍历在处理完所有节点节点的值后才处理每个节点的值。图 19.22 中树的后序遍历如下：

```
6 17 13 33 48 42 27
```

# 去重

二叉树有助于去重。在构建树的过程中，插入操作会识别出插入重复值的尝试，因为重复值在每次比较中都会像原值一样遵循“左侧”或“右侧”规则。因此，插入操作最终会将重复值与包含相同值的节点进行比较。此时，插入操作可能简单地丢弃该重复值。在树中搜索匹配键的值是非常快的，特别是对于紧密二叉树。在紧密二叉树中，每一层包含的元素数量大约是前一层的两倍。

# 19.7 树

图 19.22 是一棵紧密二叉树。具有 $n$ 个元素的紧密二叉搜索树至少有 $\log n$ 层。对于这样的树，找到匹配项或确定不存在匹配项最多需要 $n$ 次比较。搜索一个（紧密的）1000 元素的二叉搜索树最多需要 10 次比较，因为 $2^{10} > 1000$。搜索一个（紧密的）1,000,000 元素的二叉搜索树最多需要 20 次比较，因为 $2^{20} > 1,000,000$。

# 层序二叉树练习概述

本章练习介绍了二叉树层序遍历的算法，该算法从根节点层开始逐行访问树的节点。在树的每一层上，层序遍历从左到右访问节点。

# 19.7.2 IComparable 对象的二叉搜索树

19.7.1 节中的二叉树示例在所有数据类型均为 `int` 时有效。假设你想操作一个 `double` 类型的二叉树。你可以使用不同的名称重写 `TreeNode` 和 `Tree` 类，并自定义这些类以处理 `double`。同样，对于每种数据类型，你都可以创建 `TreeNode` 和 `Tree` 的自定义版本。这会导致代码扩散，并变得难以管理和维护。

理想情况下，我们希望定义一次二叉树的功能并在许多类型中重复使用。C# 等语言允许以统一的方式处理所有对象。使用此类功能使能够设计更灵活的数据结构。C# 通过泛型（第 20 章）提供了这些功能。

在下一个示例中，我们利用 C# 的多态能力，通过实现处理任何实现 `IComparable` 接口（命名空间 `System`）对象的 `TreeNode` 和 `Tree` 类。能够比较存储在二叉搜索树中的对象是非常重要的，这样我们就可以确定新类插入点的路径。实现 `IComparable` 的类与方法接收到的参数对象进行 `CompareTo`。如果调用对象小于参数对象，方法返回小于零的整数；如果调用对象大于参数对象，则返回正值。此外，调用对象和参数对象必须是相同的数据类型；否则方法将抛出 `ArgumentException`。

图 19.23–19.24 增强了 19.7.1 节的程序以实现对象。新版本 `TreeNode` 和 `Tree` 类的变化是，每个树对象可以包含任何类型的对象（例如，所有的字符串或双精度浮）。如果程序尝试在同一个 `TreeNode` 类树中插入多种类型（19.23 中的第 14、20、27、29 和 41 行），并在 `Tree` 类中的某一行代码（第 64 行）中启用 `IComparable` 对象的插入，将发生异常。对于第 30 和 42 行，所有更改都将被替换的 `int` 为 `<` 和 `>` 运算符，以便将插入的值与新节点中的值进行比较。这些行现在通过接口 `CompareTo` 方法比较 `IComparable` 对象，然后通过方法的返回值判断它是小于零（调用对象小于参数对象）还是大于零（调用对象大于参数对象）。

[注：如果此类是使用泛型编写的（第 20 章），数据类型 `int` 或 `IComparable` 可以在编译时由任何其他实现必要的运算符和方法的类型替换。]

```csharp
// 图 19.23: BinaryTreeLibrary.cs
// TreeNode 类和 Tree 类的声明。
using System;
namespace BinaryTreeLibrary2 {
    // TreeNode 类声明
    class TreeNode {
        // 自动属性 LeftNode
        public TreeNode LeftNode { get; set; }
        // 自动属性 Data
        public IComparable Data { get; private set; }
        // 自动属性 RightNode
        public TreeNode RightNode { get; set; }
        // 初始化 Data 并使之成为叶子节点
        public TreeNode(IComparable nodeData) {
            Data = nodeData;
        }
        // 将 TreeNode 插入包含节点的 Tree 中
        // 忽略重复值
        public void insert(IComparable insertValue) {
            if (insertValue.CompareTo(Data) < 0) // 插入到左子树 {
                // 插入新 TreeNode
                if (LeftNode == null)
                    LeftNode = new TreeNode(insertValue);
            } else // 继续遍历左子树 {
                Node.Insert(insertValue);
            } } else if (insertValue.CompareTo(Data) > 0) // 插入到右侧 {
                // 插入新 TreeNode
                if (RightNode == null)
                    RightNode = new TreeNode(insertValue);
            } else // 继续遍历右子树 {
                // (此处为逻辑)
            }
        }
    }
}
```

图 19.23 | `TreeNode` 类和 `Tree` 类的声明。（3 部分中的第一部分。）

```csharp
50 RightNode.Insert(insertValue);
51 }
52 }
53 
54 } // Tree 类声明
56 public class Tree
57 {
58     private TreeNode root;
59 
60     // 在二叉搜索树中插入新节点。
61     // 如果根节点为空，在此处根节点。
62     // 否则，调用 TreeNode 类的 insert 方法。
63     public void insertNode(IComparable insertValue)
64 {
65 
66     if (root == null)
67         {
68             root = new TreeNode(insertValue);
69         }
70     else
71         {
72             root.Insert(insertValue);
73         }
74 }
75 
76 // 开始前序遍历
77 {
78     public void PreorderTraversal()
79     PreorderHelper(root);
80 }
81 
82 
4 // 执行前序遍历的递归方法
85 private void PreorderHelper(TreeNode node)
86 {
87     if (node != null)
88         {
89             // 输出节点 Data
90             Console.Write($"{node.Data}");
91             
92             // 遍历左子树
93             PreorderHelper(node.LeftNode);
94             
95             // 遍历右子树
96             PreorderHelper(node.RightNode);
97         }
98 }
```

# 第 19 章 自定义链数据结构

```csharp
103
104  // 执行中序遍历的递归方法
105  private void InorderHelper(TreeNode node)
106  {
107      if (node != null)
108      {
109          // 遍历左子树
110          InorderHelper(node.LeftNode);
111      }
112          // 输出节点数据
113          Console.Write($"{node.Data}");
114
115      // 遍历右子树
116          InorderHelper(node.RightNode);
117      }
118  }
119
120  // 开始后序遍历
121  public void PostorderTraversal()
122  {
123      PostorderHelper(root);
124  }
125
126  // 执行后序遍历的递归方法
127  private void PostorderHelper(TreeNode node)
128  {
129      if (node != null)
130      {
131          // 遍历左子树
132          PostorderHelper(node.LeftNode);
133
134          // 遍历右子树
135          PostorderHelper(node.RightNode);
136
137          // 输出节点数据
138          Console.Write($"{node.Data}");
139      }
140}
141}
```

`TreeNode` 的声明和 `Tree` 类的声明（共 3 部分）创建了三个 `Tree` 对象来存储 `int`、`double` 和 `string` 值，这些值都被框架定义为 `IComparable` 类型。程序分别用 `intArray`（第 12 行）、`doubleArray`（第 13 行）和 `stringArray`（第 14–15 行）中的值填充树。

```csharp
// 图 19.23：使用 IComparable 对象测试类。
using System;
```

```csharp
4  using BinaryTree;
5  // class Tree
6  public class TreeTest
7  {
8  // test class Main
9  static void Main()
10 {
11  int[] intArray = {8, 2, 4, 3, 1, 7, 5, 6};
12  double[] doubleArray = {8.8, 2.2, 4.4, 3.3, 1.1, 7.7, 5.5, 6.6};
13  string[] stringArray = {
14    "eight", "two", "four", "three", "one", "seven", "five", "six"
15  };
16  // 创建 intTree
17  Tree intTree = new Tree();
18  PopulateTree(intArray, intTree, nameof(intTree));
19  TraverseTree(intTree, nameof(intTree));
20
21  // 创建 doubleTree
22  Tree doubleTree = new Tree();
23  PopulateTree(doubleArray, doubleTree, nameof(doubleTree));
24  TraverseTree(doubleTree, nameof(doubleTree));
25
26  // 创建 stringTree
27  Tree stringTree = new Tree();
28  PopulateTree(stringArray, stringTree, nameof(stringTree));
29  TraverseTree(stringTree, nameof(stringTree));
30 }
31
32  // 用数组元素填充树
33  private static void PopulateTree(Tree[] array, Tree tree, string name)
34  {
35    Console.WriteLine($"\n正在插入到 {name}:");
36    foreach (IComparable data in array)
37    {
38      Console.Write($"{data} ");
39      tree.InsertNode(data);
40    }
41  }
42  // 执行遍历
43  private static void TraverseTree(Tree tree, string treeType)
44  {
45    // 执行树的先序遍历
46    Console.WriteLine($"\n{treeType} 的先序遍历：");
47    tree.PreorderTraversal();
48
49    // 执行树的中序遍历
50    Console.WriteLine($"\n{treeType} 的中序遍历：");
51    tree.InorderTraversal();
52  }
53 }
```
图 19.24 | 使用 `IComparable` 对象测试 `Tree` 类。（3 部分中的第 2。）

```csharp
56 // 执行树的后序遍历
57 Console.WriteLine($"\n{treeType} 的后序遍历：");
58 tree.PostorderTraversal();
59  }
60 }
```
