
class, the TrafficSignalAlt class has no default constructor. Recall from Section 14.4 that a default constructor accepts no arguments, and that if a programmer provides any constructor for a class, the compiler will not automatically provide a default constructor. This means the client cannot write code such as

```
TrafficSignal light;
```

or

```
TrafficSignalAlt light2;
```

During the object's creation the client *must* provide an integer argument representing a traffic light color. If RED, GREEN, and YELLOW are constant instance variables (that is, constant non-`static` fields), every `TrafficSignalAlt` object has its own copy of the fields, and the RED, GREEN, and YELLOW fields cannot exist outside of any traffic light object. This leads to a chicken-and-egg problem—how can we create the first `TrafficSignalAlt` object using the symbolic constants RED, GREEN, or YELLOW? These constants do not exist unless we have a traffic light object, yet we need a traffic light object to have any of these constants!

An executing program initializes `static` class fields before it invokes the `main` function. This means any data pertaining to a class that must exist before any object of that class is created must be declared `static`. A `static` class variable exists outside of any instance of its class.

C++ allows methods to be declared `static`. A `static` method executes on behalf of the class, not an instance of the class. This means that a `static` method may not access any instance variables (that is non-`static` fields) of the class, nor may they call other non-`static` methods. Since a `static` method executes on behalf of the class, it has no access to the fields of any particular instance of that class. That explains the restriction against `static` methods accessing non-`static` data members. Since a non-`static` method may access instance variables of an object upon which it is called, a `static` method may not call a non-`static` method and thus indirectly have access to instance variables. The restriction goes only one way—any class method, `static` or non-`static`, may access a `static` data member or call a `static` method.

Looking at it from a different perspective, all non-`static` methods have the `this` implicit parameter (Section 15.3). No `static` method has the `this` parameter. This means it is a compile-time error to use `this` within a `static` method.

## 15.9 Classes vs. structs

All members of a C++ class are `private` by default. The class

```
class Point {
public:
    double x;
    double y;
};
```

must use the `public` label so clients can access a `Point` object's fields. The `struct` keyword is exactly like the `class` keyword, except that the default access to members is `public`:

```
struct Point {
    double x;    // These fields now are public
    double y;
};
```

The C language supports the struct feature, but not the class keyword. C structs do not support methods and constructors. In C++ (unlike in C), a struct can contain methods and constructors. By default, members in structs are public, but you can apply the private and public labels as in a class to fine tune client access.

Despite their similarities, C++ programmers favor classes over structs for programmer-defined types with methods. The struct construct is useful for declaring simple composite data types that are meant to be treated like primitive types. Consider the int type, for example. We can manipulate directly integers, and integers do not have methods or any hidden parts. Likewise, a geometric point object consists of two coordinates that can assume any valid floating-point values. It makes sense to allow client code to manipulate directly the coordinates, rather than forcing clients to use methods like set_x and set_y. On the other hand, it is unwise to allow clients to modify directly the denominator of a Rational object, since a fraction with a zero denominator is undefined.

> In C++, by default everything in an object defined by a struct is accessible to clients that use that object. In contrast, clients have no default access to the internals of an object that is an instance of a class. The default member access for struct instances is public, and the default member access for class instances is private.

The struct feature is, in some sense, redundant. It is a carryover from the C programming language. By retaining the struct keyword, however, C++ programs can use C libraries that use C structs. Any C++ program that expects to utilize a C library using a struct must restrict its struct definitions to the limited form supported by C. Such struct definitions may not contain non-public members, methods, constructors, etc.

## 15.10 Friends

The private members of a class by default are inaccessible to code outside of that class. Ordinarily only methods within the class itself have permission to see and modify the private instance variables and invoke the private methods within that class. This access protection allows programmers to modify the implementation of the hidden internals of a class without affecting existing client code that uses the class.

For some class designs this all-or-nothing access dictated by the public and private labels within a class or struct is too limiting. At times it can be advantageous to design a class that grants special access to some precisely specified functions or classes of objects outside of the class.

