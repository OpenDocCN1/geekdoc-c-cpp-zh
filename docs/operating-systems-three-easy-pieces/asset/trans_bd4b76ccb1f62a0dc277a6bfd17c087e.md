

# 信号量

```
sem_t s;

void *child(void *arg) {
    printf("child\n");
    sem_post(&s); // signal here: child is done
    return NULL;
}

int main(int argc, char *argv[]) {
    sem_init(&s, 0, X); // X 应该是什么?
    printf("begin\n");
    pthread_t c;
    pthread_create(&c, child, NULL);
    sem_wait(&s); // wait for child
    printf("end\n");
    return 0;
}
```

![](img/133d518e3f69f4caaead32c569ae6c49_430_0.png)

所以它可以从其中删除一个元素。在这种用法模式中，我们经常会发现一个线程在等待某些事情，而另一个线程让这些事情发生并信号该事情已经发生，从而唤醒该线程。因此，我们是将信号量作为一种排序原语（类似于我们之前使用条件变量）。

一个简单的例子如下。想象父线程创建另一个线程，然后等待它完成执行（图 31.6）。当这个程序运行时，我们希望看到以下输出：

parent: begin
child
parent: end

问题是于，如何使用信号量来实现这种效果；事实证明，答案相对容易理解。如代码所示，父线程调用 `sem_wait()`，子线程调用 `sem_post()` 来等待子线程完成执行的条件变为真。然而，这引发了一个问题：这个信号量的初始值应该是多少？

（再次思考一下，不要急着往下看）
答案显然是，信号量的值应该设置为0。有两种情况需要考虑。首先，假设父线程创建了子线程但子线程尚未运行（即它位于等待队列中而不是运行）。在这种情况下（图 31.7，第 394 页），父线程会在子线程调用 `sem_post()` 之前调用 `sem_wait()`；我们希望父线程等待子线程运行。这种情况发生的唯一可能是信号量的值不大于 0；因此，0 是初始值。父线程运行，信号量递减（变为 -1），然后等待（睡眠）。当子线程最终运行时，它将调用 `sem_post()`，信号量的值增加到 0 并唤醒父线程，父线程随后从 `sem_wait()` 返回并结束程序。

# 信号量

| Val | Parent | State | Child | State |
|---|---|---|---||-|
| 0 | create (Child) | Run | (Child exits, can run) | Ready |
| 0 | call sem_wait() | Run | | Ready |
| -1 | decr sem | Run | | Ready |
| -1 | (sem<0)→sleep | Sleep | child runs | Run |
| -1 | Switch→Child | Sleep | call sem_post() | Run |
| 0 | | Sleep | inc sem | Run |
| 0 | | Sleep | wake (Parent) | Run |
| 0 | | Ready | sem.post() returns | Run |
| 0 | sem_wait() returns | Ready | Interrupt→Parent | Ready |

图 31.7: 线程轨迹：父线程等待子线程（情况 1）

| Val | Parent | State | Child | State |
|---|---|---|---||-|
| 0 | create (Child) | Run | (Child exits; can run) | Ready |
| 0 | Interrupt→Child | Ready | child runs | Run |
| 1 | | Ready | call sem_post() | Run |
| 1 | | Ready | inc sem | Run |
| 1 | | Ready | wake (nobody) | Run |
| 1 | | Ready | sem.post() returns | Run |
| 1 | parent runs | Run | Interrupt→Parent | Ready |
| 1 | call sem_wait() | Run | | Ready |
| 0 | (sem≥0)→awake | Run | | Ready |
| 0 | decr sem | Run | | Ready |
| 0 | sem_wait() returns | Run | | Ready |

图 31.8: 线程轨迹：父线程等待子线程（情况 2）

第二种情况（图 31.8）发生在子线程在父线程有机会调用 `sem_wait()` 之前运行完成。在这种情况下，子线程会先调用 `sem_post()`，将信号量的值从 0 增加到 1。当父线程有机会运行时运行时，它将调用 `sem_wait()` 并发现信号量的值为 1；父线程将值减1（变为 0）并从 `sem_wait()` 返回无需等待，同样实现了预期的效果。

# 31.4 生产者/消费者（边界缓冲区）问题

我们在本章中确认的下一个问题被称为生产者/消费者问题，或者有时称为边界缓冲区问题 [D72]。这个问题在上一章关于条件的章节中有详细描述；详细信息请参阅该章节。

