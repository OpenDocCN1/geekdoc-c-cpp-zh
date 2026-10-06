The explicit interface implementation do introduce some extra work for a developer, however, it provides a clear vision so that you can make sure the right function can be invoked. for example, there are two interfaces that have defined the same property, and the implementation of one of those properties was accidentally forgotten. The discovery of this kind of bug will most likely be delayed until runtime.

Interfaces in F# also support inheritance. The next task is to define a new interface, inherit from I2Location, and add an extra method GetDistance. Listing 2–49 shows the sample code.

# LISTING 2-49 Defining an interface and inheritance

```
// define a base interface
type I2Location =
    abstract member X : float with get, set
    abstract member Y : float with get, set

// define an interface that inherits from I2Location
type IPoint2D =
    inherit I2Location
    abstract member GetDistance : Point2D -> float
```

Compared with the code in Listing 2-49, the code in Listing 2-50 reverses the order of IPoint2D and I2Location. This is not a problem for C#, but in F# you have to use the keyword to resolve the type reference problem. The Point2D interface has a function that takes Point2D as a parameter, while the Point2D interface is defined next. Because F# resolves the type and symbols from top to bottom and from left to right, there will be a compile error unless the keyword is applied.

# LISTING 2-50 Implementing interfaces with an inheritance relationship

```
// define an IPoint2D interface
// need the keyword to resolve the type-resolution problem
type IPoint2D =
    inherit I2Location

// this function takes I2Location as a parameter, which is defined below
    abstract member GetDistance : I2Location -> float

// define a 2D location interface
    abstract member X : float with get, set
and I2Location =
    abstract member Y : float with get, set
```

```
// define a Point2D class with a parameterized primary constructor
type Point2D(xValue:double, yValue:double) define this=
    // field x
    let mutable x = xValue
```