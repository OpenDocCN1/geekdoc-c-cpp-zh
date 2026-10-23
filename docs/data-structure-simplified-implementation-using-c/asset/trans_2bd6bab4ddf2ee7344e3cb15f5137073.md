

+   4. 编写一个程序，使显示也按层级出现。（提示使用两个队列）
+   5. 编写一个先序遍历的程序，该程序使用队列插入元素。遍历完成后显示队列中存储的每个节点。
+   6. 编写一个函数，按层级统计并显示 BST 中节点的数量。
+   7. 编写一个合并两个 BST 的程序。确保合并后得到的树仍为 BST。
+   8. 编写一个函数，用于确定 BST 中任意特定节点的以下信息
+      a) 中序前驱
+      b) 中序后继
+   9. 编写一个程序，统计 BST 中叶子节点的数量。
+   10. 编写一个程序，确定 BST 的层数。

## 高级树

## 章节目标

- 定义 BST 的局限性
- 定义线索树
- 定义各种类型的线索树
- 定义与高度相关的 BST 局限性
- 定义 AVL 树
- 在 AVL 树中插入节点
- 讨论 AVL 树中各种类型的旋转
- 调整 AVL 树的平衡因子。

### 8.1 高级树

上一章讨论的 BST 存在各种局限性，包括无法向后遍历、存在大量 NULL 节点等。BST 的另一个主要局限性是，如果 BST 是按升序或降序的序列创建的，它会表现为链表。为克服这些局限性，可以使用高级树，如线索树和 AVL 树。线索树有助于解决 BST 中 NULL 节点的数量问题，同时便于向后遍历。AVL 解决了 BST 向一侧倾斜的行为。这两个主题已在后续章节中描述。

### 8.2 线索树

线索树是 BST 的一种特殊情况，因此需要额外的组件来表示线索。存在多种线索树，可用于其特定场景。主要存在的线索树类型包括：

- 左线索树
- 右线索树
- 中序线索

在 BST 中，仅节点的左指针（为 NULL）作为线索起作用的树称为左线索树。类似地，在 BST 中，仅节点的右指针（为 NULL）作为线索起作用的 BST 称为右线索树。节点的左右指针都作为线索起作用的树称为中序线索树。考虑到中序线索树的复杂性，我们在后续章节中描述了这种（中序线索）线索树。

### 8.2.1 线索树的必要性

从之前的讨论可以明显看出，叶子节点没有子节点。因此，其左右指针表示为 NULL。随着层数的增加，NULL 指针的数量也会增加。只能单向遍历是 BST 的另一个主要局限性。为解决所有这些问题，使用线索树。在线索树中，我们将叶子的 NULL 指针连接如下：

- 左指针连接到中序前驱。
- 右指针连接到中序后继。
- 如果不存在前驱或后继，则在这种情况下 NULL 指针连接到根节点。

将指针附加到前驱和后继不仅消除了 NULL 指针，而且还便于向后遍历。在我们的后续讨论中，我们考虑了中序线索树。一旦读者能够实现中序线索树，实现左线索树或右线索树就可以轻松映射。

### 8.2.2 线索树的创建

中序线索树通常称为线索树。线索树的结构和节点的插入已在以下小节中讨论。

#### 8.2.2.1 表示中序线索树

中序线索树是 BST 的高级版本，其中还包括两个额外的组件。除了左右指针外，还管理两个线索的设置，即左线索和右线索。中序线索树的完整结构已在图 8.1 中说明。

| lthread | Left node | Data | rightNode | rthread |

Figure 8-1: Structure of an in-threaded tree

在上图中，所用符号的含义如下：

lthread: 表示左线索

leftnode: 表示左节点

info: data part of the tree

rightnode denotes the right node

rthread denotes the right thread

```
Pre-order successor in a Threaded tree
tnode * presucc( )
{
if(p->lthread==0)
return p->left;
else
{
tnode *succ=p->right;
while(p->rthread==1)
p=p->right;
}
return p;
}
```

### 8.3 线索树节点的类

用于表示图 8.1 所示的线索节点结构的类已在即将到来的程序中描述。与二叉搜索树（BST）类似，tnode（线索节点）的成员应为 public，否则这些成员在该类外部将不可见。

```
class tnode //class to create the thread tree node
{
public:
int info;
tnode *left,*right;
int lthread, rthread;  // to represent the left and right thread
tnode ()        //default constructor
{ }
tnode (int);
};
// Defining the constructor outside the class
tnode::tnode (int x)    //constructor with one argument
{
this->info=x;
lthread=rthread=1;
}
```

### 8.3.1 线索树的成员

与线索节点一致，可以创建一个类来表示线索树。该类将由线索节点和执行线索树中各种活动所需的功能组成。这些活动包括在线索树中插入项目、在线索树中遍历、在线索树中删除项目等。

```
// Class to represent the threaded tree
class thread
{
tnode *root;      // defining the threaded node
public:
thread ();
void insert (int);    // function to insert the element in threaded tree
void inorder ();
void in_order(tnode*);
void inorder_nr();// Non-recursive in order traversal
};
thread::thread() //initializing the root to zero
{
root=NULL;
}
```

在上述类中，root 已初始化为 NULL。因此，它可以表示线索树为空。

### 8.4 在线索树中插入节点

在线索树中插入项目/节点是一个复杂的过程，并且由于以下原因需要谨慎操作：

- 识别在线索树中插入节点的位置。
- 调整此新节点的左右指针。
- 调整作为新节点的父节点的节点的指针和线索。
- 考虑一种情况，即中序线索树中仅存在根节点，在这种情况下左右节点将没有节点。因此其左右线索将指向 NULL。
- 在所有其他情况下，左线索连接到中序前驱，右线索连接到中序后继。如果不存在前驱或后继。在这些情况下，线索将连接到根节点。

用于定义线索树所需各种数据成员和函数的类已描述如下：

```
Problem: To create threaded tree and inserting the node
class threadtree
{
threadnode *root; // Root of a threaded tree
void insert (int);      // function to insert the node
void inorder ();  // function for the in-order traversal
};
void threatree::insert (int x) // inserting the node in a threaded tree
{
if (root==NULL)
{
root=new threadnode;
root->data=x;
root->left=root;
root->right=root;
root->lthread=1;
root->rthread=1;
return;
}
r=root;
threadnode *newnode;
while (1)
{
if(x < r->info)
{
if(r->lthread!=0)
{
newnode->left=r->left;
r->lthread=0;
newnode->lthread=1;
newnode->right=r;
newnode->rthread=1;
```

