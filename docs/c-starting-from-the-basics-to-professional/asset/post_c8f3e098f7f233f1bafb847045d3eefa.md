
## CHAPTER 13: OPERATOR OVERLOADING

**Caution** The somewhat clumsy workaround we used in this section to deal with invalid indexes to a subscript operator—returning a non-const reference to a special “null object”—has one critical flaw. Perhaps you can already guess what this is? Hint: If supplied with an invalid index, the `operator[]()` function returns a non-const reference to `nullBox`. Exactly. The fact that this reference is non-const implies that there is nothing to prevent the caller from modifying `nullBox`. In general, allowing the user to modify the objects that are accessed through the operator is exactly what we set out to do. But for the special `nullBox` object, this exposes a grave risk. It allows a careless caller to assign a non-null value to the `nullBox` pointer, which would essentially cripple the subscript operator! The following illustrates how things could go wrong:

```cpp
Truckload load(std::make_shared<Box>(1, 2, 3));    // Create load with single box
...
load[10] = std::make_shared<Box>(6, 6, 6);         // Oops: assigning to nullBox...
...
auto secondBox = load[100];                        // Access nonexistent Box...
if (secondBox)                                     // nullBox is no longer null
{
    std::cout << secondBox->volume() << std::endl; // Prints 216 (6*6*6)
}
```

As this example shows, one accidental assignment to a nonexistent element causes unexpected and undesirable behavior. The Truckload now appears to have a box with dimensions {6, 6, 6} at index 100. (Note that this will even break the subscript operator for all Truckload objects all at once. Because `nullBox` is a static member of Truckload, it is shared between all objects of this class.)

Because of this dangerous loophole, you should never use the technique we used here in real programs. In Chapter 16 you will learn about a more appropriate mechanism for dealing with invalid function arguments: exceptions. Exceptions will allow you to return from a function without having to invent a return value.

### Function Objects

A function object or functor is an object of a class that overloads the function call operator, which is `operator()`. A function object can be passed as an argument, thus providing a powerful way to pass functions around. We will dig much deeper into this topic in Chapter 19. Here we'll just quickly show you how to overload the function call operator and give you a first idea how function objects work with a basic example.

Suppose we define a ComputeVolume class like this:

```cpp
class ComputeVolume
{
public:
    double operator()(double x, double y, double z) const { return x * y * z; }
};
```

The function call operator in a class looks like a misprint. It is `operator()`. But with this operator overloaded in place, you can use a ComputeVolume object to compute a volume.

```cpp
ComputeVolume computeVolume;                 // Create a functor
double roomVolume { computeVolume(16, 12, 8.5) }; // Room volume in cubic feet
```

The `computeVolume` object represents a function, one that can be called using its function call operator. The value in the braced initializer for `roomVolume` is the result of calling `operator()` for the `computeVolume` object, so the expression is equivalent to `computeVolume.operator()(16, 12, 8.5)`. Because function call operators often do not modify any member variables of the functor object, they are often defined as const member functions.

Of course, you can define more than one overload of the `operator()` function in a class:

```cpp
class ComputeVolume
{
public:
    double operator()(double x, double y, double z) const { return x*y*z; }
    double operator()(const Box& box) const { return box.volume(); }
};
```

Now a ComputeVolume object can return the volume of a Box object as well:

```cpp
Box box{1.0, 2.0, 3.0};
std::cout << "The volume of the box is " << computeVolume(box) << std::endl;
```

Naturally, this example will not convince you at all yet of the usefulness of function objects. But what if we told you that you have already encountered some very useful function objects? Remember `createUniformPseudoRandomNumberGenerator()`? That function created and used no less than four different function objects. The random device, the pseudo-random number generator, the uniform distribution, and the `std::bind()`—all these were objects that represent a function. The pseudo-random number generator, for instance, represents a function that returns a different number each time it is invoked. To accomplish this, the object stores certain data inside its member variables. This data is first initialized based on a given seed value (from a truly random source, ideally), and then updated each time a new number is generated (to get it ready for generating the next number). This is not possible using a regular function, as a regular function cannot store data. At best a regular function can use global or static variables, but these do not suffice in general (especially not in multithreaded applications). You need a function object for this!

