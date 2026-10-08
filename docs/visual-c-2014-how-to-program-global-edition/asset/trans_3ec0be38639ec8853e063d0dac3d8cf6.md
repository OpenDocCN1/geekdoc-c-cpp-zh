

# 836 第 19 章 自定义链数据结构

没有子节点的节点被称为叶子节点。计算机科学家自然地从根节点向下绘制树——这与自然界中树生长的方式相反。

![](img/57baed2319be0bb1b5f98674846f2711_836_0.png)

图 19.18 | 二叉树的图形表示。

## 二叉搜索树

在二叉树中，我们创建了一种特殊的二叉树称为二叉搜索树。二叉搜索树（允许节点值重复）的特点是：任何左子树中的值都小于子树父节点的值，任何右子树中的值都大于子树父节点的值。图 19.19 展示了一个对应于 9 个整数值数据集的二叉搜索树。对应的二叉搜索树的形状取决于值插入树的顺序。

![](img/57baed2319be0bb1b5f98674846f2711_836_1.png)

图 19.19 | 包含 9 个值的二叉搜索树。

### 19.7.1 整数值的二叉搜索树

图 19.20 和 19.21 的应用程序创建了一个整数二叉搜索树并通过三种方式遍历它（即遍历所有节点）——使用递归的中序、前序和后序遍历。程序生成 10 个随机数并将每个数插入树中。图 19.20 在命名空间 `BinaryTreeLibrary` 中定义了 `Tree` 类以便重用。图 19.21 定义了 `TreeTest` 类以演示类功能。`TreeTest` 类的 `Main` 方法实例化空树，然后随机生成 10 个整数并通过调用 `Tree` 的 `InsertNode` 方法将每个整数插入二叉树中。

程序随后对树进行前序、中序和后序遍历。我们很快会讨论这些遍历方法。

```csharp
// 图 19.20: BinaryTreeLibrary.cs
// TreeNode 类和 Tree 类的声明。
using System;
namespace BinaryTreeLibrary
{
    class TreeNode
    {
        // 自动属性 LeftNode
        public TreeNode LeftNode { get; set; }
        // 自动属性 Data
        public int Data { get; set; }
        // 自动属性 RightNode
        public TreeNode RightNode { get; set; }
        // 初始化 Data 并使此成为叶子节点
        public TreeNode(int nodeData)
        {
            Data = nodeData;
        }
        // 将 TreeNode 插入包含节点的 Tree 中；
        // 忽略重复值
        public void Insert(int insertValue)
        {
            if (insertValue < Data) // 插入左子树
            {
                // 插入新 TreeNode
                if (LeftNode == null)
                {
                    LeftNode = new TreeNode(insertValue);
                }
                else // 继续遍历左子树
                {
                    LeftNode.Insert(insertValue);
                }
            } else if (insertValue > Data) // 插入右子树
            {
                // 插入新 TreeNode
                if (RightNode == null)
                {
                    RightNode = new TreeNode(insertValue);
                }
                else // 继续遍历右子树
                {
                    RightNode.Insert(insertValue);
                }
            }
        }
    }
```

**图 19.20** | TreeNode 类和 Tree 类的声明。（3 部分中的第部分。）

```csharp
50 RightNode.Insert(insertValue);
51     
52 }
53 
54 }
55 
56 // Tree 类声明
57 public class Tree
58 {
59     private TreeNode root;
60 
61     // 在二叉搜索树中插入新节点。
62     // 如果根节点为空，则在此处创建根节点。
63     //// 否则，调用 TreeNode 类的 insert 方法。
64 public void insertNode(int insertValue)
65 {
66     if (root == null)
67     {
68         root = new TreeNode(insertValue);
69     }
70     else
71 {
72         root.Insert(insertValue);
73     }
74 }
75 
76 // 开始前序遍历
77 public void PreorderTraversal()
78 {
79     PreorderHelper(root);
80 }
81 
82 // 执行前序遍历的递归方法
83 private void PreorderHelper(TreeNode node)
84 {
85     if (node != null)
86     {
87         // 输出节点 Data
88         Console.Write($"{node.Data} ");
89     }
90 
91     // 遍历左子树
92     PreorderHelper(node.LeftNode);
93 
94     // 遍历右子树
95     PreorderHelper(node.RightNode);
96     }
97 }
98 
99 // 开始中序遍历
100 public void InorderTraversal()
101 {
102     InorderHelper(root);
103 }
104 }
```

