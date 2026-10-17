
# 13.2
某些并行处理器将用户在一个程序中可以创建的进程数限制为可用处理器数减一。你认为为什么会做出这种限制？这种限制在 SIMD 系统或 MIMD 系统上更有可能吗？是否有创建比处理器更多的进程的理由？解释。

# 13.3
可以在少于 `n` 步内计算 `n` 个整数的和。描述如何使用 `k` 个处理器来完成此操作，其中 `k < n`。拥有 `k > n` 是否有任何优势？

# 13.4
文本提到矩阵乘法可以使用 `n²` 个处理器在 `n` 步内完成。能否使用更多处理器在更少的步骤中完成？

# 13.5
描述 SPMD 和 MPMD 编程之间的区别。你会将图 13.3 的程序描述为 SPMD 还是 MPMD？为什么？

# 13.6
在章节讨论中，为什么我们使用术语“MPMD”而不是“fork-join”？

# 13.7
解释为什么大粒度和小粒度并行可能比中等粒度效率更低。提供编程示例来支持你的论点。

# 13.8
图 13.4 的 C 代码假设 `NUMPROCS` 小于 `SIZE`。如果 `NUMPROCS > SIZE` 会发生什么？重写图 13.4 的代码以利用额外的处理器，如果 `NUMPROCS > SIZE`。

# 13.9
解释以下 UNIX 管道中每一步发生的情况：

```
cat *_java | tr -sc A-Za-z '\\012' | sort | uniq -c | sort -rn
```

# 13.10
Microsoft Windows 版本中的命令行窗口也允许某些命令进行管道传输，例如 `dir | more`。确定这些管道是否是 UNIX 意义上的真正管道（即管道中的每个程序都是一个单独的进程，且没有中间文件保存到磁盘）。

# 13.11
一个典型的进程同步问题是资源分配问题。例如，如果系统有三台打印机，则最多有三个进程可以同时安排打印。编写一个程序来分配三台打印机给进程

## (a) Java

## (b) Ada95

## (c) Ada83

# 13.12
一个用于测试并发语言机制的标准问题（像有界缓冲区问题）是读者-写者问题。在此问题中，存储的数据会不断被多个进程读取和更新。对此问题的解决方案必须允许任意数量的读者访问数据，但一次只能允许一个写者。编写此问题的解决方案，使用 (a) Java；(b) Ada tasks。

# 13.13
Java 规范承诺获取除 `long` 或 `double` 之外的任何内置类型的单个变量的值，或更新此类变量是一个原子操作，但对 `long` 或 `double` 变量的此类操作可能不是原子的。

## (a) 解释这种差异的原因。

## (b) 这一事实如何影响有界缓冲区问题代码（图 13.6）？

## (c) 这一事实对读者-写者问题的解决方案有任何影响吗？解释。

# 13.14
另一个标准并发问题是 Dijkstra 的哲学家进餐问题。在此问题中，五位哲学家花费时间进食和思考。当哲学家准备进食时，她坐在桌子旁的五个位置之一，桌子上堆满了意大利面。不幸的是，只有五把叉子，每两盘之间一把，而哲学家需要两把叉子才能进食。哲学家会尝试拿起她旁边的两把叉子，如果成功，她会吃一段时间，离开桌子，然后回到思考。对于此问题，

## (a) 描述死锁和饥饿如何发生。

## (b) 为什么是五位哲学家而不是四位或三位？

## (c) 用 Java 或 Ada 编写一个无死锁的解决方案。

## (d) 在你对第 (c) 部分的解决方案中，能否保证没有饥饿？解释。

# 13.15
图 13.5 中矩阵乘法的 C 代码在典型的 UNIX 实现中不起作用，因为 `fork` 不会导致内存共享。此问题可通过使用文件解决，因为 `fork` 的进程继续共享文件。重写代码以使用文件正确计算矩阵 `c`。评论你解决方案的效率。

# 13.16
能否通过使用指针变量在多个进程之间共享数组的地址来纠正图 13.5？解释原因。

