
```csharp
}
}
```

The following is the output from the code:

```text
The Length of the figure is: 5.4
The Width of the figure is: 3.2
The Area of the figure is: 17.28
```

The class member variables *width* and *length* have been declared as *public*, which means that we are able to access them from the *Main()* function after creating an instance of the class. We have created an instance of the *Figure* class and given it the name *f*.

The *CalculateArea()* and *Show()* member functions are also able to access these member variables without using an instance of the class. The *Show()* member function has also been declared as public, meaning that we are able to access it from the *Main()* function using an instance of the class.

## Protected Access Specifier

This type of access specifier makes it possible for a child class to access the member functions and member variables that have been defined in the base class. This way, it is easier to implement inheritance. This will be discussed in inheritance.

## Internal Access Specifier

This type of access specifier allows a class to expose its member functions and member variables to the other objects and functions in the current assembly. This means that any member that has been created using the internal access specifier is accessible from any class or method that has been defined within the application where the member has been defined. This is demonstrated in the following example:

```csharp
using System;

namespace AccesserApplication {

  class Figure {

    // The member variables
    internal double width;
    internal double length;
    double CalculateArea() {
return length * width;
}
public void Show() {
    Console.WriteLine("The Length of the figure is: {0}", length);
    Console.WriteLine("The Width of the figure is: {0}", width);
    Console.WriteLine("The Area of the figure is: {0}", CalculateArea());
}
}//end the class Figure

class RunFigure {
    static void Main(string[] args) {
        Figure f = new Figure();
        f.length = 6.5;
        f.width = 4.8;
        f.Show();
        Console.ReadLine();
    }
}
}
```

The code should return the following result:

```text
The Length of the figure is: 6.5
The Width of the figure is: 4.8
The Area of the figure is: 31.2
```

## Chapter 14: Inheritance

With inheritance, it is possible for a programmer to define one class in terms of another class. This also makes it possible for us to reuse code and shorten the time taken to implement an application.

During the creation of a class, instead of having to create completely new member functions and data members, the programmer is able to designate that the new class inherits the members of an already existing class. The *base class* is the name for the existing class while the new class is known as the *derived class*.

Inheritance is simply an implementation of IS-A relationship<sup>[36]</sup>. For example, Cow is a Mammal.

It is possible for a class to inherit from more than one class or interfaces, meaning that it can inherit data and functions from many base interfaces or classes. The following example demonstrates the concept of the base and derived class:

```csharp
using System;

namespace InheritanceApp {
    class Figure {
        public void setWidth(int wid) {
            width = wid;
        }
        public void setHeight(int heig) {
            height = heig;
        }
        protected int width;
        protected int height;
    }
    // A Derived class
    class Rectangle: Figure {
        public int calculateArea() {
return (width * height);
}
}
class TestInheritance {
    static void Main(string[] args) {
        Rectangle R = new Rectangle();
        R.setWidth(6);
        R.setHeight(8);
        // Print the rectangle's area.
        Console.WriteLine("The area is: {0}", R.calculateArea());
        Console.ReadKey();
    }
}
}
```

The code should return the following output:

```text
The area is: 48
```

We have defined the *Figure* class with two properties namely *width* and *height*. This class also has two methods, *setWidth()* and *setHeight()*. We have then defined a class named *Rectangle*. Notice the syntax we have used to create this class:

```csharp
class Rectangle: Figure {
```

The use of the full colon signals that the Rectangle class is inheriting the Figure class. The Rectangle class only has one method, the *calculateArea()* method. However, since it has inherited the Figure class, it means that it has all the properties of the Figure class, like the width and the height.

We have then created the *TestInheritance* class. Within the method Main(), an instance of the Rectangle class has been created and given it the name R. We have used this instance to access the properties that have been defined in both the Rectangle and the Figure classes. That is how powerful inheritance is!

### Base Class Initialization

The derived class inherits the member methods and member variables defined in the

```csharp
cost = CalculateArea() * 120;
return cost;
}

public void Show() {
    base.Show();
    Console.WriteLine("The total cost for the carpet is: {0}",
CalculateCost());
}
}
}
class RunObject {
    static void Main(string[] args) {
        Carpet c = new Carpet(7.5, 9.5);
        c.Show();
        Console.ReadLine();
    }
}
}
}
```

The code will return the following output:

```text
The Width of the figure is: 9.5
The Length of the figure is: 7.5
The Area of the figure is: 71.25
The total cost for the carpet is: 8550
```

### Multiple Inheritance

Multiple inheritance is not supported in C#. However, with interfaces, it is possible
for us to implement multiple inheritance. Consider the following example:

```csharp
using System;
namespace InheritanceApp {
    class Object {
        public void setWidth(int wid) {
            width = wid;
}
public void setHeight(int heig) {
    height = heig;
}
protected int width;
protected int height;
}

// PaintCost for the Base class
public interface PaintCost {
    int calculateCost(int area);
}
// The derived class
class Board : Object, PaintCost {
    public int calculateArea() {
        return (width * height);
    }
    public int calculateCost(int area) {
        return area * 120;
    }
}
class InheritanceTester {
    static void Main(string[] args) {
        Board B = new Board();
        int area;
        B.setWidth(5);
        B.setHeight(7);

    area = B.calculateArea();
    // Show the area of the object
    Console.WriteLine("The area of the object is: {0}", B.calculateArea());
            Console.WriteLine("The total printing cost is: ${0}" ,
    B.calculateCost(area));
    Console.ReadKey();
    }
    }
}
```

The code gives the following output:

```text
The area of the object is: 35
The total printing cost is: $4200
```

## Chapter 15: Polymorphism

Polymorphism[37] is a term that means taking many forms. In programming, it is expressed as **“one interface, many functions”**. Polymorphism can take two forms, static or dynamic.

For the case of static dynamism, response to the function is determined during compile time. In dynamic polymorphism, response to the function is determined during runtime.

### Static Polymorphism

As stated above, the response to a function in this type of polymorphism is determined during compile time. The process of linking a function to an object during compile time is known as *early binding*. It is also known as *static binding*. In C#, static polymorphism can be implemented in two ways:

- Function overloading
- Operator overloading

### Function Overloading

It is possible for us to have multiple definitions for the same function name within one scope. The differences between these functions are implemented by types or the number of arguments that the functions take. Function declarations cannot be overloaded by differing the return types only.

**The following example demonstrates how to overload a function in C#:**

```csharp
using System;

namespace PolymorphismApp {
    class DisplayData {
        void display(int x) {
            Console.WriteLine("Printing an int value: {0}", x );
        }

        void display(double y) {
```
