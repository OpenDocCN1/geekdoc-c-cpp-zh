```
Point p2 -> [1.5] double xCoord
       [-4.7] double yCoord
const Point ORIGIN [0.0] double xCoord
             [0.0] double yCoord
```

The output from Program chapter 2_3 is shown below:

```
In main, declare p1...
Constructing Point object, default:
Initializing to zero
In main, declare p2...
Constructing Point object, parameterized:
Input parameters: 1.5,-4.7
In main, declare ORIGIN...
Constructing Point object, parameterized:
Input parameters: 0,0
```

# Statement Box 2.2

Class Definition: The definition of a programmer-defined class consists of two parts: a class declaration and a class implementation.

```
Syntax: Class Declaration
class ClassName
{
 access modifier:
 declaration of attributes
 access modifier:
 declaration of methods
};
```

```
Syntax: Class Implementation
#include "className.h"
definitions of class methods
```

```
Example: class Declaration
class Point
{
 private:
 double xCoord;
 double yCoord;
 public:
 Point(double x, double y);
};
Usage:
#include "Point.h"
int main()
{
 Point p1(1.5, 2.7);
```

```
Example: class Implementation
#include "Point.h"
Point::Point (double x, double y)
{
 xCoord = x;
 yCoord = Y;
}
```