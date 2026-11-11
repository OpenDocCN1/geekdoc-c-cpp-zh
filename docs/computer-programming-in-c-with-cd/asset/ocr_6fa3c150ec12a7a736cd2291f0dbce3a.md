```
```cpp
num1 = 1
num2 = 5

object no.2
num1 = 2
num2 = 10

object no.3
num1 = 3
num2 = 15

object no.4
num1 = 4
num2 = 20
```
```

In Listing 32, the ABC class is created, which has one private member, num1, and three public members, num2, setValue(), and displayValue(). The setValue() and displayValue() functions are defined outside the ABC class by using the :: operator. In the main() function, obj is an array of objects, while ptr is an array of pointer objects of the ABC class. In the for loop, the reference of the obj object array is assigned as the value of each element of the ptr object array. The -> operator is used to access the displayValue() function of the ABC class.

# Creating Pointer Objects of the Base and Derived Classes

In C++, a pointer to a base class can point to an object of any of the derived classes. The following code snippet shows how a base class can point to a derived class object:

```
```cpp
A *PtrObj;
PtrObj = & B;
PtrObj = & C;
```
```

In the preceding code snippet, A represents a base class, while B and C are derived from this base class. PtrObj is a pointer object of the class A that is initialized with the references of the B and C classes.

Listing 33 shows how to create and use pointer objects of the base and derived classes (you can find the PointerDerivedObjects.cpp file on the CD in the Code\Chapter7 folder):

# Listing 33: Creating and Using Pointer Objects of the Base and Derived Classes

```
```cpp
#include<iostream.h>
class ABC
{
int num1;
//private data member
public:
int num2;
//public data member
void setValue(int);
```
```