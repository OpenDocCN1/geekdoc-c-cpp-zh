# *Resolving Ambiguity Issues That Arise When a Derived Class Inherits Member Functions of the Same Name from Multiple Base Classes*

Lines 22--25 output the contents of object derived again by using the `get` member functions of class Derived. However, there is an ambiguity problem, because this object contains two `getData` functions, one inherited from class Base1 and one inherited from class Base2. This problem is easy to solve by using the scope resolution operator. The expression `derived.Base1::getData()` gets the value of the variable inherited from class Base1 (i.e., the int variable named `value`) and `derived.Base2::getData()` gets the value of the variable inherited from class Base2 (i.e., the char variable named `letter`). The double value in real is printed without ambiguity with the call `derived.getReal()`—there are no other member functions with that name in the hierarchy.

# *Demonstrating the Is-A Relationships in Multiple Inheritance*

The is-a relationships of single inheritance also apply in multiple-inheritance relationships. To demonstrate this, line 29 assigns the address of object derived to the Base1 pointer `base1Ptr`. This is allowed because an object of class Derived is an object of class Base1. Line 30 invokes Base1 member function `getData` via `base1Ptr` to obtain the value of only the Base1 part of the object derived. Line 33 assigns the address of object derived to the Base2 pointer `base2Ptr`. This is allowed because an object of class Derived is an object of class Base2. Line 34 invokes Base2 member function `getData` via `base2Ptr` to obtain the value of only the Base2 part of the object derived.

# 24.8  Multiple Inheritance and `virtual` Base Classes

In Section 24.7, we discussed multiple inheritance, the process by which one class inherits from two or more classes. Multiple inheritance is used, for example, in the C++ standard library to form class `basic_iostream` (Fig. 24.12).

![](bbox=[0.299, 0.606, 0.713, 0.75])

**Fig. 24.12** | Multiple inheritance to form class `basic_iostream`.

Class `basic_ios` is the base class for both `basic_istream` and `basic_ostream`, each of which is formed using single inheritance. Class `basic_iostream` inherits from both `basic_istream` and `basic_ostream`. This enables class `basic_iostream` objects to provide the functionality of `basic_istreams` and `basic_ostreams`. In multiple-inheritance hierarchies, the situation described in Fig. 24.12 is referred to as diamond inheritance.

Because classes `basic_istream` and `basic_ostream` each inherit from `basic_ios`, a potential problem exists for `basic_iostream`. Class `basic_iostream` could contain two copies of the members of class `basic_ios`—one inherited via class `basic_istream` and one