Notice that each member-function name in the function headers (lines 11, 17, 23 and 29) is preceded by the class name and `::`, which is known as the *binary scope resolution operator*. This “ties” each member function to the (now separate) GradeBook class definition (Fig. 3.11), which declares the class’s member functions and data members. Without “GradeBook::” preceding each function name, these functions would not be recognized by the compiler as member functions of class GradeBook—the compiler would consider them “free” or “loose” functions, like `main`. Such functions cannot access GradeBook’s private data or call the class’s member functions, without specifying an object. So, the compiler would not be able to compile these functions. For example, lines 19 and 25 that access variable `courseName` would cause compilation errors because `courseName` is not declared as a local variable in each function—the compiler would not know that `courseName` is already declared as a data member of class GradeBook.

# Common Programming Error 3.9

> When defining a class’s member functions outside that class, omitting the class name and binary scope resolution operator (`::`) preceding the function names causes compilation errors.

To indicate that the member functions in `GradeBook.cpp` are part of class GradeBook, we must first include the `GradeBook.h` header file (line 8 of Fig. 3.12). This allows us to access the class name GradeBook in the `GradeBook.cpp` file. When compiling GradeBook.cpp, the compiler uses the information in GradeBook.h to ensure that

+   1. the first line of each member function (lines 11, 17, 23 and 29) matches its prototype in the `GradeBook.h` file—for example, the compiler ensures that `getCourseName` accepts no parameters and returns a `string`, and that
+   2. each member function knows about the class’s data members and other member functions—for example, lines 19 and 25 can access variable `courseName` because it is declared in `GradeBook.h` as a data member of class GradeBook, and lines 13 and 32 can call functions `setCourseName` and `getCourseName`, respectively, because each is declared as a member function of the class in `GradeBook.h` (and because these calls conform with the corresponding prototypes).

# Testing Class GradeBook

Figure 3.13 performs the same GradeBook object manipulations as Fig. 3.10. Separating GradeBook’s interface from the implementation of its member functions does not affect the way that this client code uses the class. It affects only how the program is compiled and linked, which we discuss in detail shortly.

```
```cpp
// Fig. 3.13: fig03_13.cpp
// GradeBook class demonstration after separating
// its interface from its implementation.
#include <iostream>
using std::cout;
using std::endl;
```
```

**Fig. 3.13** | GradeBook class demonstration after separating its interface from its implementation. (Part 1 of 2.)