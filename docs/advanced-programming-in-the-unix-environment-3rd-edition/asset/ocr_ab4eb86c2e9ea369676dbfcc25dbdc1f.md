If we execute the program in Figure 5.12, we get

```
```text
$ ./a.out
/tmp/fileT0Hsu6
/tmp/filekmAsYQ
one line of output
```
```

The standard technique often used by the `tmpfile` function is to create a unique pathname by calling `tmpnam`, then create the file, and immediately unlink it. Recall from Section 4.15 that unlinking a file does not delete its contents until the file is closed. This way, when the file is closed, either explicitly or on program termination, the contents of the file are deleted.

The Single UNIX Specification defines two additional functions as part of the XSI option for dealing with temporary files: `mkdtemp` and `mkstemp`.

Older versions of the Single UNIX Specification defined the `tempnam` function as a way to create a temporary file in a caller-specified location. It is marked obsolescent in SUSv4.

```
```c
#include <stdlib.h>

char *mkdtemp(char *template);

                            Returns: pointer to directory name if OK, NULL on error

int mkstemp(char *template);

                            Returns: file descriptor if OK, −1 on error
```
```

The `mkdtemp` function creates a directory with a unique name, and the `mkstemp` function creates a regular file with a unique name. The name is selected using the *template* string. This string is a pathname whose last six characters are set to `XXXXXX`. The function replaces these placeholders with different characters to create a unique pathname. If successful, these functions modify the *template* string to reflect the name of the temporary file.

The directory created by `mkdtemp` is created with the following access permission bits set: `S_IRUSR | S_IWUSR | S_IXUSR`. Note that the file mode creation mask of the calling process can reset these permission bits further. If directory creation is successful, `mkdtemp` returns the name of the new directory.

The `mkstemp` function creates a regular file with a unique name and opens it. The file descriptor returned by `mkstemp` is open for reading and writing. The file created by `mkstemp` is created with access permissions `S_IRUSR | S_IWUSR`.

Unlike `tmpfile`, the temporary file created by `mkstemp` is not removed automatically for us. If we want to remove it from the file system namespace, we need to unlink it ourselves.

Use of `tmpnam` and `tempnam` does have at least one drawback: a window exists between the time that unique pathname is returned and the time that an application creates a file with that name. During this timing window, another process can create a file of the same name. The `tmpfile` and `mkstemp` functions should be used instead, as they don’t suffer from this problem.