If you are still not convinced that representing callable functions as objects is a powerful concept, or if it's all still a bit too abstract, we refer you to Chapters 19 and 20. In Chapter 19 you will learn all about the versatility of function objects (and in particular, lambda expressions), and in Chapter 20 you'll see just how powerful they are in combination with Standard Library algorithms and containers.

> **Note:** Unlike most operators, function call operators must be overloaded as member functions. They cannot be defined as regular functions. The function call operator is also the only operator that can have as many parameters as you want and that can have default arguments.

### Overloading Type Conversions

You can define an operator function as a class member to convert from the class type to another type. The type you're converting to can be a fundamental type or a class type. Operator functions that are conversions for objects of an arbitrary class, MyClass, are of this form:

```cpp
class MyClass
{
public:
    operator OtherType() const;        // Conversion from MyClass to OtherType
    // Rest of MyClass class definition...
};
```

OtherType is the destination type for the conversion. Note that no return type is specified because the target type is always implicit in the function name, so here the function must return an OtherType object. As an example, you might want to define a conversion from type Box to type double. For application reasons, you could decide that the result of this conversion would be the volume of the Box object. You could define this as follows:

```cpp
class Box
{
public:
    operator double() const { return volume(); }

    // Rest of Box class definition...
};
```

The operator function would then be called if you wrote this:

```cpp
Box box {1.0, 2.0, 3.0};
double boxVolume{ box };      // Calls conversion operator
```

This causes an implicit conversion to be inserted by the compiler. You could call the operator function explicitly with this statement:

```cpp
double total { 10.0 + static_cast<double>(box) };
```

You can prevent implicit calls of a conversion operator function by specifying it as explicit in the class. In the Box class you could, and probably should, write this:

```cpp
explicit operator double() const { return volume(); }
```

Now the compiler will not use this member for implicit conversions to type double.

> **Note:** Unlike most operators, conversion operators must be overloaded as member functions. They cannot be defined as regular functions. They are also the only operators where the `operator` keyword is not preceded by a return type (instead, the return type comes after the keyword).

### Potential Ambiguities with Conversions

When you implement conversion operators for a class, it is possible to create ambiguities that will cause compiler errors. You have seen that a constructor can also effectively implement a conversion—a conversion from type Type1 to type Type2 can be implemented by including a constructor in class Type2 with this declaration:

```cpp
Type2(const Type1& theObject);    // Constructor converting Type1 to Type2
```

This can conflict with this conversion operator in the Type1 class:

```cpp
operator Type2() const;          // Conversion from type Type1 to Type2
```

The compiler will not be able to decide which constructor or conversion operator function to use when an implicit conversion is required. To remove the ambiguity, declare either or both members as explicit.

### Overloading the Assignment Operator

You have already encountered several instances where one object of a nonfundamental type is seemingly overwritten by another using an assignment operator, like so:

```cpp
Box oneBox{1, 2, 3};
Box otherBox{4, 5, 6};
...
oneBox = otherBox;
...
std::cout << oneBox.volume() << std::endl;    // Outputs 120 (= 4 x 5 x 6)
```

But how exactly does this work? And how do you support this for your own classes?

You know that the compiler (sometimes) implicitly generates default constructors, copy constructors, and destructors. This is not all the compiler provides, though. Similar to a default copy constructor, a compiler also generates a default copy assignment operator. For Box, this operator has the following prototype:

```cpp
class Box
{
public:
    Box& operator=(const Box& rightHandSide);
    ...
};
```

Like a default copy constructor, the default copy assignment operator simply copies all the member variables of a class one by one (in the order they are declared in the class definition). You can override this default behavior by supplying a user-defined assignment operator, as we'll discuss next.

> **Note:** The assignment operator cannot be defined as a regular function. It is the only binary operator that must always be overloaded as a class member function.
