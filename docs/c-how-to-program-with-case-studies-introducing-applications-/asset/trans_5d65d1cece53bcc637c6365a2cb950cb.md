
```c
int main(void) {
    StackNodePtr stackPtr = NULL; // points to stack top
    int value = 0; // int input by user

    instructions(); // display the menu
    printf("%s", "? ");
    int choice = 0; // user's menu choice
    scanf("%d", &choice);

    // while user does not enter 3
    while (choice != 3) {
        switch (choice) {
            case 1: // push value onto stack
                printf("%s", "Enter an integer: ");
                scanf("%d", &value);
                push(&stackPtr, value);
                printStack(stackPtr);
                break;
            case 2: // pop value off stack
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
        scanf("%d", &choice);
    }

    puts("End of run.");
}

// display program instructions to user
void instructions(void) {
    puts("Enter choice:\n"
         "1 to push a value on the stack\n"
         "2 to pop a value off the stack\n"
         "3 to end program");
}

// insert a node at the stack top
void push(StackNodePtr *topPtr, int info) {
    StackNodePtr newPtr = malloc(sizeof(StackNode));
```

*图 12.2 | 一个简单的栈程序。（第 2 部分，共 4 部分。）*

```c
73        // insert the node at stack top
74        if (newPtr != NULL) {
75            newPtr->data = info;
76            newPtr->nextPtr = *topPtr;
77            *topPtr = newPtr;
78        }
79        else { // no space available
80            printf("%d not inserted. No memory available.\n", info);
81        }
82    }
83
84    // remove a node from the stack top
85    int pop(StackNodePtr *topPtr) {
86        StackNodePtr tempPtr = *topPtr;
87        int popValue = (*topPtr)->data;
88        *topPtr = (*topPtr)->nextPtr;
89        free(tempPtr);
90        return popValue;
91    }
92
93    // print the stack
94    void printStack(StackNodePtr currentPtr) {
95        if (currentPtr == NULL) { // if stack is empty
96            puts("The stack is empty.\n");
97        }
98        else {
99            puts("The stack is:");
100
101            while (currentPtr != NULL) { // while not the end of the stack
102                printf("%d --> ", currentPtr->data);
103                currentPtr = currentPtr->nextPtr;
104            }
105
106            puts("NULL\n");
107        }
108    }
109
110    // return 1 if the stack is empty, 0 otherwise
111    int isEmpty(StackNodePtr topPtr) {
112        return topPtr == NULL;
113    }
```

*图 12.2 | 一个简单的栈程序。（第 3 部分，共 4 部分。）*

```text
Enter choice:
1 to push a value on the stack
2 to pop a value off the stack
3 to end program
? 1

Enter an integer: 5
The stack is:
5 --> NULL
```

*图 12.2 | 一个简单的栈程序。（第 3 部分，共 4 部分。）*

