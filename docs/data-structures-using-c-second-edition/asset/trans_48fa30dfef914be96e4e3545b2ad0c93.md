

为新节点分配内存，并将其 DATA 部分初始化为 9，Next 部分初始化为 NULL。

取一个指向 START 的指针变量 PTR。

移动 PTR，使其指向列表的最后一个节点。

在 PTR 指向的节点之后添加新节点。具体做法是将新节点的地址存储在 PTR 的 NEXT 部分中。

### 图 6.14 在链表末尾插入元素

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 10
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET NEW_NODE -> NEXT = NULL
Step 6: SET PTR = START
Step 7: Repeat Step 8 while PTR -> NEXT != NULL
Step 8: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 9: SET PTR -> NEXT = NEW_NODE
Step 10: EXIT
```

### 图 6.15 在末尾插入新节点的算法

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PRETR = PTR
Step 7: Repeat Steps 8 and 9 while PRETR -> DATA != NUM
Step 8: SET PRETR = PTR
Step 9: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 10: SET PRETR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```

### 图 6.16 在值为 NUM 的节点之后插入新节点的算法

在第 5 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。然后我们取另一个指针变量 PRETR，它将用于存储 PTR 前驱节点的地址。最初，PRETR 被初始化为 PTR。因此，PTR、PRETR 和 START 现在都指向链表的第一个节点。

在 while 循环中，我们遍历链表以找到值等于 NUM 的节点。我们需要到达这个节点，因为新节点将插入到该节点之后。一旦到达该节点，在第 10 步和第 11 步中，我们以这样的方式更改 NEXT 指针，使新节点插入到所需节点之后。

START 为新节点分配内存，并将其 DATA 部分初始化为 9。

取两个指针变量 PTR 和 PREPTR，并将它们初始化为 START，使得 START、PTR 和 PREPTR 都指向列表的第一个节点。

移动 PTR 和 PREPTR，直到 PREPTR 的 DATA 部分等于要插入的节点的值。PREPTR 将始终指向 PTR 之前的那个节点。

在 PREPTR 和 PTR 指向的节点之间添加新节点。

### 图 6.17 在链表中给定节点之后插入元素

## 在链表中给定节点之前插入节点

考虑图 6.19 所示的链表。假设我们想在值为 3 的节点之前添加一个值为 9 的新节点。在讨论链表中将进行的更改之前，让我们先看看图 6.18 所示的算法。

### 图 6.18 在值为 NUM 的节点之前插入新节点的算法

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PREPTR = PTR
Step 7: Repeat Steps 8 and 9 while PTR -> DATA != NUM
Step 8: SET PREPTR = PTR
Step 9: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 10: SET PREPTR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```

在第 5 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。然后，我们取另一个指针变量 PREPTR 并将其初始化为 PTR。因此，PTR、PREPTR 和 START 现在都指向链表的第一个节点。

在 while 循环中，我们遍历链表以找到值等于 NUM 的节点。我们需要到达这个节点，因为新节点将插入到该节点之前。一旦到达该节点，在第 10 步和第 11 步中，我们以这样的方式更改 NEXT 指针，使新节点插入到所需节点之前。

![](img/be6359df08208122bec6fad1103de211_185_0.png)

为新节点分配内存，并将其 DATA 部分初始化为 9。

![](img/be6359df08208122bec6fad1103de211_185_1.png)

将 PREPTR 和 PTR 初始化为 START 节点。

![](img/be6359df08208122bec6fad1103de211_185_2.png)

START
PTR
PREPTR
移动 PTR 和 PREPTR，直到 PTR 的 DATA 部分等于要在其之前进行插入的节点的值。PREPTR 将始终指向 PTR 之前的那个节点。

![](img/be6359df08208122bec6fad1103de211_185_3.png)

在 PREPTR 和 PTR 指向的节点之间插入新节点。

![](img/be6359df08208122bec6fad1103de211_185_4.png)

![](img/be6359df08208122bec6fad1103de211_185_5.png)

### 图 6.19 在链表中给定节点之前插入元素

## 6.2.4 从链表中删除节点

在本节中，我们将讨论如何从已存在的链表中删除一个节点。我们将考虑三种情况，然后查看每种情况下删除是如何进行的。

- 情况 1：删除第一个节点。
- 情况 2：删除最后一个节点。
- 情况 3：删除给定节点之后的节点。

在描述这三种情况下的算法之前，让我们先讨论一个称为 UNDERFLOW 的重要术语。下溢是指当我们尝试从空链表中删除节点时发生的一种情况。当 START = NULL 或没有更多节点可删除时会发生这种情况。请注意，当我们从链表中删除一个节点时，实际上必须释放该节点占用的内存。内存将返回到空闲池，以便可用于存储其他程序和数据。无论删除的情况如何，我们始终会更改 AVAIL 指针，使其指向最近被释放的地址。

### 从链表中删除第一个节点

考虑图 6.20 中的链表。当我们想要从列表开头删除一个节点时，链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_186_0.png)

### 图 6.20 删除链表的第一个节点

图 6.21 显示了从链表中删除第一个节点的算法。在第 1 步中，我们检查链表是否存在。如果 START = NULL，则表示列表中没有节点，控制权将转移到算法的最后一条语句。但是，如果链表中有节点，则我们使用一个指针变量 PTR，将其设置为指向列表的第一个节点。为此，我们用存储列表第一个节点地址的 START 初始化 PTR。在第 3 步中，START 被设置为指向序列中的下一个节点，最后释放 PTR 指向的节点（最初是列表的第一个节点）所占用的内存，并将其返回到空闲池。

### 图 6.21 删除第一个节点的算法

```
Step 1: IF START = NULL
         Write UNDERFLOW
         Go to Step 5
       [END OF IF]
