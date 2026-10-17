
链表是计算机科学中的基础数据结构，在某些场景下比数组具有独特优势。数组具有固定大小并需要连续内存分配，而链表是动态的，可根据需要分配内存。本节将深入探讨 C 语言中链表的实现细节，涵盖创建、插入、删除和遍历操作。

## 理解链表
链表是节点的集合，每个节点包含一个数据和一个指向序列中下一个节点的指针。第一个节点称为“头节点（`head`）”，最后一个节点指向链表的末尾。链表的主要操作包括插入、删除和遍历。

- 向列表中插入一个新节点。
- 从列表中删除一个节点。
- 顺序遍历列表中的每个节点。

### 节点结构
实现链表的第一步是定义节点的结构体。在 C 语言中，这通过以下代码实现：

```c
typedef struct Node {
    int data;
    Node* next;
} Node;
```

### 创建链表
要创建一个链表，我们首先将头节点初始化为 `NULL`，表示链表为空。然后我们可以使用各种插入技术向列表中添加节点。

```c
Node* createLinkedList() { return NULL; // NULL 头节点表示空链表。 }
```

### 插入操作
链表的插入可以通过多种方式进行：

- 在列表头部插入。
- 在给定节点之后插入。
- 在列表末尾插入。

#### 在头部插入
这涉及创建一个新节点，并其 `next` 指向当前头节点，然后将头节点更新为此新节点。

```c
void insertAtBeginning(Node** head, int newData) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = newData;
    newNode->next = *head;
    *head = newNode;
}
```

代码输出：

在头部插入后：5 -> 3 -> 1 -> NULL

#### 在给定节点之后插入
这涉及调整给定节点的 `next` 指针指向新节点，并让新节点的 `next` 指向之前该节点之后的节点。

```c
void insertAfterNode(Node* prevNode, int newData) {
    if (prevNode == NULL) // 不能在 NULL 后插入
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = newData;
    newNode->next = prevNode->next;
    prevNode->next = newNode;
}
```

### 删除操作
链表的删除可以通过定位要删除的节点并调整指针以跳过被删除节点来实现。

#### 按键删除
在这里，我们搜索具有特定键的节点，然后更新指针将其从列表中移除。

```c
void deleteNodeByKey(Node** head, int key) {
    Node *temp = *head, *prev = NULL;
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }
    if (temp == NULL) // 未找到键值
    if (prev == NULL) *head = temp->next;
    else prev->next = temp->next;
    free(temp);
}
```

### 遍历
遍历链表涉及顺序访问每个节点直到到达末尾。这通常使用循环来访问每个节点。

```c
void printLinkedList(Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
}
```

通过理解并实现这些操作，你获得了动态管理数据结构的灵活性，可以根据应用程序的特定需求进行定制。链表是更复杂结构（如栈、队列，甚至是图的表示）的基础，展示了它们在计算机科学中的多功能性和重要性。

## 3.2 利用树进行高效排序和检索

树是计算机科学中最多功能且频繁使用的数据结构之一，特别是在高效排序和检索数据时。树由边连接的节点组成，其中一个节点被指定为根（`root`）。每个节点可能有多个子节点，但根节点外只有一个父节点。这种层次结构适用于各种操作，包括搜索、插入和遍历。

### 二叉搜索树 (BST)

树的一个重要例子是二叉搜索树（BST），每个节点最多有两个孩子，称为左和右。BST 强制执行特定的顺序：对于任何给定节点，左子树中的所有节点都较，右子树中的所有节点更大。这种属性使得 BST 在数据检索和排序方面非常高效。

- 允许快速检索，时间复杂度与树的高度成正比（最优情况下）。
- 在维护 BST 结构的同时插入新节点。
- 删除节点并保持树的排序。
- 支持以特定顺序访问数据的方法。

#### 节点结构
我们从定义 BST 的结构开始。

```c
typedef struct TreeNode {
    int data;
    TreeNode *left, *right;
} TreeNode;
```

