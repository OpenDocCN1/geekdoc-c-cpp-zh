![](bbox=[0.143, 0.1, 0.76, 0.302])

Figure 11.1 Apart from your code, a program consists of several libraries.

Each library usually consists of individual modules. For example, the C++ standard library, from your perspective as a user, consists of several headers. Sometimes you include `#include <vector>`, sometimes `#include <iostream>`. These headers reflect that the library was probably not developed as a single huge *.cpp file. The header modules were combined into a single library for your convenience, so you only need to specify this one *.lib file to the compiler. The compiler then picks out the things that are actually used by itself.

# 11.2 Modules

Your task now is to sensibly divide the modules of your part of the program for your own project. For this, you need to answer the question, for example, “What belongs in main.obj, teil1.obj, and teil2.obj?” And along with that: “What belongs in the main.cpp, teil1.cpp, and teil2.cpp source code files?”

`main.cpp` should probably contain `int main()`. Instead of naming the file `main.cpp`, `program.cpp` is also a reasonable name if your program will later be called `programm.exe`. Otherwise, you should break your project into parts based on functionalities. Each part goes into a separate set of *.cpp files. Each *.cpp file, in turn, is complemented by a similarly named *.hpp file. The exception is `main.cpp`, for which you normally do not need to create a header file.

> > **Interface: Each .cpp File Also Gets a .hpp File**
> >
> > Write a similarly named *.hpp header file for each *.cpp. Declare in it all the functions and other things that are directly used by other .cpp files: these form the *interface*. Intentionally keep certain elements only in the *.cpp file—specifically, those needed solely to implement the interface.