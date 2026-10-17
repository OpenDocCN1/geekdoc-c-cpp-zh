

```cpp
#include <iostream>
#include <csignal>
#include <unistd.h>

using namespace std;

void signalHandler( int signum )
{
    cout << "Interrupt signal (" << signum << ") received.\n";

    // cleanup and close up stuff here
    // terminate program

    exit(signum);
}

int main ()
{
    // register signal SIGINT and signal handler
    signal(SIGINT, signalHandler);

    while(1){
        cout << "Going to sleep...." << endl;
        sleep(1);
    }

    return 0;
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
Going to sleep....
Going to sleep....
Going to sleep....
```

现在，按下 Ctrl+C 中断程序，你会看到程序会捕获信号并通过打印以下内容退出：

```text
Going to sleep....
Going to sleep....
Going to sleep....
Interrupt signal (2) received.
```

### The raise() Function

你可以通过函数 **raise()** 生成信号，它接受一个整数信号号作为参数，语法如下。

```cpp
int raise (int sig);
```

这里，**sig** 是要发送的信号号，可为以下信号之一：SIGINT、SIGABRT、SIGFPE、SIGILL、SIGSEGV、SIGTERM、SIGHUP。以下示例展示了我们如何使用 raise() 函数在内部引发信号：

```cpp
#include <iostream>

#include <csignal>

using namespace std;

void signalHandler( int signum )
{
    cout << "Interrupt signal (" << signum << ") received.\n";

    // cleanup and close up stuff here
    // terminate program

    exit(signum);
}

int main ()
{
    int i = 0;
    // register signal SIGINT and signal handler
    signal(SIGINT, signalHandler);
```

## 37. MULTITHREADING

多线程是多任务处理的一种特殊形式，而多任务处理是使计算机能够同时运行两个或多个程序的功能。一般来说，有两种类型的多任务处理：基于进程的和基于线程的。

基于进程的多任务处理处理程序的并发执行。基于线程的多任务处理处理同一程序的各个部分的并发执行。

多线程程序包含两个或多个可以并发运行的部分。这样的程序的每个部分称为线程，每个线程定义了单独的执行路径。

C++ 不包含任何对多线程应用程序的内置支持。相反，它完全依赖于操作系统提供此功能。

本教程假设你正在 Linux 操作系统上工作，我们将使用 POSIX 编写多线程 C++ 程序。POSIX 线程，或 Pthreads 提供 API，可在许多类 Unix 的 POSIX 系统上使用，例如 FreeBSD、NetBSD、GNU/Linux、Mac OS X 和 Solaris。

### Creating Threads

用于创建 POSIX 线程的例程如下：

```cpp
#include <pthread.h>

pthread_create (thread, attr, start_routine, arg)
```

这里，pthread_create 创建一个新的线程并使其可执行。此例程可以从代码中的任何位置被调用任意多次。以下是参数的说明：

| Parameter | Description |
| --- | --- |
| thread | 子例程返回的新线程的唯一不透明标识符。 |
| attr | 可用于设置线程属性的不透明属性对象。你可以指定线程属性对象，或指定 NULL 使用默认值。 |
| start_routine | 线程创建后将执行的 C++ 例程。 |
| arg | 可传递给 start_routine 的单个参数。它必须作为 void 类型的指针强制转换通过引用传递。如果不传递参数，可使用 NULL。 |

进程可创建的最大线程数取决于实现。创建后，线程是同级线程，可以创建其他线程。线程之间没有隐含的层次结构或依赖关系。

### Terminating Threads

我们用来终止 POSIX 线程的例程如下：

```cpp
#include <pthread.h>

pthread_exit (status)
```

这里 **pthread_exit** 用于显式退出线程。通常，在线程完成其工作且不再需要存在后，会调用 pthread_exit() 例程。

如果 main() 在其创建的线程完成之前结束，并以 pthread_exit() 退出，其他线程将继续执行。否则，当 main() 结束时，它们将被自动终止。

### Example:

此简单示例代码使用 pthread_create() 例程创建 5 个线程。每个线程打印一条 "Hello World!" 消息，然后通过调用 pthread_exit() 终止。

