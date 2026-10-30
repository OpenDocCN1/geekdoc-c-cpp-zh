
```
#include <pthread.h>
int pthread_detach(pthread_t tid);
Returns: 0 if OK, error number on failure
```

正如我们将在下一章中所见，可以通过修改传给 `pthread_create` 的线程属性来创建一个已经处于分离状态的线程。

## 11.6 线程同步

当多个控制线程共享同一内存时，我们需要确保每个线程看到的数据是一致的。如果每个线程都使用其他线程不会读写或修改的变量，就不存在一致性问题。类似地，如果一个变量是只读的，那么多个线程同时读取它的值也不存在一致性问题。但是，当一个线程可能会修改另一个线程可读或可修改的变量时，我们就需要同步这些线程，以确保它们在访问该变量的内存内容时不会使用无效的值。

当一个线程修改一个变量时，其他线程在读取该变量的值时可能会看到不一致的情况。在修改操作需要多个内存周期的处理器架构上，如果内存读取发生在内存写入周期之间，就可能出现这种情况。当然，这种行为依赖于具体的架构，但可移植的程序不能对所使用的处理器架构类型做任何假设。

图 11.7 展示了一个两个线程读写同一个变量的假设示例。在这个示例中，线程 A 读取该变量，然后向它写入一个新值，但写操作需要两个内存周期。如果线程 B 在这两个写周期之间读取同一个变量，它就会看到一个不一致的值。

![](img/244bf0c3b6d0288ae397336907e37851_430_0.png)

为了解决这个问题，线程必须使用一把锁，使得每次只允许一个线程访问该变量。图 11.8 展示了这种同步。如果线程 B 想要读取该变量，它需要先获取锁。类似地，当线程 A 更新该变量时，它也需要获取同一把锁。因此，在线程 A 释放锁之前，线程 B 将无法读取该变量。

![](img/244bf0c3b6d0288ae397336907e37851_431_0.png)

图 11.8 两个线程同步内存访问

我们还需要同步两个或多个可能试图同时修改同一个变量的线程。考虑我们对一个变量进行递增操作的情况（图 11.9）。递增操作通常分为以下三个步骤。

- 1. 将内存位置中的值读取到寄存器中。
- 2. 递增寄存器中的值。
- 3. 将新值写回内存位置。

如果两个线程在几乎相同的时间试图递增同一个变量，而又没有相互同步，那么结果可能是不一致的。最终得到的值可能比之前大 1 或大 2，具体取决于第二个线程开始操作时观察到的值。如果第二个线程在第一个线程执行步骤 3 之前执行了步骤 1，第二个线程将读取到与第一个线程相同的初始值，递增它，然后写回，最终没有任何净效果。

如果修改是原子的，那么就不存在竞争。在前面的例子中，如果递增只需要一个内存周期，就不会有竞争。如果我们的数据总是表现为顺序一致的，那么我们就不需要额外的同步。当多个线程无法观察到我们数据中的不一致时，我们的操作就是顺序一致的。在现代计算机系统中，内存访问需要多个总线周期，而且多处理器通常会在多个处理器之间交错安排总线周期，因此我们无法保证数据是顺序一致的。

# 线程 A

# 线程 B

# i 的内容

将 i 取入寄存器（寄存器 = 5）

5

递增寄存器中的值（寄存器 = 6）

将 i 取入寄存器（寄存器 = 5）

5

将寄存器中的值存入 i（寄存器 = 6）

递增寄存器中的值（寄存器 = 6）

6

将寄存器中的值存入 i（寄存器 = 6）

6

时间

# 图 11.9 两个未同步的线程递增同一个变量

在顺序一致的环境中，我们可以将数据的修改解释为运行线程所执行操作的连续步骤。我们可以说“线程 A 先递增了变量，然后线程 B 递增了变量，因此它的值比之前大 2”，或者说“线程 B 先递增了变量，然后线程 A 递增了变量，因此它的值比之前大 2”。两个线程的任何可能排序都不会导致该变量产生其他值。

除了计算机架构之外，竞争还可能源于我们程序使用变量的方式，从而产生可能看到不一致的地方。例如，我们可能先递增一个变量，然后根据它的值做出决策。递增步骤和决策步骤的组合并不是原子的，这为不一致性的出现打开了一个窗口。

