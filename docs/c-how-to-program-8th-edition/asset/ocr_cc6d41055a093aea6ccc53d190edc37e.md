# 3.6 Placing a Class in a Separate File for Reusability

One of the benefits of creating class definitions is that, when packaged properly, your classes can be *reused* by other programmers. For example, you can reuse C++ Standard Library type string in any C++ program by including the header `<string>` (and, as you’ll see, by being able to link to the library’s object code).

Programmers who wish to use our GradeBook class cannot simply include the file from Fig. 3.7 in another program. As you learned in Chapter 2, function main begins the execution of every program, and every program must have *exactly one* main function. If other programmers include the code from Fig. 3.7, they get extra “baggage”—our main function—and their programs will then have two main functions. Attempting to compile a program with two main functions produces an error when the compiler tries to compile the second main function it encounters. So, placing main in the same file with a class definition *prevents that class from being reused* by other programs. In this section, we demonstrate how to make class GradeBook reusable by *separating it into another file* from the main function.

# Headers

Each of the previous examples in the chapter consists of a single .cpp file, also known as a *source-code file*, that contains a GradeBook class definition and a main function. When building an object-oriented C++ program, it’s customary to define *reusable source code* (such as a class) in a file that by convention has a .h filename extension—known as a *header*. Programs use #include preprocessor directives to include headers and take advantage of reusable software components, such as type string provided in the C++ Standard Library and user-defined types like class GradeBook.

Our next example separates the code from Fig. 3.7 into two files—GradeBook.h (Fig. 3.9) and fig03_10.cpp (Fig. 3.10). As you look at the header in Fig. 3.9, notice that it contains only the GradeBook class definition (lines 8–38), the appropriate headers and a using directive. The main function that uses class GradeBook is defined in the source-code file fig03_10.cpp (Fig. 3.10) in lines 18–18. To help you prepare for the larger programs you’ll encounter later in this book and in industry, we often use a separate source-code file containing function main to test our classes (this is called a *driver program*). You’ll soon learn how a source-code file with main can use the class definition found in a header to create objects of a class.

```
```cpp
// Fig. 3.9: GradeBook.h
// GradeBook class definition in a separate file from main.
#include <iostream>
#include <string> // class GradeBook uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
    // constructor initializes courseName with string supplied as argument
    GradeBook( string name )
    {
```
```

Fig. 3.9 | *GradeBook class definition in a separate file from main. (Part 1 of 2.)*