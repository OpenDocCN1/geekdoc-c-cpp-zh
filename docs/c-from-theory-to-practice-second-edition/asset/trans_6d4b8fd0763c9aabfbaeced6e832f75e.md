
![](img/b8da5dcf9ba7f1fad5213c453d095246_493_0.png)

图 14.3
节点删除。

## 实现示例

在创建链表之前，我们将实现链表的两种特殊情况：栈和队列。请注意，实现这些数据结构的方法有很多；我们尝试以简单易懂的方式实现它们。在下面的示例中，每个节点都是类型为 node 的结构体。如果你将来需要开发类似的数据结构，大部分代码都可以直接重用。

### 实现栈

本节中，我们将创建一个 LIFO（后进先出）栈，正如其名称所示，最后插入的节点最先被取出。它是链表的一种特殊情况，具有以下限制：

- a. 新节点只能插入到栈的开头，并成为其新的头。
- b. 只能删除头节点。

这样的栈类似于一堆脏盘子。每个新盘子都放在栈顶，而我们洗的就是顶部的盘子。

### 练习

C.14.11 定义结构类型 node，其成员为：code、name、grade，以及指向类型为 node 的结构的指针。创建一个节点为该类型结构体的栈。编写一个程序显示菜单以执行以下操作：

- 1. 插入学生。程序应读取学生的数据并将其存储在节点中，该节点成为栈的新头。
- 2. 显示已存储学生的资料。
- 3. 显示最后插入的学生资料。
- 4. 删除最后插入的学生。
- 5. 显示已存储学生的总数。
- 6. 程序终止。

为处理栈，我们使用一个全局指针。该指针始终指向栈的头。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct node
{
    char name[100];
    int code;
    float grd;
    struct node *next; /* Pointer to the next node. Notice that the existence of the structure tag enables us to declare its type. */
} node;

node *head; /* Global pointer that always points to the head of the stack. */

void add_stack(const node *p);
void show_stack(void);
void pop(void);
int size_stack(void);
void free_stack(void);

int read_text(char str[], int size, int flag);

int main(void)
{
    int sel;
    node n;

    head = NULL; /* The NULL value indicates an empty stack. */
    while(1)
    {
        printf("\nMenu selections\n");
        printf("----------------\n");

        printf("1. Add student\n");
        printf("2. View all students\n");
        printf("3. View top student\n");
        printf("4. Delete top student\n");
        printf("5. Number of students\n");
        printf("6. Exit\n");

        printf("\nEnter choice: ");
        scanf("%d", &sel);

        switch(sel)
        {
            case 1:
                getchar();
                printf("Name: ");
                read_text(n.name, sizeof(n.name), 1);

                printf("Code: ");
                scanf("%d", &n.code);
                printf("Grade: ");
                scanf("%f", &n.grd);

                add_stack(&n);
                break;

        case 2:
                if(head != NULL)
                        show_stack();
                else
                        printf("\nThe stack is empty\n");
                break;

        case 3:
                if(head != NULL)
                        printf("\nC:%d N:%s G:%.2f\n\n",
                                head->code,head->name,head->grd);
                else
                        printf("\nThe stack is empty\n");
                break;

        case 4:
                if(head != NULL)
                        pop();
                else
                        printf("\nThe stack is empty\n");
                break;

        case 5:
                if(head != NULL)
                        printf("\n%d students exist in stack\n",
                                size_stack());
                else
                        printf("\nThe stack is empty\n");
                break;

        case 6:
                if(head != NULL)
                        free_stack();
        return 0;

        default:
                printf("\nWrong choice\n");
                break;
                }
        }
        return 0;
}

void add_stack(const node *p)
{
    node *new_node;

    /* Allocate memory to create a new node. */
    new_node = (node*) malloc(sizeof(node));
    if(new_node == NULL)
    {
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    *new_node = *p; /* Copy the student's data into the new node. */
    new_node->next = head; /* The new node is inserted at the beginning of the stack. For example, when the first node is inserted the value of new_node->next becomes equal to the initial value of head, which is NULL. */
    head = new_node; /* head points to the new node, therefore the new node becomes the new head of the stack. */
}

void show_stack(void)
{
    node *p;

    p = head;
    printf("\n**** Student Data ****\n\n");
    while(p != NULL)
    {
        printf("C:%d N:%s G:%.2f\n\n", p->code, p->name, p->grd);
        p = p->next; /* In each iteration, p points to the next node. Once it becomes NULL it means that there is no other node left and the loop terminates. */
    }
}

void pop(void)
{
    node *p;

    p = head->next; /* p points to the next node after the head. This node will become the new head of the stack. */
    printf("\nStudent with code %d is deleted\n", head->code);
    free(head); /* Release the allocated memory. The information about the next node is not lost, because it was saved in p. */
    head = p; /* head points to the new head of the stack. */
}

int size_stack(void)
{
    node *p;
    int num;

    num = 0;
    p = head;
    while(p != NULL)
    {
        p = p->next;
        num++; /* This variable counts the nodes. */
    }
    return num;
}

void free_stack(void)
{
    node *p, *next_node;

    p = head;
    while (p != NULL)
    {
        next_node = p->next; /* next_node always points to the node after the one to be deleted. */
        free(p); /* Release the allocated memory. The information about the next node is not lost, because it was saved in next_node. */
        p = next_node; /* p points to the next node. */
    }
}
```

### 注释：

- a. 在 `add_stack()` 中我们传递一个指针而不是结构体本身，以避免创建结构体的副本并使函数的执行更快。我们将指针声明为 `const`，只是为了记住如何防止修改。
- b. 为了立即显示已存储学生的数量，而无需遍历栈，我们可以移除 `size_stack()` 函数并声明一个全局变量，每次插入学生时递增一次，删除学生时递减一次。一旦用户选择该菜单选项，`printf()` 就会显示其值。这要简单得多，也更快。我们使用 `size_stack()` 的原因是向你展示如何遍历栈的节点。
- c. 如果变量 `head` 在 `main()` 中被声明为局部变量，我们应该将其地址传递给需要它的函数。例如，`add_stack()` 将更改为：

```c
void add_stack(const node *p, node **head_ptr)
{
    node *new_node;

    new_node = (node*) malloc(sizeof(node));
    if (new_node == NULL)
    {
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    *new_node = *p;
    new_node->next = *head_ptr;
    *head_ptr = new_node;
}
```

调用它时我们会写：add_stack (&n, &head);

因为我们认为这段代码更复杂，至少对于初学者来说，我们更喜欢将 head 声明为全局变量并在需要时直接使用它。

### 实现队列

本节中，我们将创建一个 FIFO（先进先出）队列，正如其名称所示，最先插入的节点最先被取出。它是链表的一种特殊情况，具有以下限制：

- a. 新节点只能插入到队列的末尾，并成为其新的尾部。
- b. 只能删除头节点。

### 练习

C.14.12 定义结构类型 node，其成员为：code、name、grade，以及指向类型为 node 的结构的指针。创建一个节点为该类型结构体的队列。编写一个程序显示菜单以执行以下操作：

- 1. 插入学生。程序应读取学生的数据并将其存储在节点中，该节点成为队列的新尾部。
- 2. 显示已存储学生的资料。
- 3. 显示最后插入的学生资料。
- 4. 删除最先插入的学生。
- 5. 程序终止。

为处理队列，我们使用两个全局指针。第一个始终指向队列的头，第二个指向其尾部。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct node
{
    char name[100];
    int code;
    float grd;
    struct node *next;
} node;

node *head; /* Global pointer that always points to the head of the queue. */
node *tail; /* Global pointer that always points to the tail of the queue. */
```
