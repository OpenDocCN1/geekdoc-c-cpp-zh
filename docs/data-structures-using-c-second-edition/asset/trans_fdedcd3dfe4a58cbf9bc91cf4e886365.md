
图 6.42 展示了在双向链表末尾插入新节点的算法。在第 6 步，我们取一个指针变量 PTR 并将其初始化为 START。在 while 循环中，我们遍历链表以到达最后一个节点。一旦到达最后一个节点，在第 9 步中，我们更改最后一个节点的 NEXT 指针以存储新节点的地址。请记住，新节点的 NEXT 字段包含 NULL，这表示链表的结束。NEW_NODE 的 PREV 字段将被设置，使其指向 PTR 所指向的节点（现在是列表的倒数第二个节点）。

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 11
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET NEW_NODE -> NEXT = NULL
Step 6: SET PTR = START
Step 7: Repeat Step 8 while PTR -> NEXT != NULL
Step 8: PTR = PTR -> NEXT
        [END OF LOOP]
Step 9: SET PTR -> NEXT = NEW_NODE
Step 10: SET NEW_NODE -> PREV = PTR
Step 11: EXIT
```

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: Repeat Step 7 while PTR -> DATA != NULL
Step 7: PTR = PTR -> NEXT
        [END OF LOOP]
Step 8: SET NEW_NODE -> NEXT = PTR -> NEXT
Step 9: SET NEW_NODE -> PREV = PTR
Step 10: SET PTR -> NEXT = NEW_NODE
Step 11: SET PTR -> NEXT -> PREV = NEW_NODE
Step 12: EXIT
```

### 图 6.42 在末尾插入新节点的算法

### 图 6.43 在给定节点后插入新节点的算法

## 在双向链表中在给定节点后插入节点

考虑图 6.44 所示的双向链表。假设我们想在包含值 3 的节点后添加一个值为 9 的新节点。在讨论链表中将进行的更改之前，让我们先看看图 6.43 所示的算法。

![](img/be6359df08208122bec6fad1103de211_203_0.png)

### 图 6.44 在双向链表中在给定节点后插入新节点

```
Step 1: IF AVAIL = NULL
        Write OVERFLOW
        Go to Step 13
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: Repeat Step 7 while PTR -> DATA != NUM
Step 7: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 9: SET NEW_NODE -> NEXT = PTR
Step 10: SET NEW_NODE -> PREV = PTR -> PREV
Step 11: SET PTR -> PREV = NEW_NODE
Step 12: SET PTR -> PREV -> NEXT = NEW_NODE
Step 13: EXIT
```

图 6.43 展示了在双向链表中在给定节点后插入新节点的算法。在第 5 步，我们取一个指针 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。在 while 循环中，我们遍历链表以到达值等于 NUM 的节点。我们需要到达这个节点，因为新节点将插入到该节点之后。一旦到达这个节点，我们更改 next 和 prev 字段，使新节点插入到所需节点之后。

### 图 6.45 在给定节点前插入新节点的算法

## 在双向链表中在给定节点前插入节点

考虑图 6.46 所示的双向链表。假设我们想在包含值 3 的节点前添加一个值为 9 的新节点。在讨论链表中将进行的更改之前，让我们先看看图 6.45 所示的算法。

在第 1 步中，我们首先检查新节点是否有可用内存。在第 5 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。在 while 循环中，我们遍历链表以到达值等于 NUM 的节点。我们需要到达这个节点，因为新节点将插入到该节点之前。一旦到达这个节点，我们更改 NEXT 和 PREV 字段，使新节点插入到所需节点之前。

![](img/be6359df08208122bec6fad1103de211_204_0.png)

### 图 6.46 在双向链表中在给定节点前插入新节点

## 6.4.2 从双向链表中删除节点

在本节中，我们将看到如何从已存在的双向链表中删除一个节点。我们将考虑四种情况，然后查看每种情况下如何执行删除。

- 情况 1：删除第一个节点。
- 情况 2：删除最后一个节点。
- 情况 3：删除给定节点之后的节点。
- 情况 4：删除给定节点之前的节点。

## 从双向链表中删除第一个节点

