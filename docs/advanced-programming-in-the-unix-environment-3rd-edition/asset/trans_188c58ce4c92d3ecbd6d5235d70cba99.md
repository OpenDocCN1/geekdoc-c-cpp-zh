

## 11.6.7 自旋锁

自旋锁与互斥锁类似，不同之处在于进程被阻塞的方式：而不是通过睡眠，进程会通过忙等待（自旋）阻塞，直到能够获取锁。自旋锁可用于锁持有时间较短且线程不希望承担被调度出去成本的情况。

自旋锁通常用作低级原语来实现其他类型的锁。根据系统架构，它们可以使用测试并设置指令高效地实现。尽管高效，但它们可能导致浪费 CPU 资源：在线程自旋等待锁可用时，CPU 不能做其他事情。这就是为什么自旋锁只能持有很短时间的原因。

自旋锁在非抢占式内核中使用时很有用：除了提供互斥机制外，它们还会阻塞中断，从而防止中断处理程序通过尝试获取已被锁定的自旋锁而导致系统死锁（将中断视为另一种类型的抢占）。在这种类型的内核中，中断处理程序不能睡眠，因此它们唯一能使用的同步原语就是自旋锁。

然而，在用户级，除非你在不允许抢占的实时调度类别中运行，否则自旋锁并不那么有用。运行在分时调度类别中的用户级线程在时间片到期时或具有更高调度优先级的线程变为可运行时会被调度出去。在这些情况下，如果一个线程持有自旋锁，它将被置于睡眠状态，而被阻塞在锁上的其他线程将比预期自旋更长时间。

许多互斥锁实现已经非常高效，以至于使用互斥锁的应用程序的性能等同于它们使用自旋锁时的性能。事实上，一些互斥锁实现会在尝试获取互斥锁时自旋一段时间，只有在自旋计数阈值达到时才睡眠。这些因素，加上现代处理器允许它们以越来越快的速度进行上下文切换，使得自旋锁仅在有限的情况下才有用。

自旋锁的接口与互斥锁相似，使得相对容易用一个替换另一个。我们可以使用 pthread_spin_init 函数初始化自旋锁。要反初始化自旋锁，我们可以调用 pthread_spin_destroy 函数。

```
#include <pthread.h>

int pthread_spin_init(pthread_spinlock_t *lock, int pshared);
int pthread_spin_destroy(pthread_spinlock_t *lock);

Both return: 0 if OK, error number on failure
```

对于自旋锁，只指定了一个属性，该属性仅在平台支持线程进程共享同步选项时才重要（现在在单一 UNIX 规范中是强制性的；回顾图 2.5）。pshared 参数表示进程共享属性，它指示自旋锁将如何被获取。如果将其设置为 PTHREAD_PROCESS_SHARED，则自旋锁可以被具有访问锁底层内存的线程获取，即使这些线程来自不同的进程。否则，pshared 参数设置为 PTHREAD_PROCESS_PRIVATE，自旋锁只能由初始化它的进程内的线程访问。

要锁定自旋锁，我们可以调用 pthread_spin_lock，它会自旋直到获取锁，或调用 pthread_spin_trylock，如果锁不能立即获取则返回 EBUSY 错误。请注意 pthread_spin_trylock 不会自旋。无论如何锁定，自旋锁都可以通过调用 pthread_spin_unlock 来解锁。

```
#include <pthread.h>
int pthread_spin_lock(pthread_spinlock_t *lock);
int pthread_spin_trylock(pthread_spinlock_t *lock);
int pthread_spin_unlock(pthread_spinlock_t *lock);
All return: 0 if OK, error number on failure
```

请注意，如果自旋锁当前未锁定，则 pthread_spin_lock 函数可以不自旋地锁定它。如果线程已经锁定了它，结果是未定义的。对 pthread_spin_lock 的调用可能会以 EDEADLK 错误（或其他错误）失败，或者调用可能会无限自旋。行为取决于实现。如果我们尝试解锁未锁定的自旋锁，结果也是未定义的。

如果 pthread_spin_lock 或 pthread_spin_trylock 返回 0，则自旋锁已锁定。我们需要小心不要在持有自旋锁时调用可能导致睡眠的函数。如果我们这样做，那么当其他线程尝试获取它时，我们会通过延长它们自旋的时间来浪费 CPU 资源。

