This technique is very nice, as the code in ShowDistance is strongly typed, providing all the performance and coding benefits; but both the DLL and the object itself are loaded dynamically, providing a great deal of flexibility to your application.

# Polymorphism with Inheritance

Inheritance, discussed earlier in this chapter, can also be used to enable polymorphism. The idea here is very similar to that of multiple interfaces, as a subclass can always be treated as though it were the data type of the parent class.

> Many people consider the concepts of inheritance and polymorphism to be tightly intertwined. As you have seen, however, it is perfectly possible to use polymorphism without inheritance.

At the moment, both your Encapsulation and Poly classes are implementing a common interface named IShared. You can use polymorphism to interact with objects of either class via that common interface. The same is true if these are child classes based on the same base class through inheritance. To see how this works, in the OOExample project, add a new class named Parent by selecting Add Class and insert the following code:

```
Public MustInherit Class Parent
    Public MustOverride Function DistanceTo(ByVal x As Single, _
        ByVal y As Single) As Single
End Class
```

As described earlier, this is an abstract base class, a class with no implementation of its own. The purpose of an abstract base class is to provide a common base from which other classes can be derived.

To implement polymorphism using inheritance, you do not need to use an abstract base class. Any base class that provides overridable methods (using either the MustOverride or Overridable keywords) will work fine, as all its subclasses are guaranteed to have that same set of methods as part of their interface, and yet the subclasses can provide custom implementation for those methods.

In this example, you are simply defining the DistanceTo method as being a method that must be overridden and implemented by any subclass of Parent. Now you can bring up the Encapsulation class and change it to be a subclass of Parent:

```
Public Class Encapsulation
    Inherits Parent
    Implements IShared
```

You do not need to stop implementing the IShared interface just because you are inheriting from Parent; inheritance and multiple interfaces coexist nicely. You do, however, have to override the DistanceTo method from the Parent class.

The Encapsulation class already has a DistanceTo method with the proper method signature, so you can simply add the Overrides keyword to indicate that this method will override the declaration in the Parent class:

```
Public Overrides Function DistanceTo(ByVal x As Single, _ByVal y As Single) _
As Single Implements IShared.CalculateDistance
```

At this point, the Encapsulation class not only implements the common IShared interface and its own native interface, but also can be treated as though it were of type Parent, as it is a subclass of Parent. You can do the same thing to the Poly class:

```
Public Class Poly
    Inherits Parent
    Implements IShared
    Public Overrides Function DistanceTo( _
```