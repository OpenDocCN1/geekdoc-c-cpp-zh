```
xCoord = x;
yCoord = y;
}
```

The default constructor begins with the header `Point::Point()`. Inside the block of code that defines the default constructor, the value 0.0 is assigned to the data members `xCoord` and `yCoord`. This ensures that all `Point` objects declared using the default constructor will have an initial value of 0.0.

The parameterized constructor begins with the header `Point::Point(double x, double y)`. Inside the block of code that defines the parameterized constructor, the parameter `x` is assigned to the data member `xCoord` and the parameter `y` is assigned to the data member `yCoord`. This ensures that all Point objects declared using the parameterized constructor will have an initial value specified by the values in the type declaration statement.

![](bbox=[0.15, 0.3, 0.21, 0.34])

In the implementation of our `Point` class we have included `cout` statements in each of our constructors. `cout` statements are useful for tracing execution and debugging, and can be commented out once the method has been fully tested.

![](bbox=[0.15, 0.38, 0.21, 0.42])

Program `chapter2_3` illustrates the use of the programmer defined data type, `Point`. Note that the compiler directive `#include "Point.h"` is included in Program `chapter2_3`. Applications that want to use a programmer-defined type must include the `class` declaration file in their source code.

```
/*-------------------------------- Program chapter2_3 ----------------------------------*
/* Program 2.3 */
/* */
/* This program illustrates the use of the */
/* programmer-defined data type Point */
/* */

#include <iostream> //Required for cout
#include "Point.h" //Required for Point
using namespace std;

int main()
{
 //Declare and initialize objects.
 cout << "In main, declare p1..." << endl;
 Point p1;
 cout << "In main, declare p2..." << endl;
 Point p2(1.5, -4.7);
 cout << "In main, declare ORIGIN..." << endl;
 const Point ORIGIN(0.0, 0.0);

 return 0;
}
/*-----------------------------------------------------------*/

memory snapshot:
Point p1 -> | 0.0 | double xCoord
          | 0.0 | double yCoord
```