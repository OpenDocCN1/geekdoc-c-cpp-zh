
```cpp
//-------------------------------------------
// Class implementation (version 1)
//
// These statements define implementation of an
// xy_coordinate class. They are stored in xy-coordinate.h.
//
// This function reads the xy coordinates from the keyboard.
void xy_coordinate::input()
{
    cin >> x >> y;
}
// This function prints the xy coordinates to the screen.
void xy_coordinate::print()
{
    cout << "(" << x << "," << y << ")" << "\n";
}
// This function computes the radius.
double xy_coordinate::radius()
{
    return sqrt(x*x + y*y);
}
// This function computes the angle in radians.
double xy_coordinate::angle()
{
    // Compute angle of polar form.
    double z, pi=3.141593;
    if (x > 0)
        z = atan(y/x);
    if (x<0 && y>0)
        z = atan(y/x) + pi;
    if (x<0 && y<0)
        z = atan(y/x) - pi;
    if (x==0 && y>0)
        z = atan(y/x) - pi;
    if (x==0 && y==0)
        z = 0;
    return z;
}
//-------------------------------------------
```

We now present a program to test this new data type.

```cpp
//-------------------------------------------
// Program chapter8_7
//
// This program demonstrates the use of
// the xy_coordinate class and its functions.
#include <iostream>
#include <cmath>
#include "xy_coordinate.h"
using namespace std;

int main(void)
{
// Declare and initialize variables.
xy_coordinate pt1;

// Read input point.
cout << "Enter x and y coordinates: " << endl;
pt1.input();

// Print coordinate in xy form and polar form.
cout.setf(ios::fixed);
cout.precision(2);
cout << "Coordinate in xy form: " << endl;
pt1.print();
cout << "Coordinate in polar form: " << endl;
cout << "magnitude: " << pt1.radius() << endl;
cout << "phase (in degrees): " << pt1.angle()*180/3.141593 << endl;

// Exit program.
return 0;
}
//---------------------------------------------
```

To execute this program, you need to be sure that the xy_coordinate header file and the xy_coordinate implementation file are accessible to the compiler, along with the program file. This separation of the components allows us to build our own libraries for programmer-defined classes. These libraries can be used by many application programs in the same way that the standard libraries, such as iostream are used. The application program must include the declarations file and be linked to the implementation file. Using these files, we can now test the program. Here is a sample output from the program:

```
Enter x and y coordinates:
4 4
Coordinate in xy form:
(4.00,4.00)
Coordinate in polar form:
magnitude: 5.66
phase (in degrees): 45.00
```

## Constructor Functions

When we define a variable, we often want to assign an initial value to the variable, as in double sum=0;

If we do not initialize a variable at the time we define it, the variable holds an unknown value until valid data is assigned. Constructor functions are special member functions that are called automatically when an object of that class is declared. The constructor function is used to initialize the data members of the object being defined. When designing a class, a complete set of constructor functions should be provided. Constructor functions have three unique properties:

- a constructor is called automatically when an object of that class is declared;
- the name of a constructor function is the name of the class;
- no return value is associated with a constructor function, and it is not a void function.

To illustrate, we define two constructor functions to initialize the class members. One function initializes x and y to zero; the other initializes x and y to values in the declaration statement. The two declarations are the first ones in the public declaration list in the following code:

```cpp
//-----------------------------------------------
// Class declaration (version 2)
//
// These statements define a class for xy-coordinates.
// Assume that this declaration is stored in xy_coordinate.h.
// The update is the addition of two constructor functions.

#include <iostream>
#include <cmath>
using namespace std;

class xy_coordinate
{
    // Declare two constructor functions and six function
    // prototypes for public members.
    public:
        xy_coordinate();
        xy_coordinate(double a, double b);
        void input();
        void print();
        double radius();
        double angle();

    // Declare private data members.
    private:
        double x, y;
};
//-----------------------------------------------
```

The default constructor is called automatically whenever an object is defined in a declaration as follows:

