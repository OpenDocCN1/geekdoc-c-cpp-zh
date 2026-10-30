

这些函数的线程安全版本。这些函数与非线程安全版本同名，但在名称末尾加上了 _r，表示这些版本是可重入的。许多函数不是线程安全的，因为它们返回存储在静态内存缓冲区中的数据。它们通过更改接口来使其线程安全，要求调用者提供自己的缓冲区。

|  |  |
|---|---|
| getgrgid_r<br>getgrnam_r<br>getlogin_r<br>getpwnam_r<br>getpwuid_r<br>gmtime_r | localtime_r<br>readdir_r<br>strerror_r<br>strtok_r<br>ttyname_r |

**图 12.10** 替代的线程安全函数

如果一个函数相对于多个线程是可重入的，我们就说它是线程安全的。这并不能告诉我们，该函数是否相对于信号处理程序是可重入的。我们说一个函数如果可以安全地从异步信号处理程序中重新进入，则它是异步信号安全的。我们在讨论第 10.6 节中可重入函数时，在图 10.4 中看到了异步信号安全函数。

除了图 12.10 中列出的函数之外，POSIX.1 还提供了一种以线程安全的方式管理 FILE 对象的方法。你可以使用 flockfile 和 ftrylockfile 来获取与给定 FILE 对象关联的锁。此锁是递归的：你可以在已经持有它的情况下再次获取它，而不会导致死锁。虽然锁的确切实现未指定，但所有操作 FILE 对象的标准 I/O 例程都必须表现得好像它们在内部调用 flockfile 和 funlockfile。

```
#include <stdio.h>

int ftrylockfile(FILE *fp);
                         Returns: 0 if OK, nonzero if lock can’t be acquired
void flockfile(FILE *fp);
void funlockfile(FILE *fp);
```

尽管标准 I/O 例程可能被实现为从其自身内部数据结构的角度来看是线程安全的，但将锁定暴露给应用程序仍然是有用的。这允许应用程序将对标准 I/O 函数的多次调用组合成原子序列。当然，在处理多个 FILE 对象时，你需要注意潜在的死锁并仔细排序你的锁。

如果标准 I/O 例程获取自己的锁，那么在进行逐字符 I/O 时，我们可能会遇到严重的性能下降。在这种情况下，我们最终会为每个读取或写入的字符获取和释放锁。为了避免这种开销，提供了字符型标准 I/O 例程的未锁定版本。

```
#include <stdio.h>
int getchar_unlocked(void);
int getc_unlocked(FILE *fp);

Both return: the next character if OK, EOF on end of file or error

int putchar_unlocked(int c);
int putc_unlocked(int c, FILE *fp);

Both return: c if OK, EOF on error
```

这四个函数不应在未被 flockfile（或 ftrylockfile）和 funlockfile 调用包围的情况下调用。否则，可能会出现不可预测的结果（即由多个控制线程对数据进行未同步访问所导致的问题类型）。

一旦你锁定了 FILE 对象，你就可以在释放锁之前多次调用这些函数。这将锁定开销分摊到读取或写入的数据量上。

## 示例

图 12.11 显示了 getenv（第 7.9 节）的一种可能实现。此版本不可重入。如果两个线程同时调用它，它们会看到不一致的结果，因为返回的字符串存储在所有调用 getenv 的线程共享的单个静态缓冲区中。

```
#include <limits.h>
#include <string.h>

#define MAXSTRINGSZ 4096

static char envbuf[MAXSTRINGSZ];
extern char **environ;

char *
getenv(const char *name)
{
    int i, len;
    len = strlen(name);
    for (i = 0; environ[i] != NULL; i++) {
        if ((strncmp(name, environ[i], len) == 0) &&
            (environ[i][len] == '=')) {
            strcpy(envbuf, &environ[i][len+1], MAXSTRINGSZ-1);
            return(envbuf);
        }
    }
    return(NULL);
}
```

我们在图 12.12 中展示了 getenv 的可重入版本。此版本称为 getenv_r。它使用 pthread_once 函数确保 thread_init 函数在每个进程中只被调用一次，无论有多少线程竞争调用 getenv_r。我们将在第 12.6 节中更详细地讨论 pthread_once 函数。

