
location of the new node, this step can be implemented by the pair of assignments (in this order) NEW := AVAIL, AVAIL := LINK[AVAIL]

(c) Copying new information into the new node. In other words, INFO[NEW] := ITEM

The schematic diagram of the latter two steps is pictured in Fig. 5.18.

![](img/f1df4c31f1795198a6843c842acc2216_218_0.png)

## 在列表开头插入

Suppose our linked list is not necessarily sorted and there is no reason to insert a new node in any special place in the list. Then the easiest place to insert the node is at the beginning of the list. An algorithm that does so follows.

- **算法 5.4:** INSFFIRST(INFO, LINK, START, AVAIL, ITEM)
- 该算法将 ITEM 插入为列表的第一个节点。
- 1. [OVERFLOW]? 如果 AVAIL = NULL，则：写入：OVERFLOW，并退出。
- 2. [从 AVAIL 列表中移除第一个节点。] 设置 NEW := AVAIL 和 AVAIL := LINK[AVAIL]。
- 3. 设置 INFO[NEW] := ITEM。[将新数据复制到新节点]
- 4. 设置 LINK[NEW] := START。[新节点现在指向原始第一个节点。]
- 5. 设置 START := NEW。[更改 START 使其指向新节点。]
- 6. 退出。

步骤 1 至 3 已经讨论过，步骤 2 和 3 的示意图见图 5.18。步骤 4 和 5 的示意图见图 5.19。

![](img/f1df4c31f1795198a6843c842acc2216_218_1.png)

3. SAVE = 5 且 PTR = LINK[5] = 3。

4. 步骤 5 和 6 重复如下：
(a) BED[3] = Dean < Jones，因此 SAVE = 3 且 PTR = LINK[3] = 11。
(b) BED[11] = Fields < Jones，因此 SAVE = 11 且 PTR = LINK[11] = 8。
(c) BED[8] = Green < Jones，因此 SAVE = 8 且 PTR = LINK[8] = 1。
(d) 由于 BED[1] = Kirk > Jones，我们有：
LOC = SAVE = 8 并返回。

(b) INSLOC(BED, LINK, START, AVAIL, LOC, ITEM) [此处 LOC = 8。]
1. 由于 AVAIL ≠ NULL，控制转移到步骤 2。
2. NEW = 10 且 AVAIL = LINK[10] = 2。
3. BED[10] = Jones。
4. 由于 LOC ≠ NULL，我们有：
LINK[10] = LINK[8] = 1 且 LINK[8] = NEW = 10。
5. 退出。

图 5.22 显示了 Jones 添加到患者列表后的数据结构。我们强调，只更改了三个指针，即 AVAIL、LINK[10] 和 LINK[8]。

![](img/f1df4c31f1795198a6843c842acc2216_222_0.png)

图 5.22

以下是将元素插入有序列表的算法 5.7 的 C 实现：

图 5.23 未考虑到这样一个事实：当从我们的列表中删除节点 N 时，我们会立即将其内存空间返回到 AVAIL 列表。具体来说，为了更易于处理，它将被返回到 AVAIL 列表的开头。因此，此类删除的更精确示意图是图 5.24 中所示的图。请注意，三个指针字段按以下方式更改：

- 1. 节点 A 的下一个指针字段现在指向节点 B，即节点 N 之前指向的位置。
- 2. N 的下一个指针字段现在指向空闲池中的原始第一个节点，即 AVAIL 之前指向的位置。
- 3. AVAIL 现在指向已删除的节点 N。

![](img/f1df4c31f1795198a6843c842acc2216_226_0.png)

还有两种特殊情况。如果被删除的节点 N 是列表中的第一个节点，则 START 将指向节点 B；如果被删除的节点 N 是列表中的最后一个节点，则节点 A 将包含 NULL 指针。

## 示例 5.16

- (a) 考虑图 5.22，即病房中的患者列表。假设 Green 出院，因此 BED[8] 现在为空。那么，为了维护链表，必须执行指针字段中的以下三个更改：

```
LINK[11] = 10   LINK[8] = 2   AVAIL = 8
```

通过第一个更改，原本在 Green 之前的 Fields 现在指向原本在 Green 之后的 Jones。第二个和第三个更改将新的空床位添加到 AVAIL 列表。我们强调，在进行删除之前，我们必须找到原本指向被删除节点 BED[8] 的节点 BED[11]。

- (b) 考虑图 5.13，即经纪人及其客户的列表。假设 Nelson 的第一个客户 Teller 从客户列表中被删除。那么，为了维护链表，必须执行指针字段中的以下三个更改：

```
POINT[4] = 10   LINK[9] = 11   AVAIL = 9
```

通过第一个更改，Nelson 现在指向他原来的第二个客户 Jones。第二个和第三个更改将新的空节点添加到 AVAIL 列表。

3. 如果 INFO[PTR] = ITEM，则：
   设置 LOC := PTR 和 LOCP := SAVE。
   否则：
   设置 LOC := NULL 和 LOCP := SAVE。
   [If 结构结束。]
4. 退出。

与过程 5.9 相比，请注意此过程的简单性。在这里，我们不必考虑 ITEM 出现在第一个节点时的特殊情况，并且我们可以同时执行控制循环的两个测试。

- (c) 当 LIST 是普通链表时，算法 5.10 删除第一个包含 ITEM 的节点 N。以下是当 LIST 是带头节点的循环链表时的此类算法。

```
Algorithm 5.14: DELLOCHL(INFO, LINK, START, AVAIL, ITEM)
1. [Use Procedure 5.15 to find the location of N and its preceding node.]
   Call FINDBHL(INFO, LINK, START, ITEM, LOC, LOCP).
2. If LOC = NULL, then: Write: ITEM not in list, and Exit.
3. Set LINK[LOCP] := LINK[LOC]. [Deletes node.]
4. [Return deleted node to the AVAIL list.]
   Set LINK[LOC]:= AVAIL and AVAIL:= LOC.
5. Exit.
```

同样，我们不必考虑 ITEM 出现在第一个节点时的特殊情况，就像在算法 5.10 中所做的那样。

备注：文献中有时会出现另外两种链表变体：

- 1. 最后一个节点指回第一个节点而不是包含空指针的链表，称为循环列表
- 2. 在列表开头包含一个特殊头节点并在列表末尾包含一个特殊尾节点的链表

图 5.32 包含这些列表的示意图。

![](img/f1df4c31f1795198a6843c842acc2216_234_0.png)

![](img/f1df4c31f1795198a6843c842acc2216_234_1.png)

图 5.32
