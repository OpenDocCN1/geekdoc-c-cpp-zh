wrote the new contents to a temporary file, removed the original file, and then renamed the temporary file to be the original file. The mandatory record locking has no effect on the unlink function, which allowed this to happen.

Under FreeBSD 8.0 and Solaris 10, we can obtain the system call trace of a process with the truss(1) command. Linux 3.2.0 provides the strace(1) command for the same purpose. Mac OS X 10.6.8 provides the dtruss(1m) command to trace system calls, but its use requires superuser privileges.

+   - The vi editor was never able to edit the file. It could read the file’s contents, but whenever we tried to write new data to the file, EAGAIN was returned. If we tried to append new data to the file, the write blocked. This behavior from vi is what we expect.
+   - Using the Korn shell’s > and >> operators to overwrite or append to the file resulted in the error “cannot create.”
+   - Using the same two operators with the Bourne shell resulted in an error for >, but the >> operator just blocked until the mandatory lock was removed, and then proceeded. (The difference in the handling of the append operator occurs because the Korn shell opens the file with O_CREAT and O_APPEND, and we mentioned earlier that specifying O_CREAT generates an error. The Bourne shell, however, doesn’t specify O_CREAT if the file already exists, so the open succeeds but the next write blocks.)

Results will vary, depending on the version of the operating system you are using. The bottom line, as demonstrated by this exercise, is to be wary of mandatory record locking. As seen with the ed example, it can be circumvented.

Mandatory record locking can also be used by a malicious user to hold a read lock on a file that is publicly readable. This can prevent anyone from writing to the file. (Of course, the file has to have mandatory record locking enabled for this to occur, which may require the user to be able to change the permission bits of the file.) Consider a database file that is world readable and has mandatory record locking enabled. If a malicious user were to hold a read lock on the entire file, the file could not be written to by other processes.

# Example

We can run the program in Figure 14.12 to determine whether our system supports mandatory locking.

```
```c
#include "apue.h"
#include <errno.h>
#include <fcntl.h>
#include <sys/wait.h>

int
main(int argc, char *argv[])
{
    int              fd;
```
```