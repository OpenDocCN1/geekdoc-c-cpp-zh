| Name of option | Description | `name` argument |
|---|---|---|
| `_POSIX_V7_ILP32_OFF32` | int, long, pointer, and `off_t` types are 32 bits. | `_SC_V7_ILP32_OFF32` |
| `_POSIX_V7_ILP32_OFFBIG` | int, long, and pointer types are 32 bits; `off_t` types are at least 64 bits. | `_SC_V7_ILP32_OFFBIG` |
| `_POSIX_V7_LP64_OFF64` | int types are 32 bits; long, pointer, and `off_t` types are 64 bits. | `_SC_V7_LP64_OFF64` |
| `_POSIX_V7_LP64_OFFBIG` | int types are at least 32 bits; long, pointer, and `off_t` types are at least 64 bits. | `_SC_V7_LP64_OFFBIG` |

The c99 compiler requires that we use the getconf(1) command to map the desired data size model to the flags necessary to compile and link our programs. Different flags and libraries might be needed, depending on the environments supported by each platform.

Unfortunately, this is one area in which implementations haven’t caught up to the standards. If your system does not match the latest version of the standard, the system might support the option names from the previous version of the Single UNIX Specification: _POSIX_V6_ILP32_OFF32, _POSIX_V6_ILP32_OFFBIG, _POSIX_V6_LP64_OFF64, and _POSIX_V6_LP64_OFFBIG.

To get around this, applications can set the _FILE_OFFSET_BITS constant to 64 to enable 64-bit offsets. Doing so changes the definition of off_t to be a 64-bit signed integer. Setting _FILE_OFFSET_BITS to 32 enables 32-bit file offsets. Be aware, however, that although all four platforms discussed in this text support both 32-bit and 64-bit file offsets, setting _FILE_OFFSET_BITS is not guaranteed to be portable and might not have the desired effect.

Figure 3.4 summarizes the size in bytes of the off_t data type for the platforms covered in this book when an application doesn’t define _FILE_OFFSET_BITS, as well as the size when an application defines _FILE_OFFSET_BITS to have a value of either 32 or 64.

| Operating system | CPU architecture | `_FILE_OFFSET_BITS` value |  |
|---|---|---:|---:|---:|
|  |  | Undefined | 32 | 64 |
| FreeBSD 8.0 | x86 32-bit | 8 | 8 | 8 |
| Linux 32.0 | x86 64-bit | 8 | 8 | 8 |
| Mac OS X 10.6.8 | x86 64-bit | 8 | 8 | 8 |
| Solaris 10 | SPARC 64-bit | 8 | 4 | 8 |

Note that even though you might enable 64-bit file offsets, your ability to create a file larger than 2 GB (2^31 − 1 bytes) depends on the underlying file system type.