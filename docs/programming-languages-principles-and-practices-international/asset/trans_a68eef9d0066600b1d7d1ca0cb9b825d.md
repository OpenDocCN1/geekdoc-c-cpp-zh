

## 13.28 由于存在中断的可能性，图 13.7 中的 Java 信号量代码过于简单。以下是 `delay()` 过程的一个改进版本：

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

## 13.29 如果从 `put` 操作（图 13.6 的第 28 行）中移除关键字 `synchronized`，请解释有界缓冲区问题 Java 代码的行为。

## 13.30 在 Ada 中，你已经看到有界缓冲区既可以用任务表示，也可以用管程表示。这两种解决方案中是否有一种优于另一种？为什么？

## 13.31 共享内存系统可以通过使用互斥定义一个邮箱工具，来模仿消息传递的邮箱版本。请编写一个包，在以下语言中实现邮箱（即具有发送和接收原语的数据队列）：
(a) Java
(b) Ada

## 13.32 在 Ada 中，入口的调用者在对应的 `accept` 语句执行期间必须挂起执行。为什么这是必要的？

## 13.33 在 Ada 的 `select` 备选分支中，`accept` 语句后面可以跟更多语句。例如，在 Ada 的有界缓冲区解决方案中，我们编写了：

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

## 13.41 本章忽略了并发程序形式语义的问题。（参考文献中提到了一些研究。）你能想到在并发程序中应用公理化语义可能遇到的问题吗？指称语义呢？

## 13.42 图 13.13 中 Ada 的矩阵乘法解决方案使用矩阵的大小来确定任务数量。请重写该解决方案，使任务数量作为 `ParMult` 函数的输入参数指定。

## 13.43 Prolog 中的或并行可以看作是对备选树的并行搜索（见第 4 章），其中在每个节点上都会创建一个新进程来搜索每个子节点。请描述这些进程如何协调它们的活动以允许回溯。

## 13.44 请编写一个过程，在以下语言中对无序二叉树执行并行搜索：
(a) Java
(b) Ada

## 13.45 请讨论正文中的论断：或并行对 Prolog 更自然，而与并行对 Lisp 更自然。

## 13.46 请详细描述或并行 Prolog 如何并行计算 `delete([1,2,3],X,T)` 的三个解。你预计会节省多少时间（以步骤数计）？

## 13.47 在第 625 页的 `generate` 的与并行 Prolog 示例中，实际执行了多少并行操作？请解释。

## 13.48 在与并行 Prolog 中，如果守卫遇到未实例化的变量，执行将挂起，直到该变量被（另一个进程）实例化。为什么这是必要的？这个要求有什么问题吗？

## 13.49 请解释为什么与并行 Prolog 中的回溯很困难。

## 13.50 在图 13.4 和图 13.5 中，主进程创建新的子进程来计算矩阵乘积，然后挂起直到所有子进程完成。这是浪费的。请重写这些程序，使主进程也与其子进程并行执行一些计算。

## 13.51 请比较邮箱的概念与缓冲区的概念。

## 13.52

假设两个进程都试图递增一个不受互斥机制保护的共享变量 S。假设赋值

S := S + 1

在每个进程中由三条机器指令组成：

+   将 S 装入寄存器
+   对寄存器加 1
+   将寄存器存储到 S

在两个进程都完成其递增操作后，S 可能具有哪些值？请说明如何得到每个值。

## 注释与参考文献

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

