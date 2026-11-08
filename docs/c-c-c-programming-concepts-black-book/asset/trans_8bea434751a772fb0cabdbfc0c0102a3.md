
```c
fprintf(stdout, "\nwaiting for threads to finish...\n");
res = pthread_join(thread1, NULL);
if (res != 0) {
    fprintf(stderr, "\nThread join failed\n");
    return 0;
}

fprintf(stdout, "\nThread joined. \n");
pthread_mutex_destroy(&mutex);

return 0;
}
```

在进入下一节之前，我们先概览一下非阻塞互斥锁。使用非阻塞互斥锁的好处是：如果互斥锁尚未被锁定，那么它将获取该锁；否则，如果它已经被锁定，那么该调用将返回状态 EBUSY。以下是非阻塞互斥锁的特性：

- 通过 `int pthread_mutex_trylock(pthread_mutex_t *mutex);`，可以在不实际阻塞的情况下用互斥锁锁定对象。
- 如果互斥锁未锁定，那么 `pthread_mutex_trylock()` API 的工作方式将与 `pthread_mutex_lock()` 类似。
- 如果某个互斥锁所引用的互斥对象当前被任何线程（包括当前线程）锁定，那么对该互斥锁的调用将立即返回。
- 如果互斥锁类型为 `PTHREAD_MUTEX_RECURSIVE_NP`，且该互斥锁当前由调用线程拥有，那么互斥锁的锁定计数将加一，并且 `pthread_mutex_trylock()` 将立即返回成功。

在下一节中，我们来讨论信号量。

## 信号量

信号量是一种受保护的变量，用于同步对共享可访问资源的并行访问。信号量是一种机制，它包含一个抽象计数器以及两个可用于同步多个线程的操作。可以对信号量执行以下两种操作：

- **等待操作**——将信号量的值减一。如果信号量的值为零，那么等待操作会阻塞线程，直到其他某个线程增加信号量的值。当该值变为正数时，信号量的值减一，等待操作返回。
- **发布操作**——将信号量的值加一。如果信号量的值为零，那么发布操作会解除一个线程的阻塞，该线程正阻塞在对该信号量的等待调用上。被解除阻塞的线程将完成等待调用。发布操作也称为信号操作。

以下是使用信号量的步骤：

- 1. 包含 `<semaphore.h>`，如下所示：

    ```c
    #include <semaphore.h>
    ```

- 2. 声明一个信号量（类型为 `sem_t`），如下所示：

    ```c
    sem_t sem;
    ```

- 3. 初始化信号量，如下所示：

    ```c
    sem_init(&sem, 0, 0);
    ```

- 4. 等待信号量，如下所示：

    ```c
    sem_wait(&sem);  /* blocking */
    sem_trywait(&sem);  /* non-blocking */
    ```

- 5. 向信号量发布，如下所示：

    ```c
    sem_post(&sem);
    ```

- 6. 当不再需要信号量时销毁它，如下所示：

    ```c
    sem_destroy(&sem);
    ```

为了理解信号量的操作和用途，我们以生产者-消费者问题为例。该问题从两个进程开始——生产者和消费者。生产者进程生产某种东西，例如商品；而消费者进程消费生产者生产的商品。现在，为了维持这两个进程之间的协调，生产者和消费者进程都必须同步。如果它们不同步，就可能会遇到若干问题。例如，如果生产者以非常高的速率生产，而消费者以较低的速率消费，那么这将导致商品堆积。然而，如果消费者以高得多的速率消费，那么就会出现产品短缺。我们可以通过将商品定义为信号量变量，并执行等待和信号操作来维持生产者与消费者进程之间的协调，从而解决这个问题。解决生产者-消费者问题的代码如下所示：

