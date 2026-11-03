The name a.out is the default C program filename. You can reset this name by specifying the -o ("little o") switch followed by the desired output filename when building. For example:

```
clang -Wall ex0201.c -o ex0201
```

The preceding command uses the source code in ex0201.c to build a program named ex0201. It must be run at the command prompt in the same manner as a.out:

```
./ex0201
```

The program runs, outputting text, which appears on the next line after you type the program name:

```
Greetings, human.
```

In Code::Blocks, output appears in a terminal window. Press the Enter key to close the window. For Code::Blocks in Linux, type the exit command to close the output terminal window.

A program like ex0201 doesn’t require much testing to ensure that it works. As your programming skills mature, testing, rewriting, compiling, and debugging become a standard part of the process. Don’t be discouraged; this is how all programmers learn the craft.

> The mechanics of running a program are carried out by the device's operating system: The operating system loads the program into memory, where the processor or CPU executes the code. This is a loose description of how a program works.

![](bbox=[0.02, 0.88, 0.25, 0.94])

> In Windows, the program name ends with the exe (for executable) extension, as in ex0201.exe. In Mac OS X, Linux, and Unix, the program name has no extension: ex0201. Further, in those operating systems, the file's permissions are set for the file to run as an executable.