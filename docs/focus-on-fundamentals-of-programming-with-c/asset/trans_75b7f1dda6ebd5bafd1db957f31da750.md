

```c
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
        }
        else {
            q->next = NULL;
        }

        temp = p->info;
        freeNode(p);
    }
    return temp;
}
```

```c
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

```c
// deletes the node after the node pointed to by p
int DeleteAfter(NODEPTR p) {
    int temp;
    NODEPTR q;

    if (p == NULL || p->next == NULL) {
        error("Void deletion.");
    }

    q = p->next;
    temp = q->info;
    p->next = q->next;
    freeNode(q);
    return temp;
}
```

```c
// insert a node into its correct location within a sorted list
void Insert(NODEPTR *list, int num) {
    NODEPTR p, q;

    p = *list;
    q = NULL;
    while (p != NULL && p->info < num) {
        q = p;
        p = p->next;
    }

    if (q == NULL) {
        addFront(list, num);
    }
    else {
        InsertAfter(q, num);
    }
}
```

```c
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

```c
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

```c
// traverses a list and outputs contents of list
void outputList(NODEPTR list) {
    while (list) {
        printf("%d", list->info);
        list = list->next;
    }
    printf("\n\n");
}
```

```c
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

```c
// determines whether or not a list is empty
int isEmpty(NODEPTR list) {
    return list == NULL;
}
```

```c
// frees all the nodes in a list
void freelist(NODEPTR *list) {
    NODEPTR p;
    while (*list) {
        p = *list;
        *list = p->next;
        freeNode(p);
    }
}
```

```c
// returns a pointer to the node with the requested value;
// otherwise returns NULL
NODEPTR select(NODEPTR list, int num) {
    while (list) {
        if (list->info == num) {
            return list;
        } else {
            list = list->next;
        }
    }
    return list;
}
```

```c
// removes the first occurrence of an item in a list
int remove(NODEPTR *list, int num) {
    NODEPTR p, q;
    p = *list;
    q = NULL;
    while (p != NULL && p->info != num) {
        q = p;
        p = p->next;
    }
    if (p == NULL) {
        return -1;
    } else {
        return q == NULL ? deleteFront(list) : deleteAfter(q);
    }
}
```

```c
// makes a copy of a list
NODEPTR copyList(NODEPTR list) {
    NODEPTR newlist, p, q;
    newlist = NULL;
    while (list) {
        p = getNode();
        p->info = list->info;
        p->next = NULL;
        if (newlist == NULL) {
            newlist = p;
        } else {
            q->next = p;
        }
        q = p;
        list = list->next;
    }
    return newlist;
}
```

```c
// concatenates two lists
void concatList(NODEPTR *list1, NODEPTR list2) {
    NODEPTR p;
    if (*list1 == NULL) {
        *list1 = list2;
    } else if (list2) {
        p = *list1;
        while (p->next) {
            p = p->next;
        }
        p->next = list2;
    }
}
```

```c
// returns a pointer to a new list containing the intersection of
// two lists
NODEPTR intersect(NODEPTR list1, NODEPTR list2) {
    NODEPTR p, q, r, s, newlist;
    int found;

    p = list1;
    newlist = NULL;
    r = NULL;
    while (p) {
        q = list2;
        found = 0;
        while (q && !found) {
            if (p->info == q->info) {
                found = 1;
            } else {
                q = q->next;
            }
        }
        if (found) {
            s = getNode();
            s->info = p->info;
            s->next = NULL;
            if (!r) {
                newlist = s;
            } else {
                r->next = s;
            }
            r = s;
        }
        p = p->next;
    }
    return newlist;
}

// display an error message and aborts the program
void fatal(char *msg) {
    fprintf(stderr,
        "%s\n", msg);
    exit(1);
}
```

## 多项式加法

为了找到一元多项式的合适表示，我们必须区分多项式每一项中的系数和指数。下面展示了作为线性链表节点表示的多项式的一项。

