
```cpp
public:
void setFeet(int x) {
    iFeet=x;
}
int getFeet() {
    return iFeet;
}
void setInches(float y) {
    fInches=y;
}
float getInches() {
    return fInches;
}
```

can also be written as

```cpp
struct Distance {
    void setFeet(int x) //public by default
    iFeet=x;
    int getFeet() //public by default
    return iFeet;
    void setInches(float y) //public by default
    fInches=y;
    float getInches() //public by default
    return fInches;
}
private:
    int iFeet;
    float finches;
```

In Listing 2.4, the member functions have not been placed under any access modifier. Therefore, there are public members by default.
On the other hand, class members are private by default. This is the only difference between the class keyword and the struct keyword.
Thus, the structure Distance can be redefined by using the class keyword as shown in Listing 2.5.

### Listing 2.5 Class members are private by default

```cpp
class Distance {
    int iFeet; //private by default
    float finches; //private by default
    public:
    void setFeet(int x) {
        iFeet=x;
    }
    int getFeet() {
        return iFeet;
    }
    void setInches(float y) {
        fInches=y;
    }
    float getInches() {
        return finches;
    }
};
```

The struct keyword has been retained to maintain backward compatibility with C language. A header file created in C might contain the definition of a structure, and structures in C will have member data only. The definition of struct keyword now mandates the inclusion of member functions. Functions in C source code access member data of structures. A C++ compiler will easily compile such source code since the C++ compiler treats members of structures as public members by default.

## 2.1.2 Objects

Variables of classes are known as objects. An object of a class occupies the same amount of memory as a variable of a structure with identical data members. This is illustrated by Listing 2.6.

### Listing 2.6 Size of a class is equal to that of a structure with identical data members

| struct A | class B |
| :--- | :--- |
| char a; | char a; |
| int b; | int b; |
| float c; | float c; |

```cpp
/*Beginning of objectSize.cpp*/
#include <iostream>
struct A {
    char a;
    int b;
    float c;
};
class B {
    char a;
    int b;
    float c;
}
void main() {
    cout << sizeof(A) << endl << sizeof(B) << endl;
}
/*End of objectSize.cpp*/
```

# Output
9
9

Introducing member functions do not influence the size of objects. The reason for this will become apparent when we study this. Moreover, making data members private or public does not influence the size of objects. The access modifiers merely control the accessibility of the members.

## 2.1.3 Scope Resolution Operator

It is possible and usually necessary for the library programmer to define the member functions outside their respective classes. The scope resolution operator makes this possible. Listing 2.7 illustrates the use of the scope resolution operator.

### Listing 2.7 The scope resolution operator

```cpp
/*Beginning of scopeResolution.cpp*/
class Distance {
    int iFeet;
    float finches;
public:
    void setFeet(int);          //prototype only
    int getFoot();              //prototype only
    void setInches(float);      //prototype only
    float getInches();          //prototype only
};

void Distance::setFeet(int x) {
    iFeet=x;
}
int Distance::getFoot() {
    return iFeet;
}
void Distance::setInches(float y) {
    finches=y;
}
float Distance::getInches() {
    return finches;
}
/*End of scopeResolution.cpp*/
```

We can observe that the member functions have been only prototyped within the class; they have been defined outside. The scope resolution operator signifies the class to which they belong. The class name is specified on the left-hand side of the scope resolution operator. The name of the function being defined is on the right-hand side.

## 2.1.4 Creating Libraries Using the Scope Resolution Operator

As in C language, creating a new data type in C++ using classes is also a three-step process that is executed by the library programmer.

- Step 1: Place the class definition in a header file.

```cpp
/*Beginning of Distance.h*/
/*Header file containing the definition of the Distance class*/
class Distance {
    int feet;
    float finches;
public:
    void setFeet(int); // prototype only
    int getFeet(); // prototype only
    void setInches(float); // prototype only
    float getInches(); // prototype only
};
/*End of Distance.h*/
```

- Step 2: Place the definitions of the member functions in a C++ source file (the library source code). A file that contains definitions of the member functions of a class is known as the implementation file of that class. Compile this implementation file and put in a library.

```cpp
/*Beginning of Distlib.cpp*/
/*Implementation file for the class definition*/
#include "Distance.h"
void Distance::setFeet(int x) //definition {
    feet=x;
}
int Distance::getFeet() //definition {
    return feet;
}
void Distance::setInches(float y) //definition {
    finches=y;
}
float Distance::getInches() //definition {
    return finches;
}
/*End of Distlib.cpp*/
```

- Step 3: Provide the header file and the library, in whatever media, to other programmers who want to use this new data type.

## 2.1.5 Using Classes in Application Programs

The steps followed by programmers for using this new data type are:

- Step 1: Include the header file provided by the library programmer in their source code.

```cpp
/*Beginning of Distmain.cpp*/
#include "Distance.h"
void main() {
// ...
}
```

- Step 2: Declare variables of the new data type in their source code.

```cpp
/*Beginning of Distmain.cpp*/
#include "Distance.h"
void main() {
// ...
}
```

- Step 3: Embed calls to the associated functions by passing these in their source code. See Listing 2.8.

### Listing 2.8 Using classes application programs

```cpp
/*Beginning of Distmain.cpp*/
/*A sample driver program for creating and using objects*/
#include <iostream>
#include "Distance.h"
void main() {
    Distance d1, d2;
    d1.setFeet(2);
    d1.setInches(2.2);
    d2.setFeet(3);
    d2.setInches(3.3);
    cout << d1.getFeet() << endl;
    cout << d2.getFeet() << endl;
}
/*End of Distmain.cpp*/
```

- Step 4: Compile the source code to get the object file.

- Step 5: Link the object file with the library provided by the library programmer to get the executable or another library.

# Output of Listing 2.8
2 2.2
3 3.3

## 40 Object-Oriented Programming with C++

Implementation files are compiled and converted into static and dynamic libraries in the usual manner.
Again, we notice that there is no obvious connection between the member data being accessed within the member function and the object that is invoking it.

## 2.1.6 this Pointer

The facility to create and call member functions of class objects is provided by the C++ compiler. You have already seen how this facility is to used. However, how does the compiler support this facility? The compiler does this using a unique pointer known as this pointer. A thorough understanding of this pointer is vital for understanding many concepts in C++.
This pointer is always a constant pointer. This pointer points at the object with respect to which the function was called. An explanation that follows shortly why and how it functions.
After the compiler has ascertained that no attempt has been made to access the private members of an object by non-member functions, it converts the C++ code into an ordinary C language code as:

1. It converts the class into a structure with only data members as follows.

Before
```cpp
class Distance {
    int iFeet;
    float finches;
};
```

After
```cpp
struct Distance {
    int iFeet;
    float finches;
}
```

2. It puts a declaration of the this pointer as a leading formal argument in the prototypes of all member functions as follows.

Before
```cpp
void setFeet(int);
```

After
```cpp
void setFeet(Distance * const, int);
```

Before
```cpp
int getFeet();
```
