Each of the 25 invariant minimum values in Figure 2.8 has an associated implementation value whose name is formed by removing the _POSIX_ prefix from the name in Figure 2.8. The names without the leading _POSIX_ were intended to be the actual values that a given implementation supports. (These 25 implementation values are from items 1, 4, 5, and 7 from our list earlier in this section: 2 of the runtime increasable values, 15 of the runtime invariant values, and 7 of the pathname variable values, along with SSIZE_MAX from the numeric values.) The problem is that not all of the 25 implementation values are guaranteed to be defined in the <limits.h> header.

For example, a particular value may not be included in the header if its actual value for a given process depends on the amount of memory on the system. If the values are not defined in the header, we can’t use them as array bounds at compile time. To determine the actual implementation value at runtime, POSIX.1 decided to provide three functions for us to call—sysconf, pathconf, and fpathconf. There is still a problem, however, because some of the values are defined by POSIX.1 as being possibly “indeterminate” (logically infinite). This means that the value has no practical upper bound. On Solaris, for example, the number of functions you can register with atexit to be run when a process ends is limited only by the amount of memory on the system. Thus ATEXIT_MAX is considered indeterminate on Solaris. We’ll return to this problem of indeterminate runtime limits in Section 2.5.5.

# 2.5.3 XSI Limits

The XSI option also defines constants representing implementation limits. They include:

+   1. Minimum values: the five constants in Figure 2.10
+   2. Runtime invariant values, possibly indeterminate: IOV_MAX and PAGE_SIZE

The minimum values are listed in Figure 2.10. The last two illustrate the situation in which the POSIX.1 minimums were too small—presumably to allow for embedded POSIX.1 implementations—so symbols with larger minimum values were added for XSI-conforming systems.

| Name | Description | Minimum acceptable value | Typical value |
|---|---|---|---|
| NL_LANGMAX | maximum number of bytes in LANG environment variable | 14 | 14 |
| NZERO | default process priority | 20 | 20 |
| _XOPEN_IOV_MAX | maximum number of iovec structures that can be used with readv or writev | 16 | 16 |
| _XOPEN_NAME_MAX | number of bytes in a filename | 255 | 255 |
| _XOPEN_PATH_MAX | number of bytes in a pathname | 1,024 | 1,024 |

Figure 2.10 XSI minimum values from <limits.h>