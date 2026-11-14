

类型为 void* 的单个参数。由于我们不希望对传入任务的信息类型施加任何限制，也不希望强制每个任务处理相同类型的数据，因此我们采用结构体作为向任务传递数据的手段。为了满足所有 TCB 必须外观一致，同时又能保留对传入任务数据的灵活性这一要求，通过 void* 指针引用数据结构来移除与其关联的类型信息。在任务内部，指针必须被强制转换回原始类型，然后才能解引用以获取数据。

每个任务将拥有自己的栈。TCB 中的第三个条目是指向该栈的指针。第四个条目给出任务的优先级。第五和第六个条目是用于将 TCB 链接到上述任何队列中下一个和前一个 TCB 的指针。

## 11.11.3 一个简单的内核

现在让我们通过一系列简单的示例来开发一个初步的操作系统内核，以了解所有这些组件如何协同工作。我们假设有三个简单的作业需要调度和执行：

- 导入一些数据。
- 对数据进行计算。
- 显示数据。

初始示例将是一个操作共享数据的简单函数队列。在此示例中，数组将用作队列的底层数据类型。系统将永久运行，每个任务将按顺序调度和执行。这种实现的一个重要特征是，每个任务将运行到完成，然后才允许另一个任务运行。

第二个示例将为每个任务声明一个 TCB。TCB 将包含任务（通过指向实现任务的函数的指针引用）以及将传入该任务的数据。任务队列仍将使用数组实现，调度和分派算法将被保留。与第一个示例一样，每个任务运行到完成。两种设计都在图 11.13 的数据流图中表达。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_620_0.png)

图 11.13 三个共享公共数据缓冲区的异步任务

### 示例 11.1

图 11.14 中的软件清单给出了简单操作系统内核设计的初步版本。

```c
// Building a simple OS kernel - step 1
#include <stdio.h>
// Declare the prototypes for the tasks
void get( void* aNumber); // input task
void increment( void* aNumber); // computation task
void display( void* aNumber); // output task
void main(void)
{
int i=0; // queue index
int data; // declare a shared data
int* aPtr = &data; // point to it
void (*queue[3])(void*); // declare queue as an array of pointers to
// functions taking an arg of type void*
queue[0] = get; // enter the tasks into the queue
queue[1] = increment;
queue[2] = display;
while(1)
{
queue[i]( (void*) aPtr); // dispatch each task in turn
i = (i+1)%3;
}
return;
}
void get( void* aNumber) // perform input operation
{
printf( "Enter a number: 0-9" );
*(int*) aNumber = getchar(); // discard cr
getchar(); // convert to decimal from ascii
*(int*) aNumber -= '0';
return;
}
void increment( void* aNumber) // perform computation
{
int* aPtr = (int*) aNumber;
(*aPtr)++;
return;
}
void display( void* aNumber) // perform output operation
{
printf( "The result is: %d\n", *(int*)aNumber);
return;
}
```

图 11.14 一个简单的操作系统内核

### 示例 11.2

示例 11.1 中的设计现在已在图 11.15 中修改，以使用任务控制块。

```c
// Building a simple OS kernel - step 2
#include <stdlib.h>

// Declare the prototypes for the tasks
void get (void* aNumber);    // input task
void increment (void* aNumber); // computation task
void display (void* aNumber);   // output task

// Declare a TCB structure
typedef struct
{
    void* taskDataPtr;
    void (*taskPtr)(void*);
} TCB;

void main(void)
{
    int i=0;        // queue index
    int data;       // declare a shared data
    int* aPtr = &data; // point to it
    TCB* queue[3];  // declare queue as an array of pointers to TCBs

    // Declare some TCBs
    TCB inTask;
    TCB compTask;
    TCB outTask;
    TCB* aTCBPtr;

    // Initialize the TCBs
    inTask.taskDataPtr = (void*)&data;
    inTask.taskPtr = get;

    compTask.taskDataPtr = (void*)&data;
    compTask.taskPtr = increment;

    outTask.taskDataPtr = (void*)&data;
    outTask.taskPtr = display;

    // Initialize the task queue
    queue[0] = &inTask;
    queue[1] = &compTask;
    queue[2] = &outTask;

    // schedule and dispatch the tasks
    while(1)
    {
        aTCBPtr = queue[i];
        aTCBPtr->taskPtr( (aTCBPtr->taskDataPtr) );
        i = (i+1)%3;
    }
    return;
}

void get (void* aNumber)    // perform input operation
{
    printf ( "Enter a number: 0-9 " );
    *(int*)aNumber = getchar();   // discard cr
    *(int*)aNumber -= '0';    // convert to decimal from ascii
    return;
}

void increment (void* aNumber)     // perform computation
{
    int* aPtr = (int*) aNumber;
    (*aPtr)++;
    return;
}
void display (void* aNumber)      // perform output operation
{
    printf ("The result is: %d\n", *(int*)aNumber);
    return;
}
```