### 在 BST 中插入
向 BST 插入涉及为新节点找到正确的位置以维护 BST 属性。

```c
TreeNode* insertIntoBST(TreeNode* root, int data) {
    if (root == NULL) {
        TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));
        newNode->data = data;
        newNode->left = newNode->right = NULL;
        return newNode;
    }
    if (data < root->data) root->left = insertIntoBST(root->left, data);
    if (data > root->data) root->right = insertIntoBST(root->right, data);
    return root;
}
```

### 在 BST 中搜索
在 BST 中搜索一个值高效地利用了有序结构。

```c
TreeNode* searchBST(TreeNode* root, int key) {
    if (root == NULL || root->data == key) return root;
    if (key < root->data) return searchBST(root->left, key);
    return searchBST(root->right, key);
}
```

### 中序遍历
遍历 BST 的最方法之一是中序遍历，按升序访问节点。这种方法对于存储在 BST 中的数据特别有用。

```c
void inOrderTraversal(TreeNode* root) {
    if (root != NULL) {
        inOrderTraversal(root->left);
        printf("%d ", root->data);
        inOrderTraversal(root->right);
    }
}
```

代码输出：

BST 的中序遍历：1 2 3 4 5 6 7 8 9

通过利用树（特别是 BST），程序员可以实现高效的数据排序和检索。本节通过代码示例强调了树的基本操作和技术。当你深入研究数据结构时，精通树无疑将增强你设计稳健高效解决方案的能力。

## 3.3 图：表示技术与算法

图是一种基础数据结构，描绘了一组对象（顶点）和它们之间的连接（边）。其应用范围从计算机网络、社交网络到生物网络和交通系统。理解如何表示和遍历图对于解决复杂的计算问题至关重要。本节探索了图论的核心概念、C 语言表示技术以及许多现代技术的基础图算法。

### 基础概念

- 顶点：称为节点，表示网络中的实体。
- 边：顶点之间的连接。边可以是有向的（单向关系）或无向的（双向关系）。
- 路径：由边连接的顶点序列。
- 环：起点和终点同一个顶点的路径。
- 加权：边带有权重，表示顶点之间的代价或距离。

### 表示技术
可以使用多种技术在 C 中表示图，各自优优点。

#### 邻接矩阵
一个二维数组，`[i][j]` 单元格表示顶点 `i` 和 `j` 之间是否存在边。这种方法简单直接，但对于稀疏图空间效率较低。

```c
#define MAX_VERTICES 100
int adjacencyMatrix[MAX_VERTICES][MAX_VERTICES];
void addEdge(int i, int j) {
    adjacencyMatrix[i][j] = 1;
    adjacencyMatrix[j][i] = 1; // 用于无向图
}
```

#### 邻接表
一个列表数组，其中索引 `i` 的每个列表包含直接连接到顶点 `i` 的顶点。这种方法对于稀疏图空间效率更高。

```c
#include <stdlib.h>
typedef struct Node {
    int vertex;
    Node* next;
} Node;
Node* adjacencyList[MAX_VERTICES];
void addEdge(int i, int j) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->vertex = j;
    newNode->next = adjacencyList[i];
    adjacencyList[i] = newNode;
}
```

### 图算法
若干算法对于有效导航和分析图至关重要。

#### 深度优先搜索 (DFS)
一种遍历算法，在回溯之前沿着每个分支尽可能深地探索。它用于路径查找和环检测。

```c
void DFS(int vertex, int visited[MAX_VERTICES]) {
    visited[vertex] = 1;
    printf("%d ", vertex);
    Node* temp = adjacencyList[vertex];
    while (temp != NULL) {
        if (!visited[temp->vertex]) DFS(temp->vertex, visited);
        temp = temp->next;
    }
}
```

#### 广度优先搜索 (BFS)
一种遍历算法，在移动到下一层节点之前探索当前深度的邻居节点。寻找最短路径的理想选择。

