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
```

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