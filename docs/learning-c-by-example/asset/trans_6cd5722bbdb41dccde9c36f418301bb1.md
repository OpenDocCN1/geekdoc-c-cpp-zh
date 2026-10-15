

## 8. 线程

本章解释如何使用 C 进行线程工作。

```
ret = pthread_create (&thread, NULL, perform, &n);
if (ret)
{
    printf("\n pthread_create() failed with error [%s]\n", strerror(err
    return -1;
}
int c = getchar(); // hold app to exit
return 0;
}
```

你可以看到我们将参数 n=10 传递给函数 perform()。在函数 perform() 中，我们只是进行循环。

现在保存此代码。要编译和链接，你可以输入以下命令。

```
$ gcc -pthread -o createthread createthread.c
```

如果成功，你可以运行此应用程序。

```
$ ./createthread
```

以下是示例输出。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_88_0.png)

## 8.2 线程 ID

我们可以使用 pthread_self() 获取正在运行的线程，以下是其语法。

```
#include <pthread.h>

pthread_t pthread_self (void);
```

要使用此函数，你可以在线程函数内部调用 pthread_self()。

为了说明，创建文件，名为 threadid.c，并写入此代码。

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>

void* perform(void *arg)
{
    int i;
    int *n = (int *)arg;
    pthread_t tid;

    printf("processing from thread\r\n");
    /* get the calling thread's ID */
    tid = pthread_self();
    printf("Thread id: %d \r\n",(int)tid);
    for(i=0;i<(*n);i++)
    {
        printf("%d ",i);
    }
    printf("\r\n");
}

