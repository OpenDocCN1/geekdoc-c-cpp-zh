| Type | Description |
|---|---|
| clock_t | counter of clock ticks (process time) (Section 1.10) |
| comp_t | compressed clock ticks (not defined by POSIX.1; see Section 8.14) |
| dev_t | device numbers (major and minor) (Section 4.24) |
| fd_set | file descriptor sets (Section 4.4.1) |
| fpos_t | file position (Section 5.10) |
| gid_t | numeric group IDs |
| ino_t | i-node numbers (Section 4.14) |
| mode_t | file type, file creation mode (Section 4.5) |
| nlink_t | link counts for directory entries (Section 4.14) |
| off_t | file sizes and offsets (signed) lseek, Section 3.6) |
| pid_t | process IDs and process group IDs (signed) (Sections 8.2 and 9.4) |
| pthread_t | thread IDs (Section 11.3) |
| ptrdiff_t | result of subtracting two pointers (signed) |
| rlim_t | resource limits (Section 7.11) |
| sig_atomic_t | data type that can be accessed atomically (Section 10.15) |
| sigset_t | signal set (Section 10.11) |
| size_t | sizes of objects (such as strings) (unsigned) (Section 3.7) |
| ssize_t | functions that return a count of bytes (signed) (read, write, Section 3.7) |
| time_t | counter of seconds of calendar time (Section 1.10) |
| uid_t | numeric user IDs |
| wchar_t | can represent all distinct character codes |

# Figure 2.21 Some common primitive system data types

convert this value to seconds, we divide it by CLOCKS_PER_SEC, which is defined in the <time.h> header. POSIX.1 defines the function times that returns both the CPU time (for the caller and all its terminated children) and the clock time. All these time values are clock_t values. The sysconf function is used to obtain the number of clock ticks per second for use with the return values from the times function. What we have is the same data type (clock_t) used to hold measurements of time defined with different units by ISO C and POSIX.1. The difference can be seen in Solaris, where clock returns microseconds (hence CLOCKS_PER_SEC is 1 million), whereas sysconf returns the value 100 for clock ticks per second. Thus we must take care when using variables of type clock_t so that we don’t mix variables with different units.

Another area of potential conflict is when the ISO C standard specifies a function, but doesn’t specify it as strongly as POSIX.1 does. This is the case for functions that require a different implementation in a POSIX environment (with multiple processes) than in an ISO C environment (where very little can be assumed about the host operating system). Nevertheless, POSIX-compliant systems implement the ISO C function for compatibility. The signal function is an example. If we unknowingly use the signal function provided by Solaris (hoping to write portable code that can be run in ISO C environments and under older UNIX systems), it will provide semantics different from the POSIX.1 sigaction function. We’ll have more to say about the signal function in Chapter 10.