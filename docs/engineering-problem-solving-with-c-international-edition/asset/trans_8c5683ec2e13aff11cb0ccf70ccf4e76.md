

要从链表中删除一个值，我们需要找到要删除的节点。我们再次使用指向列表头部的指针来访问列表中的第一个数据值。然后我们使用当前节点中的指针从一个节点移动到另一个节点。如果我们到达的数据值大于要删除的值，我们将打印一条消息，表明要删除的值不在列表中。要删除的节点可以是第一个节点、两个其他节点之间的节点，或者最后一个节点。我们必须小心处理每种情况，以确保指针得到正确更新。图 7.6 到 7.8 概述了这三种情况中的每一种。对于每种情况，我们都从图 7.2 给出的链表开始。请注意，这些删除后有一些节点（和数据值）无法再被访问。例如，在图 7.6 中，我们无法再访问值 10；在图 7.7 中，我们无法再访问值 21；在图 7.8 中，我们无法再访问值 35。另外，请注意，如果列表只包含一个节点，删除第一个节点可能会导致空列表。

## 空列表

我们现在将开发一组四个函数来创建和维护链表。第一个函数用于判断链表是否为空列表，第二个函数用于打印链表的内容，第三个函数用于在正确的有序位置插入节点，第四个函数用于删除节点。链表中的每个节点将由以下结构表示：

```
struct node
{
 int data;
 struct node *link;
 };
```

![](img/02c4582f051c5b51776411c92b079035_377_0.png)

![](img/02c4582f051c5b51776411c92b079035_377_1.png)

![](img/02c4582f051c5b51776411c92b079035_377_2.png)

结构 node 有两个数据成员：一个用于存储数据值的整数和一个指向链表中下一个节点的指针。用于判断列表是否为空的函数具有以下原型：

```
int empty(struct node *head);
```

函数 empty 检查链表的头部，如果链表为空则返回值 1，否则返回值 0。该函数将由其余三个函数使用。

```
/******************************************************************/
/* This function returns a value of one if the linked list   */
/* is empty.                                                 */
/******************************************************************/
int empty(struct node *head)
{
   /* Declare variables. */
   int k=0;

   /* Determine if the list is empty. */
   if (head == NULL)
      k = 1;

   /* Return integer. */
   return k;
}
/******************************************************************/
```

打印列表的函数原型为

```
void print_list(struct node *head);
```

print_list 函数从列表的开始处开始，打印每个节点的数据值，直到到达列表末尾。该函数中 if 语句的条件引用了 empty 函数：

```
if (empty(head))
   ...
```

请记住，如果条件是数值，则值零被视为“假”，非零值被视为“真”。因此，如果列表为空，函数返回值 1，因此为“真”；否则，函数返回值零，条件则为“假”。

```
/******************************************************************/
/* This function prints a linked list.                          */
/******************************************************************/
void print_list(struct node *head)
{
   /* Declare variables. */
   struct node *next;

   /* Print linked list. */
   if (empty(head))
       printf("Empty List \n");
   else
   {
       printf("List Values: \n");
       next = head;
       while (next->link != NULL)
       {
           printf("%d \n",next->data);
           next = next->link;
       }
       printf("%d \n",next->data);
   }
   /* Void return. */
   return;
}
```

insert 函数从列表的头部开始，并在列表的正确位置插入新节点。如果新数据值已在列表中，将打印一条消息且不会插入新节点。请记住，链表的头部是指向列表中第一个节点的指针。当指针用作函数参数时，它是按值引用。由于在第一个节点之前插入节点或在空列表中插入节点时需要更新头指针，因此我们必须传递指向头指针的指针，使其成为按地址引用。这样我们就可以在函数内部根据需要更新头指针。请仔细查看语法。

```
/* This function inserts a new node in a linked list. */
void insert(struct node **ptr_to_head, struct node *nw)
{
    /* Declare variables and function prototypes. */
    struct node **next;
    /* Check for insert to empty list. */
    if (empty(*ptr_to_head))
        *ptr_to_head = nw;
    else
    {
        /* Traverse list to find location for insert. */
        next = ptr_to_head;
        while ((*next)->data < nw->data && (*next)->link != NULL)
            next = &(*next)->link;
        /* Check for duplicate data. */
        if ((*next)->data == nw->data)
            printf("Node already in list.\n");
        else
        {
            /* Check for insert after last node. */
            if ((*next)->data < nw->data)
                (*next)->link = nw;
            else
            {
                nw->link = *next;
                *next = nw;
            }
        }
    }
    /* Void return. */
    return;
}
/**********************************************************************/
```

删除节点的函数原型为：

```
void remove(struct node **ptr_to_head, int old);
```

该函数从列表的头部开始，查找数据值为 old 的节点。如果在列表中未找到 old，将打印一条消息。如果找到 old，则删除该节点并释放内存。由于每当删除列表中的第一个节点时都必须更新头指针，因此我们必须传递指向列表头部的指针。（我们没有使用 delete 这个名称，因为许多编译器将其视为保留字。）

```
/**********************************************************************/
/* This function deletes a node from a linked list. */
void remove(struct node **ptr_to_head, int old)
{
    /* Declare variables and function prototypes. */
    struct node *next, *last, *hold, *head;
    /* Check for delete to empty list. */
    head = *ptr_to_head;
    if (empty(head))
        printf("Empty list. \n");
    else
    {
        /* Check for deletion of first node. */
        if (head->data == old)
        {
            /* Delete first node. */
            hold = head;
            *ptr_to_head = head->link;
            free(hold);
        }
        else
        {
            /* Traverse list to find old node. */
            next = head->link;
            last = head;

            while ((next->data < old) && (next->link != NULL))
            {
                last = next;
                next = next->link;
            }
            /* Delete node if found. */
            if (next->data == old)
            {
                hold = last;
                last->link = next->link;
                free(hold);
            }
            else
                printf("Value %d not in list. \n", old);
        }
    }
    /* Void return. */
    return;
}
/* ---------------------------------------------------------- */
```

我们现在将展示一个 main 函数来测试这些函数。在每次调用 insert 和 remove 后都会调用 print_list 函数，以验证函数是否正常工作。

```
/* ---------------------------------------------------------- */
/* Program chapter_7_7 */
/* ---------------------------------------------------------- */
/* This program tests the functions to insert and delete */
/* items in a linked list. */
/* ---------------------------------------------------------- */
#include <stdio.h>
#include <stdlib.h>

/* Define structure to represent a node in a linked list. */
struct node
{
int data;
struct node *link;
};

int main(void)
{
/* Declare variables and function prototypes. */
int k=0, old, value;
struct node *head, *next, *previous, *nw, *pptr_to_head=&head;
void insert(struct node **pptr_to_head, struct node *nw);
void remove(struct node **pptr_to_head, int n);
int empty(struct node *head);
void print_list(struct node *head);

/* Generate and print a linked list with five nodes. */
head = (struct node *)malloc(sizeof(struct node));
next = head;
```