考虑图 6.47 所示的双向链表。当我们想要从列表开头删除一个节点时，链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_205_0.png)

释放列表第一个节点占用的内存，并将列表的第二个节点设为 START 节点。

![](img/be6359df08208122bec6fad1103de211_205_1.png)

### 图 6.47 从双向链表中删除第一个节点

图 6.48 展示了从双向链表中删除第一个节点的算法。

```
Step 1: IF START = NULL
        Write UNDERFLOW
        Go to Step 6
        [END OF IF]
Step 2: SET PTR = START
Step 3: SET START = START -> NEXT
Step 4: SET START -> PREV = NULL
Step 5: FREE PTR
Step 6: EXIT
```

在算法的第 1 步中，我们检查链表是否存在。如果 START = NULL，则表示列表中没有节点，控制权将转移到算法的最后一条语句。但是，如果链表中有节点，则我们使用临时指针变量 PTR，将其设置为指向列表的第一个节点。为此，我们用存储列表第一个节点地址的 START 初始化 PTR。在第 3 步中，START 被设置为指向序列中的下一个节点，最后释放 PTR（最初是列表的第一个节点）所占用的内存并将其返回到空闲池。

## 从双向链表中删除最后一个节点

考虑图 6.49 所示的双向链表。假设我们想从链表中删除最后一个节点，则链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_205_2.png)

取一个指向列表第一个节点的指针变量 PTR。

![](img/be6359df08208122bec6fad1103de211_205_3.png)

移动 PTR，使其现在指向列表的最后一个节点。

![](img/be6359df08208122bec6fad1103de211_205_4.png)

释放 PTR 所指向节点占用的空间，并在其前驱节点的 NEXT 字段中存储 NULL。

![](img/be6359df08208122bec6fad1103de211_205_5.png)

### 图 6.49 从双向链表中删除最后一个节点

```
Step 1: IF START = NULL
        Write UNDERFLOW
        Go to Step 7
        [END OF IF]
Step 2: SET PTR = START
Step 3: Repeat Step 4 while PTR -> NEXT != NULL
Step 4: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 5: SET PTR -> PREV -> NEXT = NULL
Step 6: FREE PTR
Step 7: EXIT
```

### 图 6.50 删除最后一个节点的算法

图 6.50 展示了删除双向链表最后一个节点的算法。在第 2 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。while 循环遍历列表以到达最后一个节点。一旦到达最后一个节点，我们还可以通过从最后一个节点的 prev 字段获取其地址来访问倒数第二个节点。要删除最后一个节点，我们只需将倒数第二个节点的 next 字段设置为 NULL，这样它就变成了链表的（新）最后一个节点。之前最后一个节点的内存被释放并返回到空闲池。

## 在双向链表中删除给定节点之后的节点

考虑图 6.51 所示的双向链表。假设我们想删除包含数据值 4 的节点之后的节点，则链表中将进行以下更改。

![](img/be6359df08208122bec6fad1103de211_206_0.png)

### 图 6.51 在双向链表中删除给定节点之后的节点

```
Step 1: IF START = NULL
        Write UNDERFLOW
        Go to Step 9
        [END OF IF]
Step 2: SET PTR = START
Step 3: Repeat Step 4 while PTR -> DATA != NUM
Step 4: SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 5: SET TEMP = PTR
Step 6: SET PTR = PTR -> NEXT
Step 7: SET PTR -> NEXT = TEMP -> NEXT
Step 8: TEMP -> NEXT -> PREV = PTR
Step 9: FREE TEMP
Step 10: EXIT
```

### 图 6.52 删除给定节点之后节点的算法

图 6.52 展示了删除双向链表中给定节点之后节点的算法。在第 2 步中，我们取一个指针变量 PTR 并将其初始化为 START。也就是说，PTR 现在指向双向链表的第一个节点。while 循环遍历链表以到达给定节点。一旦到达包含 val 的节点，其后继节点可以通过使用其 NEXT 字段中存储的地址轻松访问。给定节点的 NEXT 字段被设置为包含后继节点的 NEXT 字段中的内容。最后，给定节点之后的节点的内存被释放并返回到空闲池。