As an example, consider a variation of the SimpleRational class from Listing 14.5 (simplerational.cpp). Our new class, named OpaqueRational is shown here:

```
// Models a mathematical rational number
class OpaqueRational {
int numerator;
int denominator;
public:
// Initializes the components of an OpaqueRational object
OpaqueRational(int n, int d): numerator(n), denominator(d) {
    if (d == 0) {
        // Display error message
        std::cout << "Zero denominator error\n";
        exit(1); // Exit the program
    }
}

// The default constructor makes a zero rational number
// 0/1
OpaqueRational() : OpaqueRational(0, 1) {}
};
```

Note that clients can make an OpaqueRational object, but after its creation clients can neither see nor change the internals of the object. Gone are the set_numerator, set_denominator, get_numerator, and get_denominator methods of the SimpleRational class.

We would like to be able to print an OpaqueRational object as easily as the following:

```
OpaqueRational frac(1, 2); // Make the fraction 1/2
std::cout << frac << '\n';
```

We would like the std::cout statement to print the text

![](img/e84ad11adb18201d71595b31ce6c9eff_477_0.png)

This would require an operator<< function overloaded to accept a OpaqueRational object, and this operator<< function would need to be able to access the private instance variables of the OpaqueRational object.

A class can grant access to an outside function or another class via the friend reserved word. In Listing 15.13 (printonlyrational.cpp) we specify a friend function that allows clients to display in human-readable form an opaque rational number object via operator<< with an output stream object.

### Listing 15.13: printonlyrational.cpp

```
#include <iostream>
#include <cstdlib>
// Models a mathematical rational number
class PrintOnlyRational {
  int numerator;
  int denominator;
public:
  // Initializes the components of an PrintOnlyRational object
  PrintOnlyRational(int n, int d): numerator(n), denominator(d) {
    if (d == 0) {
      // Display error message
      std::cout << "Zero denominator error\n";
      exit(1); // Exit the program
    }
  }
  // The default constructor makes a zero rational number
  // 0/1
  PrintOnlyRational(): PrintOnlyRational(0, 1) {}
// This operator can access the internal details of an
// object of this class.
friend std::ostream& operator<<(std::ostream& os,
                                const PrintOnlyRational& f);
};

std::ostream& operator<<(std::ostream& os, const PrintOnlyRational& f) {
    os << f.numerator << '/' << f.denominator;
    return os;
}

int main() {
    PrintOnlyRational fract1{ 2 }; // The fraction 1/2
    std::cout << "The fraction is " << fract << '\n';
    PrintOnlyRational fract2{ 2, 3 }; // The fraction 2/3
    std::cout << "The fraction is " << fract2 << '\n';
}
```

Listing 15.13 (printonlyrational.cpp) prints the following:

```
The fraction is 1/2
The fraction is 2/3
```

Observe that the `operator<<` function is not a member function of the `PrintOnlyRational` class. Ordinarily `operator<<` would be unable to access the numerator and denominator fields of a `PrintOnlyRational` object. We can see, however, that the compiler allows the `operator<<` function to access the private instance variables of its `f` parameter.

We chose in Listing 15.13 (printonlyrational.cpp) to implement the `operator<<` function outside of the `PrintOnlyRational` class; however, we just as well could have implemented it inline within the body of the class, as shown here:

```
class PrintOnlyRational {
    // Other details about the private members of the class omitted here . . .
public:
    // Other details about the public members of the class omitted here . . .
    friend std::ostream& operator<<(std::ostream& os,
                                    const PrintOnlyRational& f) {
        os << f.numerator << '/' << f.denominator;
        return os;
    }
};
```

Implementing `operator<<` inline in this way makes it look very much like an inline method implementation, but it is not a member function. The reserved word `friend` at the front indicates to the compiler that it is indeed a free function; C++ does not allow member functions to be declared as friends.

Listing 15.14 (friendclass.cpp) provides an example of a friend class.

```
Listing 15.14: friendclass.cpp
#include <iostream>
```
