
s2.print(cout);
cout << endl;
//Test getSide().
cout << "Length of side of s2 is "
     << s2.getSide() << endl;
//Test area method from Rectangle
cout << " Area of s2 is "
     << s2.area() << endl;
cout << "*****************************\n";
//Test setSide()
s1.setSide(3.2);
//Test print()
cout << " Square s1 has: " << endl;
s1.print(cout);
cout << endl;
}
return 0;
}/*...........................................*/

The output from a sample run of program chapter10_7 is shown below:

```
Constructing Rectangle() ...0xbffffb68
Constructing Square()... 0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Constructing Square( Point, double)... 0xbffffb88
Square s2 has:
Width: 4 Height: 4
Origin: (5,4)
Length of side of s2 is 4
Area of s2 is 16
*****************************
Square s1 has:
Width: 3.2 Height: 3.2
Origin at: (0,0)
```

The output from Program chapter10_7 traces the construction of Square s1 and s2. s1 is defined by the default constructor and has an address of 0xbffffb68. s2 is defined by the parameterized constructor and has an address of 0xbffffb88. We see from the output that a Rectangle is constructed before a Square is constructed. This is understandable since a Square is derived from a Rectangle.

## The Cube class

A cube is a three-dimensional representation of a square. This relationship suggests that a new type to implement the concept of a cube can be derived from Square. A method to

![](img/f2bfa570e453b020c16e048c79a3ea0e_565_0.png)

Figure 10.10 UML diagram for cube.

calculate the volume of a cube will be added to the derived class, and we will overload the << to print the value of a cube instead of a rectangle. A class diagram of Cube is provided in Figure 10.10.

The definition of Cube is given below:

```
#ifndef CUBE_H
#define CUBE_H
/* ...................................................*/
/* Class declaration for Cube */
/* filename: Cube.h */
/* */
#include "Square.h" //Required for Square
#include "Point.h" //Required for Point
#include <iostream> //Required for ostream
class Cube : public Square
{
public:
Cube();
Cube(const Point& p, double);
double volume();
void print(ostream& out) const;
};
#endif
```

```
/** Class implementation for Cube ........................*/
/* */
/* filename: cube.cpp */
```

#include "Cube.h" //Required for Cube
#include <cmath> //Required for pow()

Cube::Cube() : Square()
{
    cout << "Constructing Cube()..."
         << this << endl;
}

Cube::Cube(const Point& p, double s):Square(p,s)
{
    cout << "Constructing Cube(Point, double)..."
         << this << endl;
}

double Cube::volume()
{
    return pow(getSide(), 3);
}

void Cube::print(ostream& out) const
{
    Rectangle r;
    r = *this; // A cube is a rectangle.

    //Print the depth
    out << "Depth: " << this->getSide() << " ";

    //Call Rectangle << to finish the job.
    Rectangle::print(out);
}
/*---------------------------------------------*/

A program to test the Cube class is provided next.

```
/*---------------------------------------------*/
/* Program chapter10_8 */
/* filename: testCube.cpp */
/* This program tests the Cube class */
/*---------------------------------------------*/
#include<iostream>//Required for cout
#include "Point.h"//Required for Point
#include "Cube.h"//Required for Cube
using namespace std;

int main()
{
    Point p1(4,2);

    //Test constructors.
    Cube c1, c2(p1, 3);
```

//Test << operator
cout << "c1 : ";
c1.print(cout);
cout << endl;
cout << "c2 : " ;
c2.print(cout);
cout << endl;

