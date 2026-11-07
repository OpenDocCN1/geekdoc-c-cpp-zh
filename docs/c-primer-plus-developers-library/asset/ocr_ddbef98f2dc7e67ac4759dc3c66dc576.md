you want to keep, you just use the Unix mv command to change the name of the executable file.

In C++, as in C, you can spread a program over more than one file. (Many of the programs in this book in Chapters 8 through 16 do this.) In such a case, you can compile a program by listing all the files on the command line, like this:

```
cc my.c precious.c
```

If there are multiple source code files, the compiler does not delete the object code files. That way, if you just change the my.c file, you can recompile the program with this command:

```
cc my.c precious.o
```

This recompiles the my.c file and links it with the previously compiled precious.o file. You might have to identify some libraries explicitly. For example, to access functions defined in the math library, you may have to add the -lm flag to the command line:

```
cc usingmath.c -lm
```

# Linux Compiling and Linking

Linux systems most commonly use g++, the GNU C++ compiler from the Free Software Foundation. The compiler is included in most Linux distributions, but it may not always be installed. The g++ compiler works much like the standard Unix compiler. For example, the following produces an executable file call a.out:

```
g++ spiffy.cxx
```

Some versions might require that you link in the C++ library:

```
g++ spiffy.cxx -lg++
```

To compile multiple source files, you just list them all in the command line:

```
g++ my.cxx precious.cxx
```

This produces an executable file called a.out and two object code files, my.o and precious.o. If you subsequently modify just one of the source code files, say my.cxx, you can recompile by using my.cxx and the precious.o:

```
g++ my.cxx precious.o
```

The GNU compiler is available for many platforms, including the command-line mode for Windows-based PCs as well as for Unix systems on a variety of platforms.

# Command-Line Compilers for Windows Command Prompt Mode

An inexpensive route for compiling C++ programs on a Windows PC is to download a free command-line compiler that runs in Windows Command Prompt mode, which opens an MS-DOS-like window. Free Windows downloads that include the GNU C++ compiler are Cygwin and MinGW; they use g++ as the compiler name.