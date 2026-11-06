
*copy assignment operator, move assignment operator or destructor by* following the special member function’s prototype with `= default`. This is useful, for example, when you explicitly define a constructor for a class and still want the compiler to generate a default constructor as well—in that case, add the following declaration to your class definition:

```cpp
ClassName() = default;
```

## 12.4.7 C++11: `final` Member Functions and Classes

Prior to C++11, a derived class could override *any* of its base class’s `virtual` functions. In C++11, a base-class `virtual` function that’s declared `final` in its prototype, as in

```cpp
virtual someFunction(parameters) final;
```

*cannot* be overridden in any derived class—this guarantees that the base class’s `final` member function definition will be used by all base-class objects and by all objects of the base class’s direct *and* indirect derived classes. Similarly, prior to C++11, *any* existing class could be used as a base class in a hierarchy. As of C++11, you can declare a class as `final` to prevent it from being used as a base class, as in

```cpp
class MyClass final { // this class cannot be a base class
    // class body
};
```

Attempting to override a `final` member function or inherit from a `final` base class results in a compilation error.

## 12.5 Type Fields and `switch` Statements

One way to determine an object’s type is to use a `switch` statement to check the value of a field in the object. This allows us to distinguish among object types, then invoke an appropriate action for a particular object, similar to what you can do with polymorphism. For example, in a hierarchy of shapes, if each shape object has a `shapeType` attribute, a `switch` could check the object’s `shapeType` to determine which `toString` function to call.

Using `switch` logic exposes programs to a variety of potential problems. For example, you might forget to include a type test when one is warranted, or might forget to test all possible cases in a `switch` statement. When modifying a `switch`-based system by adding new types, you might forget to insert the new cases in *all* relevant `switch` statements. Every addition or deletion of a class requires the modification of every associated `switch` statement in the system; tracking these changes can be time consuming and error prone.

### Software Engineering Observation 12.6

*Polymorphic programming can eliminate the need for `switch` logic. By using the polymorphism mechanism to perform the equivalent logic, you can avoid the kinds of errors typically associated with `switch` logic.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1583_0.png)

### Software Engineering Observation 12.7

*An interesting consequence of using polymorphism is that programs take on a simplified appearance. They contain less branching logic and simpler sequential code.*

## 12.6 Abstract Classes and Pure `virtual` Functions

When we think of a class as a type, we assume that programs will create objects of that type. However, there are cases in which it’s useful to define *classes from which you never intend to instantiate any objects*. Such classes are called **abstract classes**. Because these classes normally are used as base classes in inheritance hierarchies, we refer to them as **abstract base classes**. These classes cannot be used to instantiate objects, because, as we’ll soon see, abstract classes are *incomplete*—derived classes must define the “missing pieces” before objects of these classes can be instantiated. We build programs with abstract classes in Section 12.7.

An abstract class is a base class from which other classes can inherit. Classes that can be used to instantiate objects are called **concrete classes**. Such classes define or inherit implementations for *every* member function they declare. A good example of this is the shape hierarchy in Fig. 11.3, which begins with abstract base class `Shape`. We could have an *abstract* base class `TwoDimensionalShape` and derive such *concrete* classes as `Circle`, `Square` and `Triangle`. We could also have an *abstract* base class `ThreeDimensionalShape` and derive such *concrete* classes as `Cube`, `Sphere` and `Tetrahedron`. Abstract base classes are too generic to define real objects; we need to be *more specific* before we can think of instantiating objects. For example, if someone tells you to “draw the two-dimensional shape,” what shape would you draw? Concrete classes provide the *specifics* that make it possible to instantiate objects.

### 12.6.1 Pure `virtual` Functions

A class is made *abstract* by declaring one or more of its `virtual` functions to be “pure.” A **pure `virtual` function** is specified by placing “`=0`” in its declaration, as in

```cpp
virtual void draw() const = 0; // pure virtual function
```

The “`=0`” is a **pure specifier**. Pure `virtual` functions do *not* provide implementations. Each *concrete* derived class *must override all* base-class pure `virtual` functions with concrete implementations of those functions; otherwise, the derived class is also abstract.

The difference between a `virtual` function and a pure `virtual` function is that a `virtual` function *has* an implementation and gives the derived class the *option* of overriding the function; by contrast, a pure `virtual` function does *not* have an implementation and *requires* the derived class to override the function for that derived class to be *concrete*; otherwise the derived class remains *abstract*.

Pure `virtual` functions are used when it *does not* make sense for the base class to have an implementation of a function, but you want to force all concrete derived classes to implement the function. Returning to our earlier example of space objects, it does not make sense for the base class `SpaceObject` to have an implementation for function `draw` (as there’s no way to draw a generic space object without having specific information about what type of space object is being drawn). An example of a function that would be defined as `virtual` (and not pure `virtual`) would be one that returns a name for the object. We can name a generic `SpaceObject` (for instance, as "space object"), so a default implementation for this function can be provided, and the function does not need to be *pure* `virtual`. The function is still declared `virtual`, however, because it’s expected that derived classes will override this function to provide *more specific* names for the derived-class objects.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1586_0.png)

### Software Engineering Observation 12.8

*An abstract class defines a common public interface for the various classes that derive from it in a class hierarchy. An abstract class contains one or more pure* `virtual` *functions that concrete derived classes must override.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1587_0.png)

### Common Programming Error 12.2

Failure to override a pure `virtual` function in a derived class makes that class abstract. Attempting to instantiate an object of an abstract class causes a compilation error.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1587_1.png)

### Software Engineering Observation 12.9

An abstract class has at least one pure `virtual` function. An abstract class also can have data members and concrete functions (including constructors and destructors), which are subject to the normal rules of inheritance by derived classes.

Although we cannot instantiate objects of an abstract base class, we can use the abstract base class to declare pointers and references that can refer to objects of any concrete classes derived from the abstract class. Programs typically use such pointers and references to manipulate derived-class objects polymorphically.

### 12.6.2 Device Drivers: Polymorphism in Operating Systems

Polymorphism is particularly effective for implementing *layered software systems*. In operating systems, for example, each type of physical device could operate quite differently from the others. Even so, commands to *read* or *write* data from and to devices, respectively, may have a certain uniformity. The *write* message sent to a *device-driver* object needs to be interpreted specifically in the context of that device driver and how that device driver manipulates devices of a specific type. However, the *write* call itself really is no different from the *write* to any other device in the system—place some number of *bytes* from memory onto that device. An object-oriented operating system could use an abstract base class to provide an interface appropriate for all device drivers. Then, through inheritance from that abstract base class, derived classes are formed that all operate similarly. The capabilities (i.e., the `public` functions) offered by the device drivers are provided as pure `virtual` functions in the abstract base class. The implementations of these pure `virtual` functions are provided in the derived classes that correspond to the specific types of device drivers. This architecture also allows new devices to be *added* to a system easily. The user can just plug in the device and install its new device driver. The operating system “talks” to this new device through its device driver, which has the same `public` member functions as all other device drivers—those defined in the device driver abstract base class.
