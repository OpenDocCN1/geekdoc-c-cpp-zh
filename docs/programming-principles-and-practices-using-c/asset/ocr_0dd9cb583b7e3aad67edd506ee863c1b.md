+   * Memory
* Date and time
* Etc.

There are more C standard library functions than we present here; see a good C textbook, such as Kernighan and Ritchie, *The C Programming Language* (K&R), if you need to know more.

# **B.11.1 Files**

The `<stdio>` I/O system is based on “files.” A file (a `FILE*`) can refer to a file or to one of the standard input and output streams, `stdin`, `stdout`, and `stderr`. The standard streams are available by default; other files need to be opened:

| File open and close |
|---|---|
| `f=fopen(s,m)` | Open a file stream for a file named **s** with the mode **m**. |
| `x=fclose(f)` | Close file stream **f**; return **0** if successful. |

A “mode” is a string containing one or more directives specifying how a file is to be opened:

| File modes |
|---|---|
| `"r"` | reading |
| `"w"` | writing (discard previous contents) |
| `"a"` | append (add at end) |
| `"r+t"` | reading and writing |
| `"w+t"` | reading and writing (discard previous contents) |
| `"b"` | binary; use together with one or more other modes |

There may be (and usually are) more options on a specific system. Some options can be combined; for example, `fopen("foo", "rb")` tries to open a file called **foo** for binary reading. The I/O modes should be the same for stdio and `iostreams` (S B.7.1).

# **B.11.2 The `printf()` family**

The most popular C standard library functions are the I/O functions. However, we recommend `iostreams` because that library is type-safe and extensible. The