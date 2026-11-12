

```c
void debug_msg(char * str, const unsigned int error_level)
{
 if (error_level <= GLOBAL_ERROR_LEVEL)
 {
 if (error_level == 0)
 printf("\n**************%s", str, "**************\n");
 else
 printf("\n%s", str);

 fflush(stdout);

 if (error_level == 0)
 exit(0);
 }
}

#define DEBUG_MSG(x, level) debug_msg(x, level)
#else
#define DEBUG_MSG(x, level)
#endif
#endif
```

在此示例中，我们创建了五个级别的调试消息。当未使用软件的调试版本时，这些消息会以不导致编译错误的方式从可执行文件中剥离。

```c
#define DEBUG
#include "debug_msg.h"
unsigned int GLOBAL_ERROR_LEVEL = DEBUG_ERR_LVL_WARNING;

int main(int argc, char *argv[])
{
 DEBUG_MSG("Error from level four", DEBUG_ERR_LVL_INFO);
 DEBUG_MSG("Error from level three", DEBUG_ERR_LVL_WARNING);
 DEBUG_MSG("Error from level two", DEBUG_ERR_LVL_PROBLEM);
 DEBUG_MSG("Error from level one", DEBUG_ERR_LVL_SERIOUS);
 DEBUG_MSG("Error from level zero", DEBUG_ERR_LVL_CRITICAL);

 return 0;
}
```

要调用该函数，只需将宏放入代码中，如上一示例所示。这在主机代码中可以正常工作，但在设备代码中需要进行一些小修改才能工作。

首先，在内核中打印消息时，你需要了解一些问题。内核级 printf 仅支持计算能力 2.x。如果尝试在为计算 1.x 设备编译的内核中使用 printf，你会收到错误，称无法从全局或设备函数调用 printf。这并不完全正确——只是它不支持计算 1.x 设备，且目标架构必须是计算 2.x。

假设你拥有一个 Fermi 级别的计算设备，因此 `printf` 调用受支持。除非你特别注意避免，否则消息将由每个线程以每组 32 个（即 warp 大小）的方式打印。显然，由于你应该启动成千上万个线程，仅打印一条消息可能导致 10,000 多行滚出终端窗口顶部。由于 `printf` 缓冲区大小固定且会循环覆盖，你将丢失早期输出。

由于行也可以以任意顺序打印，如果没有时间参考来准确确认消息的来源时间，我们就不能将打印顺序视为执行顺序。因此，我们需要识别每条消息的来源并为其加上时间戳。

第一个问题很容易解决，只需让块或 warp 中的一个线程打印消息即可。按照惯例，这通常是线程 0。我们也可能希望从每个 warp 打印一条消息，因此同样只选择每个 warp 中的第一个线程来打印消息。你也可以有其他标准，例如计算光晕区域的线程等。下面展示了一组示例代码。

```c
if ( (blockIdx.x == some_block_id) && ((threadIdx.x % 32) == 0) )
{
    // Fetch raw clock value
    unsigned int clock2 = 0;
    asm("mov.u32 %0, %clock;" : "=r"(clock2));

    // Fetch the SM id
    unsigned int sm = 0;
    asm("mov.u32 %0, %smid ;" : "=r"(sm));

    printf("\nB:%05d, W:%02d, SM:%02u, CLK:%u", blockIdx.x, (threadIdx.x>>5), sm, clock2);
}
```

这只是查找指定的块 ID，并打印块 ID、warp 编号、正在执行的 SM 以及原始时钟值。

```
B:00007, W:05, SM:13, CLK:1844396538
B:00001, W:04, SM:05, CLK:1844387468
B:00002, W:09, SM:09, CLK:1844387438
B:00007, W:10, SM:13, CLK:1844396668
B:00002, W:06, SM:09, CLK:1844387312
B:00007, W:00, SM:13, CLK:1844396520
B:00005, W:12, SM:06, CLK:1844396640

B:00005, W:13, SM:02, CLK:24073638
B:00006, W:03, SM:04, CLK:24073536
B:00005, W:15, SM:02, CLK:24073642
B:00002, W:03, SM:05, CLK:24076530
B:00006, W:00, SM:04, CLK:24073572
B:00002, W:00, SM:05, CLK:24076570
```

![](img/e0b192dbaf05f61ad420bee512a8c4e4_568_0.png)

图 12.7 14 个 SM 的 warp 使用情况 (GTX470)。

在这里，我们打印块索引、warp ID、warp 正在执行的 SM 以及原始时钟值。你可以简单地将此输出重定向到文件，然后绘制散点图。由于我们选择将设备 `printf` 放在内核开头，因此它显示每个内核何时被调用。

