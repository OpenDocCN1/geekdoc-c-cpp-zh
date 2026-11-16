

各种代码技术以及在不同系统上执行一些有用的基准测试。我们将在后面展示基准测试的结果。

清单 7.1 完整展示了我们的多线程基准测试应用程序。请注意，它也包含在 CD-ROM 中。

### 清单 7.1.1 多线程基准测试应用程序

```
#include <iostream>
#include <process.h>
#include <windows.h>
#include <conio.h>

using namespace std;

#pragma pack(push,4)
__int64 g_total_val = 0;
int g_num_calculations = 0;
bool g_do_floating_point = false;
CRITICAL_SECTION g_val_update;

// Perform some nonsense calculations to burn up CPU cycles
void DoCalculations()
{
    int val = 0;
    if(g_do_floating_point)
    {
        for(int i = 0; i < g_num_calculations; i++)
        {
            for(int j = 0; j < 1000000; j++)
            {
                val += int((float)i * (float)j *
                    (float)j * (float)j - 0.25f) /
                    (val + i + j + 1));
            }
        }
        EnterCriticalSection(&g_val_update);
        g_total_val += val;
        LeaveCriticalSection(&g_val_update);
    }
    else
    {
        for(int i = 0; i < g_num_calculations; i++)
        {
            for(int j = 0; j < 1000000; j++)
            {
                val += i * j * (j - i) /
                    (val + i + j + 1);
            }
        }
    }
}

// This function is passed to CreateThread()
void ThreadFunction(LPVOID lpv)
{
    HANDLE hEvent = (HANDLE)lpv;
    DoCalculations();
    SetEvent(hEvent);
}

// Start the threaded timing tests
int main()
{
    char c;
    cout << "Do floating-point calculations (y/n)? ";
    cin >> c;
    if(c == 'y')
        g_do_floating_point = true;

    int threads = 0;
    cout << "How many total threads do you wish "
         << " to create (including the main thread)? ";
    cin >> threads;

    // Allocate an array of handles if we have
    // more than one thread
    HANDLE* phHandles = 0;
    if(threads > 1)
    {
        phHandles = new HANDLE[threads - 1];
    }

    cout << "How many millions of calculation loops "
         << " should each thread perform? ";
    cin >> g_num_calculations;
    cout << "Now performing timing calculations...";

    InitializeCriticalSection(&g_val_update);

    // Get the start time
    unsigned int start_time = timeGetTime();

    // Perform all actual calculations -
    // one per thread.
    int i;
    if(threads > 1)
    {
        for(i = 0; i < threads - 1; i++)
        {
            phHandles[i] = CreateEvent(
                NULL, FALSE, FALSE, NULL);
            if(_beginthread(&ThreadFunction, 4096,
                phHandles[i]) == -1)
                return -1;
        }
        DoCalculations();
        // Wait for all other threads to finish
        // before continuing
        WaitForMultipleObjects(threads - 1,
            phHandles, TRUE, INFINITE);
    }
    else
    {
        // Do a simple set of calculations for the
        // single-threaded path
        DoCalculations();
    }

    // Get the end time
    unsigned int end_time = timeGetTime();

    // We no longer need this critical section
    DeleteCriticalSection(&g_val_update);

    // Close and delete handles used for synchronization
    if(threads > 1)
    {
        for(i = 0; i < threads - 1; i++)
        {
            CloseHandle(phHandles[i]);
        }
        delete[] phHandles;
    }

    cout << "Finished!" << endl;
    cout << "Performed all calculations in "
        << end_time - start_time << " milliseconds" << endl;
    getch();
    return 0;
}
#pragma pack(pop)
```

本质上，这是一个基于线程的小型基准测试程序，用于对分布在任意数量线程上的数学计算进行计时。程序会询问用户要运行哪种类型的算法（浮点或整数）、要运行多少个线程，以及每个线程要运行多少百万个计算周期。

为了模拟从线程到公共池的数据流，计算出的值会定期添加到名为 g_total_val 的全局变量中。这就是我们之前讨论过的至关重要的数据传输点。由于这是一个共享访问点，保护对该变量的访问至关重要。不过，不要被迷惑，因为我们并不对该变量做任何操作。它仅用于向你展示如何从线程访问公共/全局数据。让我们简要地浏览这段代码，看看我们如何管理线程，并讨论如何将这些技术应用于音频系统。

你首先会注意到的函数是 DoCalculations()。它在每百万次递增的循环中执行一系列计算，以进行有意义的计时测试。这些计算的结果存储在全局变量 g_total_val 中。由于这是一个全局变量，且可能同时被多个线程访问，我们必须先使用互斥锁来锁定对全局变量的访问，在完成访问后再解锁。编写多线程代码时，重要的是要尽量减少必须执行的锁定次数。例如，如果我们在每次迭代时都锁定和解锁全局变量，而不是每百万次迭代一次，那么由于线程在尝试访问该变量时发生冲突增加，导致线程停滞，多线程性能将下降。

