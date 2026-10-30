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

# 2.7  Feature Test Macros

The headers define numerous POSIX.1 and XSI symbols, as we’ve described. Even so, most implementations can add their own definitions to these headers, in addition to the POSIX.1 and XSI definitions. If we want to compile a program so that it depends only on the POSIX definitions and doesn’t conflict with any implementation-defined constants, we need to define the constant _POSIX_C_SOURCE. All the POSIX.1 headers use this constant to exclude any implementation-defined definitions when _POSIX_C_SOURCE is defined.

> Older versions of the POSIX.1 standard defined the _POSIX_SOURCE constant. This was superseded by the _POSIX_C_SOURCE constant in the 2001 version of POSIX.1.

The constants _POSIX_C_SOURCE and _XOPEN_SOURCE are called *feature test macros*. All feature test macros begin with an underscore. When used, they are typically defined in the cc command, as in

```
cc -D_POSIX_C_SOURCE=200809L file.c
```