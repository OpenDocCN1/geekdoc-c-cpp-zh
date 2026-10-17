
# 代码测试、调试与优化

## 前言

代码写完以后往往要做测试（或验证）、调试，可能还要优化。

### 关于测试（或验证）

通常对应着两个英文单词 `Verification` 和 `Validation`，在资料 [[1]](http://satc.gsfc.nasa.gov/assure/agbsec5.txt) 中有关于这个的定义和一些深入的讨论，在资料 [[2]](http://www.faqs.org/qa/qa-9060.html) 中，很多人给出了自己的看法。但是正如资料 [[2]](http://www.faqs.org/qa/qa-9060.html) 提到的：

> The differences between verification and validation are unimportant except to the theorist; practitioners use the term V&V to refer to all of the activities that are aimed at making sure the software will function as required.

所以，无论测试（或验证）目的都是为了让软件的功能能够达到需求。测试和验证通常会通过一些形式化（貌似可以简单地认为有数学根据的）或者非形式化的方法去验证程序的功能是否达到要求。

### 关于调试

而调试对应英文`debug`，`debug`叫“驱除害虫”，也许一个软件的功能达到了要求，但是可能会在测试或者是正常运行时出现异常，因此需要处理它们。

### 关于优化

`debug`是为了保证程序的正确性，之后就需要考虑程序的执行效率，对于存储资源受限的嵌入式系统，程序的大小也可能是优化的对象。

很多理论性的东西实在没有研究过，暂且不说吧。这里只是想把一些需要动手实践的东西先且记录和总结一下，另外很多工具在这里都有提到和罗列，包括 Linux 内核调试相关的方法和工具。关于更详细更深入的内容还是建议直接看后面的参考资料为妙。

下面的所有演示在如下环境下进行：

```cpp
$ uname -a
Linux falcon 2.6.22-14-generic #1 SMP Tue Feb 12 07:42:25 UTC 2008 i686 GNU/Linux
$ echo $SHELL
/bin/bash
$ /bin/bash --version | grep bash
GNU bash, version 3.2.25(1)-release (i486-pc-linux-gnu)
$ gcc --version | grep gcc
gcc (GCC) 4.1.3 20070929 (prerelease) (Ubuntu 4.1.2-16ubuntu2)
$ cat /proc/cpuinfo | grep "model name"
model name      : Intel(R) Pentium(R) 4 CPU 2.80GHz 
```

## 代码测试

代码测试有很多方面，例如运行时间、函数调用关系图、代码覆盖度、性能分析（Profiling）、内存访问越界（Segmentation Fault）、缓冲区溢出（Stack Smashing 合法地进行非法的内存访问？所以很危险）、内存泄露（Memory Leak）等。

### 测试程序的运行时间 time

`Shell`提供了内置命令`time`用于测试程序的执行时间，默认显示结果包括三部分：实际花费时间（real time）、用户空间花费时间（user time）和内核空间花费时间（kernel time）。

```cpp
$ time pstree 2>&1 >/dev/null

real    0m0.024s
user    0m0.008s
sys     0m0.004s 
```

`time`命令给出了程序本身的运行时间。这个测试原理非常简单，就是在程序运行（通过`system`函数执行）前后记录了系统时间（用`times`函数），然后进行求差就可以。如果程序运行时间很短，运行一次看不到效果，可以考虑采用测试纸片厚度的方法进行测试，类似把很多纸张叠到一起来测试纸张厚度一样，我们可以让程序运行很多次。

如果程序运行时间太长，执行效率很低，那么得考虑程序内部各个部分的执行情况，从而对代码进行可能的优化。具体可能会考虑到这两点：

对于 C 语言程序而言，一个比较宏观的层次性的轮廓（profile）是函数调用图、函数内部的条件分支构成的语句块，然后就是具体的语句。把握好这样一个轮廓后，就可以有针对性地去关注程序的各个部分，包括哪些函数、哪些分支、哪些语句最值得关注（执行次数越多越值得优化，术语叫 hotspots）。

对于 Linux 下的程序而言，程序运行时涉及到的代码会涵盖两个空间，即用户空间和内核空间。由于这两个空间涉及到地址空间的隔离，在测试或调试时，可能涉及到两个空间的工具。前者绝大多数是基于`Gcc`的特定参数和系统的`ptrace`调用，而后者往往实现为内核的补丁，它们在原理上可能类似，但实际操作时后者显然会更麻烦，不过如果你不去 hack 内核，那么往往无须关心后者。

### 函数调用关系图 calltree

`calltree`可以非常简单方便地反应一个项目的函数调用关系图，虽然诸如`gprof`这样的工具也能做到，不过如果仅仅要得到函数调用图，`calltree`应该是更好的选择。如果要产生图形化的输出可以使用它的`-dot`参数。从这里可以下载到它。

这里是一份基本用法演示结果：

```cpp
$ calltree -b -np -m *.c
main:
|   close
|   commitchanges
|   |   err
|   |   |   fprintf
|   |   ferr
|   |   ftruncate
|   |   lseek
|   |   write
|   ferr
|   getmemorysize
|   modifyheaders
|   open
|   printf
|   readelfheader
|   |   err
|   |   |   fprintf
|   |   ferr
|   |   read
|   readphdrtable
|   |   err
|   |   |   fprintf
|   |   ferr
|   |   malloc
|   |   read
|   truncatezeros
|   |   err
|   |   |   fprintf
|   |   ferr
|   |   lseek
|   |   read$ 
```

这样一份结果对于“反向工程”应该会很有帮助，它能够呈现一个程序的大体结构，对于阅读和分析源代码来说是一个非常好的选择。虽然`cscope`和`ctags`也能够提供一个函数调用的“即时”（在编辑 Vim 的过程中进行调用）视图（view），但是`calltree`却给了我们一个宏观的视图。

不过这样一个视图只涉及到用户空间的函数，如果想进一步给出内核空间的宏观视图，那么`strace`，`KFT`或者`Ftrace`就可以发挥它们的作用。另外，该视图也没有给出库中的函数，如果要跟踪呢？需要`ltrace`工具。

另外发现`calltree`仅仅给出了一个程序的函数调用视图，而没有告诉我们各个函数的执行次数等情况。如果要关注这些呢？我们有`gprof`。

### 性能测试工具 gprof & kprof

参考资料[[3]](http://www.linuxjournal.com/article/6758)详细介绍了这个工具的用法，这里仅挑选其中一个例子来演示。`gprof`是一个命令行的工具，而 KDE 桌面环境下的`kprof`则给出了图形化的输出，这里仅演示前者。

首先来看一段代码（来自资料[[3]](http://www.linuxjournal.com/article/6758)），算`Fibonacci`数列的，

```cpp
#include <stdio.h>

int fibonacci(int n);

int main (int argc, char **argv)
{
    int fib;
    int n;

    for (n = 0; n <= 42; n++) {
        fib = fibonacci(n);
        printf("fibonnaci(%d) = %d\n", n, fib);
    }

    return 0;
}

int fibonacci(int n)
{
    int fib;

    if (n <= 0) {
        fib = 0;
    } else if (n == 1) {
        fib = 1;
    } else {
        fib = fibonacci(n -1) + fibonacci(n - 2);
    }

    return fib;
} 
```

通过`calltree`看看这段代码的视图，

```cpp
$ calltree -b -np -m *.c
main:
|   fibonacci
|   |   fibonacci ....
|   printf 
```

可以看出程序主要涉及到一个`fibonacci`函数，这个函数递归调用自己。为了能够使用`gprof`，需要编译时加上`-pg`选项，让`Gcc`加入相应的调试信息以便`gprof`能够产生函数执行情况的报告。

```cpp
$ gcc -pg -o fib fib.c
$ ls
fib  fib.c 
```

运行程序并查看执行时间，

```cpp
$ time ./fib
fibonnaci(0) = 0
fibonnaci(1) = 1
fibonnaci(2) = 1
fibonnaci(3) = 2
...
fibonnaci(41) = 165580141
fibonnaci(42) = 267914296

real    1m25.746s
user    1m9.952s
sys     0m0.072s
$ ls
fib  fib.c  gmon.out 
```

上面仅仅选取了部分执行结果，程序运行了 1 分多钟，代码运行以后产生了一个`gmon.out`文件，这个文件可以用于`gprof`产生一个相关的性能报告。

```cpp
$ gprof  -b ./fib gmon.out 
Flat profile:

Each sample counts as 0.01 seconds.
  %   cumulative   self              self     total           
 time   seconds   seconds    calls  ms/call  ms/call  name    
 96.04     14.31    14.31       43   332.80   332.80  fibonacci
  4.59     14.99     0.68                             main

                        Call graph

granularity: each sample hit covers 2 byte(s) for 0.07% of 14.99 seconds

index % time    self  children    called     name
                                                 <spontaneous>
[1]    100.0    0.68   14.31                 main [1]
               14.31    0.00      43/43          fibonacci [2]
-----------------------------------------------
                             2269806252             fibonacci [2]
               14.31    0.00      43/43          main [1]
[2]     95.4   14.31    0.00      43+2269806252 fibonacci [2]
                             2269806252             fibonacci [2]
-----------------------------------------------

Index by function name

   [2] fibonacci               [1] main 
```

从这份结果中可观察到程序中每个函数的执行次数等情况，从而找出值得修改的函数。在对某些部分修改之后，可以再次比较程序运行时间，查看优化结果。另外，这份结果还包含一个特别有用的东西，那就是程序的动态函数调用情况，即程序运行过程中实际执行过的函数，这和`calltree`产生的静态调用树有所不同，它能够反应程序在该次执行过程中的函数调用情况。而如果想反应程序运行的某一时刻调用过的函数，可以考虑采用`gdb`的`backtrace`命令。

类似测试纸片厚度的方法，`gprof`也提供了一个统计选项，用于对程序的多次运行结果进行统计。另外，`gprof`有一个 KDE 下图形化接口`kprof`，这两部分请参考资料[[3]](http://www.linuxjournal.com/article/6758)。

对于非 KDE 环境，可以使用 [Gprof2Dot](https://code.google.com/p/jrfonseca/wiki/Gprof2Dot) 把`gprof`输出转换成图形化结果。

关于`dot`格式的输出，也可以可以考虑通过`dot`命令把结果转成`jpg`等格式，例如：

```cpp
$ dot -Tjpg test.dot -o test.jp 
```

`gprof`虽然给出了函数级别的执行情况，但是如果想关心具体哪些条件分支被执行到，哪些语句没有被执行，该怎么办？

### 代码覆盖率测试 gcov & ggcov

如果要使用`gcov`，在编译时需要加上这两个选项`-fprofile-arcs -ftest-coverage`，这里直接用之前的`fib.c`做演示。

```cpp
$ ls
fib.c
$ gcc -fprofile-arcs -ftest-coverage -o fib fib.c
$ ls
fib  fib.c  fib.gcno 
```

运行程序，并通过`gcov`分析代码的覆盖度：

```cpp
$ ./fib
$ gcov fib.c
File 'fib.c'
Lines executed:100.00% of 12
fib.c:creating 'fib.c.gcov' 
```

12 行代码 100% 被执行到，再查看分支情况，

```cpp
$ gcov -b fib.c
File 'fib.c'
Lines executed:100.00% of 12
Branches executed:100.00% of 6
Taken at least once:100.00% of 6
Calls executed:100.00% of 4
fib.c:creating 'fib.c.gcov' 
```

发现所有函数，条件分支和语句都被执行到，说明代码的覆盖率很高，不过资料[[3]](http://www.linuxjournal.com/article/6758) `gprof`的演示显示代码的覆盖率高并不一定说明代码的性能就好，因为那些被覆盖到的代码可能能够被优化成性能更高的代码。那到底哪些代码值得被优化呢？执行次数最多的，另外，有些分支虽然都覆盖到了，但是这个分支的位置可能并不是理想的，如果一个分支的内容被执行的次数很多，那么把它作为最后一个分支的话就会浪费很多不必要的比较时间。因此，通过覆盖率测试，可以尝试着剔除那些从未执行过的代码或者把那些执行次数较多的分支移动到较早的条件分支里头。通过性能测试，可以找出那些值得优化的函数、分支或者是语句。

如果使用`-fprofile-arcs -ftest-coverage`参数编译完代码，可以接着用`-fbranch-probabilities`参数对代码进行编译，这样，编译器就可以对根据代码的分支测试情况进行优化。

## 参考资料

- [1] [Verification and Validation](http://satc.gsfc.nasa.gov/assure/agbsec5.txt)
- [2] [Verification vs Validation](http://www.faqs.org/qa/qa-9060.html)
- [3] [Using GNU profiler gprof](http://www.linuxjournal.com/article/6758)
- [Gprof2Dot](https://code.google.com/p/jrfonseca/wiki/Gprof2Dot)



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



```cpp
$ ald test
ald> display
Address 0x8048054 added to step display list
ald> n
eax = 0x00000000 ebx = 0x00000000 ecx = 0x00000001 edx = 0x00000000 
esp = 0xBFBFDEB4 ebp = 0x00000000 esi = 0x00000000 edi = 0x00000000 
ds  = 0x007B es  = 0x007B fs  = 0x0000 gs  = 0x0000 
ss  = 0x007B cs  = 0x0073 eip = 0x08048055 eflags = 0x00200292 

Flags: AF SF IF ID 

Dumping 64 bytes of memory starting at 0x08048054 in hex
08048054:  59 59 59 C6 41 0C 0A 31 D2 B2 0D 31 C0 B0 04 31    YYY.A..1...1...1
08048064:  DB CD 80 31 C0 40 CD 80 00 2E 73 79 6D 74 61 62    ...1.@....symtab
08048074:  00 2E 73 74 72 74 61 62 00 2E 73 68 73 74 72 74    ..strtab..shstrt
08048084:  61 62 00 2E 74 65 78 74 00 00 00 00 00 00 00 00    ab..text........

08048055                      59                   pop ecx 
```

可见 `ald` 在启动时就已经运行了被它调试的 `test` 程序，并且进入了程序的入口 `0x8048054`，紧接着单步执行时，就执行了程序的第一条指令 `popl ecx`。

`ald` 的命令很少，而且跟 `gdb` 很类似，比如这个几个命令用法和名字都类似 `help,next,continue,set args,break,file,quit,disassemble,enable,disable` 等。名字不太一样但功能对等的有：`examine` 对 `x`, `enter` 对 `set variable {int} 地址=数据`。

需要提到的是：Linux 下的调试器包括上面的 `gdb` 和 `ald`，以及 `strace` 等都用到了 Linux 系统提供的 `ptrace()` 系统调用，这个调用为用户访问内存映像提供了便利，如果想自己写一个调试器或者想 hack 一下 `gdb` 和 `ald`，那么好好阅读资料[12](http://linuxgazette.net/issue81/sandeep.html)和 `man ptrace` 吧。

如果确实需要用 `gdb` 调试汇编，可以参考：

*   [Linux Assembly "Hello World" Tutorial, CS 200](http://web.cecs.pdx.edu/~bjorn/CS200/linux_tutorial/)
*   [Debugging your Alpha Assembly Programs using GDB](http://lab46.corning-cc.edu/Documentation-Assembly_GDB_Debugger.php)

### 实时调试：`gdb` tracepoint

对于程序状态受时间影响的程序，用上述普通的设置断点的交互式调试方法并不合适，因为这种方式将由于交互时产生的通信延迟和用户输入命令的时延而完全改变程序的行为。所以 `gdb` 提出了一种方法以便预先设置断点以及在断点处需要获取的程序状态，从而让调试器自动执行断点处的动作，获取程序的状态，从而避免在断点处出现人机交互产生时延改变程序的行为。

这种方法叫 `tracepoints`（对应 `breakpoint`），它在 `gdb` 的用户手册里头有详细的说明，见 [Tracepoints](https://sourceware.org/gdb/onlinedocs/gdb/Tracepoints.html)。

在内核中，有实现了相应的支持，叫 [KGTP](http://lwn.net/Articles/538818/)。

### 调试内核

虽然这里并不会演示如何去 hack 内核，但是相关的工具还是需要简单提到的，[这个资料](http://elinux.org/images/c/c6/Tools_slides.pdf)列出了绝大部分用于内核调试的工具，这些对你 hack 内核应该会有帮助的。

## 代码优化

这部分暂时没有准备足够的素材，有待进一步完善。

暂且先提到两个比较重要的工具，一个是 `Oprofile`，另外一个是 `Perf`。

实际上呢？“代码测试”部分介绍的很多工具是为代码优化服务的，更多具体的细节请参考后续资料，自己做实验吧。

## 参考资料

*   [VERIFICATION AND VALIDATION](http://satc.gsfc.nasa.gov/assure/agbsec5.txt)
*   [difference between verification and Validation](http://www.faqs.org/qa/qa-9060.html)
*   [Coverage Measurement and Profiling(覆盖度测量和性能测试,Gcov and Gprof)](http://www.linuxjournal.com/article/6758)
*   Valgrind Usage
    *   [Valgrind HOWTO](http://www.faqs.org/docs/Linux-HOWTO/Valgrind-HOWTO.html)
    *   [Using Valgrind to Find Memory Leaks and Invalid Memory Use](http://www.cprogramming.com/debugging/valgrind.html)
*   [MEMWATCH](http://www.linkdata.se/sourcecode.html)
*   [Mastering Linux debugging techniques](http://www.ibm.com/developerworks/linux/library/l-debug/)
*   [Software Performance Analysis](http://arxiv.org/pdf/cs.PF/0507073.pdf)
*   [Runtime debugging in embedded systems](http://dslab.lzu.edu.cn/docs/publications/runtime_debug.pdf)
*   [绕过 libsafe 的保护--覆盖 _dl_lookup_versioned_symbol 技术](http://www.xfocus.net/articles/200208/423.html)
*   [介绍 Propolice 怎样保护 stack-smashing 的攻击](http://www.xfocus.net/articles/200103/78.html)
*   Tools Provided by System：`ltrace`,`mtrace`,`strace`
*   [Process Tracing Using Ptrace](http://linuxgazette.net/issue81/sandeep.html)
*   Kernel Debugging Related Tools：`KGDB`, `KGOV`, `KFI/KFT/Ftrace`, `GDB Tracepoint`，`UML`, `kdb`
*   用 Graphviz 可视化函数调用
*   [Linux 段错误详解](http://www.tinylab.org/explor-linux-segmentation-fault/)
*   源码分析之函数调用关系绘制系列
    *   [源码分析：静态分析 C 程序函数调用关系图](http://www.tinylab.org/callgraph-draw-the-calltree-of-c-functions/)
    *   [源码分析：动态分析 C 程序函数调用关系](http://www.tinylab.org/source-code-analysis-gprof2dot-draw-a-runtime-function-calls-the-c-program/)
    *   [源码分析：动态分析 Linux 内核函数调用关系](http://www.tinylab.org/source-code-analysis-dynamic-analysis-of-linux-kernel-function-calls/)
    *   [源码分析：函数调用关系绘制方法与逆向建模](http://www.tinylab.org/source-code-analysis-how-best-to-draw-a-function-call/)
*   Linux 下缓冲区溢出攻击的原理及对策
*   Linux 汇编语言开发指南
*   缓冲区溢出与注入分析(第一部分：进程的内存映像)
*   Optimizing C Code
*   Performance programming for scientific computing
*   Performance Programming
*   Linux Profiling and Optimization
*   High-level code optimization
*   Code Optimization
