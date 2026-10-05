
## 1.4 Summary

This book does not attempt to cover all the facets of the C++ programming language. Experienced programmers should look elsewhere for books that cover C++ in much more detail. The focus here is on introducing programming techniques and developing good habits. To that end, our approach avoids some of the more esoteric features of C++ and concentrates on the basics that transfer directly to other imperative programming languages such as Java, C#, and Python. We stick with the basics and explore more advanced features of C++ only when necessary to handle the problem at hand.

- Computers require both hardware and software to operate. Software consists of instructions that control the hardware.
- At the lowest level, the instructions for a computer program can be represented as a sequence of zeros and ones. The pattern of zeros and ones determines the instructions performed by the processor.
- Two different kinds of processors can have different machine languages.
- Application software can be developed largely without worrying about the underlying hardware. A tool called a compiler translates the higher-level, abstract language into the machine language required by the computer.
- Programmers develop software using tools such as editors, compilers, debuggers, and profilers.
- C++ is a higher-level programming language.
- An IDE is an integrated development environment—one program that provides all the tools developers need to write software.

## 1.5 Exercises

- 1. What is a compiler?
- 2. How is code compiled from source code?
- 3. What tool does a programmer use to produce C++ source code?
- 4. What tool(s) does a programmer use to convert C++ source code into executable machine code?
- 5. What does the linker do?
- 6. Does the linker deal with files containing source code or machine language code?
- 7. What does the preprocessor do to source code?
- 8. List several advantages developing software in a higher-level language has over developing software in machine language.
- 9. How can an IDE improve a programmer's productivity?
- 10. Name a popular C++ IDE used by programmers developing for Microsoft Windows.
- 11. Name a proper C++ IDE used by programmers developing for Apple Mac OS X.

## Chapter 2 
### Writing a C++ Program

Properly written C++ programs have a particular structure. The syntax must be correct, or the compiler will generate error messages and not produce executable machine language. This chapter introduces C++ by providing some example programs and associated fundamental concepts. Most of the concepts presented in this chapter are valid in other programming languages as well. While other languages may implement the concepts using slightly different syntax, the ideas are directly transferable to other languages like C, Java, C#, and Ada.

### 2.1 General Structure of a Simple C++ Program

Listing 2.1 (simple.cpp) is one of the simplest C++ programs that does something:

Listing 2.1: simple.cpp
```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "This is a simple C++ program!" << endl;
}
```

You can type the text in Listing 2.1 (simple.cpp) into an editor and save to a file named simple.cpp. The actual name of the file is irrelevant, but the name "simple" accurately describes the nature of this program. The extension .cpp is a common extension used for C++ source code.

After creating this file with a text editor and compiling it, you can run the program. The program prints the message

```
This is a simple C++ program!
```

Listing 2.1 (simple.cpp) contains five non-blank lines of code:

- #include <iostream>

This line is a preprocessor directive. All preprocessor directives within C++ source code begin with a # symbol. This one directs the preprocessor to add some predefined code to our source code before the compiler begins to process it. This process is automatic and invisible to us.

Here we want to use parts of the iostream library, a collection of precompiled C++ code that C++ programs (like ours) use. The iostream library contains routines that handle input and output (I/O) that include functions such as printing to the display, getting user input from the keyboard, and dealing with files.

Two items used in Listing 2.1 (simple.cpp), cout and endl, are not part of the C++ language itself. These items, along with many others related to input and output, were developed in C++, compiled, and stored in the iostream library. The compiler needs to be aware of these items. The #include directive specifies a file, called a header, that contains the specifications for the library code. The compiler checks how we use cout and endl within our code against the specifications in the <iostream> header to ensure that we are using the library correctly.

Most of the programs we use with this #include <iostream> directive, and some programs we will use in the future use #include other headers.

- namespace std;

The two items we need to display a message on the screen, cout and endl, have names: std::cout and std::endl. This using namespace std allows us to omit the std:: prefix and use their shorter names. This directive is optional, but if we omit it, we must use the longer names. Listing 2.2 (simple.cpp) shows how the longer names are used. The name std stands for “standard”, and using the namespace std line indicates that some of the names we use in our program are part of the so-called “namespace.”

- int main() {

This specifies the beginning of our program. Here we are declaring a function named main. C++ programs must contain this function to be executable. Details about the meaning of int and the parentheses appear in later chapters. More general information about functions appear in Chapter 8 and Chapter 9.

The opening curly brace at the end of the line marks the beginning of the body of the function. The body of the function contains the statement to execute.

- cout << "This is a C++ program!" << endl;

The body of our main function contains only one statement. This statement executes the program to print the message "C++ program!" on the screen. A statement is the fundamental unit of execution in a C++ program. Functions contain statements that the compiler translates into machine language instructions. C++ has a variety of different kinds of statements, and the chapters follow will explore these various kinds of statements. All statements in C++ end with a semicolon (;). A more detailed explanation of statements appears below.

- }

The closing curly brace marks the end of the body of the function. Both the opening curly brace and close curly brace are required for every function definition.

### 2.2 Editing, Compiling and Running the Program

Note which lines in the program end with a semicolon (;) and which do not. Do not put semicolon after the #include preprocessor directive. Do not put semicolon on the curly braces.

C++ programmers have two options for C++ development environments. One involves a command-line environment with a collection of independent tools. The other option is to use an IDE (see Section 1.2) which combines all the tools into a convenient package. Visual Studio is the dominant IDE on the Microsoft Windows platform, Linux and Apple Mac developers often use the Xcode IDE.

The myriad of features and options in these powerful IDEs can be bewildering to learn. In a command-line environment the programmer needs only a few simple commands to edit, compile, and execute programs. Some developers prefer the simplicity and flexibility of command-line environments, such as less complex projects.

One prominent command-line build system is the GCC Compiler Collection (http://gcc.gnu.org/) or GCC for short. The GCC C++ compiler, g++, is one of most C++ standards conforming compilers. The GCC C++ compiler is available for the Microsoft Windows, Apple Mac, and Linux platforms. It is a free, open-source project with a world-wide development team. Appendix C provides an overview of how to use the GCC C++ compiler.

Visual Studio and Xcode offer command line development options. Appendix B provides an overview of the Visual Studio command line development process.

### 2.3 Variations of our program

The two items in 2.1 (simple.cpp) needed to display a message on the screen, cout and endl, have longer names: std::cout and std::endl. The using namespace std allows us to omit the std:: prefixes and use shorter names. This directive is optional, but if it is used, the longer names are required. For example, Listing 2.2 (simple2.cpp) shows an alternative of writing Listing 2.1 (simple.cpp).

Listing 2.2: simple2.cpp
```cpp
#include <iostream>

int main() {
    std::cout << "This is a simple C++ program!" << std::endl;
}
```

Listing 2.3 (simple3.cpp) shows another way to use the shorter names for count and endl within a C++ program.
