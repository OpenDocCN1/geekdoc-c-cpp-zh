
```cpp
public:
   // constructor initializes courseName with string supplied as argument
   GradeBook( string name )
   {
      setCourseName( name ); // call set function to initialize courseName
   } // end GradeBook constructor

   // function to set the course name
   void setCourseName( string name )
   {
      courseName = name; // store the course name in the object
   } // end function setCourseName

   // function to get the course name
   string getCourseName()
   {
      return courseName; // return object's courseName
   } // end function getCourseName

   // display a welcome message to the GradeBook user
   void displayMessage()
   {
      // call getCourseName to get the courseName
      cout << "Welcome to the grade book for\n" << getCourseName()
           << "!" << endl;
   } // end function displayMessage
private:
   string courseName; // course name for this GradeBook
}; // end class GradeBook
```

*Fig. 3.9 | GradeBook class definition in a separate file from main. (Part 2 of 2.)*

```cpp
// Fig. 3.10: fig03_10.cpp
// Including class GradeBook from file GradeBook.h for use in main.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// function main begins program execution
int main()
{
   // create two GradeBook objects
   GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
   GradeBook gradeBook2( "CS102 Data Structures in C++" );

   // display initial value of courseName for each GradeBook
   cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
        << "\ngradeBook2 created for course: " << gradeBook2.getCourseName()
        << endl;
} // end main
```

*Fig. 3.10 | Including class GradeBook from file GradeBook.h for use in main. (Part 2 of 2.)*

```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

*Fig. 3.10 | Including class GradeBook from file GradeBook.h for use in main. (Part 2 of 2.)*

## Including a Header File That Contains a User-Defined Class

A header file such as GradeBook.h (Fig. 3.9) cannot be used to begin program execution, because it does not contain a main function. If you try to compile and link GradeBook.h by itself to create an executable application, Microsoft Visual C++ 2008 produces the linker error message:

```
error LNK2001: unresolved external symbol _mainCRTStartup
```

To compile and link for GNU C++ on Linux, you must first include the header file in a .cpp source-code file, then GNU C++ produces a linker error message containing:

```
undefined reference to `main'
```

This error indicates that the linker could not locate the program’s main function. To test class GradeBook (defined in Fig. 3.9), you must write a separate source-code file containing a main function (such as Fig. 3.10) that instantiates and uses objects of the class.

The compiler does not know what a GradeBook is because it’s a user-defined type. In fact, the compiler doesn’t even know the classes in the C++ Standard Library. To help it understand how to use a class, we must explicitly provide the compiler with the class’s definition—that’s why, for example, to use type string, a program must include the `<string>` header file. This enables the compiler to determine the amount of memory that it must reserve for each object of the class and ensure that a program calls the class’s member functions correctly.

To create GradeBook objects gradeBook1 and gradeBook2 in lines 11–12 of Fig. 3.10, the compiler must know the size of a GradeBook object. While objects conceptually contain data members and member functions, C++ objects contain only data. The compiler creates only one copy of the class’s member functions and shares that copy among all the class’s objects. Each object, of course, needs its own copy of the class’s data members, because their contents can vary among objects (such as two different BankAccount objects having two different balance data members). The member-function code, however, is not modifiable, so it can be shared among all objects of the class. Therefore, the size of an object depends on the amount of memory required to store the class’s data members. By including GradeBook.h in line 4, we give the compiler access to the information it needs (Fig. 3.9, line 37) to determine the size of a GradeBook object and to determine whether objects of the class are used correctly (in lines 11–12 and 15–16 of Fig. 3.10).

Line 4 instructs the C++ preprocessor to replace the directive with a copy of the contents of GradeBook.h (i.e., the GradeBook class definition) before the program is compiled. When the source-code file fig03_10.cpp is compiled, it now contains the GradeBook class definition (because of the #include), and the compiler is able to determine how to create GradeBook objects and see that their member functions are called correctly. Now that the class definition is in a header file (without a main function), we can include that header in any program that needs to reuse our GradeBook class.

### How Header Files Are Located

Notice that the name of the GradeBook.h header file in line 4 of Fig. 3.10 is enclosed in quotes ("") rather than angle brackets (`< >`). Normally, a program's source-code files and user-defined header files are placed in the same directory. When the preprocessor encounters a header file name in quotes, it attempts to locate the header file in the same directory as the file in which the #include directive appears. If the preprocessor cannot find the header file in that directory, it searches for it in the same location(s) as the C++ Standard Library header files. When the preprocessor encounters a header file name in angle brackets (e.g., `<iostream>`), it assumes that the header is part of the C++ Standard Library and does not look in the directory of the program that is being preprocessed.

> **Error-Prevention Tip 3.3**
>
> To ensure that the preprocessor can locate header files correctly, #include preprocessor directives should place the names of user-defined header files in quotes (e.g., "GradeBook.h") and place the names of C++ Standard Library header files in angle brackets (e.g., `<iostream>`).

### Additional Software Engineering Issues

Now that class GradeBook is defined in a header file, the class is reusable. Unfortunately, placing a class definition in a header file as in Fig. 3.9 still reveals the entire implementation of the class to the class's clients—GradeBook.h is simply a text file that anyone can open and read. Conventional software engineering wisdom says that to use an object of a class, the client code needs to know only what member functions to call, what arguments to provide to each member function and what return type to expect from each member function. The client code does not need to know how those functions are implemented.

If client code does know how a class is implemented, the client-code programmer might write client code based on the class's implementation details. Ideally, if that implementation changes, the class's clients should not have to change. Hiding the class's implementation details makes it easier to change the class's implementation while minimizing, and hopefully eliminating, changes to client code.

In Section 3.8, we show how to break up the GradeBook class into two files so that

- 1. the class is reusable,
- 2. the clients of the class know what member functions the class provides, how to call them and what return types to expect, and
- 3. the clients do *not* know how the class's member functions are implemented.

## 3.8 Separating Interface from Implementation

In the preceding section, we showed how to promote software reusability by separating a class definition from the client code (e.g., function main) that uses the class. We now introduce another fundamental principle of good software engineering—separating interface from implementation.

### Interface of a Class

Interfaces define and standardize the ways in which things such as people and systems interact with one another. For example, a radio's controls serve as an interface between the
