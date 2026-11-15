![](bbox=[0.22, 0.08, 0.55, 0.42])

Figure 10.10 UML diagram for cube.

calculate the volume of a cube will be added to the derived class, and we will overload the << to print the value of a cube instead of a rectangle. A class diagram of Cube is provided in Figure10.10.

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
void print(ostream& const;
};
#endif
```

```
/** Class implementation for Cube ........................*/
/* */
/* filename: cube.cpp */
```