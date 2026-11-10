

- 为新节点分配内存，如果分配时已知其数据域，则设置该数据域：

  ```c
  struct node *p;
  p = malloc(sizeof(struct node));
  p->data = 111;
  ```

- 将新节点的 `.next` 指针设置为指向原来的第一个节点。后一个节点通过头指针访问：

  ```c
  p->next = head;
  ```

  *必须在……之前完成此赋值……*

- 将头指针重新赋值为指向新节点：

  ```c
  head = p;
  ```

  *……在本次赋值之前。*

与用于插入数组元素的技术（10.5.1）相比，这是一种简单而快速的技术。只需为新节点创建内存，为一个或多个数据域赋值，并重新调整两个指针。没有比这更简单的了！

![](img/d75612dcf3ab36327142238ab5bb21d8_567_0.png)

### 16.11.2 在末尾添加节点

要在链表末尾添加节点，首先遍历整个链表以到达其末尾。该过程可以是迭代的或递归的，并且需要采取以下步骤：

- 按通常方式为新节点分配内存，并在必要时为其数据域赋值。同时，将其 `.next` 指针设置为 NULL。
- 为了通过迭代遍历链表到达其末尾，使用头指针的副本作为关键变量：

  ```c
  current = head;
  while (current->next != NULL)
      current = current->next;
  ```

  *最后一个节点的 `.next` 被设置为 NULL*

- 将原来的最后一个节点（其 `.next` 先前被设置为 NULL）的 `.next` 指针设置为指向新节点。

赋值语句 `current = current->next;` 需要仔细研究，因为它在许多链表操作中都会用到。该语句在每次循环迭代中改变当前节点的地址。因此，它让链表中的每个节点都能被访问。然而，由于遍历是顺序的，与数组元素的随机访问相比，它速度较慢。

> **提示：** 不要丢失头指针，因为它是你访问链表节点唯一可用的工具。遍历链表时，复制这个指针，并在循环中将该副本用作关键变量。

## 16.12 在开头和末尾删除节点

与添加类似，可以在链表中的任意位置删除节点。与插入相比，删除节点是一项简单的操作，而在端点处甚至更简单。此外，在非终端位置删除之前，通常需要先搜索某个值。良好的习惯要求删除时释放已分配的内存。

要删除链表开头的节点，头指针必须指向下一个节点，但在此之前必须先保存其原值：

```c
p = head;
head = p->next;
```

完成之后，就可以释放原来第一个节点所使用的空间：

```c
free(p);
```

对于在链表末尾删除，按通常方式遍历链表，但*你还必须定位并保存前一个节点的地址：*

```c
current = head;
while (current->next != NULL) {
    previous = current;
    current = current->next;
}
```

循环迭代完成后，current 指向最后一个节点，其内存现在可以释放。指针 previous 现在指向新的最后一个节点，因此 previous->next 应设置为 NULL。末尾的节点删除如图 16.8 所示。

![](img/d75612dcf3ab36327142238ab5bb21d8_568_0.png)

## 16.13 `head_tail_operations.c`：添加和删除单个节点

程序 16.8 演示了在链表开头和末尾的添加与删除操作。该程序首先创建一个单节点链表，然后在

```c
/* Delete node at end after ... */
current = head;
while (current->next != NULL) {            /* ... locating end of list */
    previous = current;
    current = current->next;
}
previous->next = NULL;                     /* previous is now last node */
free(current);
print_list(head);                           /* Prints 20 */

exit(0);
}

void print_list(struct node *head)
{
    while (head != NULL) {                  /* head is local variable here */
        printf("%hd ", head->data);
        head = head->next;                  /* Doesn't change head in main */
    }
    printf("\n");
    return;
}
```

**程序 16.8：`head_tail_operations.c`**

|  |  |
| --- | --- |
| 20 | *创建第一个节点* |
| 10 20 | *在开头插入节点* |
| 10 20 30 | *在末尾插入节点* |
| 20 30 | *在开头删除节点* |
| 20 | *在末尾删除节点* |

