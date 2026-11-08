
## THE STRUCTURE OF A C++ PROGRAM

When a programmer learns a new programming language, the first program he or she traditionally writes is a Hello World program—a program that displays the message “Hello World” on the screen. Creating this simple program illustrates that the language is capable of instructing the computer to communicate with the “outside” world. The C++ version of the Hello World program is shown in Figure 1-1:

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello World" << endl;
    return 0;
}
```

**Figure 1-1** Hello World program

At this point, you’re not expected to understand all the code in Figure 1-1. Just notice that the code begins with the preprocessor directive, `#include <iostream>`. The **C++ preprocessor** is a program that processes your C++ program before the compiler processes it. The `#include` directive tells the compiler to include another file when the program is compiled. This makes it easy for you to use code previously written by you or others in your programs without having to recreate it. You will learn more about the Visual C++ compiler later in this chapter. Following the `#include` you see `<iostream>`, which is the name of a header file you want to include in this program. The **iostream header file** gives your program access to what it needs to perform input and output in a C++ program. The name of the header file is placed within angle brackets (`< >`). The angle brackets tell the compiler to look for this file in a directory that is specified by the compiler you are using. You will learn more about preprocessor directives throughout this book.

> **NOTE 1**
>
> Namespaces are a relatively new addition to C++ and are used primarily in large programs. In this book, the only namespace you will use is the `std` namespace.

The next line (`using namespace std;`) instructs the compiler to use the std namespace. You can think of a **namespace** as a container that holds various program elements. The **std namespace** contains everything C++ programs need to use the Standard C++ library. The **Standard C++ library** adds functionality to the C++ programming language. For example, this program needs to use the `std` namespace to have access to `cout` and `endl`, which you see on the fifth line in Figure 1-1. Notice that this line ends with a semicolon (`;`). In fact, all C++ statements end with a semicolon. The reason the previous line, `#include <iostream>`, does not end with a semicolon is that it is a preprocessor directive, not a C++ statement.

> **NOTE 2**
>
> You can tell `main` is a function because of the parentheses; all C++ function names are followed by parentheses.

On the third line you see the start of a function named `main`. A **function** is a group of C++ statements that perform a specified task. This is a special function in a C++ program; the `main` function is the first function that executes when any program runs. The programs in the first six chapters of this book will include only a main function. In later chapters you will be able to include additional functions.

The first part of any function is its **header**. In Figure 1-1, the header for the `main` function begins with the `int` keyword, followed by the function name, which is `main`. A **keyword** is a special word that is reserved by C++ to have a special meaning. To understand the keyword `int` you need to know that functions often send values back to a calling function (for example, the result of a calculation), which can then be used elsewhere in the program. Another way to say this is that functions sometimes return a value. In Figure 1-1, the keyword `int` indicates that the `main` function returns an integer. You will learn more about functions returning values in Chapter 7 of this book.

The opening curly brace `{` on the fourth line of Figure 1-1 marks the beginning of the body of the `main` function and the closing curly brace `}` on the last line of Figure 1-1 marks the end of the `main` function. All the code within this pair of curly braces executes when the `main` function executes. In Figure 1-1, there are two lines of code between the curly braces. The first is:

```cpp
cout << "Hello World" << endl;
```

This is the line that causes the words `Hello World` to appear on the user’s screen. This line consists of multiple parts. The first part, `cout`, is the name of an object that represents the user’s screen. Next, you see `<<` which is called the **insertion** or **output** operator. You use `cout` and `<<` to output what follows, which in this example is the string constant `"Hello World"`. (The quotation marks will not appear on the screen, but they are necessary to make the program work.) After `"Hello World"` you see another `<<` which causes `endl` to be displayed (after `Hello World`) on the user’s screen. For now, think of `endl` as a **newline** that causes the cursor to be positioned on the line after `Hello World`. You will learn more about `endl` in Chapter 9 of this book. Note that the semicolon that ends the `cout << "Hello World" << endl;` statement is required because it tells the compiler that this is the end of the statement.

> **NOTE**
>
> Don’t confuse the last character in `endl`, `l` (ell), with the digit `1` (one).

The next line of code is `return 0;`. This statement instructs the compiler to return the value 0 from the `main` function. Remember, when you saw the header for the `main` function on the third line of this program, you used the keyword `int` to specify that the `main` function returns an integer; 0 is the returned integer. Conventionally, when a program returns a 0, it means “everything went well and the program is finished.”

Next, you learn about the C++ development cycle so that later in this chapter, you can compile the Hello World program and execute it.

## THE C++ DEVELOPMENT CYCLE

When you finish designing a program and writing the C++ code that implements your design, you must compile and execute your program. This three-step process of writing code, compiling code, and executing code is called the C++ development cycle. It is illustrated in Figure 1-2.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_23_0.png)

Let’s begin by learning about Step 1, writing the C++ source code.

### WRITING C++ SOURCE CODE

As you learned in the previous section, you write a C++ program by creating a function named main that contains C++ statements. But what do you use to write the program, and where do you save it?

One method you can use to write a C++ program is to use a text editor, such as the Windows text editor, Notepad. You can use any text editor, but the steps in this book assume you are using Notepad. To start Notepad, click the Start button, select Programs or All Programs, select Accessories, and then select Notepad. Once Notepad starts, you simply type in your C++ source code. **Source code** is the name used for the statements that make up a C++ program. For example, the code shown earlier in Figure 1-1 is source code.

When you save the file that contains the source code, it is important to give the file a meaningful name, and then add the extension `.cpp`. For the Hello World program, an appropriate name for the source code file is `HelloWorld.cpp`. Of course, it is also important to remember the location of the folder in which you choose to save your source code file.

You move on to Step 2 of the C++ development cycle after saving your source code file. In Step 2, you compile the source code.

### COMPILING A C++ PROGRAM

The Visual C++ compiler is named `cl`. It is a program that is responsible for a two-step process that takes your source code and transforms it into object code and then links the object code to create executable code.

> **NOTE**
>
> The Visual C++ compiler, `cl`, is actually a compiler and a linker.

**Object code** is code in computer-readable form that is linked with libraries to create an executable file. **Executable code** is the 1s and 0s that a computer needs to execute a program.
