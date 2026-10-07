# The Mechanics of Creating a Program

# Compilation and Linking

Originally, Stroustrup implemented C++ with a C++-to-C compiler program instead of developing a direct C++-to-object code compiler.This program, called efront (for front end), translated C++ source code to C source code, which could be compiled by a standard C compiler. This approach significantly introducing C++ to the community. Other implementations have used this approach to bring C++ to other platforms. As C++ has developed and grown in popularity; more implementers have turned to creating C++ compilers that generate object code directly from C source code. This direct approach speeds up the compilation process and emphasizes that C++ is a separate, if similar, language.

The mechanics of compiling depending on the implementation, and the following sections outline the basic steps, but they are no substitute for consulting the documentation for your system.

# Unix Compilation and Linking

Originally, Unix cc command invoked efront. However, efront didn't keep pace with the evolution of C++, and its last release was in 1993.These days a Unix computer might have none, a proprietary compiler, or a third-party compiler, perhaps commercial, freeware, as the GNU cc compiler. In many of these other cases (but not in the no-compiler case), the cc command still works, with the actual compiler being invoked differing from system to system. For simplicity, we'll assume that cc is available, realize that you might need to substitute a different command for cc in the following discussion.

You use the cc to compile your program.The name is in uppercase letters to distinguish from the standard Unix C compiler cc.The cc compiler is a command-line compiler, meaning you type compilation commands on the Unix command line.

For example, to compile the C++ source file spiffy.c,you would type this at the Unix prompt:

```
cc spiffy.c
```

If through skill, dedication, or luck, your program has no errors, the compiler generates an object file with an o extension. In this case, the compiler produces a file spiffy.o.

Next, the compiler automatically passes the object file to the system linker, a program that combines your code with library code to produce the executable. By default, the executable is called a .out. If you used just one source file, the linker deletes the spiffy.o file because it's no longer needed. To run the program, you just type the name of the executable:

```
a.out
```

Note that if you compile a new program, the new a.out executable file replaces the previous a.out.(That because executable files take a lot of space, overwriting executable files helps reduce storage demands.) But if you develop an executable program