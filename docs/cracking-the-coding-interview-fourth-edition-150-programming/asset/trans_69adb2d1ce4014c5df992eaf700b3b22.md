

# 第2章解答 | 链表

## 2.2 实现一个算法找到单链表的倒数第 n 个元素。

### 解决方案

注意：这个问题看起来非常适合用递归，但我们将采用一种不同的方法，因为它更复杂。在遇到此类问题时，要准备好关于递归与迭代优的后续问题。

假设：链表中最少节点数量为 n。

算法：

- 1. 创建两个指针 p1 和 p2，它们指向节点的起始位置。
- 2. 将 p2 向移动 n-1 个位置，使其指向从开头开始的第 n 个节点（使 p1 和 p2 之间的距离保持为 n）。
- 3. 检查 p2->next 是否为空，如果是则返回 p1 的值，否则 p1 和 p2 同时递增。如果 p2 的下一个节点为空，则意味着 p1 指向从倒数第 n 个节点，因为两者之间的距离是 n。
- 4. 重复步骤 3。

```
LinkedListNode nthToLast(LinkedListNode head, int n) {
  if (head == null || n < 1) {
    return null;
  }
  LinkedListNode p1 = head;
  LinkedListNode p2 = head;
  for (int j = 0; j < n - 1; ++j) { // 跳过 n-1 
    if (p2 == null) {
      return null; // 因为链表大小小于 n，未找到
    }
    p2 = p2.next;
  }
  if (p2 == null) {
    return null;
  }
  while (p2.next != null) {
    p1 = p1.next;
    p2 = p2.next;
  }
  return p1;
}
```

# 第2章解答 | 链表

## 2.3 在仅能访问目标节点的情况下，实现一个算法删除单链表中间的节点。

### 示例

输入：链表 a->b->c->d->e 中的节点 `c`

结果：无返回值，但新的链表看起来像 a->b->d->e

### 解决方案

该问题的解决方案是简单将下一个节点的数据复制到当前节点中，然后删除下一个节点。

> 注意：如果要删除的节点是链表的最后一个节点，则无法解决此问题。没关系——你的面试官希望你指出这一点。在这种情况下，你可以考虑将其标记为虚拟节点（dummy）。这是你应该与面试官讨论的问题。

```
public static boolean deleteNode(ListNode n) {
    if (n == null || n.next == null) {
        return false; // 失败
    }
    ListNode next = n.next;
    n.data = next.data;
    n.next = next.next;
    return true;
}
```

# 第2章解答 | 链表

## 2.4 你有两个由链表表示的数字，每个节点包含一个数字。数字以反向顺序存储，使得个位数字位于链表头部。编写一个函数将这两个数字相加，并将和以链表的形式返回。

### 示例

输入：(3 -> 1 -> 5), (5 -> 9 -> 2)

输出：8 -> 0 -> 8

### 解决方案

我们可以通过逐个节点相加来实现递归，就像我们处理数位数字一样。

- 1. result.data = (node1 + node2 + any carry) % 10
- 2. 如果 node1 + node2 > 10，则向下一次加法进位 1。
- 3. 相加两个节点的尾，并传递进位。

```
LinkedList addLists(ListNode l11, ListNode l12,
    int carry) {
    ListNode result = new ListNode(carry, null, null);
    int value = carry;
    if (l11 != null) {
        value += l11.data;
    }
    if (l12 != null) {
        value += l12.data;
    }
    result.data = value % 10;
    if (l11 == null || l12 == null || value >= 10) {
        ListNode more = addLists(l11 == null ? null : l11.next,
            l12 == null ? null : l12.next,
            value >= 10 ? 1 : 0);
        result.setNext(more);
    }
    return result;
}
```

# 第2章解答 | 链表

## 2.5 给定一个环链表，实现一个算法返回环的起始节点。

### 定义

环链表：其中某个节点的 next 指针指向之前的某个节点，形成一个环。

### 示例

输入：A -> B -> C -> D -> E

输出：C

### 解决方案

如果我们移动指针，一个速度为 1，另一个速度为 2，如果链表有环，它们会在哪里相遇？想象两个人在赛道上跑步——快的车总是会超过慢的车！棘点在于找到环的起点。如果它们从同一处出发，速度倍增，何时相遇？它们会在起点前 k 个节点相遇（快者跑了 k + (n-k) 步，而慢者跑了 n-k 步）。

