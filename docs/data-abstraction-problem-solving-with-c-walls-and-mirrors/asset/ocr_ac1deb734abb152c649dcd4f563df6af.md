```
item = theItem;
} // end getItem
ItemType PlainBox::getItem() const
{
    return item;
}// end getItem
```

The header file PlainBox.h contains our class declaration. We must use the preprocessor directive #include to include the PlainBox class declaration so the compiler can validate our method headers and provide access to data fields. The method headers must match those provided in the class declaration. Including the header file does not tell the compiler that the methods defined here are part of the PlainBox class. To do so, you must precede the constructor and method names with the class name followed by ::.

PlainBox::

The reason for this requirement is C++ allows a source file to contain the implementations of methods for several classes and stand-alone functions. The namespace indicator PlainBox:: is a prefix that tells the compiler that the method is part of the PlainBox namespace. A C++ namespace is a syntax structure, which as allows you to group declarations of data and methods under a common name, such as PlainBox. Once a method has been defined as part of a namespace, it has access to all the data and methods in that namespace. Thus, the constructor in Listing C1-2 have access to PlainBox's data fields and methods.

> Note: To modernize our code, the implementation files in this book will contain only methods from a single module.

# C1.3 Templates

At this point, our PlainBox class looks similar to many of the classes you probably have implemented in a previous C++ course. The class works well, as long as the characters in the game want to store a double value in a box. But what do we do if one wants to store a double and a second has a string or MagicObject instead? Since our current PlainBox class can only store a double, we would need to create new classes—PlainBoxStrings and PlainBoxForwards, for example—to hold different object types. These classes would function in exactly the same way as the PlainBox class, so we could copy the code with only a few changes. For each header file. For the PlainBoxForStrings class, the typedef would be

```
typedef string ItemType;
and for the PlainBoxForwards class, the typedef would be
```

```
typedef MagicWand ItemType;
```

We would also need to change the names of the constructors and the namespace indicators to reflect the new class names. If we had a more complex class, these changes would require a substantial amount of effort and would be an error-prone process. Later, if our friend changed the