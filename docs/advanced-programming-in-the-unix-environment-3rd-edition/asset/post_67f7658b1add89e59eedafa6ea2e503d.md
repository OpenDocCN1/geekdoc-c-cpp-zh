
For each option, we have three possibilities for a platform’s support status.

+   1. If the symbolic constant is either undefined or defined to have the value -1, then the corresponding option is unsupported by the platform at compile time. It is possible to run an old application on a newer system where the option is supported, so a runtime check might indicate the option is supported even though the option wasn’t supported at the time the application was compiled.
+   2. If the symbolic constant is defined to be greater than zero, then the corresponding option is supported.
+   3. If the symbolic constant is defined to be equal to zero, then we must call sysconf, pathconf, or fpathconf to determine whether the option is supported.

The symbolic constants used with pathconf and fpathconf are summarized in Figure 2.18. Figure 2.19 summarizes the nonobsolete options and their symbolic constants that can be used with sysconf, in addition to those listed in Figure 2.5. Note that we omit options associated with utility commands.

As with the system limits, there are several points to note regarding how options are treated by sysconf, pathconf, and fpathconf.

+   1. The value returned for _SC_VERSION indicates the four-digit year and two-digit month of the standard. This value can be 198808L, 199009L, 199506L, or some other value for a later version of the standard. The value associated with Version 3 of the Single UNIX Specification is 200112L (the 2001 edition of POSIX.1). The value associated with Version 4 of the Single UNIX Specification (the 2008 edition of POSIX.1) is 200809L.
+   2. The value returned for _SC_XOPEN_VERSION indicates the version of the XSI that the system supports. The value associated with Version 3 of the Single UNIX Specification is 600. The value associated with Version 4 of the Single UNIX Specification (the 2008 edition of POSIX.1) is 700.
+   3. The values _SC_JOB_CONTROL, _SC_SAVED_IDS, and _PC_VDISABLE no longer represent optional features. Although XPG4 and prior versions of the Single UNIX Specification required that these features be supported, Version 3 of the Single UNIX Specification is the earliest version where these features are no longer optional in POSIX.1. These symbols are retained for backward compatibility.
+   4. Platforms conforming to POSIX.1-2008 are also required to support the following options:

+   - _POSIX_ASYNCHRONOUS_IO
+   - _POSIX_BARRIERS
+   - _POSIX_CLOCK_SELECTION
+   - _POSIX_MAPPED_FILES
+   - _POSIX_MEMORY_PROTECTION
+   - `_POSIX_READER_WRITER_LOCKS`
+   - `_POSIX_REALTIME_SIGNALS`
+   - `_POSIX_SEMAPHORES`
+   - `_POSIX_SPIN_LOCKS`
+   - `_POSIX_THREAD_SAFE_FUNCTIONS`
+   - `_POSIX_THREADS`
+   - `_POSIX_TIMEOUTS`
+   - `_POSIX_TIMERS`

These constants are defined to have the value 200809L. Their corresponding _SC symbols are also retained for backward compatibility.

+   5. `_PC_CHOWN_RESTRICTED` and `_PC_NO_TRUNC` return -1 without changing `errno` if the feature is not supported for the specified *pathname* or *fd*. On all POSIX-conforming systems, the return value will be greater than zero (indicating that the feature is supported).
+   6. The referenced file for `_PC_CHOWN_RESTRICTED` must be either a file or a directory. If it is a directory, the return value indicates whether this option applies to files within that directory.
+   7. The referenced file for `_PC_NO_TRUNC` and `_PC_2_SYMLINKS` must be a directory.
+   8. For `_PC_NO_TRUNC`, the return value applies to filenames within the directory.
+   9. The referenced file for `_PC_VDISABLE` must be a terminal file.
+   10. For `_PC_ASYNC_IO`, `_PC_PRIO_IO`, and `_PC_SYNC_IO`, the referenced file must not be a directory.

| Name of option | Indicates ... | name argument |
|---|---|---|
| `_POSIX_CHOWN_RESTRICTED` | whether use of chown is restricted | `_PC_CHOWN_RESTRICTED` |
| `_POSIX_NO_TRUNC` | whether filenames longer than NAME_MAX generate an error | `_PC_NO_TRUNC` |
| `_POSIX_VDISABLE` | if defined, terminal special characters can be disabled with this value | `_PC_VDISABLE` |
| `_POSIX_ASYNC_IO` | whether asynchronous I/O can be used with the associated file | `_PC_ASYNC_IO` |
| `_POSIX_PRIO_IO` | whether prioritized I/O can be used with the associated file | `_PC_PRIO_IO` |
| `_POSIX_SYNC_IO` | whether synchronized I/O can be used with the associated file | `_PC_SYNC_IO` |
| `_POSIX2_SYMLINKS` | whether symbolic links are supported in the directory | `_PC_2_SYMLINKS` |

Figure 2.18 Options and name arguments to pathconf and fpathconf

