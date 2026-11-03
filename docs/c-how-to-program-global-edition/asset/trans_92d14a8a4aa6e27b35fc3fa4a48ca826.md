
```cpp
// insert random values between 0 and 14 in the tree
for (unsigned int i = 1; i <= 10; ++i) {
    int item = rand() % 15;
    printf("%3d", item);
    insertNode(&rootPtr, item);
}

// traverse the tree preOrder
puts("\n\nThe preOrder traversal is:");
preOrder(rootPtr);

// traverse the tree inOrder
puts("\n\nThe inOrder traversal is:");
inOrder(rootPtr);

// traverse the tree postOrder
puts("\n\nThe postOrder traversal is:");
postOrder(rootPtr);
}

// insert node into tree
void insertNode(TreeNodePtr *treePtr, int value)
{
    // if tree is empty
    if (*treePtr == NULL) {
        *treePtr = malloc(sizeof(TreeNode));

        // if memory was allocated, then assign data
        if (*treePtr != NULL) {
            (*treePtr)->data = value;
            (*treePtr)->leftPtr = NULL;
            (*treePtr)->rightPtr = NULL;
        } else {
            printf("%d not inserted. No memory available.\n", value);
        }
    }
    else { // tree is not empty
        // data to insert is less than data in current node
        if (value < (*treePtr)->data) {
            insertNode(&((*treePtr)->leftPtr), value);
        }

        // data to insert is greater than data in current node
        else if (value > (*treePtr)->data) {
            insertNode(&((*treePtr)->rightPtr), value);
        }
        else { // duplicate data value ignored
            printf("%s", "dup");
        }
    }
}
```

**图 12.19** | 创建并遍历二叉树。（第 2 部分，共 3 部分。）

```c
85 // begin inorder traversal of tree
86 void inOrder(TreeNodePtr treePtr)
87 {
88    // if tree is not empty, then traverse
89    if (treePtr != NULL) {
90       inOrder(treePtr->leftPtr);
91       printf("%3d", treePtr->data);
92       inOrder(treePtr->rightPtr);
93    }
94 }
95
96 // begin preorder traversal of tree
97 void preOrder(TreeNodePtr treePtr)
98 {
99    // if tree is not empty, then traverse
100   if (treePtr != NULL) {
101      printf("%3d", treePtr->data);
102      preOrder(treePtr->leftPtr);
103      preOrder(treePtr->rightPtr);
104   }
105 }
106
107 // begin postorder traversal of tree
108 void postOrder(TreeNodePtr treePtr)
109 {
110   // if tree is not empty, then traverse
111   if (treePtr != NULL) {
112      postOrder(treePtr->leftPtr);
113      postOrder(treePtr->rightPtr);
114      printf("%3d", treePtr->data);
115   }
116 }
```

**图 12.19** | 创建并遍历二叉树。（第 3 部分，共 3 部分。）

放入树中的数字为：
   6 7 4 12 7dup 2 2dup 5 7dup 11

前序遍历为：
   6 4 2 5 7 12 11

中序遍历为：
   2 4 5 6 7 11 12

后序遍历为：
   2 5 4 11 12 7 6

**图 12.20** | 图 12.19 中程序的示例输出。

### 12.7.1 函数 insertNode

图 12.19 中用于创建二叉搜索树并遍历它的函数是*递归的*。函数 insertNode（第 53–83 行）接收*树的地址*和一个要存储在树中的整数作为参数。在二叉搜索树中，节点只能作为叶节点插入。在二叉搜索树中插入节点的步骤如下：

- 1. 如果 `*treePtr` 为 NULL（第 56 行），则创建一个新节点（第 57 行）。调用 `malloc`，将分配的内存赋给 `*treePtr`，将要存储的整数赋给 `(*treePtr)->data`（第 61 行），将值 NULL 赋给 `(*treePtr)->leftPtr` 和 `(*treePtr)->rightPtr`（第 62–63 行），并将控制权返回给调用者（`main` 或先前对 `insertNode` 的调用）。
- 2. 如果 `*treePtr` 的值不为 NULL，且要插入的值小于 `(*treePtr)->data`，则用 `(*treePtr)->leftPtr` 的地址（第 72 行）调用函数 `insertNode`，以将该节点插入到 `treePtr` 所指向节点的左子树中。如果要插入的值大于 `(*treePtr)->data`，则用 `(*treePtr)->rightPtr` 的地址（第 77 行）调用函数 `insertNode`，以将该节点插入到 `treePtr` 所指向节点的右子树中。

递归步骤持续进行，直到找到 NULL 指针，然后由 `Step 1` 插入新节点。

### 12.7.2 遍历：函数 inOrder、preOrder 和 postOrder

函数 `inOrder`（第 86–94 行）、`preOrder`（第 97–105 行）和 `postOrder`（第 108–116 行）各自接收一个 `tree`（即指向树根节点的指针）并遍历该树。

`inOrder` 遍历的步骤如下：

- 1. 按 `inOrder` 遍历*左*子树。
- 2. 处理该节点中的值。
- 3. 按 `inOrder` 遍历*右*子树。

节点中的值要等到其*左*子树中的值处理完毕后才会被处理。图 12.21 中树的 `inOrder` 遍历结果为：

