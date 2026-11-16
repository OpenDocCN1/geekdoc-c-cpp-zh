

## 示例 2

假设一个线性链表是有序的，即较小的项位于较大项之前（也就是说，列表已排序）。我们想将一个项 x 插入到这个列表的适当位置。使用了两个函数：

- `InsertFront()` 将用于在列表前面插入一个节点。
- `InsertAfter()` 将用于在列表中间插入一个节点。

![](img/7f36c52b5170b89b142dbb7b1ea4666b_470_0.png)

同样，将算法的细节作为练习留给读者。在逐行分析算法时，请务必画图。

## 线性链表作业

编写伪代码算法来执行以下每个操作：

- 1. 确定列表中的节点数量。
- 2. 确定列表中整数的总和。
- 3. 将一个节点追加到列表末尾。
- 4. 连接两个列表。
- 5. 释放列表中的所有节点。
- 6. 从列表中删除最后一个元素。
- 7. 复制一个列表。

```
p = list
next(p) = NULL
q = getNode()
info(q) = ...
while (p != NULL)
    next(p) = q
```

```
p = list1
q = list2
while ( ... )
    p -> next = q
    p -> next -> next = list2
```

```
p = list
while (p != NULL)
    temp = next(p)
    x = info(p)
    freeNode(p)
    p = next(p)
```

```
Count = 0
p = list
while (p != NULL)
    Count = Count + 1
    p = next(p)
```

```
p = list
Sum = 0
while (p != NULL)
    temp = info(p)
    Sum = Sum + temp
    p = next(p)
```

```
q = next(p)
x = info(p)
while (p != NULL)
    next(q) = next(p)
    q = p
    p = next(p)
freeNode(q)
```

```
p = NULL
while (list != NULL)
    p = malloc(sizeof(*p))
    copy(p -> q, list -> q)
```

```
p = list
r = NULL
while (p != NULL)
    q = getNode()
if (list == NULL)
    list = q
info(q) = info(p)
```

- 在 C 中定义节点
- 线性链表操作
- 分离编译
- 线性链表代码
- 多项式加法
- 线性链表实验
- 计算非常大的阶乘实验

```
a = 0x45 => 0100 0101
b = 0xA2 => 1010 0010
a & b => 0000 0000
a | b => 1010 0111
~a => 1011 1010
a ^ b => 1000 0111
```

- 逻辑运算
- 关系运算符
- 赋值运算

## 按位运算 & ^

| a | b | a&b |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

```
struct {
    int x;
    char ch;
} A;
[Illustration: Struct memory layout with padding]
```

```
union {
    int x;
    char ch;
} U;
// to save storage space
[Illustration: Union memory layout]
```

## 在 C 中定义节点

我们已经看到，指针允许我们构建和操作各种类型的链表。通过改变指针的值，节点可以被连接、分离和重新组合，其模式会随着程序执行而增长和缩小。

我们可以创建这些节点的链，并跟踪列表中的第一个节点，然后在每个节点中存储一个指向列表中下一个节点的指针。为了实现这一点，每个节点将被定义为一个 `struct`，其中一个字段包含信息，另一个字段包含列表中下一个节点的地址。

我们按如下方式进行声明：

```
struct node {
    int info;
    struct node *next;
};
typedef struct node *NODEPTR;
```

或者，我们可以将上述两个声明合并如下：

```
typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;
```

无论哪种情况，我们都将 `NODEPTR` 声明为指向 `node struct` 的指针。请注意，`node struct` 中的 `next` 字段是一个指针，包含列表中下一个节点的地址。

我们现在可以声明一个 `NODEPTR p` 并动态创建一个新节点：

```
NODEPTR p;
p = (NODEPTR) malloc(sizeof(struct node));
```

我们访问节点的 `info` 字段如下：

```
p->info
```

并且我们可以访问节点的 `next` 字段如下：

```
p->next
```

如前所述，我们可以使用 `free()` 函数来释放动态创建的节点：

```
free(p);
```

请分析以下程序，以创建一个包含五个动态创建节点的链表：

