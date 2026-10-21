# Chapter 10

# Run-time Polymorphism by Virtual Functions

# Learning Objectives

+   - Polymorphism and its importance
+   - Difference between compile time and run-time polymorphism
+   - Pointer to objects
+   - Pointer to invoking object, the this pointer
+   - Defining a base class pointer and making it point to derived class objects
+   - Virtual functions
+   - Invoking virtual function statically
+   - Issue of passing default arguments to virtual functions
+   - Virtual destructors
+   - Pure virtual functions

# 10.1 INTRODUCTION

Polymorphism is the property of the same object to behave differently in different contexts given the same message. We have seen that overloaded functions and operators exhibit this property. Suppose there is a class of complex number and the ‘+’ operator has been overloaded for adding two complex numbers as well as a complex number with a normal number. Now, suppose the function Sum() is also defined to perform the same operations.

Look at the following statements:

```
Complex C1, C2, C3;
int i;
C3 = C1.Sum(i);
C3 = C1.Sum(C2);
C3 = C1 + i;
C3 = C1 + C2;
```

In all these cases, the object C3 behaves differently (i.e., calls different functions) when given the same message, that is, either Sum or +, depending on the context (the argument passed). Note that this type of polymorphism is decided at compile time, that is, C++ decides what to do at compile time. This is an important property of an object-oriented (OO) language, and it needs to be extended at run-time.

Suppose there is an abstract base class Vehicle that stores the data and functions common to three other derived classes, namely Car, Bus, and Scooter. Examples of such information are the registration number of the vehicle, date of manufacturing, dealer identity, date of sale, etc. Such information is stored in the Vehicle class because otherwise it needs to be stored in every class derived from the base class. The same issue also arises for the functions. There are two choices, namely, defining it in the base class alone or defining it in every class derived from the base class. Unlike