在图 12.7 中，垂直轴显示 SM，水平轴显示绝对时钟时间。我们可以看到所有 SM 大约在同一时间启动，除了少数稍晚启动的 SM，它们又是一起启动的。然后我们看到时间戳的大部分是随机分布的，因为每个块在执行开始时打印其详细信息。分布完全取决于你执行的程序以及外部资源可用所需的时间，全局内存是主要示例。

使用多个 GPU 或多个流时，我们还面临消息来源标识的问题。这同样可以通过在消息前加上唯一标识符来简单处理。在几个示例中，我们使用从设备 ID 字符串创建的字符串 `device_prefix` 来在使用多个 GPU 时做到这一点。但是，提取此信息的 API 是主机端调用，而不是设备端调用。这是有道理的，因为我们不希望 30,000 个线程各自获取设备 ID 字符串，因为对它们所有人来说都是相同的。因此，我们可以通过全局内存或常量内存提供此主机端信息。如果只有一个 GPU 和一个流，则不需要这样做，但任何非平凡的程序在可用时都将同时使用流和多个 GPU。

在多个 GPU 的情况下，你会看到时钟值有明显变化。因此，很容易看出输出流来自不同设备，但哪个来自设备 0、1、2 或 3？对于相同的设备，我们无法判断。如果这些消息来自同一设备上的不同流，又该如何？

使用绝对 TID（线程 ID）值足以标识单 GPU 内核的消息。但是，当使用多个流和/或多个设备时，需要设备号、TID 和流号的组合。

排序问题仅在查看输出时才是一个问题。你应该创建以下形式的前缀：

```
GPU ID : Stream ID : TID : Message
```

使用此前缀，可以将输出重定向到文件，并使用保持相对顺序的排序进行简单排序。然后我们会得到每个 GPU 和流的所有消息，按顺序排列。

请注意，虽然 `printf` 是在主机端显示信息的简便方法，但要意识到它会在 GPU 内存中创建一个 1 MB 缓冲区，并在某些事件发生时将该缓冲区传回主机。

因此，`printf` 输出仅在以下情况下可见：

- 1. 在随后的内核启动开始时。
- 2. 在内核执行结束时，如果设置了环境变量 `CUDA_LAUNCH_BLOCKING`（如果使用多个 GPU 或流，则不推荐）。
- 3. 作为主机端发起的同步点的结果，例如同步设备、流或事件。
- 4. `cudaMemcpy` 的阻塞操作。
- 5. 程序员发起的设备重置（`cudaDeviceReset` 或驱动程序 `cuCtxDestroy` API 调用）。

因此，在大多数情况下，你会看到打印的输出。如果没有，只需在退出主机程序之前调用 `cudaDeviceReset`，或在流的一组工作结束时调用 `cudaStreamSynchronize`，缺失的输出应该就会出现。

如果需要更大的缓冲区，可以使用 `cudaDeviceSetLimit (cudaLimitPrintfFifoSize, new_size_in_bytes)` API 调用进行设置。

## 版本控制

版本控制是任何专业软件开发的关键方面。它不需要使用非常昂贵的工具或涵盖谁可以更新什么的庞大流程。在大型项目中，版本控制绝对是必不可少的。但是，即使对于单开发者项目（这可能适用于许多读者），它也很重要。

试想一下，调试一个 30,000 线程的程序很容易。如果你对这个说法嗤之以鼻，那么你就意识到，不为你的程序进行版本控制（无论是定期还是在达到主要里程碑时），你给自己设定了多么艰巨的任务。程序员通常是一群相当自信的人，并且可以确信一开始的“简单”更改将不会出问题。然而，当事情不如计划进行时，准确记住你所做的更改集合可能很困难。如果没有程序的可用备份，要回到更改前的完全可用版本可能很困难，甚至几乎不可能。

职业世界中的大多数程序都是由团队开发的。同事可以提供一双新的眼睛来查看问题，这非常有帮助。如果你有可用代码的版本化或基线副本，那么查看差异并找出当前破坏先前可用解决方案的内容就相对容易了。如果没有这些定期基线，就不容易识别错误可能出现的位置，因此你可能不需要查看几百行代码，而是几千行。

## 为未来 GPU 开发

### Kepler

NVIDIA 从 Fermi 及后续版本呈现的路线图是 Kepler GK104 (K10)、Kepler GK110 (K20) 和 Maxwell。截至 2012 年 3 月，第一个 Kepler 版本 GK104 已发布。该产品面向消费市场，缺少一些

