
caught (the process has established a signal handler by using sigaction, for example) and a thread is waiting for the same signal in a call to sigwait, it is left up to the implementation to decide which way to deliver the signal. The implementation could either allow sigwait to return or invoke the signal handler, but not both.

To send a signal to a process, we call kill (Section 10.9). To send a signal to a thread, we call pthread_kill.

```
#include <signal.h>

int pthread_kill(pthread_t thread, int signo);

Returns: 0 if OK, error number on failure
```

We can pass a signo value of 0 to check for existence of the thread. If the default action for a signal is to terminate the process, then sending the signal to a thread will still kill the entire process.

Note that alarm timers are a process resource, and all threads share the same set of alarms. Thus, it is not possible for multiple threads in a process to use alarm timers without interfering (or cooperating) with one another (this is the subject of Exercise 12.6).

## Example

Recall that in Figure 10.23, we waited for the signal handler to set a flag indicating that the main program should exit. The only threads of control that could run were the main thread and the signal handler, so blocking the signals was sufficient to avoid missing a change to the flag. With threads, we need to use a mutex to protect the flag, as we show in Figure 12.16.

```
#include "apue.h"
#include <pthread.h>

int quitflag;    /* set nonzero by thread */
sigset_t mask;

pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t waitloc = PTHREAD_COND_INITIALIZER;

void *
thr_fn(void *arg)
{
    int err, signo;

    for (;;) {
        err = sigwait(&mask, &signo);
        if (err != 0)
            err_exit(err, "sigwait failed");
        switch (signo) {
        case SIGINT:
            printf("\ninterrupt\n");
            break;
case SIGQUIT:
    pthread_mutex_lock(&lock);
    quitflag = 1;
    pthread_mutex_unlock(&lock);
    pthread_cond_signal(&waitloc);
    return(0);

default:
    printf("unexpected signal %d\n", signo);
    exit(1);
}
}

int
main(void)
{
    int        err;
    sigset_t   oldmask;
    pthread_t  tid;

    sigemptyset(&mask);
    sigaddset(&mask, SIGINT);
    sigaddset(&mask, SIGQUIT);
    if ((err = pthread_sigmask(SIG_BLOCK, &mask, &oldmask)) != 0)
        err_exit(err, "SIG_BLOCK error");

    err = pthread_create(&tid, NULL, thr_fn, 0);
    if (err != 0)
        err_exit(err, "can't create thread");

    pthread_mutex_lock(&lock);
    while (quitflag == 0)
        pthread_cond_wait(&waitloc, &lock);
    pthread_mutex_unlock(&lock);

    /* SIGQUIT has been caught and is now blocked; do whatever */
    quitflag = 0;

    /* reset signal mask which unblocks SIGQUIT */
    if (sigprocmask(SIG_SETMASK, &oldmask, NULL) < 0)
        err_sys("SIG_SETMASK error");
    exit(0);
}
```

## Figure 12.16 Synchronous signal handling

Instead of relying on a signal handler that interrupts the main thread of control, we dedicate a separate thread of control to handle the signals. We change the value of quitflag under the protection of a mutex so that the main thread of control can't miss the wake-up call made when we call pthread_cond_signal. We use the same mutex

in the main thread of control to check the value of the flag and atomically release the mutex when we wait for the condition.

Note that we block SIGINT and SIGQUIT in the beginning of the main thread. When we create the thread to handle signals, the thread inherits the current signal mask. Since sigwait will unblock the signals, only one thread is available to receive signals. This enables us to code the main thread without having to worry about interrupts from these signals.

If we run this program, we get output similar to that from Figure 10.23:

```
$ ./a.out
^?          type the interrupt character
interrupt
^?          type the interrupt character again
interrupt
^?          and again
interrupt
^\ $        now terminate with quit character
```

## 12.9 Threads and fork

When a thread calls fork, a copy of the entire process address space is made for the child. Recall the discussion of copy-on-write in Section 8.3. The child is an entirely different process from the parent, and as long as neither one makes changes to its memory contents, copies of the memory pages can be shared between parent and child.

