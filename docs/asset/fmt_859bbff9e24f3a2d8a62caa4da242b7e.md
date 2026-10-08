
上述是倾斜二叉树。在这里，每个左子树再次表示左子树。这种类型的二叉树被称为左斜二叉树。同样，也存在右斜二叉树 [见图 9.17 (a) 和 9.17 (b)]。图 9.18 显示了左斜和右斜树的数组表示法。

![](img/c2f6b24e88575cdba9137937a75b3615_333_0.png)

图 9.17 (a) 左斜二叉树

![](img/c2f6b24e88575cdba9137937a75b3615_333_1.png)

图 9.17 (b) 右斜二叉树

| | X |
|---|---|
| 1 | Y |
| 2 | Z |
| 3 | S |
| 4 | T |
| 5 | U |
| 6 | V |

右斜二叉树

左斜二叉树

图 9.18 左-右斜二叉树

### 9.8.2 二叉树的链式表示

二叉树的另一种表示方法是链表，已知它比数组表示法更节省内存。二叉树的基础组件是节点。我们知道节点由三个字段组成，如图 9.19 所示。

- 数据 `Data`
- 左孩子
- 右孩子

| `Lchild` | `Data` | `Rchild` |
|---|---|---|

![](img/c2f6b24e88575cdba9137937a75b3615_333_2.png)

图 9.19 二叉树的链表表示

`Data`字段存储给定的值。`lchild`字段是链接字段，持有其左节点的地址。同样，`rchild`持有右节点的地址。节点可以逻辑上表示如下。图 9.20 和 9.21 显示了二叉树的链表表示。

#### 使用 C 语言的数据结构

```c
struct node {
  int data;
  struct node *rchild;
  struct node *lchild;
};
```

![](img/c2f6b24e88575cdba9137937a75b3615_334_0.png)

![](img/c2f6b24e88575cdba9137937a75b3615_334_1.png)

二叉树有一个根节点和若干个非终端节点和终端节点。终端节点被称为叶子节点。非终端节点有它们的左、右孩子节点。然而，终端节点没有孩子。在实现此时，`lchild`和`rchild`字段被保持为`NULL`。非终端节点被称为内部节点，终端节点被称为外部节点。

## 9.9 二叉树的操作

在二叉树上执行以下基本操作：

- **创建** `Create`：此操作创建一个空的二叉树。
- **构造** `Make`：此操作创建一个新的二叉树。该节点的数据字段持有某些值。
- **判空** `Empty`：当二叉树为空时，此函数返回`true`，否则返回`false`。
- **左孩子** `Lchild`：返回左孩子的指针。当节点没有左孩子时，返回`NULL`指针。
- **右孩子** `Rchild`：返回右孩子的指针，如果节点没有右孩子则返回`NULL`指针。
- **父亲** `Father`：返回节点父亲的指针，否则返回`NULL`指针。
- **兄弟** `Sibling`：返回节点兄弟的指针，否则返回`NULL`指针。
- **数据** `Data`：返回存储的值。

### 树 9.15

除了上述操作外，二叉树上还可以执行以下操作：

1. 树的遍历
2. 插入节点
3. 删除节点
4. 查找给定节点
5. 复制二叉树。

## 9.10 二叉树的遍历

形成二叉树需要三个参数。它们是节点、左子树和右子树。遍历是二叉树上最重要的操作之一，这种操作经常在数据结构上被执行。遍历意味着逐个通过树的每一个节点。每棵树只被遍历一次。假设根由`O`表示，左子树由`L`表示，右子树由`R`表示。以下是遍历组合：

1. `ORL` - 根 - 左-左
2. `OLR` - 根 - 左-右
3. `LOR` - 左 - 根 - 右
4. `LRO` - 左 - 右 - 右
5. `R` - 右 - 根 - 左
6. `RLO` - 右 - 左-根

六种方法中只有三种是标准方法，并在本章中讨论。在遍历时，总是左子树之后遍历右子树。因此，`OLR`是前序`preorder`，`LOR`是中序`inorder`，`LRO`是后序`postorder`。图 9.22 显示了一个模型树（二叉树）

![](img/c2f6b24e88575cdba9137937a75b3615_335_0.png)

图 9.22 模型树

![](img/c2f6b24e88575cdba9137937a75b3615_335_1.png)

### 树 9.19

![](img/c2f6b24e88575cdba9137937a75b3615_339_0.png)

图 9.27 前序遍历树

图 9.27 的前序遍历为`M, N, P, Q, O, R, S`和`V`。这也可以如图 9.28 所示。在这种遍历中，根节点首先访问，最后是左子树和右子树。

![](img/c2f6b24e88575cdba9137937a75b3615_339_1.png)

图 9.28 前序遍历

在先序遍历中，左子树为`N, P`和`Q`，右子树为`O, R, S`和`V`。

> 示例 9.3 编写一个程序向树中插入元素并以前序显示它们。

