
pthread_t pthread[threads-1];

这里唯一的区别是锁数组 `[]` 的类型是 `pthread_mutex_t` 而不是 `pthread_spin_t`。

下面列出了互锁实现中 `worker()` 和 `assign()` 的定义。

```c
void *worker(void *arg) {
    int tid = *((int *) arg);
    while (1) {
        pthread_mutex_lock(mtx+tid-1);
        if(workflag[tid-1]) {
            (*fnlist[tid-1])(arglist[tid-1]);
            workflag[tid-1] = 0;
            pthread_cond_signal(cv_free+tid-1);
        }
        pthread_mutex_unlock(mtx+tid-1);
    }
    return NULL;
}

void assign(int i, int tid, long *list) {
    int j = tid-1;
    while (1) {
        pthread_mutex_lock(mtx+j);
        if(workflag[j]==0) {
            fnlist[j] = (i%2==0) ? addone : addtwo;
            arglist[j] = (void *)(list+tid);
            workflag[j] = 1;
            pthread_cond_signal(cv_work+j);
            pthread_mutex_unlock(mtx+j);
            return;
        }
        pthread_mutex_unlock(mtx+j);
    }
}
```

## Pthread 库函数

`pthread_spin_lock()` 和 `pthread_spin_unlock()` 已被 `pthread_mutex_lock()` 和 `pthread_mutex_unlock()` 替换。在互斥锁的加解锁期间，内存的本地视图会被序列化，并通过内存屏（memory fence）对其他线程可见，编译器会负责提交存储在寄存器中的变量。全局变量都不需要指定为 `volatile`。我们像以前一样省略了 `spawn_workers()` 和 `shutdown_workers()` 的定义。

## 互斥实现的成本

表 5.6 显示，在四核计算机上，使用互斥实现的并行区域的平均成本为：两个线程时为 900 个周期，三个线程时为 2200 个周期，四个线程时为 5000 个周期。该成本与自旋锁实现相当，且略差。纯 C 实现要快得多。如果以经典方式实现互斥锁，尝试获取不可用锁的进程会被操作系统睡眠。当锁被释放时，该互斥锁队列中处于睡眠的进程之一会被唤醒。使用经典互斥锁，并行区域的平均成本会更高。Linux 上 pthread 库中的互斥锁并不是以经典方式实现的。它们使用 Linux 系统调用支持的 `futex` 实现。使用 `futex` 实现的互斥锁在存在竞争时完全不会进入内核。在我们的设置中，每个获取锁的线程释放锁的速度非常快，竞争线程很少睡眠。如果一个线程持有锁长时间，互斥锁会将竞争线程置睡眠。

## 使用条件变量的并行区域

使用条件变量，可以获得管理线程分配工作与工作线程执行该工作之间更可预测的交替。使用条件变量时，当工作分配给工作线程时，管理线程会向该线程发送信号。工作线程在寻找工作时不会反复地锁定和解锁互斥锁，而是等待信号。相应地，工作线程在完成工作后会向管理线程发送信号，这意味着管理线程不需要反复锁定和解锁来检查工作线程是否空闲。区域条件变量实现中的全局变量如下：

```c
void (*fnlist[nthreads])(void);
void *arglist[nthreads];
int workflag[nthreads];
pthread_mutex_t wrlock[nthreads];
pthread_cond_t cv_work[nthreads];
pthread_cond_t cv_free[nthreads];
pthread_t thrd[nthreads];
```

变量 `fnlist[]`、`arglist[]`、`workflag` 的意义与互斥实现中的相同。管理线程设置 `fnlist[tid]` 和 `arglist[tid]` 以让工作线程知道在哪个参数上执行哪个函数。正如本节考虑的所有并行区域实现一样，工作线程被要求在 `addon()` 和 `addtwo()` 之间交替。退出函数的定义如下：

```c
void exitfn(void *arg) {
    int tid = *((int *)arg);
    pthread_mutex_unlock(wrlock+tid-1);
    pthread_exit(NULL);
}
```

因为工作线程会执行 `exitfn()` 以及它被要求执行的其他函数，所以在在锁定互斥锁 `wrlock[tid]` 后，它必须在退出前解锁。条件变量 `cv_work[]` 用于管理线程告诉工作线程有工作要做。条件变量 `cv_free[]` 用于工作线程告诉管理线程它们已完成分配给它们的任务。条件变量也与互斥锁配合使用。条件变量 `cv_work` 和 `cv_free` 与互斥锁协调。工作线程通过以下函数获取控制：

```c
void *worker(void *arg) {
    int tid = *((int *)arg);
    while (1) {
        pthread_mutex_lock(wrlock+tid-1);
        if(workflag[tid-1])
            pthread_cond_wait(cv_work+tid-1, wrlock+tid-1);
        (*fnlist[tid-1])(arglist[tid-1]);
        workflag[tid-1] = 0;
        pthread_cond_signal(cv_free+tid-1);
        pthread_mutex_unlock(wrlock+tid-1);
    }
    return NULL;
}
```

工作线程锁定 `wrlock[tid-1]`，在第 4 行检查 `workflag[tid-1]`，这是工作线程和管理线程访问的共享内存区域。如果没有工作要做，它会在第 5 行在 `cv_work+tid-1` 上等待。库函数 `pthread_cond_wait()` 取一个条件变量指针和一个互斥锁指针。它在睡眠前解锁互斥锁，这意味着工作线程在寻找工作时不会竞争锁。这种在进入睡眠前解锁互斥锁是条件变量语义的核心元素。

## 5.3. Pthreads 简介

管理线程执行的对应函数定义如下。

```c
void manager(long *list, int count) {
    for(int i=0; i < count; i++) {
        for(int j=0; j < nthreads-1; j++) {
            pthread_mutex_lock(wrlock+j);
            if(workflag[j]==1)
                pthread_cond_wait(cv_free+j, wrlock+j);
            fnlist[j] = (i%2==0) ? addone : addtwo;
            arglist[j] = (void *)(list+j+1);
            workflag[j] = 1;
            pthread_cond_signal(cv_work+j);
            pthread_mutex_unlock(wrlock+j);
        }
    }
    if(i%2==0)
        addone((void *)list);
    else
        addtwo((void *)list);
}
```

管理线程在锁区域外执行其工作，但指示工作已分配的信号 `cv_work` 必须在锁区域内。如果在锁区域外发送信号，可能会在工作线程获取并验证 `workflag[tid-1]` 为 0 之后、调用 `pthread_cond_wait()` 等待 `cv_work[tid-1]` 之前到达如果发生这种情况，信号将丢失导致程序死锁。管理线程在并行区域外执行其工作，调用 `add()` 或 `addtwo()`。

```c
void spawn_workers() {
    static int tidlist[nthreads-1];
    for(int i=0; i < nthreads-1; i++) {
        workflag[i] = 0;
        tidlist[i] = i+1;
        pthread_mutex_init(wrlock+i, NULL);
    }
}
```
