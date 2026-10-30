

如果我们知道在创建线程时不需要线程的终止状态，我们可以通过修改 `pthread_attr_t` 结构中的 `detachstate` 线程属性，使线程从一开始就处于分离状态。我们可以使用 `pthread_attr_setdetachstate` 函数将 `detachstate` 线程属性设置为两个合法值之一：`PTHREAD_CREATE_DETACHED` 以使线程以分离状态启动，或 `PTHREAD_CREATE_JOINABLE` 以使线程正常启动，以便应用程序可以检索其终止状态。

```
#include <pthread.h>
int pthread_attr_getdetachstate(const pthread_attr_t *restrict attr,
                                int *detachstate);
int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
Both return: 0 if OK, error number on failure
```

我们可以调用 `pthread_attr_getdetachstate` 来获取当前的 `detachstate` 属性。第二个参数指向的整数将被设置为 `PTHREAD_CREATE_DETACHED` 或 `PTHREAD_CREATE_JOINABLE`，取决于给定 `pthread_attr_t` 结构中属性的值。

## 示例

图 12.4 显示了一个可用于以分离状态创建线程的函数。

```
#include "apue.h"
#include <pthread.h>
int
makethread(void *(*fn)(void *), void *arg)
{
    int         err;
    pthread_t   tid;
    pthread_attr_t  attr;
    err = pthread_attr_init(&attr);
    if (err != 0)
        return(err);
    err = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
    if (err == 0)
        err = pthread_create(&tid, &attr, fn, arg);
    pthread_attr_destroy(&attr);
    return(err);
}
```

图 12.4  以分离状态创建线程

请注意，我们忽略了对 `pthread_attr_destroy` 调用的返回值。在这种情况下，我们已正确初始化线程属性，因此 `pthread_attr_destroy` 不应失败。尽管如此，如果它确实失败，清理工作将变得困难：我们将不得不销毁刚刚创建的线程，而该线程可能已经在运行，与此函数的执行异步。当我们选择忽略 `pthread_attr_destroy` 的错误返回时，最坏的情况是我们会泄漏少量内存，如果 `pthread_attr_init` 分配了任何内存的话。但如果 `pthread_attr_init` 成功初始化了线程属性，而随后 `pthread_attr_destroy` 失败以清理，则我们无论如何都没有恢复策略，因为属性结构对应用程序是不透明的。用于清理结构的唯一接口是 `pthread_attr_destroy`，而它刚刚失败了。

线程栈属性的支持对于符合 POSIX 的操作系统是可选的，但如果系统支持单一 UNIX 规范中的 XSI 选项，则是必需的。在编译时，您可以使用 `_POSIX_THREAD_ATTR_STACKADDR` 和 `_POSIX_THREAD_ATTR_STACKSIZE` 符号来检查您的系统是否支持每个线程栈属性。如果定义了其中一个符号，则系统支持相应的线程栈属性。或者，您也可以通过使用 `sysconf` 函数的 `_SC_THREAD_ATTR_STACKADDR` 和 `_SC_THREAD_ATTR_STACKSIZE` 参数在运行时检查支持。我们可以使用 `pthread_attr_getstack` 和 `pthread_attr_setstack` 函数管理栈属性。

```
#include <pthread.h>

int pthread_attr_getstack(const pthread_attr_t *restrict attr,
    void **restrict stackaddr,
    size_t *restrict stacksize);

int pthread_attr_setstack(pthread_attr_t *attr,
    void *stackaddr, size_t stacksize);

Both return: 0 if OK, error number on failure
```

对于进程，虚拟地址空间的大小是固定的。由于只有一个栈，其大小通常不是问题。对于线程来说，相同数量的虚拟地址空间必须由所有线程栈共享。如果您的应用程序使用如此多的线程，以至于它们栈的总大小超过了可用的虚拟地址空间，您可能需要减小默认线程栈大小。另一方面，如果您的线程调用分配了大型自动变量的函数或调用了许多栈帧深的函数，您可能需要比默认栈大小更多的空间。

如果您用完了线程栈的虚拟地址空间，您可以使用 `malloc` 或 `mmap`（参见第 14.8 节）为替代栈分配空间，并使用 `pthread_attr_setstack` 更改您创建的线程的栈位置。`stackaddr` 参数指定的地址是用于作为线程栈的内存范围中可寻址的最低地址，已按处理器架构的适当边界对齐。当然，这假设 `malloc` 或 `mmap` 使用的虚拟地址范围与当前用于线程栈的范围不同。

`stackaddr` 线程属性定义为栈的最低内存地址。然而，这不一定是栈的开始。如果对于给定的处理器架构，栈从较高地址向较低地址增长，则 `stackaddr` 线程属性将是栈的末尾而不是开头。

