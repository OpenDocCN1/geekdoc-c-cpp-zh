
I/O multiplexing was provided with the select function in 4.2BSD. This function has always worked with any descriptor, although its main use has been for terminal I/O and network I/O. SVR3 added the poll function when the STREAMS mechanism was added. Initially, poll worked only with STREAMS devices. In SVR4, support was added to allow poll to work on any descriptor.

## 14.4.1 select and pselect Functions

The select function lets us do I/O multiplexing under all POSIX-compatible platforms. The arguments we pass to select tell the kernel

- Which descriptors we're interested in.
- Which conditions we're interested in for each descriptor. (Do we want to read from a given descriptor? Do we want to write to a given descriptor? Are we interested in an exception condition for a given descriptor?)
- How long we want to wait. (We can wait forever, wait a fixed amount of time, or not wait at all.)

On the return from select, the kernel tells us

- The total count of the number of descriptors that are ready
- Which descriptors are ready for each of the three conditions (read, write, or exception condition)

With this return information, we can call the appropriate I/O function (usually read or write) and know that the function won't block.

```
#include <sys/select.h>

int select(int maxfdp1, fd_set *restrict readfds,
    fd_set *restrict writefds, fd_set *restrict exceptfds,
    struct timeval *restrict tvptr);

Returns: count of ready descriptors, 0 on timeout, -1 on error
```

Let's look at the last argument first. It specifies how long we want to wait in terms of seconds and microseconds (recall Section 4.20). There are three conditions.

tvptr == NULL

Wait forever. This infinite wait can be interrupted if we catch a signal. Return is made when one of the specified descriptors is ready or when a signal is caught. If a signal is caught, select returns -1 with errno set to EINTR.

tvptr->tv_sec == 0 && tvptr->tv_usec == 0

Don't wait at all. All the specified descriptors are tested, and return is made immediately. This is a way to poll the system to find out the status of multiple descriptors without blocking in the select function.

tvptr->tv_sec != 0 || tvptr->tv_usec != 0