## 11.6.8 屏障

屏障是一种同步机制，可用于协调并行工作的多个线程。屏障允许每个线程等待直到所有协作线程都到达同一点，然后从那里继续执行。我们已经见过一种形式的屏障——pthread_join 函数充当屏障，允许一个线程等待另一个线程退出。

然而，屏障对象比这更通用。它们允许任意数量的线程等待直到所有线程完成处理，但线程不必退出。它们可以在所有线程到达屏障后继续工作。

我们可以使用 pthread_barrier_init 函数初始化屏障，并使用 pthread_barrier_destroy 函数反初始化屏障。

```
#include <pthread.h>
int pthread_barrier_init(pthread_barrier_t *restrict barrier,
    const pthread_barrierattr_t *restrict attr,
    unsigned int count);
int pthread_barrier_destroy(pthread_barrier_t *barrier);
Both return: 0 if OK, error number on failure
```

当我们初始化屏障时，我们使用 count 参数指定必须到达屏障的线程数，然后所有线程将被允许继续。我们使用 attr 参数指定屏障对象的属性，我们将在下一章更详细地讨论。现在，我们可以将 attr 设置为 NULL 以使用默认属性初始化屏障。如果 pthread_barrier_init 函数为屏障分配了任何资源，则在我们通过调用 pthread_barrier_destroy 函数反初始化屏障时，这些资源将被释放。

我们使用 pthread_barrier_wait 函数来指示线程已完成其工作并准备等待所有其他线程赶上。

```
#include <pthread.h>
int pthread_barrier_wait(pthread_barrier_t *barrier);
Returns: 0 or PTHREAD_BARRIER_SERIAL_THREAD if OK, error number on failure
```

如果屏障计数（在调用 pthread_barrier_init 时设置）尚未满足，则调用 pthread_barrier_wait 的线程将被置于睡眠状态。如果线程是最后一个调用 pthread_barrier_wait 的线程，从而满足屏障计数，则所有线程将被唤醒。

对于一个任意线程，它看起来像是 pthread_barrier_wait 函数返回了 PTHREAD_BARRIER_SERIAL_THREAD 的值。剩余的线程看到返回值为 0。这允许一个线程继续作为主线程，对所有其他线程完成的工作结果进行操作。

一旦屏障计数达到且线程被解除阻塞，屏障可以再次使用。然而，除非我们调用 pthread_barrier_destroy 函数然后使用不同的计数调用 pthread_barrier_init 函数，否则屏障计数不能被更改。

### 示例

图 11.16 显示了如何使用屏障来同步在单个任务上协作的线程。

```
#include "apue.h"
#include <pthread.h>
#include <limits.h>
#include <sys/time.h>

#define NTHR 8                 /* number of threads */
#define NUMNUM 8000000L        /* number of numbers to sort */
#define TNUM  (NUMNUM/NTHR)    /* number to sort per thread */

long nums[NUMNUM];
long snums[NUMNUM];

pthread_barrier_t b;

#ifdef SOLARIS
#define heapsort qsort
#else
extern int heapsort(void *, size_t, size_t,
```

```
int (*)(const void *, const void *);

#endif

/*
 * Compare two long integers (helper function for heapsort)
 */
int
complong(const void *arg1, const void *arg2)
{
    long l1 = *(long *)arg1;
    long l2 = *(long *)arg2;

    if (l1 == l2)
        return 0;
    else if (l1 < l2)
        return -1;
    else
        return 1;
}

/*
 * Worker thread to sort a portion of the set of numbers.
 */
void *
thr_fn(void *arg)
{
    long idx = (long)arg;

    heapsort(&nums[idx], TNUM, sizeof(long), complong);
    pthread_barrier_wait(&b);

    /*
     * Go off and perform more work ...
     */
    return((void *)0);
}

/*
 * Merge the results of the individual sorted ranges.
 */
void
merge()
{
    long idx[NTHR];
    long i, minidx, sidx, num;

    for (i = 0; i < NTHR; i++)
        idx[i] = i * TNUM;
    for (sidx = 0; sidx < NUMNUM; sidx++) {
        num = LONG_MAX;
        for (i = 0; i < NTHR; i++) {
            if ((idx[i] < (i+1)*TNUM) && (nums[idx[i]] < num)) {
                num = nums[idx[i]];
```

