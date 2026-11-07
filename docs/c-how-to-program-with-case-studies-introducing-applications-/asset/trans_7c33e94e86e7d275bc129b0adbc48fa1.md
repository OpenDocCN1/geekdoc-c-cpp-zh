
```c
// self-referential structure
struct queueNode {
  char data; // define data as a char
  struct queueNode *nextPtr; // queueNode pointer
};

typedef struct queueNode QueueNode;
typedef QueueNode *QueueNodePtr;

// function prototypes
void printQueue(QueueNodePtr currentPtr);
int isEmpty(QueueNodePtr headPtr);
void enqueue(QueueNodePtr *headPtr, QueueNodePtr *tailPtr, char value);
char dequeue(QueueNodePtr *headPtr, QueueNodePtr *tailPtr);
void instructions(void);

int main(void) {
  QueueNodePtr headPtr = NULL; // initialize headPtr
  QueueNodePtr tailPtr = NULL; // initialize tailPtr
  char item = '\0'; // char input by user

  instructions(); // display the menu
  printf("\n%s", "? ");
  int choice = 0; // user's menu choice
  scanf("%d", &choice);

  // while user does not enter 3
  while (choice != 3) {
    switch (choice) {
      case 1: // enqueue value
        printf("\n%s", "Enter a character: ");
        scanf("\n%c", &item);
        enqueue(&headPtr, &tailPtr, item);
        printQueue(headPtr);
        break;
      case 2: // dequeue value
        // if queue is not empty
        if (!isEmpty(headPtr)) {
          item = dequeue(&headPtr, &tailPtr);
          printf("%c has been dequeued.\n", item);
        }

        printQueue(headPtr);
        break;
      default:
        puts("Invalid choice.\n");
        instructions();
        break;
    }

    printf("\n%s", "? ");
    scanf("%d", &choice);
  }

  puts("End of run.");
}

// display program instructions to user
void instructions(void) {
    printf("Enter your choice:\n"
           "  1 to add an item to the queue\n"
           "  2 to remove an item from the queue\n"
           "  3 to end\n");
}

// insert a node at queue tail
void enqueue(QueueNodePtr *headPtr, QueueNodePtr *tailPtr, char value) {
    QueueNodePtr newPtr = malloc(sizeof(QueueNode));

    if (newPtr != NULL) { // is space available?
        newPtr->data = value;
        newPtr->nextPtr = NULL;

        // if empty, insert node at head
        if (isEmpty(*headPtr)) {
            *headPtr = newPtr;
        }
        else {
            (*tailPtr)->nextPtr = newPtr;
        }

        *tailPtr = newPtr;
    }
    else {
        printf("%c not inserted. No memory available.\n", value);
    }
}

// remove node from queue head
char dequeue(QueueNodePtr *headPtr, QueueNodePtr *tailPtr) {
    char value = (*headPtr)->data;
    QueueNodePtr tempPtr = *headPtr;
    *headPtr = (*headPtr)->nextPtr;

    // if queue is empty
    if (*headPtr == NULL) {
        *tailPtr = NULL;
    }

    free(tempPtr);
    return value;
}
```

```text
? 2
C has been dequeued.
Queue is empty.

? 2
Queue is empty.

? 4
Invalid choice.

Enter your choice:
1 to add an item to the queue
2 to remove an item from the queue
3 to end
? 3
End of run.
```

**图12.3 | 操作和维护队列。（第5部分，共5部分）**

## 12.6.1 函数 enqueue

函数 enqueue（第72–92行）接收三个参数：

- `headPtr` 的地址——队列头指针，
- `tailPtr` 的地址——队列尾指针，以及
- 要插入的值。

该函数执行以下步骤：

1. 第73行调用`malloc`创建新节点，并将分配的内存位置赋给`newPtr`。
2. 如果内存分配正确，第76–77行将待插入的值赋给`newPtr->data`，并将`NULL`赋给`newPtr->nextPtr`。
3. 如果队列为空（第80行），第81行将`newPtr`赋给`*headPtr`，因为新节点既是队列的头也是队列的尾；否则，第84行将`newPtr`赋给`(*tailPtr)->nextPtr`，因为新节点是新的尾节点。
4. 第87行将`newPtr`赋给`*tailPtr`，以更新尾指针，使其指向新的尾节点。

### 演示入队操作

下图演示入队操作。图(a)显示操作前main中的`headPtr`和`tailPtr`以及enqueue的新节点。图(b)中的虚线箭头说明了前面讨论中的步骤3和4，这些步骤将新节点添加到非空队列的尾部。

