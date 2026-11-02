same name as the class, so that the compiler can distinguish it from the class’s other member functions. An important difference between constructors and other functions is that **constructors cannot return values**, so they cannot specify a return type (not even `void`). Normally, constructors are declared public. You also can create classes with more than one constructor using **function overloading**.

C++ automatically calls a constructor for each object that’s created, which helps ensure that objects are initialized properly before they’re used in a program. The constructor call occurs when the object is created. If a class does not explicitly include constructors, the compiler provides a default constructor with **no parameters**. For example, when line 41 of Fig. 16.5 creates a GradeBook object, the default constructor is called. The default constructor provided by the compiler creates a GradeBook object without giving any initial values to the object’s fundamental type data members. For data members that are objects of other classes, the default constructor implicitly calls each data member’s default constructor to ensure that the data member is initialized properly. This is why the string data member `courseName` (in Fig. 16.5) was initialized to the empty string—the default constructor for class `string` sets the string’s value to the empty string.

In the example of Fig. 16.7, we specify a course name for a GradeBook object when the object is created (e.g., line 47). In this case, the argument `"CS101 Introduction to C++ Programming"` is passed to the GradeBook object’s constructor (lines 14–18) and used to initialize the `courseName`. Figure 16.7 defines a modified GradeBook class containing a constructor with a string parameter that receives the initial course name.

```
```cpp
// Fig. 16.7: fig16_07.cpp
// Instantiating multiple objects of the GradeBook class and using
// the GradeBook constructor to specify the course name
// when each GradeBook object is created.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // constructor initializes courseName with string supplied as argument
   explicit GradeBook( string name )
      : courseName( name ) // member initializer to initialize courseName
   {
      // empty body
   } // end GradeBook constructor

   // function to set the course name
   void setCourseName( string name )
   {
      courseName = name; // store the course name in the object
   } // end function setCourseName
```
```

**Fig. 16.7** | Instantiating multiple objects of the GradeBook class and using the GradeBook constructor to specify the course name when each GradeBook object is created. (Part 1 of 2.)