`6 13 17 27 33 42 48`

对二叉搜索树进行 `inOrder` 遍历会按*升序*打印节点值。创建二叉搜索树的过程实际上会对数据排序——因此该过程称为二叉树排序。

`preOrder` 遍历的步骤如下：

- 1. 处理该节点中的值。
- 2. 按 `preOrder` 遍历*左*子树。
- 3. 按 `preOrder` 遍历*右*子树。

每个节点中的值在访问该节点时即被处理。处理完给定节点中的值后，先处理*左*子树中的值，再处理*右*子树中的值。图 12.21 中树的*前序*遍历结果为：

`27 13 6 17 42 33 48`

![](img/bf54db922e6fa8319cba11069e785521_531_0.png)

**图 12.21** | 含七个节点的二叉搜索树。

*后序*遍历的步骤如下：

- 1. 按 postOrder 遍历*左*子树。
- 2. 按 postOrder 遍历*右*子树。
- 3. 处理该节点中的值。

每个节点中的值要等到其子节点的值打印后才会打印。图 12.21 中树的后序遍历结果为：

`6 17 13 33 48 42 27`

### 12.7.3 重复值消除

二叉搜索树便于消除重复值。在创建树的过程中，尝试插入重复值会被识别出来，因为重复值在每次比较时会做出与原值相同的“向左”或“向右”决策。因此，该重复值最终会与树中包含相同值的节点进行比较。此时可以简单地丢弃该重复值。

### 12.7.4 二叉树搜索

在二叉树中搜索与键值匹配的值也很快。如果树是紧凑填充的，则每一层包含的元素数量约为上一层的两倍。因此，含有 n 个元素的二叉搜索树最多有 log₂n 层，因而无论要找到匹配项还是确定不存在匹配项，最多需要进行 log₂n 次比较。例如，这意味着在搜索（紧凑填充的）1,000 元素二叉搜索树时，最多只需进行 10 次比较，因为 2¹⁰ > 1,000。在搜索（紧凑填充的）1,000,000 元素二叉搜索树时，最多只需进行 20 次比较，因为 2²⁰ > 1,000,000。

### 12.7.5 其他二叉树操作

练习中给出了若干其他二叉树操作的算法，例如以二维树形格式打印二叉树，以及对二叉树执行*层序遍历*。层序遍历从根节点层开始*逐行*访问树的节点。在树的每一层，节点按从左到右的顺序访问。其他二叉树练习包括：允许二叉搜索树包含重复值、在二叉树中插入字符串值，以及确定二叉树包含多少层。

## 12.8 安全的 C 编程

*CERT 安全 C 编码标准*第 8 章专门讨论内存管理建议和规则——其中许多适用于本章介绍的指针和动态内存分配的使用。如需更多信息，请访问 www.securecoding.cert.org。

- MEM01-C/MEM30-C：不应让指针保持未初始化状态。相反，应将它们赋值为 NULL 或内存中有效项的地址。当你使用 free 释放动态分配的内存时，传给 free 的指针不会被赋予新值，因此它仍指向动态分配内存原先所在的内存位置。使用这种“悬空”指针可能导致程序崩溃和安全漏洞。当你释放动态分配的内存时，应立即将该指针赋值为 NULL 或有效地址。对于在调用 free 后立即离开作用域的局部指针变量，我们选择不这样做。
- MEM01-C：当你尝试使用 free 释放已经释放过的动态内存时，会发生未定义行为——这称为“双重释放漏洞”。为确保不会尝试多次释放同一块内存，请在调用 free 后立即将指针设置为 NULL——尝试释放 NULL 指针不会产生任何效果。
- ERR33-C：大多数标准库函数都会返回值，使你能够判断这些函数是否正确完成了任务。例如，如果函数 malloc 无法分配所请求的内存，就会返回 NULL。在尝试使用存储 malloc 返回值的指针之前，你应始终确保 malloc 没有返回 NULL。

## 小结

### 第 12.1 节 引言

- 动态数据结构（第 510 页）在执行时增长和收缩。
- 链表（第 510 页）是“排成一行”的数据项集合——插入和删除可在链表中的任意位置进行。
- 对于栈（第 510 页），插入和删除只能在栈顶（第 510 页）进行。
- 队列（第 510 页）表示等待队列；插入在队列的后端（也称为尾部；第 510 页）进行，删除从队列的前端（也称为头部；第 510 页）进行。
- 二叉树有助于高速搜索和排序数据、高效消除重复数据项、表示文件系统目录，以及将表达式编译为机器语言。

### 第 12.2 节 自引用结构

- 自引用结构（第 511 页）包含一个指针成员，该成员指向同一类型的结构。
- 自引用结构可以链接在一起，形成链表、队列、栈和树。
- NULL 指针（第 511 页）通常表示数据结构的末尾。

### 第 12.3 节 动态内存分配

- 创建和维护动态数据结构需要动态内存分配（第 511 页）。
- 函数 malloc 和 free 以及运算符 sizeof 对动态内存分配至关重要。
- 函数 malloc（第 511 页）接收要分配的字节数，并返回一个指向所分配内存的 void * 指针。
- void * 指针可以赋给任何指针类型的变量。
- 函数 malloc 通常与 sizeof 运算符一起使用。