```cpp
#include <iostream>

#include <cstdlib>

#include <pthread.h>

using namespace std;

#define NUM_THREADS     5

void *PrintHello(void *threadid)
{
    long tid;

    tid = (long)threadid;

    cout << "Hello World! Thread ID, " << tid << endl;
    pthread_exit(NULL);
}

int main ()
{
    pthread_t threads[NUM_THREADS];
    int rc;
    int i;

    for( i=0; i < NUM_THREADS; i++ ){
        cout << "main() : creating thread, " << i << endl;
        rc = pthread_create(&threads[i], NULL,
                            PrintHello, (void *)i);
        if (rc){
            cout << "Error:unable to create thread," << rc << endl;
            exit(-1);
        }
    }
    pthread_exit(NULL);
}
```

使用 -lpthread 库编译以下程序，如下所示：

```bash
$gcc test.cpp -lpthread
```

现在，执行你的程序，输出如下：

```text
main() : creating thread, 0
main() : creating thread, 1
main() : creating thread, 2
main() : creating thread, 3
main() : creating thread, 4
Hello World! Thread ID, 0
Hello World! Thread ID, 1
Hello World! Thread ID, 2
Hello World! Thread ID, 3
Hello World! Thread ID, 4
```

pthread_join() 子例程会阻塞调用线程，直到指定的 'threadid' 线程终止。当线程被创建时，其属性之一定义了它是可连接的还是分离的。只有创建为可连接的线程才可以被连接。如果线程被创建为分离的，它永远无法被连接。

此示例演示了如何通过使用 Pthread join 例程等待线程完成。

```cpp
#include <iostream>
#include <cstdlib>
#include <pthread.h>
#include <unistd.h>

using namespace std;

#define NUM_THREADS     5

void *wait(void *t)
{
    int i;
    long tid;

    tid = (long)t;

    sleep(1);
    cout << "Sleeping in thread " << endl;
    cout << "Thread with id : " << tid << " ...exiting " << endl;
    pthread_exit(NULL);
}

int main ()
{
    int rc;
    int i;
    pthread_t threads[NUM_THREADS];
    pthread_attr_t attr;
    void *status;

    // Initialize and set thread joinable
    pthread_attr_init(&attr);
    pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_JOINABLE);

    for( i=0; i < NUM_THREADS; i++ ){
        cout << "main() : creating thread, " << i << endl;
        rc = pthread_create(&threads[i], NULL, wait, (void *)i );
        if (rc){
            cout << "Error:unable to create thread," << rc << endl;
            exit(-1);
        }
    }

    // free attribute and wait for the other threads
    pthread_attr_destroy(&attr);
    for( i=0; i < NUM_THREADS; i++ ){
        rc = pthread_join(threads[i], &status);
        if (rc){
            cout << "Error:unable to join," << rc << endl;
            exit(-1);
        }
        cout << "Main: completed thread id :" << i ;
        cout << "  exiting with status :" << status << endl;
    }

    cout << "Main: program exiting." << endl;
    pthread_exit(NULL);
}
```

当上面的代码被编译并执行时，会产生以下结果：

```text
main() : creating thread, 0
main() : creating thread, 1
main() : creating thread, 2
```

## 38. WEB PROGRAMMING

### What is CGI?

通用网关接口，或 CGI，是一组定义 Web 服务器与自定义脚本之间信息交换方式的标准。

CGI 规范目前由 NCSA 维护，NCSA 将 CGI 定义如下：

通用网关接口，或 CGI，是外部网关程序与信息服务器（如 HTTP 服务器）交互的规范。

当前版本为 CGI/1.1，CGI/1.2 正在进行中。

### Web Browsing

为了理解 CGI 的概念，让我们看看当我们点击超链接浏览特定网页或 URL 时会发生什么。

- 你的浏览器联系 HTTP Web 服务器并请求 URL，即文件名。
- Web 服务器会解析 URL 并查找文件名。如果找到请求的文件，则 Web 服务器会将该文件发送回浏览器，否则发送错误消息，表明你请求了错误的文件。
- Web 浏览器从 Web 服务器接收响应，并根据接收到的响应显示接收到的文件或错误消息。

然而，可以设置 HTTP 服务器，使得每当请求某个目录中的文件时，该文件不会被发送回去；相反，它作为程序执行，并将程序的输出发送回浏览器显示。

通用网关接口（CGI）是使应用程序（称为 CGI 程序或 CGI 脚本）与 Web 服务器和客户端交互的标准协议。这些 CGI 程序可以用 Python、PERL、Shell、C 或 C++ 等编写。

### CGI Architecture Diagram

以下简单程序展示了 CGI 的简单架构：

