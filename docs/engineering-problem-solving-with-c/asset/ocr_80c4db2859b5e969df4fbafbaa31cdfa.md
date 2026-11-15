```
main()
Step1: Point p1 (2.3, -7.1)
Step6: cout << p1.getX() << endl;
Step8: return 0;

Point::Point (double x, double y)
Step2: cout << "Constructing Point object, parameterized: \n";
Step3: cout << "Input parameters: " << x << ", " << y << endl;
Step4: xCoord = X;
Step5: yCoord = y;

Point::getX ()
Step7: return xCoord;
```

Memory snapshot: main()
Step 1: Point p1
2.3 double xCoord
-71 double yCoord

# Figure 6.6 Program trace and memory snapshot.

methods. We have defined the mutator methods in the class implementation. The expanded class implementation is given below.

```
/********************************************************************************/
/* Point Class Chapter6_7 */
/* filename: Point.cpp */
/* #include "Point.h" //Required for Point */
/* #include <iostream> //Required for cout */
/* #include <cmath> //Required for sqrt() and pow() */
using namespace std;

//Parameterized constructor
Point::Point(double x, double y)
{
//input parameters x,y
cout << " Constructing Point object, parameterized: \n";
cout << " Input parameters: " << x << ", " << y << endl;
xCoord = x;
yCoord = y;
}

//Default constructor
Point::Point()
{
cout << " Constructing Point object, default: \n";
cout << " initializing to zero" << endl;
xCoord = 0.0;
yCoord = 0.0;
}
```