```c
#include <stdio.h>
#include <conio.h>
struct tree {
    long data;
    struct tree *left;
    struct tree *right;
};
struct tree *btree=NULL;
struct tree *insert(struct tree*btree,long digit);
void main()
{
    long digit;
    clrscr();
    puts("Enter integers: and 0 to quit");
    scanf("%ld",&digit);
    while(digit!=0)
    {
        btree= insert (btree,digit);
        scanf("%ld",&digit);
    }
    puts("\nPreorder traversing btree:\n\n");
    preorder(btree);
}
struct tree*insert(struct tree*btree,long digit)
{
    if (btree==NULL)
    {
        btree=(struct tree*) malloc(sizeof(struct tree));
        btree->left=btree->right=NULL;
        btree->data=digit;
    }
    else
    {
        if (digit<btree->data)
            btree->left=insert(btree->left,digit);
        else
            if (digit>btree->data)
                btree->right=insert(btree->right, digit);
            else
                if (digit==btree->data)
                {
                    puts("Duplicates nodes: Program exited");
                    exit(0);
                }
    }
    return(btree);
}
void preorder(struct tree*btree)
{
    if (btree!=NULL)
    {
        printf("%4ld",btree->data);
        preorder(btree->left);
        preorder(btree->right);
    }
}
```

OUTPUT

Enter integers: and 0 to quit

5 2 1 7

Preorder traversing btree:

5 2 1 7

![](img/c2f6b24e88575cdba9137937a75b3615_340_0.png)

#### 解析：

该程序将二叉树存储在结构`tree`的结构变量`*btree*`中。通过调用`insert()`插入元素。使用`preorder()`完成前序遍历。图 9.29 显示了程序中插入的`*btree*`。

二叉树的前序序列为`5, 2, 1, 7`。

### 9.10.3 后序遍历

在后序遍历中，首先遍历左子树和右子树，最后访问根节点。非空二叉树的后序遍历实现如下：

- 1. 首先，以后序方式遍历左子树。
- 2. 然后，以后序遍历右子树。
- 3. 最后，访问根节点 `N`。

在这种类型中，左、右子树被递归处理。首先以后序遍历左子树。之后，以后序遍历右子树。最后，显示根节点的数据。

图 9.30 的后序遍历为`P, Q, N, R, V, S, O`和`M`。这也可以如图 9.31 所示。在这种遍历中，首先遍历左子树，然后是右子树，最后是根节点。

在后序中，左子树为`P, Q`和`N`，右子树为`R, V, S`和`O`。

![](img/c2f6b24e88575cdba9137937a75b3615_341_0.png)

![](img/c2f6b24e88575cdba9137937a75b3615_341_1.png)

> 示例 9.4 向树中插入节点并用后序方法遍历这些节点的程序。

```c
#include <stdio.h>
#include <conio.h>
struct tree
{
    long data;
    struct tree *left;
    struct tree *right;
};
struct tree *btree=NULL;
struct tree *insert(struct tree*btree,long digit);
void postorder(struct tree*btree);
void main()
{
    long digit;
    clrscr();
    puts("Enter integers: and 0 to quit\n");
    scanf("%ld",&digit);
    while(digit!=0)
    {
        btree= insert(btree,digit);
        scanf("%ld",&digit);
    }
    puts("Postorder traversing btree:\n");
    postorder(btree);
struct tree *insert(struct tree*btree,long digit)
{
    if (btree==NULL)
    {
        btree=(struct tree*) malloc(sizeof(struct tree));
        btree->left=btree->right=NULL;
        btree->data=digit;
    }
    else
    {
        if (digit<btree->data)
            btree->left=insert(btree->left,digit);
        else
            if (digit>btree->data)
                btree->right=insert(btree->right,digit);
            else
            if (digit==btree->data)
            {
                puts("Duplicates nodes: Program exited\n");
                exit(0);
            }
    }
    return(btree);
}
void postorder(struct tree*btree)
{
    if (btree!=NULL)
    {
        postorder(btree->left);
        postorder(btree->right);
        printf("%ld",btree->data);
    }
}
```

OUTPUT
Enter integers: and 0 to quit
5 3 4 1 9 7
Postorder traversing btree:
1 4 3 7 9 5

#### 解析：

在此程序中，`*btree*`用于存储二叉树。`*btree*`是结构`tree`的变量。在此程序中，调用`insert()`在`*btree*`中插入元素。`postorder()`用于后序方式遍历二叉树。图 9.32 显示了程序中插入的`btree`。图 9.32 中树的后序遍历为`1, 4, 3, 7, 9`和`5`。

![](img/c2f6b24e88575cdba9137937a75b3615_343_0.png)

图 9.32 示例 9.5 编写一个菜单驱动程序实现 (1) 中序 (2) 前序和 (3) 后序。

```c
#include <stdio.h>
#include <conio.h>
struct tree {
    long data;
    struct tree *left;
    struct tree *right;
};
struct tree *btree=NULL;
struct tree *insert(struct tree*btree,long digit);
void inorder(struct tree*btree);
void preorder(struct tree*btree);
void postorder(struct tree*btree);
void main() {
    long digit;
    int ch;
    clrscr();
    puts("Enter integers: and 0 to quit");
    scanf("%ld",&digit);
    while(digit!=0) {
    btree = insert(btree,digit);
    scanf("%ld",&digit);
    }
    while(1)
    {
        clrscr();
        printf("1. Inorder traversal of btree\n");
        printf("2. Preorder traversal of btree\n");
        printf("3. Postorder traversal of btree\n");
        printf("4. Exit\n");
        printf("Enter the choice: ");
        scanf("%d",&ch);
        switch (ch)
        {
            case 1: printf("The inorder traversing of tree\n");
                inorder(btree);
                getch(); break;
            case 2: printf("The Preorder traversing of tree\n");
```