| Name of option | Indicates | name argument |
|---|---|---|
| `_POSIX_ASYNCHRONOUS_IO` | whether the implementation supports POSIX asynchronous I/O | `_SC_ASYNCHRONOUS_IO` |
| `_POSIX_BARRIERS` | whether the implementation supports barriers | `_SC_BARRIERS` |
| `_POSIX_CLOCK_SELECTION` | whether the implementation supports clock selection | `_SC_CLOCK_SELECTION` |
| `_POSIX_JOB_CONTROL` | whether the implementation supports job control | `_SC_JOB_CONTROL` |
| `_POSIX_MAPPED_FILES` | whether the implementation supports memory-mapped files | `_SC_MAPPED_FILES` |
| `_POSIX_MEMORY_PROTECTION` | whether the implementation supports memory protection | `_SC_MEMORY_PROTECTION` |
| `_POSIX_READER_WRITER_LOCKS` | whether the implementation supports reader-writer locks | `_SC_READER_WRITER_LOCKS` |
| `_POSIX_REALTIME_SIGNALS` | whether the implementation supports real-time signals | `_SC_REALTIME_SIGNALS` |
| `_POSIX_SAVED_IDS` | whether the implementation supports the saved set-user-ID and the saved set-group-ID | `_SC_SAVED_IDS` |
| `_POSIX_SEMAPHORES` | whether the implementation supports POSIX semaphores | `_SC_SEMAPHORES` |
| `_POSIX_SHELL` | whether the implementation supports the POSIX shell | `_SC_SHELL` |
| `_POSIX_SPIN_LOCKS` | whether the implementation supports spin locks | `_SC_SPIN_LOCKS` |
| `_POSIX_THREAD_SAFE_FUNCTIONS` | whether the implementation supports thread-safe functions | `_SC_THREAD_SAFE_FUNCTIONS` |
| `_POSIX_THREADS` | whether the implementation supports threads | `_SC_THREADS` |
| `_POSIX_TIMEOUTS` | whether the implementation supports timeout-based variants of selected functions | `_SC_TIMEOUTS` |
| `_POSIX_TIMERS` | whether the implementation supports timers | `_SC_TIMERS` |
| `_POSIX_VERSION` | the POSIX.1 version | `_SC_VERSION` |
| `_XOPEN_CRYPT` | whether the implementation supports the XSI encryption option group | `_SC_XOPEN_CRYPT` |
| `_XOPEN_REALTIME` | whether the implementation supports the XSI real-time option group | `_SC_XOPEN_REALTIME` |
| `_XOPEN_REALTIME_THREADS` | whether the implementation supports the XSI real-time threads option group | `_SC_XOPEN_REALTIME_THREADS` |
| `_XOPEN_SHM` | whether the implementation supports the XSI shared memory option group | `_SC_XOPEN_SHM` |
| `_XOPEN_VERSION` | the XSI version | `_SC_XOPEN_VERSION` |

Figure 2.19  Options and name arguments to sysconf

Figure 2.20 shows several configuration options and their corresponding values on the four sample systems we discuss in this text. An entry is “unsupported” if the system defines the symbolic constant but it has a value of −1, or if it has a value of 0 but the corresponding sysconf or pathconf call returned −1. It is interesting to see that some system implementations haven’t yet caught up to the latest version of the Single UNIX Specification.

| Limit | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 — UFS file system | Solaris 10 — PCFS file system |
|---|---:|---:|---:|---:|---:|
| `_POSIX_CHOWN_RESTRICTED` | 1 | 1 | 200112 | 1 | 1 |
| `_POSIX_JOB_CONTROL` | 1 | 1 | 200112 | 1 | 1 |
| `_POSIX_NO_TRUNC` | 1 | 1 | 200112 | 1 | unsupported |
| `_POSIX_SAVED_IDS` | unsupported | 1 | 200112 | 1 | 1 |
| `_POSIX_THREADS` | 200112 | 200809 | 200112 | 200112 | 200112 |
| `_POSIX_VDISABLE` | 255 | 0 | 255 | 0 | 0 |
| `_POSIX_VERSION` | 200112 | 200809 | 200112 | 200112 | 200112 |
| `_XOPEN_UNIX` | unsupported | 1 | 1 | 1 | 1 |
| `_XOPEN_VERSION` | unsupported | 700 | 600 | 600 | 600 |

**Figure 2.20**  Examples of configuration options

Note that pathconf returns a value of −1 for _PC_NO_TRUNC when used with a file from a PCFS file system on Solaris. The PCFS file system supports the DOS format (for floppy disks), and DOS filenames are silently truncated to the 8.3 format limit that the DOS file system requires.

## 2.7 Feature Test Macros

The headers define numerous POSIX.1 and XSI symbols, as we’ve described. Even so, most implementations can add their own definitions to these headers, in addition to the POSIX.1 and XSI definitions. If we want to compile a program so that it depends only on the POSIX definitions and doesn’t conflict with any implementation-defined constants, we need to define the constant _POSIX_C_SOURCE. All the POSIX.1 headers use this constant to exclude any implementation-defined definitions when _POSIX_C_SOURCE is defined.

> Older versions of the POSIX.1 standard defined the _POSIX_SOURCE constant. This was superseded by the _POSIX_C_SOURCE constant in the 2001 version of POSIX.1.

The constants _POSIX_C_SOURCE and _XOPEN_SOURCE are called *feature test macros*. All feature test macros begin with an underscore. When used, they are typically defined in the cc command, as in

```
cc -D_POSIX_C_SOURCE=200809L file.c
```
