```
#include <unistd.h>
pid_t getpgid(pid_t pid);

Returns: process group ID if OK, -1 on error
```

If pid is 0, the process group ID of the calling process is returned. Thus

```
getpgid(0);
```

is equivalent to

```
getpgrp();
```

Each process group can have a process group leader. The leader is identified by its process group ID being equal to its process ID.

It is possible for a process group leader to create a process group, create processes in the group, and then terminate. The process group still exists, as long as at least one process is in the group, regardless of whether the group leader terminates. This is called the process group lifetime—the period of time that begins when the group is created and ends when the last remaining process leaves the group. The last remaining process in the process group can either terminate or enter some other process group.

A process joins an existing process group or creates a new process group by calling setpgid. (In the next section, we’ll see that setsid also creates a new process group.)

```
#include <unistd.h>
int setpgid(pid_t pid, pid_t pgid);

Returns: 0 if OK, -1 on error
```

This function sets the process group ID to pgid in the process whose process ID equals pid. If the two arguments are equal, the process specified by pid becomes a process group leader. If pid is 0, the process ID of the caller is used. Also, if pgid is 0, the process ID specified by pid is used as the process group ID.

A process can set the process group ID of only itself or any of its children. Furthermore, it can’t change the process group ID of one of its children after that child has called one of the exec functions.

In most job-control shells, this function is called after a fork to have the parent set the process group ID of the child, and to have the child set its own process group ID. One of these calls is redundant, but by doing both, we are guaranteed that the child is placed into its own process group before either process assumes that this has happened. If we didn’t do this, we would have a race condition, since the child’s process group membership would depend on which process executes first.

When we discuss signals, we’ll see how we can send a signal to either a single process (identified by its process ID) or a process group (identified by its process group ID). Similarly, the waitpid function from Section 8.6 lets us wait for either a single process or one process from a specified process group.