```c
#include <stdio.h>
#include <malloc.h>
#include <pthread.h>
#include <semaphore.h>

struct job {
    struct job* next;
    int         num;
};

struct job* job_queue;

pthread_mutex_t job_queue_mutex = PTHREAD_MUTEX_INITIALIZER;

/* A semaphore counting the number of jobs in the queue. */
sem_t job_queue_count;

void initialize_job_queue ()
{
        job_queue = NULL;
        sem_init (&job_queue_count, 0, 0);
}

void process_job(struct job *job)
{
        int square = 0;
        /* Process job */
        square = job->num * job->num;
        fprintf(stdout, "\nProcessed job, num=[%d] output=[%d]", job->num, square);
}

void enqueue_job (int num)
{
        struct job* new_job;
        new_job = (struct job*) malloc (sizeof (struct job));
        pthread_mutex_lock (&job_queue_mutex);
        new_job->next = job_queue;
        new_job->num = num;
        fprintf(stdout, "\nAdding new job. num=[%d]", new_job->num);
        job_queue = new_job;
        sem_post (&job_queue_count);
        pthread_mutex_unlock (&job_queue_mutex);
}

void* thread_producer_function (void* arg)
{
    int j = 0;

    while (1) {
        struct job* next_job;
        enqueue_job(j);
        j++;
        if (j % 5 == 0) {
            sleep(5);
        }
    }
    return NULL;
}

void* thread_consumer_function (void* arg)
{
    struct job* next_job;
    while (1) {
        fprintf(stdout, "\nConsumer waiting for new job..."); fflush(stdout);
        sem_wait (&job_queue_count);
        fprintf(stdout, "\nConsumer got new job."); fflush(stdout);

        pthread_mutex_lock (&job_queue_mutex);
        next_job = job_queue;
        job_queue = job_queue->next;
        process_job (next_job);
        pthread_mutex_unlock (&job_queue_mutex);
        free (next_job);
    }
    return NULL;
}

int
main()
{
    pthread_t          thread_producer;
    pthread_t          thread_consumer;
    int                res = 0;
    int                i   = 0;

    initialize_job_queue();

    res = pthread_create(&thread_producer, NULL, thread_producer_function, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread creation failed\n");
        return 1;
    }

    res = pthread_create(&thread_consumer, NULL, thread_consumer_function, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread creation failed\n");
        return 1;
    }

    fprintf(stdout, "\nwaiting for threads to finish...\n");
    res = pthread_join(thread_producer, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread join failed\n");
        return 0;
    }
    res = pthread_join(thread_consumer, NULL);
    if (res != 0) {
        fprintf(stderr, "\nthread join failed\n");
        return 0;
    }

    pthread_mutex_destroy(&job_queue_mutex);

    return 0;
}
```

以下是一些信号量 API：

```c
int sem_init(sem_t *sem, int pshared, unsigned int value);
sem - initialises the semaphore pointed to by sem
pshared - should be set to 0 if the semaphore is shared between threads of a process
value - initial value of the semaphore

int sem_post(sem_t *sem);
sem - address of the semaphore

int sem_wait(sem_t *sem);
Blocks if value of sem is zero

int sem_trywait(sem_t *sem);
If value of sem is zero, call returns with error

int sem_timedwait(sem_t *sem, const struct timespec *abs_timeout);
If value of sem is zero, the call blocks for a maximum of the time specified in the
call.

int sem_destroy(sem_t *sem);
sem - destroys the semaphore pointed to by sem
```

我们再考虑另一个程序，以展示在使用信号量的线程编程中 CPU 周期是如何被浪费的：

```c
/* Demonstrating busy waiting for cpu cycles for mutex variables */
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

int continue_flag;
pthread_mutex_t continue_flag_mutex;

void do_work ()
{
    fprintf(stdout, "\nworker thread: working..."); fflush(stdout);
}

void* worker_thread_function(void *arg)
{
    int cont_flag = 0;
    while (1) {
        pthread_mutex_lock(&continue_flag_mutex);
        if (continue_flag) {
            do_work();
        }
        pthread_mutex_unlock(&continue_flag_mutex);
    }
}
int
main()
{
    pthread_t            worker_thread;
    int                  res = 0;

    continue_flag = 0;
    pthread_mutex_init(&continue_flag_mutex, NULL);

    res = pthread_create(&worker_thread, NULL, worker_thread_function, NULL);
    if (res != 0) {
        fprintf(stderr, "\nThread creation failed\n");
        return 1;
    }

    while (1) {
        pthread_mutex_lock(&continue_flag_mutex);
        continue_flag = 1;
        pthread_mutex_unlock(&continue_flag_mutex);
        fprintf(stdout, "\nmain thread: Start work\n\n"); fflush(stdout);
        sleep(2);
        pthread_mutex_lock(&continue_flag_mutex);
        continue_flag = 0;
        pthread_mutex_unlock(&continue_flag_mutex);
        fprintf(stdout, "\nmain thread: Stop work\n\n"); fflush(stdout);
        sleep(3);
    }

    fprintf(stdout, "\nWaiting for thread to finish...\n");
    res = pthread_join(worker_thread, NULL);
    if (res != 0) {
        fprintf(stderr, "\nThread join failed\n");
        return 0;
    }

    fprintf(stdout, "\nThread joined. \n");
    pthread_mutex_destroy(&continue_flag_mutex);

    return 0;
}
```
