
```
return (width * height);
}
};
class Triangle: public Shape{
    public:
        Triangle( int a=0, int b=0):Shape(a, b) { }
        int area ()
        {
            cout << "Triangle class area :" <<endl;
            return (width * height / 2);
        }
};
// Main function for the program
int main( )
{
    Shape *shape;
    Rectangle rec(10,7);
    Triangle  tri(10,5);

    // store the address of Rectangle
    shape = &rec;
    // call rectangle area.
    shape->area();

    // store the address of Triangle
    shape = &tri;
    // call triangle area.
    shape->area();

    return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```
Parent class area
Parent class area
```

The reason for the incorrect output is that the call of the function area() is being set once by the compiler as the version defined in the base class. This is called **static resolution** of the function call, or **static linkage** - the function call is fixed before the program is executed. This is also sometimes called **early binding** because the area() function is set during the compilation of the program.

But now, let's make a slight modification in our program and precede the declaration of area() in the Shape class with the keyword **virtual** so that it looks like this:

```
class Shape {

    protected:

        int width, height;

    public:

        Shape( int a=0, int b=0)
        {
            width = a;
            height = b;
        }

        virtual int area()
        {
            cout << "Parent class area :" <<endl;
            return 0;
        }
};
```

After this slight modification, when the previous example code is compiled and executed, it produces the following result:

```
Rectangle class area
Triangle class area
```

This time, the compiler looks at the contents of the pointer instead of its type. Hence, since addresses of objects of tri and rec classes are stored in *shape the respective area() function is called.

## 27. DATA ABSTRACTION

Data abstraction refers to providing only essential information to the outside world and hiding their background details, i.e., to represent the needed information in program without presenting the details.

Data abstraction is a programming (and design) technique that relies on the separation of interface and implementation.

Let's take one real life example of a TV, which you can turn on and off, change the channel, adjust the volume, and add external components such as speakers, VCRs, and DVD players, BUT you do not know its internal details, that is, you do not know how it receives signals over the air or through a cable, how it translates them, and finally displays them on the screen.

Thus, we can say a television clearly separates its internal implementation from its external interface and you can play with its interfaces like the power button, channel changer, and volume control without having zero knowledge of its internals.

In C++, classes provides great level of **data abstraction**. They provide sufficient public methods to the outside world to play with the functionality of the object and to manipulate object data, i.e., state without actually knowing how class has been implemented internally.

For example, your program can make a call to the **sort()** function without knowing what algorithm the function actually uses to sort the given values. In fact, the underlying implementation of the sorting functionality could change between releases of the library, and as long as the interface stays the same, your function call will still work.

In C++, we use **classes** to define our own abstract data types (ADT). You can use the **cout** object of class **ostream** to stream data to standard output like this:

```
```cpp
#include <iostream>

using namespace std;

int main( )
{
    cout << "Hello C++" <<endl;
    return 0;
}
```
```

Here, you don't need to understand how **cout displays** the text on the user's screen. You need to only know the public interface and the underlying implementation of ‘cout’ is free to change.

## Access Labels Enforce Abstraction

In C++, we use access labels to define the abstract interface to the class. A class may contain zero or more access labels:

- Members defined with a public label are accessible to all parts of the program. The data-abstraction view of a type is defined by its public members.
- Members defined with a private label are not accessible to code that uses the class. The private sections hide the implementation from code that uses the type.

There are no restrictions on how often an access label may appear. Each access label specifies the access level of the succeeding member definitions. The specified access level remains in effect until the next access label is encountered or the closing right brace of the class body is seen.

## Benefits of Data Abstraction

Data abstraction provides two important advantages:

- Class internals are protected from inadvertent user-level errors, which might corrupt the state of the object.
- The class implementation may evolve over time in response to changing requirements or bug reports without requiring change in user-level code.

By defining data members only in the private section of the class, the class author is free to make changes in the data. If the implementation changes, only the class code needs to be examined to see what affect the change may have. If data is public, then any function that directly access the data members of the old representation might be broken.

## Data Abstraction Example

Any C++ program where you implement a class with public and private members is an example of data abstraction. Consider the following example:

```
```cpp
#include <iostream>

using namespace std;

class Adder{
    public:
        // constructor
        Adder(int i = 0)
```
```

```
```cpp
{
    total = i;
}

// interface to outside world
void addNum(int number)
{
    total += number;
}

// interface to outside world
int getTotal()
{
    return total;
};

private:
    // hidden data from outside world
    int total;
};

int main( )
{
    Adder a;

    a.addNum(10);
    a.addNum(20);
    a.addNum(30);

    cout << "Total " << a.getTotal() << endl;
    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
Total 60
```
```

Above class adds numbers together, and returns the sum. The public members **addNum** and **getTotal** are the interfaces to the outside world and a user needs to know them to use the class. The private member **total** is something that the user doesn't need to know about, but is needed for the class to operate properly.

defined after the public specifier are accessible by all other functions in your program.

Making one class a friend of another, exposes the implementation details and reduces encapsulation. The ideal is to keep as many of the details of each class hidden from all other classes as possible.

## Data Encapsulation Example

Any C++ program where you implement a class with public and private members is an example of data encapsulation and data abstraction. Consider the following example:

```
```cpp
#include <iostream>

using namespace std;

class Adder{
   public:

      // constructor
      Adder(int i = 0)
      {
         total = i;
      }

      // interface to outside world
      void addNum(int number)
      {
         total += number;
      }

      // interface to outside world
      int getTotal()
      {
         return total;
      };
   private:

      // hidden data from outside world
      int total;
};
int main( )
{
```
```

## 29. INTERFACES

An interface describes the behavior or capabilities of a C++ class without committing to a particular implementation of that class.

The C++ interfaces are implemented using **abstract classes** and these abstract classes should not be confused with data abstraction which is a concept of keeping implementation details separate from associated data.

A class is made abstract by declaring at least one of its functions as **pure virtual** function. A pure virtual function is specified by placing "= 0" in its declaration as follows:

```
```cpp
class Box
{
    public:

        // pure virtual function
        virtual double getVolume() = 0;
    private:

        double length;      // Length of a box
        double breadth;     // Breadth of a box
        double height;      // Height of a box
};
```
```

The purpose of an **abstract class** (often referred to as an ABC) is to provide an appropriate base class from which other classes can inherit. Abstract classes cannot be used to instantiate objects and serves only as an **interface**. Attempting to instantiate an object of an abstract class causes a compilation error.

Thus, if a subclass of an ABC needs to be instantiated, it has to implement each of the virtual functions, which means that it supports the interface declared by the ABC. Failure to override a pure virtual function in a derived class, then attempting to instantiate objects of that class, is a compilation error.

Classes that can be used to instantiate objects are called **concrete classes**.

## Abstract Class Example

Consider the following example where parent class provides an interface to the base class to implement a function called **getArea()**:

```
```cpp
#include <iostream>
```

![](img/7976f323fd1a5c8774f95fbf029a106f_245_0.png)
