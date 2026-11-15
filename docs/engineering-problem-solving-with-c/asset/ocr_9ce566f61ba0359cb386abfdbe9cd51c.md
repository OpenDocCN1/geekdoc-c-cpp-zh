# Notice the first line of the class declaration:

```
class Square : public Rectangle
```

: public specifies that Square will inherit all public and protected members of Rectangle. However, a derived class does not inherit constructors from its base class, thus new constructors must be defined for each derived class.

The constructors defined for a derived class will always call a constructor of their base class. The base class default constructor will be called implicitly at the beginning of execution of a derived constructor, or the derived constructor may explicitly call a parameterized constructor of its base class. When a derived class constructor makes an explicit call to a parameterized constructor of its base class the explicit call must be the first executable statement in the default constructor.

![](bbox=[0.13, 0.25, 0.2, 0.3])

The implementation of Square is given below:

```
/*--------------------------------------------------------------*/
/* Class implementation for Square                             */
/* filename: Square.cpp                                        */
/*--------------------------------------------------------------*/

#include "Square.h"

//Constructors
Square::Square()
{
    //Rectangle constructor called implicitly.
    cout << "Construction Square(). " << this
         << endl;
}

Square::Square(const Point& p, double s):Rectangle(s,s,
                                           p.getX(),
                                           p.getY())
{
    //Parameterized constructor explicitly called in parameter list.
    cout << "Constructing Square( Point, double). " << this
         << endl;
}

double Square::getSide() const
{
    return getWidth();
}

void Square::setSide(double s)
{
    setWidth(s);
    setHeight(s);
}
/*--------------------------------------------------------------*/
```

We will look first at the default constructor of Square. Since the Square class has no additional attributes to initialize, a call to the default constructor of the Rectangle class is all that is needed. The call to the default constructor is done implicitly, thus the only statement in the block that defines the default constructor for Square is a print statement to