```text
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

**图 12.2** | 一个简单的栈程序。（第 4 部分，共 4 部分。）

### 12.5.1 函数 push

**函数 push**（*第 70–82 行*）使用以下步骤将一个新节点放入栈中：

- 1. 调用 `malloc` 创建一个新节点，然后将分配内存的地址赋给 `newPtr`（第 71 行）。
- 2. 将入栈的值赋给 `newPtr->data`（第 75 行），并将 `*topPtr`（指向栈顶的指针）赋给 `newPtr->nextPtr`（第 76 行）。新栈顶节点的链接成员现在指向前一个栈顶节点。
- 3. 将 `newPtr` 赋给 `*topPtr`（第 77 行）——这会修改 `main` 中的 `stackPtr`，使其指向新的栈顶。

下图说明了 push 操作。部分 (a) 显示了执行 push 操作将新节点插入栈顶之前的栈和新节点——`*topPtr` 表示 `main` 中的 `stackPtr`。部分 (b) 中的虚线箭头说明了前面讨论的 *步骤 2 和 3*，它们将包含 12 的节点插入栈顶。

栈中包含每次调用函数时为自动局部变量创建的空间。当函数返回其调用者时，该函数自动变量所占的空间会从栈中弹出，这些变量对程序来说就不再已知。编译器在求值表达式和生成机器语言代码的过程中有时也会使用栈。练习中探讨了若干栈应用。

### 自测

- 1. *多项选择* 以下哪项陈述是*错误的*？
  - a) 栈必须实现为链表的一种受限版本。
  - b) 新节点只从栈顶添加和移除。
  - c) 栈是一种后进先出（LIFO）数据结构。
  - d) 栈通过指向其栈顶元素的指针来引用。

**答案：** (a) 是 *错误的*。实际上，栈*可以*实现为链表的一种受限版本，但并非必须如此。

- 2. *多项选择* 以下陈述 a)、b) 或 c) 中哪项是*错误的*？
  - a) 当调用函数时，它必须知道如何返回其调用者，因此被调用函数的返回地址被压入栈中。
  - b) 在一系列函数调用中，连续的返回地址按后进先出顺序压入栈中，以便每个函数都能返回其调用者。
  - c) 栈以与传统非递归调用相同的方式支持递归函数调用。
  - d) 以上所有陈述都是*正确的*。

**答案：** (a) 是 *错误的*。实际上，压入栈中的是*调用者的*返回地址。

## 12.6 队列

队列类似于杂货店的结账队伍：

- 排在第一位的人先得到服务。
- 其他顾客只能从队尾加入队列并等待服务。

只能从队列的头部（前端）移除节点，并且只能在尾部（后端）插入节点。因此，队列被称为先进先出（FIFO）数据结构。插入和移除操作分别称为入队（enqueue，读作“en-cue”）和出队（dequeue，读作“dee-cue”）。

### 队列应用

队列在计算机系统中有许多应用：

- 对于只有一个处理器的计算机，一次只能服务一个用户。其他用户的条目被放入队列。随着用户得到服务，每个条目逐渐前进到队列前端。队列前端的条目是下一个得到服务的条目。
- 同样，对于当今的多核系统，运行的程序可能比处理器多。当前未运行的程序被放入队列，直到当前忙碌的处理器变得可用。在附录 C 中，我们讨论多线程。当程序的工作被划分为多个可并行执行的线程时，线程数可能多于处理器数。当前未运行的线程需要在队列中等待。
- 队列还支持打印假脱机。一个办公室可能只有一台打印机。许多用户可以在给定时间发送文档进行打印。当打印机忙碌时，额外的文档被假脱机到内存或二级存储中，就像缝纫线绕在线轴上直到需要时一样。这些文档在队列中等待，直到打印机变得可用。
- 通过计算机网络（如互联网）传输的信息包也会在队列中等待。每当一个包到达网络节点时，都必须沿着通往最终目的地的路径将其路由到网络中的下一个节点。路由节点一次路由一个包，因此额外的包会被入队，直到路由器可以路由它们。

### 队列图示

下图说明了一个包含若干节点的队列。注意分别指向队列头和尾的指针。与链表和栈一样，未将队列最后一个节点中的链接设置为 NULL 可能会导致逻辑错误。

![](img/43d318ad505997c339a3ea78d716d162_670_0.png)

### 实现队列

图 12.3 执行队列操作。该程序提供以下选项：在队列中插入节点（函数 enqueue）、从队列中移除节点（函数 dequeue）以及终止程序。第 7–10 行定义 struct queueNode，我们将用它表示队列的节点。同样，我们使用 typedef（第 12–13 行）使代码更具可读性。此应用程序中的许多逻辑与我们的链表和栈示例类似，因此这里我们重点关注差异。最初，headPtr 和 tailPtr（第 23–24 行）都为 NULL，表示空队列。

```c
1 // fig12_03.c
2 // Operating and maintaining a queue
3 #include <stdio.h>
4 #include <stdlib.h>
5
```