# 13.17
## (a) 用 Java 编写矩阵乘法问题的解决方案，使用一个线程处理答案的每一行和每一列。

## (b) 用 Java 编写矩阵乘法问题的解决方案，使用少于答案矩阵元素数量的固定数量的线程，其中每个线程寻找答案矩阵中尚未处理的下一个元素。

# 13.18
重复上一个练习，使用 Ada。

# 13.19
给定两个进程 `p` 和 `q`，以及一个初始化为 1 的信号量 `S`，假设 `p` 和 `q` 进行以下调用：

```
p: delay(S);
...
delay(S);
q: delay(S);
...
signal(S);
```

描述对于 `S` 的这些操作的所有可能顺序会发生什么。

# 13.20
描述忙等待实现的信号量如何导致饥饿。

# 13.21
除了死锁和饥饿之外，并发进程还可能经历活锁，其中没有进程被阻塞，所有进程都能执行，但每个进程不断重复相同的代码而无法成功。在 (a) Java 或 (b) Ada 中编写一个简单的程序作为活锁的示例。

# 13.22
这是信号量操作的替代代码：

```
Delay(S) : S := S − 1;
    if S < 0 then suspend the calling process;
Signal(S): S := S + 1;
    if S >= 0 then wake up a waiting process;
```

将其与第 13.4 节中的代码进行比较。行为上有任何差异吗？

# 13.23
将信号量初始化为负值有意义吗？为什么或为什么不？

# 13.24
有时语言只提供二进制信号量机制，其中存储的值是布尔值而不是整数。然后，`wait` 和 `signal` 操作变为

```
Delay(S) : if S = true then S := false
    else suspend the calling process
Signal(S): if processes are waiting then wake up a process
    else S := true;
```

（为了与二进制信号量区分，文本中描述的信号量有时称为计数信号量。）展示如何使用二进制信号量实现计数信号量。

# 13.25
有时锁与信号量区分开来，因为它是不可阻塞的：一次只有一个进程可以获取锁，但如果进程未能获取锁，它可以继续执行。假设锁 `L` 有两个操作，一个布尔函数 `lock-lock(L)`，如果锁已被获取则返回 true，否则返回 false，以及 `unlock-lock(L)`，它解锁锁（如果锁已解锁则无效果）。编写锁的实现：

## (a) Java

## (b) Ada

# 13.26
如果一个监视器入口调用另一个监视器入口，可能会导致死锁。

## (a) 构造一个示例来展示这种情况如何发生。

## (b) Java 如何处理这个问题？

## (c) Ada 呢？

# 13.27
假设图 13.7 中 Java 信号量实现的 `signal` 操作代码被改为：

```
public synchronized void signal(){
    notify();
    count++;
}
```

这会起作用吗？解释。

# 13.28
由于存在中断的可能性，图 13.7 中的 Java 信号量代码过于简单。以下是 `delay()` 过程的一个改进版本：

```
// adapted from Lea [2000], p. 267

public void delay() throws InterruptedException{
    if (Thread.interrupted())
        throw new InterruptedException();
    synchronized(this){
        try{
            while (count <= 0) wait();
            count--;
        }catch(InterruptedException ie){
            notify(); throw ie;
        }
    }
}
```

请仔细解释该代码与图 13.7 中的代码之间每一处不同的原因。

# 13.29
如果从 `put` 操作（图 13.6 的第 28 行）中移除关键字 `synchronized`，请解释有界缓冲区问题 Java 代码的行为。

# 13.30
在 Ada 中，你已经看到有界缓冲区既可以用任务表示，也可以用管程表示。这两种解决方案中是否有一种优于另一种？为什么？

# 13.31
共享内存系统可以通过使用互斥定义一个邮箱工具，来模仿消息传递的邮箱版本。请编写一个包，在以下语言中实现邮箱（即具有发送和接收原语的数据队列）：

## (a) Java

## (b) Ada

# 13.32
在 Ada 中，入口的调用者在对应的 `accept` 语句执行期间必须挂起执行。为什么这是必要的？

