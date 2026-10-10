
因为工作线程会执行 `exitfn()` 以及它被要求执行的其他函数，所以在在锁定互斥锁 `wrlock[tid]` 后，它必须在退出前解锁。条件变量 `cv_work[]` 用于管理线程告诉工作线程有工作要做。条件变量 `cv_free[]` 用于工作线程告诉管理线程它们已完成分配给它们的任务。条件变量也与互斥锁配合使用。条件变量 `cv_work` 和 `cv_free` 与互斥锁协调。工作线程通过以下函数获取控制：

```c
void *worker(void *arg) {
    int tid = *((int *)arg);
    while (1) {
        pthread_mutex_lock(wrlock+tid-1);
        if(workflag[tid-1])
            pthread_cond_wait(cv_work+tid-1, wrlock+tid-1);
        (*fnlist[tid-1])(arglist[tid-1]);
        workflag[tid-1] = 0;
        pthread_cond_signal(cv_free+tid-1);
        pthread_mutex_unlock(wrlock+tid-1);
    }
    return NULL;
}
```

工作线程锁定 `wrlock[tid-1]`，在第 4 行检查 `workflag[tid-1]`，这是工作线程和管理线程访问的共享内存区域。如果没有工作要做，它会在第 5 行在 `cv_work+tid-1` 上等待。库函数 `pthread_cond_wait()` 取一个条件变量指针和一个互斥锁指针。它在睡眠前解锁互斥锁，这意味着工作线程在寻找工作时不会竞争锁。这种在进入睡眠前解锁互斥锁是条件变量语义的核心元素。

## 5.3. Pthreads 简介

管理线程执行的对应函数定义如下。

```c
void manager(long *list, int count) {
    for(int i=0; i < count; i++) {
        for(int j=0; j < nthreads-1; j++) {
            pthread_mutex_lock(wrlock+j);
            if(workflag[j]==1)
                pthread_cond_wait(cv_free+j, wrlock+j);
            fnlist[j] = (i%2==0) ? addone : addtwo;
            arglist[j] = (void *)(list+j+1);
            workflag[j] = 1;
            pthread_cond_signal(cv_work+j);
            pthread_mutex_unlock(wrlock+j);
        }
    }
    if(i%2==0)
        addone((void *)list);
    else
        addtwo((void *)list);
}
```

管理线程在锁区域外执行其工作，但指示工作已分配的信号 `cv_work` 必须在锁区域内。如果在锁区域外发送信号，可能会在工作线程获取并验证 `workflag[tid-1]` 为 0 之后、调用 `pthread_cond_wait()` 等待 `cv_work[tid-1]` 之前到达如果发生这种情况，信号将丢失导致程序死锁。管理线程在并行区域外执行其工作，调用 `add()` 或 `addtwo()`。

```c
void spawn_workers() {
    static int tidlist[nthreads-1];
    for(int i=0; i < nthreads-1; i++) {
        workflag[i] = 0;
        tidlist[i] = i+1;
        pthread_mutex_init(wrlock+i, NULL);
    }
}
```

```c
pthread_cond_init(cv_work+i, NULL);
pthread_cond_init(cv_free+i, NULL);
pthread_create(pthread+i, NULL, worker, tidlist+i);
}
```

将 `tidlist[]` 定义为 `static` 的原因之前已经解释过。唯一的语法元素是用于创建和初始化条件变量的函数。条件变量以及互斥锁和线程都是使用 `NULL` 或默认属性创建的。

销毁线程函数的完整列表给出的。

```c
void shutdown(){
    static int tidlist[threads-1];
    for(int i=0; i < threads-1; i++){
        pthread_mutex_lock(wrcklock+i);
        if(workflag[i]==1)
            pthread_cond_wait(cv_free+i, wrcklock+i);
        tidlist[i] = i+1;
        fnlist[i] = exitfn;
        arlist[i] = tidlist+i;
        workflag[i]=1;
        pthread_cond_signal(cv_work+i);
        pthread_mutex_unlock(wrcklock+i);
    }
    for(int i=0; i < threads-1; i++){
        pthread_join(pthread[i], NULL);
        pthread_mutex_destroy(wrcklock+i);
        pthread_cond_destroy(cv_work+i);
        pthread_cond_destroy(cv_free+i);
    }
}
```

