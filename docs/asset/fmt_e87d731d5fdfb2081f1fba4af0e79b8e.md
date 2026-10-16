
Bit-fields (§8.2.7) give access to parts of a word. If two threads simultaneously access two fields of the same word, all bets are off. If `b` and `c` are two fields of the same word, most hardware has no way of avoiding the problem (the race condition) from the `b`-and `c` example without using some form of (potentially very expensive) locking. Lock and unlock operations are not a cost we could implicitly impose on bit-fields, which are commonly used in critical device drivers. Consequently, the language defines memory location as the unit of memory for which sensible behavior is guaranteed to exclude individual bit-fields.

A memory location is either an object of arithmetic type (§6.2.1), a pointer, or a maximal sequence of adjacent bit-fields all having nonzero width. For example:

```
struct S {
char a;
int b:5;
unsigned c:11; unsigned :0; unsigned d:8;

// location #1 // location #2

// note: :0 is “special”(§8.2.7) // location #3
struct { int ee:8; } e; // location #4
};
```

Here, `S` has exactly four separate memory locations. Don’t try to update bit-fields `b` and `c` from separate threads without explicit synchronization.

From the explanation above, you might conclude that if `x` and `y` are of the same type, `x=y` is guaranteed to result in `x` being a copy of `y`. This is true if and only if you don’t have a data race (§41.2.4) and if `x` and `y` are memory locations. However, if `x` and `y` are of a multiword struct they are not a single memory location, and if you have a data race, all behavior is undefined, so make sure you have proper synchronization in place if you share data (§41.3, §42.3.1).

# 41.2.2 Instruction Reordering

To gain performance, compilers, optimizers, and hardware reorder instructions. Consider:

```
// thread 1:
int x;
bool x_init;

void init() {
x = initialize(); // no use of x_init in initialize()
x_init = true;
// ...
}
```

For this piece of code there is no stated reason to assign to `x` before assigning to `x_init`. The optimizer (or the hardware instruction scheduler) may decide to speed up the program by executing `x_init=true` first.

We probably meant for `x_init` to indicate whether `x` had been initialized by `initializer()` or not. However, we did not say that, so the hardware, the compiler, and the optimizer do not know that.

Add another thread to the program:

```
// thread 2:
extern int x;
extern bool x_init;

void f2() {
int y;
while (!x_init) // if necessary,wait for initialization to complete
this_thread::sleep_for(milliseconds{10});
y=x;
// ...
}
```

Now we have a problem: thread 2 may never wait and thus will assign an uninitialized `x` to `y`. Even if thread 1 did not set `x_init` and `x` in “the wrong order,” we still may have a problem. In thread 2, there are no assignments to `x_init`, so an optimizer may decide to lift the evaluation of `!x_init` out of the loop, so that thread 2 either never sleeps or sleeps forever.

# 41.2.3 Memory Order

The time needed to get the value of a word from memory into a cache, then into a register, can be (on a processor’s time scale) very long. At best, maybe 500 instructions are executed before the value reaches the register, and another 500 instructions are executed before a new value reaches its intended location. The figure 500 is a guess that depends on machine architecture and varies over time, but for the last decades it has steadily increased. When there is no rush to load and store a particular value because the computation is optimized for throughput, the time taken can be much higher. A value can be “away from its location” for tens of thousands of instruction cycles. This is one of the facts that give modern hardware its amazing performance, but it also opens huge opportunities for confusion as different threads look at a value at different times and in different places in the memory hierarchy. For example, my simplified description mentions only a single cache; many popular architectures use a three-level cache. To illustrate, here is a diagram of a possible two-level cache architecture where each core has its own level-2 cache, a pair of cores share a level-1 cache, and all cores share the memory:

```
core 1 core 2 core 3 core 4 cache 2.1 cache 2.2 cache 2.3 cache 2.4 cache 1.1 cache 1.2 memory
```

*Memory ordering* is the term used to describe what a programmer can assume about what a thread sees when it looks at a value from memory. The simplest memory order is called *sequentially consistent*. In a sequentially consistent memory model, every thread sees the effects of every operation done in the same order. The order is as if the instructions were done sequentially in a single thread. A thread can still reorder operations, but at every point where another thread might observe a variable, the set of operations performed before and (therefore) the value of the memory location observed must be well defined and the same for all threads. An operation that “observes” a value and thereby forces a consistent view of a memory location is called an *atomic operation* (see §41.3). A simple read or write does not impose an order.

There are many possible sequentially consistent orders for a given set of threads. Consider:

```
// thread 1:          // thread 2:
char c = 0;          char b = 0;
extern char b;       extern char c;
void f1()            void f2()
{
    c = 1;               b = 1;
    int x = b;            int y = c;
}
```