# 13.33
在 Ada 的 `select` 备选分支中，`accept` 语句后面可以跟更多语句。例如，在 Ada 的有界缓冲区解决方案中，我们编写了：

```
accept insert (ch: in character) do
    bufferEnd := bufferEnd mod MaxBufferSize + 1;
    store (bufferEnd) := ch;
end insert;
bufferSize := bufferSize + 1;
```

请注意，`bufferSize` 是在 `accept` 语句之外递增的。这样做有原因吗？该语句能否放到 `accept` 内部？`store(bufferEnd) := ch` 语句能否移到 `accept` 之外？为什么？

```
task body Mult is
    begin
        accept DoRow (i: in INTEGER ) do
            for j in 1..Size loop
                c(i, j) := 0;
                for k in 1..Size loop
                    c(i, j) := c(i, j) + a(i, k)*b(k, j);
                end loop;
            end loop;
        end;
    end Mult;
```

这个解决方案有什么问题？

# 13.41
本章忽略了并发程序形式语义的问题。（参考文献中提到了一些研究。）你能想到在并发程序中应用公理化语义可能遇到的问题吗？指称语义呢？

# 13.42
图 13.13 中 Ada 的矩阵乘法解决方案使用矩阵的大小来确定任务数量。请重写该解决方案，使任务数量作为 `ParMult` 函数的输入参数指定。

# 13.43
Prolog 中的或并行可以看作是对备选树的并行搜索（见第 4 章），其中在每个节点上都会创建一个新进程来搜索每个子节点。请描述这些进程如何协调它们的活动以允许回溯。

# 13.44
请编写一个过程，在以下语言中对无序二叉树执行并行搜索：

## (a) Java

## (b) Ada

# 13.45
请讨论正文中的论断：或并行对 Prolog 更自然，而与并行对 Lisp 更自然。

# 13.46
请详细描述或并行 Prolog 如何并行计算 `delete([1,2,3],X,T)` 的三个解。你预计会节省多少时间（以步骤数计）？

# 13.47
在第 625 页的 `generate` 的与并行 Prolog 示例中，实际执行了多少并行操作？请解释。

# 13.48
在与并行 Prolog 中，如果守卫遇到未实例化的变量，执行将挂起，直到该变量被（另一个进程）实例化。为什么这是必要的？这个要求有什么问题吗？

# 13.49
请解释为什么与并行 Prolog 中的回溯很困难。

# 13.50
在图 13.4 和图 13.5 中，主进程创建新的子进程来计算矩阵乘积，然后挂起直到所有子进程完成。这是浪费的。请重写这些程序，使主进程也与其子进程并行执行一些计算。

# 13.51
请比较邮箱的概念与缓冲区的概念。

# 13.52
假设两个进程都试图递增一个不受互斥机制保护的共享变量 `S`。假设赋值

```
S := S + 1
```

在每个进程中由三条机器指令组成：

+   将 `S` 装入寄存器

+   对寄存器加 1

+   将寄存器存储到 `S`

在两个进程都完成其递增操作后，`S` 可能具有哪些值？请说明如何得到每个值。

# 注释与参考文献

并行/并发编程领域非常庞大，涉及操作系统、体系结构和语言问题。在本章中，我们几乎只涉及了具体的语言问题，主要以 Java 和 Ada 作为示例。通常，一门完整的课程会专门讨论并行编程，并且经常使用第三方库支持的一种语言无关的协议。该领域两本有用的教材是 Andrews [2000] 和 Wilkinson and Allen [1997]。

并行编程语言的综述包括 ACM Computing Surveys 1989 年 9 月号（第 21 卷第 3 期）和 IEEE Software 1989 年 7 月号。以下还提到了这些期刊中的一些单篇文章。另一篇综述文章是 Andrews and Schneider [1983]。

使用 Java 线程进行编程的研究见 Lea [2000]、Horstmann and Cornell [1999]（第二卷）和 Arnold et al. [2000]。关于线程的另一种观点，参见 Butenhof [1997]，该书描述了 UNIX 的 Pthreads 标准。使用 Ada 任务和 Ada95 受保护类型进行编程的研究见 Cohen [1996]；另见 Wegner and Smolka [1983]。

