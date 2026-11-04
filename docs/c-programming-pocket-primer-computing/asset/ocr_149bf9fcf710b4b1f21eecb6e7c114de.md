Launch the compiled code in [Listing 7.16](#) and you will see the following result:

Value of quotient : 4

The next section briefly discusses system calls in C, which is definitely an advanced topic. However, there are two code samples that are within your grasp, and they provide a gentle introduction to this topic.

# SYSTEM CALLS IN C (OPTIONAL)

This topic is the final topic of this book, and arguably the most complex. This section provided an extremely brief description of system calls so that you will be aware of their existence and their purpose. This section also contains a very simple example of a C program that makes a system call.

# Removing a File

[Listing 7.18](#) displays the contents of `SystemDeleteFile.c` that illustrates how to invoke the `unlink()` command to delete a file.

# **LISTING 7.18: SystemDeleteFile.c**

```
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
```
```