//Test volume.
cout << " Volume of a c2 is " << c2.volume()
<< endl;
return 0;
}
```

```
/******************************************************************/
```

Program chapter10_8 generated the following output on a sample run:

```
Constructing Rectangle() ...0xbffffb68
Constructing Square() ...0xbffffb68
Constructing Cube() ...0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Constructing Square(Point, double) ...0xbffffb88
Constructing Cube(Point, double)...0xbffffb88
c1: Depth: 1 Width: 1 Height: 1
c2: Depth: 3 Width: 3 Height: 3
Origin at: (4,2)
Volume of a c2 is 27
```

Again we see the order in which constructors are called when building objects of derived types.

## 10.7 virtual Methods

All methods defined in Rectangle, Square, and Cube classes are, by default, non-virtual methods. When a non-virtual method is called, the method executed is the method defined by the static class type of the calling object. Consider the following example:

```
Point p1(2, 1);
Cube c1(p1,4);
Rectangle r1(1, 3.5, 4.5);
r1 = c1;
r1.print(cout);
...
```

In the above example, r1 is assigned the value of c1. This is valid since a Cube is a Rectangle. However, when r1 calls the print method, it calls the print method defined in Rectangle, not Cube, because the static class type of r1 is Rectangle. The output from the above code segment would be as follows:

```
Constructing Rectangle(parameter list)...0xbffffb68
Constructing Square( Point, double)... 0xbffffb68
Constructing Cube(Point, double)...0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Width: 4 Height: 4
Origin at: (2,1)
```

If a method is defined to be virtual, and pointers or references to objects are used instead of statically defined objects, then C++ supports dynamic binding. Dynamic binding refers to the binding of an object to a specific type at run time. Consider the following example that uses pointers to objects:

```
///Define an array of pointers to Rectangles
Rectangle* rPtrs[4];

//Define 2 Cubes and 2 Squares.
Point p1(2,1); Point p2;
Cube c1(p1,4);
Cube c2(p1,5);
Square s1, s2(p2,5.5);

rPtrs[0] = &c1;
rPtrs[1] = &c2;
rPtrs[2] = &s1;
rPtrs[3] = &s2;

for(int i=0; i<4; ++i)
{
   rPtrs[i]->print(cout);
   cout << endl;
}
...
```

The array rPtrs holds pointers to Rectangles, but the pointers are referencing Cubes and Squares. Since the print method defined in Rectangle is non-virtual, the print method defined in the Rectangle class will be called four times, as illustrated in the output generated from the above code segment:

```
Constructing Rectangle(parameter list)... 0xbffffb20
Constructing Square( Point, double)... 0xbffffb20
Constructing Cube(Point, double)...0xbffffb20
Constructing Rectangle(parameter list)... 0xbffffb40
Constructing Square( Point, double)... 0xbffffb40
Constructing Cube(Point, double)...0xbffffb40
Constructing Rectangle() ... 0xbffffb60
Constructing Square()... 0xbffffb60
Constructing Rectangle(parameter list)...0xbffffb80
Constructing Square( Point, double)...0xbffffb80
Width: 4 Height: 4
Origin at: (2,1)
Origin at: (2,1)
Width: 1 Height: 1
Origin at: (0,0)
Width: 5 Height: 5
Origin at: (0,0)
```

When the keyword virtual is applied to the print method prototype, as in:

```
virtual void print(ostream&) const;
```

the above code segment generates the following output:

```
Constructing Rectangle(parameter list)... 0xbffffb10
Constructing Square( Point, double)... 0xbffffb10
Constructing Cube(Point, double)...0xbffffb10
Constructing Rectangle(parameter list)... 0xbffffb34
Constructing Square( Point, double)... 0xbffffb34
Constructing Cube(Point, double)...0xbffffb34
Constructing Rectangle()... 0xbffffb58
Constructing Square()... 0xbffffb58
Constructing Square(parameter list)... 0xbffffb7c
Constructing Cube( Point, double)... 0xbffffb7c
Depth: 4 Width: 4 Height: 4
Origin at: (2,1)
Depth: 5 Width: 5 Height: 5
Origin at: (2,1)
Width: 1 Height: 1
Origin at: (0,0)
Width: 5 Height: 5
Origin at: (0,0)
```

Notice that cubes and squares are printed using the version of the method that corresponds to the dynamic type of the pointer in the array rPtrs. No change to Square or Cube is required. In C++ dynamic binding is only supported through the use of virtual methods, and pointers or references.

![](img/f2bfa570e453b020c16e048c79a3ea0e_569_0.png)

## Practice!

Assume that the print() function defined in the Rectangle class is a virtual function. Given the declaration statements:

```
Point p1(1,2), p2;
Cube *cptr, c1(p1,4);
Square *sptr, s1(p2,5);
Rectangle *rptr, r1(2,2,7,9);
```

show the output generated by the following code segments: Use the Cube class and the Square class defined in this section.
