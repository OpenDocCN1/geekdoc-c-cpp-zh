
// class implementation section
Circle::Circle(double r)  // constructor
{
    radius = r;
}

// calculate the area of a circle
double Circle::calcval()
{
    return(PI * radius * radius);
}

Except for substituting the access specifier protected in place of the usual private specifier for the data member, this code is a standard class definition. The only variable not defined is PI, which is used in the calcval() function. It's defined as follows:

```
const double PI = 2.0 * asin(1.0);
```

This definition is simply a "trick" that forces the computer to return the value of PI accurate to as many decimal places as your computer allows. This value is obtained by taking the arcsine of 1.0, which is π/2, and multiplying the result by 2.

Having defined the base class, you can now extend it to a derived class, which has this definition:

```
// class declaration section where Cylinder is derived from Circle
class Cylinder : public Circle
{
    protected:
        double length;  // add one data member and
    public:             // two member functions
    Cylinder(double r = 1.0, double l = 1.0) : Circle(r), length(l) {}
    double calcval();
};
```

```
// class implementation section
double Cylinder::calcval()   // calculates a volume
{
    return (length * Circle::calcval()); // note the base function call
}
```

This definition encompasses several important concepts related to derived classes. First, as a derived class, Cylinder contains all the data members and member functions of its base class, Circle, plus any of its own members it might add. In this case, the Cylinder class consists of a radius data member, inherited from the Circle class, plus a length data member. Therefore, each Cylinder object contains two data members, as shown in Figure 12.3.

## Figure 12.3 Relationship between Circle and Cylinder data members

![](img/202cface8244f523c2641baa2e00d7dd_563_0.png)

In addition, the Cylinder class inherits Circle’s member functions. This inheritance is shown in the Cylinder constructor, which uses a base/member initialization list (see Section 11.1) that calls the Circle constructor. It’s also shown in Cylinder’s calcval() function, which makes a call to Circle::calcval().

In both classes, the same function name, calcval(), has been used to illustrate overriding a base function with a derived function. When a cylinder object calls calcval(), it’s a request to use the Cylinder version of the function; a Circle object call to calcval() is a request to use the Circle version. In this case, the Cylinder class can access only the class version of calcval() by using the scope resolution operator, as in the call Circle::calcval(). Program 12.1 uses these two classes in the context of a complete program.

## Program 12.1

```
#include <iostream>
#include <cmath>
using namespace std;
```

```
const double PI = 2.0 * asin(1.0);

// class declaration section
class Circle
{
protected:
    double radius;
public:
    Circle(double = 1.0);  // constructor
    double calcval();
};

// class implementation section for Circle
Circle::Circle(double r)  // constructor
{
    radius = r;
}
```

The first three output lines are straightforward and are produced by the first three cout statements in the program. As the output shows, a call to calcval() with a Circle object activates the Circle version of this function, and a call to calcval() with a Cylinder object activates the Cylinder version.

The assignment statement Circle_1 = Cylinder_1; introduces another important relationship between a base and derived class: A derived class object can be assigned to a base class object. This relationship shouldn’t be surprising because base and derived classes share a common set of data member types. In this type of assignment, only this set of data members, which consists of all the base class data members, is assigned. Therefore, as shown in Figure 12.4, the Cylinder to Circle assignment results in the following memberwise assignment:

Circle_1.radius = Cylinder_1.radius;

![](img/202cface8244f523c2641baa2e00d7dd_565_0.png)

The length data member of the Cylinder object isn’t used in the assignment because it has no equivalent variable in the Circle class. The reverse cast, from base to derived class, isn’t as simple and requires a constructor to initialize the derived class members that aren’t in the base class.

Before leaving Program 12.1, one other point should be made. Although the Circle constructor was called explicitly by using a base/member initialization list for the Cylinder constructor, an implicit call could have been made. In the absence of an explicit derived class constructor, the compiler automatically calls the default base class constructor first, before the derived class constructor is called. This order of calling works because the derived class contains all the base class’s data members. In a similar fashion, destructor methods are called in the reverse order—first derived class and then base class.

## EXERCISES 12.1

- 1. (Review) Define the following terms:
- a. inheritance
- d. simple inheritance
- b. base class
- e. multiple inheritance
- c. derived class
- f. class hierarchy
- 2. (Review) Describe the difference between private and protected class members.
- 3. (Review) What three features must a programming language include to be classified as an object-oriented language?

4. (Modify) a. Modify Program 12.1 to include a derived class named Sphere from the base Circle class. The only additional class members of Sphere should be a constructor and a calcval() function that returns the sphere's volume. (Note: Volume = 4 / 3 πr³.)
b. Include the class constructed for Exercise 4a in a working C++ program. Have your program call all the member functions in the Sphere class.

5. (Program) a. Create a base class named Point consisting of x and y data members representing point coordinates. From this class, derive a class named Circle with another data member named radius. For this derived class, the x and y data members represent a circle's center coordinates. The member functions of the Point class should consist of a constructor, an area() function that returns 0, and a distance() function that returns the distance between two points (x₁, y₁) and (x₂, y₂), where distance = √((x₂ - x₁)² + (y₂ - y₁)²) Additionally, the derived class should have a constructor and an override function named area() that returns a circle's area.
b. Include the classes constructed for Exercise 5a in a working C++ program. Have your program call all the member functions in each class. In addition, call the base class's distance() function with two Circle objects and explain the result this function returns.

6. (Modify) a. Using the classes constructed for Exercise 5a, derive a class named Cylinder from the Circle class. The Cylinder class should have a constructor and a member function named area() that determines a cylinder's surface area. For this function, use the algorithm surface area = 2πr(l + r), where r is the radius of the cylinder and l is the length.
b. Include the classes constructed for Exercise 6a in a working C++ program. Have your program call all the member functions in the Cylinder class.
c. What do you think the result might be if the Point (base) class's distance() function is called with two Cylinder objects?

7. (Program) a. Create a base class named Rectangle containing length and width data members. From this class, derive a class named Box with another data member named depth. The member functions of the base Rectangle class should consist of a constructor and an area() function. The derived Box class should have a constructor, a volume() function, and an override function named area() that returns the surface area of the box.
b. Include the classes constructed for Exercise 7a in a working C++ program. Have your program call all the member functions in each class, and verify the results manually.

## 12.2 Polymorphism

As defined previously, polymorphism allows using the same function name to invoke one response in a base class's objects and another response in a derived class's objects. Overriding a base member function by using an overloaded derived member function, as shown with the calcval() function in Program 12.1, is an example of polymorphism. In some situations, however, this method of overriding doesn't work the way you might want. To understand why, take a look at Program 12.2.
