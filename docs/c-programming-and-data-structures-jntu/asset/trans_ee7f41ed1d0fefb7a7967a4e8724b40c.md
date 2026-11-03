

![](img/65953ea584e494f3d396b2252cb5ea53_422_0.png)

图 15.13 在双向链表中插入新的首项

![](img/65953ea584e494f3d396b2252cb5ea53_422_1.png)

图 15.14 在双向链表中间插入新项

- 3. 在链表末尾插入一项：在这种情况下，项 New 将被添加到 C 的末尾。因此，C 的 next 指针现在将不再是 0。相反，它将指向 New。同样，New 的 previous 指针将指向 C。最后，New 的 next 指针将变为 0。如图 15.15 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_423_0.png)

图 15.15 在双向链表末尾插入新项

## 删除一项

删除一项也有三种可能的情况，与向双向链表添加一项的情况非常相似。要删除的项可以是第一项、中间某处的项，或者末尾的项。

- 1. 删除链表中的首项：这个过程相当简单。假设我们原来的链表是 A-B-C。要删除第一项（即 A），我们只需将 A 的 next 指针设为 0，并将 B 的 previous 指针也设为 0。注意，A 作为链表中的第一项，其 previous 指针已经是 0。此后，B 自动成为链表中的第一项。如图 15.16 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_423_1.png)

图 15.16 删除双向链表中的首项

### 2. 删除链表中间某处的项：

删除链表中间某处的项，涉及调整待删除项前后两个项的 previous 指针和 next 指针。这里，从链表 A-B-C 中删除项 B。因此，需要进行以下更改：

- (a) A 的 next 指针当前指向 B，现在应指向 C。
- (b) 同样，B 的 previous 指针原本指向 A。现在，C 的 previous 指针应改为指向 A。

为此，应将 B 的 previous 指针和 next 指针设为 0。这会自动将项 B 从链表中删除。如图 15.17 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_424_0.png)

![](img/65953ea584e494f3d396b2252cb5ea53_424_1.png)

图 15.17 从双向链表中间删除一项

注意，链表中项的删除是逻辑上的，而不是物理上的。也就是说，要删除的项（此处为 B）并不会被物理移除，而仅仅是调整 A 和 C 的指针，就会自动将 B 从链表中移除。

### 3. 删除链表中的最后一项：

删除链表中的最后一项（在我们的示例中为 C）是最简单的。为此，应将 B 的 next 指针（通常指向 C）现在设为 0。这实现了两个目标：B 成为链表中的最后一项，同时 C 被自动从链表中移除。同样，C 的 previous 指针应设为 0。该操作如图 15.18 所示。

我们将借助一个程序来说明其余两个操作（即显示链表中的所有项和搜索特定项）。作为附加功能，我们将在向链表中插入新项时自动对链表进行排序。也就是说，链表中的新项会自动添加到其正确的排序位置。

![](img/65953ea584e494f3d396b2252cb5ea53_425_0.png)

图 15.18 删除双向链表中的最后一项

使用双向链表的程序如图 15.19 所示。

```
/* This is a simple program that illustrates the use of a double linked list */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Global linked list variables */
struct linked_list
{
    int number;
    struct linked_list *next; /* pointer to the next item */
    struct linked_list *previous; /* pointer to the previous item */
} list_entry;

struct linked_list *first; /* pointer to the first entry in the list */
struct linked_list *last; /* pointer to the last entry in the list */

/* Function declarations */
char user_choice(void);
void insert(void);
void item_insert(struct linked_list *i, struct linked_list **first, struct linked_list **last);
void item_delete(struct linked_list **first, struct linked_list **last);
struct linked_list *find(int n);
void list(void);
void search(void);
```

图 15.19 双向链表程序——第 I 部分

