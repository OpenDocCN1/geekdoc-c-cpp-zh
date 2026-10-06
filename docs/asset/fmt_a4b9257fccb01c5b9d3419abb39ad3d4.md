
gc: objects in each generation: 3 0 4477

gc: objects in permanent generation: 0

gc: done, 0 unreachable, 0 collectible.0008s elapsed

你使用 `gc.DEBUG_COLLECTABLE` 来发现项目何时被作为垃圾收集。当你将其与 `gc.DEBUG_SAVEALL` 调试标志结合时，它们在被收集后会被移动到列表 `gc.garbage` 中：

```
>>> import gc
>>> gc.set_debug(gc.DEBUG_COLLECTABLE | gc.DEBUG_SAVEALL)
>>> z = [0, 1, 2, 3]
>>> z.append(del)
>>> del z
>>> gc.collect()
gc: collectable <list 0x10d594a00>
>>> gc.garbage
[[0, 1, 2, 3, [...]]]
```

你可以通过调用 `get_threshold()` 获取垃圾回收器运行的阈值：

```
>>> gc.get_threshold()
(700, 10, 10)
```

你还可以获取当前的阈值计数：

```
>>> gc.get_count()
(688, 1, 1)
```

最后，你可以手动为某代运行收集算法，它将返回收集的总数：

```
>>> gc.collect(0)
24
```

如果你不指定代，它将默认为 2，这会合并第 0 代和第 1 代：

```
>>> gc.collect()
20
```

## 结论

在本章中，你已经了解了 CPython 如何分配、管理和释放内存。即使是最简单的 Python 脚本，这些操作在生命周期内也会发生数千次。CPython 内存管理系统的可靠性和可扩展性使其能够从几行的脚本一直扩展到世界上最大的网站之一。

在本章中展示的对象分配和原始内存分配系统在开发 C 扩展模块时非常有用。C 扩展模块需要对 CPython 的内存管理系统有深入了解。即使缺少一个 `Py_INCREF` 也会导致内存泄漏或系统崩溃。

在处理纯 Python 代码时，如果你正在设计长时间运行的代码，GC 的知识是有用的。例如，如果你设计了一个运行数小时、几天甚至更久的函数，该函数需要在其执行的系统限制内仔细管理其内存。你可以使用本章中学到的技术来控制和调整 GC 代，以更好地优化你的代码及其内存占用。

# 并行与并发

第一批计算机被设计为一次只一件事。它们的大部分工作在计算数学领域。随着时间的推移，计算机需要处理来自各种来源的输入。有些输入来自遥远的星系。其结果是计算机应用程序花费大量时间空等响应。无论响应是来自总线、内存、计算、API 还是远程资源。

计算的另一个进展是操作系统从单用户终端转向多任务操作系统。应用程序需要在后台运行，以监听并响应网络以及处理如鼠标光标之类的输入。在现代多核 CPU 出现之前就需要多任务，因此操作系统长期就能处理多个进程。任何操作系统的核心都是进程注册表。操作系统提供了一种处理多个进程的方法：

## 并发模型

| 方法 | 模块 | 并发 | 并行 |
|---|---|---|---|
| 线程 | `threading` | 是 | 否 |
| 多进程 | `multiprocessing` | 是 | 是 |
| 异步 | `asyncio` | 是 | 否 |
| 子解释器 | `subinterpreters` | 是 | 是 |

## 进程结构

操作系统的任务之一是控制运行的进程。这些进程可以是浏览器或 IDE 等 UI 应用程序。

当进程执行时，你计算机上的 CPU 还会保留额外数据，例如：

- 寄存器：持有当前正在执行的指令或进程该指令所需的任何其他数据
- 指令指针 `Instruction Pointer` 或程序计数器 `Program Counter`：指示程序序列中执行的是哪条指令

IPython 进程由编译后的 IPython 解释器和编译后的模块组成。这些模块在运行时加载，并由 IPython 评估循环转换为指令：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_230_0.png)

程序寄存器和程序计数器指向进程中的单条指令。这意味着在任何时刻只有一条指令在执行。

对于 CPython 来说，这意味着在任何时刻只有有一条 Python 字节码指令在执行。

允许进程中并行执行指令主要有两种方法：

1. 派生 `Fork` 另一个进程
2. 派生 `Spawn` 一个线程

## 多进程并行

POSIX 系统提供了一个 API，允许任何进程 `fork` 派生一个子进程。

派生进程是对操作系统的低级 API，任何运行中的进程都可以调用。

