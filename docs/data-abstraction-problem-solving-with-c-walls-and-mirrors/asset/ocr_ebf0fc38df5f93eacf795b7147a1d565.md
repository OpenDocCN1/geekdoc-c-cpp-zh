# C++ INTERLUDE 1 C++ Classes

```
PlainBox<ItemType>():
PlainBox<ItemType>::setItem(const item);
boxColor = theColor;
}// end constructor
template<class ItemType>
Color ToyBox<ItemType>::getColor() const
{
    return boxColor;
}// getColor
```

Inheritance enables you to reuse software components like PlainBox, but it can use a PlainBox or ToyBox class does not inherit the constructors from PlainBox or method to initialize the private data fields in PlainBox. For the default constructor of our base class, we place the statement

PlainBox<ItemType>();

as the first statement in each of the ToyBox constructors. This ensures that the data fields in the base class are correctly initialized. Only the default constructor of derived-class can be called in this way. If we need control over setting base-class data fields, a derived-class constructor must call the appropriate base class methods, as shown in the ToyBox constructor. In this event, the base-class name indicator should precede the method name, so the compiler knows where to find the method's code. Using the namespace is necessary only within constructors, as you'll see when we implement the MagicBox.

A client of ToyBox class can create and use a ToyBox object in the way that we did for PlainBox:

```
string favoriteToy = "Jack-in-the-Box"
toyBox::string = myCase(favoriteToy, RED); // A red toy box
string oldToy = myCase.getItem(); // oldToy is a Jack-in-the-Box
favoriteToy = "Spinning Top";nmyCase.setItem(favoriteToy); // myCase now holds a Spinning Top
```

# C.1.42 Overriding Base-Class Methods

You can add any new members to a derived class as you like. Although you cannot revise a base-class private data fields and should not hide their names, you can redefine inherited methods; a method in a derived class is overrides, or redefines, a method in the base class if the two methods have the same name and parameter declarations—that is, if the same signature.

To see an example of when we need to redefine a base-class method, let's consider the implementation of the MagicBox. This box magically changes any item placed inside to a copy of the first item it ever had. A simple way to do this is to store only the first item. All calls to setItem will then do nothing; therefore, every get returns the first item in the box.

As with the toy box, we can derive our class from the PlainBox class, but also need a data field to indicate if an initial item has been stored in our box. We can use a boolean, firstItemStored, which is set to true once the first item has been stored in the box. We can then check this flag to see what setItem should do. If firstItemStored is false, we the argument passed to

![](bbox=[0.055, 0.055, 0.115, 0.945])