应用程序还可以使用 `pthread_attr_getstacksize` 和 `pthread_attr_setstacksize` 函数获取和设置 `stacksize` 线程属性。

```
#include <pthread.h>
int pthread_attr_getstacksize(const pthread_attr_t *restrict attr, size_t *restrict stacksize);
int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);
Both return: 0 if OK, error number on failure
```

`pthread_attr_setstacksize` 函数在您想要更改默认栈大小但不想自行分配线程栈时很有用。设置 `stacksize` 属性时，我们选择的大小不能小于 `PTHREAD_STACK_MIN`。

`guardsize` 线程属性控制线程栈末尾之后内存范围的大小，以防止栈溢出。其默认值是实现定义的，但常用的值是系统页大小。我们可以将 `guardsize` 线程属性设置为 0 以禁用此功能：在这种情况下，不会提供保护缓冲区。此外，如果我们更改 `stackaddr` 线程属性，系统会假设我们将自行管理栈，并禁用栈保护缓冲区，就像我们将 `guardsize` 线程属性设置为 0 一样。

```
#include <pthread.h>
int pthread_attr_getguardsize(const pthread_attr_t *restrict attr, size_t *restrict guardsize);
int pthread_attr_setguardsize(pthread_attr_t *attr, size_t guardsize);
Both return: 0 if OK, error number on failure
```

如果修改了 `guardsize` 线程属性，操作系统可能会将其向上舍入为页大小的整数倍。如果线程的栈指针溢出到保护区域，应用程序将收到错误，可能伴随信号。

单一 UNIX 规范定义了若干其他可选的线程属性， intended for use by real-time applications。我们在此不讨论它们。

线程还有其他未由 `pthread_attr_t` 结构表示的属性：取消状态和取消类型。我们在第 12.7 节中讨论它们。

## 12.4 同步属性

正如线程具有属性一样，它们的同步对象也有属性。在第 11.6.7 节中，我们看到自旋锁有一个称为进程共享属性的属性。在本节中，我们讨论互斥锁、读写锁、条件变量和屏障的属性。

### 12.4.1 互斥锁属性

互斥锁属性由 `pthread_mutexattr_t` 结构表示。每当我们在第 11 章中初始化互斥锁时，我们都通过使用 `PTHREAD_MUTEX_INITIALIZER` 常量或通过调用 `pthread_mutex_init` 函数并将指向互斥锁属性结构的指针参数设为 null 来接受默认属性。

在处理非默认属性时，我们使用 `pthread_mutexattr_init` 初始化 `pthread_mutexattr_t` 结构，并使用 `pthread_mutexattr_destroy` 对其进行去初始化。

```
#include <pthread.h>

int pthread_mutexattr_init(pthread_mutexattr_t *attr);
int pthread_mutexattr_destroy(pthread_mutexattr_t *attr);

Both return: 0 if OK, error number on failure
```

`pthread_mutexattr_init` 函数将使用默认互斥锁属性初始化 `pthread_mutexattr_t` 结构。有三个感兴趣的属性：进程共享属性、健壮属性和类型属性。在 POSIX.1 中，进程共享属性是可选的；您可以通过检查是否定义了 `_POSIX_THREAD_PROCESS_SHARED` 符号来测试平台是否支持它。您也可以通过将 `_SC_THREAD_PROCESS_SHARED` 参数传递给 `sysconf` 函数在运行时进行检查。虽然此选项不是 POSIX 符合操作系统必须提供的，但单一 UNIX 规范要求 XSI 符合的操作系统确实支持它。

在进程内部，多个线程可以访问同一个同步对象。这是我们在第 11 章中看到的默认行为。在这种情况下，进程共享互斥锁属性设置为 `PTHREAD_PROCESS_PRIVATE`。

正如我们在第 14 章和第 15 章中将看到的那样，存在允许独立进程将同一内存范围映射到其独立地址空间的机制。由多个进程访问共享数据通常需要同步，就像由多个线程访问共享数据一样。如果进程共享互斥锁属性设置为 `PTHREAD_PROCESS_SHARED`，则从多个进程之间共享的内存范围分配的互斥锁可用于这些进程之间的同步。

我们可以使用 `pthread_mutexattr_getpshared` 函数查询 `pthread_mutexattr_t` 结构的进程共享属性。我们可以使用 `pthread_mutexattr_setpshared` 函数更改进程共享属性。

```
#include <pthread.h>

int pthread_mutexattr_getpshared(const pthread_mutexattr_t * restrict attr,
    int *restrict pshared);

int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr,
    int pshared);

Both return: 0 if OK, error number on failure
```

进程共享互斥锁属性允许 pthread 库在属性设置为 `PTHREAD_PROCESS_PRIVATE` 时提供更高效的互斥锁实现，这是在多线程应用程序中的默认情况。pthread 库可以然后

