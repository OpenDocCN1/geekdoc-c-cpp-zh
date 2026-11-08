
API 的每个参数解释如下：

- thread 参数是新线程的 ID
- attr 参数指定新线程的属性（将在本章后面讨论）
- 新线程通过调用 start_routine 并以 arg 作为参数开始执行

让我们编译并运行该程序。编译时，应在编译过程中将程序链接到 pthread 库，如下所示：

```
gcc thread1.c -o thread1 -lpthread
```

现在，要运行程序，请在 UNIX 提示符下执行以下命令：

```
./thread1
```

在前面的程序中，我们通过使用指向线程的指针调用了 pthread_create()。在 pthread_create() 调用中，线程属性以 NULL 发送，启动函数指针设置为 thread_function()，并将 thread_params 作为参数传递给 pthread_create()。pthread_create() 成功执行后，主线程和子线程以重叠方式运行，体现了并行性的本质。在 main() 函数中，主线程打印 "In main" 1000 次，子线程打印 "I'm thread" 10000 次。

由于主线程循环 1000 次，而子线程循环 10000 次，主线程将在子线程之前完成执行。这可能导致前面程序中出现一个关键问题。比主线程更晚完成的子线程会作为僵尸线程留在系统中。僵尸线程是一种特殊的线程，它们已经完成执行，但仍存在于活动线程表中。它们无事可做，但由于没有正常退出，它们仍然持有其生命周期内使用的资源。这个问题的解决方案是使用 pthread_join()，它可以正确清理僵尸线程；否则，这种情况无法处理。

从主线程调用 pthread_join() 将使其先等待子线程完成。只有到那时，主线程才能退出。pthread_join() 的语法如下：

```c
int pthread_join (pthread_t thread_id,
                  void **retval);
```

pthread_join() API 等待由 thread_id 标识的线程终止。通常，线程可以在以下情况下终止：

- 线程调用 pthread_exit()。
- 线程从线程函数返回。
- 线程被取消。
- 进程中的线程调用 exit() 函数，或者主线程从 main() 函数返回。这会终止该进程创建的所有线程。

retVal 参数收集来自已终止线程的返回值。如果没有任何要返回的内容，则可以传递 NULL。在多线程环境中，一个进程中的所有线程都是对等线程；因此，在执行周期中，任何线程都可以加入该进程中的另一个线程。

现在，考虑 thread2.c 程序，以理解 pthread_join() 的工作方式：

```c
/* thread2.c - demonstrating the usage of pthread_join */
#include <stdio.h>
#include <pthread.h>

struct thread_args {
    char    name[20];
    int     count;
};

void *thread_function(void *arg);

int
main ()
{
    int             local_counter = 100;
    int             ret         = 0;
    pthread_t       thread;
    struct thread_args  params;

    strcpy (params.name, "I'm thread");
    params.count = 10000;

    ret = pthread_create(&thread, NULL, thread_function, (void*)&params);
    if (ret != 0) {
        fprintf(stderr, "\nthread creation failed\n");
        return 1;
    }

    printf("Output:\n");
    while (local_counter) {
        printf("in main\n");
        local_counter--;
    }

    printf("\nwaiting for thread to finish...\n");
    ret = pthread_join(thread, NULL);
    if (ret != 0) {
        fprintf(stderr, "\nthread join failed\n");
        return 0;
    }
    printf("\nthread joined\n");

    return 0;
}

void *thread_function(void *arg)
{
    struct thread_args  *params = (struct thread_args*)arg;

    while (params->count) {
        printf("%s\n", params->name);
        params->count--;
    }
}
```

在前面的程序中，主线程完成其执行，并等待子线程完成之后才能退出。调用 pthread_join() 时传入了 retVal，其被设置为 NULL。

现在，让我们考虑一种情况：子线程在退出之前向主线程返回某些内容。为此，我们使用 pthread_join() API 的第二个参数，如下面的程序所示：