| 系数 | 指数 | 指向下一项的链接 |
|---|---|---|

例如：

3X² 将表示为：

| 3.0 | 2 | |
|---|---|---|

X⁴ 将表示为：

| 1.0 | 4 | |
|---|---|---|

5 将表示为：

| 5.0 | 0 | |
|---|---|---|

3X⁵ - 2X³ + 4 将表示为：

| 3.0 | 5 | -> | -2.0 | 3 | -> | 4.0 | 0 | |
|---|---|---|---|---|---|---|---|---|

### 多项式表示

请注意将多项式表示为线性链表的以下三个前提条件：

- 项必须在线性链表中按指数递减顺序存储。
- 不允许两个项具有相同的指数。
- 不允许任何项具有零系数。

线性链表的每个节点将表示多项式的一项，是一个包含以下信息的 `struct`：

- 系数
- 指数
- 指向多项式下一项的指针

```c
typedef struct poly {
    float coeff;
    int expn;
    struct poly *next;
} *POLYPTR;
```

### 相加两个多项式

要将两个多项式相加，我们只需各扫描一次：

- 如果在两个多项式中找到指数相同的项，则相加系数并将新项复制到和多项式的末尾；否则，将指数较大的项复制到和多项式中并继续。
- 当到达其中一个多项式的末尾时，将另一个多项式的剩余部分复制到和多项式中。
- 我们必须小心不要在和中包含系数为 0 的项。例如：

  ```
  6X^5 + 2X^4 + 3X^3 + 2X
  +
  3X^5 - 2X^4 - 5X^2 - 8X + 7
  9X^5 + 3X^4 - 5X^2 - 6X + 7
  ```

```c
// poly.c

#include <stdio.h>

typedef struct poly {
    float coeff;
    int expon;
    struct poly *next;
} *POLYPTR;

POLYPTR sum(POLYPTR p, POLYPTR q) {
    float coeff;
    POLYPTR add = NULL;
    while (p != NULL && q != NULL) {
        if (p->expon == q->expon) {
            coeff = p->coeff + q->coeff;
            if (coeff) {
                makeTerm(&add, coeff, p->expon);
                p = p->next;
                q = q->next;
            }
        } else if (p->expon > q->expon) {
            makeTerm(&add, p->coeff, p->expon);
            p = p->next;
        } else {
            makeTerm(&add, q->coeff, q->expon);
            q = q->next;
        }
    }
    while (p) {
        makeTerm(&add, p->coeff, p->expon);
        p = p->next;
    }
    while (q) {
        makeTerm(&add, q->coeff, q->expon);
        q = q->next;
    }
    return add;
}
```

在算法的多个位置，我们必须使用给定的系数和指数创建一个新项，并将其放在和多项式的末尾，即指针 `last` 所指向的项之后。请注意，指针 `add` 将始终指向创建的第一个项，而指针 `last` 将始终指向和多项式的最后一个项。

```c
void makeTerm(POLYPTR *add, float coeff, int expon) {
    POLYPTR t;
    POLYPTR last = NULL;

    t = (POLYPTR) malloc(sizeof(struct poly));
    t->coeff = coeff;
    t->expon = expon;
    t->next = NULL;
    if (last == NULL) {
        *add = t;
    }
    else {
        last->next = t;
    }
    last = t;
}
```

多项式的其他操作可以编程为与我们的加法函数性质相同的函数。为了额外学分，看看你能否完成以下任务：

- 编写一个方法，输入一系列系数和指数，并将它们形成如前所述的链式多项式。
- 编写一个函数，用于相减两个多项式。
- 编写一个函数，用于计算多项式的一阶、二阶和三阶导数。
- 编写一个函数，用于将多项式乘以标量。
- 编写一个函数，给定一个多项式和一个整数，在该整数处求解多项式的值。
- 编写一个函数，将多项式作为系数和指数的序列以吸引人的方式打印出来。

