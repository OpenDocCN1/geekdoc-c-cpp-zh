```
{
  PlainBox<ItemType>();
  setItem(theItem);
  boxColor = theColor;
} // end constructor

template<class ItemType>
Color ToyBox<ItemType>::getColor() const
{
  return boxColor;
} // end getColor
```

Inheritance enables you to reuse software components when you define a new class. Our ToyBox class does not inherit the constructors from PlainBox, but it can use a PlainBox constructor or method to initialize the private data field in PlainBox. To use the default constructor of our base class, we place the statement

```
PlainBox<ItemType>();
```

as the first statement in each of the ToyBox constructors. This ensures that the data fields in the base class are correctly initialized. Only the default constructor can be called in this way. If we need more control over setting base-class data fields, a derived-class constructor must call the appropriate base-class mutation methods, as shown in the third ToyBox constructor. In this event, the base-class name-space indicator should precede the method name, so the compiler knows where to find the method's definition. Using the namespace indicator is necessary only within constructors, as you'll see when we implement the MagicBox class.

A client of our ToyBox class can create and use a ToyBox object in much the same way that we did for PlainBox:

```
string favoriteToy = "Jack-in-the-Box";
ToyBox<string> myToyCase(favoriteToy, RED); // A red toy box
string oldToy = myToyCase.getItem(); // oldToy is a Jack-in-the-Box
favoriteToy = "Spinning Top";
myToyCase.setItem(favoriteToy); // myToyCase now holds a Spinning Top
```

# C1.4.2 Overriding Base-Class Methods

You can add as many new members to a derived class as you like. Although you cannot revise a base class's private data fields and should not revise their names, you can redefine inherited methods; this is called overriding a base-class method. A method in a derived class overrides, or redefines, a method in the base class if the two methods have the same name and parameter declarations—that is, if they have the same signatures.

To see an example of when we may need to redefine a base-class method, let's consider the implementation of the class MagicBox. This box magically changes any item placed inside to a copy of the first item it ever held. A simple way to do this is to store only the first item. Future calls to setItem will do nothing. Therefore, every call to getItem returns the first item stored in the box.

As with the toy box, we can derive our class from the PlainBox class, but we also need a data field to indicate if an initial item has been stored in our box. We can use a boolean field, firstItemStored, which is set to true once the first item has been stored in the box. We can then check this flag to see what setItem should do. If firstItemStored is false, we know that the argument passed to