```
// dynamic.c

#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;

void main(void) {
    int i;
    NODEPTR list, p, q;

    list = (NODEPTR) malloc(sizeof(struct node));
    p = list;
    p->info = 1;

    for (i = 2; i <= 5; i++) {
        q = (NODEPTR) malloc(sizeof(struct node));
        q->info = i;
        p->next = q;
        p = q;
    }
    p->next = NULL;
}
```

## 线性链表操作

以下是操作整数线性链表的函数。对于你来说，非常重要的一点是，要分析每个函数，以确保你理解它们的工作原理。请务必画出链表图来帮助你可视化算法。如果不画出链表图以及算法执行过程中列表的变化，就很难编写使用链表的代码。

```
// returns the address of a newly created node
NODEPTR getNode(void) {
    NODEPTR p;

    p = (NODEPTR) malloc(sizeof(struct node));
    if (p == NULL) {
        error("List overflow.");
    }
    return(p);
}

// frees the node pointed to by p
void freeNode(NODEPTR p) {
    free(p);
}

// adds a new node to the front of the list
void addFront(NODEPTR *list, int num) {
    NODEPTR p;

    p = getNode();
    p->info = num;
    p->next = *list;
    *list = p;
}
```

```
// deletes the node at the front of the list
int deleteFront(NODEPTR *list) {
    int temp;
    NODEPTR p;
    if (*list == NULL) {
        error("List underflow.");
    }
    p = *list;
    temp = p->info;
    *list = p->next;
    freeNode(p);
    return temp;
}
```

```
// adds an element to the end of a list
void addLast(NODEPTR *list, int num) {
    NODEPTR p, q;
    p = getNode();
    p->info = num;
    p->next = NULL;
    if (*list == NULL) {
        *list = p;
    } else {
        q = *list;
        while (q->next) {
            q = q->next;
        }
        q->next = p;
    }
}
```

```
// deletes the last element in a list
int deleteLast(NODEPTR *list) {
    NODEPTR p, q;
    int temp = -1;

    if (*list) {
        p = *list;
        q = NULL;
        while (p->next) {
            q = p;
            p = p->next;
        }

        if (!q) {
            *list = NULL;
        } else {
            q->next = NULL;
        }

        temp = p->info;
        freeNode(p);
    }

    return temp;
}
```

```
// inserts a new node after the node pointed to by p
void insertAfter(NODEPTR p, int num) {
    NODEPTR q;

    if (p == NULL) {
        error("Void insertion.");
    }

    q = getNode();
    q->info = num;
    q->next = p->next;
    p->next = q;
}
```

```
// deletes the node after the node pointed to by p
int deleteAfter(NODEPTR p) {
    NODEPTR temp;
    NODEPTR q;

    if (p == NULL || p->next == NULL) {
        error("Void delete()\n");
    }
    q = p->next;
    temp = q->info;
    p->next = q->next;
    freeNode(q);
    return temp;
}
```

```
// insert a node into its correct location within a sorted list
void insert(NODEPTR *list, int num) {
    NODEPTR p, q;

    p = *list;
    q = NULL;
    while (p != NULL && p->info < num) {
        q = p;
        p = p->next;
    }

    if (q == NULL) {
        addFront(list, num);
    } else {
        insertAfter(q, num);
    }
}
```

```
// returns the number of nodes in the list
int numElements(NODEPTR list) {
    int count = 0;

    while (list) {
        count++;
        list = list->next;
    }

    return count;
}
```

```
// returns sum of integers in the list
int sumElements(NODEPTR list) {
    int sum=0;

    while (list) {
        sum += list->info;
        list = list->next;
    }
    return sum;
}
```

```
// traverses a list and outputs contents of list
void outputList(NODEPTR list) {
    while (list) {
        printf("%d", list->info);
        list = list->next;
    }
    printf("\n\n");
}
```

```
// Returns true if the item is found in the list
int contains(NODEPTR list, int num) {
    NODEPTR p;

    p = list;
    while (p != NULL && p->info != num) {
        p = p->next;
    }

    return p != NULL;
}
```

```
// determines whether or not a list is empty
int isEmpty(NODEPTR list) {
    return list == NULL;
}
```

