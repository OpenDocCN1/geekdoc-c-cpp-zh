
### 程序 18.12 使用队列对象模拟排队过程（续）

```cpp
// Printing the header for statistical data
cout << left << setw (10) << "Arrive" << setw (10) << "Start";
cout << left << setw (10) << "Delay" << setw (10) << "Leave";
cout << left << setw (10) << "Serve time" << endl;
// Calculation and printing statistics
while (line.size() > 0)
{
    arriveDelay = line.front().first;
    serveTime = line.front().second;
    arrive = arrive + arriveDelay;
    if (arrive >= leave)
    {
        start = arrive;
    }
    else
    {
        start = leave;
    }
    leave = start + line.front().second;
    wait = start - arrive;
    cout << left << setw(10) << arrive << setw (10) << start;
    cout << left << setw (10) << wait;
    cout << setw (10) << leave;
    cout << left << setw (12) << serveTime << endl;
    totalServeTime += serveTime;
    totalWait += wait;
    line.pop();
}
// Printing the summary
double averageWait = static_cast <double> (totalWait) / size;
cout << "----------------------------------------------" << endl;
cout << "Total serve time: " << totalServeTime << endl;
cout << "Average Delay: " << averageWait << endl;
return 0;
}
```

| 到达 | 开始 | 延迟 | 离开 | 服务时间 |
|---:|---:|---:|---:|---:|
| 5 | 5 | 0 | 12 | 7 |
| 6 | 12 | 6 | 22 | 10 |
| 8 | 22 | 14 | 32 | 10 |
| 10 | 32 | 22 | 39 | 7 |
| 13 | 39 | 26 | 48 | 9 |
| 16 | 48 | 32 | 54 | 6 |
| 20 | 54 | 34 | 63 | 9 |

程序输出表明，尽管捐赠是随机到达的，我们仍可以将其归为五类。我们也可以添加一些代码来求每一类捐赠值的总和与平均值，但我们将此留作练习。

## 18.4 二叉搜索树

链表、栈和队列是线性集合；*树*是一种非线性集合。在一般树中，每个节点可以有两个或更多指向其他节点的链接。尽管一般树在计算机科学中有许多应用（例如目录），但我们更常遇到的是**二叉树**，即最多有两棵子树的树。二叉树的一种特殊情况称为**二叉搜索树**，其中左子树中节点的值小于根的值，右子树中的值大于根的值。图 18.16 展示了一棵二叉搜索树。

### 18.4.1 遍历

二叉搜索树的遍历要求按照预先确定的顺序对树中的每个节点处理一次且仅处理一次。我们讨论三种常见的遍历：*前序*、*中序*和*后序*。

### 前序遍历

在**前序遍历**中，首先处理根节点，然后以前序遍历左子树中的所有节点，再以前序遍历右子树中的所有节点。对图 18.16 中的子树进行前序遍历，得到以下序列。注意，根节点出现在开头。

- 80, 62, 45, 72, 84, –, 86

当我们希望首先访问树或子树中的根节点时，前序遍历很有用。

### 中序遍历

在**中序遍历**中，根节点的处理位于两棵子树之间。换句话说，我们需要先遍历整个左子树，然后处理根节点，再遍历右子树。每个子树都应遵循这一规则。对图 18.16 中的子树进行中序遍历，得到以下序列。整棵树的根节点位于中间。注意，在二叉搜索树的中序遍历中，各值按升序处理。

- 45, 62, 72, 80, –, 84, 86

![](img/d68f6199646ca63591a6d8419e0ed4ba_859_0.png)

**图 18.16** 整数二叉搜索树

### 后序遍历

在**后序遍历**中，根节点的处理在两棵子树处理之后。换句话说，我们需要先遍历左子树，然后遍历右子树，最后处理根节点。每个子树都应遵循这一规则。对图 18.16 中的子树进行后序遍历，得到以下序列。注意，整棵树的根节点出现在最后。

| 45 | 72 | 62 | – | 86 | 84 | 80 |
|---|---|---|---|---|---|---|

### 18.4.2 实现

我们讨论二叉搜索树的三种遍历。当二叉搜索树被正确实现时，二叉搜索树中的数据值是有序的，这意味着我们可以更容易地搜索该树（这也是“二叉搜索树”名称的由来）。这三种遍历帮助我们构建二叉搜索树、搜索二叉搜索树以及销毁二叉搜索树。然而，对于每项活动，我们必须使用正确的遍历。

### 插入

如何在二叉搜索树中插入节点？答案是必须找到待插入节点的位置。查找位置应从根节点开始。我们必须插入根节点，然后插入左子树或右子树。在每个子树中，我们都做同样的事情。这意味着我们可以编写如下所示的递归算法：

```
If the tree is empty, insert as the root.                         // Base case
Insert at the left subtree if value is less than root value.     // General case
Insert at the right subtree if value is greater than root value.  // General case
```

### 销毁

如何销毁一棵二叉搜索树？答案是我们逐个节点地进行。然而，要删除一个节点，其左子树和右子树必须为空。这表明销毁二叉搜索树需要后序遍历，因为最后必须销毁的节点是根节点。我们必须销毁左子树，然后销毁右子树，最后销毁根节点。这意味着我们可以编写如下所示的递归算法：

```
Destroy the left subtree.                    // General case
Destroy the right subtree.                   // General case
Delete data item in the root.                // Base case
```

### 打印

如何打印二叉搜索树中的项以得到有序列表？答案是我们逐个节点地进行。左子树在该节点之前处理，右子树在该节点之后处理。这表明打印所有节点的值是一个递归过程，如下所示：

```
Print items at the left subtree.              // General case
Print the root.                               // Base case
Print the items in right subtree.             // General case
```

### 程序 18.14 文件 `binarysearchtree.h`（续）

```cpp
void inorder() const;
void preorder() const;
void postorder() const;
int size() const;
bool empty() const;
};
#endif
```

请注意，我们有一些公有成员函数和一些私有成员函数。公有成员函数是由用户（对于析构函数则是系统）调用的非递归函数。这些函数调用时使用的参数数量最少。私有成员函数是由相应的非递归成员函数调用的递归辅助函数。例如，我们有一个非递归成员函数，当树对象离开作用域时由系统调用，但它会调用 destroy 成员函数，使用后序遍历销毁整棵树。我们还有一个由用户调用的 insert 函数，用户只提供节点数据的值，但它会调用一个递归辅助函数，将节点插入适当位置并维护二叉搜索树的属性（数据项的有序集合）。我们还创建了三个遍历函数，它们又调用相应的递归辅助函数。

**实现文件** 程序 18.15 展示了程序 18.14 中接口文件对应的实现文件。

### 程序 18.15 二叉搜索树的实现文件

```cpp
/************************************************************
 * The implementation file to define the member function     *
 * declared in the interface file                            *
 ************************************************************/
#ifndef BINARYSEARCHTREE_CPP
#define BINARYSEARCHTREE_CPP
#include "binarySearchTree.h"

// Constructor
template <class T>
BinarySearchTree<T> :: BinarySearchTree()
:root (0), count (0)
{
}
// Destructor
template <class T>
BinarySearchTree<T> :: ~BinarySearchTree ()
{
    destroy (root);
}
```
