
第 5 章 线程与共享内存

```c
ss = 0x4173bf90
ss = 0x4193cf90
ss = 0x41b9cf90
```

这些地址与栈地址不同：它们不像第 4.4.1 节中那样以 0x7fff 开头。这些地址属于动态内存区域。在创建线程期间，每个线程都会在动态内存中被分配一个线程栈。

三个线程打印的地址 `ss` 的值差异约为 2 MB，而我们使用的系统上的最大线程栈大小约为 2 MB。这是很典型的。

## 互斥锁与自旋锁

`print_message()` 函数打印到终端，所有线程共享终端。消息可能会像下面的片段一样乱码：

> Message for thread3Message for thread2
> M_e_s_s_a_g_e_ f_o_r_ t_h_r_e_a_d_2_

每个线程必须将这一块打印语句视为临界区域。互斥锁（Mutex）是 Pthread 库中实现互斥的一种机制。下面的函数使用单个互斥锁来确保一组打印语句一次只由一个线程执行。

```c
pthread_mutex_t mutex=THREAD_MUTEX_INITIALIZER;
void *print_message_mutex(void *arg){
    char *s = (char *)arg;
    char ss[400];
    int l = strlen(s);
    for(int i=0; i < l; i++){
        ss[2*i] = s[i];
        ss[2*i+1] = (s[i]==' ') ? '?' : '_';
    }
    ss[2*l] = '\0';
    pthread_mutex_lock(&mutex);
    printf("%s",s);
    printf("\n");
    printf("%s", ss);
    printf("\n");
    printf("ss = %p \n\n", (void *)ss);
    pthread_mutex_unlock(&mutex);
    return NULL;
}
```

## 5.3. Pthreads 简介

该函数使用的语法非常简单，几乎不需要解释。在第一行中，定义并初始化了一个变量 `mutex`。互斥锁在进入打印语句块之前被锁定，在退出时解锁。

另一种互斥机制是自旋锁（Spinlock）。打印消息函数的自旋锁版本如下：

```c
pthread_spinlock_t spinlock;
void *print_message_spinlock(void *arg){
    char *s = (char *)arg;
    char ss [400];
    int l = strlen(s);
    for(int i=0; i < l; i++){
        ss[2*i] = s[i];
        ss[2*i+1] = (s[i]==' ') ? ',' : ';';
    }
    ss[2*l] = '\0';
    pthread_spin_lock(&spinlock);
    printf("%s", s);
    printf("\n");
    printf("%s", ss);
    printf("\n");
    printf("ss = %p \n\n", (void *)ss);
    pthread_spin_unlock(&spinlock);
    return NULL;
}
```

第一行定义了一个自旋锁但没有对其进行初始化。自旋锁在进入打印语句块之前锁定，在打印完成后解锁。自旋锁由主线程初始化如下：

pthread_spin_init(&spinlock, PTHREAD_PROCESS_PRIVATE);

经典互斥锁的行为上与 Pthread 互斥锁不同，它们引入于计算机早期，那时大多数计算机只有一个处理器。当一个进程尝试锁定经典互斥锁但该锁已锁定时，内核会将该进程置于睡眠状态并调度另一个进程运行。当互斥锁可用可以锁定时，睡眠的进程将被重新唤醒并调度运行。

如果假设每个线程都拥有一个处理器内核，那么自旋锁可能是强制互斥的优选方法。自旋锁不会释放处理器，而在循环中等待直到锁可用。自旋锁通过原子操作使用共享锁变量来实现互斥。

在简单的程序中，Pthread 互斥锁的行为比经典互斥锁更接近自旋锁。在复杂的程序中，Pthread 互斥锁的行为可能类似于经典互斥锁。

## 莱布尼茨级的部分和

我们对 Pthreads 的讨论仅限于打印消息。我们转向莱布尼茨级来说明如何传递多个参数以及如何获取线程计算出的答案。

在下面的代码片段中，线程数量（包括主线程）固定为四个，假设程序运行在四核机器上。只要该数是偶数，它就可以设置为核心数，无论核心数是多少。

```c
const int NTHREADS = 4;
struct leib_stuff{
    int offset;
    int n;
    double sum;
};
```

每个线程接收一个指向 `struct leib_stuff` 的指针。该结构包含三项信息。第一项是该特定线程开始累加莱布尼茨级的起始偏移量。第二项是必须累加的莱布尼茨级项数。第三项供每个线程用于返回其负责的莱布尼茨级部分和。每个线程假设其所占部分和中的所有项的符号相同。因此，线程数必须是偶数。

在早期的示例中，主线程不参与工作线程。主线程与其他线程之间存在某种内在的不对称性。例如，主线程利用用户模式栈，而其他任何线程都无法使用。然而，理想情况是让所有线程（包括主线程）执行完全相同的工作。在本示例中，主线程将累加其负责的莱布尼茨级项。因此，只显式创建了三个线程。

创建的三个线程都通过以下函数获取控制：

```c
void *leibniz(*arg){
    int offset = ((struct leib_stuff*)arg)->offset;
    int n = ((struct leib_stuff*)arg)->n;
    double sum = 0;
    for(int i=offset; i < n; i += 2*i+1)
        sum += 4.0/(2*i+1);
    ((struct leib_stuff*)arg)->sum = sum;
    return arg;
}
```

我们可以像阅读用于单线程执行的函数一样阅读它。它的特殊之处在于参数传递和返回计算和的方式。线程发现其偏移量和项数，并在 `struct leib_stuff` 中的第三项中存入计算的部分和。

主线程也计算其负责的莱布尼茨级和，并累加所有线程的总和。它的定义如下：

```c
double leibsum(int nterms){
    pthread_t t[NTHREADS-1];
    struct leib_stuff info[NTHREADS-1];
    for(int i=1; i < NTHREADS; i++){
        info[i-1].offset = i;
        info[i-1].n = nterms;
        pthread_create(&(t[i-1]), NULL, leibniz, (void *)(info+(i-1)));
    }
    double ans = 0;
    for(int i=0; i < NTHREADS-1; i++){
        void *res;
        pthread_join(t[i], &res);
        ans += info[i].sum;
    }
    return ans;
}
```

## 5.3.2 线程创建的开销

为了找到创建和销毁线程的开销，我们使用下面的简单函数，它执行：

```c
void *adde(void *arg){
    long *p = (long *)arg;
    *p += 1;
    return NULL;
}
```

该函数接收一个指向 long 的指针并将其指向的位置加1。定义的函数负责创建线程并要求它们执行执行 `add()`。

```c
void add_list(long *list, int nthreads){
    pthread_t *plist = new pthread_t[nthreads-1];
    *list += 1;
    for(int i=0; i < nthreads-1; i++)
        pthread_create(plist+i, NULL, adde, (void *)(list+i+1));
    for(int i=0; i < nthreads-1; i++){
        void *result;
        pthread_join(plist[i], &result);
    }
    delete[] plist;
}
```

该函数被多次调用，`nthreads` 为三。在一个具有四核心的3.4 GHz AVX 机器上（见附录表 A.1），有三个进程，两个用于创建线程和一个主线程，每个进程都获得一个内核。每个线程的工作微不足道。在每次调用中，大部分周期都被线程的创建和销毁所消耗。