![](img/43d318ad505997c339a3ea78d716d162_675_0.png)

## 12.6.2 函数 dequeue

函数 dequeue（第95–107行）接收队列头尾指针的地址作为参数，并移除队列的第一个节点。出队操作执行以下步骤：

1. 第96行将`(*headPtr)->data`赋给value，以保存被出队的数据。
2. 第97行将`*headPtr`赋给`tempPtr`，用于释放内存。
3. 第98行将`(*headPtr)->nextPtr`赋给`*headPtr`，使得main中的队列头指针现在指向新的头节点。
4. 第101行检查`*headPtr`是否为`NULL`。如果是，第102行将`NULL`赋给`*tailPtr`，因为此时队列为空。
5. 第105行释放`tempPtr`指向的内存。
6. 第106行将value返回给调用者。

### 演示出队操作

下图演示函数 dequeue。图(a)显示出队操作前的队列——`headPtr`和`*tailPtr`用于修改main中的`headPtr`和`tailPtr`。图(b)显示`tempPtr`指向被出队的节点，并且main中的`headPtr`已更新为指向队列的新首节点。

![](img/43d318ad505997c339a3ea78d716d162_675_1.png)

## 自测

1. （多选题）以下关于队列的说法哪一项是错误的？

    - a) 队列类似于杂货店的结账队列——排队的第一人先接受服务，其他顾客在队尾加入并等待服务。
    - b) 队列节点只能从队列头部（开始处）移除，且只能在队列尾部（末端）插入。
    - c) 队列是一种先进后出（FILO）的数据结构。
    - d) 插入和移除操作分别称为入队（发音“en-cue”）和出队（发音“dee-cue”）。

    答案：（c）是错误的。实际上，队列是一种先进先出（FIFO）的数据结构。

2. （填空题）对于当今的______系统，可能同时运行的程序数量多于处理器数量，因此当前未运行的程序会被放入队列，直到当前忙碌的处理器变为可用。

    答案：多核。

## 12.7 树

到目前为止，我们介绍了线性数据结构——链表、栈和队列。树是一种非线性、二维的数据结构，具有特殊性质。树的节点包含两个或多个链接。本节讨论二叉树——其节点包含两个链接，如下图所示：

![](img/43d318ad505997c339a3ea78d716d162_676_0.png)

每个节点中的两个链接可能为`NULL`、其中一个为`NULL`，或两个都不为`NULL`。根节点是树中的第一个节点。根节点上的每个链接指向一个子节点。左子节点是左子树中的第一个节点，右子节点是右子树中的第一个节点。给定节点的子节点称为兄弟节点。没有子节点的节点是叶节点。如果不将叶节点的链接设置为`NULL`，可能导致运行时错误。计算机科学家通常将树绘制为根节点位于顶部——这与自然界中的树正好相反。

### 二叉搜索树

本节介绍一个包含唯一值的二叉搜索树，其特点是任何左子树中的值都小于其父节点的值，而任何右子树中的值都大于其父节点的值。下图展示了一个包含九个值的二叉搜索树：

![](img/43d318ad505997c339a3ea78d716d162_677_0.png)

对于一组数据，二叉搜索树的形状可能不同，这取决于插入其值的顺序。

### 实现二叉搜索树

图12.4创建了一棵二叉搜索树并遍历其节点——即访问树中的每个节点以对节点值执行某些操作，例如显示它们。我们将以三种方式遍历树——中序遍历、前序遍历和后序遍历。程序生成10个随机数并将每个随机数插入树中，但重复值会被丢弃。第9–13行定义了`struct treeNode`，用于表示树的节点。我们再次使用`typedef`（第15–16行）使代码更具可读性。

```c
// fig12_04.c
// Creating and traversing a binary tree
// preorder, inorder, and postorder
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// self-referential structure
struct treeNode {
   struct treeNode *leftPtr; // pointer to left subtree
   int data; // node value
   struct treeNode *rightPtr; // pointer to right subtree
};

typedef struct treeNode TreeNode; // synonym for struct treeNode
typedef TreeNode *TreeNodePtr; // synonym for TreeNode *

// prototypes
void insert(TreeNodePtr *treePtr, int value);
void inOrder(TreeNodePtr treePtr);
void preOrder(TreeNodePtr treePtr);
void postOrder(TreeNodePtr treePtr);

int main(void) {
   TreeNodePtr rootPtr = NULL; // tree initially empty
```

**图12.4 | 创建并遍历二叉树。（第1部分，共3部分）**

