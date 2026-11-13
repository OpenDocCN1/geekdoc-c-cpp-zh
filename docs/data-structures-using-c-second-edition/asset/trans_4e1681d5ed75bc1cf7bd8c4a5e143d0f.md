

## 在双向链表中删除给定节点之前的节点

考虑图 6.53 所示的双向链表。假设我们要删除值为 4 的节点的前驱节点。在讨论链表中将要进行的更改之前，让我们先看看算法。

![](img/be6359df08208122bec6fad1103de211_207_0.png)

图 6.53 在双向链表中删除给定节点之前的节点

- 步骤 1: IF START = NULL
- 输出 UNDERFLOW
- 转到步骤 9
- [IF 结束]
- 步骤 2: 设置 PTR = START
- 步骤 3: 重复步骤 4，当 PTR -> DATA != NUM 时
- 步骤 4: 设置 PTR = PTR -> NEXT
- [循环结束]
- 步骤 5: 设置 TEMP = PTR -> PREV
- 步骤 6: 设置 TEMP -> PREV -> NEXT = PTR
- 步骤 7: 设置 PTR -> PREV = TEMP -> PREV
- 步骤 8: 释放 TEMP
- 步骤 9: 退出

图 6.54 删除给定节点之前节点的算法

图 6.54 显示了删除双向链表中给定节点之前节点的算法。在步骤 2 中，我们取一个指针变量 PTR，并将其初始化为 START。也就是说，PTR 现在指向链表的第一个节点。while 循环遍历链表以到达所需节点。一旦我们到达包含 val 的节点，PTR 的 PREV 字段将被设置为包含 PTR 之前节点的前驱节点的地址。PTR 之前节点的内存被释放并返回到空闲池。

因此，我们可以看到，只要知道该节点的地址，就可以在常数次操作内插入或删除一个节点。请注意，在单向链表的情况下这是不可能的，因为执行相同操作还需要前一个节点的地址。

## 编程示例

- 3. 编写一个程序来创建双向链表，并在所有情况下执行插入和删除操作。