回到问题，快者 (n2) 和慢者 (n1) 在环链表周围移动，n2 会在起点前 k 个节点。由于 n2 在起点前 k 个节点，n1 和 n2 会在起点前 k 个节点相遇。

我们现在知道了：

- 1. 起点在前 k 个节点（根据定义）。
- 2. n1 和 n2 的相遇点在起点前 k 个节点（所示）。

因此，如果我们移动 n1 回到起点并让 n2 留在相遇点，以相同的速度移动，它们会在起点相遇。

```
LinkedList FindBeginning(LinkedListNode head) {
    ListNode n1 = head;
    ListNode n2 = head;

    // 寻找相遇点
    while (n2.next != null) {
        n1 = n1.next;
        n2 = n2.next.next;
        if (n1 == n2) {
            break;
        }
    }

    // 错误检查 - 没有相遇点，因此没有环
    if (n2.next == null) {
        return null;
    }

    /* 将 n1 移动起点。保持 n2 在相遇点。
       如果它们以相同的速度移动，会在起点相遇。 */
    while (n1 != n2) {
        n1 = n1.next;
        n2 = n2.next;
    }

    // 现在 n2 指向环的起点
    return n2;
}
```

# 第3章解答 | 栈与队列

## 3.1 描述如何使用单个数组实现三个栈。

### 解决方案

方法 1：

将数组分为三部分，允许每个栈在有限空间内增长（注意：[" 表示包含，") 表示排除）。

- 对于栈 1，使用 [0, n/3)
- 对于栈 2，使用 [n/3, 2n/3)
- 对于栈 3，使用 [2n/3, n)

该解决方案基于假设没有没有各个栈空间使用的额外信息，且无法使用任何额外空间。在这些限制下，我们只能平分。

```
int stackSize = 300;
int[] buffer = new int[stackSize * 3];
int[] stackPointer = {0, 0, 0}; // 栈指针指向元素
void push(int stackNum, int value) {
    /* 找到数组中顶部元素的索引 + 1，
       增加栈指针 */
    int index = stackSize * stackNum + stackPointer[stackNum] + 1;
    stackPointer[stackNum]++;
    buffer[index] = value;
}
int pop(int stackNum) {
    int index = stackSize * stackNum + stackPointer[stackNum];
    stackPointer[stackNum]--;
    int value = buffer[index];
    buffer[index] = 0;
    return value;
}
int peek(int stackNum) {
    int index = stackSize * stackNum + stackPointer[stackNum];
    return buffer[index];
}
boolean isEmpty(int stackNum) {
    return stackPointer[stackNum] == stackNum * stackSize;
}
```

方法 2：

在这种方法中，只要数组中有剩余空间，任何栈都可以增长。

我们顺序为栈分配空间，并将新块链接到上一个块。这意味着栈中的任何新元素都保留指向该栈上一个元素的指针。

在此实现中，我们面临未使用空间的问题。例如，如果一个栈删除了部分元素，删除的元素不一定出现在数组的末尾。在这种情况下，我们将无法使用这些新释放的空间。

为了克服这一缺陷，我们可以维护一个空闲列表，整个数组空间初始赋予空闲列表。对于每次插入，我们从空闲列表中删除一个条目。在删除情况下，我们只需将空闲单元的索引添加到空闲列表中。

在此实现中，我们可以在变量空间利用方面具有灵活性，但我们需要增加空间复杂度。

```
int stackSize = 300;
int indexUsed = 0;
int[] stackPointer = {-1, -1, -1};
StackNode[] buffer = new StackNode[stackSize * 3];
void push(int stackNum, int value) {
    int lastIndex = stackPointer[stackNum];
    stackPointer[stackNum] = indexUsed;
    indexUsed++;
    buffer[stackPointer[stackNum]] = new StackNode(lastIndex, value);
}
int pop(int stackNum) {
    int value = buffer[stackPointer[stackNum]].value;
    int lastIndex = stackPointer[stackNum];
    stackPointer[stackNum] = buffer[stackPointer[stackNum]].previous;
    buffer[lastIndex] = null;
    indexUsed--;
    return value;
}
int peek(int stackNum) { return buffer[stackPointer[stackNum]].value; }
boolean isEmpty(int stackNum) { return stackPointer[stackNum] == -1; }
class StackNode {
    public int previous;
    public int value;
    public StackNode(int p, int v) {
    value = v;
    previous = p;
    }
}
```