```cpp
#include <stdio.h>
#include <stdlib.h>
void BFS(int startVertex) {
    int visited[MAX_VERTICES] = {0};
    int queue[MAX_VERTICES], front = 0, rear = 0;
    queue[rear++] = startVertex;
    visited[startVertex] = 1;
    while (front < rear) {
        int v = queue[front++];
        printf("%d ", v);
        Node* temp = adjacencyList[v];
        while (temp != NULL) {
            if (!visited[temp->vertex]) {
                visited[temp->vertex] = 1;
                queue[rear++] = temp->vertex;
            }
            temp = temp->next;
        }
    }
}
```

```c
currentVertex = queue[front++]; temp = adjacencyList[currentVertex]; 
{ adjVertex = temp->vertex; if (!visited[adjVertex]) { adjVertex = 1; 
temp = temp->next; } }
```

代码输出:

DFS 遍历：0 1 3 4 2

BFS 遍历：0 1 2 3 4

在 C 语言中实现图及其相关算法需要对指针和动态内存分配有深入的理解。通过精通图的表示技术和遍历算法，开发者可以解决诸从网络分析、优化到复杂的游戏 AI 等各种问题。图（Graphs）释放了建模和解决现实世界问题的潜力，使其程序员工具箱中不可或缺的工具。

## 3.4 栈与队列：使用数组和链表实现功能

栈（Stacks）和队列（Queues）是计算机科学中基础的数据结构，广泛用于按特定管理数据。栈遵循后进先出（LIFO）原则，最后添加的元素最先移除。相反，队列遵循先进先出（FIFO）原则，先添加的元素最先移除。本节将探讨如何在 C 语言编程中使用数组和链表实现栈和队列，并对它们的操作、优势和实际应用提供详细视角。

### 栈

#### 栈操作

- 将元素推（Push）到栈顶。
- 弹出（Pop）一个元素并返回栈顶元素。
- 查看（Peek）栈顶元素而不将其移除。
- 检查栈是否为空。

##### 使用数组实现栈
数组提供实现栈的简单方法，使用一个整数来跟踪栈顶元素的索引。

```c
#define MAX_SIZE 100
typedef struct {
    int items[MAX_SIZE];
    int top;
} Stack;

void initializeStack(Stack* stack) {
    stack->top = -1;
}

void push(Stack* stack, int item) {
    if (stack->top == MAX_SIZE - 1) {
        stack->items[++stack->top] = item;
    }
}

int pop(Stack* stack) {
    if (stack->top == -1) {
        return -1;
    }
    return stack->items[stack->top--];
}

int peek(Stack* stack) {
    if (stack->top == -1) {
        return -1;
    }
    return stack->items[stack->top];
}

int isEmpty(Stack* stack) {
    return stack->top == -1;
}
```

##### 使用链表实现栈
对于动态大小需求，链表提供了更灵活的栈实现，没有固定大小限制。

```c
typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct {
    Node* top;
} StackLinkedList;

void initializeStackLinkedList(StackLinkedList* stack) {
    stack->top = NULL;
}

void pushLinkedList(StackLinkedList* stack, int item) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = item;
    newNode->next = stack->top;
    stack->top = newNode;
}
```

```c
int popLinkedList(StackLinkedList* stack) {
    if (stack->top == NULL) {
        return -1;
    }
    Node* temp = stack->top;
    int item = temp->data;
    stack->top = temp->next;
    free(temp);
    return item;
}

int peekLinkedList(StackLinkedList* stack) {
    if (stack->top == NULL) {
        return -1;
    }
    return stack->top->data;
}
```

### 队列

#### 队列操作

- 将元素入队（Enqueue）到队列尾。
- 出队（Dequeue）一个元素并返回队列头部元素。
- 查看（Peek）队列头部元素而不将其移除。
- 检查队列是否为空。

##### 使用数组实现队列
与栈，数组可以实现队列。然而，为了高效管理队列的头部和尾部，我们使用了循环队列的方法。
