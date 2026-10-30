
## 10.19 sleep, nanosleep, and clock_nanosleep Functions

We’ve used the sleep function in numerous examples throughout the text, and we showed two flawed implementations of it in Figures 10.7 and 10.8.

```
#include <unistd.h>
unsigned int sleep(unsigned int seconds);
Returns: 0 or number of unslept seconds
```

This function causes the calling process to be suspended until either

- 1. The amount of wall clock time specified by seconds has elapsed.
- 2. A signal is caught by the process and the signal handler returns.

As with an alarm signal, the actual return may occur at a time later than requested because of other system activity.

In case 1, the return value is 0. When sleep returns early because of some signal being caught (case 2), the return value is the number of unslept seconds (the requested time minus the actual time slept).

Although sleep can be implemented with the alarm function (Section 10.10), this isn’t required. If alarm is used, however, there can be interactions between the two functions. The POSIX.1 standard leaves all these interactions unspecified. For example, if we do an alarm(10) and 3 wall clock seconds later do a sleep(5), what happens? The sleep will return in 5 seconds (assuming that some other signal isn’t caught in the interim), but will another SIGALRM be generated 2 seconds later? These details depend on the implementation.

> FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8, and Solaris 10 implement sleep using the nanosleep function, which allows the implementation to be independent of signals and the alarm timer. For portability, you shouldn’t make any assumptions about the implementation of sleep, but if you have any intentions of mixing calls to sleep with any other timing functions, you need to be aware of possible interactions.

### Example

Figure 10.29 shows an implementation of the POSIX.1 sleep function. This function is a modification of Figure 10.7, which handles signals reliably, avoiding the race condition in the earlier implementation. We still do not handle any interactions with previously set alarms. (As we mentioned, these interactions are explicitly undefined by POSIX.1.)

```
#include "apue.h"

static void
sig_alarm(int signo)
{
    /* nothing to do, just returning wakes up sigsuspend() */
}
unsigned int
sleep(unsigned int seconds)
{
    struct sigaction  newact, oldact;
    sigset_t          newmask, oldmask, suspmask;
    unsigned int      unslept;
    /* set our handler, save previous information */
    newact.sa_handler = sig_alrm;
    sigemptyset(&newact.sa_mask);
    newact.sa_flags = 0;
    sigaction(SIGALRM, &newact, &oldact);
    /* block SIGALRM and save current signal mask */
    sigemptyset(&newmask);
    sigaddset(&newmask, SIGALRM);
    sigprocmask(SIG_BLOCK, &newmask, &oldmask);
    alarm(seconds);
    suspmask = oldmask;
    /* make sure SIGALRM isn't blocked */
    sigdelset(&suspmask, SIGALRM);
    /* wait for any signal to be caught */
    sigsuspend(&suspmask);
    /* some signal has been caught, SIGALRM is now blocked */
    unslept = alarm(0);
    /* reset previous action */
    sigaction(SIGALRM, &oldact, NULL);
    /* reset signal mask, which unblocks SIGALRM */
    sigprocmask(SIG_SETMASK, &oldmask, NULL);
    return(unslept);
}
```

### Figure 10.29 Reliable implementation of sleep

It takes more code to write this reliable implementation than what is shown in Figure 10.7. We don't use any form of nonlocal branching (as we did in Figure 10.8 to avoid the race condition between alarm and pause), so there is no effect on other signal handlers that may be executing when the SIGALRM is handled.

The nanosleep function is similar to the sleep function, but provides nanosecond-level granularity.

```
#include <time.h>
int nanosleep(const struct timespec *reqtp, struct timespec *remtp);
Returns: 0 if slept for requested time or -1 on error
```

This function suspends the calling process until either the requested time has elapsed or the function is interrupted by a signal. The reqtp parameter specifies the amount of time to sleep in seconds and nanoseconds. If the sleep interval is interrupted by a signal and the process doesn’t terminate, the timespec structure pointed to by the remtp parameter will be set to the amount of time left in the sleep interval. We can set this parameter to NULL if we are uninterested in the time unslept.

If the system doesn’t support nanosecond granularity, the requested time is rounded up. Because the nanosleep function doesn’t involve the generation of any signals, we can use it without worrying about interactions with other functions.