Assuming that the initialization of `c` and `b` is done statically (before any thread starts), there are three possible executions:

```
c = 1; b = 1; c = 1;
x = b; y = c; b = 1;
b = 1; c = 1; x = b;
y = c; x = b; y = c;
```

The results are **01**, **10**, and **11**, respectively. The only result we cannot get is **00**. Obviously, to get a predictable result, you need some form of synchronization of the access to the shared variables.

The sequential consistent order is just about all a programmer can effectively reason about, but on some machine architectures it imposes significant synchronization costs that can be eliminated by relaxing the rules. For example, two threads running on separate cores might decide to initiate the reads of `x` and `y` before the writes of `a` and `b` or at least before the writes had completed. That could give the nonsequentially consistent result **00**. More relaxed memory models allow that.

# 41.2.4 Data Races

From these examples, every sensible person will conclude that we have to be very careful 当编程线程时。但如何做到？首先，我们必须避免 *数据竞争*。如果两个线程可以同时访问一个内存位置（定义见 §41.2.1）并且其中至少一个访问是写操作，则这两个线程存在数据竞争。请注意，精确定义“同时”并非易事。如果两个线程存在数据竞争，则没有任何语言保证成立：行为是未定义的。这听起来可能很严厉，但数据竞争的影响可以（如 §41.2.2 所示）是严重的。优化器（或硬件指令调度器）可能会基于对值的假设重新排序代码，并且可能基于此类假设执行或不执行代码段（影响看似无关的数据）。

避免数据竞争的方法有很多：

- 只使用单个线程。这消除了并发的好处（除非你使用进程或协程）。

- 对可能存在数据竞争的每个数据项加锁。这几乎和单线程一样有效地消除了并发的好处，因为我们很容易陷入所有线程都在等待只有一个线程的情况。更糟的是，过度使用锁会增加死锁的机会，即一个线程永远等待另一个线程，以及其他锁定问题。

- 仔细查看代码并通过选择性地添加锁来避免数据竞争。这可能是目前最流行的方法，但容易出错。

- 让程序检测所有数据竞争并为程序员报告以便修复，或自动插入锁。能够做到这一点且适用于商业规模和复杂度的程序并不常见。能够做到这一点并保证不存在死锁的程序仍然是研究项目。

- 设计代码使线程仅通过简单的 put-and-get 风格接口通信，这些接口不需要两个线程直接操作单个内存位置（§5.3.5.1，§42.4）。

- 使用更高级别的库或工具，使数据共享和/或并发变得隐式或足够程式化以使共享可管理。示例包括库中算法的并行实现、基于指令的工具（例如 OpenMP）以及事务内存（通常缩写为 *TM*）。

可以将本章的其余部分看作是一种自下而上的方法，以实现对上述最后一种编程风格的一种变体的支持。在此过程中，我们遇到了支持几乎所有避免数据竞争的方法所需的工具。

为什么程序员必须忍受所有这些复杂性？另一种选择是只提供一个简单、顺序一致的模型，并尽可能少（或没有）数据竞争的机会。我可以给出两个原因：

- [1] 那不是世界的真实情况。机器架构的复杂性是真实存在的，而像 C++ 这样的系统编程语言必须为程序员提供与之共存的工具。也许有一天机器架构师会提供更简单的替代方案，但现在有人必须处理机器架构师提供的令人困惑的各种低级设施，以提供客户要求的性能。

- [2] 我们（C++ 标准委员会）认真考虑过这一点。我们希望提供一个内存模型，它是 Java 和 C# 提供的改进版本。这将为委员会和一些程序员节省大量工作。然而，这个想法被操作系统和虚拟机的提供者 effectively 否决了：他们坚持需要大致与当时各种 C++ 实现提供的相同——即现在由 C++ 标准提供的。替代方案将是你的操作系统和你的虚拟机“减慢两倍或更多”。我想编程语言狂热者可能会欢迎以牺牲其他语言为代价简化 C++ 的机会，但这样做既不实际也不专业。

幸运的是，大多数程序员永远不必直接在硬件的最低层工作。大多数程序员根本不需要理解内存模型，可以将重排序问题视为有趣的好奇心：

> *编写无数据竞争的代码并且不要乱用内存顺序（§41.3）；然后内存模型保证代码按天真预期执行。甚至比顺序一致性还要好。*

我发现机器架构是一个迷人的话题（例如参见 [Hennesey,2011] [McKenney,2012]），但作为明智而富有成效的程序员，我们在可能的情况下远离软件的最低层。把这些留给专家去享受那些专家为你提供的更高层。

# 41.3 Atomics
