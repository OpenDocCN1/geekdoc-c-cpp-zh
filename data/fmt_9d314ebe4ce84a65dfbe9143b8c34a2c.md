
### 5.3.1 Pthreads 简介

每个线程都可能运行在不同的处理器核心上。在第 3 行，程序定义了 `pthread_t` 类型的变量。Pthread 库将使用这些变量访问关于线程的信息。关于创建线程的后续信息可以通过 `thread1`、`thread2` 或 `thread3` 获取。每个线程都有自己的栈。这个栈用于存储线程执行的函数所定义的局部变量。当线程进行函数调用时，返回地址会被推入其栈中。

在第 14 行，`print_message()` 函数打印 `ss` 的值，它是指向线程栈位置的指针。三个线程的输出如下：

第 5 章 线程与共享内存

```c
ss = 0x4173bf90
ss = 0x4193cf90
ss = 0x41b9cf90
```

这些地址与栈地址不同：它们不像第 4.4.1 节中那样以 `0x7fff` 开头。这些地址属于动态内存区域。在创建线程期间，每个线程都会在动态内存中被分配一个线程栈。

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

`pthread_spin_init(&spinlock, PTHREAD_PROCESS_PRIVATE);`

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

### 5.3.2 线程创建的开销

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

# 第 5 章 线程与共享内存

```
5.57948e+06
5.06503e+06
```

周期的中位数为 78,242。

创建和销毁 Pthreads 的典型开销似乎略*小于* $10^6$ 个周期。考虑到内核使用的每个进程描述符几乎占用 6 KB，这个数字是不合理的。创建线程的成本会随系统而异，但在许多不同的系统上，这些数字在定性上是相同的。这里使用的带有四个核心的 3.4 GHz AVX 计算机只有一个处理器封装。在具有多个处理器的计算机上，每个核心创建一个线程的开销预计可能会更高。

然而，在四核 3.4 GHz AVX 计算机上，创建三个线程的开销可能会遇到数百万个周期的概率比在拥有数十个核心的机器上大得多，即使处理器核心被分在两个封装中。在四核计算机上，线程等待某些其他进程的时间片耗尽的概率比在 12 核计算机上更高。

### 5.3.3 使用 Pthreads 的并行区域

本节从一个简单的 OpenMP 程序开始。该 OpenMP 程序在两个并行区域之间交替。在第一个并行区域中，每个线程运行一个名为 `addone()` 的函数。在第二个并行区域中，每个线程运行一个名为 `addtwwo()` 的函数。

在节的后部分，并行区域用纯 C 实现，除了创建和启动 Pthreads 之外。第二和第三种实现分别使用了自旋锁和互斥锁。最后的实现使用了条件变量。

所有四种实现的基本思想如下：如果线程数为 $n$，包括主线程，主线程首先创建 $n-1$ 个工作线程。工作线程在完成任务不会退出，而是等待主线程向它们发送更多工作。线程只有在主线程告诉它们时才会退出。

对应 OpenMP 程序的并行区域，主线程告诉工作线程交替执行 `addone()` 和 `addtwwo()`。主线程本身交替执行这两个函数。

一眼表 5.6 已经显示了一些问题。自旋锁和互斥锁的实现看起来非常相似。这是由于我们的实验设置相当简单。

## 5.3. Pthreads 简介

| 线程 | 2 | 3 | 4 | 8 |
|---|---|---|---|---|
| OpenMP (gcc++) | 1,400 | 1,700 | 2,100 | 40,000 |
| 纯 C | 720 | 975 | 1,200 | * |
| 自旋锁 (随机) | 760 | 2,000 | 4,200 | |
| 互斥锁 | 900 | 2,200 | 6,500 | $9.2 \times 10^7$ |
| 条件变量 | 30,000 | 28,000 | 9,000 | 18,000 |

表 5.6：进入和退出并行区域的周期开销。所有测量均在一台 3.4 GHz 四核 AVX 计算机上进行（全称见表 A.1）。

如果线程在并行区域内执行复杂的函数，这两种实现看起来会有所不同。

C 和自旋锁实现不会自愿让出处理器核心。在我们的设置中，互斥锁也是如此。结果是，当线程数大于核心数时，所有三种实现都是高度浪费的。