Wait the specified number of seconds and microseconds. Return is made when one of the specified descriptors is ready or when the timeout value expires. If the timeout expires before any of the descriptors is ready, the return value is 0. (If the system doesn't provide microsecond resolution, the tvptr->tv_usec value is rounded up to the nearest supported value.) As with the first condition, this wait can also be interrupted by a caught signal.

> POSIX.1 allows an implementation to modify the timeval structure, so after select returns, you can't rely on the structure containing the same values it did before calling select. FreeBSD 8.0, Mac OS X 10.6.8, and Solaris 10 all leave the structure unchanged, but Linux 3.2.0 will update it with the time remaining if select returns before the timeout value expires.

The middle three arguments—readfds, writefds, and exceptfds—are pointers to descriptor sets. These three sets specify which descriptors we're interested in and for which conditions (readable, writable, or an exception condition). A descriptor set is stored in an fd_set data type. This data type is chosen by the implementation so that it can hold one bit for each possible descriptor. We can consider it to be just a big array of bits, as shown in Figure 14.15.

![](img/244bf0c3b6d0288ae397336907e37851_536_0.png)

### Figure 14.15 Specifying the read, write, and exception descriptors for select

The only thing we can do with the fd_set data type is allocate a variable of this type, assign a variable of this type to another variable of the same type, or use one of the following four functions on a variable of this type.

```
#include <sys/select.h>

int FD_ISSET(int fd, fd_set *fdset);

Returns: nonzero if fd is in set, 0 otherwise

void FD_CLR(int fd, fd_set *fdset);
void FD_SET(int fd, fd_set *fdset);
void FD_ZERO(fd_set *fdset);
```

These interfaces can be implemented as either macros or functions. An fd_set is set to all zero bits by calling FD_ZERO. To turn on a single bit in a set, we use FD_SET. We can clear a single bit by calling FD_CLR. Finally, we can test whether a given bit is turned on in the set with FD_ISSET.

After declaring a descriptor set, we must zero the set using FD_ZERO. We then set bits in the set for each descriptor that we’re interested in, as in

```
fd_set rset;
int fd;

FD_ZERO(&rset);
FD_SET(fd, &rset);
FD_SET(STDIN_FILENO, &rset);
```

On return from select, we can test whether a given bit in the set is still on using FD_ISSET:

```
if (FD_ISSET(fd, &rset)) {
    :
}
```

Any (or all) of the middle three arguments to select (the pointers to the descriptor sets) can be null pointers if we’re not interested in that condition. If all three pointers are NULL, then we have a higher-precision timer than is provided by sleep. (Recall from Section 10.19 that sleep waits for an integral number of seconds. With select, we can wait for intervals less than one second; the actual resolution depends on the system’s clock.) Exercise 14.5 shows such a function.

The first argument to select, maxfdp1, stands for “maximum file descriptor plus 1.” We calculate the highest descriptor that we’re interested in, considering all three of the descriptor sets, add 1, and that’s the first argument. We could just set the first argument to FD_SETSIZE, a constant in <sys/select.h> that specifies the maximum number of descriptors (often 1,024), but this value is too large for most applications. Indeed, most applications probably use between 3 and 10 descriptors. (Some applications need many more descriptors, but these UNIX programs are atypical.) By specifying the highest descriptor that we’re interested in, we can prevent the kernel from going through hundreds of unused bits in the three descriptor sets, looking for bits that are turned on.

As an example, Figure 14.16 shows what two descriptor sets look like if we write

```
fd_set readset, writeset;

FD_ZERO(&readset);
FD_ZERO(&writeset);
FD_SET(0, &readset);
FD_SET(3, &readset);
FD_SET(1, &writeset);
FD_SET(2, &writeset);
select(4, &readset, &writeset, NULL, NULL);
```

It is important to realize that whether a descriptor is blocking or not doesn’t affect whether select blocks. That is, if we have a nonblocking descriptor that we want to read from and we call select with a timeout value of 5 seconds, select will block for up to 5 seconds. Similarly, if we specify an infinite timeout, select blocks until data is ready for the descriptor or until a signal is caught.

If we encounter the end of file on a descriptor, that descriptor is considered readable by select. When the call read and it returns 0—the way to signify end of file on UNIX systems. (Many people incorrectly assume that select indicates an exception condition on a descriptor when the end of file is reached.)

POSIX.1 also defines a variant of select called pselect.

```
#include <sys/select.h>

int pselect(int maxfd1, fd_set *restrict readfds,
            fd_set *restrict writefds, fd_set *restrict exceptfds,
            const struct timespec *restrict ts,
            const sigset_t *restrict sigmask);
```

Returns: count of ready descriptors, 0 on timeout, -1 on error

The pselect function is identical to select, with the following exceptions.

- The timeout value for select is specified by a timeval structure, but for pselect, a timespec structure is used. (Recall the definition of the timespec structure in Section 4.2.) Instead of seconds and microseconds, the timespec structure represents the timeout value in seconds and nanoseconds. This provides a higher-resolution timeout if the platform supports that fine a level of granularity.
- The timeout value for pselect is declared const, and we are guaranteed that its value will not change as a result of calling pselect.
- An optional signal mask argument is available with pselect. If sigmask is NULL, pselect behaves as select does with respect to signals. Otherwise, sigmask points to a signal mask that is atomically installed when pselect is called. On return, the previous signal mask is restored.

## 14.4.2 poll Function

The poll function is similar to select, but the programmer interface is different. This function was originally introduced in System V to support the STREAMS subsystem, but we are able to use it with any type of file descriptor.

```
#include <poll.h>

int poll(struct pollfd farray[], nfds_t nfds, int timeout);
```

Returns: count of ready descriptors, 0 on timeout, -1 on error
