
After it is declared, a const identifier can be used in any C++ statement in place of the number it represents. For example, these assignment statements are valid:

```cpp
circum = 2 * PI * radius;        weight = DENSITY * volume;
```

These statements must appear after the declarations for all their variables. Because a const declaration equates a constant to an identifier, and the identifier can be used as a replacement for its initializing constant, these identifiers are referred to as symbolic constants, named constants, or simply constants. These terms are used interchangeably in this book.

## Placement of Statements

At this stage, you have been introduced to a variety of statement types. The general rule in C++ for statement placement is simply that a variable or symbolic constant must be declared before it can be used. Although this rule permits placing both preprocessor directives and declaration statements throughout a program, doing so results in a poor program structure. For good programming form, the following statement ordering should be used:

```cpp
preprocessor directives

int main()
{
    // symbolic constants
    // variable declarations

    // other executable statements

    return value;
}
```

As new statement types are introduced, the placement structure will be expanded to accommodate them. Note that comment statements can be intermixed anywhere within this basic structure. Program 3.14 illustrates this basic structure and uses a symbolic constant to calculate the weight of a steel cylinder. The density of the steel is 0.284 lb/in³ (= 7.738 kg/m³).

## Assignment, Formatting, and Interactive Input

### Program 3.14

```cpp
// This program determines the weight of a steel cylinder
// by multiplying the volume of the cylinder its density.
// The volume of the cylinder is given by the formula PI * pow(radius,2) * height.
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main() {
    const double PI = 3.1416;
    const double DENSITY = 0.284;
    double radius, height, weight;

    cout << "The radius of the cylinder (in inches): " <<
    cin >> radius;
    cout << "The height of the cylinder (in inches): " <<
    cin >> height;
    weight = DENSITY * PI * pow(radius, 2) * height;
    cout << setios(ios::fixed)
         << setflags(ios::showpoint)
         << setprecision(4)
         << "The cylinder weighs " << weight << " pounds" << endl;

    return 0;
}
```

Notice in Program 3.14 two symbolic constants have been defined: PI and DENSITY. The following run was made to determine the weight of the cylinder with a radius of 3 inches and a height of 12 inches.

Enter the radius of the cylinder (in inches): 3
Enter the height of the cylinder (in inches): 12
The cylinder weighs 96.3592 pounds

The advantage of using the named constant PI in Program 3.14 is that it clearly identifies the value of 3.1416 in terms most people recognize. The advantage of using the named constant DENSITY is that the programmer can change the value of the density for another material without having to search through the program to where DENSITY is used. If, course, many different materials are used, DENSITY should be changed from a symbolic constant to a variable. A natural question, then, is asking the difference between symbolic constants and variables.

## Chapter 3 Symbolic Constants

A variable's value can be altered anywhere in a program. By its nature, a named constant is a fixed value that must not be altered after it's defined. Naming a constant rather than assigning the value to a variable ensures that the value in the constant can't be altered. When a named constant appears in an instance, it has the same effect as the constant it represents. Therefore, DENSITY in Program 3.14 is simply another way of representing the number 0.284. Because DENSITY and the number 0.284 are equivalent, the value of DENSITY cannot be subsequently changed in the program. After DENSITY has been defined as a constant, an assignment statement such as

```cpp
DENSITY = 0.156;
```

is meaningless and in an error message because DENSITY is not a variable. Because DENSITY is only a stand-in for the value 0.284, this statement is equivalent to writing the invalid expression 0.284 = 0.156.

In addition to using a constant to name constants, in Program 3.14, you can also use this to equate the value of a constant expression to a symbolic name. A constant expression consists of operators and constants. For example, the statement

```cpp
const double DEG_TO_RAD = 3.1416/180.0;
```

equates the value of the symbolic name, as always, can be used in any statement following its definition. For example, the expression 3.1416/180.0 is required for converting degrees to radians, the symbolic name for this conversion factor can be used conveniently. For example, in the assignment statement whenever this symbolic name is required.

```cpp
height = distance * sin(angle * DEG_TO_RAD);
```

the symbolic constant DEG_TO_RAD is used to convert the value in angle to a radian measure.

A previously defined named constant can also be used in a subsequent statement. For example, the following sequence of statements is:

```cpp
const double PI = 3.1416;
const double DEG_TO_RAD = PI/180.0;
height = distance * sin(angle * DEG_TO_RAD);
```

## Assignment, Formatting, and Interactive Input

### Program 3.15

```cpp
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main() {
    const double PI = 3.1416;
    const double DENSITY = 0.284;
    double radius, height, weight;

    cout << "The radius of the cylinder (in inches): " <<
    cin >> radius;
    cout << "The height of the cylinder (in inches): " <<
    cin >> height;
    weight = DENSITY * PI * pow(radius, 2) * height;
    cout << setios(ios::fixed)
         << setflags(ios::showpoint)
         << setprecision(4)
         << "The cylinder weighs " << weight << " pounds" << endl;

    return 0;
}
```