图 19.20 | TreeNode 类和 Tree 类的声明。（3 部分中的第2 部分。）

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
112
113      // 输出节点数据
114      Console.Write($"{node.Data}");
115
116      // 遍历右子树
117          InorderHelper(node.RightNode);
118      }
119  }
120
121  // 开始后序遍历
122  public void PostorderTraversal()
123  {
124      PostorderHelper(root);
125  }
126
127  // 执行后序遍历的递归方法
128  private void PostorderHelper(TreeNode node)
129  {
130      if (node != null)
131      {
132          // 遍历左子树
133          PostorderHelper(node.LeftNode);
134      }
135
136      // 遍历右子树
137          PostorderHelper(node.RightNode);
138      }
139
140      // 输出节点数据
141      Console.Write($"{node.Data}");
142  }
```

图 19.20 | TreeNode 类和 Tree 类的声明。（3 部分中的第3 部分。）

```csharp
// 图 19.20: BinaryTreeLibrary.cs
// TreeNode 类和 Tree 类的声明。
using System;
namespace BinaryTreeLibrary
{
    class TreeNode
    {
        // 自动属性 LeftNode
        public TreeNode LeftNode { get; set; }
        // 自动属性 Data
        public int Data { get; set; }
        // 自动属性 RightNode
        public TreeNode RightNode { get; set; }
        // 初始化 Data 并使此成为叶子节点
        public TreeNode(int nodeData)
        {
            Data = nodeData;
        }
        // 将 TreeNode 插入包含节点的 Tree 中；
        // 忽略重复值
        public void Insert(int insertValue)
        {
            if (insertValue < Data) // 插入左子树
            {
                // 插入新 TreeNode
                if (LeftNode == null)
                {
                    LeftNode = new TreeNode(insertValue);
                }
                else // 继续遍历左子树
                {
                    LeftNode.Insert(insertValue);
                }
            } else if (insertValue > Data) // 插入右子树
            {
                // 插入新 TreeNode
                if (RightNode == null)
                {
                    RightNode = new TreeNode(insertValue);
                }
                else // 继续遍历右子树
                {
                    RightNode.Insert(insertValue);
                }
            }
        }
    }
// Tree 类声明
public class Tree
{
    private TreeNode root;

    // 在二叉搜索树中插入新节点。
    // 如果根节点为空，则在此处创建根节点。
    //// 否则，调用 TreeNode 类的 insert 方法。
    public void insertNode(int insertValue)
    {
        if (root == null)
        {
            root = new TreeNode(insertValue);
        }
        else
        {
            root.Insert(insertValue);
        }
    }

    // 开始前序遍历
    public void PreorderTraversal()
    {
        PreorderHelper(root);
    }

    // 执行前序遍历的递归方法
    private void PreorderHelper(TreeNode node)
    {
        if (node != null)
        {
            // 输出节点 Data
            Console.Write($"{node.Data} ");
        }

        // 遍历左子树
        PreorderHelper(node.LeftNode);

        // 遍历右子树
        PreorderHelper(node.RightNode);
    }

    // 开始中序遍历
    public void InorderTraversal()
    {
        InorderHelper(root);
    }

