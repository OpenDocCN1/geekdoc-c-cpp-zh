
You should always place a class's data members within its private section. Typically, you provide methods—such as setRadius and getRadius—to access the data members. In this way, you control how and whether the rest of the program can access the data members. This design principle should lead to programs that not only are easier to debug, but also have fewer logical errors from the beginning.

A class's data members should be private

Some method declarations, such as

```
double getRadius() const;
```

const methods cannot change a class's data members

are tagged with const. Such methods cannot alter the data members of the class. Making getRadius a const method is a fail-safe technique that ensures that it will only return the current value of the sphere's radius, without changing it.

## A.8.2 The Implementation File

Let's begin implementing the class Sphere by examining its constructors.

**Constructors.** A constructor allocates memory for an object and can initialize the object's data to particular values. A class can have more than one constructor, as is the case for the class Sphere.

A default constructor has no arguments

The first constructor in Sphere is the **default constructor**:

```
Sphere();
```

A default constructor by definition has no arguments. Typically, a default constructor initializes data members to values that the class implementation chooses. For example, the implementation

```
Sphere::Sphere()
{
    theRadius = 1.0;
} // end default constructor
```

sets theRadius to 1.0. Chapter 3 will show you another way to initialize data members within constructors that is preferable to using assignment statements.

Notice the qualifier Sphere:: that precedes the constructor's name. When you implement any method, you qualify its name with its class type followed by the **scope resolution operator** :: to distinguish it from other methods that might have the same name.

When you declare an instance of the class, you implicitly invoke a constructor. For example, the statement

```
Sphere unitSphere;
```

invokes the default constructor, which creates the object unitSphere and sets its radius to 1.0. Notice that you do not include parentheses after unitSphere.

The next constructor in Sphere is

```
Sphere(double initialRadius);
```

It creates a sphere object of radius initialRadius. This constructor needs only to initialize the private data member theRadius to initialRadius. Its implementation is

```
Sphere::Sphere(double initialRadius)
{
    theRadius = initialRadius;
} // end constructor
```

You implicitly invoke this constructor by writing a declaration such as

```
Sphere mySphere(5.1);
```

In this case, the object mySphere has a radius of 5.1.

We can make the previous constructor ensure that the given radius is not negative by writing its definition as follows:

```
Sphere::Sphere(double initialRadius)
{
   if (initialRadius > 0)
      theRadius = initialRadius;
   else
      theRadius = 1.0;
} // end constructor
```

> Note: If you omit all constructors from your class, the compiler will generate a default constructor—that is, one with no arguments—for you. A compiler-generated default constructor, however, might not initialize data members to values that you will find suitable. If you define a constructor that has arguments but you omit the default constructor, the compiler will not generate one for you. Thus, you will not be able to write statements such as Sphere defaultSphere;

Typically, you place the implementation of a class's constructors and other methods in an implementation file whose name ends in .cpp. Listing A-3 contains an implementation file for the class Sphere. Notice that within the definition of a method, you can reference the class's data member or invoke its other methods without preceding the member names with Sphere::. In particular, notice how the constructor calls the method setRadius to avoid duplicating the code that ensures a positive radius.

## LISTING A-3 The implementation file Sphere.cpp

```
// #include "Sphere.cpp" /
#include "Sphere.h" // Include the header file
using namespace std;
Sphere::Sphere()
{
   theRadius = 1.0;
} // end default constructor
Sphere::Sphere(double initialRadius)
{
   setRadius(initialRadius); // Sphere:: not needed here
} // end constructor
void Sphere::setRadius(double newRadius)
{
   if (newRadius > 0)
      theRadius = newRadius;
   else
      theRadius = 1.0;
} // end setRadius
double Sphere::getRadius() const
{
   return theRadius;
} // end getRadius

double Sphere::getDiameter() const
{
   return 2.0 * theRadius;
} // end getDiameter

double Sphere::getCircumference() const
{
   return PI * getDiameter();
} // end getCircumference

double Sphere::getArea() const
{
   return 4.0 * PI * theRadius * theRadius;
} // end getArea

double Sphere::getVolume() const
{
   double radiusCubed = theRadius * theRadius * theRadius;
   return (4.0 * PI * radiusCubed) / 3.0;
} // end getVolume

// End of implementation file.
```

A local variable such as radiusCubed should not be a data member

> **Note: Local variables**
> 
> You should distinguish between a class's data members and any local variables that the implementation of a method requires. It is inappropriate for such local variables to be data members of the class.

## A.8.3 Using the Class Sphere

The following simple program demonstrates the use of the class Sphere:

```
#include <iostream>
#include "Sphere.h"

using namespace std;

int main()
{
   Sphere unitSphere; // Radius is 1.0
   Sphere mySphere( 5.1 ); // Radius is 5.1

   unitSphere.displayStatistics();
   mySphere.setRadius( 4.2 ); // Resets radius to 4.2
   cout << "mySphere.getDiameter() < endl;
   return 0; // end main
}
```

An object such as mySphere can, on request, reset the value of its radius; return its radius; and compute its diameter, surface area, circumference, and volume. These requests to an object are called messages and are simply calls to methods. Thus, an object responds to a message by acting on its data. To invoke an object’s method, you qualify the method’s name—such as setRadius—with the object variable—such as mySphere.

Notice that the previous program included the header file Sphere.h, but did not include the implementation file Sphere.cpp. You compile a class’s implementation file separately from the program that uses the class. The way you tell the operating system where to locate the compiled implementation depends on the particular system. Section A.9 of this appendix and C++ Interlude 1 provide more information about header and implementation files.

The previous program is an example of a client of a class. A client of a particular class is simply a program or module that uses the class. We will reserve the term user for the person who uses a program.

## A.8.4 Inheritance

A brief discussion of inheritance is provided here, because it is a common way to create new classes in C++. Further discussions of inheritance occur as needed throughout the book.

A class derived from the class Sphere

Suppose we want to give our spheres a color, knowing that we have already developed the class Sphere. Instead of writing an entirely new class of spheres that have a color, we can reuse the Sphere implementation and add color characteristics and operations by using inheritance. Here is a declaration of the class SphereInColor that uses inheritance:

```
#include "Sphere.h"
enum Color {RED, BLUE, GREEN, YELLOW};
class SphereInColor : public Sphere
{
private:
    Color sphereColor;
public:
    SphereInColor(Color initialColor);
    SphereInColor(Color initialColor, double initialRadius);
    void setColor(Color newColor);
    Color getColor() const;
}; // end SphereInColor
```

The class Sphere is called the base class or superclass, and SphereInColor is called the derived class or subclass of the class Sphere.

Any instance of the derived class is also considered to be an instance of the base class and can be used in a program anywhere that an instance of the base class can be used. Also, when the keyword public precedes the name of the base class in the new class’s header, any of the publicly defined methods or data members that can be used with instances of the base class can be used with instances of the derived class. The derived class instances also have the additional methods and data members that are publicly defined in the derived class definition.

The implementation of the methods for the class SphereInColor is as follows:

```
SphereInColor::SphereInColor(Color initialColor): Sphere()
{
    sphereColor = initialColor;
} // end constructor
SphereInColor::SphereInColor(Color initialColor, double initialRadius)
    : Sphere(initialRadius)
{
    sphereColor = initialColor;
} // end constructor
