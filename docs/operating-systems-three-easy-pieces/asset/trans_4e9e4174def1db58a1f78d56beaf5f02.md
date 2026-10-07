
# 322

# 间隙：线程 API

```c
typedef struct { int a; int b; } myarg_t;
typedef struct { int x; int y; } myret_t;

void *mythread(void *arg) {
    myret_t *rvals = malloc(sizeof(myret_t));
    rvals->x = 1;
    rvals->y = 2;
    return (void *) rvals;
}

int main(int argc, char *argv[]) {
    thread_t *rvals;
    myarg_t args = { 10, 20 };
    pthread_join(p, NULL, mythread, &args);
    printf("returned %d %d\n", rvals->x, rvals->y);
    free(rvals);
    return 0;
}
```

### ### 图 27.2：等待线程完成

其次，如果我们只是传递一个单一值作为参数（例如，一个 `long int`），我们不需要将其封装成参数。图 27.3（第 323 页）展示了一个示例。在这种情况下，情况会简单得多，因为我们不需要在结构体内部封装参数和返回值。

第三，我们应该注意，对于线程如何返回值，必须极其小心。具体来说，不要返回一个指向线程调用栈上分配的内容的指针。如果你这样做了，你认为会发生什么？（思考一下！）这里有一个危险的代码示例，是根据图 27.2 中的示例修改的。

```c
void *mythread(void *arg) {
    myret_t *args = (myret_t *) arg;
    printf("%d %da\n", args->a, args->b);
    myret_t oops; // 分配在栈上：错误
    oops.x = 1;
    oops.y = 2;
    return (void *) &oops;
}
```

在这种情况下，变量 `oops` 被分配在 `mythread` 的栈上。然而，当它返回时，该值会被自动释放（这正是栈如此容易使用的原因，毕竟！），而返回一个指向已释放变量的指针会导致各种糟糕的后果。当然，当你打印你返回的值时，你可能会（但并不一定！）感到惊讶。试一下并亲自发现吧！

操作系统
[版本 1.01]

WWW.OSTEP.ORG

# 间隙

```c
void *mythread(void *arg) {
    long long int value = (long long int) arg;
    printf("%lld\n", value);
    return (void *) (value + 1);
}
```

```c
int main(int argc, char *argv[]) {
    pthread_t p;
    long long int rvalue;
    pthread_create(&p, NULL, mythread, (void *) 100);
    pthread_join(p, (void **) &rvalue);
    printf("%lld\n", rvalue);
    return 0;
}
```

图 27.3：向线程传递更的参数

最后，你可能会发现使用 `pthread_create()` 创建线程后紧接着调用 `pthread_join()` 是一种非常奇怪创建线程的方式。事实上，有一种更简单的方法来解释这个任务；它被称为过程调用。显然，我们将创建多个线程并等待它们完成，否则使用线程根本没有意义。

我们不应该认为所有多线程代码都必须使用 `join` 例程。例如，一个多线程服务器可能会创建若干工作线程，然后使用主线程接受请求并将它们传递给工作线程。这类链接程序可能不需要 `join`。然而，一个创建线程来执行特定任务（并行执行）的并行程序可能会使用 `join` 来确保在退出或移动到计算阶段阶段之前完成所有工作。

# 27.3 锁

除了线程创建和连接之外，POSIX 线程库提供的下一个最有用的函数可能是通过锁为临界区提供互斥的函数。用于此目的最基础的一对例程由以下提供：

```c
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

> 幸运的是，当你编写这样的代码时，gcc 可能会报错，这又是关注编译器警告的另一个原因。

© 2008–19, ARPACI-DUSSEAU

三部曲入门

# 间隙：线程 API

这些例程应该是易于理解和使用的。当你有一段代码是临界区，因此需要保护以确保操作正确运行时，锁是非常有用的。你可能可以想象锁的样子：

```c
pthread_mutex_t lock;
pthread_mutex_lock(&lock);
x = x + 1; // 或者无论你的临界区是什么
pthread_mutex_unlock(&lock);
```

[content]:
[第 362 页]

# 间隙：线程 API

```c
// 保持代码整洁；仅在失败时退出
void Pthread_lock (pthread_mutex_t *mutex) {
  int rc = pthread_mutex_lock(mutex);
  assert(rc == 0);
}
```

图 27.4：一个示例

锁和解锁例程并不是线程库中与锁交互的唯一例程。另外两个关注的例程是：

```c
int pthread_mutex_try_lock(pthread_mutex_t *mutex);
int pthread_mutex_timedlock(pthread_mutex_t *mutex, struct timespec *abs_timeout);
```

这两个被用于获取锁。如果锁已被占用，`trylock` 版本会失败；`timedlock` 版本在超时或获取锁（以先发生的为准）后返回。因此，超时为 0 的 `timedlock` 退化为 `trylock` 情况。

# 27.4 条件变量

任何线程库的另一个主要组件（特别是 POSIX 线程）是条件变量的存在。当线程之间必须进行某种信号传递时（如果一个线程等待另一个线程完成某些操作），条件变量是有用的。程序使用两个主要的例程与此变量交互：

```c
int pthread_cond_wait(pthread_cond_t *cond, pthread_mutex_t *mutex);
int pthread_cond_signal(pthread_cond_t *cond);
```

使用条件变量需要额外一个与此条件相关的锁。在调用上述任何例程时，应该持有该锁。

第一个例程 `pthread_cond_wait()` 让调用线程睡眠，并等待另一个线程信号它，通常当程序中发生了某些该睡眠线程可能关心的变化时。典型的用例如下：

```c
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
```

```c
pthread_mutex_lock(&lock);
while (ready == 0)
  pthread_cond_wait(&cond, &lock);
pthread_mutex_unlock(&lock);
```