    // 执行中序遍历的递归方法
    private void InorderHelper(TreeNode node)
    {
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

## 第 19 章 自定义数据结构

```csharp
// 图 19.20: BinaryTreeLibrary.cs
// TreeNode 类和 Tree 类的声明。
using System;
namespace BinaryTreeLibrary
{
    class TreeNode
    {
        // 自动属性 LeftNode
        public TreeNode LeftNode { get; set; }
        // 自动属性 Data
        public int Data { get; set; }
        // 自动属性 RightNode
        public TreeNode RightNode { get; set; }
        // 初始化 Data 并使此成为叶子节点
        public TreeNode(int nodeData)
        {
            Data = nodeData;
        }
        // 将 TreeNode 插入包含节点的 Tree 中；
        // 忽略重复值
        public void Insert(int insertValue)
        {
            if (insertValue < Data) // 插入左子树
            {
                // 插入新 TreeNode
                if (LeftNode == null)
                {
                    LeftNode = new TreeNode(insertValue);
                }
                else // 继续遍历左子树
                {
                    LeftNode.Insert(insertValue);
                }
            } else if (insertValue > Data) // 插入右子树
            {
                // 插入新 TreeNode
                if (RightNode == null)
                {
                    RightNode = new TreeNode(insertValue);
                }
                else // 继续遍历右子树
                {
                    RightNode.Insert(insertValue);
                }
            }
        }
    }
}

// Tree 类声明
public class Tree
{
    private TreeNode root;

    // 在二叉搜索树中插入新节点。
    // 如果根节点为空，则在此处创建根节点。
    //// 否则，调用 TreeNode 类的 insert 方法。
    public void insertNode(int insertValue)
    {
        if (root == null)
        {
            root = new TreeNode(insertValue);
        }
        else
        {
            root.Insert(insertValue);
        }
    }

    // 开始前序遍历
    public void PreorderTraversal()
    {
        PreorderHelper(root);
    }

    // 执行前序遍历的递归方法
    private void PreorderHelper(TreeNode node)
    {
        if (node != null)
        {
            // 输出节点 Data
            Console.Write($"{node.Data} ");
        }

        // 遍历左子树
        PreorderHelper(node.LeftNode);

        // 遍历右子树
        PreorderHelper(node.RightNode);
    }

    // 开始中序遍历
    public void InorderTraversal()
    {
        InorderHelper(root);
    }

    // 执行中序遍历的递归方法
    private void InorderHelper(TreeNode node)
    {
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

// 图 19.20: BinaryTreeLibrary.cs
// TreeNode 类和 Tree 类的声明。
using System;
namespace BinaryTreeLibrary
{
    class TreeNode
    {
        // 自动属性 LeftNode
        public TreeNode LeftNode { get; set; }
        // 自动属性 Data
        public int Data { get; set; }
        // 自动属性 RightNode
        public TreeNode RightNode { get; set; }
        // 初始化 Data 并使此成为叶子节点
        public TreeNode(int nodeData)
        {
            Data = nodeData;
        }
        // 将 TreeNode 插入包含节点的 Tree 中；
        // 忽略重复值
        public void Insert(int insertValue)
        {
            if (insertValue < Data) // 插入左子树
            {
                // 插入新 TreeNode
                if (LeftNode == null)
                {
                    LeftNode = new TreeNode(insertValue);
                }
                else // 继续遍历左子树
                {
                    LeftNode.Insert(insertValue);
                }
            } else if (insertValue > Data) // 插入右子树
            {
                // 插入新 TreeNode
                if (RightNode == null)
                {
                    RightNode = new TreeNode(insertValue);
                }
                else // 继续遍历右子树
                {
                    RightNode.Insert(insertValue);
                }
            }
        }
    }
// Tree 类声明
public class Tree
{
    private TreeNode root;

    // 在二叉搜索树中插入新节点。
    // 如果根节点为空，则在此处创建根节点。
    //// 否则，调用 TreeNode 类的 insert 方法。
    public void insertNode(int insertValue)
    {
        if (root == null)
        {
            root = new TreeNode(insertValue);
        }
        else
        {
            root.Insert(insertValue);
        }
    }

    // 开始前序遍历
    public void PreorderTraversal()
    {
        PreorderHelper(root);
    }

    // 执行前序遍历的递归方法
    private void PreorderHelper(TreeNode node)
    {
        if (node != null)
        {
            // 输出节点 Data
            Console.Write($"{node.Data} ");
        }

        // 遍历左子树
        PreorderHelper(node.LeftNode);

        // 遍历右子树
        PreorderHelper(node.RightNode);
    }

    // 开始中序遍历
    public void InorderTraversal()
    {
        InorderHelper(root);
    }

    // 执行中序遍历的递归方法
    private void InorderHelper(TreeNode node)
    {
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