**程序输出：`head_tail_operations.c`**

`print_list` 函数使用头指针作为参数，打印所有链表节点数据成员的值。然而，参数 head 是该函数的局部变量。因此，尽管 head 的值在每次循环迭代中都会改变，但改变后的值在函数外部不可用。若要在不使用函数的情况下打印此链表，请将 head 复制到一个单独的变量中，并在循环中将该副本用作关键变量。

> **注意：** 本程序在链表开头执行的添加和删除操作，对应于与栈相关的*压入*和*弹出*操作。这种数据结构将在 16.16.1 节中讨论。

## 16.14 `list_manipulation.c`：一个链表处理程序

现在我们将探讨其他链表处理操作，但这一次，我们将为每一种操作开发一个函数。程序 16.9 使用了一些这样的用户自定义函数，用于处理链表中间位置的查询和编辑操作。其中一些函数直接从 `main` 调用，另一些则从这些函数中调用。该程序执行以下任务：

- 根据用户输入创建链表。
- 遍历链表以计数并打印节点。
- 在节点中搜索用户指定的值。
- 根据搜索结果添加和删除节点。

该程序列出了函数原型和 `main` 函数。函数定义在随后讨论它们的子节中展示。这些讨论不包括 `print_list` 函数，因为该函数已在 16.13 节中解释过。

该程序首先使用 `scanf`、`malloc` 和 `add_node` 函数创建链表。由于所有用户自定义函数都使用指向 `struct node` 的指针作为参数，因此结构体本身必须在 `main` 之前声明。这使得该结构体及其指针成为全局的，即在整份文件中可见。

```c
/* list_manipulation.c: A comprehensive program that uses 6 functions to
                         create, query, add and delete nodes of a linked list. */
#include <stdio.h>
#include <stdlib.h>

struct node {                               /* Declaration before main */
    short data;
    struct node *next;
};

/* The function prototypes */
void add_node(struct node *p, struct node *q);
void print_list(struct node *head);
short count_nodes(struct node *head);
struct node *find_node(struct node *head, short val);
void insert_after(struct node *head, short val1, short val2);
void delete_node(struct node **head, short val);

int main(void)
{
    struct node *head, *p, *q;
    short count = 0, temp, val1, val2;

    /* Create the list first */
    fputs("Key in some short integers and press [Ctrl-d]:\n", stderr);
    while (scanf("%hd", &temp) == 1) {
        count++;
        q = malloc(sizeof(struct node));
        q->data = temp;
        if (count == 1)
            head = p = q;                 /* p represents previous node */
        else {
            add_node(p, q);               /* Establishes links between two nodes */
            p = q;                         /* Assigns current node to previous node */
        }
    }

    q->next = NULL;                   /* Marks end of linked list */

    print_list(head);                 /* Prints the list */
    printf("Number of nodes in list = %d\n", count_nodes(head));

    /* Search for a value and insert a node after located node */
    fputs("Values to search and insert: ", stderr);
    scanf("%hd%hd", &val1, &val2);
    insert_after(head, val1, val2);
    print_list(head);

    /* Search for a value and delete the located node */
    fputs("Value to delete: ", stderr);
    scanf("%hd", &val1);
    delete_node(&head, val1);         /* Allows head pointer to be modified */
    print_list(head);

    exit(0);
}

... Functions definitions ...
```

**程序 16.9：`list_manipulation.c`**

```c
Key in some short integers and press [Ctrl-d]:
11 22 33 44 66 77 88 99
11 22 33 44 66 77 88 99
Number of nodes in list = 8
Values to search and insert: 44 55
11 22 33 44 55 66 77 88 99
Value to delete: 66
11 22 33 44 55 77 88 99
```

**程序输出：`list_manipulation.c`**

### 16.14.1 add_node 函数

```c
void add_node(struct node *p, struct node *q)
{
    q->next = p->next;
    p->next = q;
    return;
}
```

> 该语句在创建链表时是多余的

