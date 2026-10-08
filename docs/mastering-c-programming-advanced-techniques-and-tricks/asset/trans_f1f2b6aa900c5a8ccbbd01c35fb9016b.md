

# C语言多线程基础

在C语言中的多线程是旨在构建高性能、高效应用的开发者来说的一个核心概念。通过多线程，程序可以并发执行多个线程，从而更好地利用系统资源并加快执行速度。本节将深入探讨C语言中多线程的基础知识，利用 POSIX 线程 (Pthreads) 库，这是一块用于创建、管理和同步线程的标准线程库。

POSIX 线程（通常称为 Pthreads）提供了一组用于在C中创建和操作线程的函数。它在不同的类Unix 操作系统上提供了一种可移植的方法。对于寻求实现多线程的C语言程序员来说，理解 Pthreads 至关重要。

### 创建线程
创建新线程的核心函数是 `pthread_create()`。该函数需要四个参数：线程标识符的指针、任何线程属性、线程将运行的函数以及传递给该函数的参数。

### 合并 (Joining)
为了确保父线程等待子线程完成，使用了 `pthread_join()`。当父线程在继续执行之前需要子线程的输出时，这种机制是关重要的。

### 同步 (Synchronizing)
线程之间的协调对于避免竞态条件和确保数据完整性至关重要。Pthreads 提供了互斥锁（mutexes）和线程间信号条件变量（condition variables）等机制。

### 终止线程 (Terminating Threads)
线程可以通过从线程函数返回、调用 `pthread_exit()` 或被另一个线程取消来终止。

示例：C语言简单的多线程程序

让我们来看一个简单的示例来演示C中的多线程。该程序创建两个线程，每个线程向标准输出打印一条消息。

```c
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>

void *PrintHello(void *arg) {
    long tid = (long)arg;
    printf("Hello World! It's me, thread #%ld!\n", tid);
}

int main () {
    pthread_t threads[2];
    int rc;
    for (long t = 0; t < 2; t++) {
        rc = pthread_create(&threads[t], NULL, PrintHello, (void *)t);
        if (rc) {
            printf("Error creating thread");
        }
    }
    /* Wait for all threads to complete */
    for (long t = 0; t < 2; t++) {
        pthread_join(threads[t], NULL);
    }
    return 0;
}
```

main中: 创建线程
main中: 创建线程 1
Hello World! It's me, thread #0!
Hello World! It's me, thread #1!
main中: 所有线程已完成

此示例演示了在C语言中使用Pthreads创建、运行和合并线程。

### 线程中的挑战
- 访问共享资源的代码区域必须小心管理，以避免竞态条件。
- 当多个线程等待彼此以释放资源时，可能会发生死锁。
- 创建和管理大量线程会引入开销和复杂性。

由Pthreads库促进的C语言多线程是开发高效性能应用的强大技术。通过理解这些基本概念并应用这些技术，开发者可以有效利用并发性。

# 4.2

# 使用pthreads创建线程：基础与实践

在C语言并发编程领域，POSIX线程（或pthreads）的使用是实现多线程的一种突出方法。本节阐述了使用pthreads创建线程的基础元素和最佳实践，强调了线程生命周期管理、线程间数据共享以及缓解竞态条件和死锁等常见陷阱的必要性。

### 理解线程
pthreads库提供了丰富的线程创建、终止和同步函数。掌握C线程的关键在于深入理解这些功能以及它们在执行环境中如何交互。

### thread_create()
pthreads的核心是`pthread_create()`函数，它初始化一个新的线程。该函数原型如下：

```c
int pthread_create(pthread_t *thread, const pthread_attr_t *attr,
               void (*start_routine) (void *), void *arg);
```

参数为：
- `thread`: 线程标识符的指针，通常用于后续引用。
- `attr`: 指定线程属性。
- `start_routine`: 执行函数的指针。
- `arg`: 用于函数的参数。

成功调用 `pthread_create` 返回0，新创建的线程在指定的程序开始执行。

