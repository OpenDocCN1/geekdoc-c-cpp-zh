# Chapter 10 Objects and Classes

# Classes and Structures

Class descriptions look much like visibility declarations with the addition of member functions and the public and private visibility labels. In fact, C++ extends to structures the same features classes have. The only difference is that the default access type for a struct is public, whereas the default type for a class is private. C++ programmers commonly use classes to implement class descriptions while restricting structures to representing pure data objects (often plain-old data structures, POD structures).

# Implementing Class Member Functions

We still have to create the second part of the class specification: providing code for those member functions represented by a prototype in the class declaration. Member function definitions are much like regular function definitions. Each has a function header and a function body. Member function definitions can return types and arguments. But they also have two special characteristics:

+   * When you define a member function, you use the scope-resolution operator (::) to identify the class to which the function belongs.
* Class methods can access the private components of the class.

Let's look at these now.
First, the header for a member function uses the scope-resolution operator (::) to indicate which class the function belongs. For example, the header for the update() member function looks like this:

```
void Stock::update(double price)
```

This notation means you are defining the update() function that is a member of the Stock class. Not only does this identify update() as a member function, but it means you can use the same name for a member function for a different class. For example, an update() function for a Buffon class would have this function header:

```
void Buffon::update()
```

Thus, the scope-resolution operator resolves the identity of the class to which a method definition applies. We say that the identifier update() has class scope. Other members of the Stock class can, if necessary, use the update() method without using the scope-resolution operator. That's because they belong to the same class, making update() in scope. Using update() outside the class declaration and method definitions, requires special measures, which we will get to soon.

One way of looking at method names is that the complete name of a class method includes the class name. Stock:update() is called the qualified name of the function. A simple update(), on the other hand, is an abbreviation (the unqualified name) for the full name—one that can be just in class scope.

The second special characteristic of methods is that a method can access the private members of a class. For example, the show() method can use code like: