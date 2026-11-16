

```c
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

```c
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
        } else {
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
int deleteAfter(NODEPTR p) {
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
    }
    else {
        insertAfter(q, num);
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
    int sum = 0;
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
        printf("%8d", list->info);
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

void freeList(NODEPTR *list) {
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
        }
        else {
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
    }
    else {
        return q == NULL ? deleteFront(list) : deleteAfter(q);
    }
}
```

```c
// makes a copy of a list
NODEPTR copyList (NODEPTR list) {
    NODEPTR newlist, p, q;

    newlist = NULL;
    while (list) {
        p = getNode();
        p->info = list->info;
        p->next = NULL;
        if (newlist == NULL) {
            newlist = p;
        }
        else {
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
    }
    else if (list2) {
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
            }
            else {
                q = q->next;
            }
        }
        if (found) {
            s = getNode();
            s->info = p->info;
            s->next = NULL;
            if (!r) {
                newlist = s;
            }
            else {
                r->next = s;
            }
            r = s;
        }
        p = p->next;
    }
    return newlist;
}
```

```c
// display an error message and aborts the program

void error(char *msg) {
    puts(msg);
    exit(1);
}
```

## 分离编译

C 并不要求特定程序的所有语句都必须包含在单个文件中。C 程序可以由分别编写在不同文件中的函数构建，并链接成一个程序。截至目前，我们每个项目的所有 C 源代码都放在单个 .c 文件中。但现在，随着我们的程序变得越来越长，我们需要找到一种更高效的方式来组织代码。

我们可以将源文件编译为“目标代码”，并将其函数与其他源文件中的其他函数链接。如果一个文件中的函数需要调用另一个文件中包含的函数，则可以以常规方式进行函数调用，参数可以以通常的方式传递和返回。在修改和调试程序时，如果每次编译只处理大程序的一部分，会更容易一些。一旦我们编写并调试了一个函数，在处理程序中的其他函数时，就不需要不断重新编译它了。

考虑以下两个 C 源文件：

| 文件 1 | 文件 2 |
|---|---|
| `int main(void) {` | `void faa(void) {` |
| ` foo();` | ` puts("Green");` |
| ` faa();` | ` }` |
| `}` | |
| `void foo(void) {` | |
| ` puts("Red");` | |
| `}` | |

C 编译器找到文件 1 中的两个函数调用。对 `foo()` 的引用在同一文件中找到 `foo()` 的定义时得到解析。对 `faa()` 的引用在文件 2 中找到 `faa()` 的定义时得到解析。指定给 C 编译器的所有目标文件都会被“拉入” C 编译器，并自动包含在最终可执行文件中。

在我们的链表声明和函数的例子中，我们创建两个文件，`list.h` 和 `list.c`。`.h` 文件称为头文件，通常包含声明以及函数原型。以下是我们线性链表的头文件示例：

```c
// list.h

#ifndef LIST_H
#define LIST_H

typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;

NODEPTR getNode(void);
void freeNode(NODEPTR p);
void addFront(NODEPTR *list, int num);
int deleteFront(NODEPTR *list);
void addLast(NODEPTR *list, int num);
int deleteLast(NODEPTR *list);
void insertAfter(NODEPTR p, int num);
int deleteAfter(NODEPTR p);
void insert(NODEPTR *list, int num);
int numElements(NODEPTR list);
void outputList(NODEPTR list);
int contains(NODEPTR list, int num);
int isEmpty(NODEPTR list);
void freeList(NODEPTR *list);
NODEPTR select(NODEPTR list, int num);
int remove(NODEPTR *list, int num);
NODEPTR copyList (NODEPTR list);
void concatList(NODEPTR *list1, NODEPTR list2);
NODEPTR intersect (NODEPTR list1, NODEPTR list2);
void error(char *msg);

#endif
```

请注意头文件中 NODEPTR 结构体定义和函数原型的位置。为了防止编译器多次查看此头文件，我们使用预处理器条件编译命令，告诉编译器仅将此代码引入项目一次：

```c
#ifndef LIST_H
#define LIST_H

...

#endif
```

