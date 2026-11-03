main() is called. For example-

```
#pragma startup func1
```

The function func1() will be called before the main() function.

# #pragma exit

It allows the programmer to specify the function that should be called upon program exit i.e. before the program terminates.

```
#pragma exit func2
```

The function func2() will be called just before the program terminates.

# #pragma inline

It tells the compiler that inline assembly code is contained in the program.

# #pragma warn

We can turn warning messages on or off using this pragma.

# 12.7 How to see the code expanded by the Preprocessor

Throughout the chapter we have discussed all the concepts by explaining how the preprocessor expands your code. Now we'll tell you how to view the code after the preprocessing phase. The procedure may vary on different systems, we'll discuss it for Turbo C and UNIX.

With Turbo C, we have a utility(executable file) named cpp( C preprocessor). This utility creates a file that contains the expanded source code. The name of this file is same as that of source code file and it has a ".i" extension. For example suppose the source code is present in file d:\myfile.c, then the expanded code would be present in myfile.i. We can create the expanded file at the command prompt as-

```
C:\TC>cpp d:\myfile.c
```

If the source code contains #include directive, then we'll have to specify the path of include file: For example if c:\tc\include is path of included files then we have to write as-

```
C:\TC>cpp -Ic:\tc\include d:\myfile.c
```

The file myfile.i will be created in the directory where cpp is present. We can view this file using a text editor or by type command. To know more about the syntax of usage of cpp just type cpp at the command prompt.

In UNIX, we can view the expanded code by using the option -E. With this option the output of the preprocessor is displayed on the terminal. If we use option -P, then the output of the preprocessor is stored in a file with the same name as source file but with a ".i" extension. We can use -I to inform the preprocessor about the path of included files.

# Exercise

Assume stdio.h is included in all programs.

```
(1) #define MAX 5;
main()
{
    printf("%d",MAX);
}
```