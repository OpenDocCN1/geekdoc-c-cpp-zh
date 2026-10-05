

## 5.3 Pthreads 简介

到为止，我们对线程的讨论仅限于 OpenMP。OpenMP 是一种有限的编程模型，它主要适用于数据静态且访问模式规则的情况。Pthreads 则是一种更强大的编程模型。

Linux 内核支持创建和运行线程的 Pthread 接口。在 Linux 中，每个线程都是独立的进程。线程的创建与进程创建相同。线程组的特征是它们都使用相同的页表。同一组内不同线程生成的相同虚拟地址映射到相同的物理内存位置。因此，线程为不同进程共享内存提供了一种无缝的方式。

Pthreads 是一种强大的编程模型。使用 Pthreads 编写的程序范围远超科学计算。在本节中，我们将介绍 Pthreads，从基础内容开始逐步过渡到高级的主题。

在 5.3.1 中，我们通过一个简单的打印消息程序来介绍 Pthreads。文中介绍了实现互斥的两种主要技术：互斥锁（mutexes）和自旋锁（spinlocks）。求利布尼茨级数是另一个例子。

每个线程都需要一个栈来在函数调用成功后保存其状态。用户模式栈（在下一节中解释）仅由一个线程（主线程）使用。在 5.3.1 中，我们解释了如何为每个线程设置栈。线程栈通常有几 MB，并不大。因此，在线程编程中不要滥用栈是非常重要的。

在 5.3.2 中，我们确定线程创建的开销通常在 10⁶ 左右，偶尔会大出 10或 100 倍。这个数字解释了 OpenMP 程序进入第一个并行区域时产生的巨大开销。当 OpenMP 程序首次进入并行区域时会创建线程，线程创建开销是一项主要成本。该成本甚至可以达到毫秒。

5.3.3 节考虑了几个高级主题。该节的主题是使用 Pthreads 实现 OpenMP 并行区域。文中探索了几种实现方法。如果并行区域中的线程数量保持不变，则为第一个并行区域创建的线程可以重复使用。这解释了为什么典型的 OpenMP 并行区域与第一个并行区域相比成本较低。

5.3.3 节展示了内存屏（memory fences）和缓存一致性（cache coherence）在线程编程中的核心作用。尽管缓存一致性的作用对程序员来说是不可见的（除非主动查找），否则没有缓存一致性就无法进行多线程编程。当多个线程使用同一缓存行时，将写入从一个缓存传播到另一个缓存可能是巨大的开销源。5.3.3 节还展示了 TLB 刷新如何影响线程编程。

### 5.3.1 Pthreads

我们对 Pthreads 的讨论始于一个可能存在于简单顺序执行程序中的函数。`print_message()` 函数使用了基础 C 语法，且不包含任何 Pthread 构造。事实上，它被编译成汇编指令时，就像是一个单线程程序一样——这是我们在讨论 OpenMP 时提到过的一个重要点。稍后每个 Pthread 将通过此程序来获取控制权。

```c
void *print_message(void *arg) {
    char *s = (char *)arg;
    char ss [400];
    int l = strlen(s);
    for(int i=0; i < l; i++){
        ss[2*i] = s[i];
        ss[2*i+1] = (s[i]==' ') ? '_' : '_';
    }
    ss[2*l] = '\0';
    printf("%s",s);
    printf("\n");
    printf("%s", ss);
    printf("\n = %p\n", (void*)ss);
    return NULL;
}
```

`print_message()` 可能与 Pthreads 有关系的唯一迹象出现在它的第一行。它被声明为一个接受单个 `void *` 类型参数的函数，并返回一个 `void *` 类型的值。任何我们想要发送到 Pthread 的参数必须封装在内存区域中，并以 `void *` 指针的形式发送。

该函数的参数是一个消息或字符字符串。在第 2 行，该消息被传递给线程。`call_threads()` 创建创建三个线程并向每个线程发送一个字符串。

```c
#include <pthread.h>
#include <stdio.h>
#include <string.h>

void call_threads() {
    pthread_t thread1, thread2, thread3;
    char s[400];
    void *result;

    pthread_create(&thread1, NULL, print_message, "Message for 1");
    pthread_create(&thread2, NULL, print_message, "Message for 2");
    pthread_create(&thread3, NULL, print_message, "Message for 3");

    pthread_join(thread1, NULL, &result);
    pthread_join(thread2, NULL, &result);
    pthread_join(thread3, NULL, &result);
}
```

### 5.3.1 Pthreads 简介

每个线程都可能运行在不同的处理器核心上。在第 3 行，程序定义了 `pthread_t` 类型的变量。Pthread 库将使用这些变量访问关于线程的信息。关于创建线程的后续信息可以通过 `thread1`、`thread2` 或 `thread3` 获取。每个线程都有自己的栈。这个栈用于存储线程执行的函数所定义的局部变量。当线程进行函数调用时，返回地址会被推入其栈中。

在第 14 行，`print_message()` 函数打印 `ss` 的值，它是指向线程栈位置的指针。三个线程的输出如下：

