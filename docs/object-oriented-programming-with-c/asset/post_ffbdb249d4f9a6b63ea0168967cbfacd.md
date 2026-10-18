
```cpp
constructor (arglist) : initialization-section
{ assignment-section
}
```

The _assignment-section_ is nothing but the body of the constructor function and is used to assign initial values to its data members. The part immediately following the colon is known as the _initialization section_. We can use this section to provide initial values to the base constructors and also to initialize its own class members. This means that we can use either of the sections to initialize the data members of the constructor's class. The initialization section basically contains a list of initializations separated by commas. This list is known as _initialization list_. Consider a simple example:

```cpp
class XYZ
{
int a;
int b;
public:
XYZ(int i, int j) : a(i), b(2 * j) { }
};
main()
{
XYZ x(2, 3);
}
```

This program will initialize **a** to 2 and **b** to 6. Note how the data members are initialized, just by using the variable name followed by the initialization value enclosed in the parenthesis (like a function call). Any of the parameters of the argument list may be used as the initialization value and the items in the list may be in any order. For example, the constructor **XYZ** may also be written as:

```cpp
XYZ(int i, int j) : b(i), a(i + j) { }
```

In this case, **a** will be initialized to 5 and **b** to 2. Remember, the data members are initialized in the order of declaration, independent of the order in the initialization list. This enables us to have statements such as

```cpp
XYZ(int i, int j) : a(i), b(a * j) { }
```

Here a is initialized to 2 and b to 6. Remember, a which has been declared first is initialized first and then its value is used to initialize b. However, the following will not work:

```cpp
XYZ(int i, int j) : b(i), a(b * j) { }
```

because the value of b is not available to a which is to be initialized first.

The following statements are also valid:

```cpp
XYZ(int i, int j) : a(i) { b = j; }
XYZ(int i, int j) { a = i; b = j; }
```

We can omit either section, if it is not needed. Program 8.8 illustrates the use of initialization lists in the base and derived constructors.

## Program 8.8 Initialization List in Constructors

```cpp
#include <iostream>
using namespace std;
class alpha
{
int x;
public:
alpha(int i)
{
x = i;
cout << "\n alpha constructed";

g.show_beta();
g.show_gamma();
return 0;
};
```

The output of Program 8.8 would be:

```
beta constructed
alpha constructed
gamma constructed
Display member values
x = 4
p = 2.5
q = 5
u = 2
v = 4
```

> **NOTE:** *The argument list of the derived constructor **gamma** contains only three parameters **a**, **b** and **c** which are used to initialize the five data members contained in all the three classes.*

## 8.12 Member Classes: Nesting of Classes

Inheritance is the mechanism of deriving certain properties of one class into another. We have seen in detail how this is implemented using the concept of derived classes. C++ supports yet another way of inheriting properties of one class into another. This approach takes a view that an object can be a collection of many other objects. That is, a class can contain objects of other classes as its members as shown below:

```cpp
class alpha {...};
class beta {...};
```

```cpp
class gamma
{
alpha a; // a is an object of alpha class
beta b; // b is an object of beta class
....
};
```

All objects of **gamma** class will contain the objects **a** and **b**. This kind of relationship is called *containership* or *nesting*. Creation of an object that contains another object is very different than the creation of an independent object. An independent object is created by its constructor when it is declared with arguments. On the other hand, a nested object is created in two stages. First, the member objects are created using their respective constructors and then the other members are created. This means, constructors of all the member objects should be called before its own constructor body is executed. This is accomplished using an initialization list in the constructor of the nested class.

Example:

```cpp
class gamma
{
....
alpha a; // a is object of alpha
beta b; // b is object of beta
public:
gamma(arglist): a(arglist1), b(arglist2)
{
// constructor body
}
};
```

*arglist* is the list of arguments that is to be supplied when a **gamma** object is defined. These parameters are used for initializing the members of **gamma**. *arglist1* is the argument list for the constructor of **a** and *arglist2* is the argument list for the constructor of **b**. *arglist1* and *arglist2* may or may not use the arguments from *arglist*.

Remember, _a_(_arglist1_) and _b_(_arglist2_) are function calls and therefore the arguments do not contain the data types. They are simply variables or constants.

```cpp
gamma(int x, int y, float z) : a(x), b(x,z)
{
Assignment section (for ordinary other members)
}
```

We can use as many member objects as are required in a class. For each member object we add a constructor call in the initializer list. The constructors of the member objects are called in the order in which they are declared in the nested class.

## Summary

- The mechanism of deriving a new class from an old class is called inheritance. Inheritance provides the concept of reusability. The C++ classes can be reused using inheritance.
- The derived class inherits some or all of the properties of the base class.
- A derived class with only one base class is called single inheritance.
- A class can inherit properties from more than one class which is known as multiple inheritance.
- A class can be derived from another derived class which is known as multilevel inheritance.
- When the properties of one class are inherited by more than one class, it is called hierarchical inheritance.
- A private member of a class cannot be inherited either in public mode or in private mode.
- A protected member inherited in public mode becomes protected, whereas inherited in private mode becomes private in the derived class.
- A public member inherited in public mode becomes public, whereas inherited in private mode becomes private in the derived class.
- The friend functions and the member functions of a friend class can directly access the private and protected data.
- The member functions of a derived class can directly access only the protected and public data. However, they can access the private data through the member functions of the base class.
- Multipath inheritance may lead to duplication of inherited members from a ‘grandparent’ base class. This may be avoided by making the common base class a virtual base class.
- In multiple inheritance, the base classes are constructed in the order in which they appear in the declaration of the derived class.
- In multilevel inheritance, the constructors are executed in the order of inheritance.
- A class can contain objects of other classes. This is known as containership or nesting.

## Key Terms

- abstract class
- access control
- access mechanism
- ancestor class
- assignment section
- base class
- base constructor
- child class
- common base class
- containership
- derivation
- derived class
- derived constructor
- direct base class
- dot operator
- duplicate members
- father class
- **friend**
- grandfather class
- grandparent class
- hierarchical inheritance
- hybrid inheritance
- indirect base class
- inheritance
- inheritance path
- initialization list
- initialization section
- intermediate base
- member classes
- multilevel inheritance
- multiple inheritance
- nesting
- **private**
- private derivation
- private members
- privately derived
- **protected**
- protected members
- **public**
- public derivation
- public members
- publicly derived
- reusability
- single inheritance
- subclass
- virtual base class
- visibility mode
- visibility modifier

## Review Questions

- 8.1 What does inheritance mean in C++?
- 8.2 What are the different forms of inheritance? Give an example for each.
- 8.3 Describe the syntax of the single inheritance in C++.
- 8.4 We know that a private member of a base class is not inheritable. Is it anyway possible for the objects of a derived class to access the private members of the base class? If yes, how? Remember, the base class cannot be modified.
- 8.5 How do the properties of the following two derived classes differ?

  - (a) `class D1: private B{//...};`
  - (b) `class D2: public B{//....};`

- 8.6 When do we use the protected visibility specifier to a class member?
