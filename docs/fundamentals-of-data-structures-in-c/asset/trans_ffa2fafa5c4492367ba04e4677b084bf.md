

## 3.7 基于链表的队列实现

表示队列的另一种方法是使用单链表。这种表示方式比使用数组表示队列具有更多优势。其优势如下

- 在声明队列时无需指定要存储的元素数量（因为在向队列添加元素时，内存是在运行时动态分配的）。
- 插入和删除操作可以轻松高效地处理。
- 基于链表的队列表示可以根据列表中的插入和删除操作动态增长和缩减大小，而不会浪费内存空间。
- 可以为每个队列使用一条链来高效表示多个队列。

可以对队列执行的基本操作如下，

- 入队操作
- 出队操作
- 窥视操作
- 查看队列大小
- 查看队列内容。

### 3.7.1 入队操作

ENQUEUE 是一种用于向队列中添加新元素的操作。队列的 ENQUEUE 操作也可以使用单链表实现。以下过程有助于更好地理解。

- 创建一个带有三个参数的函数 ENQUEUE()，即队列的 FRONT 指针、REAR 指针以及要插入的 ELEMENT。
- 创建一个新指针（即 NEWPTR）来保存新元素。
- 使用 GETNODE() 动态为新指针分配队列节点的大小。
- 将 ELEMENT 赋值给新指针的数据字段。
- 将 REAR 指针的链接赋值给 NEWPTR。
- 将队列的 REAR 指针赋值给 NEWPTR。

图 3.12a 显示了 ENQUEUE 操作前的队列和新节点。在图 3.12b 中，REAR 指针的链接被指向新节点，并将尾指针赋值给新节点。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_188_0.png)

### 声明结构体 Queue 的算法

```
Struct QUEUE
DATA : Data Field
NEXT : Link Field (Address of Struct QUEUE)
End Struct
```

### 为新节点分配内存的算法

```
GETNODE()
SIZE : INTEGER
NEWNODE : QUEUE
Step 1 : Set SIZE = get the size of the QUEUE
Step 2 : Set NEWNODE = Allocate the space from memory for the size of SIZE and
return the initial address
Step 3 : Return NEWNODE
End GETNODE()
```

### 在队列中插入节点的算法

```
ENQUEUE(FRONT : QUEUE, REAR : QUEUE, VALUE : DATA)
NEWPTR : QUEUE
Step 1 : Set NEWPTR = GETNODE()
Step 2 : If (NEWPTR == NULL)
Print "Memory is Not Available"
Return -1
[End of If Structure]
Step 3 : Set NEWPTR -> DATA = value
Step 4 : Set NEWPTR -> NEXT = NULL
Step 5 : If (FRONT == NULL AND REAR == NULL)
FRONT = NEWPTR
Else
REAR -> NEXT = NEWPTR
[End of If Structure]
Step 6 : Set REAR = NEWPTR
Step 7 : Return 0
End ENQUEUE()
```

### 3.7.2 出队操作

DEQUEUE 是一种用于从队列 FRONT 移除元素的操作。队列的 DEQUEUE 操作也可以使用单链表实现。以下过程可以帮助你更好地理解。

- 创建一个带有三个参数的函数 DEQUEUE()，即 FRONT 指针、队列的 REAR 以及存储要删除的最后一个元素的地址。
- 创建一个临时指针（即 tempptr）来保存被移除的元素。
- 将 FRONT 指针赋值给临时指针。
- 将 FRONT 指针指向第一个节点之后的节点，其他节点保持不变。
- 使用 RELEASENODE() 释放临时指针分配的内存。

| 释放待删除节点内存的算法 |
| :--- |
| RELEASENODE(NEWNODE : QUEUE) |
| Step 1 : 释放 NEWNODE 的 QUEUE 空间 |
| Step 2 : 返回 |
| End RELEASENODE() |

| 从队列中移除节点的算法 |
| :--- |
| DEQUEUE(FRONT : QUEUE, REAR : QUEUE, VALUE : DATA) |
| TEMP : QUEUE |
| Step 1 : If (FRONT == NULL AND REAR == NULL) |
| Print "QUEUE is Underflow" |
| Return -1 |
| [End of if Structure] |
| Step 2 : Set TEMP = FRONT |
| Step 3 : Set VALUE = FRONT -> DATA |
| Step 4 : If (FRONT == REAR) |
| Set REAR = NULL |
| [End of if Structure] |
| Step 5 : Set FRONT = FRONT -> NEXT |
| Step 6 : RELEASENODE(TEMP) |
| Step 7 : Return 0 |
| End DEQUEUE() |

