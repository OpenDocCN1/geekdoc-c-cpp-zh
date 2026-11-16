+   g++ -Wall -std=c++14 -o simple simple.cpp

The -std=c++14 option directs the compiler to process the C++ source code according to the rules of the C++14 standard which the International Standards Organization (ISO) adopted in 2014. Since this standard is relatively new, if you omit this part of the command, g++ assumes the programmer is writing the source code under the rules of the older, 1998 ISO C++ standard, usually referred to as C++98.

The code in this book is based on the C++11 standard.

+   g++ -Wall -std=c++14 -o simple simple.cpp

The -o simple part of the command specifies the name of the executable program. The desired name appears after the -o part, so our executable program will be named simple.exe on Microsoft Windows systems. On Mac and Linux platforms the name of the executable file produced will be just simple (no exe extension). If the C++ source code contains no errors, the compiler will produce the executable file named simple.exe (or simple). On a Windows Machine we can run the compiled program from the command line by typing the command

```
simple
```

(We also can use the full name, simple.exe.) On a Unix-like system (macOS or Linux), we instead would type

```
./simple
```

to execute the program.

+   g++ -Wall -std=c++14 -o simple simple.cpp

simple.cpp specifies the name of the C++ source file we wish to compile. Here the file simple.cpp must reside in our current working directory for the compiler to process it.

The general form of the command to compile a C++ source file, therefore, is

```
g++ -Wall -std=c++14 -o executable source
```

where source is the name of the file containing the C++ source code, and executable is the name of the executable program the build process generates.

When you are finished with the executable file simple.exe, you can delete it with the following command:

```
del simple.exe
```

We can reconstruct the executable file whenever we like by simply recompiling the source file. Be careful not to delete accidentally the source file, or you have no choice but to type it in again.