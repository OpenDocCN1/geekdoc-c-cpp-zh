

用于显示可执行文件 client 和 createpipe 的类型、它们以字节为单位的大小，以及它们代码、数据和 bss 段以字节为单位的大小，以及它们大小的总和以十进制和十六进制表示。

```
$ file client createpipe
client:  ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32,
BuildID[sha1]=becc6bdae9989b9bda647121091fffa660e95741, not stripped
createpipe: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32,
BuildID[sha1]=457bd89c9d371b63fb7601757b1f2b37f012174c, not stripped
$ ls -l client createpipe
-rwxr-xr-x 1 sarwar faculty 9048 Oct 21 18:42 client
-rwxr-xr-x 1 sarwar faculty 8816 Oct 21 17:19 createpipe
$ size client createpipe
text    data    bss     dec     hex     filename
2341    624     8       2973    b9d     client
1641    584     8       2233    8b9     createpipe
$
```

file 命令的输出显示 client 和 createpipe 都是 ELF 64 位格式的可执行文件。ls -l 命令的输出显示它们的大小分别为 9,048 和 8,816 字节。最后，size 命令的输出显示它们 text、data 和 bss 段以字节为单位的大小，以及它们大小的总和。

## Exercise 16.1

静态链接和动态链接有什么区别？

## Exercise 16.2

使用 size 命令确定 Linux 命令 find 和 sort 的可执行文件的 text、data 和 bss 段的大小。显示命令运行及其输出。

### 16.2.5 What Is a Thread?

当进程从其“main”函数调用一个函数时，执行的控制权从 main 函数转移到被调用函数的代码。函数返回后，调用函数中函数调用之后的语句将被执行。如果被调用的函数调用另一个函数，控制权转移到新被调用的函数，返回到其调用者，并最终返回到 main 函数。因此，随着程序的执行，存在单一的控制流，也称为执行线程，通常称为线程，它通常从 main 函数开始，依次移动到被调用的函数，最终返回到 main 函数。当 main 函数完成执行时，进程中唯一的执行线程以及进程本身终止。这样的进程被称为单线程进程，它们中唯一的线程被称为主线程。我们也可以说单线程进程只有一个与之关联的 PC，并且 PC 在任何给定时间的值决定了线程中下一个要执行的指令的地址。

所有传统程序都会产生单线程进程。图 16.3 显示了一个典型的单线程 C 程序，其中程序执行从 main 函数开始，并在函数被调用时移动到不同的函数。从 main 到其他函数再返回所遵循的单一执行路径——即程序中的执行线程——如图 16.4 所示。请注意，唯一的执行线程如何按以下顺序从一个函数移动到另一个函数并返回：

```
main → f1 → f2 → f1 → main → f3 → main → f1 → main
```

你可以通过在程序中执行一段代码，通常是一个函数，使得该函数代码像一个独立的程序一样执行，但没有 main 函数，并且在函数所在的进程的地址空间内执行，来在你的程序中创建另一个执行线程。这意味着这个执行线程有自己的 PC 和栈。然而，由于它在进程的地址空间内执行，它与进程中的所有其他执行线程，包括主线程，共享数据、代码和其他之前讨论过的程序段。

你可以使用其中一个线程库的 API 来创建和管理线程。通过这些库使用用户程序创建的线程，它们不为内核所知，并且完全由用户级线程库管理，被称为用户级线程。这些库的代码和数据结构维护在用户空间。内核不知道也不为此类线程提供支持。这意味着内核只管理进程，而相关的线程库管理线程，包括它们的调度。

一些编程语言如 Java 为用户级线程提供直接支持。此类线程由程序本身通过使用线程库的 API 创建和管理。

如果线程库在内核中实现，操作系统维护库的代码和数据结构。对这些库中用于创建和管理线程的函数的调用会导致系统调用。通过使用此类库的用户程序创建的线程被称为内核级线程。内核处理进程和线程，包括它们的调度。

有多个库可用于实现用户级和内核级线程。POSIX 标准 Pthreads 可以作为用户级或内核级库提供。

几乎所有现代通用操作系统的内核都是多线程的。这意味着它们可以同时为多个系统调用提供服务。这是通过将对应于系统调用的代码作为线程而不是函数调用运行来实现的。因此，例如，来自同一进程或不同进程中线程的 read() 系统调用的多个调用可以同时得到服务。提供此类多线程服务的操作系统内核被称为多线程内核。

我们使用库调用来创建、终止和管理线程。如果线程库是内核线程库，每个库调用最终都会调用系统调用。内核将了解线程并负责管理它们，包括它们的调度。否则，用户级库管理线程。

在图 16.5 中，我们展示了一个具有四个线程的多线程进程：主线程、函数 f1() 的两个线程和函数 f3() 的一个线程。设计为线程的函数必须使用终止线程的库函数终止，例如 pthread_exit(...)。我们使用 Pthreads 库函数来创建和终止线程的名称。请注意，你需要在程序中包含头文件 /usr/include/pthread.h 并使用 gcc 编译器使用 -pthread 选项将 Pthreads 库与可执行代码链接，如