图 11.15 一个简单的操作系统内核

前两个示例中的设计可能存在两个基本问题。第一个源于任务集合中的控制流。因为每个任务在完成前都会占用 CPU，如果任何任务不释放控制权，系统将永久挂起。典型例子是 get() 任务，它取决于用户输入一段数据。

第二个潜在问题源于任务间通信的受影响方式。所有任务都共享一个名为 data 的公共变量。在当前设计中，两个任务正在读取数据，只有一个任务在写入数据。此外，由于同一时间只能有一个任务处于活动状态，因此没有问题。

中断服务例程（ISR）。要实现设计改进，必须进行多项修改。必须编写中断服务例程（ISR），并将 ISR 添加到中断向量表中。

## 11.11.4 再论中断

由于每个处理器和交叉编译器都使用专有协议来管理中断，我们将通过将伪代码与 C 例程相结合来说明通用过程。为此，我们将定义伪代码函数 setVect()，如图 11.16 所示。

| 语法 | 说明 |
|------|------|
| `void setVect(unsigned int intNum, void (*anISR*)(void));` | |
| `intNum` | 中断号 |
| `anISR` | 中断服务例程 |

图 11.16 指定中断服务例程

调用时，该函数将 ISR 函数的指针写入中断向量表中的指定插槽。

每个处理器将支持的中断与相应的硬件或软件功能或源关联。中断可能源于处理器内部或外部，并可能专有于系统或用户。

在定义和使用中断时，必须确保为每个正在使用的中断编写并分配一个 ISR，并确保该例程分配给正确的中断。如果使用了中断但未编写或分配 ISR，则当中断发生时，向量表中相关插槽的（无效）内容将被解释为 ISR 的地址。处理器将向该内存地址传递控制，该地址没有关联任何有意义的代码；随后指令（或数据）的执行可能导致系统崩溃。

大多数微处理器支持多个级别的中断控制。在此上下文中，控制指定系统（以及最终进程）接受或忽略中断的能力。最高级别的控制由 enable 和 disable 指令提供。正如名称所暗示的，enable 指令允许系统识别中断。

disable 指令则起相反作用。

第二级控制通过屏蔽实现。这种功能允许有选择地监听或忽略单个中断。通常，微处理器支持一个屏蔽寄存器，每个中断关联一位。如果屏蔽位是逻辑 1，则相关中断在发生时会被识别。同样，当该位是逻辑 0 时，中断将被忽略。如果支持屏蔽，通常至少有一个中断会被指定为不可屏蔽。也就是说，必须监听并响应该中断。通常，不可屏蔽中断与系统级功能相关，并且常常是灾难管理工具。

第三级控制为每个中断分配优先级。高优先级中断可以中断低优先级中断，但反之则不行。在大多数情况下，每个中断的优先级由微处理器制造商设定。

中断可以被视为异步函数或子程序调用。系统处理中断的机制大多与我们在函数调用中遇到的机制相同。与函数调用一样，在中断下，系统状态信息保存在栈中并在返回时恢复。因此，与函数调用一样，也可能发生栈溢出。如果在基于优先级的方案中允许中断在同一级别的 ISR 中中断另一个中断，则存在栈溢出的潜在风险，必须加以管理。通常的解决方案是根据需要禁用或屏蔽中断，以确保不会发生溢出。在禁用或屏蔽中断时，请记住，导致事件仍然会发生；系统只是不响应。因此，在使用中断和 ISR 时，始终保持例程尽可能简单和简短。超过 12–18 行代码的 ISR 可能太长了。目标是响应中断，完成绝对需要完成的最少工作，然后退出 ISR；如有必要，进一步处理可以在某个任务或前台进程中完成。

示例 11.3 说明了使用中断来管理来自键盘的系统异步输入。在该设计中，所有任务现在都全局访问共享变量，如图 11.17 的数据和控制流图所示。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_624_0.png)