图 3.13a 显示了 DEQUEUE 操作前的队列。在图 3.13b 中，创建了一个临时指针（即 tempptr），并使其指向要移除的节点（即 FRONT 指针指向的节点）。FRONT 指针被指向第一个节点之后的节点，其他节点保持不变。临时指针分配的内存被释放。因此，FRONT 指针指向的元素从队列中移除。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_190_0.png)

请注意，队列和链表的表示方式相同。队列与普通链表的区别在于，插入和删除可以在链表的任何位置进行，但在队列中，插入只能在尾端进行，删除只能在头端进行。

### 3.7.3 PEEK 操作

PEEK 操作用于显示队列 FRONT 处由 FRONT 指针指向的元素，而不实际移除它。队列的 PEEK 操作也使用链表实现。在实现 PEEK 操作时，需要检查队列的下溢条件。用户不应尝试从空队列中 PEEK 元素。这种尝试是非法的，应予以避免。

```
Algorithm to Retrieve the Contents from the Top of the Queue

PEEK(FRONT : QUEUE, VALUE : DATA)
Step 1 : If (IS_EMPTY(FRONT))
    Print "Queue is Empty."
    Return
[End of If Structure]
Step 2 : VALUE = FRONT -> DATA
End PEEK()
```

### 3.7.4 遍历队列

要读取或显示队列中的信息，必须从 FRONT 节点开始逐个节点地遍历（移动）链表，直到到达 REAR 节点。遍历列表涉及以下步骤。

- 将 FRONT 指针的地址赋值给一个变量。
- 显示数据字段中的信息。
- 通过推进指针直到 REAR，从一个节点遍历到另一个节点。

### 3.7.5 空队列

如果队列不包含任何元素，则称为**空队列**。如果要从队列中出队一个元素，必须检查队列是否为空，因为不能从空队列中出队元素。如果在链表中队列的 FRONT 和 REAR 都指向 NULL，则称为空队列。如果要从空队列中出队一个元素，将显示输出 "queue is underflow"。

```
Algorithm for IS_EMPTY()

IS_EMPTY(FRONT : QUEUE)
Step 1 : If (FRONT == NULL)
    Return 1
    Else
    Return 0
    [End of If Structure]
End IS_EMPTY()
```

### 3.7.6 已满队列

如果队列包含的元素数量等于其大小，则称队列已满。如果要将元素入队到队列中，必须检查队列是否已满，因为当队列已满时无法将元素入队。对于使用链表表示的队列，队列中存储元素没有限制，因为存储队列元素所需的内存是使用 `malloc()` 函数动态分配的。但是，如果存储队列元素所需的内存不可用，则无法将元素入队到队列中。如果在链表中 malloc() 函数返回 NULL，则称为已满队列。如果需要从已满队列中入队一个元素，将显示输出 "queue is overflow"。

```
Algorithm for IS_FULL()

IS_FULL()
TEMP : QUEUE
Step 1 : TEMP = GETNODE()
Step 2 : If (TEMP == NULL)
    Return 1
    Else
    RELEASENODE(TEMP)
    Return 0
    [End of If Structure]
End IS_FULL()
```

### 3.7.7 队列大小

对于使用链表表示的队列，存储元素没有限制，因为存储队列元素所需的内存是使用 malloc() 函数动态分配的。要查找队列的大小（即已存储的元素数量）以检查存储队列元素所需的内存是否可用，请使用如程序 3.2 中所述的 size() 函数。请注意，当链表指向的内存指向 NULL 时，无法将元素存储在队列中。

```
Algorithm: to Count the Nodes in a Queue

SIZE(FRONT : QUEUE)
COUNT : INTEGER
Step 1 : COUNT = 0
Step 2 : If (FRONT == NULL)
    Return COUNT
    [End of If Structure]
Step 3 : Do While(FRONT != NULL)
    COUNT = COUNT + 1
    FRONT = FRONT -> NEXT
    [End of Step 3 While Structure]
Step 4 : Return COUNT
End SIZE()
```

