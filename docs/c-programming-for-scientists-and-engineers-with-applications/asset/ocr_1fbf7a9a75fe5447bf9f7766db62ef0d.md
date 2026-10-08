# 1.4.2 Program Compilation

The first step in testing and debugging a program on the computer is compilation. During this process, the computer checks whether the program has syntax, punctuation, or spelling errors, that is, that it follows grammatical rules for C. If it appears to be all right, it is translated into machine code.

Note that the compilation process does not detect incorrect spelling of the names of library modules or other separately compiled modules. It also does not detect errors in the description of input and output data. And it does not detect errors in logic that lead to wrong answers, nonterminating repetitions, or impossible divisions by zero. Any mistakes in defining the lower-level modules of a complicated problem will not show up until later.

When the compiler detects an error, it identifies the location of the error and indicates what is wrong. It is up to the programmer to go back and fix the source code before compiling again. Or if any program logic is changed, it may be necessary to desk the source code once more, using the sample data.

When the program compiles correctly, it produces object code and a list of the other modules needed. These are either stored for later use, or submitted to the linker in the program execution phase of the process. A program that compiles correctly does not need to be compiled again.

# 1.4.3 Program Execution

After the main program and any submodules have been written and compiled correctly, the resulting object modules are linked along with any mathematical or other library routines, and a single executable module is built. The process of building an executable module, or linking, is shown in Figure 1.15. The linkers and loaders of the operating system are responsible for building the executable and executing it. If these systems detect errors, corrections must be made to the appropriate source code module, any changed modules are recompiled, and the linking is repeated.

When the program is finally executed, the computer carries out the programmer's instructions in logical sequence, accepts the designated input, performs the required calculations, and produces output. The output includes messages indicating whether the execution contained errors and statistics about the computer resources used. When there are execution errors, the source code must be corrected and the program recompiled, re-linked, and re-executed. The programming