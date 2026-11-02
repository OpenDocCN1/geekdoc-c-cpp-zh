
### 12.4.3 函数 `printList`

函数 `printList`（第 156–173 行）接收指向链表起始位置的指针作为参数，并将该指针称为 `currentPtr`。该函数首先判断链表是否为*空*（第 159–161 行），如果为空，则打印 "List is empty." 并终止。否则，它打印链表中的数据（第 162–172 行）。当 `currentPtr` 不为 NULL 时，函数打印 `currentPtr->data` 的值，并将 `currentPtr->nextPtr` 赋给 `currentPtr`，以推进到下一个节点。如果链表中最后一个节点的链接不为 NULL，打印算法将试图打印超出链表末尾的内容，从而发生错误。对于链表、栈和队列，打印算法是相同的。

练习 12.20 要求你实现一个递归函数，以反向打印链表。练习 12.21 要求读者实现一个递归函数，在链表中搜索特定的数据项。

## 12.5 栈

栈可以实现为链表的一种受限版本。新节点可以加入栈中，也可以从栈中移除，但*只能在顶部*进行。因此，栈被称为后进先出（LIFO）数据结构。栈通过指向栈顶元素的指针来引用。栈中最后一个节点的链接成员被设置为 NULL，以表示栈底。

图 12.7 展示了一个包含若干节点的栈——`stackPtr` 指向栈顶元素。在这些图中，我们以相同的方式表示栈和链表。栈和链表的区别在于：在链表中，插入和删除可以发生在*任何位置*，但在栈中，插入和删除*只能在顶部*进行。

> **常见编程错误 12.5**
>
> *未将栈底节点中的链接设置为 NULL 可能导致运行时错误。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_521_0.png)

**图 12.7** | 栈的图形表示。

### *主要的栈操作*

用于操作栈的主要函数是 push 和 pop。函数 push 创建一个新节点，并将其放在栈的*顶部*。函数 pop *从栈顶移除一个节点*，*释放*分配给被弹出节点的内存，并*返回被弹出的值*。

### *实现栈*

图 12.8（输出如图 12.9 所示）实现了一个简单的整数栈。程序提供三个选项：1）将一个值压入栈（函数 push），2）从栈中弹出一个值（函数 pop），3）终止程序。

```c
// Fig. 12.8: fig12_08.c
// A simple stack program
#include <stdio.h>
#include <stdlib.h>

// self-referential structure
struct stackNode {
    int data; // define data as an int
    struct stackNode *nextPtr; // stackNode pointer
};

typedef struct stackNode StackNode; // synonym for struct stackNode
typedef StackNode *StackNodePtr; // synonym for StackNode*

// prototypes
void push(StackNodePtr *topPtr, int info);
int pop(StackNodePtr *topPtr);
int isEmpty(StackNodePtr topPtr);
void printStack(StackNodePtr currentPtr);
void instructions(void);

// function main begins program execution
int main(void)
{
    StackNodePtr stackPtr = NULL; // points to stack top
    int value; // int input by user

    instructions(); // display the menu
    printf("%s", "\n");
    unsigned int choice; // user's menu choice
    scanf("%u", &choice);

    // while user does not enter 3
    while (choice != 3) {

        switch (choice) {

            // push value onto stack
            case 1:
                printf("%s", "Enter an integer: ");
                scanf("%d", &value);
                push(&stackPtr, value);
                printStack(stackPtr);
                break;
            // pop value off stack
            case 2:
                // if stack is not empty
                if (!isEmpty(stackPtr)) {
                    printf("The popped value is %d.\n", pop(&stackPtr));
                }

                printStack(stackPtr);
                break;
            default:
                puts("Invalid choice.\n");
                instructions();
                break;
        }

        printf("%s", "? ");
        scanf("%u", &choice);
    }

    puts("End of run.");
}

// display program instructions to user
void instructions(void)
{
    puts("Enter choice:\n"
        "1 to push a value on the stack\n"
        "2 to pop a value off the stack\n"
        "3 to end program");
}

// insert a node at the stack top
void push(StackNodePtr *topPtr, int info)
{
    StackNodePtr newPtr = malloc(sizeof(StackNode));

    // insert the node at stack top
    if (newPtr != NULL) {
        newPtr->data = info;
        newPtr->nextPtr = *topPtr;
        *topPtr = newPtr;
    }
    else { // no space available
        printf("%d not inserted. No memory available.\n", info);
    }
}

// remove a node from the stack top
int pop(StackNodePtr *topPtr)
{
    StackNodePtr tempPtr = *topPtr;
    int popValue = (*topPtr)->data;
    *topPtr = (*topPtr)->nextPtr;
    free(tempPtr);
    return popValue;
}

// print the stack
void printStack(StackNodePtr currentPtr)
{
    // if stack is empty
    if (currentPtr == NULL) {
        puts("The stack is empty.\n");
    }
    else {
        puts("The stack is:");

        // while not the end of the stack
        while (currentPtr != NULL) {
            printf("%d --> ", currentPtr->data);
            currentPtr = currentPtr->nextPtr;
        }

    }
    puts("NULL\n");
}

// return 1 if the stack is empty, 0 otherwise
int isEmpty(StackNodePtr topPtr)
{
    return topPtr == NULL;
}
```

**图 12.8** | 一个简单的栈程序。

```text
Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 1
Enter an integer: 5
The stack is:
5 --> NULL

? 1
Enter an integer: 6
The stack is:
6 --> 5 --> NULL

? 1
Enter an integer: 4
The stack is:
4 --> 6 --> 5 --> NULL

? 2
The popped value is 4.
The stack is:
6 --> 5 --> NULL

? 2
The popped value is 6.
The stack is:
5 --> NULL

? 2
The popped value is 5.
The stack is empty.

? 2
The stack is empty.

? 4
Invalid choice.

Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 3
End of run.
```

**图 12.9** | 图 12.8 程序的示例输出。

### 12.5.1 函数 push

函数 push（第 76–89 行）将一个新建节点放在栈顶。该函数由三个步骤组成：

- 1. 通过调用 `malloc` 创建一个*新节点*，并将分配内存的位置赋给 `newPtr`（第 78 行）。
- 2. 将要在栈中放置的值赋给 `newPtr->data`（第 82 行），并将 `*topPtr`（*栈顶指针*）赋给 `newPtr->nextPtr`（第 83 行）——`newPtr` 的*链接成员*现在指向*先前的栈顶节点*。
- 3. 将 `newPtr` 赋给 `*topPtr`（第 84 行）——`*topPtr` 现在指向*新的栈顶*。

涉及 `*topPtr` 的操作会改变 `main` 中 `stackPtr` 的值。图 12.10 说明了函数 push。该图的 (a) 部分显示了 push 操作之前的 `stackPtr` 和新节点。(b) 部分中的虚线箭头说明了 push 操作的*第 2 步和第 3 步*，这些步骤使包含 12 的节点成为新的栈顶。

![](img/d0d3b7423c2d9e5650be79209ea1885d_525_0.png)

**图 12.10** | push 操作。

### 12.5.2 函数 pop

函数 pop（第 92–99 行）移除栈顶的节点。函数 main 在调用 pop 之前判断栈是否为空。pop 操作由五个步骤组成：

- 1. 将 `*topPtr` 赋给 `tempPtr`（第 94 行）；`tempPtr` 将用于*释放*不需要的内存。
- 2. 将 `(*topPtr)->data` 赋给 `popValue`（第 95 行），以*保存*栈顶节点中的值。
- 3. 将 `(*topPtr)->nextPtr` 赋给 `*topPtr`（第 96 行），使 `*topPtr` 包含*新栈顶节点的地址*。
- 4. *释放* `tempPtr` 所指向的内存（第 97 行）。
- 5. *返回 popValue* 给调用者（第 98 行）。

图 12.11 说明了函数 pop。(a) 部分显示了上一次 push 操作之后的栈。(b) 部分显示 `tempPtr` 指向栈的*第一个节点*，而 `*topPtr` 指向栈的*第二个节点*。函数 free 用于*释放内存*，该内存由 `tempPtr` 指向。

![](img/d0d3b7423c2d9e5650be79209ea1885d_526_0.png)

### 12.5.3 栈的应用

栈有许多有趣的应用。例如，每当发生*函数调用*时，被调用的函数必须知道如何*返回*其调用者，因此*返回地址*被压入栈中（第 5.7 节）。在一系列函数调用中，连续的返回地址按*后进先出*顺序压入栈中，以便每个函数都能返回其调用者。栈以与传统非递归调用相同的方式支持递归函数调用。

栈包含每次调用函数时为*自动变量*创建的空间。当函数返回其调用者时，该函数自动变量的空间从栈中弹出，这些变量不再为程序所知。编译器在求值表达式和生成机器语言代码的过程中有时也会使用栈。练习题探讨了栈的几种应用。

