When a class declaration contains a pure virtual function, you can't create an object of that class. The idea is that classes with pure virtual functions exist solely to serve as base classes. For a class to be a genuine ABC, it has to have at least one pure virtual function. It is the = 0 in the prototype that makes a virtual function a pure virtual function. In the case of the Area() method, the function has no definition, but C++ allows even a pure virtual function to have a definition. For example, perhaps all the base methods are like Move() in that they can be defined for the base class, but you still need to make the class abstract. You could then make the prototype virtual:

```
```cpp
void Move(int nx, ny) = 0;
```
```

This makes the base class abstract. But then you could still provide a definition in the implementation file:

```
```cpp
void BaseEllipse::Move(int nx, ny)  { x = nx;  y = ny; }
```
```

In short, the = 0 in the prototype indicates that the class is an abstract base class and that the class doesn't necessarily have to define the function.

Now you can derive the Ellipse class and Circle class from the BaseEllipse class, adding the members needed to complete each class. One point to note is that the Circle class always represents circles, whereas the Ellipse class represents ellipses that can also be circles. However, an Ellipse class circle can be recaled to a non-circle, whereas a Circle class circle must remain a circle.

A program using these classes would be able to create Ellipse objects and Circle objects but no BaseEllipse objects. Because Circle and Ellipse objects have the same base class, a collection of such objects can be managed with an array of BaseEllipse pointers. Classes such as Circle and Ellipse are sometimes termed concrete classes to indicate that you can create objects of those types.

In short, an ABC describes an interface that uses a least one pure virtual function, and classes derived from an ABC use regular virtual functions to implement the interface in terms of the properties of the particular derived class.

# ## Applying the ABC Concept

You'd probably like to see a complete example of an ABC, so let's apply the concept to representing the Brass and BrassPlus accounts, starting with an ABC called AcctABC. This class should contain all methods and data members that are common to both the Brass and the BrassPlus classes. The methods that are to work differently for the BrassPlus class than they do for the Brass class should be declared as virtual functions. At least one virtual function should be a pure virtual function in order to make the AcctABC class abstract.

Listing 13.11 is a header file that declares the AcctABC class (an ABC) and the Brass and BrassPlus classes (both concrete classes). To facilitate derived class access to base class data, AcctABC provides some protected methods. Recall that protected methods are methods that derived-class methods can call but that are not part of the public interface for derived-class objects. AcctABC also provides a protected member function to handle the