### 11.6.1 互斥锁

我们可以使用 pthreads 的互斥接口来保护数据，并确保每次只有一个线程能访问。互斥锁（mutex）本质上是一把锁，我们在访问共享资源之前设置它（加锁），在完成之后释放它（解锁）。当它被设置时，任何其他试图设置它的线程都将阻塞，直到我们释放它。如果我们解锁互斥锁时有多个线程被阻塞，那么所有阻塞在该锁上的线程都将变为可运行状态，最先运行的线程将能够设置该锁。其他线程会发现互斥锁仍处于锁定状态，于是回去继续等待它再次可用。这样，每次只有一个线程能够继续执行。

这种互斥机制只有在我们设计线程遵循相同的数据访问规则时才有效。操作系统不会为我们串行化对数据的访问。如果我们允许一个线程在未先获取锁的情况下访问共享资源，那么即使其余线程在尝试访问共享资源之前确实获取了锁，仍然可能发生不一致。

互斥锁变量由 `pthread_mutex_t` 数据类型表示。在使用互斥锁变量之前，我们必须先对其进行初始化：要么将它设置为常量 `PTHREAD_MUTEX_INITIALIZER`（仅用于静态分配的互斥锁），要么调用 `pthread_mutex_init`。如果我们动态分配互斥锁（例如通过调用 `malloc`），那么需要在释放内存之前调用 `pthread_mutex_destroy`。

```
#include <pthread.h>

int pthread_mutex_init(pthread_mutex_t *restrict mutex,
    const pthread_mutexattr_t *restrict attr);

int pthread_mutex_destroy(pthread_mutex_t *mutex);

Both return: 0 if OK, error number on failure
```

要用默认属性初始化互斥锁，我们将 `attr` 设置为 `NULL`。我们将在 12.4 节中讨论互斥锁属性。

要对互斥锁加锁，我们调用 `pthread_mutex_lock`。如果互斥锁已经被锁定，调用线程将阻塞，直到该互斥锁被解锁。要解锁互斥锁，我们调用 `pthread_mutex_unlock`。

```
#include <pthread.h>

int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);

All return: 0 if OK, error number on failure
```

如果线程无法承担阻塞的成本，可以使用 `pthread_mutex_trylock` 来有条件地对互斥锁加锁。如果在调用 `pthread_mutex_trylock` 时互斥锁处于未锁定状态，那么 `pthread_mutex_trylock` 将不阻塞地锁定该互斥锁并返回 0。否则，`pthread_mutex_trylock` 将失败，返回 `EBUSY` 且不锁定互斥锁。

# 示例

图 11.10 展示了使用互斥锁保护一个数据结构的例子。当多个线程需要访问一个动态分配的对象时，我们可以在对象中嵌入一个引用计数，以确保在所有线程使用完该对象之前不会释放其内存。

```
#include <stdlib.h>
#include <pthread.h>

struct foo {
    int f_count;
    pthread_mutex_t f_lock;
    int f_id;
    /* ... more stuff here ... */
};

struct foo *
foo_alloc(int id) /* allocate the object */
{
    struct foo *fp;
    if ((fp = malloc(sizeof(struct foo))) != NULL) {
        fp->f_count = 1;
        fp->f_id = id;
        if (pthread_mutex_init(&fp->f_lock, NULL) != 0) {
            free(fp);
            return(NULL);
        }
        /* ... continue initialization ... */
    }
    return(fp);
}

void
foo_hold(struct foo *fp) /* add a reference to the object */
{
    pthread_mutex_lock(&fp->f_lock);
    fp->f_count++;
    pthread_mutex_unlock(&fp->f_lock);
}

void
foo_rele(struct foo *fp) /* release a reference to the object */
{
    pthread_mutex_lock(&fp->f_lock);
    if (--fp->f_count == 0) { /* last reference */
        pthread_mutex_unlock(&fp->f_lock);
        pthread_mutex_destroy(&fp->f_lock);
        free(fp);
    } else {
        pthread_mutex_unlock(&fp->f_lock);
    }
}
```

# 图 11.10 使用互斥锁保护数据结构

在递增引用计数、递减引用计数和检查引用计数是否变为 0 之前，我们会锁定互斥锁。无需锁定