```c
#include <stdio.h>
#include <conio.h>
#include <malloc.h>

struct node
{
    struct node *next;
    int data;
    struct node *prev;
};
struct node *start = NULL;
struct node *create_ll(struct node *);
struct node *display(struct node *);
struct node *insert_beg(struct node *);
struct node *insert_end(struct node *);
struct node *insert_before(struct node *);
struct node *insert_after(struct node *);
struct node *delete_beg(struct node *);
struct node *delete_end(struct node *);
struct node *delete_before(struct node *);
struct node *delete_after(struct node *);
struct node *delete_list(struct node *);
int main()
{
    int option;
    clrscr();
    do
    {
        printf("\n\n *****MAIN MENU *****");
        printf("\n 1: Create a list");
        printf("\n 2: Display the list");
        printf("\n 3: Add a node at the beginning");
        printf("\n 4: Add a node at the end");
        printf("\n 5: Add a node before a given node");
        printf("\n 6: Add a node after a given node");
        printf("\n 7: Delete a node from the beginning");
        printf("\n 8: Delete a node from the end");
        printf("\n 9: Delete a node before a given node");
        printf("\n 10: Delete a node after a given node");
        printf("\n 11: Delete the entire list");
        printf("\n 12: EXIT");
        printf("\n\n Enter your option : ");
        scanf("%d", &option);
        switch(option)
        {
            case 1: start = create_ll(start);
                    printf("\n DOUBLY LINKED LIST CREATED");
            case 2: break;
                    start = display(start);
            case 3: break;
                    start = insert_beg(start);
            case 4: break;
                    start = insert_end(start);
            case 5: break;
                    start = insert_before(start);
            case 6: break;
                    start = insert_after(start);
            case 7: break;
                    start = delete_beg(start);
            case 8: break;
                    start = delete_end(start);
            case 9: break;
                    start = delete_before(start);
            case 10: start = delete_after(start);
                      break;
            case 11: start = delete_list(start);
                     printf("\n DOUBLY LINKED LIST DELETED");
                     break;
        }while(option != 12);
        getch();
        return 0;
    }
struct node *create_ll(struct node *start)
{
    struct node *new_node, *ptr;
    int num;
    printf("\n Enter -1 to end");
    printf("\n Enter the data : ");
    scanf("%d", &num);
    while(num != -1)
    {
        if(start == NULL)
        {
            new_node = (struct node*)malloc(sizeof(struct node));
            new_node->prev = NULL;
            new_node->data = num;
            new_node->next = NULL;
            start = new_node;
        }
        else
        {
            ptr=start;
            new_node = (struct node*)malloc(sizeof(struct node));
            new_node->data=num;
            while(ptr->next!=NULL)
                ptr=ptr->next;
            ptr->next = new_node;
            new_node->prev=ptr;
            new_node->next=NULL;
        }
        printf("\n Enter the data : ");
        scanf("%d", &num);
    }
    return start;
}
struct node *display(struct node *start)
{
    struct node *ptr;
    ptr=start;
    while(ptr!=NULL)
    {
        printf("\t %d", ptr -> data);
        ptr = ptr->next;
    }
    return start;
}
struct node *insert_beg(struct node *start)
{
    struct node *new_node;
    int num;
    printf("\n Enter the data : ");
    scanf("%d", &num);
    new_node = (struct node *)malloc(sizeof(struct node));
    new_node->data = num;
    start->prev = new_node;
    new_node->next = start;
    new_node->prev = NULL;
    start = new_node;
    return start;
}
struct node *insert_end(struct node *start)
{
    struct node *ptr, *new_node;
    int num;
    printf("\n Enter the data : ");
    scanf("%d", &num);
    new_node = (struct node *)malloc(sizeof(struct node));
    new_node->data = num;
    ptr = start;
    while(ptr->next != NULL)
        ptr = ptr->next;
    ptr->next = new_node;
    new_node->prev = ptr;
    new_node->next = NULL;
    return start;
}
struct node *insert_before(struct node *start)
{
    struct node *new_node, *ptr;
    int num, val;
    printf("\n Enter the data : ");
    scanf("%d", &num);
    printf("\n Enter the value before which the data has to be inserted :");
    scanf("%d", &val);
    new_node = (struct node *)malloc(sizeof(struct node));
    new_node->data = num;
    ptr = start;
    while(ptr->data != val)
        ptr = ptr -> next;
    new_node -> next = ptr;
    new_node -> prev = ptr->prev;
    ptr->prev -> next = new_node;
    ptr->prev = new_node;
    return start;
}
struct node *insert_after(struct node *start)
{
    struct node *new_node, *ptr;
    int num, val;
    printf("\n Enter the data : ");
    scanf("%d", &num);
    printf("\n Enter the value after which the data has to be inserted :");
    scanf("%d", &val);
    new_node = (struct node *)malloc(sizeof(struct node));
    new_node->data = num;
    ptr = start;
    while(ptr->data != val)
        ptr = ptr -> next;
    new_node -> next = ptr -> next;
    new_node -> prev = ptr->next;
    ptr->next = new_node;
    return start;
}
struct node *delete_beg(struct node *start)
{
    struct node *ptr;
    ptr = start;
    start = start -> next;
    start -> prev = NULL;
    free(ptr);
    return start;
}
struct node *delete_end(struct node *start)
{
    struct node *ptr;
    ptr = start -> next;
    while(ptr -> next != NULL)
    ptr = ptr -> next;
    ptr -> prev -> next = NULL;
    free(ptr);
    return start;
}
struct node *delete_after(struct node *start)
{
    struct node *ptr, *temp;
    int val;
    printf("\n Enter the value after which the node has to deleted : ");
    scanf("%d", &val);
    ptr = start;
    while(ptr -> data != val)
    ptr = ptr -> next;
    temp = ptr -> next;
    ptr -> next = temp -> next;
    temp -> next -> prev = ptr;
    free(temp);
    return start;
}
struct node *delete_before(struct node *start)
{
    struct node *ptr, *temp;
    int val;
    printf("\n Enter the value before which the node has to deleted : ");
    scanf("%d", &val);
    ptr = start;
    while(ptr -> data != val)
    ptr = ptr -> next;
    temp = ptr -> prev;
    if(temp == start)
    start = delete_beg(start);
    else
    {
    ptr -> prev = temp -> prev;
    temp -> prev -> next = ptr;
    }
    free(temp);
    return start;
}
struct node *delete_list(struct node *start)
{
    while(start != NULL)
    start = delete_beg(start);
    return start;
}
```

