
the denominator before performing the division. Listing 7.17 displays the contents of DivByZero.c that illustrates how to prevent division by zero, along with a suitable text message.

### LISTING 7.17: DivByZero.c

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int dividend = 20;
    int divisor = 5;
    int quotient;

    if( divisor == 0){
        fprintf(stderr, "Division by zero: exiting program\n");
        exit(EXIT_FAILURE);
    }

    quotient = dividend / divisor;
    fprintf(stderr, "Value of quotient : %d\n", quotient );

    exit(EXIT_SUCCESS);
}
```

Listing 7.17 contains a `main()` function that initializes three integer-valued variables, followed by conditional logic that checks the value of the variable divisor.

Notice that the program exits with a value of EXIT_SUCCESS in case of success, where EXIT_SUCCESS is a macro, and exits with a status EXIT_FAILURE in case of an error.

One other detail: The C standard does not require any particular value for EXIT_SUCCESS and EXIT_FAILURE. The only requirement is that they must be defined and their value must be representable in an int.

Launch the compiled code in Listing 7.17 and you will see the following result:

```text
Value of quotient : 4
```

The next section briefly discusses system calls in C, which is definitely an advanced topic. However, there are two code samples that are within your grasp, and they provide a gentle introduction to this topic.

## SYSTEM CALLS IN C (OPTIONAL)

This topic is the final topic of this book, and arguably the most complex. This section provided an extremely brief description of system calls so that you will be aware of their existence and their purpose. This section also contains a very simple example of a C program that makes a system call.

### Removing a File

Listing 7.18 displays the contents of `SystemDeleteFile.c` that illustrates how to invoke the `unlink()` command to delete a file.

### LISTING 7.18: SystemDeleteFile.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>

int main()
{
    char *filename = "text.txt";

    if (unlink("text.txt") == -1)
    {
        printf("File %s does not exist\n", filename);
    }
    else
    {
        printf("Successfully removed file %s\n", filename);
    }

    return 0;
}
```

**Listing 7.18** contains a `main()` function that initializes the variable `filename` with the value `text.txt`. The next portion of code is conditional logic that invokes the built-in C function `unlink()` in order to delete the file `text.txt`. If the command fails, a suitable message is displayed. If the result is successful, a different message is displayed.

Now create a file called `text.txt` in the directory that contains file `SystemDeleteFile.c`. Compile this code and invoke the binary executable and you will see the following output:

```text
Successfully removed file text.txt
```

Invoke this command again and this time you will see a different message:

```text
File text.txt does not exist
```

### Listing the Files in a Directory

**Listing 7.19** displays the contents of `SystemForkExec.c` that illustrates how to use the `fork()` and `exec()` system calls to create a new process that lists the contents of a directory. Keep in mind that the `fork()` and `exec()` system calls are not part of the C language, and they are only available on systems that support the POSIX standard.

### LISTING 7.19: SystemForkExec.c

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    char *ls_args[] = { "/bin/ls", "-l", NULL };

    int pid = fork();

    if(pid == 0) // the child
    {
        execv(ls_args[0], ls_args);
    }
    else if(pid > 0) // the parent
    {
        // wait for the child to complete
        wait(NULL);
    }
    else
    {
        printf("Error: negative process ID\n");
    }

    exit(0);
}
```

Listing 7.19 starts with several #include statements that are required in order to execute the fork() and exec() system calls. The next section contains the main() function that initializes a character pointer to an array with three elements: the full path to the Unix ls command, the option to be used with the ls command, and the value NULL.

Next, the fork() function is invoked and the result is used to initialize the value of the integer pid. The key point to remember: if pid is zero, then we are in the child process; if pid is positive, then we are in the parent process; any other value for pid is an error (i.e., the fork() command failed).

The preceding scenarios are captured via conditional logic, where appropriate messages are displayed. The output from launching the code in Listing 7.19 is here:

```text
-rwxr-xr-x 1 owner staff 8560 Jul 24 19:22 SystemForkExec
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 a
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 b
-rw-r--r-- 1 owner staff    0 Jul 24 19:22 c
```

The binary executable SystemForkExec was invoked in a directory that contains the binary executable and the three files a, b, and c (all of size 0).

## DEFINING CUSTOM FUNCTIONS IN MULTIPLE FILES (OPTIONAL)

This section shows you how to define custom functions in two C files and then include them in the compilation to create a single executable.

Listing 7.20, Listing 7.21, and Listing 7.22 display the contents of the files FindChar2.h, FindChar2.c, and FindMain2.c, which are compiled into one binary executable called FindMain2.

### LISTING 7.20: FindChar2.h

```c
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c);
```

Listing 7.20 is a very short header file: it contains two header files and the function prototype for the function findChar().

### LISTING 7.21: FindChar2.c

```c
#include <ctype.h>
#include <stdio.h>

void findChar(char str[], char c)
{
    int matchCount = 0;

    printf("String: %s\n", str);
    printf("Char:   %c\n", c);

    for(int i=0; str[i]; i++)
    {
        if(str[i] == c)
        {
            printf("Match in position: %d\n", i);
            ++matchCount;
        }
    }

    printf("Count:  %d\n\n", matchCount);
}
```

Listing 7.21 contains the implementation details of the function `findChar()` that you saw in a code sample in Chapter 3.

### LISTING 7.22: FindMain2.c

```c
#include "FindChar2.h"

int main()
{
    char str1[] = "pasta";
    findChar(str1, 'a');

    char str2[] = "New York City";
    findChar(str2, 'k');

    char str3[] = "California";
    findChar(str3, 'z');

    return (0);
}
```

**Listing 7.22** contains a local header file called `FindChar2.h` (i.e., it's not part of the C language), followed by a `main()` function. Notice that the `main()` function defines three strings and invokes the `findChar()` function (defined in `FindChar2.c`) three times.

The C programs `FindChar2.c` and `FindMain2.c` need to be specified in the compilation step involving `gcc`, as shown here:

```bash
# do not change the order of the next two lines:
gcc -std=c11 -Wall -c FindChar2.c
gcc -std=c11 FindChar2.o FindMain2.c -o FindMain2
```

The output of the preceding code snippet is the binary executable `FindMain2`, and the output from launching `FindMain2` is here:

```text
String: pasta
Char: a
Match in position: 1
Match in position: 4
Count: 2

String: New York City
Char: k
Match in position: 7
Count: 1

String: California
Char: z
Count: 0
```

The preceding example is manageable because there are only three files involved, which you can specify from the command line when you invoke `gcc`. However, a C program can have multiple dependencies involving dozens of files, and keeping track of them (along with dependencies on header files and custom libraries) can quickly become untenable. One solution involves the make utility, which is discussed in the Appendix.

## STANDARD HEADER FILES AND LIBRARIES

As you have seen throughout the code samples in this book, C programs invariably require standard header files in order to compile them into object files, along with standard libraries in order to perform the link step that creates an executable file.

Note that /usr/include is used on Unix and Unix-like systems only, whereas Windows compilers have their “include” files somewhere in the installation directory.

### Standard Header Files (Unix-like Systems)

On Unix-like systems, the directory /usr/include contains various “header” files, some of which are displayed below (from a Macbook Pro):

- AppleTextureEncoder.h
- AssertMacros.h
- Availability.h
- AvailabilityInternal.h
- AvailabilityMacros.h
- Block.h
- CommonCrypto
- ConditionalMacros.h
- MacTypes.h
- [files omitted for brevity]
- wordexp.h
