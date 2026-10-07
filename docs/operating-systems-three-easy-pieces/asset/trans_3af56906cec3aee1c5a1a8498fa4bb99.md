

# 条件变量

| Tc1 | State | Tc2 | State | Tp | State | Count | Comment |
|---|---|---|---|---|---|---|---|
| c1 | Run | | Ready | Ready | 0 | |
| c2 | Run | | Ready | Ready | 0 | |
| c3 | Sleep | | Ready | Ready | 0 | 无数据可取 |
| | Sleep | | p1 | Run | 0 | |
| | Sleep | | p4 | Run | 1 | 缓冲区现满 |
| | Ready | | p5 | Run | 1 | Tc1 被唤醒 |
| | Ready | | p6 | Run | 1 | |
| | Ready | | p1 | Run | 1 | |
| | Ready | | p2 | Run | 1 | |
| | Ready | | p3 | Sleep | 1 | 缓冲区满；休眠 |
| | Ready | c1 | | Sleep | 1 | Tc2 溜入... |
| | Ready | c2 | | Sleep | 1 | |
| | Ready | c4 | | Sleep | 0 | ... 并取走了数据 |
| | Ready | c5 | | Ready | 0 | Tp 被唤醒 |
| | Ready | c6 | | Ready | 0 | |
| c4 | Run | | Ready | 0 | 噢！没有数据 |

图 30.9：线程轨迹：解决方案 (v1)

缓冲区是满的 (p2)，发现并非如此后，继续填充缓冲区 (p4)。然后生产者发送信号表示缓冲区已填充 (p5)。关键点在于，这使得第一个消费者 (Tc1) 从等待条件变量的休眠状态移动到就绪队列；Tc1 现在可以运行（但尚未运行）。生产者随后继续执行，直到发现缓冲区已满，此时它进入休眠状态 (p6, p1–p3)。

问题就发生在这里：另一个线程 (Tc2) 溜入并消耗了缓冲区中唯一的值 (c1, c2, c4, c5, c6，由于缓冲区是满的，跳过了 c3 处的等待）；假设 Tc1 在返回等待之前运行，它重新获取了锁并返回。然后它获取了 (1)，但没有缓冲区可以消费了！断言以某种方式阻止了 Tc1 尝试消费，因为 Tc2 溜入并消费了缓冲区中产生的唯一值。图 30.9 显示了连锁反应，以及其随时间变化的调度器状态（就绪、运行或休眠）。

问题的出现有一个简单的原因：在生产者唤醒 Tc1 之后、Tc1 运行之前，缓冲区的状态发生了变化（多亏于 Tc2）。信号线程会唤醒它们；因此，这暗示世界状态已经发生了变化（在这种情况下，缓冲区中放置了一个值），但不能保证当被唤醒的线程运行时，状态仍然符合预期。这种对“信号”含义的解释通常被称为 **Mesa 语义**，其命名源于第一个以此方式构建条件变量的研究 [LR80]；与之对比的是，被称为

© 2008–19, ARPACI-DUSSEAU

三个简单部分

# 378 条件变量

```
int loops;
cond_t cond;
mutex_t mutex;
```

```
void *producer(void *arg) {
    int i;
    for (i = 0; i < loops; i++) {
        Pthread_mutex_lock(&mutex); // p1
        while (count == 1) { // p2
            Pthread_cond_wait(&cond, &mutex); // p3
            put(i); // p4
        }
        Pthread_cond_signal(&cond); // p5
        Pthread_mutex_unlock(&mutex); // p6
    }
}
```

```
void *consumer(void *arg) {
    int i;
    for (i = 0; i < loops; i++) {
        Pthread_mutex_lock(&mutex); // c1
        while (count == 0) { // c2
            int temp = get(); // c3
            Pthread_cond_wait(&cond, &mutex); // c4
        }
        Pthread_cond_signal(&cond); // c5
        Pthread_mutex_unlock(&mutex); // c6
        printf("%d\n", temp);
    }
}
```

图 30.10：生产者/消费者：单条件变量与 While 循环

**Hoare 语义** 构建起来更困难，但它提供了更强的保证，确保线程在被唤醒后立即运行 [H74]。几乎每个系统都采用 Mesa 语义。

# **更好，但仍然存在：用 While 而非 If**

幸运的是，这个修复很容易（图 30.10）：将 `if` 改为 **while**。考虑一下它的工作原理：现在 T1 被唤醒并在（持有锁的情况下）重新检查共享变量的状态 (c2)。如果此时缓冲区为空，消费者将直接返回休眠 (c3)。生产者中的对应逻辑 (p2) 也随之改变了更改。

得益于 Mesa 语义，记忆条件变量的一个简单规则是：**始终使用循环**。有时你不需要检查条件，但这样做总是安全的；尽管这样做并会让你无忧。

然而，这段代码有一个 Bug，是上述提到的两个问题中的第二个。你能看到吗？它似乎有些……（文本截断）

