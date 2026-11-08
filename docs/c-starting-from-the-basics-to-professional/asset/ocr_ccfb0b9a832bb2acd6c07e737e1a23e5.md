```
```cpp
bool hasLargerVolumeThan(Cube cube); // Compare volume of a cube with another
private:
    double m_side;
};
```
```

With this definition for Cube, Ex12_04.cpp will not compile. The compiler never uses a constructor declared as explicit for an implicit conversion, so it can be used only explicitly in the program. By using the explicit keyword with constructors that have a single parameter, you prevent implicit conversions from the parameter type to the class type. The hasLargerVolumeThan() member only accepts a Cube object as an argument, so calling it with an argument of type double does not compile.

> > **Tip**  Implicit conversions may lead to confusing code; most of the time it becomes far more obvious why code compiles and what it does if you use explicit conversions. By default, you should therefore declare single-argument constructors as explicit (note that this includes constructors with multiple parameters where at least all but the first have default values); omit explicit only if implicit type conversions are truly desirable.

> > **Note**  While less common, any constructor that is not a single-argument constructor can be marked as explicit as well. Suppose processBox() is a function with a single parameter of type Box or const Box&, then in modern C++ the expression processBox({1.0, 2.0, 3.0}) is a valid shorthand for processBox(Box{1.0, 2.0, 3.0}). To prohibit such shorthand notations, and thus to force the explicit mention of the Box type upon each construction, you can mark the ternary Box(double, double, double) constructor as explicit.

# Delegating Constructors

A class can have several constructors that provide different ways of creating an object. The code for one constructor can call another of the same class in the initialization list. This can avoid repeating the same code in several constructors. Here’s a simple illustration of this using the Box class:

```
```cpp
class Box
{
public:
    Box(double length, double width, double height);
    explicit Box(double side);   // Constructor for a cube (explicit!)
    Box() = default;             // Defaulted default constructor

    double volume();             // Function to calculate the volume of a box

private:
    double m_length{1.0};
    double m_width {1.0};
    double m_height{1.0};
};
```
```