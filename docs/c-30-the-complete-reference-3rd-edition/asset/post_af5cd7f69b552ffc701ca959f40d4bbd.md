
```csharp
// Constructor.
public Triangle(string s, double w, double h) : base(w, h) {
    Style = s;
}

// Construct an isosceles triangle.
public Triangle(double x) : base(x) {
    Style = "isosceles";
}

// Return area of triangle.
public double Area() {
    return Width * Height / 2;
}

// Display a triangle's style.
public void ShowStyle() {
    Console.WriteLine("Triangle is " + Style);
}

// Extend Triangle.
class ColorTriangle : Triangle {
    string color;

    public ColorTriangle(string c, string s,
                         double w, double h) : base(s, w, h) {
        color = c;
    }

    // Display the color.
    public void ShowColor() {
        Console.WriteLine("Color is " + color);
    }
}

class Shapes6 {
    static void Main() {
        ColorTriangle t1 =
            new ColorTriangle("Blue", "right", 8.0, 12.0);
        ColorTriangle t2 =
            new ColorTriangle("Red", "isosceles", 2.0, 2.0);

        Console.WriteLine("Info for t1: ");
        t1.ShowStyle();
        t1.ShowDim();
        t1.ShowColor();
        Console.WriteLine("Area is " + t1.Area());

        Console.WriteLine();

        Console.WriteLine("Info for t2: ");
        t2.ShowStyle();
        t2.ShowDim();
        t2.ShowColor();
        Console.WriteLine("Area is " + t2.Area());
    }
}
```

The output of this program is shown here:

```text
Info for t1:
Triangle is right
Width and height are 8 and 12
Color is Blue
Area is 48

Info for t2:
Triangle is isosceles
Width and height are 2 and 2
Color is Red
Area is 2
```

Because of inheritance, ColorTriangle can make use of the previously defined classes of Triangle and TwoDShape, adding only the extra information it needs for its own, specific application. This is part of the value of inheritance; it allows the reuse of code.

This example illustrates one other important point: base always refers to the constructor in the closest base class. The base in ColorTriangle calls the constructor in Triangle. The base in Triangle calls the constructor in TwoDShape. In a class hierarchy, if a base class constructor requires parameters, then all derived classes must pass those parameters "up the line." This is true whether or not a derived class needs parameters of its own.

## When Are Constructors Called?

In the foregoing discussion of inheritance and class hierarchies, an important question may have occurred to you: When a derived class object is created, whose constructor is executed first? The one in the derived class or the one defined by the base class? For example, given a derived class called B and a base class called A, is A's constructor called before B's, or vice versa? The answer is that in a class hierarchy, constructors are called in order of derivation, from base class to derived class. Furthermore, this order is the same whether or not base is used. If base is not used, then the default (parameterless) constructor of each base class will be executed. The following program illustrates the order of constructor execution:

```csharp
// Demonstrate when constructors are called.
using System;

// Create a base class.
class A {
    public A() {
        Console.WriteLine("Constructing A.");
    }
}

// Create a class derived from A.
class B : A {
    public B() {
        Console.WriteLine("Constructing B.");
    }
}

// Create a class derived from B.
class C : B {
    public C() {
        Console.WriteLine("Constructing C.");
    }
}

class OrderOfConstruction {
    static void Main() {
        C c = new C();
    }
}
```

The output from this program is shown here:

```text
Constructing A.
Constructing B.
Constructing C.
```

As you can see, the constructors are called in order of derivation.

If you think about it, it makes sense that constructors are executed in order of derivation. Because a base class has no knowledge of any derived class, any initialization it needs to perform is separate from and possibly prerequisite to any initialization performed by the derived class. Therefore, it must be executed first.

## Base Class References and Derived Objects

As you know, C# is a strongly typed language. Aside from the standard conversions and automatic promotions that apply to its value types, type compatibility is strictly enforced. Therefore, a reference variable for one class type cannot normally refer to an object of another class type. For example, consider the following program that declares two classes that are identical in their composition:

```csharp
// This program will not compile.

class X {
    int a;
    public X(int i) { a = i; }
}

class Y {
    int a;
    public Y(int i) { a = i; }
}

class IncompatibleRef {
    static void Main() {
        X x = new X(10);
        X x2;
        Y y = new Y(5);

        x2 = x; // OK, both of same type

        x2 = y; // Error, not of same type
    }
}
```

Here, even though class X and class Y are physically the same, it is not possible to assign a reference of type Y to a variable of type X because they have different types. Therefore, this line is incorrect because it causes a compile-time type mismatch:

```csharp
x2 = y; // Error, not of same type
```

In general, an object reference variable can refer only to objects of its type.

There is, however, an important exception to C#'s strict type enforcement. A reference variable of a base class can be assigned a reference to an object of any class derived from that base class. This is legal because an instance of a derived type encapsulates an instance of the base type. Thus, a base class reference can refer to it. Here is an example:

```csharp
// A base class reference can refer to a derived class object.

using System;

class X {
    public int a;

    public X(int i) {
        a = i;
    }
}

class Y : X {
    public int b;

    public Y(int i, int j) : base(i) {
        b = j;
    }
}

class BaseRef {
    static void Main() {
        X x = new X(10);
        X x2;
        Y y = new Y(5, 6);

        x2 = x; // OK, both of same type
        Console.WriteLine("x2.a: " + x2.a);

        x2 = y; // OK because Y is derived from X
        Console.WriteLine("x2.a: " + x2.a);

        // X references know only about X members
        x2.a = 19; // OK
        // x2.b = 27; // Error, X doesn't have a b member
    }
}
```

In this program, Y is derived from X. Now, the assignment

```csharp
x2 = y; // OK because Y is derived from X
```

is permissible because a base class reference, x2 in this case, can refer to a derived class object (which is the object referred to by y).

It is important to understand that it is the type of the reference variable—not the type of the object that it refers to—that determines what members can be accessed. That is, when a reference to a derived class object is assigned to a base class reference variable, you will have access only to those parts of the object defined by the base class. This is why you can't access b even when it refers to a Y object. This makes sense because the base class has no knowledge of what a derived class adds to it. This is why the last line of code in the program is commented out.

Although the preceding discussion may seem a bit esoteric, it has some important practical applications. One is described here. The other is discussed later in this chapter, when virtual methods are covered.

An important place where derived class references are assigned to base class variables is when constructors are called in a class hierarchy. As you know, it is common for a class to define a constructor that takes an object of its class as a parameter. This allows the class to construct a copy of an object. Classes derived from such a class can take advantage of this feature. For example, consider the following versions of TwoDShape and Triangle. Both add constructors that take an object as a parameter.

```csharp
// Pass a derived class reference to a base class reference.

using System;

class TwoDShape {
    double pri_width;
    double pri_height;

    // Default constructor.
    public TwoDShape() {
        Width = Height = 0.0;
    }

    // Constructor for TwoDShape.
    public TwoDShape(double w, double h) {
        Width = w;
        Height = h;
    }

    // Construct object with equal width and height.
    public TwoDShape(double x) {
        Width = Height = x;
    }
}
```
