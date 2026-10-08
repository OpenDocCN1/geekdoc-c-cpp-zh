

```c
currentVertex = queue[front++]; temp = adjacencyList[currentVertex]; 
{ adjVertex = temp->vertex; if (!visited[adjVertex]) { adjVertex = 1; 
temp = temp->next; } }
```

# 代码输出:

DFS 遍历：0 1 3 4 2
BFS 遍历：0 1 2 3 4

在 C 语言中实现图及其相关算法需要对指针和动态内存分配有深入的理解。通过精通图的表示技术和遍历算法，开发者可以解决诸从网络分析、优化到复杂的游戏 AI 等各种问题。图（Graphs）释放了建模和解决现实世界问题的潜力，使其程序员工具箱中不可或缺的工具。

## 3.4

## 栈与队列：使用数组和链表实现功能

栈（Stacks）和队列（Queues）是计算机科学中基础的数据结构，广泛用于按特定管理数据。栈遵循后进先出（LIFO）原则，最后添加的元素最先移除。相反，队列遵循先进先出（FIFO）原则，先添加的元素最先移除。本节将探讨如何在 C 语言编程中使用数组和链表实现栈和队列，并对它们的操作、优势和实际应用提供详细视角。

## 栈

### 栈操作：

- 将元素推（Push）到栈顶。
- 弹出（Pop）一个元素并返回栈顶元素。
- 查看（Peek）栈顶元素而不将其移除。
- 检查栈是否为空。

使用数组实现栈：数组提供实现栈的简单方法，使用一个整数来跟踪栈顶元素的索引。

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

使用链表实现栈：对于动态大小需求，链表提供了更灵活的栈实现，没有固定大小限制。

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

## 队列

### 队列操作：

- 将元素入队（Enqueue）到队列尾。
- 出队（Dequeue）一个元素并返回队列头部元素。
- 查看（Peek）队列头部元素而不将其移除。
- 检查队列是否为空。

使用数组实现队列：与栈，数组可以实现队列。然而，为了高效管理队列的头部和尾部，我们使用了循环队列的方法。

```c
#define MAX_SIZE 100
typedef struct {
    int items[MAX_SIZE];
    int front, rear;
} Queue;

void initializeQueue(Queue* queue) {
    queue->front = -1;
    queue->rear = -1;
}

void enqueue(Queue* queue, int item) {
    if ((queue->front == 0 && queue->rear == MAX_SIZE - 1) || 
        (queue->front == (queue->rear + 1) % MAX_SIZE)) {
        // 队列满了
    } else {
        if (queue->front == -1) { // 第一个入队元素
            queue->front = queue->rear = 0;
            queue->items[queue->rear] = item;
        } else if (queue->rear == MAX_SIZE - 1 && queue->front != 0) {
            // 回环
            queue->rear = 0;
            queue->items[queue->rear] = item;
        } else {
            queue->items[++queue->rear] = item;
        }
    }
}

int dequeue(Queue* queue) {
    if (queue->front == -1) {
        return -1;
    }
    int data = queue->items[queue->front];
    if (queue->front == queue->rear) { // 只有一个元素
        queue->front = queue->rear = -1;
    } else if (queue->front == MAX_SIZE - 1) {
        // 回环
        queue->front = 0;
    } else {
        queue->front++;
    }
    return data;
}
```

使用链表实现队列：链表提供了一种优雅且动态实现队列的方式，避免了循环队列的复杂性。

```c
typedef struct QueueNode {
    int data;
    struct QueueNode* next;
} QueueNode;

typedef struct {
    QueueNode *front, *rear;
} QueueLinkedList;

void initializeQueueLinkedList(QueueLinkedList* queue) {
    queue->front = NULL;
    queue->rear = NULL;
}

void enqueueLinkedList(QueueLinkedList* queue, int item) {
    QueueNode* newNode = (QueueNode*)malloc(sizeof(QueueNode));
    newNode->data = item;
    newNode->next = NULL;
    if (queue->rear == NULL) {
        queue->front = queue->rear = newNode;
    } else {
        queue->rear->next = newNode;
        queue->rear = newNode;
    }
}

int dequeueLinkedList(QueueLinkedList* queue) {
    if (queue->front == NULL) {
        return -1;
    }
    QueueNode* temp = queue->front;
    int data = temp->data;
    queue->front = queue->front->next;
    if (queue->front == NULL) {
        queue->rear = NULL;
    }
    free(temp);
    return data;
}
```

通过使用数组和链表来实现栈和队列，我们可以深入探索它们的功能、潜在应用以及编程中的实践。

## 3.5

## 哈希表：设计与处理冲突

哈希表（Hash Tables）是支持高效算法和数据存储的关键数据结构。通过提供快速插入、删除和查找操作，哈希表显著提升了现代应用程序的性能。哈希表的核心在于通过哈希函数将键映射到值。本节将探讨在 C 语言中设计哈希表的细节。

## 设计基础哈希表

哈希表的主要组件包括：

- 将键转换为哈希表索引的哈希函数。
- 存储与键关联的值的数组槽位。
- 管理多个键哈希到同一个桶的情况的冲突处理策略。

### 简单哈希函数：设计哈希表的基础步骤涉及制定高效的哈希函数。为了演示，我们将使用一个基于取模的哈希函数。

```c
#define TABLE_SIZE 100
unsigned int hash(int key) {
    return key % TABLE_SIZE;
}
```

## 使用链链法实现哈希表

链链法是处理哈希表冲突的流行技术。当多个键哈希到同一个值时，会在每个桶创建一个链表。

### 哈希表条目结构：哈希表中的每个条目包含一个键、值以及指向下一个条目的指针以形成链。

```c
typedef struct Entry {
    int key;
    int value;
    struct Entry* next;
} Entry;

typedef Entry* HashTable[TABLE_SIZE];
```

### 插入条目：为了插入键值对，我们使用哈希函数确定合适的桶，并将新条目添加到该桶链表的头部。

```c
void insert(HashTable ht, int key, int value) {
    int index = hash(key);
    Entry* newEntry = (Entry*)malloc(sizeof(Entry));
    newEntry->key = key;
    newEntry->value = value;
    newEntry->next = ht[index];
    ht[index] = newEntry;
}
```

### 查找条目：搜索涉及哈希键以定位合适的桶，然后遍历链表找到条目。

```c
Entry* search(HashTable ht, int key) {
    int index = hash(key);
    Entry* entry = ht[index];
    while (entry != NULL) {
        if (entry->key == key) return entry;
        entry = entry->next;
    }
    return NULL; // 未找到键
}
```

### 删除条目：删除操作需要从哈希索引处的链表中找到该条目，然后将其从列表中移除。

```c
void delete(HashTable ht, int key) {
    int index = hash(key);
    Entry* entry = ht[index];
    Entry* prev = NULL;
    while (entry != NULL) {
        if (entry->key == key) {
            if (prev == NULL) {
                ht[index] = entry->next; // 列表中第一个条目
            } else {
                prev->next = entry->next;
            }
            free(entry);
            return;
        }
        prev = entry;
        entry = entry->next;
    }
}
```

# 代码输出:

向哈希表插入键值对 (1, 'A'), (101, 'B'), (201, 'C')...
搜索键 101：找到值 'B'
从哈希表删除键 101...
搜索键 101：未找到键