当进行此调用时，操作系统会克隆当前运行进程的所有属性并创建一个新进程。

该克隆操作包含了父进程的堆、寄存器和计数器位置。子进程可以在派生时从父进程读取任何变量。

### 在 POSIX 中派生进程

作为一个例子，以在 C 语言动态内存分配开始时使用的“华氏度转摄氏度”应用程序为例。将其修改为为每个华氏度值派生一个子进程，而不是按顺序计算。

这是通过使用 `fork()` 函数实现的。每个子进程将从该点继续运行：

`python-book-samples ▸ 33 ▸▸ thread_celcius.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
static const double five_ninths = 5.0/9.0;
double celsius(double fahrenheit){
    return (fahrenheit - 32) * five_ninths;
}
int main(int argc, char** argv) {
    if (argc != 2) {
        return -1;
    }
    int number = atoi(argv[1]);
    for (int i = 1; i <= number; i++) {
        double f_value = 100 + (i*10);
        pid_t child = fork();
        if (child == 0) { // 是子进程
            double c_value = celsius(f_value);
            printf("%f F %f C (pid %d)\n", f_value, c_value, getpid());
            exit(0);
        }
    }
    printf("Spawned %d processes from %d\n", number, getpid());
    return 0;
}
```

在命令行运行此程序将得到类似下面的输出：

```
$ ./thread_celcius 4
110.000000 F is 43.333333 C (pid 57179)
120.000000 F is 48.888889 C (pid 57180)
Spawned 4 processes from 57178
130.000000 F is 54.444444 C (pid 57181)
140.000000 F is 60.000000 C (pid 57182)
```

## Windows 中的多进程

到为止，你一直在阅读 POSIX 模型。Windows 不提供 `fork()` 的等效方法，Python 应尽可能在 Linux、macOS 和 Windows 上拥有相同的 API。为了解决这个问题，使用了 `CreateProcess()` API 来派生另一个 `python.exe` 进程并带有 `-c` 命令行参数。

这一步骤被称为派生 `spawning` 进程，并且在 POSIX 上也可用。你将在本章中看到它的引用。

## multiprocessing 包

CPython 在操作系统进程 API 之上提供了一个 API。该 API 使在 Python 中创建多进程并行变得简单。

该 API 从 `multiprocessing` 包可用。该包提供了进程池、队列、派生、创建共享内存、连接进程等强大功能。

## 相关源文件

| 文件 | 目的 |
| --- | --- |
| `Lib/multiprocessing` | `multiprocessing` 包的 Python 源码 |
| `Modules/_posixsubprocess.c` | 封装 POSIX `fork()` 系统调用的 C 扩展模块 |
| `Modules/_winapi.c` | 封装 Windows API 的 C 扩展模块 |
| `PC/msvcmodule.c` | Microsoft Visual C Library 使用的 C 扩展模块 |

## 派生与 fork

`multiprocessing` 包提供了三种启动新进程的方法。

1. 派生解释器 `fork` 在 POSIX 上
2. 派生一个新的解释器 `spawn` 在 POSIX 和 Windows 上
3. 运行 Fork 服务器，其中创建一个新进程然后派生任意数量的进程 仅限 POSIX

> 注意
> 对于 Windows 和 macOS，默认启动方法是 `Spawning`。对于 Linux，默认是 `Forking`。你可以使用 `multiprocessing.set_start_method()` 函数覆盖默认方法。

每个进程都有显著的开销，池 `Pool` 会将池中的每个进程视为“工作线程”。如果一个工作线程完成了任务，它将被重用。如果你将该行：

```python
with mp.Pool(4) as pool:
```

替换为：

```python
with mp.Pool(4, maasksperchild=1) as pool:
```

之前的多进程示例将打印类似以下的内容：

```
$ python pool_process_celcius.py
110F is 43.333333333333336C (pid 5654)
120F is 48.88888888888889C (pid 5653)
130F is 54.44444444444444C (pid 5652)
140F is 60.0C (pid 5655)
```

输出显示了新生成的进程的进程 ID `pid` 以及计算出的值。

## 子进程的创建

这两个脚本都会创建一个新的 Python 解释器进程，并使用 `pickle` 向其传递数据。

| 说明 |
| :--- |
| `pickle` 模块是一个用于 Python 对象的序列化包。Davide Mastromatte 在 realpy.com 上写了一篇关于 `pickle` 模块的精彩文章。 |

对于 POSIX 系统，`multiprocessing` 模块创建子进程等同于此命令：
