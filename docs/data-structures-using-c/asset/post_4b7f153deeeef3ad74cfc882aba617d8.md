
### A.8.1 Types of Polymorphism

Polymorphism is one of the important features of OOP. There are two types of polymorphism—compile-time and run-time. Compile-time polymorphism is achieved using function overloading and operator overloading, whereas run-time polymorphism is achieved using virtual functions.

## A.9 CONSTRUCTORS AND DESTRUCTORS

Let us discuss about constructor, destructor, and overloading.

### A.9.1 Constructors

Constructors are methods used to initialize an object during definition. Consider the following class definition:

```cpp
class Car
{
 int mirror;
 int colour;
 public:
 Car() // constructor
 {
 mirror = 0; // no mirrors
 colour = 0; // colour 0 means a white colour car
 cout << "A car is created\n";
 }
};
```

Here, the function Car() is a constructor.

Constructors have the same name as that of the class. They have no return value. However, similar to other functions, they can take arguments. For example, we may want to initialize a car to coordinates other than the default (0, 0). We, therefore, define a second constructor taking two integer arguments within the class as follows:

```cpp
class Car
{
 int mirror, colour;
 public:
 Car()
 {
 mirror = colour = 0;
 }
 Car(const int M, const int C) // Parameterized constructor
 {
 mirror = M;
 colour = C;
 }
 void setMirror(const int M);
 void setColour(const int C);
 int getMirror() {return mirror;}
 int getColour(){return colour;}
};
```

Thus, constructors can be overloaded in this manner. Constructors are implicitly called when we define objects of their classes:

```
Point WhiteCar; calls Car::Car()
Point RedCar(2, 3); calls Car::Car(const int, const int)
```

To create a Point from another Point by copying the properties of one object to a newly created one, the copy process needs to be taken care of. Let us consider the class Point in the following code. In the class Point, we add a third constructor that takes care of copying values from one object to the newly created one.

```cpp
class Point
{
int _x, _y;
public:
Point()
{
_x = _y = 0;
}
Point(const int x, const int y)
{
_x = x;
_y = y;
}
Point(const Point & from) // Copy constructor
{
_x = from._x;
_y = from._y;
}
void setX(const int val);
void setY(const int val);
int getX() { return _x; }
int getY() { return _y; }
};
```

The third constructor takes a constant reference to an object of class Point as an argument and assigns _x and _y, the corresponding values of the provided object.

This type of constructor is important and is known as the copy constructor. It is highly recommended that each class includes such a constructor, even if it is as simple as the one in the example. The copy constructor is called in the following cases:

```
Point Apoint; calls Point::Point()
Point Bpoint(apoint); calls Point::Point(const Point &)
Point Cpoint = Apoint; calls Point::Point(const Point &)
```

The syntax for writing a copy constructor is as follows:

```cpp
classname(const classname & obj)
{
... 
}
```

Here, obj is a reference to the object, which is used to initialize another object. A constructor is called once for global objects and for static objects. For local objects, the constructor is called each time the object declaration is encountered. With the help of constructors, one of the requirements of ADT implementation, namely initialization at definition time, is fulfilled. We still need a mechanism that automatically destroys an object when it gets invalid (for example, because of leaving its scope). Therefore, destructors are defined.

### A.9.2 Destructors

Consider a class `List` for a linked list. The elements of the list are dynamically appended and removed. The constructor helps in creating an initial empty list. However, when we leave the scope of the definition of a list object, we must ensure that the allocated memory is released. We, therefore, define a special method called `destructor`, which is called once for each object at its destruction time.

Destruction of an object takes place when the object leaves its scope of definition or is explicitly destroyed. The latter happens when we dynamically allocate an object and release it when it is no longer needed. Destructors are declared similar to constructors. Thus, they also use the class name, but are prefixed by a tilde (~).