在条件变量实现中，线程会优雅地让出 CPU。因此，当线程数大于核心数时，它是效率最高的。

奇怪的是，条件变量实现在四个或八个线程时比两个线程快，而两个线程又比一个线程快（见表 5.6）。理解这个谜团的解释非常重要，因为它可能发生在几乎任何程序中。解释（TLB 刷新）将在后文给出。

gcc++ 实现 OpenMP 也仅在进入并行区域时创建线程。总的来说，它看起来比我们所有的实现都要好。进入第一个 OpenMP 并行区域代价很高，因为要创建线程。如果线程数在并行区域之间变化，并行区域将不断受到相同开销的影响。

C 实现强调了缓存一致性的核心作用，这对于多线程编程是至关重要且基础的。从缓存传播写入可能会导致巨大的开销。C 实现还引入了内存屏。

## 一个简单的 OpenMP 程序

在即将列出的程序中，两个 OpenMP 并行区域交替调用以下函数：

```c
void addone(void *arg){
  long *p = (long *)(arg);
  *p += 1;
}
void addtwo(void *arg){
  long *p = (long *)(arg);
  *p += 2;
}
```

这些函数接收一个强制转换为 `void *` 的 long 指针，解引用它，然后在 long 类型的位置加 1 或 2。直接加 1 和 2 而不通过调用通过指针工作的函数会更简单。OpenMP 并行区域调用这些函数是为了保持与 Pthread 实现的紧密类比。Pthread 实现也使用了这两个函数。

这是带有两个并行区域的 OpenMP 程序。

```c
void ompmaster(long *list, int nthreads, int count){
  for(int i=0; i < count; i++){
    #pragma omp parallel num_threads(nthreads-1)
    shared(list)
    {
      int j = omp_get_thread_num();
      addone((long *)(list+j));
    }
    #pragma omp parallel num_threads(nthreads-1)
    shared(list)
    {
      int j = omp_get_thread_num();
      addtwo((long *)(list+j));
    }
  }
}
```

该程序有两个并行区域，其中一个并行区域对 `list[]` 的项加 1。线程 ID 由 `omp_get_thread_num()` 返回。另一个并行区域使用 `addtwo()` 对相同的项加。由于并行区域在一个迭代 `count/2` 次的循环中，调用 `ompmaster` 的效果是根据线程数加3。

## 5.3. Threads 简介

### C 语言并行区域

第一个实现对 Pthreads 的使用极少。以下定义是基础：

```c
typedef void (*fnlist_t[threads])(void *);
typedef void *arglist_t[threads];
volatile fnlist_t fnlist;
volatile arglist_t arglist;
volatile long work_count[threads];
volatile long done_count[threads];
```

这段代码定义了两个类型 `fnlist` 和 `arglist` 以及四个变量。这里 `threads`（定义未给出）等于线程数。`list_t` 类型是带有单个 `void *` 参数的函数数组。`arglist_t` 类型是 `void *` 指针数组。

### 工作函数

这四个 `volatile` 变量供工作线程与管理器进行通信。主线程设置 `fnlist[tid]` 和 `arglist[tid]` 以告诉标识为 `tid` 的线程应该执行哪个函数以及传递什么参数。例如，将 `fnlist[tid]` 设置为 `addone` 以要求标识为 `tid` 的工作线程执行本节之前的 `addone()` 函数。

主线程使用数组 `work_count[tid]` 告诉标识为 `tid` 的工作线程分配了多少工作。工作线程使用 `done_count[tid]` 告诉管理器它完成了多少工作。

用于主线程和工作线程之间通信的四个数组确保了每次引用都会生成加载或存储指令。特别是，编译器不会将这些任何项分配给寄存器，这会干扰管理器和工作线程之间的通信。

使用 `pthread_create()` 创建的线程都从一个接收指针作为参数并返回指针的函数开始执行。工作线程从以下函数开始：

```c
void *worker(void *arg){
    int tid = *((int *)arg);
    while(1){
        while(work_count[tid] == done_count[tid]);
        if(work_count[tid]==done_count[tid]+1){
```
