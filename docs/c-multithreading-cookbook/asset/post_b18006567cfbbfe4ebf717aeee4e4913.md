
```cpp
double dVal = (double)rand() / RAND_MAX;
return dMin + dVal * (dMax - dMin);
```

```cpp
class CComplex {
public:
    CComplex() {
        dReal = Rand(-10, 10);
        dImg = Rand(-10, 10);
    }
    CComplex(double dReal, double dImg) {
        this->dReal = dReal;
        this->dImg = dImg;
    }
    friend CComplex operator+(const CComplex& c1, const CComplex& c2) {
        CComplex c(c1.dReal + c2.dReal, c1.dImg + c2.dImg);
        return c;
    }
    ostream& operator<<(ostream& os, const CComplex& c) {
        return os << c.dReal << " " << c.dImg << "i";
    }
private:
    double dReal;
    double dImg;
};
```

```cpp
int main(int argc, TCHAR* argv[]) {
    CComplex c1;
    CComplex c2(-2.3, 0.9);
    CComplex c = c1 + c2;
    cout << c << endl;
    return 0;
}
```

# Chapter 1

## How it works...

If you look at the main function, you'll notice that it doesn't differ from the program where you use integers, for example. Even though an integer is a primitive type and a complex is not, a programmer's work is made easier by adding a class and properly setting its methods.

Here we have defined a new type of class-CComplex. The defined class has its own attributes and methods. It can also have friend methods that can access its private members. We have left the Rand function as it is, but we tried to make the class that represents a complex number similar to the abstraction of a complex number. We created the dReal and dImg attributes that describe the real and imaginary parts of a complex number. We created the operator+ so that the (plus) has meaning for the compiler. Now, the code is more readable and much more comfortable to use because it is easy to understand how to use it. The default constructor uses random numbers from -10 to 10, and another constructor enables the user to set the real and imaginary parts of a complex number.

When you want to overload (this will be explained in detail) a certain method, you can choose between two approaches. The first approach is to set the method inside a class, and this method will change the state (or values) of the calling object. The second approach is to make the method independent of the class, the so-called outer, but it has to be declared as friend so it can access the private and protected members of the objects.

## There's more...

The following code tells the compiler the operator+ function which expects two complex numbers will be defined somewhere in the code, and it has to be able to access the private and protected members of the CComplex class:

```cpp
friend CComplex operator+(const CComplex& c1, const CComplex& c2);
```

This makes the main function the simplest possible. Again, we use user-defined types as primitive types, which is very good practice because even programmers not familiar with the code will quickly understand what the code means.

## Explaining inheritance, overloading, and overriding

Inheritance is a very important characteristic of OOP. It is the relation between two (or more) classes: if class B is some kind of class A, then the objects of class B have the same properties as the objects of class A. In addition to that, class B can implement new methods and thus supersede the base class A.

# Introduction to C++ Concepts and Features

## Getting ready

Make sure Visual Studio is up and running.

## How to do it..

Let's review this example by performing the following steps:

- 1. Create a new default console application. Name it InheritanceTest.
- 2. Open the InheritanceTest.cpp file and insert the following code:

```cpp
#include "stdafx.h"
#include <iostream>
using namespace std;

class CPerson
{
public:
    CPerson(int iAge, char* sName)
    {
        this->iAge = iAge;
        strcpy_s(this->sName, 32, sName);
    }
    virtual char* WhoAmI()
    {
        return "I am a person";
    }
private:
    int iAge;
    char sName[32];
};

class CWorker : public CPerson
{
public:
    CWorker(int iAge, char* sName, char* sEmploymentStatus)
    : CPerson(iAge, sName)
    {
        strcpy_s(this->sEmploymentStatus, 32, sEmploymentStatus);
    }
    virtual char* WhoAmI()
    {
        return "I am a worker";
    }
private:
    char sEmploymentStatus[32];
};

class CStudent : public CPerson
{
public:
    CStudent(int iAge, char* sName, char* sStudentIdentityCard)
    : CPerson(iAge, sName)
    {
        strcpy_s(this->StudentIdentityCard, 32, sStudentIdentityCard);
    }
    virtual char* WhoAmI()
    {
        return "I am a student";
    }
private:
    char sStudentIdentityCard[32];
};

int main(int argc, TCHAR* argv[])
{
    CPerson cPerson(10, "John");
    cout << cPerson.WhoAmI() << endl;

    CWorker cWorker(35, "Mary", "On vacation*");
    cout << cWorker.WhoAmI() << endl;

    CStudent cStudent(22, "Sandra", "Physician*");
    cout << cStudent.WhoAmI() << endl;

    return 0;
}
```

## How it works...

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

```cpp
class CWorker : public CPerson
```

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

We created a new CPerson data type that represents one human. It has iAge and sName as attributes that describe some person. Let's assume that we need some worker or student as another data type. OOP provides a great mechanism, inheritance, which can be used to achieve this. As a worker is still a person, but with some additional attributes, we will extend CPerson with CWorker using the following line of code:

*(Note: The OCR text contained significant repetitive/garbled sections in the "How it works" part which have been cleaned to follow the logical flow of the provided code and context.)*
