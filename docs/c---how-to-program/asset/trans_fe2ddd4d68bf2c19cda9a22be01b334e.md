
## 常见编程错误 12.7

*不将树中叶节点的链接设置为 NULL 可能导致运行时错误。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_534_0.png)

**图 12.18** | 二叉搜索树。

图 12.19（输出如图 12.20 所示）创建一棵二叉搜索树，并以三种方式*遍历*它——中序、前序和后序。该程序生成 10 个随机数，并将每个数插入树中，但*重复*值会被*丢弃*。

```c
// Fig. 12.19: fig12_19.c
// Creating and traversing a binary tree
// preorder, inorder, and postorder
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// self-referential structure
struct treeNode {
   struct treeNode *leftPtr;  // pointer to left subtree
   int data;                  // node value
   struct treeNode *rightPtr; // pointer to right subtree
};

typedef struct treeNode TreeNode;   // synonym for struct treeNode
typedef TreeNode *TreeNodePtr;       // synonym for TreeNode*

// prototypes
void insertNode(TreeNodePtr *treePtr, int value);
void inOrder(TreeNodePtr treePtr);
void preOrder(TreeNodePtr treePtr);
void postOrder(TreeNodePtr treePtr);

// function main begins program execution
int main(void)
{
   TreeNodePtr rootPtr = NULL; // tree initially empty

   srand(time(NULL));
   puts("The numbers being placed in the tree are:");
```

**图 12.19** | 创建并遍历二叉树。（第 1 部分，共 3 部分。）

```c
32    // insert random values between 0 and 14 in the tree
33    for (unsigned int i = 1; i <= 10; ++i) {
34       int item = rand() % 15;
35       printf("%d", item);
36       insertNode(&rootPtr, item);
37    }

39    // traverse the tree preOrder
40    puts("\n\nThe preOrder traversal is:");
41    preOrder(rootPtr);

43    // traverse the tree inOrder
44    puts("\n\nThe inOrder traversal is:");
45    inOrder(rootPtr);

47    // traverse the tree postOrder
48    puts("\n\nThe postOrder traversal is:");
49    postOrder(rootPtr);
50    }

52    // insert node into tree
53    void insertNode(TreeNodePtr *treePtr, int value)
54    {
55       // if tree is empty
56       if (*treePtr == NULL) {
57          *treePtr = malloc(sizeof(TreeNode));

59          // if memory was allocated, then assign data
60          if (*treePtr != NULL) {
61             (*treePtr)->data = value;
62             (*treePtr)->leftPtr = NULL;
63             (*treePtr)->rightPtr = NULL;
64          }
65          else {
66             printf("%d not inserted. No memory available.\n", value);
67          }
68       }
69       else { // tree is not empty
70          // data to insert is less than data in current node
71          if (value < (*treePtr)->data) {
72             insertNode(&((*treePtr)->leftPtr), value);
73          }

75          // data to insert is greater than data in current node
76          else if (value > (*treePtr)->data) {
77             insertNode(&((*treePtr)->rightPtr), value);
78          }
79          else { // duplicate data value ignored
80             printf("%s", "dup");
81          }
82       }
83    }
```

图 12.19 | 创建并遍历二叉树。（第 2 部分，共 3 部分。）

```c
85  // begin inorder traversal of tree
86  void inOrder(TreeNodePtr treePtr)
87  {
88      // if tree is not empty, then traverse
89      if (treePtr != NULL) {
90          inOrder(treePtr->leftPtr);
91          printf("%3d", treePtr->data);
92          inOrder(treePtr->rightPtr);
93      }
94  }
95
96  // begin preorder traversal of tree
97  void preOrder(TreeNodePtr treePtr)
98  {
99      // if tree is not empty, then traverse
100     if (treePtr != NULL) {
101         printf("%3d", treePtr->data);
102         preOrder(treePtr->leftPtr);
103         preOrder(treePtr->rightPtr);
104     }
105 }
106
107 // begin postorder traversal of tree
108 void postOrder(TreeNodePtr treePtr)
109 {
110     // if tree is not empty, then traverse
111     if (treePtr != NULL) {
112         postOrder(treePtr->leftPtr);
113         postOrder(treePtr->rightPtr);
114         printf("%3d", treePtr->data);
115     }
116 }
```

图 12.19 | 创建并遍历二叉树。（第 3 部分，共 3 部分。）

```
The numbers being placed in the tree are:
  6  7  4 12  7dup  2  2dup  5  7dup 11

The preOrder traversal is:
  6  4  2  5  7 12 11

The inOrder traversal is:
  2  4  5  6  7 11 12

The postOrder traversal is:
  2  5  4 11 12  7  6
```

**图 12.20** | 图 12.19 程序的示例输出。

### 12.7.1 函数 insertNode

图 12.19 中用于创建二叉搜索树并遍历它的函数是*递归的*。函数 `insertNode`（第 53—83 行）接收*树的地址*和一个要存储在树中的整数作为参数。在二叉搜索树中，节点只能作为*叶节点*插入。在二叉搜索树中插入节点的步骤如下：

