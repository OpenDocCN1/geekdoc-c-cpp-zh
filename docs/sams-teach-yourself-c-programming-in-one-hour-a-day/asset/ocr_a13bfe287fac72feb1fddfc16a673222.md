# LESSON 1 Getting Started with C

development, is performed by a program called a compiler. The compiler takes your source code file as input and produces a disk file containing the machine language instructions that correspond to your source code statements. The machine language instructions created by the compiler are object code, and the disk file containing them is an object file.

> NOTEnThis book covers ANSI Standard C. This means that it doesn't matter which C compiler you use, as long as it follows the ANSI Standard. Not all compilers support the standards. The specific name of the current standard for C is ISO/IEC 9899:2011. Rather than using this complex name, this book refers to C11.

With your graphical IDE, compiling is simple. In most graphical environments, you can compile a program listing by selecting the compile icon or selecting something from a menu. After the code is compiled, selecting the run icon or selecting something from a menu executes the program. You should check your compiler's manuals for specifics on compiling and running a program. The Code::Blocks program that you can download for free is an example of a development environment that has versions for most operating systems. There are other graphical development environments, both free and for sale, for almost every platform. Pick your favorite.

After you compile, you have an object file. If you look at a list of the files in the directory or folder where you compiled, you should find a file that the .obj (rather than a .c) has the same name as your source file. The obj extension is recognized as an object file and is used by the linker. On a Linux or UNIX system, the compiler creates object files with an extension of .o instead of .obj.

# Linking to Create an Executable File

One more step is required before you can run your program. Part of the ANSI C language definition is a function library that contains object code (code that has already been compiled). A predefined function contains code that has already been written and supplied in a ready-to-use form with your compiler package.

The printf() function used in the previous example is a library function. These library functions perform frequently needed tasks, such as displaying information and reading data from disk files. If your program uses any of these functions (and hardly a program exists that doesn't use at least one), the object file produced when your source