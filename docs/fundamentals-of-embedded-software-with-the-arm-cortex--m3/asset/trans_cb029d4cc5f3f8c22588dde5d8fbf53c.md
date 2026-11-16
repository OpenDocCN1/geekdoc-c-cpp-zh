

7. 下面所示的函数在多线程应用程序中被多个线程调用时会导致运行时错误。请说明问题的原因，然后修改该函数以纠正问题，但不要更改函数的参数列表或其返回值。

```
int ExtractWords(char *sentence, char *words[])
{
    char *word;
    int count;
    count = 0;
    word = sentence;
    for (;;) {
        word = strtok(word, ";,:.?!");
        if (!word) break;
        words[count++] = word;
        word = NULL;
    }
    return count;
}
```

8. 以下哪些函数是线程安全的？

```
int f1(int select)
{
    static const int a[] = {-2, -1, 0, +1, +2} ;
    ...
    return a[select] ;
}
```

```
char *f2(char *b)
{
    static char a[100] ;
    strcpy(a, b) ;
    return a ;
}
```

```
long long int f3(void)
{
    static long long int x = 0 ;
    return ++x ;
}
```

```
unsigned f4(unsigned a, unsigned b)
{
    if (a == 0) return 0 ;
    if (a == 1) return b ;
    return f4(a - 1, b) ;
}
```

9. 图12-3中所示的原始strtok函数不是线程安全的。设计一个线程安全的版本，仅在绝对必要时通过禁用中断来保护其每个临界区。

10. 在不添加代码保护其临界区的情况下，设计以下函数的线程安全版本。

```
double AvgSoFar(double value)
{
    static double total = 0.0 ;
    static int count = 0 ;
    return (total += value) / ++count ;
}
```

## 系统初始化

桌面应用程序员从不需要担心*系统*初始化。绝大多数应用程序由某种操作系统加载和执行，该操作系统在引导过程中已经初始化了系统，以提供适当的运行时环境。然而，嵌入式应用程序几乎总是从断电状态启动。当通电时，处理器没有堆栈、没有堆、没有中断系统，也没有定时器。此外，I/O设备必须初始化，变量的初始值必须从ROM复制到RAM。

使系统启动并运行所需做的大部分工作都是特定于硬件的。也就是说，它根据CPU类型、内存的数量和类型以及连接的I/O设备种类而异。它也可能是特定于软件的，因为每个编译器和/或实时内核可能会对内存应如何组织、中断系统应如何配置以及首选的定时器滴答速率提出其自身特殊的要求。

本章不可能涵盖初始化可以或应该如何进行的每一种可能变体；它*确实*涵盖了使用IAR Systems Embedded Workbench编写C程序并编译为在德州仪器LM3S811（一种基于ARM Cortex-M3处理器的微控制器MCU）上运行的程序可能如何进行初始化。除此之外，本章将说明如何对一些I/O设备（包括中断控制器和可编程定时器）进行编程。

初始化进行的事件顺序不一定与这里呈现的相同。但是，一般而言，CPU初始化通常是第一步，启用中断系统通常是最后一步。

## 13.1 内存布局

设计初始化代码的一个良好起点是考虑编译器的期望。大多数应用程序将内存分为五个区域：程序代码（称为“文本”）、已初始化静态量（称为“数据”）、未初始化静态量（称为“bss”）、堆栈和堆。尽管这些区域的相对位置可能不同，但初始向量表和代码必须位于非易失性内存（如闪存EPROM）中，向量表位于地址0，其他所有内容位于读/写内存（RAM）中（图13-1）。

![](img/f0b8aa873b11dc585ed698a10d04e7a7_243_0.png)

图13-1 嵌入式C程序的内存组织。

## 13.2 CPU和向量表

首次通电时，ARM Cortex-M3处理器会自动从地址0（向量表的第一个条目）加载堆栈指针（R13），并从地址4（向量表的第二个条目）加载程序计数器（R15）。然后开始执行。因此，初始向量表及其指向的代码必须保存在非易失性内存中，该内存在断电后不会丢失其内容。

堆栈可以声明为32位无符号长整型数组。由于第一次压栈将存储在SP-4给出的地址，因此SP应初始化为数组中最后一个条目之后的32位字的地址。因此，如果数组声明为1：

```
static unsigned long pulStack[128] @ ".noninit" ;
```

