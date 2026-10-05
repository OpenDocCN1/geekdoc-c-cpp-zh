Execution refers to using system resources like CPU, memory, I/O devices in order to complete a particular task. For the execution of hello.c program, it needs to use all these resources like CPU for processing, I/O device- monitor for displaying the result "hello India" and so on.

The issue is that the source program we have written, hello.c is not understandable to the machine. It needs some effort. The given program is written in human-readable form (high level) and the machine could not understand this. So, hello.c needs translation from high-level form to low-level form (machine understandable). This translation can be done using a compiler or interpreter.

The process of compilation depends on the compiler we are using, some of the compilers are Turbo C, Dev-C, GCC, etc. Their translation process is entirely different. The compiled file is referred to as executable object files. On a Unix system, the execution of a C program can be done using GCC compiler as follows:

```
unix> gcc -o hello.c
```

The source file hello.c is read by GCC compiler driver which translates it into an executable object file.

```
unix> ./hello
```

The loader loads this executable file into the main memory, and the CPU will start processing.

The translation using GCC is not a single phase thing. The GCC passes the source program to its four components: (i) preprocessor, (ii) compiler, (iii) assembler, and (iv) linker. They are altogether referred to as a compilation system. Figure 1.2 will give a better idea of the compilation system as follows: