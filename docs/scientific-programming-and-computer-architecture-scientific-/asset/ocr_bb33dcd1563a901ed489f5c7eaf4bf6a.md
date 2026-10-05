8 Chapter 1. C/C++ Review

![](bbox=[0.263, 0.143, 0.736, 0.417])

Figure 1.2: The three program sources are aitken.c, leibniz.c, and logseries.c. They are combined to produce two different executables, extrapolating the partial sums of the Leibniz series and the Taylor series of log(1+x), respectively. The .o object files are omitted from this figure.

being compiled. The crucial information that is missing is the address and definition of the function in aitken.c that is invoked in leibniz.c. That information is supplied only when the object files aitken.o and leibniz.o are combined into an executable, which we will call leibniz.exe, by the linker. The linker's job is to eliminate unresolved references in the object files and put together an executable without any unresolved references. The executable is the program that ultimately runs on the computer.

We will make the discussion of compilation and linking more concrete in later sections. The overall picture is as follows: the program is separated into multiple source files, the source files are compiled separately into object files holding machine instructions, and the linker merges the object files and eliminates unresolved references to produce an executable. The overall picture for the Aitken program is shown in figure 1.2.

Exercise 1.1.1. Substitute $s_n = S + a\lambda^n$ into the Aitken formula (1.1) and verify that

> We assume the GNU/Linux operating system, the executable files will use the .exe extension as in Windows for greater clarity.