- 1. 如果 `*treePtr` 为 NULL（第 56 行），则创建一个新节点（第 57 行）。调用 `malloc`，将分配的内存赋给 `*treePtr`，将要存储的整数赋给 `(*treePtr)->data`（第 61 行），将 NULL 值赋给 `(*treePtr)->leftPtr` 和 `(*treePtr)->rightPtr`（第 62—63 行），并将控制权返回给调用者（`main` 或之前对 `insertNode` 的调用）。

- 2. 如果 `*treePtr` 的值不为 NULL，且要插入的值*小于* `(*treePtr)->data`，则用 `(*treePtr)->leftPtr` 的地址（第 72 行）调用函数 `insertNode`，以将该节点插入 `*treePtr` 所指向节点的*左*子树中。如果要插入的值*大于* `(*treePtr)->data`，则用 `(*treePtr)->rightPtr` 的地址（第 77 行）调用函数 `insertNode`，以将该节点插入 `*treePtr` 所指向节点的*右*子树中。

这些*递归*步骤会一直继续，直到找到 NULL 指针，然后由*步骤 1*插入新节点。

### 12.7.2 遍历：函数 inOrder、preOrder 和 postOrder

函数 `inOrder`（第 86—94 行）、`preOrder`（第 97—105 行）和 `postOrder`（第 108—116 行）各自接收一棵*树*（即*指向树根节点的指针*），并*遍历*该树。

- 1. 按 `inOrder` 遍历*左*子树。
- 2. 处理该节点中的值。
- 3. 按 `inOrder` 遍历*右*子树。

节点中的值要等到其*左*子树中的值处理完毕后才会被处理。图 12.21 中树的中序遍历结果为：

6 13 17 27 33 42 48

二叉搜索树的中序遍历会按*升序*打印节点值。创建二叉搜索树的过程实际上会对数据排序——因此该过程称为二叉树排序。

前序遍历的步骤如下：

- 1. 处理该节点中的值。
- 2. 按 `preOrder` 遍历*左*子树。
- 3. 按 `preOrder` 遍历*右*子树。

![](img/d0d3b7423c2d9e5650be79209ea1885d_537_0.png)

**图 12.21** | 包含七个节点的二叉搜索树。

- **MEM01-C/MEM30-C:** 指针不应保持未初始化状态。相反，应将它们赋值为 `NULL` 或内存中有效项的地址。当你使用 `free` 释放动态分配的内存时，传给 `free` 的指针不会被赋予新值，因此它仍然指向动态分配内存*曾经*所在的内存位置。使用这种“悬空”指针可能导致程序崩溃和安全漏洞。当你释放动态分配的内存时，应立即将该指针赋值为 `NULL` 或一个有效地址。对于在调用 `free` 后立即超出作用域的局部指针变量，我们选择不这样做。
- **MEM01-C:** 当你尝试使用 `free` 释放已经释放过的动态内存时，会发生未定义行为——这称为“双重释放漏洞”。为确保不会多次尝试释放同一内存，在调用 `free` 后立即将指针设置为 `NULL`——尝试释放 `NULL` 指针没有效果。
- **ERR33-C:** 大多数标准库函数会返回值，使你能够确定函数是否正确地完成了任务。例如，如果函数 `malloc` 无法分配请求的内存，则返回 `NULL`。在尝试使用存储 `malloc` 返回值的指针之前，你应*始终*确保 `malloc` 没有返回 `NULL`。

## 小结

### 第 12.1 节 引言

- 动态数据结构（第 510 页）在程序执行时增长和收缩。
- 链表（第 510 页）是“排成一行”的数据项集合——插入和删除可在链表中的任何位置进行。
- 对于栈（第 510 页），插入和删除只在栈顶（第 510 页）进行。
- 队列（第 510 页）表示等待队列；插入在队列的后端（也称为尾部；第 510 页）进行，删除从队列的前端（也称为头部；第 510 页）进行。
- 二叉树有助于高速搜索和排序数据、高效消除重复数据项、表示文件系统目录，以及将表达式编译为机器语言。

### 第 12.2 节 自引用结构

- 自引用结构（第 511 页）包含一个指向同类型结构的指针成员。
- 自引用结构可以链接在一起，形成链表、队列、栈和树。
- `NULL` 指针（第 511 页）通常表示数据结构的结束。

### 第 12.3 节 动态内存分配

- 创建和维护动态数据结构需要动态内存分配（第 511 页）。
- 函数 `malloc` 和 `free`，以及运算符 `sizeof`，对于动态内存分配至关重要。
- 函数 `malloc`（第 511 页）接收要分配的字节数，并返回指向所分配内存的 `void *` 指针。`void *` 指针可以赋给任何指针类型的变量。
- 函数 `malloc` 通常与 `sizeof` 运算符一起使用。