int main(int argc, char* argv[])
{
    pthread_t thread;
    int ret;
    errno = 0;
    int n = 10;

    ret = pthread_create (&thread, NULL, perform, &n);
    if (ret)
    {
        printf("\n pthread_create() failed with error [%s]\n",strerror(err
        return -1;
    }
    int c = getchar(); // hold app to exit
    return 0;
}
```

## 8.3 终止线程

我们可以使用两种方法终止线程，自身终止和终止其他线程。我们将在下一节中探索这些方法。

### 8.3.1 自身终止

线程可以使用 pthread_exit() 停止其处理。以下是 pthread_exit() 的语法。

```
#include <pthread.h>

void pthread_exit (void *retval);
```

为了说明，我们基于线程构建应用程序并调用函数 perform()。在函数 perform() 中，我们进行循环，并在循环索引为 3 后通过调用 pthread_exit() 从内部线程退出。

要实现，我们创建一个文件，名为 selfexit.c，并写入此代码。

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>

void* perform(void *arg)
{
    int i;
    int *n = (int *)arg;

    printf("processing from thread\r\n");
    for(i=0;i<(*n);i++)
    {
        if(i==3)
        {
            printf("Terminating thread\r\n");
            /* exit this thread */
            pthread_exit((void *)0);
        }
        printf("%d ",i);
    }
    printf("\r\n");
}

int main(int argc, char* argv[])
{
```

```
int pthread_setcancelstate(int state, int *oldstate);
void pthread_testcancel(void);
```

为了说明，我们构建应用程序以创建线程并尝试使用 pthread_cancel() 终止它。

创建一个文件，名为 terminateother.c，并写入此代码。

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>

void* perform(void *arg)
{
    int n = 0;

    // I'm not ready to be canceled
    pthread_setcancelstate(PTHREAD_CANCEL_DISABLE, NULL);
    printf("processing from thread\r\n");
    while(1)
    {
        printf("%d ",n);
        n++;

        pthread_testcancel();
        if(n>5)
        {
            // I'm ready to be canceled
            pthread_setcancelstate(PTHREAD_CANCEL_ENABLE, NULL);
        }

        sleep(1);
    }
    printf("\r\n");
}

int main(int argc, char* argv[])
{
    pthread_t thread;
    int ret, status;
    errno = 0;

    ret = pthread_create (&thread, NULL, perform, NULL);
    if (ret)
    {
        printf("\n pthread_create() failed with error [%s]\n",strerror(err
        return -1;
    }
    sleep(10);
```

```
errno = 0;
status = pthread_cancel(thread);
if (status)
{
    printf("\n pthread_cancel() failed with error [%s]\n",strerror(e
    return -1;
}

int c = getchar(); // hold app to exit
return 0;
}
```

说明：

- 在主入口 main() 中，我们创建了一个线程并传递 perform() 函数
- 我们使用 sleep() 保持当前进程 10 秒
- 之后，我们尝试通过调用 pthread_cancel() 终止线程
- pthread_cancel() 函数返回状态值。你可以验证此返回值
- 在 perform() 函数中，首先我们调用 pthread_setcancelstate() 来禁用线程取消
- 在循环 n>5 后，我们启用线程取消
- pthread_testcancel() 函数被调用以创建一个取消点

保存此代码。编译并运行它。

以下是示例输出。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_94_0.png)

保存此代码。因为我们使用 math.h，我们在编译和链接时添加库 -lm。以下是编译此代码的语法。

```
```bash
$ gcc -pthread -o jointhread jointhread.c -lm
$ ./jointhread
```
```

现在你可以运行它。示例输出如图所示。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_97_0.png)

## 8.5 线程互斥锁

你拥有诸如数据变量、文件、数据库等资源，只能由一个线程访问。它被称为互斥锁。为了说明，你有一个存储在变量 n 上的数据。你还有 5 个线程访问此数据。第一条规则是数据变量只能由一个线程访问。这意味着数据变量将被锁定，因此另一个线程无法访问它。

互斥锁是控制访问资源的线程同步机制之一。

你可以使用以下函数实现线程互斥锁。

```
#include <pthread.h>

int pthread_mutex_init(pthread_mutex_t *restrict mutex,
    const pthread_mutexattr_t *restrict attr);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

注意：

- pthread_mutex_init() 初始化互斥锁对象
- pthread_mutex_destroy() 销毁互斥锁对象
- pthread_mutex_lock() 锁定互斥锁对象
- pthread_mutex_unlock() 解锁/释放互斥锁对象

为了实现，我们创建一个文件，名为 mutex.c。首先我们定义头文件和全局变量。写入此代码。

```
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>

pthread_t thread[5];
int total_finished_jobs;
pthread_mutex_t lock;
```

变量 total_finished_jobs 只能由一个线程访问。

在 main() 入口点，我们实例化互斥锁对象并创建 5 个线程。

```
int main(int argc, char* argv[])
{
    int i, ret;
    errno = 0;
```

```
```c
total_finished_jobs = 0;

if (pthread_mutex_init(&lock, NULL) != 0)
{
    printf("\n pthread_mutex_init() failed with error [%s]\n", strerror
    return 1;
}

for (i=0;i<5;i++)
{
    ret = pthread_create (&thread[i], NULL, perform_job, NULL);
    if (ret)
    {
        printf("\n pthread_create() failed with error [%s]\n", strerror
        return -1;
    }
}

int c = getchar(); // hold app to exit
pthread_mutex_destroy(&lock);

return 0;
}
```
```

每个线程调用 perform_job() 函数。当访问变量 total_finished_jobs 时，我们尝试锁定对象 lock。之后，我们更新 total_finished_jobs 的值。

以下是 perform_job() 函数的实现。

```
```c
void* perform_job(void *arg)
{
    int i;
    pthread_t tid;

    tid = pthread_self();
    printf("processing from thread %ld \r\n", tid);
    printf("Thread %ld. Started Job. \r\n", tid);

    // do something for doing job
    for(i=0;i<20;i++)
    {
        sleep(1);
    }

    // update job counter
    pthread_mutex_lock(&lock);
    total_finished_jobs++;
    printf("Thread %ld. Finished Job. \r\n", tid);
    printf("Total current finished job: %d \r\n", total_finished_jobs);
    pthread_mutex_unlock(&lock);
}
```