By inheriting a copy of the address space, the child also inherits the state of every mutex, reader-writer lock, and condition variable from the parent process. If the parent consists of more than one thread, the child will need to clean up the lock state if it isn’t going to call exec immediately after fork returns.

Inside the child process, only one thread exists. It is made from a copy of the thread that called fork in the parent. If the threads in the parent process hold any locks, the same locks will also be held in the child process. The problem is that the child process doesn’t contain copies of the threads holding the locks, so there is no way for the child to know which locks are held and need to be unlocked.

```
#include <pthread.h>
int pthread_atfork(void (*prepare)(void), void (*parent)(void), void (*child)(void));
Returns: 0 if OK, error number on failure
```

With pthread_atfork, we can install up to three functions to help clean up the locks. The prepare fork handler is called in the parent before fork creates the child process. This fork handler’s job is to acquire all locks defined by the parent. The parent fork handler is called in the context of the parent after fork has created the child process, but before fork has returned. This fork handler’s job is to unlock all the locks acquired by the prepare fork handler. The child fork handler is called in the context of the child process before returning from fork. Like the parent fork handler, the child fork handler must release all the locks acquired by the prepare fork handler.

Note that the locks are not locked once and unlocked twice, as it might appear. When the child address space is created, it gets a copy of all locks that the parent defined. Because the prepare fork handler acquired all the locks, the memory in the parent and the memory in the child start out with identical contents. When the parent and the child unlock their “copy” of the locks, new memory is allocated for the child, and the memory contents from the parent are copied to the child’s memory (copy-on-write), so we are left with a situation that looks as if the parent locked all its copies of the locks and the child locked all its copies of the locks. The parent and the child end up unlocking duplicate locks stored in different memory locations, as if the following sequence of events occurred:

- 1. The parent acquired all its locks.
- 2. The child acquired all its locks.
- 3. The parent released its locks.
- 4. The child released its locks.

We can call pthread_atfork multiple times to install more than one set of fork handlers. If we don’t have a need to use one of the handlers, we can pass a null pointer for the particular handler argument, and it will have no effect. When multiple fork handlers are used, the order in which the handlers are called differs. The parent and child fork handlers are called in the order in which they were registered, whereas the prepare fork handlers are called in the opposite order from which they were registered. This ordering allows multiple modules to register their own fork handlers and still honor the locking hierarchy.

- 3. A child process is created.
- 4. The child fork handler from module B is called to release all of module B's locks in the child process.
- 5. The child fork handler from module A is called to release all of module A's locks in the child process.
- 6. The fork function returns to the child.
- 7. The parent fork handler from module B is called to release all of module B's locks in the parent process.
- 8. The parent fork handler from module A is called to release all of module A's locks in the parent process.
- 9. The fork function returns to the parent.

If the fork handlers serve to clean up the lock state, what cleans up the state of condition variables? On some implementations, condition variables might not need any cleaning up. However, an implementation that uses a lock as part of the implementation of condition variables will require cleaning up. The problem is that no interface exists to allow us to do this. If the lock is embedded in the condition variable data structure, then we can't use condition variables after calling fork, because there is no portable way to clean up its state. On the other hand, if an implementation uses a global lock to protect all condition variable data structures in a process, then the implementation itself can clean up the lock in the fork library routine. Application programs shouldn't rely on implementation details like this, however.

## Example

The program in Figure 12.17 illustrates the use of pthread_atfork and fork handlers.

```
#include "apue.h"
#include <pthread.h>

pthread_mutex_t lock1 = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t lock2 = PTHREAD_MUTEX_INITIALIZER;

void
prepare(void)
{
    int err;

    printf("preparing locks...\n");
    if ((err = pthread_mutex_lock(&lock1)) != 0)
        err_cont(err, "can't lock lock1 in prepare handler");
    if ((err = pthread_mutex_lock(&lock2)) != 0)
        err_cont(err, "can't lock lock2 in prepare handler");
}

void
parent(void)
{
```