DoCalculations() 函数被包装在一个名为 ThreadFunction() 的函数中，该函数以指向 void 指针的指针作为参数。这是新线程的入口点。当该函数退出时，线程会自行终止。

程序的其余部分乍看之下相当直观。程序会向用户询问几个问题，例如要执行哪种类型的计算以及要创建多少个计算线程。在获取所需信息后，程序会设置一个计时器，然后启动一个或多个线程，每个线程在 DoCalculations() 函数内执行一系列计算。计算的“结果”全部存储在全局变量 g_total_val 中。

这个示例项目演示了如何将任务拆分为可变数量的多个并发执行任务。我们将使用这个程序在几台不同的测试机器上进行一些简单的计时测试，以展示多线程在理想情况下如何提高效率。

对于这些测试，示例程序在两台测试机器上运行。机器一是一台运行 Windows XP Professional 的双 Xeon Pentium 4 2.4 GHz 机器。测试分别在开启和关闭 HyperThreading 的情况下进行，以展示不同的结果。机器二是一台 Pentium 4 1.5 GHz Windows 2000 Professional 机器，不具备 HyperThreading 功能且只有一个处理器。对于每种配置，我们都运行了展示整数计算和混合整数与浮点计算的测试。测试周期数（12 亿次）的选择是为了获得合理的执行时间。请记住，总时间远不如特定配置行中每个测试的相关执行时间重要。我们使用了一种相对原始的计时机制，因此总体执行计时误差大约为正负 20 毫秒。表 7.1.1 提供了结果。

### 表 7.1.1 示例程序测试结果

| 配置 | 1 个线程 | 2 个线程 | 3 个线程 | 4 个线程 | 5 个线程 | 6 个线程 |
|---|---|---|---|---|---|---|
| M1, HT, 整数 | 28078ms | 16625ms | 12172ms | 10125ms | 10438ms | 10516ms |
| M1, HT, 浮点 | 68719ms | 34843ms | 23500ms | 19813ms | 20672ms | 20578ms |
| M1, 无 HT, 整数 | 28063ms | 14047ms | 14062ms | 14046ms | 14141ms | 14078ms |
| M1, 无 HT, 浮点 | 68859ms | 34422ms | 29797ms | 27484ms | 26032ms | 25125ms |
| M2, 整数 | 43312ms | 43532ms | 43492ms | 43593ms | 44163ms | 43442ms |
| M2, 浮点 | 147323ms | 108246ms | 95247ms | 90059ms | 85943ms | 82418ms |

键= M1 = 机器 1，M2 = 机器 2，HT = 已启用 HyperThreading，无 HT = 已禁用 HyperThreading，整数 = 执行基于整数的计算，浮点 = 执行浮点和整数计算。

你可以看到，在双处理器机器上从一个线程切换到两个执行线程时，性能提升最为显著。这并不意外，因为两个线程可以在两个物理处理器上同时执行。唯一的效率损失来自同步两个线程的执行和数据收集。这就是为什么在理论上，在这种情况下你永远不应该看到 100% 的性能提升。

在考察 HyperThreading 带来的性能提升时（这意味着在启用了 HyperThreading 的双处理器机器上运行三个或四个线程），你可以看到大约 30% 的更适度但仍然显著的提升。这与 Intel 的研究相符，该研究指出在最佳情况下你可以期望获得多少提升。值得注意的一个更有趣的结果是，两台机器上的浮点测试在超过两个线程后仍然显示出性能改进的奇怪事实，即使人们在逻辑上可能期望相反的结果。虽然这些结果的确切原因不清楚，但可以推测，操作系统和处理器都是为执行多个线程而设计和优化的，因此在这种配置下表现得更加最优，即使是在多处理器机器上也是如此。这些结果主要通过混合浮点和整数计算实现的事实也可能起到一定作用。

最后，值得注意的是每个线程实际产生的开销有多大（或者更确切地说，有多小）——在我们的测试中，结果几乎可以忽略不计。要获得更准确的测量结果，你必须大幅增加线程数量或延长测试运行时间。在机器二上，由于它本质上是单处理器且没有 HyperThreading 技术，任何超过一个的线程数都必须由操作系统模拟。

从这些数字中我们可以推断出什么？在运行 Windows 操作系统的现代 PC 上，在单个处理器上运行多个任务非常高效，只要线程数量不过大即可。然而，在为并行执行设计的系统上，当并发执行且平衡的线程数等于处理器数量（无论是虚拟的（如 HyperThreading 的情况）还是物理的）时，我们可以看到显著的性能提升。如果任何游戏系统可以

