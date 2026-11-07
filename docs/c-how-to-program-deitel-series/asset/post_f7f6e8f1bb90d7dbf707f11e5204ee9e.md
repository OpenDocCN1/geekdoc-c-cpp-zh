
```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

**Fig. 3.13** | GradeBook class demonstration after separating its interface from its implementation. (Part 2 of 2.)

As in Fig. 3.10, line 5 of Fig. 3.13 includes the GradeBook.h header so that the compiler can ensure that GradeBook objects are created and manipulated correctly in the client code. Before executing this program, the source-code files in Fig. 3.12 and Fig. 3.13 must both be compiled, then linked together—that is, the member-function calls in the client code need to be tied to the implementations of the class’s member functions—a job performed by the linker.

## The Compilation and Linking Process

The diagram in Fig. 3.14 shows the compilation and linking process that results in an executable GradeBook application that can be used by instructors. Often a class’s interface and implementation will be created and compiled by one programmer and used by a separate programmer who implements the client code that uses the class. So, the diagram shows what’s required by both the class-implementation programmer and the client-code programmer. The dashed lines in the diagram show the pieces required by the class-implementation programmer, the client-code programmer and the GradeBook application user, respectively. [*Note: Figure 3.14 is not a UML diagram.*]

A class-implementation programmer responsible for creating a reusable GradeBook class creates the header GradeBook.h and the source-code file GradeBook.cpp that #includes the header, then compiles the source-code file to create GradeBook’s object code. To hide the class’s member-function implementation details, the class-implementation programmer would provide the client-code programmer with the header GradeBook.h (which specifies the class’s interface and data members) and the GradeBook object code (i.e., the machine code instructions that represent GradeBook’s member functions). The client-code programmer is *not* given GradeBook.cpp, so the client remains unaware of how GradeBook’s member functions are implemented.

The client-code programmer needs to know only GradeBook’s interface to use the class and must be able to link its object code. Since the interface of the class is part of the class definition in the GradeBook.h header, the client-code programmer must have access to this file and must #include it in the client’s source-code file. When the client code is compiled, the compiler uses the class definition in GradeBook.h to ensure that the main function creates and manipulates objects of class GradeBook correctly.

- To create the compilable GradeBook application, the last step is to link:

  1. the object code for the main function (i.e., the client code),
  2. the object code for class GradeBook’s member-function implementations and
  3. the C++ Standard Library object code for the C++ classes (e.g., string) used by the class-implementation programmer and the client-code programmer.

The linker’s output is the *executable* GradeBook application that instructors can use to manage their students’ grades. Compilers and IDEs typically invoke the linker for you after compiling your code.

likely. Suppose that a university can print student transcripts containing course names of only 25 characters or less. If the university uses a system containing GradeBook objects to generate the transcripts, we might want class GradeBook to ensure that its data member courseName never contains more than 25 characters. The program of Figs. 3.15–3.17 enhances GradeBook’s member function setCourseName to perform this validation (also known as validity checking).

## GradeBook Class Definition

GradeBook’s class definition (Fig. 3.15)—and hence, its interface—is identical to that of Fig. 3.11. Since the interface remains unchanged, clients of this class need not be changed when the definition of member function setCourseName is modified. This enables clients to take advantage of the improved GradeBook class simply by linking the client code to the updated GradeBook’s object code.

```cpp
// Fig. 3.15: GradeBook.h
// GradeBook class definition presents the public interface of the class.
// the class-member-function definitions appear in GradeBook.cpp.
#include <string> // program uses C++ standard string class

// GradeBook class definition
class GradeBook
{
public:
   explicit GradeBook( std::string ); // constructor initialize courseName
   void setCourseName( std::string ); // sets the course name
   std::string getCourseName() const; // gets the course name
   void displayMessage() const; // displays a welcome message
private:
   std::string courseName; // course name for this GradeBook
}; // end class GradeBook
```

**Fig. 3.15** | GradeBook class definition presents the public interface of the class.

## Validating the Course Name with GradeBook Member Function setCourseName

The changes to class GradeBook are in the definitions of the constructor (Fig. 3.16, lines 9–12) and setCourseName (lines 16–29). Rather than using a member initializer, the constructor now calls setCourseName. In general, all data members should be initialized with member initializers. However, sometimes a constructor must also validate its argument(s)—often, this is handled in the constructor’s body (line 11). The call to setCourseName validates the constructor’s argument and sets the data member courseName. Initially, courseName’s value will be set to the empty string before the constructor’s body executes, then setCourseName will modify courseName’s value.

In setCourseName, the if statement in lines 18–19 determines whether parameter name contains a valid course name (i.e., a string of 25 or fewer characters). If the course name is valid, line 19 stores it in data member courseName. Note the expression name.size() in line 18. This is a member-function call just like myGradeBook.displayMessage(). The C++ Standard Library’s string class defines a member function size that returns the number of characters in a string object. Parameter name is a string object, so the call name.size() returns the number of characters in name. If this value is less than or equal to 25, name is valid and line 19 executes.

```cpp
// Fig. 3.16: GradeBook.cpp
// Implementations of the GradeBook member-function definitions.
// The setCourseName function performs validation.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// constructor initializes courseName with string supplied as argument
GradeBook::GradeBook( string name )
{
   setCourseName( name ); // validate and store courseName
} // end GradeBook constructor

// function that sets the course name;
// ensures that the course name has at most 25 characters
void GradeBook::setCourseName( string name )
{
   if ( name.size() <= 25 ) // if name has 25 or fewer characters
      courseName = name; // store the course name in the object

   if ( name.size() > 25 ) // if name has more than 25 characters
   {
      // set courseName to first 25 characters of parameter name
      courseName = name.substr( 0, 25 ); // start at 0, length of 25

      cerr << "Name \"" << name << "\" exceeds maximum length (25)\n"
           << "Limiting courseName to first 25 characters.\n" << endl;
   } // end if
} // end function setCourseName

// function to get the course name
string GradeBook::getCourseName() const
{
   return courseName; // return object's courseName
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage() const
{
   // call getCourseName to get the courseName
   cout << "Welcome to the grade book for\n" << getCourseName()
        << "!" << endl;
} // end function displayMessage
```

**Fig. 3.16** | Member-function definitions for class GradeBook with a set function that validates the length of data member `courseName`.

The if statement in lines 21–28 handles the case in which setCourseName receives an *invalid* course name (i.e., a name that is more than 25 characters long). Even if parameter name is too long, we still want to leave the GradeBook object in a *consistent state*—that is,