```
/* start of the program */
void main(void)
{
    first = last = NULL; /* initialize first and last pointers */
    while (1)
{
    switch (user_choice())
    {
        case 1: insert();
            break;

        case 2: item_delete (&first, &last);
            break;

        case 3: list();
            break;

        case 4: search();
            break;

        case 5: return;
    }
}

/* User selects a particular operation to be performed */
char user_choice (void)
{
    char c;

    /* display the menu of available choices */
    printf ("1. Insert an item\n");
    printf ("2. Delete an item\n");
    printf ("3. Print all items\n");
    printf ("4. Search for an item\n");
    printf ("5. Exit\n");

    do
    {
        printf ("Enter your choice: ");
        c = getchar ();
    } while (c < '1' || c > '5');

    return c;
}
```

图 15.19 双向链表程序——第 II 部分

```
/* Accept and store an item at an appropriate position in the list */
void insert (void)
{
    struct linked_list *info;
    int n;    /* Used to accept user input */

    while (1)
    {
        info = (struct linked_list *) malloc (sizeof(list_entry));
        if (!info)
{
    printf ("Insufficient memory");
    return ;
}
/* request user for the next number, 9999 to stop entry */
printf ("Enter the number to be stored, 9999 to quit: ");
scanf ("%d", &n);

if (n == 9999)
    break;
else
{
    /* otherwise, add the number to the info structure */
    info->number = n;
    item_insert (info, &first, &last);
}
}
}
```

图 15.19 双向链表程序——第 III 部分

```
/* Insert an item into the list */
void item_insert (
    struct linked_list *i, /* new item to be added */
    struct linked_list **first, /* first element in the list */
    struct linked_list **last /* last element in the list */
)
{
    struct linked_list *old, *p;

    /* if this is the very first item to be inserted into the list */
    if (*last == NULL)
    {
        i->next = NULL;
        i->previous = NULL;
        *last = i;
        *first = i;
        return;
    }

    /* Begin at the start of the list */
    p = *first;
    old = NULL;

    while (p) /* while there are more items in the list */
    {
        /* if number in the list is less than the one
        entered by the user */
        if (p->number < i->number)
        {
            old = p;
            p = p->next;
}
else
{
  /* if p is not the first item in the list, insert i somewhere middle in the list */
  if (p->previous)
  {
    p->previous->next = i;
    i->next = p;
    i->previous = p->previous;
    p->previous = i;
    return;
  }

  /* i would be the new first item */
  i->next = p;
  i->previous = NULL;
  *first = i;
  return;
}
}
/* i should be the last item */
old->next = i;
i->next = NULL;
i->previous = old;
*last = i;
}
```

图 15.19 双向链表程序——第 IV 部分

```
/* Delete an item from the list */
void item_delete (struct linked_list **first, struct linked_list **last)
{
  struct linked_list *info;
  int s;

  /* accept the number that the user wants to delete */
  printf ("Enter number to be deleted: ");
  scanf ("%d", &s);

  /* find that number in the list */
  info = find (s);

  /* deletion process only if the item is available in the list */
  if (info)
  {
    /* if the first item of the list is to be deleted */
    if (*first == info)
    {
      *first = info->next;

if (*first)
    (*first)->previous = NULL;
else
    *last = NULL;
}
else  /* item to be deleted is somewhere in middle */
{
    info->previous->next = info->next;

    if (info != *last)
        info->next->previous = info->previous;
    else
        *last = info->previous;
}
/* free up the allocated space */
free (info);
}
}
```

图 15.19 双向链表程序——第 V 部分

```
/* find an item in the list */
struct linked_list* find (int n)
{
    struct linked_list *info = first;

    /* while there are more items in the list */
    while (info)
    {
        /* item to be searched is found */
        if (n == info->number) return info;

        /* otherwise, simply move to the next item in the list */
        info = info->next;
    }

    /* if control comes here, it means item was not found */
    printf ("Number entered by you is not in the list\n");
    return NULL;
}
```

```
/* display all the items in the list */
void list (void)
{
    struct linked_list *info = first;

    /* as long as there are more items in the list */
    while (info)
    {
        /* display the current item in the list */
        printf ("%d\n", info->number);

        /* move to the next item in the list */

```