通过要求线程执行 `exitfn()` 来终止线程。这里的新语法是销毁条件变量的函数。管理线程在销毁条件变量和对应该工作线程的互斥锁之前，必须与该工作线程 join。

## 5.3 Pthreads 简介

当使用条件变量实现并行区域时，如果管理线程想要分配工作但工作线程正忙，它会进入睡眠。如果工作线程空闲但发现没有被分配工作，它们也会让自己进入睡眠。互斥锁的自旋行为在这里不会发生。管理线程分配工作与工作线程完成工作之间存在规律且可预测的交替。

## TLB 刷新与条件变量实现的代价

表 5.6 显示，使用条件变量实现的并行区域在两个线程时的平均代价为 30,000 个周期。在四核 3.4 GHz AVX 机器上（完整名称见 A.1），代价要低得多，在四个线程时仅为 9,000 个周期。即使使用八个线程，每个并行区域的平均代价也只有 18,000 个周期，且远低于两个线程的代价。

这个谜团的解释似乎如下：对于两个、四个或八个线程，在管理线程分配工作与工作线程完成工作的交替期间会发生上下文切换。对于两个线程，线程会在 3.4 GHz AVX 机器的四个核心之间进行切换。当工作线程或管理线程被切换出时，编辑器、网页浏览器或内核线程将获得处理器。对于八个线程，每个并行区域的平均上下文切换多得多，但在同一线程组的两个线程之间的上下文切换中，几乎每次切换的开销都小得多。内核不需要切换页表或刷新 TLB。当具有不同虚拟地址空间的进程切换时，TLB 刷新对于保持内存系统的完整性和正确性至关重要。上下文切换及相关因素的巨大开销似乎解释了为什么只有两个线程时条件变量的实现要贵得多。

**练习 5.3.1.** 编写一个程序使用 Pthreads 反转一个长数组。你的程序需要互斥锁或自旋锁吗？你预计你的程序比相同任务的 OpenMP 程序更快还是更慢？请解释。

**练习 5.3.2.** 解释为什么在并行区域的 C 实现中使用 `volatile` 限定，而在使用互斥锁、自旋锁或条件变量的实现中未使用。

## 5.4 程序内存

在 4.4 节描述的虚拟内存设置中，每个进程都有自己的页表将虚拟内存映射到物理内存，每条带有内存引用的指令都会调用这种从虚拟到物理的映射。虚拟内存系统允许许多不同的进程在同一台计算机上共存。线程是共享从虚拟到物理映射的进程组。此外，每个线程可以在其他线程通常不可见的区域定义自己的局部变量。因此，线程的概念与内存系统紧密相关，理解程序内存有助于理解线程。

在本节中，我们局限于单线程程序，但深入研究程序内存的设置和组织方式。5.4.1 节展示了如何在 Linux 中定义一个新的系统调用。操作系统是一个程序，与其他任何其他程序一样，系统调用是用户程序用于调用它的函数集。因此，有用于读和写文件的系统调用等。几乎不应该编写自己的系统调用。Linux 提供了大量的系统调用集，多到人们难以全面掌握其中的许多功能。

尽管有此警告， 5.4 节中定义的系统调用具有若干教学目的。稍后，我们向 Linux 内核中插入打印语句，以检查内存系统和线程创建。该系统调用用于开启或关闭这些打印语句。

实现系统调用的第一个教训简单来说就是理解：操作系统只是另一个程序，尽管是一个极其复杂的程序。由于操作系统管理不同且同时的进程，并发处理一直是一个问题。线程编程的许多主题（如互斥）在很久以前就出现了。

程序对操作系统的依赖比大多数人认为的要多得多。当我们深入理解速度或某些特性时，不可避免地会进入操作系统。我们对内核的这些探索有助于我们理解段错误、内存错误和线程创建。

> 关于 Linux 系统调用，请参 Kerrisk (2010)。

## 5.4 栈

