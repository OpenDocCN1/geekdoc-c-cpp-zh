

## 284 第 14 章：线程

将条件变量作为线程间传递互斥锁的一种方式。

OpenStep 规范包含了这个封装了 `NSConditionLock` 的低级原语类。与 POSIX 版本不同（后者在每次调用时都需要与互斥锁关联），该类包含它自己的互斥锁并实现了 `NSLocking` 协议。

这意味着你可以将条件锁当作锁来使用，尽管这样做会浪费资源。作为锁，条件锁还关联了一个整数变量，表示条件。当你在条件锁上进行睡眠（sleep）时，你可以指定一个值。只有当条件锁被该值信号（signal）触发时，你的线程才会被唤醒。

当你等待的条件是一个整数值时，条件锁非常方便，但在其他情况下则不那么方便。通常，你希望线程在对象进入特定状态时唤醒。使用低级 POSIX 函数实现这一点非常容易，因为它们要求你自己测试条件，但使用 `NSConditionLock` 就没那么容易了。

为了解决这个问题，Apple 引入了 `NSCondition` 类。它是对 POSIX 互斥锁和条件变量的简单封装。你可以锁定它，在释放锁的同时进行睡眠，然后从另一个线程向它发送信号来唤醒它。

当你对一个

在睡眠后唤醒时，

### 等待条件 285

**NSCondition**，条件对象将处于锁定状态。你必须测试你的条件，然后要么解锁条件对象，要么返回睡眠。

在几乎所有使用条件变量的情况下，你都使用相同的模式。通常情况下，它们允许你在线程之间建立生产者-消费者关系。消费者线程需要睡眠，直到有数据在等待它。生产者线程在有数据可供其使用时需要唤醒消费者线程。

本节开头的示例展示了类中的两个方法。`-addToQueue` 方法预期从生产者线程中调用，而 `-main` 方法实现了消费者线程。

消费者线程的代码展示了线程化对象的几个重要特性。它没有使用 `NSRunLoop`，而是实现了它自己的运行循环（一个无限循环），并显式地在每次迭代中创建和销毁自动释放池。在每次迭代中，如果没有数据等待，它会首先锁定条件，释放锁并睡眠。

生产者线程随后可以获取锁并信号条件。当这种情况发生时，消费者线程将在锁可用时立即准备唤醒。生产者通过释放锁允许了这一点。

消费者线程随后获取下一段数据进行处理并释放锁。在这个示例中，增加和减少共享变量被用作向共享数据结构中添加某些数据的代理。

**注意：** 从条件变量唤醒线程所需的操作序列是非常昂贵的，因此可能的情况下应该避免。对于两个线程之间的通信，我通常倾向于使用无锁环形缓冲区（lockless ring buffer），它在空闲一段时间后切换到锁定模式。Apple 的 Grand Central Dispatch（GCD）在内部实现了这种模型，因此你可以使用它，而不需要自己编写环形缓冲区代码。

## Blocks 与 Grand Central

Objective-C 最近添加的内容之一是支持 *blocks*（块），也称为 *closures*（闭包）。Blocks 是 Smalltalk 的一部分，但由于几个原因在 Objective-C 中被省略了。Smalltalk 使用它们进行流控制，而 Objective-C 继承了 C 的流控制原语，因此不需要它们。编译器和运行时库的额外复杂性加上性能损耗，意味着最初它们对 Objective-C 并不是高优先级。

闭包是一个可以在其他作用域内部创建的函数，并可以引用该作用域内部的变量。通常，函数可以引用三类东西：全局变量、参数和局部变量。它只能存在于全局作用域中。相比之下，block 可以在函数内部、甚至在另一个 block 内部声明。它可以引用声明 block 时可见的任何变量。

## 将变量绑定到 Blocks

```
int (^add)(int, int) =
^(int a, int b)
{
    return a + b;
};
```
源自：blockScope.m

你可以将函数看作 block 的特殊情况。从概念上讲，函数是一个声明在全局作用域中的 block。它们的实现方式略有不同，但在这种情况下，这些差异微乎其微。

因此，block 最简单的情况等同于函数。它接收一些参数，产生一些输出，并且不引用自身作用域之外的任何内容。本节开头的代码片段展示了此类 block 的示例。该声明位于全局作用域，看起来像是一种非常冗长的函数声明形式。

另一种类型的 block 引用其声明所在函数作用域中的内容。你可以在 `blockScope.m` 的其他部分看到这种 block。

这个 block 引用了两个变量。`counter` 是一个静态变量，这意味着它存储在从程序镜像映射的内存中，

### 将变量绑定到 Blocks 289

注意：虽然暴露给程序员的只有一种类型的 block，但在实现中存在两种。你可以通过检查 `isa` 指针来确定你拥有的是哪种 block，尽管公共 API 并不保证这一点，且可能会在不通知的情况下更改。如果你创建一个不引用参数或全局变量之外的任何内容的 block，那么该 block 是静态分配的，每当在概念上创建它时，你都会得到指向同一个对象的指针。
如果你创建一个引用栈上内容的 block，那么该 block 是动态分配的。这意味着对它的任何引用都将引用同一个变量。此处的实现非常复杂。变量从栈被移动到堆内存中一段引用计数的代码中。这意味着对它的任何引用都会引用同一个变量。此处的实现非常复杂。变量从栈移动到堆内存中一段引用计数的代码中。

```
void(^getCounter(void))(void)
{
    static int counter;
    int c = counter;
    void(^block)(void) = ^(void)
    {
        printf("current: %d ", counter);
        printf("old: %d\n", c);
    }
    counter++;
    return Block_copy(block);
}

int main(void)
{
    void(^block)(void) = getCounter();
    block(); block();
    void(^block2)(void) = getCounter();
    block2(); block2();
    block(); block();
    return 0;
}
```
源自：blockScope

```
current: 1 old: 0
current: 1 old: 0
current: 2 old: 1
current: 2 old: 1
current: 2 old: 0
current: 2 old: 0
```
来自 block 输出

传统的闭包引用的是外层作用域中的真实变量，而不是拷贝。你可以通过对变量使用 `__block` 修饰符来实现这种行为。这种实现非常复杂。变量从栈移动到堆内存中一段引用计数的代码中。这意味着对它的任何引用都会引用同一个变量。`blockCapture.m` 示例演示了这一点，该函数创建了两个关联的计数器。

```
typedef int (^counter_t)(void);
void linkedCounters(counter_t *a, counter_t *b)
{
  _block int c = 0;
  *a = ^(void) { return c++; };
  *b = ^(void) { return c++; };
  *a = Block_copy(*a);
  *b = Block_copy(*b);
  c++;
}

int main(void)
{
  counter_t pre, post;
  linkedCounters(&post, &pre);
  printf("%d %d, %d, %d\n",
  pre(), post(), pre(), post());
  return 0;
}
```
源自：blockCapture.m

这两个计数器都引用内存中的同一个变量：一个先返回它再增加；另一个先增加再返回它。每个 block 都会打印它创建时 `counter` 的值。

