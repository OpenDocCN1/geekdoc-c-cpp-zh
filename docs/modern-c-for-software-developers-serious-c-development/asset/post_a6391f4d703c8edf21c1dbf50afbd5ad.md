
# C++ Operators

Operators are symbols that denote operations on variables called operands. Familiar operators include: +, /, *, %. These are the arithmetic operators. We also have relational operators such as <, >, <=, >= and !=. All of these operators are binary operators since they require two operands. We also have unary operators such as ++, -- and so on. Unary operators need only one operand.

Operators work with native types such as int and float, for example. In C++ the semantics of operators are extended to apply to user-defined data types (classes). This is accomplished by operator overloading.

Operator overloading is closely related to function overloading. In C++, we can overload most operators so that they perform special relative to the class in which they are defined. For example, a class that maintains a stack might overload the '+' operator to perform a push operation and '-' to perform a pop. Ideally, when an operator is overloaded, none of its original meaning is lost. Instead, the type of objects to which it applies is expanded.

The ability to overload operators is one of C++’s most powerful features. It allows the full integration of new class types into the programming environment. After overloading the appropriate operators, we can use objects in expressions in the same way that we use these operators with the C++ built-in (native) data types.

We overload operators by creating class member operator functions. A member operator function defines the operation that the overloaded operator will perform relative to the class that it is member of.

An operator function is created by using the keyword operator. Operator functions can be either member functions of a class or free functions. Typically, free operator functions are friend functions of a class.

# Creating An Operator Member Function

A class member operator function has the following syntax:

```
return-type class-name::operator#(argument list)
{
    // program statements
}
```

The # is a placeholder for an operator such as +, -, *, /, >= and so forth. When we create an operator function, substitute such an operator for the #. For example, if we are overloading the division operator '/', the operator is operator/ (or operator /). If we are overloading the '+' operator, the operator function is operator+ (or operator +).

Operator functions typically return an object of the class that they are a member of, but the return type can be anything.

When we are overloading a unary operator, the member operator function's argument list will be empty. When we are overloading a binary operator, the argument list will contain one parameter (the other parameter is the class to which the operator belongs).

The following program declares a class called Location, which stores longitude and latitude values. This class overloads the addition operator +:

```cpp#include <iostream>
using namespace std;

class Location
{
    int longitude, latitude;
public:
    // constructors
    Location() {}
    Location(int lg, int lt)
{
  longitude = lg;
  latitude = lt;
    }

    void show() {
  cout << longitude << ":" << latitude << endl;
    }

    // operator+ declaration
    Location operator+(Location);
}

// definition of the overloaded operator +
Location::operator+(Location loc2) {
  Location temp;
  temp.longitude = loc2.longitude + latitude;
  temp.latitude = loc2.latitude + latitude;
  return temp;
}
```

```cpp
int main() {
  Location obj1(10, 20), obj2(5, 30);
  obj1.show(); // displays 10:20
  obj2.show(); // displays 5:30
  obj1 = obj1 + obj2;
  obj1.show(); // displays 15:50

  return 0;
}
```

```cpp
// output
10:20
5:30
15:50
```

Note that:

a + b = a.operator+(b)

It is common for an overloaded operator function to return an object of the class that it belongs to, for example:

```cpp
obj3 = obj1 + obj2;
```

Having the operator+ return an object of type Location makes it possible to write the following statement:

```cpp
(obj1+obj2).show();
```

It is important to understand that an operator function can return an object of any type and that the type returned depends solely upon our implementation.

The following example overloads the unary increment operator ++ for the Location class. This operator does not have any arguments:

```cpp
#include <iostream>
class Location {
public:
    int longitude, latitude;
    // constructor
    Location(int lng, int lat) {
        longitude = lng;
        latitude = lat;
    }
    // operator++ declaration
    Location operator++();
};

// Overloaded ++ operator for Location
Location Location::operator++() {
    longitude++;
    latitude++;
    return *this;
}

int main() {
    Location foo(100, 49);
    //foo.operator++()
    ++foo;
    std::cout << foo.longitude << ":" << foo.latitude << std::endl;
}
```

```cpp
// output
101:50
```

# Overloading The Shorthand Operators

We can overload any of the C++ "shorthand" operators, such as +=, -=, and the like.

# Operator Overloading Restrictions

The following restrictions apply to operator overloading:

- the precedence of an operator cannot be changed.
- we cannot change the number of operands that an operator takes.

# Operator Inheritance

When a class inherits from another class, some of the members of the base class become members of the derived class.

When the access mode for a base class is public, all of the public members of the base class become public members of the derived class, and all the protected members of the base class become protected members of the derived class.

When a base class is inherited through private access mode, all of the public and protected members of the base class become private members of the derived class.

# C++ Class Inheritance

Inheritance enables the creation of hierarchical classifications. For example, we can create a general class that defines some basic traits. This class can then be inherited by other, more specific classes, each adding only those attributes that are unique to the inheriting class.

A class that is inherited is called a base class. A class that inherits from a base class is called a derived class.

# Base Class Access Control

When a class inherits from another class, some of the members of the base class become members of the derived class. Class inheritance uses this syntax:

```cpp
class derived-class-name : access_mode base-class-name {
  // body of derived class
};
```

The access mode keyword determines which attributes of the base class are inherited. The access mode must be either public, private, or protected. If no access mode is specified, it is private by default if the derived class is a class. If the derived class is a struct, then the default access mode is public.

# Operator Overloading Using a Friend Function

We can overload an operator using a non-member friend function. Since a friend function is not a member of the class, it does not have this pointer.

Note that a binary operator using a friend function must have two parameters, and a unary operator using a friend function must have one parameter.

Note that: a + b is the same operator+(a, b)

The following program defines a friend function for the addition operator:

```cpp
// Use friend function
#include <iostream>
class Location
{
    int longitude, latitude;
public:
    // constructors
    Location() {}
    Location(int lg, int lt)
{
  longitude = lg;
  latitude = lt;
    }

    void show() {
  std::cout << longitude << ":" << latitude << "\n";
    }

    // operator+ declaration
    friend Location operator+(Location);
};

// operator+ is overloaded using a friend function.
Location operator+(Location op1, Location op2) {
    Location temp;
    temp.longitude = op1.longitude + op2.longitude;
    temp.latitude = op1.latitude + op2.latitude;
    return temp;
}

int main() {
    Location obj1(10, 20), obj2(5, 30);
    obj1 = obj1 + obj2;
    obj1.show();
    return 0;
}

// output
15 50
```

Some restrictions apply to friend functions:

- the =, [], or -> operators cannot be overloaded by a friend function.
- when overloading the increment or decrement operators with a friend function, we must use reference parameters.