# 信号量

# 旁注：设置信号量的值

我们现在已经看到了两个初始化信号量的例子。在第一种情况下，我们将值设置为 1，将信号量作为锁；在第二种情况下，将其设置为 0，将信号量用于排序。那么信号量初始化的通用规则是什么呢？多亏 Kivowitz，一种简单的思考方法是考虑你在初始化后愿意给出的资源数量。对于锁，这个值是 1，因为你愿意在初始化后立即将其锁定（给出去）。对于排序情况，值是 0，因为在开始时没有东西可以给出；当线程完成时，值增加到 1。尝试对未来的问题进行这种思考，或许会有帮助。

# 第一次尝试

我们解决问题的第一次尝试引入了两个信号量 `empty` 和 `full`，它们分别用于指示缓冲区已被清空或填充。在这个例子中，生产者首先等待缓冲区为空以便放入数据，而消费者同样等待缓冲区被填充。让我们假设 MAX=1（只有一个缓冲区），并看看这是否有效。再次假设有两个线程，一个生产者和一个消费者。检查一个单 CPU 的特定场景。假设消费者首先运行。因此，消费者将调用 `sem_wait(&full)`。由于 `full` 被初始化为 0，它将递减 `full`（变为 -1），阻塞生产者。如果生产者被中断并开始运行，它将从 `sem_wait(&empty)` 返回。由于 `empty` 被初始化为 MAX（在这种情况下为 1），生产者继续执行 P3 并调用 `sem_post(&full)` 将 `full` 的值从 -1 变为 0 并唤醒消费者。在这种情况下，可能会发生这种情况：如果生产者继续运行，它将循环并再次命中 P1。然而，此时它会阻塞，因为空信号量的值为 0。如果生产者被中断开始运行，它将从 `sem_wait(&full)`（C1）返回，发现缓冲区已满并消费它。在任何情况下，我们都实现了预期的行为。

你可以用更多线程尝试这个示例（例如多个生产者和多个消费者）。应该是有效的。

```
int buffer[MAX];
int fill = 0;
int use = 0;

void put(int buffer) {
    buffer[fill] = value; // F1
    fill = (fill + 1) % MAX; // F2
}

int get() {
    int tmp = buffer[use]; // G1
    use = (use + 1) % MAX; // G2
    return tmp;
}
```
图 31.9: Put 和 Get 函数

```
sem_t empty;
sem_t full;

void *producer(void *arg) {
    int i;
    for (i = 0; i < loops; i++) {
        sem_wait(&empty); // P1
        put(i);           // P2
        sem_post(&full);  // P3
    }
}

void *consumer(void *arg) {
    int i, tmp = 0;
    while (1) {
        sem_wait(&full); // C1
        tmp = get(&empty); // C2
        sem_post(&empty);  // C3
        printf("%d\n", tmp);
    }
}

int main(int argc, char *argv[]) {
    sem_init(&empty, 0, MAX); // MAX 个空
    sem_init(&full, 0, 0);   // 0 个满
}
```
图 31.10: 添加满和空条件

```
void *producer(void *arg) {
  int i;
  for (i = 0; i < loops; i++) {
    sem_wait(&mutex);    // P0 (新增行)
    sem_wait(&empty);     // P1
    put(i);               // P2
    sem_post(&full);      // P3
    sem_post(&mutex);     // P4 (新增行)
  }
}

void *consumer(void *arg) {
  int i;
  for (i = 0; i < loops; i++) {
    sem_wait(&empty);     // C0 (新增行)
    sem_wait(&full);      // C1
    int tmp = get();      // C2
    sem_post(&empty);     // C3
    sem_post(&mutex);     // C4 (新增行)
    printf("%d\n", tmp);
  }
}
```
图 31.11: 添加互斥锁（错误地）

# 解决方案：添加互斥锁

如你所见，我们在这里得到了`互斥`。缓冲区索引的增加操作是一个临界区域，必须经过小心保护。让我们使用我们的二进制信号量朋友添加一些锁。图 31.11 显示了我们的尝试。

正如“新增行”注释所示，我们在代码的整个 `put()`/`get()` 部分周围添加了一些锁。这似乎是正确的想法，但它同样不起作用。为什么？为什么会发生死锁？花点考虑一下；尝试找到产生死锁的情况。程序发生死锁必须经过哪些步骤序列？