```
#include <string.h>
#include <errno.h>
#include <pthread.h>
#include <stdlib.h>

extern char **environ;

pthread_mutex_t env_mutex;

static pthread_once_t init_done = PTHREAD_ONCE_INIT;
static void
thread_init(void)
{
    pthread_mutexattr_t attr;
    pthread_mutexattr_init(&attr);
    pthread_mutexattr_settype(&attr, PTHREAD_MUTEX_RECURSIVE);
    pthread_mutex_init(&env_mutex, &attr);
    pthread_mutexattr_destroy(&attr);
}

int
getenv_r(const char *name, char *buf, int buflen)
{
    int i, len, olen;
    pthread_once(&init_done, thread_init);
    len = strlen(name);
    pthread_mutex_lock(&env_mutex);
    for (i = 0; environ[i] != NULL; i++) {
        if ((strncmp(name, environ[i], len) == 0) &&
            (environ[i][len] == '=')) {
            olen = strlen(&environ[i][len+1]);
            if (olen >= buflen) {
                pthread_mutex_unlock(&env_mutex);
                return(ENOSPC);
            }
            strcpy(buf, &environ[i][len+1]);
            pthread_mutex_unlock(&env_mutex);
            return(0);
        }
    }
    pthread_mutex_unlock(&env_mutex);
    return(ENOENT);
}
```

为了使 getenv_r 可重入，我们更改了接口，以便调用者必须提供自己的缓冲区。因此每个线程可以使用不同的缓冲区来避免相互干扰。但是，请注意，这不足以使 getenv_r 线程安全。为了使 getenv_r 线程安全，我们需要防止在搜索请求字符串时环境发生变化。我们可以使用互斥锁来序列化 getenv_r 和 putenv 对环境列表的访问。

我们本可以使用读写锁来允许 getenv_r 的多个并发调用，但增加的并发性可能不会显著提高程序的性能，原因有两个。首先，环境列表通常不是很长，因此我们在扫描列表时不会持有互斥锁太久。其次，对 getenv 和 putenv 的调用并不频繁，因此如果我们改进它们的性能，也不会显著影响程序的整体性能。

即使我们可以使 getenv_r 线程安全，这也不意味着它相对于信号处理程序是可重入的。如果我们使用非递归互斥锁，我们就冒着线程在信号处理程序中调用 getenv_r 时导致自身死锁的风险。如果信号处理程序在线程执行 getenv_r 时中断了线程，我们已经持有 env_mutex 锁，因此再次尝试锁定它将会阻塞，导致线程死锁。因此我们必须使用递归互斥锁来防止其他线程在我们查看它们时更改数据结构，并防止信号处理程序导致的死锁。问题在于 pthread 函数不能保证是异步信号安全的，因此我们不能使用它们使另一个函数异步信号安全。

## 12.6 线程特定数据

线程特定数据，也称为线程私有数据，是一种用于存储和查找与特定线程关联的数据的机制。我们称数据为线程特定或线程私有，是因为我们希望每个线程访问其自己的数据副本，而不必担心与其他线程同步访问。

许多人费了很大劲设计了一个促进共享进程数据和属性的线程模型。那么为什么有人会想要推广防止在该模型中共享的接口呢？有两个原因。

首先，有时我们需要在每个线程的基础上维护数据。由于不能保证线程 ID 是小的、顺序的整数，我们不能简单地分配一个按线程数据的数组并使用线程 ID 作为索引。即使我们可以依赖小的、顺序的线程 ID，我们也希望有一点额外的保护，以便一个线程不能篡改另一个线程的数据。

线程私有数据的第二个原因是提供一种将基于进程的接口适配到多线程环境中的机制。这方面的一个明显例子是 errno。回顾第 1.7 节中对 errno 的讨论。较旧的接口（在线程出现之前）将 errno 定义为在进程上下文中全局可访问的整数。系统调用和库例程在失败时将 errno 作为副作用设置。为了使线程能够使用这些相同的系统调用和库例程

