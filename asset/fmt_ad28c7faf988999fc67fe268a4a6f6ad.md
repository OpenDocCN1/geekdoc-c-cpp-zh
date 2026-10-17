
```c
#ifndef H_LINKED_LIST_H
#define H_LINKED_LIST_H
typedef struct {
    void *data;
    struct conscell *next;
} conscell;
consccell* list_push(conscell *list, void *data);
consccell* list_pop(conscell *list);
void list_free(conscell *list);
consccell* list_reverse(conscell *list);
consccell* list_sort(conscell *list, int (*compare)(const void *a, const void *b));
consccell* list_filter(conscell *list, int (*filter)(const void *a));
int list_length(conscell *list);
#endif /* H_LINKED_LIST_H */
```

列表 16.2：`linked-list.c` 中的函数 `list_push` 在链表头部添加一个节点。

```c
consccell* list_push(conscell *list, void *data) {
    consccell *new = malloc(sizeof(new));
    new->data = data;
    new->next = list;
    return new;
}
```

### 16.3.1 `list_push()` 的演示：`test1.c`

列表 16.3：文件 `test1.c` 提供了 `list_push()` 的演示。它从空链表开始，推入四个项，然后扫描链表并打印值。让我们通过代码：第 5 行：这里声明的 `list` 变量指向链表的第一个元素。第 6 行：这里引入了一些任意数字作为数据。第 7 行：我们将 `&a` 传递给 `list_push()`，它创建了一个 `conscell` 并将其链接到链表。第 12 行：我们遍历链表并打印存储其中的数据。由于数据是 `void` 指针，不能直接解引用；这就是为什么要将 `p->data` 强制转换为 `(int *)`。

151

列表 16.3：`test1.c` 提供了 `list_push()` 的演示。它从空链表开始，然后推入四个项。

我们将程序编译为名为 `test1` 的执行文件并运行它。

```
./test1
原始链表：
1000 -45
```

注意相对于原始 `a`, `b`, `c`, `d` 的顺序。你能解释一下为什么会这样吗？

备注 16.1。不要把 `test.c` 中的程序视为完成品。良好的程序会在退出前释放所有分配的内存。这个程序没有。你可能需要在调用完第 16.5 节的 `list_free()` 后在这里修复 `test.c`。

## 16.4 函数 `list_pop()`

出现在列表 16.1 第 8 行的 `list_pop()` 函数几乎是 `list_push()` 的反向——它移除链表头节点。它释放之前为节点 `cons cell` 分配的内存，并返回新头的地址。我们设计 `list_pop()` 以便对空列表调用是安全的；因为没有要移除的节点，它什么都不会做。通常，函数的用法如下

`list = list_pop(list);`

弹出节点后，关联的数据变得不可访问。如果你需要数据，请获取它。如果你显式分配了数据的内存，你有责任在弹出节点之前释放这些内存。`list_pop()` 函数不知道 `cons cell` 指向的数据性质。

编写一个 `list_pop()` 的实现——这并不难——并添加到你的 `linked-list.c` 中。

### 16.4.1 `list_pop()` 的演示：`test2.c`

将 `test1.c` 复制到 `test2.c`，并添加代码弹出两个节点然后打印结果。再弹出三个节点并打印结果。我的结果是这样的：

## 16.5. `ll1_free()` 函数

```
$ ./test2
the original linked list:
12 1000 -45 101
the list after popping two nodes:
-45 101
the list after popping three more:
```

最后一步没有打印内容，因为列表为空。注意，根据我们对 `ll1_pop()` 的规范，对包含四个节点的链表执行五次 `ll1_pop()` 是可能的。

## 16.5 `ll1_free()` 函数

出现在列表 16.1 第 9 行的 `ll1_free()` 函数用于释放为链表中所有单元分配的内存。通常在你完成对链表的操作后，会调用 `ll1_free()`。

请记住，`ll1_free()` 并不知道链表节点指向数据的性质。如果你显式地为数据分配了内存，那么在调用 `ll1_free()` 之前，你需要遍历列表和内存。

以下是 `ll1_free()` 的一种实现方式：

```c
void ll1_free(conscell *list) { // 版本 1：迭代
  while (list != NULL) {
    conscell *p = list->next;             // 记住下一个节点
    free(list);                            // 释放头节点
    list = p;                               // 生成一个更短的列表
  }
}
```

注意那里的删除“踏步”。如果我们过早释放了一个节点，就会丢失它的 `next` 指针，从而与列表其余部分隔离开。技巧是保持领先一个节点，并在释放当前节点之前保存它的地址。

该实现是一个迭代算法——它在 `while` 循环中遍历链表并对每个节点执行操作直到到达末尾。或者，`ll1_free()` 也可以用递归算法实现，视角完全不同。我将先用文字描述这种非常 Lisp 式的算法：

- 1. 如果列表为空，则无事可做。
- 2. 否则，分离并释放头节点，并对剩余列表调用 `ll1_free()`。