Step 2: SET PTR = START
Step 3: SET START = START -> NEXT
Step 4: FREE PTR
Step 5: EXIT
```

### 从链表中删除最后一个节点

考虑图 6.22 所示的链表。假设我们想要从链表中删除最后一个节点，那么链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_186_1.png)

### 图 6.22 删除链表的最后一个节点

图 6.23 显示了从链表中删除最后一个节点的算法。在第 2 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。在 while 循环中，我们取另一个指针变量 PREPTR，使其始终指向 PTR 之前的一个节点。一旦到达最后一个节点和倒数第二个节点，我们将倒数第二个节点的 NEXT 指针设置为 NULL，这样它现在就成为链表的（新）最后一个节点。之前最后一个节点的内存被释放并返回到空闲池。

```
Step 1: IF START = NULL
       Write UNDERFLOW
       Go to Step 8
       [END OF IF]
Step 2: SET PTR = START
Step 3: Repeat Steps 4 and 5 while PTR -> NEXT != NULL
Step 4: SET PREPTR = PTR
Step 5: SET PTR = PTR -> NEXT
       [END OF LOOP]
Step 6: SET PREPTR -> NEXT = NULL
Step 7: FREE PTR
Step 8: EXIT
```

### 图 6.23 删除最后一个节点的算法

### 从链表中删除给定节点之后的节点

考虑图 6.24 所示的链表。假设我们想要删除包含数据值 4 的节点之后的节点，那么链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_187_0.png)

取最初指向 START 的指针变量 PTR 和 PREPTR。

![](img/be6359df08208122bec6fad1103de211_187_1.png)

移动 PREPTR 和 PTR，使 PREPTR 指向包含 VAL 的节点，PTR 指向其后继节点。

![](img/be6359df08208122bec6fad1103de211_187_2.png)

![](img/be6359df08208122bec6fad1103de211_187_3.png)

![](img/be6359df08208122bec6fad1103de211_187_4.png)

将 PREPTR 的 NEXT 部分设置为 PTR 的 Next 部分。

![](img/be6359df08208122bec6fad1103de211_187_5.png)

### 图 6.24 从链表中删除给定节点之后的节点

图 6.25 显示了从链表中删除给定节点之后的节点的算法。在第 2 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。在 while 循环中，我们取另一个指针变量 PREPTR，使其始终指向 PTR 之前的一个节点。一旦到达包含 VAL 的节点及其后继节点，我们将包含 VAL 的节点的 next 指针设置为其后继节点的 next 字段中包含的地址。给定节点之后的节点的内存被释放并返回到空闲池。

