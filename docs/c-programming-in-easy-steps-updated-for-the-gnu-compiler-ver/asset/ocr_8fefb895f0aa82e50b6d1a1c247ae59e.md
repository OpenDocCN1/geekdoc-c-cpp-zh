# Compiling a C program

The C source code files for the examples in this book are stored in a directory created expressly for that purpose. The directory is named “MyPrograms” and its absolute address on Windows is C:\MyPrograms, whereas on Linux it’s at /home/user/MyPrograms. The hello.c source code file, created by following the steps on pages 12-13, is saved in this directory awaiting compilation to produce a version in executable byte code format.

![](bbox=[0.08, 0.2, 0.2, 0.32])

At a command prompt, type gcc --help then hit Return to see a list of all compiler options.

1. At a command prompt, issue a cd command with the path to the MyPrograms directory to navigate there

2. At a command prompt in the MyPrograms directory, type gcc hello.c then hit Return to compile the program

When the compilation succeeds, the compiler creates an executable file alongside the original source code file. By default, this file will be named a.out on Linux systems and a.exe on Windows systems. Compiling a different C source code file in the MyPrograms directory would now overwrite the first executable file without warning. This is obviously unsatisfactory so a custom name for the executable file must be specified when compiling hello.c. This can be achieved by including a -o option followed by a custom name in the compiler command.

3. At a command prompt in the MyPrograms directory, type gcc hello.c -o hello.exe then hit Return to compile the program once more

On both Linux and Windows systems an executable file named hello.exe is now created alongside the C source code file:

![](bbox=[0.42, 0.88, 0.97, 0.99])