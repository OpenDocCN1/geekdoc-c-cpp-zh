The output from these statements is:

The radius of the circle is: 10 centimeters
The area is 3.14159 square centimeters

Notice that no decimal point is displayed in the value of radius, even though radius is declared to be of type double. Although this is the default format for printing floating point values in C++, we can override this format using stream functions and manipulators.

![](bbox=[0.06, 0.25, 0.18, 0.42])

# Stream Objects

The identifier cout is declared to be an object of type ostream and is defined by the compiler to stream data to standard output. The ostream class includes methods, also referred to as member functions. Member functions are defined within a class definition, and can be called only by objects of the same class type. Since cout is an object of type ostream the cout object can call member functions of the ostream class to set the state of the format flags associated with standard output. The format flags are data members of the ostream class. A special operator called the dot operator (.) is used when an object calls one of its member functions. The following program uses two member functions of the ostream class to set the desired format for streaming floating point values to standard output. The setf() member function is used to set the format for displaying a floating point value to fixed form, or decimal form. The member function precision() is used to set the number of significant digits that should be displayed to the right of the decimal point.

```
/*------------------------------------------*/
/* Program chapter2_4 */
/* */
/* This program computes area of a circle. */
/* Results are displayed with two digits */
/* to the right of the decimal point. */
/*------------------------------------------*/
#include<iostream> //Required for cout, setf() and precision().
#include<cmath> //Required for acos().
using namespace std;

const double PI = acos(-1.0);

int main()
{
//Declare and initialize objects.
double radius(10), area;
area = PI*radius*radius;
//Call the setf member function using dot operator.
cout.setf(ios::fixed); //Fixed form(xx.xx).

//Call the precision member function using dot operator.
cout.precision(2); //Display 2 digits to right of decimal.
```