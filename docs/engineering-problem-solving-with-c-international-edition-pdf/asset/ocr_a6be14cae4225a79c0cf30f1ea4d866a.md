```
(
//input parameters x,y
cout << " Constructing Point object, parameterized: \n" ;
cout << " input parameters: " << x << " ." << y << endl;
xCoord = x;
yCoord = y;
)
//Default constructor
Point::Point()
{
    cout << " Constructing Point object, default: \n" ;
    cout << " initializing to zero" << endl;
    xCoord = 0.0;
    yCoord = 0.0;
}
```

The parameterized constructor begins with the header Point::Point(double x, double y). Parameterized constructors provide parameters for specifying the initial values of the data members. The parameterized Point constructor provides two parameters, x and y, both of type double. Inside the statement block, the values of these parameters will be assigned to the data members. We begin our statement block with two cout statements for debugging and clarification. These statements will be removed once the Point class has been fully designed and implemented. Following the cout statements, the value of x is assigned to xCoord and the value of y is assigned to yCoord.

The default constructor begins with the header Point::Point(). Since no parameters are provided in the header, the statement block assigns the constant 0.0 to both xCoord and yCoord. Note that we could have chosen any constant as the initial value. The following program declares two objects of type Point.

```
/**
*---------------------------------------------------*
* Program chapter2_3                                *
*                                                   *
* This program illustrates the use of the           *
* programmer-defined data type Point                *
*                                                   *
*/
```

```
#include <iostream> //Required for cout
#include "Point.h" //Required for Point
using namespace std;

int main()
{
    //Declare and initialize objects.
    cout << " In main, declare p1..." << endl;
    cout << p1;
    cout << " \nIn main, declare p2..." << endl;
    Point p2(1.5, -4.7);
    cout << " \nIn main, declare ORIGIN..." << endl;
    const Point ORIGIN(0.0, 0.0);
    return 0;
}
/*---------------------------------------------------*/
```