则SP的初始值可以指定为&pulStack[128]。为了避免在两个地方指定堆栈大小（128），相同的初始值可以指定为：

```
((unsigned long)&pulStack[0]) + sizeof(pulStack)
```

或简化为：

```
(unsigned long) pulStack + sizeof(pulStack)
```

1 行首以"at"符号(@)开头的行末的非同寻常文本用于IAR的Embedded Workbench，用于告诉编译器该变量不应包含在由启动代码初始化的静态量中，该启动代码在进入函数main之前执行，如第13.3.2节所述。

加载到程序计数器中的值是启动函数的入口地址，其责任是根据需要执行任何其他初始化，然后转移到函数main的入口点以启动应用程序。

向量表中还有两个条目必须在执行开始前具有初始值。由于不可屏蔽中断和硬故障不能被禁用，这两个异常的处理程序必须已经存在，并且它们的入口地址存储为向量表中地址8和12的下一个两个条目。所有其他中断最初处于禁用状态，所有中断优先级均处于默认值。因此，至少向量表必须填充其前四个条目。使用IAR Embedded Workbench时，可以使用以下代码在C中创建向量表并强制将其位于地址0：

```
// A union that describes the entries of the vector table. The union is needed
// since the first entry is the stack pointer and the remainder are function pointers.
typedef union
{
    void (*pfnHandler)(void);
    unsigned long ulPtr;
} uVectorEntry;
```

```
// The vector table. Note that the proper constructs must be placed on
// this to ensure that it ends up at physical address 0x0000.0000.
__root const uVectorEntry _vector_table[] @ ".invec" =
{
    .ulPtr = (unsigned long) pulStack + sizeof(pulStack), // Initial SP
    .iar_program_start, // Initial PC
    NmiISR, // The NMI handler
    FaultISR, // The hard fault handler
    ...
}
```

表的声明使用了IAR Embedded Workbench编译器支持的几个C语言扩展：

- 1. 声明开头出现的文本"__root"可防止链接器删除该变量，即使标识符"__vector_table"在程序的其他任何地方都未按名称引用。

- 2. 文本"@".invec"导致链接器将向量表定位于从地址0开始的位置。

- 3. 表中的第一个条目使用名为指定初始化器的C99特性。它是一个用花括号括起来的表达式；表达式开头的".ulPtr = "文本告诉编译器，该值应分配给名为ulPtr的联合体成员。

第一次堆栈压栈将值存储到地址SP-4，因此表达式“(unsigned long) pulStack + sizeof(pulStack)”产生紧邻堆栈上方的32位字的地址。

## 13.3 C运行时环境

处理器启动并运行后，但在执行进入函数main之前，启动函数必须初始化位于读/写内存中的已初始化静态量（data）和未初始化静态量（bss）的内容。

### 13.3.1 从非易失性内存复制初始值到数据区域

所有静态变量（隐式包括所有全局变量）都必须由启动函数初始化。那些在声明中指定了初始值的静态量作为一个连续组位于“数据”区域；作为它们初始值的常量作为一个相应但分离的连续组位于非易失性内存的文本区域。在进入函数main之前，启动函数必须将这些常量复制到读/写内存的数据区域中各自的目标位置。使用IAR Embedded Workbench IDE创建的程序所使用的启动函数如下所示：

```
unsigned long *pulSrc, *pulDest, *pulEnd;
//
// Copy the data segment initializers from flash to SRAM.
//
pulSrc = __segment_begin("DATA_ID");
pulDest = __segment_begin("DATA_I");
pulEnd = __segment_end("DATA_I");
while(pulDest < pulEnd)
{
    *pulDest++ = *pulSrc++;
}
```

除了通过从非易失性内存复制来初始化数据部分外，在某些MCU上，将程序代码复制到读/写内存也是可取的，因为非易失性内存的访问时间通常比读/写内存慢一些。

### 13.3.2 清零未初始化静态量

在C语言中，有一个约定，即内存bss区域中的未初始化静态量在启动期间被填充为零。此区域包括所有未指定初始值而声明的静态对象。由于某些程序包含依赖于此

2. “__segment_begin()”和“__segment_end()”用于IAR的Embedded Workbench，用于提供由参数指定的段的第一个字节和之后字节的地址：“DATA_ID”指非易失性内存中作为已初始化静态量（data）初始值的常量；“DATA_I”指已初始化静态量所在的读/写内存中的段。