这是该算法的 C 语言实现。注意，与迭代版本不同，它完全没有显式的循环结构！

```c
void ll1_free(conscell *list) { // 版本 2：递归
  if (list != NULL) {
    conscell *p = list->next;             // 记住下一个节点
    free(list);                            // 释放头节点
    ll1_free(p);                              // 递归：释放剩余列表
  }
}
```

选择 `ll1_free()` 的任一实现，并将其插入到你的 `linked-list.c` 中。这两个实现的效果相同，因此对于我们的目的来说选择并不重要，但为了实验，尝试两种方法会极好主意。

### 16.5.1 ■ `ll1_free()` 的演示：`test3.c`

将 `test1.c` 复制为 `test3.c`。在退出前添加释放链表的代码，并打印它的执行结果，如下所示：

```c
ll1_free(list);
printf("*list memory freed\n");
```

我的输出如下：

```
$ ./test3
the original linked list:
12 1000 -45 101
linked list freed
```

> **备注 16.2。** `ll1_free()` 函数释放了为链表单元分配的内存。它不会释放为相应数据（如果有）分配的内存。在调用 `ll1_free()` 之前，释放与数据相关的所有内存是程序员的责任。为了让本章示例尽可能简单，我将示例数据限制为不需要内存分配和释放的数值。在我们之后将遇到的更实际的情况下，数据总是被分配且必须释放的。

> **备注 16.3。** 在 `ll1_free(list)` 返回后，`list` 的值毫无意义；它指向的内存不再属于你，当然，你不应该引用它。通常这不是一个问题——你到底为什么要引用一个不存在的列表？——但有些程序员因为将指针设置为 `NULL` 而感到不适。如果你想这样做，那么在 `ll1_free(list)` 返回后你需要显式地设置 `list = NULL`。或者，你可以重新设计 `ll1_free()`，让它不是接收 `list` 而是接收列表地址，如 `ll1_free(&list)` 所示。这会告诉你 `list` 存储在哪里，从而在返回之前让调用者能够将其设置为 `NULL`。Hanson [26]，例如，这种方法

## 16.6 `ll1_reverse()` 函数

你已经观察到，当我们一次构建一个链表时，`list` 是反向插入的。在很多情况下这不是问题，但在少数情况下，我们应该反转给定列表节点的顺序。出现在第 149 页列表 16.1 第 10 行的 `ll1_reverse()` 正是为此。它接收一个列表并返回反转后的列表地址：

```c
list = ll1_reverse(list);
```

反转算法可能并不显而易见——我知道我第一次想到它时并不如此——但一旦你看到它，就会变得简单。因此，我建议你花几分钟思考如何反转一个链表。想清楚后（或者放弃），继续阅读。

## 16.7 `ll1_sort()` 函数

思路是：考虑两个列表，`list1` 是原始列表，`list2` 初始为空。从 `list1` 移除第一个节点并将其添加到 `list2`。直到 `list1` 耗尽。`list2` 就是所需的反转列表。将 `list2` 返回给调用者。

编写 `ll1_reverse()` 的实现，并将其添加到你的 `linked-list.c` 中。

### 16.6.1 - `ll1_reverse()` 的演示：`test4.c`

为了测试你的工作，将 `test3.c` 复制为 `test4.c`。反转原始列表并打印。输出如下：

```
$ ./test4
the original list:
12 1000 -45 101
the reversed list:
101 -45 1000
```

## 16.7 - `ll1_sort()` 函数

出现在第 149 页列表 16.1 第 11 行的 `ll1_sort()` 用于根据某些标准对列表重新排序。`ll1_sort()` 接受三个参数：

- 1. 第一个参数 `list` 指向要排序的列表。
- 2. 第二个参数 `cmp` 是用户提供的比较函数。
- 3. 第三个参数 `params`，比较函数可能不需要。

典型的调用如下：

```c
ll1_sort(list, cmp, NULL);
```

在下一节中，我将详细阐述算法的细节。

### 16.7.1 - 比较函数

我将通过以下示例解释比较函数的本质：

示例 1：假设每个节点的数据是一个整数。我们希望按升序（或降序）对列表排序。对于示例1，合理的比较函数是：

```c
int cmp1(int a, int b) {
    if (a < b)
        return -1;
    else if (a > b)
        return 1;
    else
        return 0;
}
```

示例 2：假设每个节点的数据是一个坐标对。我们希望根据到给定点 $p = (x,y)$ 的距离对列表排序。对于示例2，引入一个结构来存储坐标对是有意义的

```c
struct point { double x; double y; };
```

并将此类结构的地址传递给比较函数，如下：

```c
int cmp2(struct point *a, struct point *b, struct point *p) {
    double dx, dy, d1, d2;
    dx = a->x - p->x;
    dy = a->y - p->y;
    d1 = dx*dx + dy*dy;
    dx = b->x - p->x;
    dy = b->y - p->y;
    d2 = dx*dx + dy*dy;
    if (d1 < d2)
        return -1;
    else if (d1 > d2)
        return 1;
    else
        return 0;
}
```

