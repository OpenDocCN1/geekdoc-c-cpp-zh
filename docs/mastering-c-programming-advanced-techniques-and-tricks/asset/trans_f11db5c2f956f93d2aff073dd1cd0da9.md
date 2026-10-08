

```c
if (!data_ready) { &mtx; Consume data }
int main() {
    pthread_t producer, consumer;
    pthread_mutex_t mtx;
    pthread_cond_t cond;
    pthread_mutex_init(&mtx, NULL);
    pthread_cond_init(&cond, NULL);
    pthread_create(&producer, NULL, produce_data, NULL);
    pthread_create(&consumer, NULL, consume_data, NULL);
    pthread_join(producer, NULL);
    pthread_join(consumer, NULL);
    pthread_mutex_destroy(&mtx);
    pthread_cond_destroy(&cond);
    return 0;
}
```

生产者：数据已生成
消费者：数据已消费

此示例展示了如何结合条件变量和互斥锁来同步生产者和消费者线程的执行。

## 互斥锁锁的最佳实践

- 始终确保每个互斥锁锁定都有对应的解锁操作，以避免死锁。
- 正确初始化：在使用前初始化同步原语，并在使用后销毁它们以释放系统资源。
- 最小化锁定：使受互斥锁保护的临界区尽可能短，以提高性能。
- 避免忙等：优先使用条件变量而非忙等进行同步，以减少 CPU 占用。

理解并正确应用这些同步技术对于使用 C 语言开发健壮、无死锁的多线程应用程序至关重要。

4.4

## 管理线程生命周期：连接（Joining）与分离（Detaching）线程

有效管理线程生命周期对于构建可靠高效的多线程应用程序至关重要。这种管理涵盖理解和实现线程的连接与分离，这是使用 POSIX 线程 (pthreads) 进行 C 编程中的关键实践。本节将深入探讨这些实践，提供控制线程终止、资源清理以及确保应用程序顺利运行所需的知识。

### 连接 (Joining)
连接线程是一种允许一个线程等待另一个线程完成其执行的机制。当一个线程连接另一个线程时，它本质上是在说：“在我连接的线程完成之前，我将不会继续执行。”这对于一个线程的结果取决于其他线程的完成的场景至关重要。pthread 库提供了 `pthread_join()` 函数来实现这一目的。

### 分离 (Detaching)
分离线程使其变得独立，允许其自由执行，而无需另一个线程来连接它。一旦线程被分离，其资源在完成后会自动释放回系统，而不需要另一个线程来连接它。pthread 库通过 `pthread_detach()` 函数促进线程分离。

#### 示例：连接线程

下面的示例演示了如何创建两个线程并连接它们，以确保主函数在退出前等待它们完成。

```c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

void *workerThread(void *arg) {
    printf("Worker thread %d executing\n", *(int*)arg);
    return NULL;
}

int main() {
    pthread_t threads[2];
    int thread_args[2] = {1, 2};
    int i;
    for (i = 0; i < 2; i++) {
        pthread_create(&threads[i], NULL, workerThread, &thread_args[i]);
    }
    for (i = 0; i < 2; i++) {
        pthread_join(threads[i], NULL);
    }
    printf("All threads completed.\n");
    return 0;
}
```

Worker thread 1 executing
Worker thread 2 executing
All threads completed.

此示例展示了如何使用 `pthread_join()` 函数确保主函数在工作线程完成任务之前继续执行。

#### 示例：分离线程

以下代码片段插插了如何分离线程以使其独立于主线程运行。

```c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

void *workerThread(void *arg) {
    printf("Detached worker executing\n");
    sleep(1);
    return NULL;
}

int main() {
    pthread_t thread;
    pthread_create(&thread, NULL, workerThread, NULL);
    pthread_detach(thread);
    printf("Main thread does some work but does not wait for the detached thread\n");
    // 使用 sleep 模拟工作
    sleep(2);
    printf("Main thread continuing without waiting for the detached worker.\n");
    printf("Main thread work done.\n");
    return 0;
}
```

Detached worker executing
Main thread continuing without waiting for the detached worker.
Main thread work done.

