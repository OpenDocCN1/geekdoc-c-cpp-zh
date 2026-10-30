+   If times is a non-null pointer and both tv_nsec fields are set to UTIME_OMIT, no permissions checks are performed.

With futimens, you need to open the file to change its times. The utimensat function provides a way to change a file's times using the file's name. The pathname argument is evaluated relative to the fd argument, which is either a file descriptor of an open directory or the special value AT_FDCWD to force evaluation relative to the current directory of the calling process. If pathname specifies an absolute pathname, then the fd argument is ignored.

The flag argument to utimensat can be used to further modify the default behavior. If the AT_SYMLINK_NOFOLLOW flag is set, then the times of the symbolic link itself are changed (if the pathname refers to a symbolic link). The default behavior is to follow a symbolic link and modify the times of the file to which the link refers.

Both futimens and utimensat are included in POSIX.1. A third function, utimes, is included in the Single UNIX Specification as part of the XSI option.

```
#include <sys/time.h>
int utimes(const char *pathname, const struct timeval times[2]);
Returns: 0 if OK, -1 on error
```

The utimes function operates on a pathname. The times argument is a pointer to an array of two timestamps—access time and modification time—but they are expressed in seconds and microseconds:

```
struct timeval {
    time_t tv_sec;    /* seconds */
    long   tv_usec;   /* microseconds */
};
```

Note that we are unable to specify a value for the changed-status time, st_ctim—the time the i-node was last changed—as this field is automatically updated when the utime function is called.

On some versions of the UNIX System, the touch(1) command uses one of these functions. Also, the standard archive programs, tar(1) and cpio(1), optionally call these functions to set a file's times to the time values saved when the file was archived.

# Example

The program shown in Figure 4.21 truncates files to zero length using the O_TRUNC option of the open function, but does not change their access time or modification time. To do this, the program first obtains the times with the stat function, truncates the file, and then resets the times with the futimens function.

```
#include "apue.h"
#include <fcntl.h>

int
main(int argc, char *argv[])
```