`xy_coordinate pt1;`

Thus pt1 is an object of the class xy-coordinate. The data members of the object pt1 are initialized to the values assigned by the default constructor function xy-coordinate(). The constructor function with parameters is called automatically whenever an object is defined in a declaration statement as follows:

`xy_coordinate pt2(3,4);`

The data members of the object pt2 will be initialized to the values passed through the parameter list using the constructor function xy-coordinate(double a, double b). Thus, x is given the value 3 and y is given the value 4.

Constructor functions are programmer-defined functions. Here are the constructor functions that should be added to the class implementation file:

```cpp
//--------------------------------------------------------------
// This constructor function initializes x and y to zero.
xy_coordinate::xy_coordinate()
{
    x = 0;
    y = 0;
}
//--------------------------------------------------------------
// This constructor function initializes x and y to parameters.
xy_coordinate::xy_coordinate(double a, double b)
{
    x = a;
    y = b;
}
//--------------------------------------------------------------
```

## Class Operators

The assignment operator is defined for objects of the same class type. If pt1 and pt2 are both xy_coordinate objects, then this statement is a valid statement:

`pt1 = pt2;`

Each data member of the object pt1 is assigned the value of the corresponding data member of the object pt2. However, the C++ arithmetic operators and relational operators cannot automatically be used with a programmer-defined class type. This comparison is not valid:

`if (pt1 == pt2) (invalid comparison)`

A class definition can include a set of operators to be used with objects of the class.

## Overload

The ability to overload operators is a powerful feature in C++. Overloading operators allows a programmer-defined data type to be used as easily as any predefined data type. As an example, consider the arithmetic operators defined in C++. These operators are defined to operate on all predefined data types. However, they are not defined for objects of programmer-defined data types. When designing a class data type, a set of arithmetic operators that work on objects of the class may be included. Operators are included in a class definition in the same way as member functions, except that the keyword operator is used. It is followed by the name of the function, where the name of the function is one of the predefined C++ operators. Only predefined operators may be overloaded. You may not, for example, define a new operator ** to perform exponentiation since this operator is not one of the predefined operators in C++. In the next section, we illustrate the use of overloaded operators in the definition of a complex number class that includes the arithmetic operators (i.e., +, -, *, /).

## 8.8 Numerical Technique: Complex Roots

Complex numbers are needed to solve many problems in science and engineering, particularly in physics and electrical engineering. Therefore, it is often very useful to define a complex class in C++. (Some compilers have added a complex class, but since it is not part of the standards, you will not find it consistently available.) Recall that a complex number has the form a + bi, where i is √-1 and a and b are real numbers. Thus, the real part of the number is represented by a, and the imaginary part of the number is represented by b. An obvious way to represent a complex number is with an ordered pair of real values. Thus, complex number representations are very similar to the xy-coordinate representation in the previous section. In fact, if we just relabel the x-axis to the real axis, and relabel the y-axis the imaginary axis, we will have a representation for complex values, as shown in Figure 8.3.

To input a complex number from the keyboard, we enter two values; hence, the input function is essentially the same as for xy-coordinates. The output of a complex number is different, because we want to include a reference to i. For example, the complex value represented the pair of numbers (3, 5) could be printed as 3+5i. If the imaginary part is negative, then we would prefer the output to be 3−2i instead of 3+−2i. This preference is handled in the member function definition for printing a complex number.

When an arithmetic operation is performed between two complex values, the result is also a complex value. The rules for complex arithmetic are not as familiar as those for integers or real values. Table 8.3 lists results of the basic operations with two complex numbers.

We often refer to the magnitude and phase of a complex number. These are the r and θ values, respectively, shown in Figure 8.3. These are exactly the same as the magnitude and phase of an xy-coordinate, so we will be able to use similar definitions.

![](img/02c4582f051c5b51776411c92b079035_417_0.png)

Figure 8.3 Graphical representation of a complex number.
