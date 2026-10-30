
routines，errno 被重新定义为线程私有数据。因此，一个线程进行设置 errno 的调用不会影响进程中其他线程的 errno 值。

请记住，进程中的所有线程都可以访问进程的整个地址空间。除了使用寄存器外，一个线程无法阻止另一个线程访问其数据。即使对于线程特定数据也是如此。尽管底层实现并不阻止访问，但提供用于管理线程特定数据的函数通过使线程更难访问其他线程的线程特定数据，从而促进线程之间的数据分离。

在分配线程特定数据之前，我们需要创建一个与数据关联的键。该键将用于访问线程特定数据。我们使用 pthread_key_create 来创建这样的键。

```
#include <pthread.h>

int pthread_key_create(pthread_key_t *keyp, void (*destructor)(void *));
Returns: 0 if OK, error number on failure
```

创建的键存储在 keyp 指向的内存位置。同一键可以被进程中的所有线程使用，但每个线程会将不同的线程特定数据地址与该键关联。当键被创建时，每个线程的数据地址都被设置为 null 值。

除了创建键之外，pthread_key_create 还会将一个可选的析构函数与键关联。当线程退出时，如果数据地址已被设置为非 null 值，则会调用析构函数，并将数据地址作为唯一参数传递。如果 destructor 为 null，则不会将析构函数与键关联。当线程正常退出时，无论是通过调用 pthread_exit 还是通过返回，析构函数都会被调用。此外，如果线程被取消，析构函数也会被调用，但仅在最后一个清理处理程序返回之后。但是如果线程调用 exit、_exit、_Exit 或 abort，或以其他方式异常退出，则不会调用析构函数。

线程通常使用 malloc 为其线程特定数据分配内存。析构函数通常会释放已分配的内存。如果线程在未释放内存的情况下退出，则内存会丢失——被进程泄漏。

一个线程可以为线程特定数据分配多个键。每个键都可以关联一个析构函数。可以为每个键使用不同的析构函数，也可以让所有键使用相同的函数。每个操作系统实现都可以对进程可以分配的键的数量设置限制（请回顾图 12.1 中的 PTHREAD_KEYS_MAX）。

当线程退出时，其线程特定数据的析构函数会以实现定义顺序被调用。析构函数有可能调用另一个函数，该函数创建新的线程特定数据并将其与键关联。在所有析构函数被调用后，系统会检查是否与键关联了任何非 null 的线程特定值，如果有，则会再次调用析构函数。此过程会重复，直到线程的所有键的线程特定数据值都为 null，或者已尝试 PTHREAD_DESTRUCTOR_ITERATIONS 次（图 12.1）。

我们可以通过调用 pthread_key_delete 来解除键与所有线程的线程特定数据值的关联。

```
#include <pthread.h>
int pthread_key_delete(pthread_key_t key);
Returns: 0 if OK, error number on failure
```

请注意，调用 pthread_key_delete 不会调用与键关联的析构函数。要释放与键的线程特定数据值关联的任何内存，我们需要在应用程序中采取额外的步骤。

我们需要确保分配的键不会因为初始化期间的竞争而改变。如下所示的代码可能会导致两个线程都调用 pthread_key_create：

```
void destructor(void *);

pthread_key_t key;
int init_done = 0;

int
threadfunc(void *arg)
{
    if (!init_done) {
        init_done = 1;
        err = pthread_key_create(&key, destructor);
    }
    :
}
```

根据系统调度线程的方式，一些线程可能会看到一个键值，而其他线程可能会看到不同的值。解决此竞争的方法是使用 pthread_once。

```
#include <pthread.h>

pthread_once_t initflag = PTHREAD_ONCE_INIT;
int pthread_once(pthread_once_t *initflag, void (*initfn)(void));
Returns: 0 if OK, error number on failure
```

initflag 必须是 nonlocal 变量（即全局或静态）并且初始化为 PTHREAD_ONCE_INIT。

如果每个线程都调用 pthread_once，系统保证初始化例程 initfn 只会被调用一次，即在第一次调用 pthread_once 时。创建键而不会出现竞争的正确方法如下：

```
void destructor(void *);

pthread_key_t key;
pthread_once_t init_done = PTHREAD_ONCE_INIT;
```

```
void
thread_init(void)
{
    err = pthread_key_create(&key, destructor);
}
int
threadfunc(void *arg)
{
    pthread_once(&init_done, thread_init);
    :
}
```

一旦键被创建，我们就可以通过调用 pthread_setspecific 将线程特定数据与键关联。我们可以通过 pthread_getspecific 获取线程特定数据的地址。

```
#include <pthread.h>
void *pthread_getspecific(pthread_key_t key);
    Returns: thread-specific data value or NULL if no value
            has been associated with the key
int pthread_setspecific(pthread_key_t key, const void *value);
    Returns: 0 if OK, error number on failure
```

如果没有线程特定数据与键关联，pthread_getspecific 将返回空指针。我们可以使用此返回值来确定是否需要调用 pthread_setspecific。

## Example

在图 12.11 中，我们展示了 getenv 的一个假设实现。我们提出了一个新的接口来提供相同的功能，但以线程安全的方式（图 12.12）。但如果我们无法修改应用程序程序以使用新接口会怎样？在这种情况下，我们可以使用线程特定数据来维护用于保存返回字符串的数据缓冲区的每个线程副本。这在图 12.13 中显示。

```
#include <limits.h>
#include <string.h>
#include <pthread.h>
#include <stdlib.h>

#define MAXSTRINGSZ 4096

static pthread_key_t key;
static pthread_once_t init_done = PTHREAD_ONCE_INIT;
pthread_mutex_t env_mutex = PTHREAD_MUTEX_INITIALIZER;
```

```
extern char **environ;

static void
thread_init(void)
{
    pthread_key_create(&key, free);
}

char *
getenv(const char *name)
{
    int i, len;
    char *envbuf;

    pthread_once(&init_done, thread_init);
    pthread_mutex_lock(&env_mutex);
    envbuf = (char *)pthread_getspecific(key);
    if (envbuf == NULL) {
        envbuf = malloc(MAXSTRINGSZ);
        if (envbuf == NULL) {
            pthread_mutex_unlock(&env_mutex);
            return(NULL);
        }
        pthread_setspecific(key, envbuf);
    }
    len = strlen(name);
    for (i = 0; environ[i] != NULL; i++) {
        if ((strncmp(name, environ[i], len) == 0) &&
            (environ[i][len] == '=')) {
            strncpy(envbuf, &environ[i][len+1], MAXSTRINGSZ-1);
            pthread_mutex_unlock(&env_mutex);
            return(envbuf);
        }
    }
    pthread_mutex_unlock(&env_mutex);
    return(NULL);
}
```

### Figure 12.13 A thread-safe, compatible version of getenv

我们使用 pthread_once 来确保仅为我们将使用的线程特定数据创建一个键。如果 pthread_getspecific 返回空指针，我们需要分配内存缓冲区并将其与键关联。否则，我们使用 pthread_getspecific 返回的内存缓冲区。对于析构函数，我们使用 free 来释放 malloc 之前分配的内存。仅当线程特定数据的值为非 null 时，析构函数才会被调用并传入线程特定数据的值。

请注意，尽管此版本的 getenv 是线程安全的，但它不是异步信号安全的。即使我们使互斥锁可重入，我们也无法使其相对于信号处理程序可重入，因为它调用了 malloc，而 malloc 本身不是异步信号安全的。

