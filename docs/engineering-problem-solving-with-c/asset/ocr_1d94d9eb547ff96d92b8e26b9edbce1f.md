```
//Mutator Methods
void setX(double newX) ;
void setY(double newY) ;
);
/*--------------------------------------------------------------*/
```

# Accessor Methods

Accessor methods are value-returning member functions with an empty parameter list. The sole purpose of an accessor method is to return the value of an attribute. Because accessor methods are small, simple methods, they can be defined within the class declaration. The current convention is to name these methods get Attribute(). Notice that we use the const modifier in the definition of our accessor methods. Accessor methods are intended to provide read-only access to an attribute, and the use of the const modifier enforces this. Any attempt to modify a private attribute within a const method will result in a compilation error, as illustrated in our test program. To illustrate the use of accessor methods, we will modify our test program to use the accessor method getX(), to print the value of the x coordinate of a point.

```
#include <iostream>
#include "Point.h"
using namespace std;
int main()
{
    Point p1(2.3, -7.1);
    cout << p1.getX() << endl;
    return 0;
}
```

Since the accessor method getX() is public, the test program now compiles without error and prints the value 2.3 to standard output when executed as shown below. A program trace and memory snapshot is provided for illustration in Figure 6.6.

```
Ingbers-MacBook-Pro:Programs jaingber$ g++ main.cpp Point.cpp
Ingbers-MacBook-Pro:Programs jaingber$ ./a.out
Constructing Point object, parameterized:
input parameters: 2.3,-7.1
2.3
```

Note that the g++ compiler writes the executable code to a file named a.out. The command ./a.out asks the operating system to executes the file a.out, found in the current working directory (./).

# Mutator Methods

Mutator methods are defined as void member functions with one or more input parameters. The sole purpose of a mutator method is to mutate, or change, the value of the calling object. Input parameters allow an application to specify a new value to be assigned to an attribute. The current convention is to name these methods set Attribute(). Notice that we do not use the const modifier in the prototypes of the mutator methods as we did with the accessor