该函数计算点 $a$ 和 $b$ 到 $p$ 的距离（实际上是距离的平方），并根据距离之间的关系返回 -1、0 或 +1。

遗憾的是，这两个比较函数都不适用于我们的目的，因为它们的参数与其数据类型紧密耦合。我们希望排序函数 `list_sort()` 是通用的，即适用于任何链表，无论关联的数据类型如何。基于此，我们假定一种如下形式的通用比较函数：

```c
int cmp(const void *a, const void *b, void *params);
```

## 16.7. `l1_sort()` 函数

由于 `void` 指针与所有数据类型的指针兼容，这种形式的比较函数是理想的；任何类型数据的指针都可以传递给它。该函数的前两个参数指向要比较的项。第三个参数是一个可能用于比较、也可能不用于比较的参数。将之前的比较函数 `cmp1()` 修改为我们的新形式，我们得到：

```c
int cmp1(const void *aa, const void *bb, void *pp) // 正确形式
{
    int a = *(int *)aa;
    int b = *(int *)bb;
    if (a < b)
        return -1;
    else if (a > b)
        return 1;
    else
        return 0;
}
```

该函数将 `void` 指针 `aa` 转换为指向 `int` 的指针，然后解引用以获取其值 `a`。它对 `bb` 执行了相同的操作。然后，它的处理方式与之前的 `cmp1()` 完全相同。参数 `pp` 未被使用。同样，修改后的 `cmp2()` 形式如下：

```c
int cmp2(const void *aa, const void *bb, void *pp) // 正确形式
{
    struct point *a = (struct point *)aa;
    struct point *b = (struct point *)bb;
    struct point *p = (struct point *)pp;
    double dx, dy, d1, d2;
    dx = a->x - p->x;
    dy = a->y - p->y;
    d1 = dx+dx + dy+dy; // a 到 p 的距离平方
    dx = b->x - p->x;
    dy = b->y - p->y;
    d2 = dx+dx + dy+dy; // b 到 p 的距离平方
    if (d1 < d2)
        return -1;
    else if (d1 > d2)
        return 1;
    else
        return 0;
}
```

现在 `cmp1()` 和 `cmp2()` 具有相同的签名/原型，这才是关键。它们的内部实现非常高效。

## 16.7.2 ■ 快速排序

排序是一个巨大的课题，有很多关于它的书籍。例如，参见高纳斯的《计算机程序设计艺术》[34]。我将描述所谓的快速排序算法，该算法在递归形式下特别适合排序链表。以下是该算法的文字描述：

| | | | |

|---|---|---|---|

| 1. | | 原始列表（未排序） | |

| 2. | list₁ | 头部 | list₂ |

| 3. | 排序后的 list₁ | 头部 | 排序后的 list₂ |

| 4. | | 重组后的（排序列表） | |

**图 16.1：** 此图显示了快速排序算法的步骤。第 1 行表示原始（未排序）列表。在第 2 行中，我们分离了列表头部，并将其余部分分为 `list₁`、`list_` 和 `list₂`，其中 `list_` 中的所有项（根据比较标准）都“小于”头部，而 `list₁` 和 `list₂` 由剩余部分组成。在第 3 行中，我们对 `list_` 和 `list₂` 进行排序，在第 4 行中，我们将这三部分拼接成一个完全排序的列表。

- 1. 如果列表为空，则无事可做。结果是空列表。
- 2. 否则，断开列表第一个节点（头部）并设置它。将其余部分分为两个列表：`list_` 和 `list₂`，其中 `list_` 由所有“小于”第一个节点（根据比较函数）的节点组成，而 `list₂` 包含其他节点。
- 3. 排序 `list_` 和 `list₂`。
- 4. 将列表重组为 `list₁$\rightarrow$list₂`。这就是所需的排序列表。

该过程是高度递归的，因为对子列表 `list_` 和 `list₂` 的排序在步骤 3 中再次调用了该过程。图 16.1 以生动的方式展示了这一过程。列表 16.4 给出了该算法在 C 语言中的非常字面的实现。仔细研究列表 16.4，确保你理解它的每一个细节；然后将其添加到你的链表中。

> **备注 16.4。** 虽然 `ll_sort()` 函数在轮廓上是直白递归的，但列表 16.4 嵌入的 `while` 循环是迭代的。也可以将其替换为递归。该 `while` 循环的目的是根据给定标准将列表分为 `list_` 和 `list₂`。下一节的主题 `ll_filter()` 正是做这一点，并且是严格递归的。原则上，可以将 `ll_sort()` 中的 `while` 循环替换为对 `ll_filter()` 的调用，并获得一个纯递归的 `ll_sort()`。遗憾的是，从 `ll_sort()` 向 `ll_filter()` 传递参数的编码细节变得冗长并模糊了底层思想的概念简单性。你可能想尝试一下。

## 16.7.3 `ll_sort()` 的演示：`test5.c`