```c
/* thread3.c - demonstrating returning of args from child thread by pthread_join */
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

struct thread_args {
    int        num1;
    int        num2;
};
void *thread_function_sum(void *arg);
void *thread_function_product(void *arg);

int
main ()
{
    int         count  = 1000;
    int         ret    = 0;
    pthread_t   thread1;
    pthread_t   thread2;
    struct thread_args params;
    void        *thread_result = NULL;

    params.num1 = 5;
    params.num2 = 15;

    ret = pthread_create(&thread1, NULL, thread_function_sum, (void*)&params);
    if (ret != 0) {
        fprintf(stderr, "\nThread creation failed\n");
        return 1;
    }

    ret = pthread_create(&thread2, NULL, thread_function_product, (void*)&params);
    if (ret != 0) {
        fprintf(stderr, "\nThread creation failed\n");
        return 1;
    }

    printf("OUTPUT:\n");

    printf("\nWaiting for threads to finish...\n");
    ret = pthread_join(thread1, &thread_result);
    if (ret != 0) {
        fprintf(stderr, "\nThread join failed\n");
        return 0;
    }
    printf("\nThread1 joined. sum=[%d]\n", *((int*)(thread_result)));

    ret = pthread_join(thread2, &thread_result);
    if (ret != 0) {
        fprintf(stderr, "\nThread join failed\n");
        return 0;
    }
    printf("\nThread2 joined. product=[%d]\n", *((int*)(thread_result)));

    return 0;
}

void *thread_function_sum(void *arg)
{
    struct thread_args  *params = (struct thread_args*)arg;
    int                 *result = (int*)malloc(sizeof(int));

    *result = params->num1 + params->num2;
    return result;
}

void *thread_function_product(void *arg)
{
    struct thread_args  *params = (struct thread_args*)arg;
    int                 *result = (int*)malloc(sizeof(int));

    *result = params->num1 * params->num2;
    return result;
}
```

在前面的程序中，我们从 main() 函数创建了一个主线程和两个子线程。创建后，这三个线程都以重叠方式开始执行。现在，两个子线程在 pthread_create() API 中具有不同的 start_routine 作为其参数。子线程 1 调用 thread_function_sum()，子线程 2 调用 thread_function_product()。这两个函数在各自的 start_routine 中执行一定量的处理，并在退出时返回一个值。前面的程序与 thread2.c 程序略有不同，因为 pthread_join() 调用具有一个非空的 void 指针类型参数。两个线程函数都通过 pthread_join() 调用中的第二个参数返回其输出。主线程在完成其执行后，等待子线程完成它们的工作。子线程退出后，主线程获取子线程的返回值并相应地处理它们。

现在让我们详细了解线程属性。

## 线程属性

在之前使用 pthread_create() API 的程序中，我们有意将其第二个参数传递为 NULL，以简化程序。调用 pthread_create() API 时，如果我们在线程属性的位置传递 NULL，那么线程将使用默认属性创建，也就是说，它将是一个可加入线程。然而，如果我们想指定自定义线程属性，则需要按如下方式显式处理该调用：

- 通过声明自动变量创建 pthread_attr_t 对象
- 对对象调用 pthread_attr_init()，以使用默认值初始化它
- 根据需求修改 pthread 属性对象并设置必要的属性
- 将指向 pthread 属性对象的指针作为参数传入 pthread_create()
- 调用 pthread_attr_destroy() 释放属性对象

以下不同类型的自定义线程属性可以传递给 pthread_create() API：

- 可加入线程（默认）——当线程终止时，它不会被自动清理。这意味着该线程会变成僵尸线程，直到对其调用 pthread_join()。
- 分离线程——当线程终止时，它会被自动清理，因此无需调用 pthread_join()。
- 线程的调度策略（实时？PTHREAD_INHERIT_SCHED、PTHREAD_EXPLICIT_SCHED、SCHED_OTHER）——这指定线程应使用的调度策略类型。它主要用于实时线程，以将它们与其他线程区分开来。
- 调度参数——这在线程属性对象中设置调度参数。通过使用它，可以设置线程的优先级。
- InheritSched 属性（默认：PTHREAD_EXPLICIT_SCHED 从父线程继承：PTHREAD_INHERIT_SCHED）——这主要用于创建新线程。
- 作用域（内核线程：PTHREAD_SCOPE_SYSTEM，用户线程——PTHREAD_SCOPE_PROCESS，选择其中之一，而不是两者都选）。这帮助我们在两种不同模式下工作——内核空间和用户空间。