```
gcc -w -pthread prog.c -o prog
```

单线程和多线程进程的典型图形表示如图 16.6 所示。请注意，在 tid3 开始运行并且 tid1 尚未完成之后，四个线程同时运行：main、tid1、tid2 和 tid3。

### 16.2.6 Commonalities and Differences between Processes and Threads

进程和线程有几个共同点。例如，每个都有自己的 ID、栈和 PC。

进程和线程之间有几个区别。例如，虽然进程在其自己的地址空间内运行，但进程内的线程在进程的地址空间内运行。同样，进程有自己的数据和文本（代码）区域，但线程共享进程中的文本和数据区域。

### 16.2.7 Data Sharing among Threads and the Critical Section Problem

线程之间的数据共享是一把双刃剑。虽然这通过防止数据重复来节省内存空间，但它确实要求线程在访问数据时以互斥方式访问，通过在访问数据之前锁定数据并在之后解锁它。如果不这样做，进程产生的

## Code

```
#include <stdio.h>
int main(int argc, char* argv[])
{
	int i;
	char c;
	printf("Hello, world!\n");
	...
	f1(...);
	...
	f1(...);
	...
	f2(...);
	...
	f1(...);
	...
	exit(0);
}
void f1(int i, int* ip)
{
	...
	if (...)
	then
	f2(...);
	else
	...
}
void f2(char c)
{
	...
}
void f3(char* s)
{
	...
}
```

## FIGURE 16.3 Single-threaded process with only the main thread.

![](img/2a18e06cd9c6395e451f26126ecba1fd_504_0.png)

## FIGURE 16.4 The flow of control (thread) of the program: a single-threaded process.

like an independent program but without a main function and within the address space of the process in which the function resides. This means that this thread of execution has its own PC and stack. However, because it executes within the address space of a process, it shares with all other threads of execution, including the main thread, data, code, and other segments of the program previously discussed.

You may use the API for one of the several thread libraries to create and manage threads. The threads created by user programs using these libraries, which are not known to the kernel and are managed solely by the user-level thread libraries, are known as user-level threads. The code and data structures for these libraries are maintained in the user space. The kernel does not know about and provides no support for such threads. It means that the kernel only manages processes and the relevant thread library manages threads, including their scheduling.

Some programming languages such as Java provide direct support for user-level threads. Such threads are created and managed by the program itself through the use of the API of a thread library.

If a thread library is implemented in the kernel, the operating system maintains the code and data structures for the library. Calls to functions in these libraries for creating and managing threads result in system calls. The threads created by the user programs using such libraries are known as kernel-level threads. The kernel handles both processes and threads, including their scheduling.

Several libraries are available for the implementation of user- and kernel-level threads. The POSIX standard Pthreads may be provided as user- or kernel-level libraries.

Kernels of almost all modern general-purpose operating systems are multithreaded. This means that they can serve multiple system calls simultaneously. This is done by running the code corresponding to a system call as a thread instead of a function call. Thus, for example, multiple invocations of the read() system call from threads within the same process or different processes may be served simultaneously. The operating system kernels that offer such multithreaded services are known as multithreaded kernels.

We use library calls to create, terminate, and manage threads. If the threads library were for kernel threads, each library call would eventually invoke a system call. The kernel would have the knowledge of threads and would be responsible for managing them, including their scheduling. Otherwise, the user-level library manages threads.

In Figure 16.5, we show a multithreaded process with four threads: the main thread, two threads of the function f1(), and one thread for the function f3(). A function that is designed to become a thread must terminate with a library function that terminates the thread, such as pthread_exit(...). We use the names of the Pthreads library functions for the creation and termination of threads. Note that you need to include the header file /usr/include/pthread.h in your program and link the Pthreads library with the executable code using the -pthread option with the gcc compiler, as in

```
gcc -w -pthread prog.c -o prog
```

The typical graphical representations of single-threaded and multithreaded processes are shown in Figure 16.6. Note that after tid3 has started running and tid1 has not finished, four threads run simultaneously: main, tid1, tid2, and tid3.

### 16.2.6 Commonalities and Differences between Processes and Threads

Processes and threads have several things in common. For example, each has its own ID, stack, and PC.

There are several differences between processes and threads. For example, whereas processes operate within their own address spaces, threads within a process operate within the address space of the process. Similarly, processes have their own data and text (code) areas but threads share the text and data areas in the process.

### 16.2.7 Data Sharing among Threads and the Critical Section Problem

Data sharing among threads is a mixed blessing. Although this saves memory space by preventing the duplication of data, it does require that threads access data on a mutually exclusive basis by locking data before accessing it and unlocking it afterwards. If this were not done, the results produced by the process