```cpp
class Point
{
    int _x, _y;
public:
    Point()
    {
        _x = _y = 0;
    }
    Point(const int x, const int y)
    {
        _x = x;
        _y = y;
    }
    Point(const Point & from)
    {
        _x = from._x;
        _y = from._y;
    }
// destructor definition
    ~Point() { /* Nothing to do!*/ }
    void setX(const int val);
    void setY(const int val);
    int getX() { return _x; }
    int getY() { return _y; }
}; // end of class declaration
void main(void)
{
    Point appoint; // constructor Point::Point()
    // called automatically.
}; // here destructor for appoint is called automatically
```

Destructors have no arguments, and it is even improper to define one. As they are implicitly called at destruction time, a user has no need to specify actual arguments. Destructors are the complements of constructors. Local objects are created when the respective block is entered, and destroyed when the block is exited from. Hence, the object's respective constructor is called on block entry and the destructor is called on the block exit. Global objects are destroyed when the program terminates. So, their destructor is called automatically on program termination.

### A.9.3 Constructor with Default Arguments

C++ allows a function to assign a parameter a default value when no argument corresponding to that parameter is specified in a call to that function. Program Code A.20 shows a constructor with parameters.

```
PROGRAM CODE A.20

// Constructor with parameters
class Initialize
{
int A;
public:
Initialize(int A = 10) // constructor
{
cout << A;
}
main()
{
Initialize(); // displays default 10
Initialize(5); // displays specified 5
}
}

Output:
10
5
```

All parameters that take default values must appear to the right of those that do not, as follows:

```
Initialize(int A = 10, int B); // incorrect
Initialize(int B, int A = 10); // correct
```

Program Code A.21 is an example to find the volume of a cube.

```
PROGRAM CODE A.21
// To find volume of a cube
#include<iostream.h>
class cube
{
    int x, y, z;
    public:
    cube(int i = 0, int j = 0, int k = 0)
    {
        x = i;
        y = j;
        z = k;
    }
    int volume()
    {
        int volume;
        volume = x * y * z;
        return volume;
    }
}

int main()
{
    cube A(2, 3, 4); cube B;
    cout << A.volume() << endl;
    cout << B.volume() << endl;
    return 0;
}

Output:
24
0
```

Writing a constructor with default parameters is advantageous. For the class Cube if, by default, the constructor is not written, then two constructors are to be defined: one with parameters for object A and other without parameters for object B.

## A.10 INHERITANCE

Inheritance is one of the key features of object-oriented languages. Reusability is achieved through inheritance wherein instead of creating a new class that is similar to the already existing one, we can reuse the existing one. The mechanism of deriving a new class from an existing one is called inheritance.

We can define a general class that has common features related to a set of items. This class is called superclass or base class. A derived class inherits some or all the features of the base class. The superclass can be inherited by other classes, which can add their own unique features to it. These classes are called subclass or derived class. The syntax for a derived class is given as follows:

```
class derived class name: access right Base class name
{
    ...
}
```

The phrase ‘inherits from’ is replaced by a colon in class definition. As an example, let us design a class for 3D points using the already existing class Point. Access right is also referred as visibility mode. The visibility mode is optional and if present may be either public or private. Visibility mode specifies whether the characteristics of the base class are privately or publicly derived.

```cpp
class Point3D:public Point
{
    int _z;
    public:
    Point3D()
    {
        setX(0);
        setY(0);
        _z = 0;
    }
    Point3D(const int x, const int y, const int z)
    {
        setX(x);
        setY(y);
        _z = z;
    }
    ~Point3D() { /* Nothing to do */ }
    int getZ(){return _z;}
    void setZ(const int val){_z = val;}
};
```

### A.10.1 Types of Inheritance

In the definition, the keyword public is used in the first line of the class definition as its signature. This is necessary because C++ distinguishes two types of inheritance, public and private. By default, classes are privately derived from each other. We need to explicitly instruct the compiler to use public inheritance.

The type of inheritance influences the access rights to the elements of the base class. Using public inheritance, everything that is declared private in a base class remains private in the subclass. Similarly, everything that is public remains public. When using private inheritance, the features are quite different as shown in Table A.1.
