

# 基于锁的并发数据结构

在移动锁之前，我们首先将描述如何在一些常用数据结构中使用锁。在数据结构中添加锁使其能够被线程使用，这使得该结构变得了线程安全。当然，具体如何添加这些锁决定了数据结构的正确性和性能。因此，我们面临的挑战是：

> 关键问题：如何在数据结构中添加锁？
> 对于一个特定的数据结构，我们应该如何对其添加锁以确保其能够正常工作？此外，我们应该如何添加锁，才能使数据结构产生高性能，允许许多线程同时访问该结构（即并发访问）？

当然，我们无法涵盖所有的数据结构或所有添加并发的方法，因为这是一个已经研究了多年的课题，并发表了（字面上的）数以千计的相关研究论文。因此，我们希望对所需的思维方式提供足够的介绍，并向你推荐一些良好的素材资源，供你自行进一步查询。我们发现 Moir 和 Shavit 的综述是一份极佳的信息来源 [MS04]。

## 29.1 并发计数器

最简单的数据结构之一是计数器。它是一种常用且接口简单的结构。我们在图 29.1 中定义了一个简单的非并发计数器。

### 简单但不可扩展

如你所见，非同步的计数器是一个平而易举的数据结构，只需要少量代码即可实现。现在我们面临下一个挑战：如何让它变得线程安全？图 29.2 展示了我们如何做。

```c
typedef struct __counter_t {
    int value;
} counter_t;

void init(counter_t *c) {
    c->value = 0;
}

void increment(counter_t *c) {
    c->value++;
}

void decrement(counter_t *c) {
    c->value--;
}

int get(counter_t *c) {
    return c->value;
}
```

图 29.1：没有锁的计数器

这个并发计数器简单且运行正常。事实上，它遵循了最简单、最基础的并发数据结构常见的设计模式：它添加了一个单锁，在执行操作数据结构的例程时获取锁，并在从调用返回时释放锁。通过这种方式，它类似于使用监视器（monitors）构建的数据结构 [BH73]，在你调用和从对象方法返回时，锁会自动获取和释放。

此时，你已经有了一个可以工作的并发数据结构。如果你的数据结构太慢，你将需要做比添加单锁更多的的操作；如果需要，此类优化是本章节后续的内容。注意，如果数据结构并不慢，你不需要做任何事情；简单的方法就能很好。

为了理解简单方法的性能代价，我们运行了一个基准测试，其中每个线程更新共享计数器百万次；我们改变线程的数量。图 29.5 显示了一个到四个线程所花费的总时间；每个线程更新计数器一百万次。该实验是在一台带有 Intel 2.7 GHz CPU 的 iMac 上运行的；随着 CPU 的增加，我们必须在单位时间内完成更多的总工作。

从图中顶行（标记为“Precise”），你可以看到同步计数器的性能扩展性很差。虽然单个线程可以在极短的时间内完成百万次计数器更新（大约 0.03 秒），但让两个线程并发地每个更新计数器百万次会导致严重的减速（耗时超过 5 秒！）。随着线程的增加，情况变得更加糟糕。

```c
typedef struct __counter_t {
    int value;
    pthread_mutex_t lock;
} counter_t;

void init(counter_t *c) {
    c->value = 0;
    pthread_mutex_init(&c->lock, NULL);
}

void increment(counter_t *c) {
    pthread_mutex_lock(&c->lock);
    c->value++;
    pthread_mutex_unlock(&c->lock);
}

void decrement(counter_t *c) {
    pthread_mutex_lock(&c->lock);
    c->value--;
    pthread_mutex_unlock(&c->lock);
}

int get(counter_t *c) {
    pthread_mutex_lock(&c->lock);
    int rc = c->value;
    pthread_mutex_unlock(&c->lock);
    return rc;
}
```

> 图 29.2：带锁的计数器

理想情况下，你希望看到线程能像单线程一样快速完成。这种被称为完美扩展；尽管做了更多工作，但所花费的时间并没有增加。

### 可扩展计数

为了清楚这一点，让我们来看一个示例（图 29.3）。在这个示例中，每个 CPU 都有自己的局部计数器，只有当局部计数器达到阈值时才会更新全局计数器。S 越小，它就越像非同步计数器；S 越大，它就越可扩展。

（注：源码中图 29.3 的表格文本是碎片化的。根据“可扩展计数”的上下文，以下是近似计数器的重建逻辑。）

```c
typedef struct __counter_t {
    int global;
    pthread_mutex_t glock;
    int local[NUMCPUS];
    pthread_mutex_t locks[NUMCPUS];
    int threshold;
} counter_t;

// init：记录阈值，初始化锁
// 局部计数和全局计数的值
void init(counter_t *c, int threshold) {
    c->threshold = threshold;
    c->global = 0;
    pthread_mutex_init(&c->glock, NULL);
    for (int i = 0; i < NUMCPUS; i++) {
        c->local[i] = 0;
        pthread_mutex_init(&c->locks[i], NULL);
    }
}

// update：通常，只需获取局部锁并更新
// 局部值；局部计数达到“阈值”，
// 获取全局锁并将局部值转移到它
void update(counter_t *c, int threadID, int amt) {
    int cpu = threadID % NUMCPUS;
    pthread_mutex_lock(&c->locks[cpu]);
    c->local[cpu] += amt;
    if (c->local[cpu] >= c->threshold) {
        // 转移到全局（假设 amt > 0）
        pthread_mutex_lock(&c->glock);
        c->global += c->local[cpu];
        pthread_mutex_unlock(&c->glock);
        c->local[cpu] = 0;
    }
    pthread_mutex_unlock(&c->locks[cpu]);
}

// get：返回全局值（近似值）
int get(counter_t *c) {
    pthread_mutex_lock(&c->glock);
    int val = c->global;
    pthread_mutex_unlock(&c->glock);
    return val; // 仅近似；
}
```

图 29.4：近似计数器实现