5.4.2 节介绍了栈。栈是最简单且最重要的数据结构之一。所有的编程模型都基于函数调用，而栈是在调用调用处保存状态并在返回处恢复状态的数据结构。理解状态的保存和恢复对所有编程都有用。另一个优势是它有助于理解在抽象设置中可能看起来人工的抽象。在 5.4.2 节中，我们用栈来解释递归。

系统调的定义位于 Linux 源码树中 `kernel/sys.c` 文件的末（版本 3.6）。^8

```c
1 int dv_print_flag=0;
2 EXPORT_SYMBOL(dv_print_flag);
3
4 asmlinkage long sys_set_dvflag(int flag){
5 dv_print_flag = flag;
6 return 77;
7 }
```

第 1 行定义了一个 int 类型的全局变量。该全局变量用于控制内核其他部分的打印级别。例如，如果变量的值在 [100, 200) 范围内，与线程/进程相关的内核函数将打印消息。对于其他范围，文件 I/O 相关函数将打印消息。这些消息的目的是帮助我们理解内核内部发生了什么。打印这些消息需要对内核的其他部分进行修改。

第 2 行导出了该全局变量。Linux 内核通过链接成千上万个编译单元构建，而 `sys.c` 只是其中之一。内核的一部分（如设备驱动程序）使用 `valloc()` 动态加载。导出全局变量是为了使其对动态链接模块可见。我们的一些打印消息将位于设备驱动和其他模块中。

第 4 行的 `asmlinkage` 饰符是该系统调用定义中的新元素。它是第一个提示，说明系统调用与任何函数不同。如果一个普通函数有一个 int 类型的单个参数，按照约定，在 64 位 Linux 中参数通过 `%edi` 寄存器传递。^9 在执行系统调用时，没有这种约定。系统调用的所有参数都通过内核栈传递（栈将在下一节中讨论）。`asmlinkage` 修饰符告诉编译器该函数将在栈上接收其所有参数。

退出系统调用是特殊的，与进入时一样。使用 `SYEXIT` 指令来退出系统调用。

> ^8 参见 Love (2010)。
> ^9 关于 GNU/Linux 寄存器的函数调用约定，请参阅 gcc 手册或 Agner Fog 网页上的优化文档第 5 部分：http://www.agner.org/optimize/

## 5.4. 程序内存

为了让全局变量 `dv_print_flag` 对所有编译单元可见，在源码树的 `include/linux/printk.h` 中放置了声明：

```c
extern int dv_print_flag;
```

内核没有与 C 库链接。但内核无法调用 `printf()`。但 Linux 内核有 `printk()`，它是相似的。

与普通函数不同，系统调用不是通过它们的名称调用的。相反，有一个系统调用表。我们需要在表中创建一个条目，并在头文件中使系统调用的声明可见。表项位于文件

```
arch/x86/syscalls/syscall_64.tbl
```

在 Linux 3.6 中，该文件格式如下：

| Number | Type | Name |
| :--- | :--- | :--- |
| 313 | common | set_dvflag |

系统调用号为 313。已经有 312 个系统调用了。函数名位于末尾。虽然系统调用是通过编号而不是名称调用的，但按照惯例会将调用封装在函数或宏内部。对于这个系统调用，封装函数或宏的名字将是 `set_dvflag`。通常的做法是去掉 `sys` 前缀来派生名称。

系统调用表是由内核准备并供处理器可用的函数指针表。实现系统调的函数必须在 `include/linux/syscalls.h` 中声明。对于系统调用号 313，声明为：

```c
asmlinkage long sys_set_dvflag(int flag);
```

内核现在可以设置函数指针表了。如果内核已构建并加载，¹⁰，我们可以如下调用第 313 号系统调用：

```c
#include <unistd.h>
#include <asm/unistd.h>
```

> ¹⁰ 关于构建和加载 Linux 内核的指南，请参阅 http://kernelnewbies.org/KernelBuild。这些说明在 Ubuntu Linux 上运行良好，但在 Fedora Linux 上无效。

# 第 5 章 线程与共享内存

```c
long y=syscall(__NR_set_dvflag, 100);
```
