kernel and is known as a system process. Process ID 1 is usually the init process and is invoked by the kernel at the end of the bootstrap procedure. The program file for this process was `/etc/init` in older versions of the UNIX System and is `/sbin/init` in newer versions. This process is responsible for bringing up a UNIX system after the kernel has been bootstrapped. init usually reads the system-dependent initialization files—the `/etc/rc*` files or `/etc/inittab` and the files in `/etc/init.d`—and brings the system to a certain state, such as multiuser. The init process never dies. It is a normal user process, not a system process within the kernel, like the swapper, although it does run with superuser privileges. Later in this chapter, we’ll see how init becomes the parent process of any orphaned child process.

> In Mac OS X 10.4, the init process was replaced with the launchd process, which performs the same set of tasks as init, but has expanded functionality. See Section 5.10 in Sing [2006] for a discussion of how launchd operates.

Each UNIX System implementation has its own set of kernel processes that provide operating system services. For example, on some virtual memory implementations of the UNIX System, process ID 2 is the `page daemon`. This process is responsible for supporting the paging of the virtual memory system.

In addition to the process ID, there are other identifiers for every process. The following functions return these identifiers.

```
```c
#include <unistd.h>

pid_t getpid(void);
                         Returns: process ID of calling process

pid_t getppid(void);
                         Returns: parent process ID of calling process

uid_t getuid(void);
                         Returns: real user ID of calling process

uid_t geteuid(void);
                         Returns: effective user ID of calling process

gid_t getgid(void);
                         Returns: real group ID of calling process

gid_t getegid(void);
                         Returns: effective group ID of calling process
```
```

Note that none of these functions has an error return. We’ll return to the parent process ID in the next section when we discuss the fork function. The real and effective user and group IDs were discussed in Section 4.4.