> The nanosleep function used to belong to the Timers option in the Single UNIX Specification, but was moved to the base in SUSv4.

With the introduction of multiple system clocks (recall Section 6.10), we need a way to suspend the calling thread using a delay time relative to a particular clock. The clock_nanosleep function provides us with this capability.

```
#include <time.h>
int clock_nanosleep(const clockid_t clock_id, int flags,
    const struct timespec *reqtp, struct timespec *remtp);
Returns: 0 if slept for requested time or error number on failure
```

The clock_id argument specifies the clock against which the time delay is evaluated. Identifiers for clocks are listed in Figure 6.8. The flags argument is used to control whether the delay is absolute or relative. When flags is set to 0, the sleep time is relative (i.e., how long we want to sleep). When it is set to TIMER_ABSTIME, the sleep time is absolute (i.e., we want to sleep until the clock reaches the specified time).

The other arguments, reqtp and remtp, are the same as in the nanosleep function. However, when we use an absolute time, the remtp argument is unused, because it isn’t needed; we can reuse the same value for the reqtp argument for additional calls to clock_nanosleep until the clock reaches the specified absolute time value.

Note that except for error returns, the call
clock_nanosleep(CLOCK_REALTIME, 0, reqtp, remtp);
has the same effect as the call
nanosleep(reqtp, remtp);

The problem with using a relative sleep is that some applications require precision with how long they sleep, and a relative sleep time can lead to sleeping longer than desired. For example, if an application wants to perform a task at regular intervals, it would have to get the current time, calculate the amount of time until the next time to execute the task, and then call nanosleep. Between the time that the current time is obtained and the call to nanosleep is made, processor scheduling and preemption can result in the relative sleep time extending past the desired interval. Using an absolute time improves the precision, even though a time-sharing process scheduler makes no guarantee that our task will execute immediately after our sleep time has ended.

> In older versions of the Single UNIX Specification, the clock_nanosleep function belonged to the Clock Selection option. In SUSv4, it was moved to the base.

## 10.20 sigqueue Function

In Section 10.8 we said that most UNIX systems don’t queue signals. With the real-time extensions to POSIX.1, some systems began adding support for queueing signals. With SUSv4, the queued signal functionality has moved from the real-time extensions to the base specification.

Generally a signal carries one bit of information: the signal itself. In addition to queueing signals, these extensions allow applications to pass more information along with the delivery (recall Section 10.14). This information is embedded in a siginfo structure. Along with system-provided information, applications can pass an integer or a pointer to a buffer containing more information to the signal handler.

To use queued signals we have to do the following:

- 1. Specify the SA_SIGINFO flag when we install a signal handler using the sigaction function. If we don’t specify this flag, the signal will be posted, but it is left up to the implementation whether the signal is queued.
- 2. Provide a signal handler in the sa_sigaction member of the sigaction structure instead of using the usual sa_handler field. Implementations might allow us to use the sa_handler field, but we won’t be able to obtain the extra information sent with the sigqueue function.
- 3. Use the sigqueue function to send signals.

```
#include <signal.h>
int sigqueue(pid_t pid, int signo, const union sigval value)
Returns: 0 if OK, -1 on error
```

The sigqueue function is similar to the kill function, except that we can only direct signals to a single process with sigqueue, and we can use the value argument to transmit either an integer or a pointer value to the signal handler.

Signals can’t be queued infinitely. Recall the SIGQUEUE_MAX limit from Figure 2.9 and Figure 2.11. When this limit is reached, sigqueue can fail with errno set to EAGAIN.

With the real-time signal enhancements, a separate set of signals was introduced for application use. These are the signal numbers between SIGRTMIN and SIGRTMAX, inclusive. Be aware that the default action for these signals is to terminate the process.

Figure 10.30 summarizes the way queued signals differ in behavior among the implementations covered in this text.

| Behavior | SUS | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|
| supports sigqueue | • | • | • |  | • |
| queues other signals besides SIGRTMIN to SIGRTMAX | optional | • |  |  | • |
| queues signals even if the caller doesn’t use the SA_SIGINFO flag | optional | • | • |  |  |

Figure 10.30 Behavior of queued signals on various platforms