示例：基础线程创建与执行

以下示例演示了执行基本任务的线程创建和执行。

```c
#include <stdio.h>
#include <pthread.h>

// 生成输出的线程函数
void *PrintMessage(void *arg) {
    char *message = (char *)arg;
    printf("%s\n", message);
}

int main () {
    pthread_t thread;
    int rc;
    char *msg = "Hello, World!";
    rc = pthread_create(&thread, NULL, PrintMessage, (void *)msg);
    if (rc) {
        printf("Error creating thread");
    }
    pthread_join(thread, NULL);
    return 0;
}
```

Hello, World!

此简单示例放大了通过`pthread_join()`等待线程完成的过程——定义线程函数、带参数创建线程。这种演示的方法为创建更复杂的多线程应用奠定了基础。

### 线程中的最佳实践
- **合并 (Joining)**: 始终使用`pthread_join()`合并已创建的线程。防止资源泄漏并确保主程序等待线程完成。
- **错误 (Error)**: 始终检查创建线程的返回值。处理错误以防止意外行为。
- **管理线程 (Managing Thread)**: 在线程传递参数或处理共享数据时要格外。使用互斥锁或其他同步技术管理对共享资源的访问。
- **资源 (Resource)**: 在创建多个线程时注意资源分配和限制。过度的线程创建会导致性能下降或资源耗尽。

使用pthreads封装了C语言并发编程的力量和复杂性。通过仔细应用此处概述的原则和实践，开发者可以有效利用pthreads的能力构建并发应用。

# 4.3

# 同步技术：互斥锁、信号量和条件变量

多线程应用中的同步对于避免竞态条件、死锁和数据损坏等并发问题至关重要。在C编程中，特别是使用pthreads时，有几种同步技术可用：互斥锁、信号量和条件变量。这些技术每种都有不同的用途，并适用于不同的同步问题。

互斥锁（mutual exclusion）是一种授予共享资源独占访问的同步原语。在线程释放互斥锁之前，这确保了修改共享数据的代码区域不会同时执行。

示例：使用互斥锁实现互斥

考虑两个线程增加共享计数器的场景。互斥锁可以确保计数器正确增加而不受干扰。

```c
#include <stdio.h>
#include <pthread.h>

#define NUM_THREADS 2
int counter = 0;
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

void *increment_counter(void *arg) {
    pthread_mutex_lock(&lock);
    counter++;
    pthread_mutex_unlock(&lock);
}

int main() {
    pthread_t threads[NUM_THREADS];
    for (int i = 0; i < NUM_THREADS; i++) {
        pthread_create(&threads[i], NULL, increment_counter, NULL);
    }
    for (int i = 0; i < NUM_THREADS; i++) {
        pthread_join(threads[i], NULL);
    }
    printf("Counter value: %d\n", counter);
    return 0;
}
```

Counter value: 1
Counter value: 2

此示例说明了使用互斥锁来确保计数器变量的独占访问，防止竞态条件。

信号量是互斥锁的通用同步工具。它们维护零到最大值之间的计数，指示资源的可用性。如果线程尝试在信号量为零时增加（post）或减少（wait），它将阻塞，直到计数大于零。

条件变量提供了一种阻塞线程直到某些条件满足的方法。它们通常与互斥锁结合使用，根据共享数据的状态来同步执行流。

示例：使用条件变量进行同步

以下示例演示了使用条件变量同步两个线程，其中一个生产数据，另一个消费数据。

```c
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
int data_ready = 0;

void *producer(void *arg) {
    pthread_mutex_lock(&mtx);
    data_ready = 1;
    pthread_cond_signal(&cond);
    pthread_mutex_unlock(&mtx);
}

void *consumer(void *arg) {
    pthread_mutex_lock(&mtx);
    while (!data_ready) {
        pthread_cond_wait(&cond, &mtx);
    }
    printf("Data received!\n");
    pthread_mutex_unlock(&mtx);
}
```