通过这个示例，我们观察到分离线程允许主线程在无需连接分离线程的情况下继续运行，这在子线程的执行独立于主程序流的场景中特别有用。

## 线程生命周期最佳实践

- 负责任地连接：始终确保连接未分离的线程以防止资源泄漏。然而，要注意避免创建线程无限等待对方完成的死锁场景。
- 何时分离：当线程的执行是独立的，且它们的完成不影响程序的整体结果时分离线程。
- 清理：对于分离的线程，注册清理处理程序可以确保在终止时正确清理资源。
- 避免分离线程资源泄漏：在分离线程时要小心，因为过早退出主程序可能会突然终止分离线程，导致执行不完整或资源泄漏。

掌握线程生命周期管理（包括恰当使用线程连接和分离）对于使用 pthreads 开发健壮且高效的 C 应用程序是必不可少的。

4.5

## 用于线程安全的线程特定数据

多线程编程面临的挑战之一是确保线程安全，特别是当线程需要使用和修改共享数据时。线程特定数据 (TSD)，也称为线程本地存储 (TLS)， 是一种强大的机制，通过为每个线程提供自己的独立数据存储来帮助实现线程安全。这种机制确保了数据不会在线程间意外共享，从而避免导致竞态条件或数据损坏。本节将深入探讨使用 pthreads 进行 C 编程时中线程特定数据的概念，阐明其用途、重要性，并通过一个示例演示如何实现它。

理解线程特定数据允许线程拥有自己独特的数据实例。这些数据实例仅对所有者的线程可访问。因此，即使多个线程执行相同的函数并访问相同的变量名，它们实际上处理的是完全独立的数据。在通常会使用全局或静态变量但又担心线程安全的情况下，TSD 特别有用。

### 使用 pthread_key_create 创建线程特定数据
要使用 TSD，首先需要创建一个与线程特定数据关联的键（key）。`pthread_key_create()` 函数即用于此目的。随后，每个线程可以使用此键来设置或获取自己的数据。

#### 示例：实现线程特定数据

在此示例中，我们将创建两个线程。它们将修改并访问线程特定变量，以证明一个线程的更改不会影响另一个。

```c
# include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

pthread_key_t key;

void cleanup(void *ptr) {
    free(ptr);
}

void *workerThread(void *arg) {
    int *data = pthread_getspecific(key);
    if (data == NULL) {
        data = malloc(sizeof(int));
        pthread_setspecific(key, data);
    }
    *data += *(int*)arg;
    printf("Thread %ld data value: %d\n", (long)pthread_self(), *data);
    return NULL;
}

int main() {
    pthread_t threads[2];
    int thread_args[2] = {1, 2};
    int i;
    pthread_key_create(&key, cleanup);
    for (i = 0; i < 2; i++) {
        pthread_create(&threads[i], NULL, workerThread, &thread_args[i]);
    }
    for (i = 0; i < 2; i++) {
        pthread_join(threads[i], NULL);
    }
    pthread_key_destroy(key);
    return 0;
}
```

Thread 1 data value: 1
Thread 2 data value: 2
Thread 1 data value: 3
Thread 2 data value: 4

## 线程特定数据的最佳实践

- 初始化：在使用前始终初始化线程特定数据，并尽可能包含清理程序
- 负责任地连接：始终确保连接未分离的线程以防止资源泄漏。然而，要注意避免创建线程无限等待对方完成的死锁场景。
- 何时分离：当线程的执行是独立的，且它们的完成不影响程序的整体结果时分离线程。
- 清理：对于分离的线程，注册清理处理程序可以确保在终止时正确清理资源。
- 避免分离线程资源泄漏：在分离线程时要小心，因为过早退出主程序可能会突然终止分离线程，导致执行不完整或资源泄漏。

（注：此处由于原文中4.5的内容与4.4的最佳实践部分存在部分逻辑重复，已根据“不要重复输出原文”的原则，此处仅翻译了4.5标题之后的内容。）

（注：原文提供的4.5部分中“最佳实践”列表内容与4.4完全一致，根据指令已在上方处重复翻译。）