并行体系结构的综述见 Duncan [1990]。第 13.1 节的图改编自 Karp [1987]，其中还研究了几种向 FORTRAN 添加并行性的方法。另见 Karp and Babb [1988]，其中有与第 13.2 节类似的示例。

信号量由 Dijkstra [1968b] 引入。关于它们在操作系统中的使用，见 Stallings [2000]。管程由 Hoare [1974] 引入，并被纳入 Brinch-Hansen [1975] 设计的 Concurrent Pascal 语言。

调度策略、公平性和饥饿问题在本章中仅简要提及，而相关的进程优先级问题完全没有讨论。关于 Java 方法的讨论，见 Lea [2000]，特别是 3.4.1 和 3.7 节。关于 Ada95 方法的讨论，见 Cohen [1996] 第 18.6 节。

消息传递，包括一种称为通信顺序进程（Communicating Sequential Processes，CSP）的理论框架，由 Hoare [1978] 引入。CSP 经常用作并发程序形式语义和验证的基础；见 Schneider [2000]。CSP 也是编程语言 Occam 的灵感来源，该语言设计用于在称为 transputer 的专有并行系统上运行；见 Jones and Goldsmith [1988]。关于使用称为进程代数（process algebra）的技术处理并发程序形式语义的不同方法，见 Milner [1994]。

Multilisp 的描述见 Halstead [1985]。QLisp 的描述见 Goldman and Gabriel [1989]。并行逻辑编程的综述包括 Kergommeaux and Codognet [1994]、Ciancarini [1992]、Shapiro [1989] 和 Tick [1991]。Parlog 的研究见 Conlon [1989]、Gregory [1987] 和 Ringwood [1988]。FGHC 的描述见 Ueda [1987]。逻辑编程中的并发与约束（第 4 章）密切相关；见 Ueda [2000] 或 Saraswat and Van Hentenryck [1995]。

关于网络上分布式并行计算的各种协议的信息，可以在 Horstmann and Cornell [1999] 第二卷（Java 的 RMI）和 Pacheco [1996]（MPI）中找到。关于 CORBA 和 COM 的书籍多到无法一一列举，因为这些协议不仅用于并发，还用于程序互操作。简要介绍见 Horstmann and Cornell [1999]。

有几个项目将互联网用作大型并行处理系统；其中最著名的可能是“互联网梅森素数大搜索项目”（Great Internet Mersenne Prime Search Project，见 www.mersenne.org），该项目目前保持着已知最大素数的纪录。

Erlang 的描述见 Armstrong [2007] 和 [2010]。

Abelson et al. 1998. "关于算法语言 Scheme 的修订报告," Higher-Order and Symbolic Computation 11(1): 5–105, 1998 年 8 月。 (也称为 R³RS。)

Abelson, H. and G. J. Sussman with Julie Sussman. 1996. 《计算机程序的构造和解释》(第 2 版)。剑桥，马萨诸塞州：MIT Press。

Aggoun, A. and N. Beldiceanu. 1991. "CHIP 编译器系统的概述," in K. Furukawa (Ed.) Logic Programming, 第八届国际会议论文集, 巴黎, 法国, 剑桥：MIT Press, pp. 775–789。

Aho, A. V., J. E. Hopcroft, and J. D. Ullman. 1983. 《数据结构与算法》。雷丁，马萨诸塞州：Addison-Wesley。

Aho, A. V., B. W. Kernighan, and P. J. Weinberger. 1988. 《AWK 编程语言》。雷丁，马萨诸塞州：Addison-Wesley。

Aho, A. V., R. Sethi, and J. D. Ullman. 1986. 《编译原理、技术与工具》。雷丁，马萨诸塞州：Addison-Wesley。

Alexandrescu, A. 2001. 《现代 C++ 设计：通用编程与设计模式的应用》。雷丁，马萨诸塞州：Addison-Wesley。

Andrews, G. R. 2000. 《多线程、并行和分布式编程基础》。雷丁，马萨诸塞州：Addison-Wesley。
