Now you can modify all the dimensions of a Box object in a single statement:

```
```cpp
Box myBox{3.0, 4.0, 5.0};                 // Create a box
myBox.setLength(-20.0)->setWidth(40.0)->setHeight(10.0); // Set all dimensions of myBox
```
```

Because the mutator functions return the this pointer, you can use the value returned by one function to call the next. Thus, the pointer returned by setLength() is used to call setWidth(), which returns a pointer you can use to call setHeight(). Isn’t that nice?

Instead of a pointer, you can of course return a reference as well. The setLength() function, for instance, would then be defined as follows:

```
```cpp
Box& Box::setLength(double length)
{
    if (length > 0) m_length = length;
    return *this;
}
```
```

If you do the same for setWidth() and setHeight(), you obtain the Box class of Ex12_08. The sample program in Ex12_08.cpp then shows that returning references to *this allows you to chain member function calls together as follows:

```
```cpp
myBox.setLength(-20.0).setWidth(40.0).setHeight(10.0); // Set all dimensions of myBox
```
```

This pattern is called *method chaining*. If the goal is to facilitate statements that employ method chaining, it is commonly done using references. You will encounter several conventional examples of this pattern in the next chapter when we discuss operator overloading.

> **Tip**  Method chaining is not something you usually do for setters. Being able to set all member variables of an object in a single statement (instead of one statement per variable) is useful, but you already have a mechanism to initialize all the members at once: it’s called a constructor. If you combine constructors with the *assignment operator* you’ll learn about in the next chapter, you can write statements such as this:

```
```cpp
myBox = Box(-20.0, 40.0, 10.0); // Reinitialize a Box using constructor + assignment
```
```

Or, even shorter (the compiler will deduce which constructor to use here):

```
```cpp
myBox = {-20.0, 40.0, 10.0};
```
```

# ## const Objects and const Member Functions

A const variable is a variable whose value cannot be altered. You know this already. Naturally, you can also define const variables of class types. These variables are then called const objects. None of the member variables that constitute the state of a const object can be altered. In other words, any member variable of a const object is itself a constant and thus immutable.